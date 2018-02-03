---

layout: post
title: "(JS) arrow function(화살표 함수)의 장점은 무엇일까?"
category: JS 

---

## 이 글을 작성하게 된 계기
습관적으로 사용하는 Arrow function은 과연 어떤 장점들을 가지고 있는지 한번 정리해 보고 싶었습니다.

## 먼저 Arrow function는 뭐고 어디에 썼을까
기존 함수 선언을 화살표(`=>`)를 통해 선언해 줍니다. 
```js
(param1, param2, …, paramN) => expression
                        //  => { return expression } 과 동일한 의미입니다.
(param1 = value1, param2, param3 = value2) => { statements }

// 즉시 실행 함수는 
(function(){
    //expression;
}());

(() => {
    //expression
})()
```

## Arrow funciton의 장점은 무엇일까?
1. 짧은 함수를 작성할 수 있게 됩니다. 밑 예제같은 콜백함수를 작성할 때 간결하겠네요.
2. 
```js
let a = ["a","b","c","d"];
let b = a.map(function(s){return s.length});
let c = a.map((s)=>s.length());
let d = a.filter((item, index) => index % 2);
```

2. 기존 자바스크립트에서 this는 dynamic scoping 이 되었는데 이 경우 lexical scoping을 사용하게 된다. 고로 따로 binding을 사용하지 않아도 된다. 정리하면 `자신만의 this를 생성하지 않고 자신을 포함하고 있는 context의 this를 이어 받습니다`.
* ES5 의 bind 예를 살펴 보면

```js
function Prefixer(prefix) {
  this.prefix = prefix;
}

Prefixer.prototype.prefixArray = function (arr) {
  return arr.map(function (x) {
    return this.prefix + ' ' + x;;
  }.bind(this)); // this: Prefixer 생성자 함수의 인스턴스
};

var pre = new Prefixer('Hi');
console.log(pre.prefixArray(['Lee', 'Kim']));
```

* 위 코드를 ES6의 Arrow function을 사용하면

```js
function Prefixer(prefix) {
  this.prefix = prefix;
}

Prefixer.prototype.prefixArray = function (arr) {
  return arr.map(x => `${this.prefix}  ${x}`);
};

const pre = new Prefixer('Hi');
console.log(pre.prefixArray(['Lee', 'Kim']));
```

훨씬 직관적이고 간결하게 쓸 수 있다.

## lexical scope란?
렉시컬 스코프란 `소스코드가 작성된 그 문맥`에 결정된다고 합니다. 현대 프로그래밍 대부분 언어는 렉시컬 스코프 규칙을 따르고 있다고 합니다.
가장 많이 언급되는 예제라고 하는데

```js
var x = 'global';
function foo(){
    var x = 'local';
    bar();
}
function bar(){
    console.log(x);
}
foo(); // global
bar(); // global
```

렉시컬 환경의 대응표(환경 레코드)에서 변수를 찾아보고, 없다면 바깥 렉시컬 환경을 참조하여 찾아보는 식으로 중첩 스코프가 가능해진다고 합니다. 

## Arrow function은 어느곳에 사용하면 안될까?
1. 번외이지만.. 가장 먼저 IE환경에서 아직 제공하지 않습니다. 쓰려면 babel과!
<img src="../../../post_img/201802/03/1.PNG"/><br/>
2. 메소드

```js
const obj = {
    name: "han",
    hi: () => console.log(`Hi ${this.name}`)
};
obj.hi(); // Hi undefined
```

위 bind의 설명했을 때와 같이 이 경우 호출한 객체에 바인딩되는 것이 아닌 전역객체에 바인딩 된다. 이때는 이렇게 축약표현을 작성하는 것이 좋다고 합니다.

```js
const obj = {
    name: "han",
    hi(){ 
        console.log(`Hi ${this.name}`);
    }
};
obj.hi(); // Hi undefined
```

3. prototype
이 때는 메소드가 아닌 일반 함수가 할당 된다. 고로 기존처럼 작성해야 한다.

```js
const obj = {
  name: 'Lee',
};
Object.prototype.hi = () => console.log(`Hi ${this.name}`);
obj.hi(); // Hi undefined

// 이게 옳은 표현이라고 한다.
Object.prototype.sayHi = function() {
  console.log(`Hi ${this.name}`);
};
```

4. 생성자
생성자 함수는 prototype 프로퍼티를 갖지만 arrow function은 prototype 프로퍼티를 갖지 않는다고 합니다. 고로 사용할 수 없다!

5. addEventListener
이 경우 this가 상위 컨택스트를 가리 킨다고 합니다. 고로 이전처럼 function(){}으로 사용하는 것이 옳은 표현입니다. 

```js
button.addEventListener('click', () => {
  console.log(this === window); // => true
  console.log(this === button); // => false
});

button.addEventListener('click', function() {
  console.log(this === window); // => false
  console.log(this === button); // => true
});
```

## 결론은?
편리하지만 용도에 맞춰서 작성하는 것이 좋을 것 같다. 그리고 빠르게 변화하는 사항이니 이후에 어떻게 변화되는지 계속되서 주목할 필요가 있는 것 같습니다. 

## 참조
* [링크, MDN.화살표 함수란?](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Functions/%EC%95%A0%EB%A1%9C%EC%9A%B0_%ED%8E%91%EC%85%98)
* [링크, 언제 화살표 함수를 사용하면 안될까?](https://dmitripavlutin.com/when-not-to-use-arrow-functions-in-javascript/)
* [링크, 자바스크립트의 스코프와 클로저](http://meetup.toast.com/posts/86)
* [링크, arrow function](http://poiemaweb.com/es6-arrow-function)

<br/><br/>
