---

layout: post
title: "(캡스톤) 캡스톤[4.22]"
category: PYTHON

---

### 오늘 할일(4월 22일)
> 오늘의 목표다.
1. 수강신청 사이트 크롤링 및 validation 체크

#### 수정하면서 안점
* python은 && || operator대신 and 와 or을 쓴다 한다.
* 장소를 따로 파싱했지만 장소가 없는 과목또한 많다.(대부분 건축, 간호)이걸 어떻게 처리할 지에 대해 생각해봐야한다.
* 요일과 장소가 균일하게 등장하지 않는다. 하지만 hidden 으로 숨겨진 값들이 있다. 한번 빈칸으로 들어가는 값이 있는지 찾아봤지만 없었다.
```python
for tr in trs:
    pr = parse(tr)
    for idx, res in enumerate(pr):
        if(idx == 12 and res == ''):
            print(idx, res)
# 0 과목코드 / 1 분반그룹 / 2 과목명 / 3 학년 / 4 학점 / 5 과목구분 / 6 요일 및 강의실 / 7 담당교수 / 8 평가방식 / 9 비고 10 ? / 11 ? / 12 요일 시간 / 13 ?
# 아무것도 출력 안됨
```
* 다행히도 웹강이 순서 뒤로 가는 경우는 없는 것 같다.
```python
for tr in trs:
    pr = parse(tr)
    br = []
    for idx, res in enumerate(pr):
        if idx == 12:
            pas = day_time_parse(res)
            if len(pas) > 1:
                if "D0" in pas[1]:
                    print(pas[1])
# 결과 없음
```
* 요일을 3일 이상 나가거나 장소가 3군데 이상 바뀌는 경우를 찾아보니
```python
for idx, res in enumerate(pr):
    if idx == 6:
        br = class_parse(res)
        if len(br) > 2:
            print("br",br)
        # print(idx, br)
    elif idx == 12:
        pas = day_time_parse(res)
        if len(pas) > 2:
            print("pas",pas)
```

<img src = '/post_img/201704/22/1.png'/><br/>
* 3일 이상 나가는 과목은 11개 정도 된다. 더 늘어나지 않을 보장은 없으니..(강의실은 무조건 요일보단 같거나 적게 매칭될 것이다.)
* 그래서 쪼갰다. 뭔가 허접하지만..
```python
def class_parse(dtr):
    str = dtr
    val = 0
    idx = 0
    start = False
    bring = ""
    ret = []
    for ch in str:
        for a in day:
            if ch == a:
                val += 1
        if ch == '(':
            start = True
        elif ch == ')':
            for i in range(0, val):
                ret.append(bring)
            start = False
            bring = ""
            val = 0
        elif start == True:
            bring = bring + ch
    return ret
```
* 하지만 반례가 있다. 같은 요일 1,2 교시는 A교실 3,4,5교시는 B교실 일 경우.. 시간을 파싱한 데이터와 요일을 파싱한 데이터의 갯수가 달라져 매칭이안된다..(아...)
* 그냥 요일을 이용해서 파싱을 해야할것같다.
* 가장 파싱하기 힘든 예시 네개
    * 셀0(웹강의) /월9,10,11,12(60주년-013)
        * {D0T0 : 웹강의, D1T9T10T11T12 : 60주년-013}
    * 금7,8(60주년-707) /금9,10,11,12(60주년-808)
        * {D5T7T8 : 60주년-707, D5T9T10T11T12:60주년-808}
    * 수10,11,12,금7,8,9(5동106B)
        * {D3T10T11T12 : 5동106B, D5T7T8T9 : 5동106B}
    * 월10,11,12,수10,11,12(하-207) /금9,10,11,12(하-424)
