---

layout: post
title: "(SWIFT) Swift Syntax[1]"
categories: SWIFT

---

#### SYNTAX에 관한 글은 모두 이 [유다시티 인강(Learn Swift Programming Syntax )](https://classroom.udacity.com/courses/ud902/lessons/4667459037/concepts/46437489340923)에서 나왔습니다.

#### 기본적인 내용은 뛰어넘겠습니다. 다른 언어와의 다른점, 사용법에 중점을 두겠습니다.

### Type
* float
* Double
* Int
* Bool : bool 형은 C++이나 C, Objective-C처럼 0, 1로 할당 할 수 없다.

### Operator
* if - else : else를 if 중괄호 닫은 다음에 쓰는것이 올바른 swift 표기법이라 함

```Objective-C
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

* OR(||), AND(&&)는 C와 사용법이 같다.

```Objective-C
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
