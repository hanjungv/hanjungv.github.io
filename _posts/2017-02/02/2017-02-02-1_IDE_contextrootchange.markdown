---

layout: post
title: "(IDE) 이클립스에서 context root 변경 '/'"
category: IDE

---

프로젝트 properties에서 web project settings으로 이동<br/>
→ context root 를 / 로 변경<br/>
→ 메뉴 — 프로젝트 — 클린<br/>
→ server뷰에서 tomcat선택, +펼침, 해당프로젝트 선택 후 삭제<br/>
→ server뷰에서 tomcat선택, -마우스 우클릭, clean<br/>
→ server뷰에서 tomcat선택, -마우스 우클릭, add and remove<br/>
→ 해당프로젝트 선택 후 Add<br/>
<br/>
**
사실 그냥 새로 만들고 만들때 재설정하는게 제일 편한것같다.<br/>
처음 프로젝트를 만들 때 마지막 설정 하는 부분에 context root를 설정 하는 부분에 */* 로 설정한다.
**
<br/><br/>