```python
from bs4 import BeautifulSoup
import requests
import re

days = {"셀":"D0", "월":"D1", "화":"D2", "수":"D3", "목":"D4", "금":"D5", "토":"D6"}

def parse(tr):
    data = []
    tds = tr.find_all('td')
    for td in tds:
        data.append(td.text)
    return data


def ready_parse(str):
    br = str.strip()
    for day in days:
        for key in day:
            br = br.replace(key, key + ",")
    return br

def isday(compday):
    for day in days:
        for key in day:
            if compday == key:
                return True
    return False

def parse_time_day(str):
    ready_p = ready_parse(str)
    ans = {}
    btr = re.split(r"[\:\,\.\(\)\/\s]", ready_p)
    day_start = False
    bring_day = ""
    bring_time = ""
    bring_class = ""
    dayday = []
    classclass = []
    timetime = []

    for elem in btr:
        if elem == '':
            continue
        if isday(elem) == True:
            if day_start == False:
                day_start = True
            else:
                dayday.append(bring_day)
                timetime.append(bring_time)
                bring_time = ""
            bring_day = days[elem]
            continue
        if day_start == True:
            if elem.isdigit():
                bring_time = bring_time + "T" + elem
                # 숫자일 경우
            else:
                bring_class = elem
                dayday.append(bring_day)
                timetime.append(bring_time)
                for i in range(0, len(timetime) - len(classclass)):
                    classclass.append(bring_class)
                bring_day = ""
                bring_time = ""
                day_start = False
                # 장소일 경우

    if len(classclass) == 0:
        for a in range(0, len(dayday)):
            classclass.append('장소미정')

    for idx, a in enumerate(dayday):
        dd = dayday[idx]
        tt = timetime[idx]
        res1 = dd + tt
        ans[res1] = classclass[idx]
    return ans


url = 'http://sugang.inha.ac.kr/sugang/SU_51001/Lec_Time_Search.aspx'
r = requests.get(url)

soup = BeautifulSoup(r.text,'html.parser')
select = soup.find('select',id='ddlTime1')
options = select.find_all('option')

timedatas = []

for o in options:
    if o['value'] == '선택':
        continue
    timedatas.append({
        'name': o.text,
        'value': o['value']
    })

soup = BeautifulSoup(r.text,'html.parser')
select = soup.find('select',id='ddlDept')
options = select.find_all('option')

majors = []

for o in options:
    majors.append({
        'name': o.text,
        'value': o['value']
    })

event_target = ''
event_argument = ''
last_focus = ''
view_state = soup.find('input',id='__VIEWSTATE')['value']
view_state_generator = soup.find('input',id='__VIEWSTATEGENERATOR')['value']
event_validation = soup.find('input',id='__EVENTVALIDATION')['value']

# rdoKwamokGubun : 99 전체 / 06 전선 / 05 전필 / 02 교선 / 01  교필 / 09 일선 / 08 교직

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
        'ibtnSearch3.x': '48',
        'ibtnSearch3.y': '12',
        'ibtnSearch3': '조회'
    })
    soup = BeautifulSoup(r.text, "html.parser")
    table = soup.find('table', id='dgList')
    trs = table.find_all('tr')
    for tr in trs:
        pr = parse(tr)
        class_res = []
        day_res = []
        for idx, res in enumerate(pr):
            if idx == 6:
                print(parse_time_day(res))
        if len(class_res)!=len(day_res):
            print(class_res, day_res)
            # 0 과목코드 / 1 분반그룹 / 2 과목명 / 3 학년 / 4 학점 / 5 과목구분 / 6 요일 및 강의실 / 7 담당교수 / 8 평가방식 / 9 비고
            # 10 ? / 11 ? / 12 요일 시간 / 13 ?

            # D0 : 웹강
            # D1 ~ D7 : 월 ~ 금
            # T1 ~ T25 : 1교시 ~ 25교시


```
* 일단 완성한 파싱 코드이다. 정규식을 이용하여 각 데이터를 split했고 규칙을 찾아 데이터를 만들어 dictionary 형태로 만들어줬다.
* 강의실이 입력이 안되는 경우도 많아 강의실이 없는경우 '장소미정'으로 두었다.
* 이렇게 할 경우 예외에 모두 정당하게 처리 될 수 있는 코드가 된다.(사실 어떤 예외가 발생할 지는 모르지만..)


#### 아직도 하는 고민들
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
    -> 지속적인 테스트 필요


<br/><br/>
