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
* 만들수 있는 방법은 많지만 쉽게 따라할 수 있는 방식으로 설명했습니다.
* 저는 블로그를 만들고 -> GA를 달고 -> 커스터 마이징 하는 과정을 설명해 드리려 합니다. 그 기준은 제가 사용하고 있는 테마입니다.

#### 블로그 만들기
1> 깃헙 아이디는 있으실거라 생각합니다. <br/>
2> **반드시 루비를 설치하고 오셔야 합니다. 구글을 조금만 찾으면 쉽게 설치할 수 있을 겁니다! [설치링크 ](https://www.ruby-lang.org/ko/documentation/installation/)** <br/>
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

5> 먼저 깃에 꼭 **자신의아이디.github.io** 로 repository를 만듭니다.<br/>
저같은 경우는 아이디가 hanjungv이므로 hanjungv.github.io로 만들었습니다.<br/><br/>
<img src = '/post_img/201702/03/blog1.png' width="600"/><br/><br/>
6> 관리할 폴더에

```
// 테마 클론 따기, 원하는 테마를 받으시면 됩니다. 여기선 제 테마 기준으로 설명하겠습니다.
$ git clone https://github.com/daattali/beautiful-jekyll.git
$ cd beautiful-jekyll
$ bundle install
// 제 깃으로 관리를 할 것이기 때문에
$ rm -rf .git
$ rm -rf .gitignore
$ git init
$ git add .
$ git commit -m "blog first commit"
$ git remote add origin https://github.com/myid/myid.github.io.git
$ git push origin master
```
여기까지 하고 깃헙에 들어가서 푸시가 제대로 됬는지 확인해 봅시다.<br/><br/>
<img src = '/post_img/201702/03/blog2.png' width="600"/><br/><br/>
코드가 올라간 것이 보이면 제대로 하셨습니다.

7> 클론한 코드를 살펴보겠습니다.<br/><br/>
<img src = '/post_img/201702/03/blog3.png' width="200"/><br/>
* readme 파일이 테마작성자의 마음대로 되어있으니 수정을 원하시면 하시면 됩니다. 저같은 경우는 라이센스를 남기고 나머지는 전부 지웠습니다.
* posts 디렉토리에는 제가 올릴 포스트들의 내용이 들어갈 것입니다.
* 저희는 config.yml의 내용을 수정하면서 대부분의 설정을 끝낼 것입니다. 제 config 파일입니다.

```yml
#_config.yml, 수정한 부분만 옮겨 적어보겠습니다.
url: "http://hanjungv.github.io"
# meta tag 관한 내용입니다. 수정해 주셔야 검색에 수월해 지실 겁니다.
title: HANDEVBLOG
description: Dev_blog_by_hanjung
# nav링크는 aboutme를 남기고 전부 지웠습니다.
navbar-links:
  About Me: "aboutme"
# 프로필 이미지 입니다. 이부분은 메타 태그와 연관되어지니 수정하시는게 좋을 것입니다.
avatar: "/img/profile.JPG"
# footer 관련 내용입니다 필요하신 사항 입력해 주세요. 그리고 true false로 footer에 링크를 띄울 것을 선택해줍니다.
author:
  name: hanjung
  email: "hanjungv@gmail.com"
  facebook: profile.php?id=100005573837145  # eg. daattali
  github: hanjungv    # eg. daattali
  linkedin: hanjungv  # eg. daattali
footer-links-active:
  rss: false
  facebook: true
  email: false
  twitter: false
  google-plus: false
  github: true
  reddit: false
  linkedin: false
  xing: false
  stackoverflow: false
  snapchat: false
  instagram: false
  youtube: false
  spotify: false
  telephone: false
# 포스트를 share할 수 있게 할지, 어디에 가능하게 할지 선택해 줍니다.
share-links-active:
  twitter: true
  facebook: true
  google: false
  linkedin: true
# timezone은 서울로 수정해줬습니다. 크게 의미는 없는 것 같습니다.
timezone: "Asia/Seoul"
```

* 수정 후 저장하신 다음 프로젝트 디렉토리에서  

```
$ git add .
$ git commit -m "커밋내용"
$ git push origin master
```
를 마친 뒤 myid.github.io 에 들어가 보겠습니다!<br/>
만들어 놓은 블로그가 제대로 나오는 것을 볼 수 있습니다.

8> 포스트는 이전에 만들어져 있던 것을 토대로 작성해주시면 됩니다.<br/>
글씨가 너무 크거나 디자인을 수정하고 싶으시면 css파일을 수정해 주시면 됩니다.<br/>

### 구글 어널리틱스 달기
* 블로그에 방문자가 몇 명이 있고 몇명이 이 글을 보는지, 타켓팅이 어떻게 되는지 GA로 분석 할 수 있습니다.<br/>
[구글 애널리틱스](https://analytics.google.com/)<br/>
* 구글 애널리틱스에 들어가 관리할 대상을 추가합니다.
<br/><br/>
<img src = '/post_img/201702/03/blog4.png' width="600"/><br/><br/>
* 값을 입력해줍니다. 주소와 이름을 입력하게 되면 하나의 자바스크립트 코드를 따란 하고 받게됩니다.

```javascript
<script>
  (function(i,s,o,g,r,a,m){i['GoogleAnalyticsObject']=r;i[r]=i[r]||function(){
  (i[r].q=i[r].q||[]).push(arguments)},i[r].l=1*new Date();a=s.createElement(o),
  m=s.getElementsByTagName(o)[0];a.async=1;a.src=g;m.parentNode.insertBefore(a,m)
  })(window,document,'script','https://www.google-analytics.com/analytics.js','ga');

  ga('create', 'UA-~~~~~~-~', 'auto');
  ga('send', 'pageview');

</script>
```

* 여기서 저희는   ga('create', 'UA-~~~~~~-~', 'auto'); UA 부분의 알파벳과 숫자만 복사해 _config.yml을 엽니다.
<br/><br/>
<img src = '/post_img/201702/03/blog5.png' width="600"/><br/><br/>
* 이부분의 주석을 제거해 준 뒤 UA 부터 마지막 숫자까지의 값을 넣어준 뒤 다시 깃으로 푸시합니다.
* 제대로 달렸는지 확인은 블로그에 들어가 관리자도구를 킨 뒤 Network에서 analytics.js가 생긴 것을 보면 됩니다.
<br/><br/>
<img src = '/post_img/201702/03/blog6.png' width="600"/><br/><br/>
* 구글 태그매니저나 페이스북 관리도 이와같이 API키만 가져와 사용하게 됩니다.

#### 마지막으로
* 웹페이지 구축환경에 익숙하지 않다면 처음에 입맛대로 바꾸는것이 꽤 힘들수도
* 하지만 블로그를 하면서 마크다운, 깃, HTML, CSS, GA 하는법 등을 경험하는 것이 학생인 자신의 입장에선 상당히 좋을 것 같다.
* **잘 모르겠는 것은 페북이나 카톡으로 개인적으로 연락 주시길..**
