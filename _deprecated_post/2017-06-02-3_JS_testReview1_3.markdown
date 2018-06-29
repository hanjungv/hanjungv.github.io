---

layout: post
title: "(JS) 2017.05.30에 있었던 어느 한 시험에 대한 복기"
category: JS

---

### 개요
* 17년 5월 30일 모 기업 프론트엔드 시험이 있었다.
* 여실히 나의 실력을 복기할 수 있었던 좋은 기회같았다.
* 탈락이 예상되지만 복습을 해서 부족한 점을 채워야 다음에 기회가 왔을때 안놓치겠지
* 부족했다고 생각하는 점을 정리해보면
    1. WebStorage를 공부했었지만 막상 쓸라하니 넘나 새로웠다!
    2. JS에서 시계를 출력할 때 어떻게 할 지 넘나 우왕좌왕(하..)
    3. 게시판 CRUD 생성과 생성 알고리즘에 대해 고민만 하다 구현은 못한점
    4. JavaScript, jQuery 코드가 깔끔하지 못했다.
    5. GMT...GMT....

### Moment JS를 사용하기
시계는 GMT+9로 출력이 되었어야 했고 추가와 삭제가 되었어야 했다. 시험때 사용했던 코드를 살짝 보면..

```javascript
var stdTime = [9];
function eraseClock(id){
  stdTime[id] = -999;
}
$(document).ready(function(){
    //render Time
    function startTime() {
      var today = new Date();
      for(var i = 0; i<stdTime.length; i++){
        var standardTime = Number(stdTime[i]);
        if(standardTime == -999) {
          $("#clock"+i).html("");
          continue;
        }
        var h = (Number(today.getHours()) + standardTime -9)%24;
        var m = today.getMinutes();
        var s = today.getSeconds();
        m = checkTime(m);
        s = checkTime(s);
        $("#clock"+i).html(h + ":" + m + ":" + s + "<span style = 'font-size:20px;'>(기준: GMT+"+standardTime+")</span><button id = 'erase"+i+"' class = 'btn btn-default' onClick = 'eraseClock("+i+")'>erase</button>");
      }
      var t = setTimeout(startTime, 500);
    }
    function checkTime(i) {
      if (i < 10) {i = "0" + i};
      return i;
    }
    startTime();
    // create button click
    $("#createClockBtn").click(function(){
      var gmt = $("#standardTime").val();
      var len = stdTime.length;
      $("#clock").append("<div class = 'clock"+len+"' id = 'clock"+len+"'></div>");
      stdTime.push(gmt);
    });
});
```

* 하.. 아무리 봐도 이쁜 코드는 아니다. 그래도 작동은 잘 되니..
* 현재시간을 Date로 불러와 시간, 분, 초를 나눈다. 라이브러리를 사용하지 않으니 매우 꽤 노가다성이 짙고 정확도 또한 떨어질 것 같다.

<img src = '/post_img/201706/02/2.png'/>
<img src = '/post_img/201706/02/3.png'/>
* 일단 결과는 잘 나온다. 삭제도 잘되고
* 이 코드를 [moment.js, http://momentjs.com/](http://momentjs.com/)를 사용해서 만들어보자

1. moment.js를 넣고 되던 부분을 바꿔보자

```javascript
let stdTime = [9];
function eraseClock(id){
  stdTime[id] = -999;
}
$(document).ready(function(){
    //render Time
    function startTime() {
      let date = moment().format('YYYY-MM-DD, HH:mm:ss');
      for (let i = 0; i < stdTime.length; i++) {
        let standardTime = Number(stdTime[i]);
        if (standardTime == -999) {
          $("#clock" + i).html("");
          continue;
        }
        $("#clock" + i).html(moment().add(standardTime-9, 'hours').format('H:mm:ss') + "<span style = 'font-size:20px;'>(기준: GMT+" + standardTime + ")</span><button id = 'erase" + i + "' class = 'btn btn-default' onClick = 'eraseClock(" + i + ")'>erase</button>");
      }
    }
    setInterval(startTime, 500);
    let userName = localStorage.getItem("userName");
    $("#userNameShow").append(userName+"님 반갑습니다!");
    $("#createClockBtn").click(function(){
      let gmt = $("#standardTime").val();
      let len = stdTime.length;
      $("#clock").append("<div class = 'clock"+len+"' id = 'clock"+len+"'></div>");
      stdTime.push(gmt);
    });
});
```

* 많~이 짧아진 것은 아니지만 -1시가 되거나 61분등이 되는 validation문제를 라이브러리에서 알아서 해준다. add같은 함수로 매우 직관적이게 시간을 더할 수 있게 되었다.

2. 시간 크기를 비교해야 하는 순간이 온다면 어떻게 비교할 것인가
* Unix time을 이용하자. [Unix time](https://ko.wikipedia.org/wiki/%EC%9C%A0%EB%8B%89%EC%8A%A4_%EC%8B%9C%EA%B0%84)은 1970년 1월 1일 00:00:00(UTC) 부터 경과시간을 초로 나타낸 것이라 한다.
* 데이터를 저장할 때 지정 시간을 moment().format('X')를 하게되면 초 단위로 Unix time을 얻을 수 있다. 이 값으로 비교를 하면 된다.

2-1. 그럼 그 값은 input으로 어떻게 받을 것인가?
그냥 값 받아서 moment(val).format("YYYY-MM-DD, HH:mm:ss").format('X')
..

### WebStorage


<br/><br/>