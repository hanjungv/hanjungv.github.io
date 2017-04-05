---

layout: post
title: "(캡스톤) 캡스톤[4.5]"
category: PYTHON

---

### 몽고디비 연습(4월 5일)
> 오늘의 목표다.
1. 데이터 가공 해서 올바르게 추출, 맨하탄 거리구하기.
2. 가장 유사한 인물 찾아보기
3. 알고리즘 고민

#### 현재의 상태
<img src = '/post_img/201704/05/1.png/'>
* "subject"라는 키에 값들이 dictionary 형태로 들어가게 된다.

#### 현재 맨하탄 함수의 구성
* 하나의 유저에서 다른 유저와 같은 과목을 들었을 때 그 rating의 차이(아마 지금은 두 값이 모두 1로 되어있어 값은 0이 되겠지..)
* 일단은 함수에 딕셔너리 형태로 두 값을 넘겨줘야 함.

#### 기존 함수가 일단 잘 출력이 되는가 확인..

```python
# push를 하니 Array값이 들어가 set으로 바꿈!
# subject에 value를 가짐
def getDataFromMysql():
    rows = cursor.fetchall()
    for i in rows:
        sch_id = i[0]
        cou_id = str(i[1]) #str로 썼음
        collection.update(
            {
                "_id": sch_id
            },
            {
                "$set":
                    {
                        "subject." + cou_id: 1.0
                    }
            },
            upsert=True)

# manhattan 함수
# rating이 다를 때 의미가 있는 것 같다. 바꿔야 함. 일단 계산이 되는지 보자
def manhattan(rating1, rating2):
    distance = 0
    for key in rating1:
        if key in rating2:
            print(key)
            distance += abs(rating1[key] - rating2[key])
    return distance

#일단 두명의 유저는 같은 과목을 들은 학생이다.
user1 = collection.find({"_id":1561})
user2 = collection.find({"_id":1562})
aa = user1[0]["subject"]
bb = user2[0]["subject"]
# 출력을 해보면
print(aa)
print(bb)
print(manhattan(aa,bb))
```
<img src = '/post_img/201704/05/2.png/'>
* 겹치는 키들과 맨하탄 거리가 출력된다(물론 0이 나오겠지..)
* 일단 잘 작동이 되는 것을 확인했다.

#### 일단 여기까지 오면서..
* 적어보니 이걸 왜이렇게 오래 잡고있었나 싶지만..
* List인지 Dict인지 Set인지 각각 value를 뽑는데 어려움이 있었다.
* 일단 참조한 [stackoverflow](http://stackoverflow.com/questions/2225038/determine-the-type-of-an-object)를 보면

```python
>>> type([]) is list
True
>>> type({}) is dict
True
>>> type('') is str
True
>>> type(0) is int
True
>>> type({})
<type 'dict'>
>>> type([])
<type 'list'>
```

* dictionary value, key, 쌍 뽑기

```python
print(aa.keys())
print(aa.values())
print(aa.items())
# 출력은 이렇다.
# dict_keys(['3594', '4254', '4026', '2695', '3439'])
# dict_values([1.0, 1.0, 1.0, 1.0, 1.0])
# dict_items([('3594', 1.0), ('4254', 1.0), ('4026', 1.0), ('2695', 1.0), ('3439', 1.0)])
```

#### 가장 유사한 학생 찾아보기
* 방식은 단순하다. 1:1로 manhattan 계산을 한 뒤 list를 반환한다.
* 그럼 맨하탄 계산법을 수정해야 한다.
    * 지금 데이터를 가지고 할 수 있는 최선의 방법이 뭘까..
* 일단은 distance를 계산하여 리턴해 주는 함수를 만들었다.

```python
def computeNearestNeighbor(compUser, users):
    distances = []
    compUser_numb = compUser[0].get('_id')
    for user in users:
        user_numb = user.get('_id')
        if user_numb != compUser_numb:
            distance = manhattan(user["subject"], compUser[0]["subject"])
            distances.append((distance, user["_id"]))
    distances.sort()
    return distances
```
* 개선필요 : distance 순으로 줄을 세웠다. 이후에는 갯수 제한을 둬 제일 작은것과 비교하는 방법이 좀 더 좋을것 같다.
* 일단 결과 화면은 적절하게 나온다. 이제 맨하탄 계산법을 수정해야한다.


<br/><br/>
