---

layout: post
title: "(캡스톤) 캡스톤[4.30]"
category: PYTHON

---

### 오늘 할일(4월 30일)
> 오늘의 목표다.
*  나에게 있는 수많은 테이블을 채울 시간이다 ㅠㅠ

### 채울 테이블 리뷰
* 일단은 5개 정도를 크롤링해서 채워 줄 수 있다.<br/>
* 전공<br/>
<img src = '/post_img/201704/30/1.png' width = "200"/><br/>
* 전공과 course를 잇는 테이블, 중간에서 M:N 관계를 맺어준다.<br/>
<img src = '/post_img/201704/30/2.png' width = "200"/><br/>
* 과목, 이부분은 코드로 중복을 체크해줘야한다. <br/>
<img src = '/post_img/201704/30/3.png' width = "200"/><br/>
* 학기<br/>
<img src = '/post_img/201704/30/4.png' width = "200"/><br/>
* 추천 해줄 과목들이 들어간다. 과목코드 + 교수님으로 유니크를 판단한다.<br/>
<img src = '/post_img/201704/30/5.png' width = "200"/><br/>

### 파이썬 코드 짜기

#### Term table
* 연도는 2017, 2018 이런식으로... semester은 spring, summer, fall, winter로 구성될 것이다. 몇개 그냥 만들어 주자.

```python
def fill_term_table():
    year = 2016
    seme = ["spring","summer","fall","winter"]
    for a in range(0,10):
        for ss in seme:
            Query = """INSERT INTO Terms (year, semester) VALUES (%s, %s)"""
            cursor.execute(Query, (year, ss))
            cnn.commit()
        year = year + 1
```
<img src = '/post_img/201704/30/6.png' width = "400"/><br/>

#### Majors table
* 전공은 실제 전공과 밑에 있는 기타 내용을 합쳐버려서 운영할 것이다.

```python
def fill_major_table():
    Query = "INSERT INTO Majors (title) VALUES (%s)"
    for dept in majors:
        cursor.execute(Query, (dept["name"],))
        # 하나를 넣을 때 tuple형태로 넘어가므로 , 가 필요하다고한다.
        cnn.commit()
    for dept in rests:
        cursor.execute(Query, (dept["name"],))
        cnn.commit()
```
<img src = '/post_img/201704/30/7.png' width = "400"/><br/>
<img src = '/post_img/201704/30/8.png' width = "400"/><br/>

#### Courses table, MajorCourses, Recommendable table
* Courses table
    * 일단 이전과 달라진 것이 있다면 TermId를 찾아서 관계를 맺어준다는 것
    * tuple로 넘어오기 때문에 값을 잘 빼서 써야한다. 난 Id만 필요하니..
* MajorCourses
    * 일단 커밋이 Courses table에 된 후 채워줘야한다.
    * lastrowid를 뽑아와서 lastId와 deptId를 가지고 와서 매칭해준다.
* Recommendable table


