---

layout: post
title: "(SWIFT) Swift Syntax[1]"
categories: SWIFT

---

#### SYNTAX에 관한 글은 모두 이 [유다시티 인강(Learn Swift Programming Syntax )](https://classroom.udacity.com/courses/ud902/lessons/4667459037/concepts/46437489340923)에서 나왔습니다.

##### 기본적인 내용은 뛰어넘겠습니다. 다른 언어와의 다른점, 사용법에 중점을 두겠습니다.

### Type
* float
* Double
* Int
* Bool : bool 형은 C++이나 C, Objective-C처럼 0, 1로 할당 할 수 없다.

### Operator
* if - else : else를 if 중괄호 닫은 다음에 쓰는것이 올바른 swift 표기법이라 함

```javascript
if Val == true{
    // ~ true 일 때
} else {
    // ~ false 일 때
}
// or
if Val{
    // ~ true 일 때
} else {
    // ~ false 일 때
}
// or
if !Val{
    // ~ false 일 때
} else {
    // ~ true 일 때
}
```

* OR, AND는 C와 사용법이 같다.

```javascript
if val1 || val2{
    // or 해당될 떄
} else {
    // or 해당 안 될 때
}
if val1 && val2{
    // and 해당될 떄
} else {
    // and 해당 안 될 때
}
```

### String
* 기본적인 String은 struct형으로 구성되어있다.
* 형을 강제하지 않는다면 이전에 사용하던 스위프트는 Objective-C에서 나온 NSString class와 자유자제로 넘나들 수 있다.
* 그 말은 수많은 편리한 메서드드 사용할 수 있다.

```javascript
//e를 3으로 바꿔라
let newPassword = password.replacingOccurrences(of: "e", with: "3")
//for문 이용하기
let str1 = "helloworld"
for cha in str1.characters{
    if cha == 'o'{
        print("It's ")
    }
}
//등등 많은 메서드들이 있음
```

### Constant & Variable
* let은 상수, var는 변수
* 스위프트에서는 예민하다. let값을 변경할 경우 에러메세지를 띄움

<br/><br/>
