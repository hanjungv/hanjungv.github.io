---

layout: post
title: "(SWIFT) Swift Syntax[2]"
category: SWIFT

---

#### SYNTAX에 관한 글은 모두 이 [유다시티 인강(Learn Swift Programming Syntax )](https://classroom.udacity.com/courses/ud902/lessons/4667459037/concepts/46437489340923)에서 나왔습니다.

##### 기본적인 내용은 뛰어넘겠습니다. 다른 언어와의 다른점, 사용법에 중점을 두겠습니다.

#### Optional

* [기본적인 내용](https://hanjungv.github.io/2017-02-01-3_Swift_optional/)은 이 포스트에 정리되어 있습니다.
* 추가되는 내용들
    * Swift는 nil은 안된다라는 생각으로 만들어짐
    * 그럼에도 nil이 필요한 순간이 있을 수 밖에 없기 때문에 nil을 사용함
        * 메서드가 아무 값도 리턴을 안할 때 (init method 같은것 Ex> Int(), String())
        * object가 생성될 때 initialize를 할 수 없는 경우(Ex> 버튼생성 때 같은 경우)
    * 일반적으로 optional binding을 할 때는 할당되는 상수와 이름을 같게 함, Xcode에서는 헷갈리지 않게 하기위해 색을 다르게 표기함
    * optional chaining의 리턴값은 optional type이다. optional type으로 쓰기를 원하지 않을 때 binding과 같이 사용한다.

```javascript
if let zee = zee {
    zee * 2
} else {
    "No value"
}
```

```javascript
if let imageSize = anotherImageView.image?.size {
    print("Here's the image size: \(imageSize)")
} else {
    print("This image hasn't been set.")
}
```

#### Collections
* Array : 배열이다. 순서가 있다.
* Dictionary : key-value 쌍으로 다님. 순서는 없다.
* Set: 구분되는 값들의 집합. 순서는 없다.

> array

```javascript
// 선언법. 둘 다 똑같다.
var numbers = Array<Double>()
var moreNumbers = [Double]()
// 기본적인 메서드
var roadTripMusic = ["Neil Young","Kendrick Lamar","Flo Rida", "Nirvana"]
roadTripMusic.append("Rae Sremmurd")
roadTripMusic.insert("Dej Loaf", at: 2)
roadTripMusic.remove(at: 3)
roadTripMusic.insert("Keith Urban", at: 3)
roadTripMusic.count
```

> Dictionary

```javascript
//선언법
var groupsDict = [String:String]()
//이런식으로도 쓸 수 있다.
var averageLifeSpanDict = [String:CountableRange<Int>]()
var lifeSpanDict = ["African Grey Parrot": 50...70, "Tiger Salamander": 12...15, "Bottlenose Dolphin": 20...30]
//update하기
var group = animalGroupsDict.updateValue("gaggle", forKey: "geese")
//Dictionary 의 리턴값은 optional type이다. 물어보는 케이스가 많고 nil의 경우가 많음
//binding 형태로 출력해주면 optional type이 아닌 값을 얻을 수 있다.
if let groupOfWhales = animalGroupsDict["whales"] {
    print("We saw a \(groupOfWhales) of whales from the boat.")
} else {
    print("No value found for that key.")
}
```

> Sets

```javascript
//선언법
var utensils = Set<String>()
var trees = Set<Character>()
//기본적인 메서드
trees.insert("🌲")
trees.remove("🌵")
trees.count
```

<br/><br/>
