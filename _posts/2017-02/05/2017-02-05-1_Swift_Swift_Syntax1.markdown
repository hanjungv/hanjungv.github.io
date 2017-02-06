---

layout: post
title: "(SWIFT) Swift Syntax[4]"
categories: SWIFT

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

#### closure



 <br/><br/>
