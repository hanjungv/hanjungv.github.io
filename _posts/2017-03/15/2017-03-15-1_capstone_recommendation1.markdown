---

layout: post
title: "(캡스톤) Recommendation Systems"
category: CAPSTONE

---

# 스탠퍼드 mining massive datasets 교육자료
* [자료 링크](http://infolab.stanford.edu/~ullman/mmds/ch9.pdf)
* 개인적인 기준으로 정리, 해석이 올바르지 않을 수도 있습니다.
* 왜 읽나요? 캡스톤 주제 때문에.. 배경지식 습득이 목적입니다.

## Chap 9(Recommendation Systems)
* Recommendation system == predicting user responses
* 이 시스템을 우린 두가지 광범위한 그룹으로 나눌 수 있다
    * **Content-based Systems**
        * netflix, 내가 만약 코미디 영화를 봤다 -> 코미디 영화를 추천
    * **Collaborative filtering systems**
        * user와 item을 고려, 유사성을 판단하여 item을 추천
        * 새로운 알고리즘이 무궁무진하게 계속해서 나오고 있다.

### 9.1 A Model for Recommendation Systems
* Model은 주로 matrix의 형태를 띈다.

#### 9.1.1 The Utility Matrix
* **utility matrix의 빈칸을 예측하는 것**, 추천 시스템의 목표는 여기서 나온다.

<img src = '/post_img/201703/15/1.png'/>
* 이 그림을 예로 살펴보자
    * Utility matrix는 user와 item을 통해 나타내게 된다. 이 그림에서는 ABCD가 user HP(Harry porter), TW(Twilight), SW(Star Wars)를 나타내는 item이다.
    * user와 item이 pair로 나타나게 되고 value들은 item의 rating을 의미한다.
    * ex> A 유저가 SW2를 좋아할까?
        * 평가를 할 때 producer, director, stars 등등을 고려해 평가를 해야하고..
        * SW1과 SW2의 유사성을 판단해서 A는 SW1을 싫어했으니까 SW2도 싫어하겠지.. 라고 결론
        * 물론 데이터가 더 많아야 하고 다른 경향도 살펴봐야 하지만 이런식으로 결론을 내리는 과정을 거친다.
    * 확실히 해야 하는 것은 **추천 시스템의 목표는 랭킹을 매겨 높은 점수를 안내해 주는 것이 아니라 유저가 높은 rating을 줄 것 같은 것을 보여주는 안내 하는 것**

#### 9.1.2 The Long Tail
<img src = '/post_img/201703/15/2.png' width ='500'/>
* 과거 그래프의 발생확률이 낮은 부분을 무시하는 경향이 있었다
* 이후 인터넷, 새로운 물류 기술의 발달로 이런 부분도 경제적으로 의미가 있다고 생각, 이를 ```롱테일``` 이라 한다.
* ```Longtail 현상```을 설명 하기 위해 한가지 예시를 들어보자
    * 책방의 추천 시스템은 단순했다. 사람들이 가장 많이 사는 것을 앞에 놓는 식으로
    * 아마존 같은 것이 등장하자 인기의 경계가 모호해졌고 롱테일의 부분 또한 매우 중요해 졌다.

#### 9.1.3 Applications of Recommendation Systems
* 상품추천하는 것들에 대한 예시가 나온다
    * 상품추천 : online-retailer(Amazon) 등
    * 영화추천 : netflix 같은거, 넷플릭스는 이러한 추천 시스템의 정확도가 매우 높다고 한다.
    * 뉴스추천 : youtube나.. 등등

#### 9.1.4 Populating the Utility Matrix
* 일반적으로 두가지 value에 접근하는 방법이 있다
    * item의 rate를 유저에게 묻는다.
        * 일반적으로 대부분 이런식으로 얻는다.
        * 왓챠같은거..
        * 하지만 유저가 점수를 입력할 의지가 없다면 힘들다.
        * 점수가 편향 될 수 있다.
    * user의 행동을 예측한다.
        * 아마존이나 유튜브 같은 곳에서 이런 방식을 많이 사용
        * 만약 물건을 사거나 동영상을 봤을 경우 비슷한(like) 상품을 소팅하여 사지않은(보지않은) 것을 유저에게 보여준다.

### 9.3 Collaborative Filtering
#### 9.3.1 Measuring Simility

<img src = '/post_img/201703/15/1.png' width ='500'/>
* Jaccard Distance
    * matrix의 value를 무시하고 아이템의 집합에만 집중을 한다.
    * value가 없이 구매력만 판단하는 utility라면 좋을 것
    * 1 - Jaccard Simility(둘의 교집합 / 둘의 합집합)
        * ex> 만약 A와 B의 교집합이 1이고 합집합이 5이면 Jaccard Simility는 1/5
        <br/>그리고 Distance는 4/5. 만약 A와 C의 Distance가 1/2라면 A와 C의 유사도가 더 높은 것.
* Cosine Distance
    * 이 역시 이미지를 참고해보자
    * 빈칸을 0이라 치고 A와 B의 cosine을 재면
    <img src = '/post_img/201703/15/3.png' width ='300'/>
    * 빈칸을 0이라 치고 A와 C의 cosine을 재면
    <img src = '/post_img/201703/15/4.png' width ='300'/>
    * A와 B는 0.380 A와 C는 0.322 이므로 A와 B가 더 비슷하다 할 수 있다.
* Rounding the Data
    * 명백하게 낮은 value를 준 것을 제거 시킨다. 그리고 value를 1로 만든다!
    <img src = '/post_img/201703/15/5.png' width ='400'/>
    * 그리고 jaccard distance를 계산하여 판단한다. A와 B는 3/4 A와 C는 1이다.
    * Cosine Distance와 동일한 결과가 나오는 것을 볼 수 있다.
* Normalizing Ratings
    * 정규화를 어떻게 했더라..

    * 내용추가 중..

## Content-based는 추후에(캡스톤과 직접적 관련이 없다 생각하여 잠시 생략)
### 9.2 Content-based Recommendations
#### 9.2.1 Item Profiles
#### 9.2.2 Discovering Features of Documents
#### 9.2.3 Obtaining Item Features From Tags
#### 9.2.4 Representing Item Profiles
#### 9.2.5 User Profiles
#### 9.2.6 Recommending Items to Users Based on Content
#### 9.2.7 Classification Algorithms
#### 9.2.8 Exercises for Section 9.2

<br/><br/>
