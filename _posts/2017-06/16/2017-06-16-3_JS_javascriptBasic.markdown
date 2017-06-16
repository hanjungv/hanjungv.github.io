---

layout: post
title: "(JS) Javascript 베이직"
category: JS

---

### scope chain
자바스크립트 변수는 ES6에서 블록 레벨을 지원하기 전까지는 주로 함수 단위의 scope를 갖는다고 합니다. 내부함수에서 외부 함수의 변수를 사용하려면 클로저를 이용하면 된다고 합니다. 가급적이면 자바스크립트에서는 전역변수의 사용을 막고 있습니다.

#### 스코프 체인이란?
* 각 함수 내에 유효범위를 나타내는 [[scope]]가 리스트로 관리되게 되는데 이를 '스코프 체인'이라 한다.
* 중첩함수일 때 상위함수의 유효범위까지 흡수하는 것을 말합니다. 즉, 하위함수가 실행되는 동안 참조하는 상위 함수의 변수 또는 함수의 메모리를 참조하는 것입니다. 

```javascript
let x = 10;
(function foo(){
    let y = 20;
    (function bar(){
        let z = 30;
        console.log(x+y+z);
    })();
})();
```
<img src = '/post_img/201706/16/1.png'/><br/>
* inner함수가 실행 되었지만 outer, global의 변수를 사용할 수 있게 된다.

* 참조 : http://heeestorys.tistory.com/687

### 호이스팅
* 호이스트란, 변수의 정의가 그 범위에 따라 선언과 할당으로 분리되는 것을 의미합니다. 모든 변수 선언은 호이스팅 됩니다.
* hoist라는 단어를 생각해보면 "끌어올리다"라는 단어로 나타내집니다.

#### 변수 호이스팅

```javascript
function hoist(){
	console.log(a); //undefined
	var a = 10;
	console.log(a); //10
}
```
* var는 호이스팅이 된다. 다른 언어같으면 에러를 뱉어야 하는 시점에 자바스크립트는 undefined를 나타내게 된다.
```javascript
function hoist(){
	var a;
    console.log(a); //undefined
	a = 10;
	console.log(a); //10
}
```
* 이렇게 작동하게 된다. 하지만 ES6에서 나오게 된 let과 const는 호이스팅을 지원하지 않게 된다. 이로써 좀 더 직관적이게 사용할 수 있게 된 것 같다.
```javascript
function hoist(){
	console.log(a); // a is not defined
	let a = 10;
	console.log(a);
}
```

#### 함수 호이스팅

```javascript
console.log(add(2,3));  //5
function add(a,b){
    return a+b;
}
console.log(add(2,3));  //5
```
* 함수가 먼저 선언되지 않았는데도 5가 정상적으로 출력이 된다. 호이스팅 때문이다. 이러한 코드는 혼란을 줄 수 있다.
```javascript
console.log(add(2,3));  //add is not defined
let add = function(a,b){
    return a+b;
}
console.log(add(2,3));  //5
```
* 이런식으로 작성을 하게 되면 좀 더 명확하게 코딩을 할 수 있게 된다.
* 참조 : http://programmer-seva.tistory.com/24

### closures란?
* 내부함수가 외부함수의 맥락에 접근 할 수 있는것을 의미한다.
* 클로저는 독립적인 (자유) 변수를 가리키는 함수이다. 또는, 클로저 안에 정의된 함수는 만들어진 환경을 ‘기억한다’.
* 클로저를 통해 내부 변수를 참조하는 동안에는 내부 변수가 차지하는 메모리를 GC가 회수하지 않는다. 따라서 클로저 사용이 끝나면 참조를 제거하는 것이 좋다.

```javascript
function outter(){
    let title = "coding everyday";
    function inner(){
        console.log(title);
    }
}
let ff = outter();  //outter의 생명은 이미 끝났는데
ff();   // inner에서 title에 접근을 할 수 있게 됨
```

* private 변수처럼 사용할 수 있게 된다. 변수를 외부에서 접근할 때 안전하게 사용할 수 있다.

```javascript
function factory_movie(title){
    return {
        get_title : function (){
            return title;
        },
        set_title : function(_title){
            title = _title
        }
    }   // return 값으로 객체를 return 하고 속성으로 두가지 함수를 리턴한다.
}
ghost = factory_movie('Ghost in the shell');
matrix = factory_movie('Matrix');
 
alert(ghost.get_title());
alert(matrix.get_title());
 
ghost.set_title('공각기동대');
 
alert(ghost.get_title());
alert(matrix.get_title());
```

