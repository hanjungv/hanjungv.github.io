---

layout: post
title: "(CSS) 마크업 개발 레벨 테스트 질문 by Toby Yun"
category: CSS

---

> [http://tobyyun.tumblr.com/](http://tobyyun.tumblr.com/) 에서 나오는 면접질문들을 간단하게 정리해 보았다.

## HTML
1. Doctype을 사용하지 않을 때는 무슨 일이 발생할까요?
2. 웹표준에 맞게 작업할 때 b, i 태그 대신 적합한 태그는 각각 무엇일까요?
  * `<strong>`, `<em>`
3. block 요소와 inline 요소에 해당하는 태그들을 각각 5개씩 적어보세요.
  * p, section, footer, header, form, ul, li,..
  * strong, em, span, img, select, ..
4. blockquote 태그는 어떤 용도로 사용해야 할까요?
5. 인라인 스타일(style=“property:value”)을 가급적 사용하지 말아야 할 이유는 무엇일까요?
  * 후에 유지보수 할 때 우선순위 파악이 힘들어짐
6. myPhoto.jpg 파일을 img 태그로 작성해보세요.
  * `<img src = "myPhoto.jpg" alt = "myphoth"/>`
7. HTML에서 id 속성을 사용하는 이유와 주의 할 점은 무엇일까요?
8. ‘TopArea'라는 클래스명이 좋지 않은 이름이라면 그 이유는 무엇일까요?
  * `hypen(-)`을 이용하자
9. 'blue-box'라는 클래스명이 좋지 않은 이름이라면 그 이유는 무엇일까요?
10. HTML5에 새롭게 추가된 aside 태그는 어떤 용도로 사용해야 할까요?
11. input 태그와 항상 함께 사용해야 할 태그는 무엇일까요?
  * label, button
12. 모바일 웹 또는 반응형웹디자인 프로젝트에서 각 기기에 적합한 화면을 보여주기 위해 필요한 meta 태그는 무엇일까요?
  * `<meta name = "viewport" content = "width = device-width">`

## CSS
1. 화면 상에는 보이지 않으나, 스크린 리더에서 읽혀야 하는 요소에 주어야 할 스타일링을 작성해보세요.
2. float 속성을 가진 자식을 품은 부모요소는 높이 값이 0이 되는 때가 있습니다. 이 현상을 해소하는법(clearing)을 알고 있나요?
3. border-box와 content-box의 차이점은 무엇일까요?
  * box-sizing에는 border-box와 content-box, padding-box가 있다.
  * content-box가 디폴트, content-box에는 height, width에 content만 포함한다. 패딩이 늘어날 경우 늘어난다.
  * padding-box는 width 와 height 속성이 padding 을 포함한다. border, margin 은 포함하지 않는다.
  * border-box margin을 제외한 값이 적용된다. IE
4. position: relative는 어떤 경우에 사용 하나요?
5. CSS Reset은 무엇이며 왜 사용할까요?
  * 크로스 브라우징을 하기 위해 사용
  * 각 브라우저마다 다르게 적용되는 css를 적용하기 위해 사용됨
  * http://cssreset.com/
6. Sass, less, Stylus와 같은 CSS 프리프로세서를 사용해본적이 있나요?
  * 아니옹! 써보겠습니다
7. id, class, inline style, !important를 우선순위 순으로 나열해보세요.
  * !impotrant / inline style / id / class 순서이다.
8. CSS에서 상속이 되는 속성을 2개만 꼽아보세요.
  * color, font-size, text-align, line-height
  * padding, width, height, margin, position 등은 상속 되지 않는다.
9. Sprite image 기법을 사용하는 이유는 무엇일까요?
  * 
10. Sprite image 기법을 사용하는데 필요한 CSS 속성들을 꼽아보세요.
  * 
11. 점진적 향상(Progressive Enhancement)의 뜻을 설명 할 수 있나요?
  * [http://intellegibilisverum.tistory.com/entry/%EC%A0%90%EC%A7%84%EC%A0%81-%EA%B8%B0%EB%8A%A5-%ED%96%A5%EC%83%81](http://intellegibilisverum.tistory.com/entry/%EC%A0%90%EC%A7%84%EC%A0%81-%EA%B8%B0%EB%8A%A5-%ED%96%A5%EC%83%81)
12. 웹폰트를 적용하기 위해서는 어떤 확장자의 폰트 파일들이 필요할까요?
  * .eot / .woff / .ttf /.svg
  * .eot는 ie4~ie8 까지 지원
  * .woff는 ie9~, 타브라우저도 지원
13. 개발사 접두어(vendor prefix)를 꼭 사용해야 할 CSS 속성(property)를 2개만 꼽아보세요.
14. 반응형웹디자인의 3가지 요소를 꼽아보세요.
  * Fluid grid
  * flexible image
  * media query
15. 모바일기기를 대응할 때 기준으로 삼는 해상도 사이즈는 몇이며 그 이유는 무엇인가요?
  * http://www.nextree.co.kr/p8622/
16. :first-child와 :last-child가 지원하는 IE의 버전명을 적어보세요.
  * first : IE 7.0
  * last : IE 9.0
17. 포토샵(또는 다른 그래픽툴)에서 이미지를 자를 때 어떤 기능을 사용하나요? (메뉴명, 단축키 등)
18. jpg, gif, png의 차이점을 설명해보세요.
  * jpg : 손실압축
  * png : 비손실압축, 용량이 다른 것에 비해 크다.
  * gif : 비손실압축, 색이 단색인 곳에 좋다. 하지만 색이 다양한 사진의 경우 손실이 큼
19. 가상컨텐츠(:before, :after)는 어떤 용도로 사용할까요?
20. 블럭요소 안의 어떤 자식 요소를 정중앙에 놓는 방법을 알고 있습니까?
  * margin:0 auto;
21. box-model이란
  * margin - border - padding - content
22. display에 대해 설명
  * block : p, header,footer,section 등등, 가로 길이가 100%가 됨
  * inline : span, 단락 내에서 해당 단락의 흐름을 방해하지 않고 작성됨
  * inline-block : block으로 만들어지나 inline처럼 배치

<br/><br/>