```python
def fill_course_and_recommendable_table():
    for dept in majors:
        r = requests.post(url,data={
            'ddlDept':dept['value'],
            '__EVENTTARGET': event_target,
            '__EVENTARGUMENT': event_argument,
            '__LASTFOCUS': last_focus,
            '__VIEWSTATE': view_state,
            '__VIEWSTATEGENERATOR': view_state_generator,
            '__EVENTVALIDATION': event_validation,
            'rdoKwamokGubun': '99',
            'ibtnSearch1.x': '48',
            'ibtnSearch1.y': '12',
            'ibtnSearch1': '조회'
        })
        soup = BeautifulSoup(r.text, "html.parser")
        table = soup.find('table', id='dgList')
        trs = table.find_all('tr')
        for tr in trs:
            timeclass = ""
            code = ""
            split_class = ""
            title = ""
            grade = ""
            credit = 0
            class_type = ""
            instructor = ""
            eval = ""
            etc = ""
            pr = parsebase(tr)
            sub_link = parselink(tr)
            for idx, res in enumerate(pr):
                if idx == 0:
                    code = str(res)
                elif idx == 1:
                    split_class = str(res)
                elif idx == 2:
                    title = str(res)
                elif idx == 3:
                    grade = str(res)
                elif idx == 4:
                    credit = int(float(res))
                elif idx == 5:
                    class_type = str(res)
                elif idx == 6:
                    result = parse_time_day(res)
                    for key in result:
                        timeclass = timeclass + key + ":" + result[key] + ";"
                elif idx == 7:
                    instructor = str(res)
                elif idx == 8:
                    eval = str(res)
                elif idx == 9:
                    etc = str(res)

            # Courses 채우기
            termIds = cursor.execute("SELECT id FROM Terms where year = '2017' and semester = 'spring'")
            termId = cursor.fetchone()

            Query = """INSERT INTO  courses (grade, credit, classType, time, instructor, eval, etc, code, title, splitClass, active, url, TermId)
                        VALUES (%s, %s, %s, %s, %s, %s, %s, %s, %s, %s, %s, %s, %s)"""
            cursor.execute(Query, (grade, credit, class_type, timeclass, instructor, eval,etc,code, title, split_class, 1, url, termId[0]))

            cnn.commit()

            # MajorCourse 테이블 채우기
            lastId = cursor.lastrowid
            deptIds = cursor.execute("SELECT id FROM Majors where title = '%s'" % dept["name"])
            deptId = cursor.fetchone()

            Query = "INSERT INTO  MajorCourses (CourseId, MajorId) VALUES (%s, %s)"
            cursor.execute(Query, (lastId, deptId[0]))

            cnn.commit()

            # Recommendable table채우기
            distinctcode = make_distinctCode(code, instructor)
            isExists = cursor.execute("SELECT id FROM RecommendableCourses where distinctCode = '%s'" % distinctcode)
            isThere = cursor.fetchone()

            if isThere == None:
                Query = """INSERT INTO  RecommendableCourses (title, eval, instructor, grade, credit, classType, distinctCode, active)
                                       VALUES (%s, %s, %s, %s, %s, %s, %s, %s)"""
                cursor.execute(Query, (title, eval, instructor, grade, credit, class_type, distinctcode, 1))
                cnn.commit()


    for rest in rests:
        r = requests.post(url, data={
            'ddlKita':rest['value'],
            '__EVENTTARGET': event_target,
            '__EVENTARGUMENT': event_argument,
            '__LASTFOCUS': last_focus,
            '__VIEWSTATE': view_state,
            '__VIEWSTATEGENERATOR': view_state_generator,
            '__EVENTVALIDATION': event_validation,
            'rdoKwamokGubun': '99',
            'ibtnSearch2.x': '48',
            'ibtnSearch2.y': '12',
            'ibtnSearch2': '조회'
        })
        soup = BeautifulSoup(r.text, "html.parser")
        table = soup.find('table', id='dgList')
        trs = table.find_all('tr')
        year = "2017"
        semester = "spring"
        for tr in trs:
            timeclass = ""
            code = ""
            split_class = ""
            title = ""
            grade = ""
            credit = 0
            class_type = ""
            instructor = ""
            eval = ""
            etc = ""
            pr = parsebase(tr)
            sub_link = parselink(tr)
            for idx, res in enumerate(pr):
                if idx == 0:
                    code = str(res)
                elif idx == 1:
                    split_class = str(res)
                elif idx == 2:
                    title = str(res)
                elif idx == 3:
                    grade = str(res)
                elif idx == 4:
                    credit = int(float(res))
                elif idx == 5:
                    class_type = str(res)
                elif idx == 6:
                    result = parse_time_day(res)
                    for key in result:
                        timeclass = timeclass + key + ":" + result[key] + ";"
                elif idx == 7:
                    instructor = str(res)
                elif idx == 8:
                    eval = str(res)
                elif idx == 9:
                    etc = str(res)


            # Courses 채우기
            termIds = cursor.execute("SELECT id FROM Terms where year = '2017' and semester = 'spring'")
            termId = cursor.fetchone()
            Query = """INSERT INTO  courses (grade, credit, classType, time, instructor, eval, etc, code, title, splitClass, active, url, TermId)
                                   VALUES (%s, %s, %s, %s, %s, %s, %s, %s, %s, %s, %s, %s, %s)"""
            cursor.execute(Query, (grade, credit, class_type, timeclass, instructor, eval, etc, code, title, split_class, 1, url, termId[0]))

            cnn.commit()

            # MajorCourse 테이블 채우기
            lastId = cursor.lastrowid
            deptIds = cursor.execute("SELECT id FROM Majors where title = '%s'" % dept["name"])
            deptId = cursor.fetchone()

            Query = "INSERT INTO  MajorCourses (CourseId, MajorId) VALUES (%s, %s)"
            cursor.execute(Query, (lastId, deptId[0]))

            cnn.commit()

            # Recommendable table채우기

            distinctcode = make_distinctCode(code,instructor)
            isExists = cursor.execute("SELECT id FROM RecommendableCourses where distinctCode = '%s'" % distinctcode)
            isThere = cursor.fetchone()
            if isThere == None:
                Query = """INSERT INTO  RecommendableCourses (title, eval, instructor, grade, credit, classType, distinctcode, active)
                                       VALUES (%s, %s, %s, %s, %s, %s, %s, %s)"""
                cursor.execute(Query, (title, eval, instructor, grade, credit, class_type, etc, 1))
                cnn.commit()
```

<img src = '/post_img/201704/30/10.png'/><br/>
<img src = '/post_img/201704/30/11.png'/><br/>
* 에러없이 실행되는 것을 확인 할 수 있고!<br/>
<img src = '/post_img/201704/30/12.png'/><br/>
<img src = '/post_img/201704/30/13.png'/><br/>
<img src = '/post_img/201704/30/14.png'/><br/>

* 잘 들어가는 것을 확인 할 수 있다.
* 내일은 user가 가지고 있는 data의 seed를 만들고 MongoDB collection을 어떻게 관리하는 것이 좋은지 알아볼 예정이다.
* 주말이니까 이제그만..ㅠㅠ



<br/><br/>
