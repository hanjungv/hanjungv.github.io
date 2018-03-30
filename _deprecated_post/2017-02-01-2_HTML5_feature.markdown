---

layout: post
category: HTML
title: "(HTML5) html5 특징"

---

* pre-HTML
    * 하나의 소스가 브라우저마다 다르게 보임
    * 브라우저 내의 영역이 많아지지만 이를 표준화 할 수 없었음
    * CSS의 의존도가 높았고 둔탁함
    * 모바일 기기, 전자제품 등에 포괄적으로 연동 되는 웹이 필요해짐
* HTML5
    * 별도의 플러그인 없이도 다양한 멀티비디어 컨텐츠 확인 가능(플래시 플레이어 없이 영상 재생가능)
    * 어도비, 실버라이트, 자바FX 등 플러그인 기반의 인터넷 애플리케이션을 줄임
    * 간단한 업데이트
    * 기존의 마크업 요소들을 재 정의 : div 대신 header, nav, article 등으로 사용자들에게 명확한 문서윤곽을 정해줌
* 간단한 코드구조를 보면 이렇다. 적응이 되서 그런진 모르겠지만 바꾸기가 힘듦…

```html
//HTML4
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
</body>
//HTML5
<body>
    <header></header>
    <nav></nav>
    <article>
        <section>
        </section>
    </article>
    <sidebar></sidebar>
    <footer></footer>
</body>
```

* HTML4에서 사용되던 element들의 삭제와 변경
    1. acronym  ⇒  abbr
    2. applet  ⇒  object
    3. basefont  ⇒ CSS
    4. big  ⇒ CSS
    5. center  ⇒ CSS
    6. dir  ⇒  ul
    7. font  ⇒ CSS
    8. frame
    9. frameset
    10. noframes
    11. strike  ⇒ CSS,  s , or  del
    12. tt  ⇒ CSS
* New Input Types
    1. color : 색을 고를 수 있는 파레트가 나옴
    2. date : 달력이 나온다
    3. datetime : 시간까지 기록 가능
    4. datetime-local
    5. email : 자동으로 이메일 양식을 체크 해 줄것
    6. month
    7. number
    8. range : 바 형식으로 range를 조절 할 수 있다
    9. search
    10. tel
    11. time
    12. url
    13. week : 몇년도 몇번째 주인지 알 수 있다.
* New Input Attributes
    1. autocomplete : 민감하지 않은 정보들을 저장하여 다시 쓸 수 있게 합니다.
    2. autofocus : 페이지가 로드 될 떄 focus가 되게 합니다.
    3. form
    4. formaction : 액션
    5. formenctype : 암호화
    6. formmethod : 메소드
    7. formnovalidate :validate를 할 것인가
    8. formtarget
    9. height and width : 넓이 높이를 지정할 수 있게 됐습니다.
    10. list : 사용자에게 리스트가 제공 됩니다.
    11. min and max : value들의 최대 최소 값을 한정 시킬 수 있습니다.
    12. multiple : input에 여러가지 값을 넣는 것을 허용
    13. pattern (regexp) : 정규식을 넣어 잘못될 경우를 판단 할 수 있게 합니다
    14. placeholder : input박스 내의 placeholder
    15. required : 반드시 입력이 되게(option같은 곳에 사용)
    16. step : 증가율, 증가량

### 참조
* (참조 : w3school / http://html5ref.clearboth.org/html5:attribute:step_input)
* (참조 : w3school / http://html5ref.clearboth.org/html5:attribute:step_input)
* (출처 : https://en.wikipedia.org/wiki/HTML5#Differences_from_HTML_4)

<br/><br/>
