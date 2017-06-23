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

<img src = '/post_img/201706/23/1.png'/><br/>
* 위 그림처럼 bar형태의 그래프가 id가 chart인 영역에 그려졌다.
* bar 형태가 아닌 그래프는 어떤 것을 지원할까
    * "line","spline","step","area","area-spline","area-step","bar","scatter","pie","donut","gauge" 의 형태를 지원한다. 각각 이런 형태를 나타낸다.

<img src = '/post_img/201706/23/2.png'/><br/>
<img src = '/post_img/201706/23/3.png'/><br/>
<img src = '/post_img/201706/23/4.png'/><br/>
<img src = '/post_img/201706/23/5.png'/><br/>
<img src = '/post_img/201706/23/6.png'/><br/>
<img src = '/post_img/201706/23/7.png'/><br/>

* 전부 다 출력해보니 x축과 y축의 0이 맞지 않게 나오는 모습이 보인다. 일부러 그런 것 같기도 하고.. 개인적으로 수정이 필요하다 생각된다.
    * 사이트를 더 보다보니 http://c3js.org/ 를 이용했단 말이 나오는데 이 c3라는 d3의 차트라이브러리도 x,y 축을 일부러 나눈것 같은 모습을 볼 수 있었다.

* types라는 것으로 여러 데이터 타입의 형태를 다르게 할 수 있다.

```javascript
let chart = bb.generate({
    bindto: "#chart",
    data: {
        types: {
          data1: "bar",
          data2: "spline"
        },
        columns: [
            ["data1", 30, 200, 100, 170, 150, 250],
            ["data2", 130, 100, 140, 35, 110, 50]
        ]
    }
});
```

<img src = '/post_img/201706/23/8.png'/><br/>
* 이런식의 그림을 볼 수 있다.



<br/><br/>
