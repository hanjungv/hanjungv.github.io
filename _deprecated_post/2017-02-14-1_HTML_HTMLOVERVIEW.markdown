---

layout: post
title: "(HTML) HTML overview[1/3]"
category: HTML

---

##### 멋쟁이 사자처럼을 준비하면서 저 나름대로 준비를 해야할 것 같아 시작했습니다. 지적 감사히 받겠습니다.

### HTML이란?
* Hyper Text Markup Language의 약자
* 마크업의 문법적 특성을 갖는 컴퓨터 언어
* 굉장히 쉽다. 시작을 하기에 좋은 언어!

### HTML문서 구조
* 머리와 몸, 사람과 같이 생각해보자

```HTML
//HTML4
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8">
        <title>주로 head에는 문서 정보, 문자set 등을 명시해준다.</title>
    </head>
    <body>
        <div id ="header"></div>
        <div id ="nav">
        </div>
        <div class ="article">
            <div class ="section">
            </div>
        </div>
        <div id ="slidebar">
        </div>
        <div id ="footer">
        </div>

        //HTML5의 의미론적 태그
        <header></header>
        <nav></nav>
        <article>
            <section>
            </section>
        </article>
        <sidebar></sidebar>
        <footer></footer>
    </body>
</html>
```

### DOCTYPE이 뭘까?
* Document Type Declaration
* 브라우저에서 어떤 타입으로 표준되고 있는지 알려 주는 역할
* html 문서일 때 <!DOCTYPE html> 이런 식으로 쓴다.
* [위키를 참고해보자!](https://ko.wikipedia.org/wiki/%EB%AC%B8%EC%84%9C_%ED%98%95%EC%8B%9D_%EC%84%A0%EC%96%B8)


### Tag 소개(1/2)
* **p**, paragraph
    - 단락을 구분
* **br**, forced line-break
    - 줄을 개행시켜준다.
* **img**, image

```html
<img src = "이미지 위치" alt = "alternative text, 이미지가 깨졌을 시 나오는 " title = "도움말" height = "300" width = "300"/>
// 높이와 너비의 단위는 px
```

* **table**, 표
    - td는 table data의 줄임말
    - tr은 table row의 줄임말, 구분을 지어줄 때 쓰자
    - thead, tbody, tfoot 으로 의미론적으로 구분
    - 예전에는 테이블을 통해 레이아웃을 잡는 경우가 많았는데 W3C에서 그렇게 사용하지 말자 라고 권장이 내려옴.
    - 실제로 table을 자주 사용하면 웹페이지가 느려진다.

```html
<table>
    <thead>
        <tr>
            <td>이름</td>     
            <td>성별</td>   
            <td>주소</td>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>한정</td>
            <td>남</td>      
            <td >서울</td>
        </tr>
        <tr>
            <td>이민정</td>  
            <td>여</td>      
            <td>서울</td>
        </tr>
    </tbody>
</table>
```

 <br/><br/>
