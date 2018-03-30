---

layout: post
title: "(캡스톤) 캡스톤[4.9]"
category: PYTHON

---

### 다른 방법 학습(4월 9일)
> 오늘의 목표다.
1. 일단 있는 데이터로 계산을 해보자
    * 컴공 친구를 찾아 그 친구에 가장 유사한 과목을 찾아보자

### Cosine Similarity

```python
import mysql.connector
import pymongo
from mysql.connector import errorcode
from pymongo import MongoClient
import math
from math import *
import operator


# mysql connect
try:
    cnn = mysql.connector.connect(
        user = 'root',
        password = 'hotspot1',
        database = 'timetable'
    )
    print("It works")

except mysql.connector.Error as err:
    if err.errno == errorcode.ER_ACCESS_DENIED_ERROR:
        print("something is wrong with user or password")
    elif err.errno == errorcode.ER_BAD_DB_ERROR:
        print("Database Does not exist")
    else:
        print(err)

# mongodb connect

mongoClient = MongoClient()
db = mongoClient.rec
collection = db.users

cursor = cnn.cursor(buffered=True)

def get_data_from_mysql():
    Query = "select schedule_id, course_id from selections;"
    cursor.execute(Query)
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


def get_cosine_similarity(rating1,rating2):
    x = 0
    y = 0
    xy = 0
    for key in rating1:
        x += rating1[key]*rating1[key]
        if key in rating2:
            xy += rating2[key]*rating1[key]
    for key in rating2:
        y += rating2[key]*rating2[key]
    similarity = xy / (sqrt(x)*sqrt(y))
    return similarity


def compute_nearest_neighborhood(self,users):
    distances = []
    compusernumb = self[0].get('_id')
    for user in users:
        userNumb = user.get('_id')
        if userNumb != compusernumb:
            dist = get_cosine_similarity(user["subject"],self[0]["subject"])
            if dist > 0:
                distances.append((dist,user["_id"]))
    distances.sort(reverse=True)
    if len(distances) > 20:
        return distances[:20]
    else:
        return distances


def recommend(self,users):
    nearest_set = compute_nearest_neighborhood(self,users)
    userSubject = self[0]["subject"]
    recommendation = {}
    for ne in nearest_set:
        weight = ne[0]
        userId = ne[1]
        neSubject = collection.find({"_id": userId})[0]["subject"]
        for sub in neSubject:
            if sub not in userSubject:
                if sub not in recommendation:
                    recommendation[sub] = weight
                else:
                    recommendation[sub] += weight
    sort_rec = sorted(recommendation.items(),key=operator.itemgetter(1),reverse=True)
    #sort 할 때 0으로 하면 key 기준 1은 value기준
    return sort_rec

```

#### 결과 테스트

<img src = '/post_img/201704/09/1.png' width="700"/>
* course_id가 4769인 것은 이문규 교수님의 문해기를 의미합니다.

<img src = '/post_img/201704/09/2.png' width="700"/>
* 문해기를 듣는 42번 학생을 대상으로 한번 과목을 추천해 보겠습니다

<img src = '/post_img/201704/09/3.png' width="240"/>
* 결과를 출력해보면 42번 학생과 similarity가 비슷한 친구들의 weight를 더해 봤을 때 3779(송민석교수님 OS), 4615(타메르교수님 데이터통신), 3371(이주홍교수님 DB), 5083(최규승 교수님 지식재산 이론과 실제)과목을 같이 많이 선택하는 군요.(대충맞는거같은데?)

<img src = '/post_img/201704/09/4.png' width="240"/>
* 컴공말고 환경공학과 쪽으로 떠나보면 김정환 교수님의 수처리 단위조작(전공필수)를 듣는 친구들은 4984(폐기물처리1), 5094(물리화학적수처리 공정설계)를 같이 선택하는것같습니다.(이것도 대충맞다고 하네요bb)



#### 아직도 하는 고민들
* 추천서버는 오직 추천만?
* 데이터 관리는 어떻게..
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
