---

layout: post
title: "(Swift) Navigation과 Modality"
categories: SWIFT

---

Navigation과 modality는 ios의 인터페이스 가이드 라인이다.

### Navigation

* Hierarchical navigation<br/><br/>
<img src = "/post_img/201702/01/nav1.png" />
	* 하나의 선택 → 다른 뷰로 이동, 주로 세팅이나 메일에서 이런 스타일을 갖는다.
<br/><br/>
* Flat navigation<br/><br/>
<img src = "/post_img/201702/01/nav2.png" />
	* 카테고리로 왔다 갔다 하는 스타일, 주로 앱스토어나 음악 앱에서 이런 스타일을 갖는다.
<br/><br/>
* Content-driven or experience-driven navigation<br/><br/>
<img src = "/post_img/201702/01/nav3.png" />
	* 자유롭게 이동이 가능, 일반적인 앱들이 이런 패턴을 갖는다.

### 그리고 권장하는 내용..
* 사람들이 다음 path로 어떻게 갈지 명확, 논리적, 예측가능하게 쉽게 구성을 해야 한다.
* swipe 같은 제스쳐 효과를 이용하자!
* navigation 요소를 사용해서 구성하자! 유저들은 이미 이것에 친숙하다.
* 그리고 navigation bar에는 title을 보여주면서 현재의 위치와 이전 위치를 명확하게 하는게 좋을 것 같다.
* 날씨 같은 페이지 구성은 같고 내용이 위치에 따라 변하는 경우에는 page control을 이용하자.

### Page Control은 뭐지?
<img src = "/post_img/201702/01/nav4.png" /><br/><br/>
이런 형태의 뷰는 웹에서 이미 구현해 봤을터..이런 형태의 뷰 구성을 PageControl이라고 한다. UIPageControl을 이용하면 쉽게 구현이 가능하다고 한다.

### 이 내용을 발견한 블로그에서 주운 내용(개발과는 멀고도 가까운 이야기)
* 앱을 제작할 때 고민하는 것중에 하나는 이 앱을 사용자들에게 어떻게 각인 시킬까에 대한 것이다.
* 이에 대한 고민해결책으로 Coachmark와 walkthrough 같은 기법을 사용한다고 함.
* 코치마크는 해당부분만 하이라이트를 주고 텍스트로 된 도움말을 덧붙이며 안내를 하는 방식을 말한다
* walkthrough는 앱에 강점을 표현하거나 컨셉등을 소개할 때 코치마크보다 더 다양하게 보여주는 방식임. 이때 PageControl을 이용해서 앱을 더 자세히 보여주거나 다른 방식을 써서 강점을 보여주는 방식이다.
* 이러한 것에 문제점은 유저들에 진입장벽을 느끼게 할 수도 있다.

### Modality

* Modal은 예를 드는게 더 편할 것 같다.
<img src = "/post_img/201702/01/nav5.png" /><br/><br/>
* Modal 방식
<img src = "/post_img/201702/01/nav6.png" /><br/><br/>
<img src = "/post_img/201702/01/nav7.png" /><br/><br/>
	* 적절한 modal 방식을 찾아 선택한다

### 그리고 권장하는 내용..
* modality의 사용은 최소화 하자. 꼭 필요로 할 때만!
* modal을 안정적이게 나가게 해야하는 방안이 꼭 필요하다!
* 복잡한 정보를 얻는 방안으로는 modal은 적절한 방안이 아니다
* 제목을 명시해 꼭 이 modal이 의미하는게 뭔지 나타내자
* popover위에 modal은 적절하지 않다.

#### 참조
* https://developer.apple.com/ios/human-interface-guidelines/interaction/navigation/
* https://developer.apple.com/ios/human-interface-guidelines/interaction/modality/
* https://minieetea.com/2014/01/archives/1253

<br/><br/>
