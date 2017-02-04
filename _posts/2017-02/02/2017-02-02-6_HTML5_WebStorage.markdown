---

layout: post
title: "(HTML5) WebStorage"
categories: HTML

---

### WebStorage 이란?

* HTML5부터 지원
* 브라우저 자체에서 데이터를 저장할 수 있는 객체를 제공
* LocalStorage와 SessionStroage. LocalStorage는 브라우저가 꺼져도 데이터가 소멸되지 않음. 세션은 사라짐
* 쿠키는 4kb의 저장공간. 웹스토리지는 브라우저마다 다르지만 5MB정도를 지원한다.
* 다른 도메인끼리 공유는 불가능하다.
* 만료시간은 따로 설정 할 수 없다.

#### 간단한 예제

```html
// 데이터 조회
localStorage.setItem("foo","bar"); //setItem
localStorage.foo = "bar" //객체에 직접 접근
localStorage["foo"] = "bar" //dictionary

//모든 데이터 삭제
localStorage.clear()

//Array, Object 저장
var bar = {
    foo1: "bar1",
    foo2: "bar2",
    foo3: "bar3"
}
localStorage.setItem("foo",JSON.stringify(bar)); // 스트링 형태로 저장해야함

//꺼낼때
var bar = localStorage.getItem("foo");
JSON.parse(bar); // 파싱
```

<br/><br/>
