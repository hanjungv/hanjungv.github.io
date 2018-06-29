---

layout: post
title: "(Swift) temp와 Library와 document"
category: SWIFT

---

* 앱을 구성할 때 목적에 맞게 분리할 필요가 있다. 이 이유로 앱스토어에서 reject을 받기도함
<br/><br/>
<img src = "/post_img/201702/01/tempcache.png" />
<br/><br/>

### document(App/documents)
* 아이클라우드 백업시 자동으로 올라간다.
* 사용자 데이터를 주로 여기에 담아놓음
* 만약 앱을 삭제 했다가 다시 백업을 받고 그 앱을 다시 실행한다면 예전처럼 작동할 확률이 매우크다

### Library(App/Library)
* 클라우드 백업이 가능(Caches를 제외하면)
* 사용자 데이터와는 무관한 데이터들이 여기에 들어가게 된다.

### temp(App/tmp)
* 클라우드 백업이 되지 않는다.
* 일회성 자료들이 여기에 담기게 된다.
<br/><br/>
