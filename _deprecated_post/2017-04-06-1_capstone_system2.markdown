---

layout: post
title: "(캡스톤) 캡스톤[4.6]"
category: PYTHON

---

### 다른 방법 학습(4월 6일)
> 오늘의 목표다.
1. http://guidetodatamining.com/ 2장내용을 다 읽고
2. 내용을 정리해본다음에
3. 이를 이용한 코드를 짜보자

그러면 뭔가 추천시스템 방향이 보이지 않을까?싶다.(제발)

#### 2장 Collaborative filtering
> 다 읽고 보니 이 자료는 궁금했던 부분을 많이 해결해줬다. 초심자에게 매우 좋은 자료인것같다.

##### 내용정리
1. **Manhattan Distance**
2. **Euclidean Distance**
    * pythagorean Theorem : 구하는 법은 전부 알 것이다.
3. N-dimmensional에서 구하는 예제, 한번 쓱 보면 알 수 있다.
<img src = '/post_img/201704/06/1.png'>

* 위 내용은 이미 python으로 예제를 만들어 보았었다. 앞선 포스트에 있다.
    * [포스트 1](https://hanjungv.github.io/2017-04-03-1_capstone_system/)
    * [포스트 2](https://hanjungv.github.io/2017-04-05-1_capstone_system1/)
4. Manhattan Distance와 Euclidean Distance는 missing value가 없을 때 좋다고 한다. 지금 우리의 sparse한 데이터 분석에 적절하진 않은 것 같다. 이부분은 뒤에서 좀 더 이야기 해보자.
5. **Pearson Correlation Coefficient**
<img src = '/post_img/201704/06/2.png'>
    * 이런 경우가 있다고 생각해 보자. 여기서 4점은 같은 의미의 4점이 아니다.
    <img src = '/post_img/201704/06/3.png'>
    * 그래프를 그려보면 이런 형태로 그래프가 그려질 것이다. straight line이 그려진다면 'perfect Agreement'상태를 나타낸다.<br/>
    <img src = '/post_img/201704/06/4.png'>
    * 다른 그래프를 보면 'Pretty Good Agreement', 'Not so Good Agreement'를 알 수 있다. 수식으로 어떻게 구할 수 있을 까?<br/>
    <img src = '/post_img/201704/06/5.png'>
    * 이 수식은 Pearson의 근사값 계산을 쉽게 해주는 공식이다. 코딩 또한 쉽다.

```python
from math import sqrt
def pearson(rating1, rating2):
    sum_xy = 0
    sum_x = 0
    sum_y = 0
    sum_x2 = 0
    sum_y2 = 0
    n = 0
    for key in rating1:
        if key in rating2:
            n += 1
            x = rating1[key]
            y = rating2[key]
            sum_xy += x * y
            sum_x += x
            sum_y += y
            sum_x2 += x**2
            sum_y2 += y**2
    # if no ratings in common return 0
    if n == 0:
        return 0
    # now compute denominator
        denominator = sqrt(sum_x2 - (sum_x**2) / n) *
                    sqrt(sum_y2 - (sum_y**2) / n)
    if denominator == 0:
        return 0
    else:
        return (sum_xy - (sum_x * sum_y) / n) / denominator
```
6. **Cosine Similarity**
    * 가장 많이 사용하는 방식! Collaborative filtering에 많이 쓰인다.
    <img src = '/post_img/201704/06/6.png'>
    * 계산법이다. 1에 가까우면 Similarity가 높은것이고 -1에 가까우면 반대에 가까운것이다.
    * 예를 한번 살펴보자
    <img src = '/post_img/201704/06/7.png'>
    * 이러한 표를 가지고 있다면<br/>
    <img src = '/post_img/201704/06/8.png'>
    <img src = '/post_img/201704/06/9.png'>
    * 즉 결과는 0.935, 매우 친밀한 상태이다.<br/>
    <img src = '/post_img/201704/06/10.png'>
7. 어떤 Similarity를 선택할 것인가?
    * Manhattan / Euclidean 은 **dense** 한 데이터에 적합하다.
    * Pearson은 **grade-inflation** 이 있는 곳에 적합하다.
    * Cosine Similarity는 **sparse** 한 데이터에 적합하다.
8. 우린 데이터가 sparse한 편이다. 또한 grade-inflation이 있을 것이라 예상이 된다.(1~10점 사이의 rating을 줄 것이다.)
9. 뭔가 발생될 수 있는 상황이 예시로 등장한다.
    * distance를 선택할 때 0이 많을 때 안좋은 이유가 등장하는데
    * A라는 사람이 26곡을 평가했고 B라는 사람과 25곡이 겹친다.
    * 또 C라는 사람은 150곡을 평가했는데 그중 A와 25곡이 겹친다.
    * 그러면 둘 다 같은 친밀도를 가져야하는데 Distance로 계산할 경우 값이 달라지게 된다.
    * 왜냐? Distance는 둘 다 0이 아닌 이상 엄청나게 영향력 있는 값으로 변해 반영이 된다.
10. k-nearest neighbor
    <img src = '/post_img/201704/06/11.png'>
    * 만약 나와 이러한 유사도를 가지고 있다면 k = 2일 때
    <img src = '/post_img/201704/06/12.png'>
    * 내 점수는 4.2 정도로 예상이 되는 것을 알 수 있다.
    * 예상 점수를 이런식으로 사용할 수 있을 것 같다.

# 정리중

#### 그 외의 고민들
* 연산 횟수가 엄청날 것 같다.
    * Similarity를 구해야 한다.
    * 그리고 user와 가장 가까운 k-nearest 집단을 만든다.
    * 그리고 그 집단에서 추천되어야 하는 과목을 선택한다.
        * 여기서 만약에 그 과목을 다들었다면 어떻게 할까?
        * 역으로 하나도 안들었다면?
    * 만약 1명이 추가되면 어떻게 연산 할 것인가?
    * 계산했던것은 어떻게 관리할까?
* Cosine Similarity로 점수를 예측 할 수 있을까?
* 서버는 어떻게 둘 것인가..
    * 이건 좀 장기적으로 볼만한 문제..


<br/><br/>
