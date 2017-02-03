---

layout: post
title: "지킬 BLOG 만드는 방법"
categories: etc

---

### 지킬이란?
* GitHub Page 내부엔진
* 깃헙에서 프로젝트나 블로그, 웹사이트를 무료로 호스팅 해주는 서비스!
* 지금 이 블로그가 지킬(Jekyll)로 만들어졌습니다.
* 마크다운과 친숙하고 HTML, CSS를 볼 줄 알며 깃헙을 자주 쓰시는 분들에게 적절한 것 같습니다.
    * 사실 저도 잘 모르는데 그냥 하는겁니다.

#### 이 [링크](http://jekyllrb-ko.github.io/docs/quickstart/)를 보고 차근차근 시작할 수 있지만 하나하나 하기엔 우린 시간이 없으므로 속성으로 시작해 보겠습니다.

#### 아셔야 하는 점
* 우선 저는 맥 유저입니다.
* 루비온레일즈 프로젝트를 해본 경험이 있어 루비가 설치되어 있었습니다.
* 깃 사용법은 따로 나와있지 않습니다.
* 저는 블로그를 만들고 -> GA를 달고 -> 커스터 마이징 하는 과정을 설명해 드리려 합니다. 그 기준은 제가 사용하고 있는 테마입니다.

#### 블로그 만들기
1> 깃헙 아이디는 있으실거라 생각합니다. <br/>
2> **반드시 루비를 설치하고 오셔야 합니다. 구글을 조금만 찾으면 쉽게 설치할 수 있을 겁니다(제발 쉽길)** <br/>
3> 터미널 창에서 지킬을 설치합시다 <br/>

```
$ gem install jekyll
```

4-1> 제가 사용하는 지킬 테마는 여기에 있습니다.[https://github.com/daattali/beautiful-jekyll#readme](https://github.com/daattali/beautiful-jekyll#readme)<br/>
4-2> 원래는 이 다음에 new를 통해 페이지를 만들어야 하지만 저희는 이쁜 테마를 쇼핑하러 가겠습니다.<br/>
돈이 많으시면 유료로 된 것을 골라도 좋습니다. 대표적인 사이트들입니다. 다른데서 고르셔도 됩니다.<br/>
고를 때 포스팅할 **글 내용이 어떻게 보이는지**, **카테고라이징** 이 필요한 사이트면 그런 기능이 있는지 살펴보시는게 좋을 것 같습니다.<br/>
    * [http://jekyllthemes.org/](http://jekyllthemes.org/)<br/>
    * [https://jekyllthemes.io/](https://jekyllthemes.io/)<br/>
    * [http://themes.jekyllrc.org/](http://themes.jekyllrc.org/)<br/>

5>
