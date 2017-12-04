---

layout: post
title: "(ETC) D2 코딩체로 visual studio code, Eclipse, intellij 폰트 바꾸기"
category: ETC

---

> D2에서 지속적으로 코딩 폰트를 제공중에 있는걸 얼마전에 알았습니다.(ㅈㅅ!) 한글 폰트에 있어서 조금 변경이 필요하다고 느끼던 시점에 이런것들이 나오니 바로 적용을 시켜보았습니다.

## 폰트 설치하기 
1. 깃헙: [https://github.com/naver/d2codingfont](https://github.com/naver/d2codingfont)에 들어가서 (2017.11.29 에 나온 1.3버전이 최신 버전이여서 이걸 다운받았습니다.) 알집을 다운받아주세요. 8메가 정도 되네요

2. 폰트 설치하는 법은 매우 쉽습니다. 저는 Mac OS를 사용하고 있는데요 아마 제가 기억하기로는 윈도우도 똑같을 거에요. 폰트를 엽니다. <br/>
<img src="../../../post_img/201712/04/1.png" /><br/>

3. 그리고 그냥 다운받은거 전부 드래그해서 폰트가 쌓인 곳에 넣어주세요 그러면 이렇게 추가된 것을 볼 수 있습니다. 설치 끝~<br/>
<img src="../../../post_img/201712/04/2.png" /><br/>

--- 
## IDE에 적용을 해보자
사실 별거 없다. 그냥 적용하고 어떻게 보이는지 보여드리고 싶었을 뿐..

### Eclipse
1. Preference에 들어가요<br/>
<img src="../../../post_img/201712/04/3.png" /><br/>
2. General->Appearance->Colors and Fonts로 이동<br/>
<img src="../../../post_img/201712/04/4.png" /><br/>
3. Basic에 Text Font를 눌러서 바꾸자. D2Coding이 제대로 등록되어있다면 보일것이다.
<img src="../../../post_img/201712/04/5.png" /><br/>
4. 결과. 뭔가 이클립스 다운 느낌이 사라졌다. 뭔가 서브라임 같기도 하고..만족스럽다.
<img src="../../../post_img/201712/04/6.png" /><br/>

### Intellij
1. Preference에 들어가요. Editor -> Font로 이동해요<br/>
<img src="../../../post_img/201712/04/7.png" /><br/>
2. Font를 D2Coding으로 바꿔요<br/>
<img src="../../../post_img/201712/04/8.png" /><br/>
3. 결과. 음...네!
<img src="../../../post_img/201712/04/9.png" /><br/>

### VSCode
1. Preference에 들어가요. 그리고 `"editor.fontFamily": "D2Coding"`를 추가해주세요. 이렇게<br/>
<img src="../../../post_img/201712/04/10.png" /><br/>
2. 그러고 껐다 키면 결과가 나와요.<br/>
<img src="../../../post_img/201712/04/11.png" /><br/>

개인적으로 VSCode랑 Eclipse는 적용 시키는게 이쁜고 가독성도 올라가는 것 같은데 인텔리제이는 잘 모르겠어요. 아무튼 이러한 폰트 가독성을 높이는 노력들을 시도하는것은 저희같은 사람들에게 좋은 시도인것 같습니다. 


<br/><br/>
