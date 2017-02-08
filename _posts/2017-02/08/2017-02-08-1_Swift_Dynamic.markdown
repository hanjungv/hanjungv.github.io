---

layout: post
title: "(Swift) Dynamic modifier"
category: SWIFT

---

### Dynamic modifier(선언변경자)
* Objective-C 에서는 클래스의 메서드를 호출하거나 프로퍼티를 참조하는것을 **함수호출** 이라 하지않고 **메세지 디스패치** 라고 함
    * 과정 : 호출자는 메세지를 전달(이런 메서드를 부를 것) -> 메세지를 참조하고 클래스 코드를 찾아감
* 여기서 동적 dispatch와 정적 dispatch가 등장, 특성에 맞게 선택한다.
    * 정적 dispatch
        * 컴파일 타임에 이미 어떤 클래스가 호출될 지 알고 있음.
        * 최적화가 가능해진다.
    * 동적 dispatch
        * 런타임 과정에 어떤 클래스를 호출할지 정함.
        * 런타임과정에 구현된 코드를 수정해 버릴 수 있다.
        * 속도 저하의 요소가 될 수 있다.
* dynamic modifier를 이용하면 동적 dispatch가 가능해지게 된다.

```javascript
class MyClass {
    dynamic var imADynamicallyDispatchedString: String
    dynamic func imADynamicallyDispatchedFunction() {
        //여기의 구현 코드는 동적 디스패치로 호출됩니다.
    }
}
```
#### Realm에서 dynamic을 꼭 사용해야 하는가?
* [realm docs](https://realm.io/docs/swift/latest/#property-attributes)를 봐보자

> **Realm model properties need the dynamic var attribute in order for these properties to become accessors for the underlying database data.**<br/><br/>
There are two exceptions to this: List and RealmOptional properties cannot be declared as dynamic because generic properties cannot be represented in the Objective-C runtime, which is used for dynamic dispatch of dynamic properties, and should always be declared with let.

 <br/><br/>
