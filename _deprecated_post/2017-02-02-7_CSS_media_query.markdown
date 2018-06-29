---

layout: post
title: "(CSS) Media query"
category: CSS

---

* media type은 단말기 종류에 따라 각각 다른 스타일 시트를 적용 하는 기능(CSS2.1~)
* CSS3에서 좀 더 구체적인 조건에서 필요한 스타일을 적용할 수 있도록 확장함! 이를 미디어 쿼리라 한다.

```CSS3
@media not|only (mediatype) and (media feature) {
    CSS-Code;
}
```

```html
// or
<link rel="stylesheet" media="mediatype and|not|only (media feature)" href="mystylesheet.css">
```

### media types
1. all: 모든 디바이스에 적용
2. print: printer에 사용
3. screen : 컴퓨터 스크린, 태블릿, 스마트폰 등에 쓰임..
4. speech : 스크린 리더기에 사용, 스크린 내용을 읽어주는 미디어 일때

### media features(조건문)
1. height, width : 둘 다 해당, 둘 다 미디어에 따라 다른 값들이 검출 됩니다.
2. width:320px (미디어가 320px일때)
3. max-width:320px (320px 이하의 미디어 일 때)
4. min-width:320px (320px 이상의 미디어 일 때)
5. device : device의 물리적인 값들을 기준으로(해상도와 너비는 같지 않을 수 있다0
6. device-width:320px (기기의 너비가 320px일때)
7. max-device-width:320px (320px 이하의 화면일 때)
8. min-device-width:320px (320px 이상의 화면일 때)
9. orientation : 화면 회전 width, height가 아닌 portrait, landscape값으로 구분한다. 대부분 세로로 긴 핸드폰의 형태이기 때문에 기본상태는 portrait, 가로로 돌렸을 때는 landscape. 데스크톱에는 가로 세로 개념이 없음. 그렇다고 이 개념이 모바일 개념은 아니다.
10. aspect-ratio, min-aspect-ratio, max-aspect-ratio(화면비율) : width/height
11. aspect-ratio:1 : 화면 비율이 1:1인경우
12. aspect-ratio:16/9 : 일반적인 화면 비율인 16:9를 의미합니다(1920*1080)
13. device-aspect-ratio, min-device-aspect-ratio, max-device-aspect-ratio :단말기의 물리적인 화면 비율
14. color, min-color, max-color : 단말기에서 사용하는 최대 색상 비트 수에 대응(단위는 자연수)
15. color:3 : 2³ = 8개의 색상 사용
16. color-index, min-color-index, max-color-index : 최대 색상 수에 대응
17. monochrome, min-monochrome, max-monochrome : 흑백만 사용하는 단말기에서의 픽셀당 비트수, 얼마나 자유롭게 표현되는지를 확인함
18. resolution, min-resolution, max-resolution : 단말기의 해상도
19. grid : 단말기가 grid방식인지 bitmap방식인지
20. grid:1 ⇒ 문자로만 표기되는 tty, 주로 터미널, 전화액정
21. grid:0 ⇒ 대부분의 컴퓨터와 스마트폰 웹 브라우저에 해당
22. -webkit-min-device-pixel-ratio : 단말기의 화소와 실제 화면의 pixel간의 비율

```html
<!-- 아이폰4 -->
<link rel="stylesheet" media="only screen and (-webkit-min-device-pixel-ratio: 2)" type="text/css" href="iphone4.css">
<!-- 안드로이드 -->
<link rel="stylesheet" media="only screen and (-webkit-min-device-pixel-ratio: 1.5)" type="text/css" href="android.css">
```

<br/><br/>
