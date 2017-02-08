---

layout: post
title: "(Swift) Swift Syntax[4/4]"
category: SWIFT

---

#### SYNTAX에 관한 글은 모두 이 [유다시티 인강(Learn Swift Programming Syntax )](https://classroom.udacity.com/courses/ud902/lessons/4667459037/concepts/46437489340923)에서 나왔습니다.

##### 기본적인 내용은 뛰어넘겠습니다. 다른 언어와의 다른점, 사용법에 중점을 두겠습니다.

#### enum & struct

> enum

```javascript
//enum 선언하는 법
    enum CaliforniaPark {
        case yosemite, deathValley, lasson, sequoia
    }
//enum값을 switch case에서 사용할 때 하나라도 case 문에서 빠지게 되면 컴파일에러가 난다.
    switch destination {
    case .yosemite:
        warning = "Beware of aggressive bears!"
    case .deathValley:
        warning = "Beware of dehydration!"
    case .lasson:
        warning = "Watch out for boiling pools!"
    //case .sequoia:
        //warning = "Watch out for falling trees!"  //compile error 발생
    }
```

> Struct

```javascript
// Struct 예시. 메서드를 가질 수도 있다.
struct Beer {
    var style = "Pale Ale"
    var percentAlcohol = 5.0
    static var cheersDict = ["English": "Cheers!","German": "Prost!", "Japanese": "乾杯", "Mandarin": "干杯!","Russian":"На здоровье!", "Spanish":"Salud!", "Italian": "Cin cin!"]
    var suggestedVolumePerServing:String {
        get {
            let volume: Int = Int(12.0/(percentAlcohol/5.0))
            return "\(volume) ounces"
        }
    }

    static func cheers(_ language: String) {
        if let cheers = cheersDict[language] {
            print("\(cheers)")
        }
    }
}
```

> Struct vs enum vs Class, 각각 언제 쓸까?

Type | Struct | enum | class
:---:|:---:|:---:|:---:
상속 |  X | X | O
호출형태 | value | value | reference
특징 | 스위프트의 큰 뼈대에 쓰임, 속도 | 정해진 값을 줄 때 등등.. | 스위프트의 큰 프레임워크 대부분

#### Protocol

* 최소한으로 가져야 할 속성이나 메서드를 정의, 구현은 하지 않는다. 클래스, 구조체 모두에 속성을 줄 수 있다.

```javascript
//protocol 정의
protocol Souschef {
    func chop(vegetable: String) -> String
    func rinse(vegetable: String) -> String
}
//protocol의 정의는 여기서!
class Roommate: Souschef, Equatable {
    var hungry = true
    var name: String

    init(hungry: Bool, name: String) {
        self.hungry = hungry
        self.name = name
    }
    //여기서 해당 protocol을 구현해서 사용함
    func chop(vegetable: String) -> String {
        return "She's choppin' \(vegetable)!"
    }

    func rinse(vegetable: String) -> String {
        return "The \(vegetable) is so fresh and so clean"
    }
}
```

#### extension : 이미 정의된 속성을 확장 시켜서 사용할 수 있음


#### closure
* 함수와 다르게 정의가 따로 있지 않음. 파라미터를 ()로 클로저를 {}로 정의

```javascript
//일반적인 클로저 타입
{ (parameters) -> return type in
     statements to execute
}
//sort내에 이런식으로 클로저를 정의할 수도
var youngestToOldest = birthYears.sorted(by: { (year1: Int, year2: Int) -> Bool in
    return year1 > year2
})
//예시
func helloGenerator(message: String) -> (String, String) -> String {
  return { (firstName: String, lastName: String) -> String in
    return lastName + firstName + message
  }
}
let hello = helloGenerator(message: "님 안녕하세요!")
hello("정", "한")
//둘은 같은 함수이다. 매우 간결해 진 것을 볼 수 있다.
let hello: (String, String) -> String = { $1 + $0 + "님 안녕하세요!" }
hello("정", "한")
```


* 참조 : https://devxoul.gitbooks.io/ios-with-swift-in-40-hours/content/Chapter-3/functions-and-closures.html
 <br/><br/>
