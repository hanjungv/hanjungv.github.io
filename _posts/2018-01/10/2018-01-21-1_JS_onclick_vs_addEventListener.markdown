---

layout: post
title: "(JS) addEventListener() vs onclick()"
category: JS 

---

## 이 글을 작성하게 된 계기
지난 1월 18일에 있었던 김성호 선임님이 해주신 자바스크립트 강의를 들으면서 직접 질문했었던 궁금한 점을 다시 정리해 보려고 작성하였습니다. 잘못된 내용이 포함되어 있을 수 있으니 지적 환영합니다!

## 여기서 말하는 `onclick`과 `addEventListener`이란?
```js
document.getElementById('trigger').onclick = () => {
    alert('hello!');
}
```
이런식으로 trigger라는 아이디를 가진 객체를 찾아 클릭시 이벤트를 발생 시키는 방식입니다. 비슷한 메서드로 `onmouseover()`, `onkeydown()` 등등이 있을 것입니다.
```js
document.getElementById('trigger').addEventListener('click',()=>{
    alert('hello!');
},false);
```
`addEventListener()`또한 위 메서드와 비슷하게 어떤 이벤트가 있으면 어떤 행동을 취할 지 함수를 작성하게 됩니다. 둘 다 비슷하게 동작하는데 왜 `addEventListener()`로 작성하는 방식이 모던한 방식일까요?

## 왜 `addEventListener()`로 작성하는 방식이 모던할까?
### 1. 여러 개의 이벤트를 overwrite할 수 있다.
둘의 차이를 물을 때 가장 많이 나오는 예제이다.
overwrite라고 말을 작성하니 조금 애매한 느낌이 있으니 예제를 살펴보자
```js
let obj = document.getElementById('trigger');
let do1 = () => {
    alert("do1");
};
let do2 = () => {
    alert("do2");
};
obj.onclick = do1;
obj.onclick = do2;
```
위 예제에서는 `do1` 함수는 작동하지 않을 것이다. `do2`를 작성하면서 `do1`은 작동하지 않게 된 것이다. `addEventListener()`는 어떻게 작동할 까

```js
obj.addEventListener('click', do1, false);
obj.addEventListener('click', do2, false);
```
이렇게 쓸 경우 do1과 do2 모두가 작성 순서대로 작동하게 된다.
한 클릭이 일어났을 때 여러가지 일이 동작하게 하고 싶다면, 하지만 함수는 분리되어 있다면 addEventListener로 작성하는 것이 필요할 것이다.

### 2. 작성 중에 bubbling, capturing을 설정할 수 있다.
클릭 시 이 함수가 버블링으로 작동할지 캡쳐링으로 작동할지 작성시 판단할 수 있다. 메서드를 잘 보게 되면 `addEventListener("type", 리스너(작동될 함수), 캡쳐링을 쓸지)`가 들어가게 된다. 세번째 parameter가 true일 경우 캡쳐링을 쓴다. false일 경우 버블링을 쓴다 라는것을 작성시 판단하면서 사용할 수 있게 됩니다.(default는 false입니다.)

### 3. 여러개의 이벤트 타입들을 쉽게 바인딩 할 수 있다.
만약 버튼을 누르거나 버튼에 마우스를 올릴 때 모두 함수를 동작하게 하고 싶다면 이렇게 코드를 작성해야 할 것이다.
```js
obj.onclick = do1;
obj.onmouseover = do1;
```
갯수가 많아질수록 관리가 힘들것이다. `addEventListener()`는
```js
['mouseover', 'click'].map(function(e) {
    obj.addEventListener(e, do1);
});
```
로 작성할 수 있다. (더 좋은 코드가 있을 수 있지만). 한 배열객체에서 이벤트 발생 type들을 관리할 수 있게 된다.

## 그럼 onclick을 사용하면서 얻을 수 있는 장점은 없을까?
실제로 [CANIUSE, https://caniuse.com/#search=addeventlistener](https://caniuse.com/#search=addeventlistener)를 확인해 보면 onclick은 모든 버전의 브라우저를 지원하지만 addEventListener는 IE 6,7,8버전을 지원하지 않는 것을 볼 수 있었습니다. 

## 결론은?
인라인으로 작성할 때 얻을수 있는 여러가지 편리함들이 있을 수 있겠지만 제가 김성호 선임님에게 어느것이 더 나은 방식일까 물어봤을 때 선임님께서는 "onclick()으로 얻을 수 있는 장점이 물론 있겠지만 addEventListener()를 사용해서 얻는 장점에 비하면 너무 적을 것 같다." 라고 말해주셨습니다. 

## 참조
* [링크, stackoverflow addeventlistener vs onclick](https://stackoverflow.com/questions/6348494/addeventlistener-vs-onclick)


<br/><br/>