* 클로저를 사용하는데 있어서 가장 발생하기 쉬운 에러이다.
```javascript
var arr = []
for(var i = 0; i < 5; i++){
    arr[i] = function(){
        return i;
    }
}
for(var index in arr) {
    console.log(arr[index]());  //5,5,5,5,5 
}
```
* 5가 5번 출력되는 이유는 i가 외부함수의 변수로 인식
```javascript
var arr = []
for(var i = 0; i < 5; i++){
    arr[i] = function(id){  //외부함수에서 가지고 오게 됨, 이 함수가 만들어지는 시점에 i값을 id로 가지고 있어서 수행할 수 있게 됨
		return function(){
			return id;  //내부 함수의 변수인 id를 
        }
    }(i);
}
for(var index in arr) {
    console.log(arr[index]());  //0,1,2,3,4
}
```

* 블**에서 풀었던 문제가 그대로 moz에 있어서 가지고 와봤다.

```javascript
function showHelp(help) {
  document.getElementById('help').innerHTML = help;
}
function setupHelp() {
  var helpText = [
      {'id': 'email', 'help': 'Your e-mail address'},
      {'id': 'name', 'help': 'Your full name'},
      {'id': 'age', 'help': 'Your age (you must be over 16)'}
    ];

  for (var i = 0; i < helpText.length; i++) {
    var item = helpText[i];
    document.getElementById(item.id).onfocus = function() {
      showHelp(item.help);
    }
  }
}
setupHelp();
```
* 이 코드가 input태그에 따라 경고문이 바뀌게 되어야하는데 age로 전부 나오게 된다.
```javascript
function showHelp(help) {
  document.getElementById('help').innerHTML = help;
}
function setupHelp() {
  var helpText = [
      {'id': 'email', 'help': 'Your e-mail address'},
      {'id': 'name', 'help': 'Your full name'},
      {'id': 'age', 'help': 'Your age (you must be over 16)'}
    ];

  for (var i = 0; i < helpText.length; i++) {
    var item = helpText[i];
    document.getElementById(item.id).onfocus = function(helpText) {
      return function(){
        showHelp(helpText.help);
      }
    }(item);
  }
}
setupHelp();
```
* 이런식으로 외부함수의 변수를 파라미터로 받아 내부함수에서 접근하게 할 수 있다.
```javascript
function showHelp(help) {
  document.getElementById('help').innerHTML = help;
}
function makeHelpCallback(help) {
  return function() {
    showHelp(help);
  };
}
function setupHelp() {
  var helpText = [
      {'id': 'email', 'help': 'Your e-mail address'},
      {'id': 'name', 'help': 'Your full name'},
      {'id': 'age', 'help': 'Your age (you must be over 16)'}
    ];

  for (var i = 0; i < helpText.length; i++) {
    var item = helpText[i];
    document.getElementById(item.id).onfocus = makeHelpCallback(item.help);
  }
}
setupHelp();
```
* 아니면 이런식으로 새로운 함수를 만들어서 접근해도된다.
```javascript
function showHelp(help) {
  document.getElementById('help').innerHTML = help;
}
function setupHelp() {
  var helpText = [
      {'id': 'email', 'help': 'Your e-mail address'},
      {'id': 'name', 'help': 'Your full name'},
      {'id': 'age', 'help': 'Your age (you must be over 16)'}
    ];

  for (var i = 0; i < helpText.length; i++) {
    let item = helpText[i];
    document.getElementById(item.id).onfocus = function() {
      showHelp(item.help);
    }
  }
}
setupHelp();
```

* let을 사용하게 되면 블록범위로 변수를 할당하여 접근이 쉬워지게 된다. 위 코드도 전부 let으로 바꿔 주기만 하면

```javascript
let arr = []
for(let i = 0; i < 5; i++){
    arr[i] = function(){
        return i;
    }
}
for(let index in arr) {
    console.log(arr[index]());  //0,1,2,3,4
}
for(let i=0; i<5; i++){
    arr[index] = null;  //해제
}
```

* 정상작동한다.
* 참조 : https://opentutorials.org/module/532/6544

### prototype chaining
* ES6전까지 JS에는 class가 존재하지 않았다. 자바스크립트의 모든 Object는 prototype이란 다른 Object를 가리키는 링크를 갖고 있는데 이 Object의 연쇄를 prototype chaining이라고 합니다. 
* 객체의 생성 과정에서 모태가 되는 프로토타입과의 연결고리가 이어져 상속관계를 통하여 상위 프로토타입으로 연속해서 이어지는 관계를 프로토타입 체인이라고 한다. 이 연결은 __proto__ 를 따라 올라가게 된다.

### namespace
* 공부해서 채우자ㅠㅠ



<br/><br/>