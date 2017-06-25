---

layout: post
title: "(JS) Billboard.js 사용해보기"
category: JS

---

## Billboard.js란
* 링크 : [https://naver.github.io/billboard.js/](https://naver.github.io/billboard.js/)
* 도큐먼트 : [https://naver.github.io/billboard.js/release/latest/doc/index.html](https://naver.github.io/billboard.js/release/latest/doc/index.html)
* 네이버에서 만든 차트 라이브러리이다.
* d3.js 기반이라고 한다.[https://d3js.org/](https://d3js.org/)
* d3.js란?
    * ㅇㅇ

### 설치법
d3.js기반이기에 이를 먼저 로드 시켜줘야 한다. 그리고 다운 받은 js, css 파일을 폴더에 포함시켜 로드시킨다.

```html
<!--d3js CDN-->
<script src="https://d3js.org/d3.v4.min.js"></script>
<!--다운 받아서 포함 시키기-->
<link rel="stylesheet" href="/css/billboard.css">
<script src = "js/billboard.js"></script>
```


### 사용법
* 사용법은 다른 그래프 라이브러리처럼 바인딩할 하나의 division을 만들고 그 곳에 차트를 만들게 된다. 사이트에 있는 예제를 하나 사용해 보면

```html
<body>
  <head>
    <title>billboard</title>
    <script src="https://d3js.org/d3.v4.min.js"></script>
    <link rel="stylesheet" href="/css/billboard.css">
    <script src = "js/billboard.js"></script>
  </head>
  <body>
    <div id="chart"></div>
  </body>
</body>
<script>
var chart = bb.generate({
    bindto: "#chart",
    data: {
        type: "bar",
        columns: [
            ["data1", 30, 200, 100, 170, 150, 250],
            ["data2", 130, 100, 140, 35, 110, 50]
        ]
    }
});
</script>
```

<img src = '/post_img/2017-06/23/1.png'/>



<br/><br/>