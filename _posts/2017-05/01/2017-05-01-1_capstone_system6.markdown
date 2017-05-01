---

layout: post
title: "(캡스톤) 캡스톤[5.1]"
category: PYTHON

---

### 오늘 할일(5월 1일)
> 오늘의 목표다.
*  seed를 만들자.
    * seed를 만드는 이유? mysql data를 뽑아서 mongodb collection에 넣어줘야 하는 코드 까지 만들어야함.
    * 가공하는 부분까지 코드를 만들어야 하니 어떤형태가 나올지 지금은 모른다.
    * 그러니까 일단 해서 직접 뽑아서 내가 원하는 모양대로 만들어보자

### 시드를 만들어서 mysql에 넣어보자
<img src = '/post_img/201705/01/1.png' width="300"/><br/>
* 내가 시드를 넣을 테이블이다. UserId를 각각 가지고 있다.
* 유저가 각각 Recommendation table을 갖게 된다. distinctCode는 RecommendableCourses에 담겨있는 코드이다. 예측한 결과는 score가 빈 상태로 저장이 될 것이고 평가가 된 내용은 score가 0보다 큰 값이 입력될 것이다.
* 고로 우리가 넣을 데이터는 (일단은) distinctCode와 score, UserId를 채워줘 보자
* score는 1~5점, UserId는 1~10으로 해보자. 데이터가 각각 구분되는 distinctCode는 20개 내외 알파벳 A ~ 랜덤으로 선택되게 하자

```python

import time
import datetime

# 현재 시간 넣기
ts = time.time()
timestamp = datetime.datetime.fromtimestamp(ts).strftime('%Y-%m-%d %H:%M:%S')

distCode = ['A','B','C','D','E','F','G','H','I','J','K','L','M','N','O','P','Q','R','S','T','U','V','W','X','Y','Z']

# 유저 만들기
randEmails = random.sample(distCode,11)
for email in randEmails:
    randEmail = email + "@gg.com"
    Query = "INSERT INTO  Users (email, password, createdAt, updatedAt) VALUES (%s, %s, %s, %s)"
    cursor.execute(Query, (randEmail, "ddd",timestamp,timestamp))
    cnn.commit()

# 추천한 것 만들기
for userId in range(1,11):
    randScr = random.randint(1, 5)
    randCodes = random.sample(distCode,7)
    for randCode in randCodes:
        Query = "INSERT INTO  UserRecommendations (distinctCode, score, UserId, createdAt, updatedAt) VALUES (%s, %s, %s, %s, %s)"
        cursor.execute(Query, (randCode, randScr, userId,timestamp,timestamp))
        cnn.commit()

cnn.close()
```

### 그걸 가지고 와서 MongoDB collection에 넣어보기

* UserRecommendations DB를 만들어서 scoreCollection에 일단 넣어줬다.
* 여기까진 쉽게 된다.

```python
mongoClient = MongoClient()
db = mongoClient.UserRecommendations
scoreCollection= db.scoreCollection
preScoreCollection = db.preScoreCollection

def get_data_from_Userrecommendations():
    Query = "select distinctCode, score, UserId from UserRecommendations;"
    cursor.execute(Query)
    rows = cursor.fetchall()
    for i in rows:
        distCode = i[0]
        score = i[1]
        userId = i[2]
        scoreCollection.update(
            {
                "_id": userId
            },
            {
                "$set":
                    {
                        "subject." + distCode: score
                    }
            },
            upsert=True)

get_data_from_Userrecommendations()
```

<img src = '/post_img/201705/01/2.png'/><br/>
* 오늘은 많이 못했으니 내일 열심히 ㅠㅠ




<br/><br/>
