---

layout: post
title: "(캡스톤) 캡스톤 뭐했는지 정리"
category: PYTHON

---

### 환경설정(3월 30일)
> 해야하는 것이 뭐가 있냐 하면
1. 가지고 있는 sql 파일을 내 컴퓨터에 import 하기
2. import한 자료 파이썬에서 connector 이용해서 연결하기
3. 쿼리 입력해서 출력해보기
4. 몽고디비도 연결해서
5. 데이터 가공해보기

#### 시작하기
* 먼저 맥에는 mysql과 mongodb가 깔려있다. 이전에 예제를 해봤던게 남아있어서..다행인 것 같다.
* 파이썬과 파이참만 새로 깔았다. 사실 이부분에 있어서 왜 데이터 분석을 파이썬과 NOSQL을 이용해야 하는지 조금 의문이 간다.
* 일단 파이썬이 스트링 분석을 편하게 해주는 부분이 많아 그렇게 생각하고 시작해 보겠다.

#### SQL import
* Workbench에서 쉽게 하였다.
1. 로컬에서 작업을 할 것이기 때문에 선택
<img src = '/post_img/201704/03/1.png' width ='500'/>
2. Data Import 선택
<img src = '/post_img/201704/03/2.png' width ='300'/>
3. Import 파일을 폴더에서 선택하고(...에서 선택하세요)
<img src = '/post_img/201704/03/3.png' width ='700'/>
4. databases를 선택한 뒤 Import하게 되면
<img src = '/post_img/201704/03/4.png' width ='300'/>
5. 쿼리 몇개를 넣어서 확인해보자. 잘 Import가 된 것을 볼 수 있다.`select * from selections;`
<img src = '/post_img/201704/03/5.png' width ='600'/>

#### import한 내용 python에서 쓸 수 있게 연결
* [커넥터 설치 참조 유튜브, https://www.youtube.com/watch?v=1ji8lqiBJe0](https://www.youtube.com/watch?v=1ji8lqiBJe0)
* Pycharm에서 예제로 Hello.py를 만들고 연결을 해보겠다.

~~~PYTHON
import mysql.connector
from mysql.connector import errorcode

try:
    cnn = mysql.connector.connect(
        user = 'root',
        password = '**',
        database = 'mysql'
    )
    print("It works")
except mysql.connector.Error as err:
    if err.errno == errorcode.ER_ACCESS_DENIED_ERROR:
        print("something is wrong with user or password")
    elif err.errno == errorcode.ER_BAD_DB_ERROR:
        print("Database Does not exist")
    else:
        print(err)

cursor = cnn.cursor(buffered=True)

Query = "select * from selections" #실행할 쿼리
cursor.execute(Query)

rows = cursor.fetchall()

for i in rows:
    print(i)

cnn.commit()
cursor.close()
cnn.close()
~~~

* 출력을 해보니 안에 들어있는 수많은 값들이 tuple 형태로 넘어오는 것을 확인
<img src = '/post_img/201704/03/6.png' width ='700'/>


#### 몽고디비 연결, Collections 만들기
`$ python3 -m pip install pymongo` 먼저 설치 하고

~~~PYTHON
import mysql.connector
import pymongo
from mysql.connector import errorcode
from pymongo import MongoClient

# mysql connect
try:
    cnn = mysql.connector.connect(
        user = 'root',
        password = 'hotspot1',
        database = 'mysql'
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
db = mongoClient.rec_test # collectio
collection = db.testCollection


cursor = cnn.cursor(buffered=True)
Query = "select schedule_id, course_id from selections;"
cursor.execute(Query)

rows = cursor.fetchall()

# 넘겨받은 row의 인자는 tuple로 구성되어있다. tuple은 수정할 수 없다
for i in rows:
    sch_id = i[0]
    cou_id = i[1]
    collection.insert({"schedule_id":sch_id, "course_id": cou_id, "score": 1})

co = db.testCollection.find({"schedule_id":990});

for a in co:
    print(a)

cnn.commit()
cursor.close()
cnn.close()
~~~

* 결과화면
<img src = '/post_img/201704/03/7.png' width ='700'/>

### 데이터 가공해보기(4월 3일)
> [공부하기 아주 보기 좋은 사이트](http://guidetodatamining.com/)를 발견했다.
1. 데이터 가공해보기
2. 계산해서 데이터 보기
3. 컴퓨터공학과만 계산결과 뽑아서 어떻게 계산 결과 나오는지 보기





<br/><br/>
