---

layout: post
title: "지킬에 channel.io 달기"
category: etc

---

### 시작하기에 앞서
* 채널의 존재는 이미 예~전부터 알고있었다. 회사에서 사용하는 채팅 서비스 인줄 알았다.
* 제드의 블로그를 구경하다 채널처럼 생긴 버튼을 찾아 눌러보니 채널이었다. 음?
* 찾아보니 1인 사용자는 무료사용이었다. 물론 아무도 메세지를 안보내겠지만 채팅 서비스를 블로그에 달아보자<br/>
<img src = '/post_img/201705/18/1.png' height = '500'/><br/>

### 채널.io 소개
* [http://channel.io/ko](http://channel.io/ko) : CTP 선배님들이 몸담고 있는 ZOYI 코퍼레이션의 채팅서비스이다.
* 아직 자세히 사용해 보지 않았지만 봇기능과 사이트 방문자 분석기능, 채팅 저장, 팀 커뮤티케이션, 앱 등 여러가지를 제공한다.
* 게다가 친절한 도큐먼트까지 존재한다!
* 이런 기능을 제공하는데 가격 또한 합리적이다.

#### 설치법
[도큐먼트 가이드, 웹에 채널 붙이기](https://help.channel.io/hc/ko/articles/115004846527-%EC%B1%84%EB%84%90-%ED%94%8C%EB%9F%AC%EA%B7%B8%EC%9D%B8-%EA%B0%80%EC%9D%B4%EB%93%9C-%EC%9B%B9%EC%97%90-%EB%B6%99%EC%9D%B4%EA%B8%B0)에 자세히 나와있지만 한번 다시 해보려 합니다.
1. 일단 가입을 하고 채널을 만듭니다. 사이트의 정보를 입력하면 채널이 생성 될 것입니다!
2. 채널에 들어가서 이 톱니바퀴 모양을 클릭해 줍니다.<br/>
<img src = '/post_img/201705/18/2.png' height = '100'/><br/>
3. **플러그인 관리하기** 로 넘어가서 코드보기를 눌러주세요<br/>
<img src = '/post_img/201705/18/3.png' height = '100'/><br/>
4. 코드를 그대로 긁어서 지킬 includes 폴더에 channel.html에 그대로 복사, 붙여넣기를 해보겠습니다.<br/>
<img src = '/post_img/201705/18/4.png' height = '400'/><br/>
<img src = '/post_img/201705/18/5.png' height = '400'/><br/>
5. 그리고 footer_script.html에 가서 이 한줄을 추가해주면 일단 끝!<br/>
<img src = '/post_img/201705/18/6.png' height = '60'/><br/>


<br/><br/>
