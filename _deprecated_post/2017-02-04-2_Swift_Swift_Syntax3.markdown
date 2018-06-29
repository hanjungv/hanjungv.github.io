---

layout: post
title: "(Swift) Swift Syntax[3/4]"
category: SWIFT

---

#### SYNTAX에 관한 글은 모두 이 [유다시티 인강(Learn Swift Programming Syntax )](https://classroom.udacity.com/courses/ud902/lessons/4667459037/concepts/46437489340923)에서 나왔습니다.

##### 기본적인 내용은 뛰어넘겠습니다. 다른 언어와의 다른점, 사용법에 중점을 두겠습니다.

#### Control Flow

##### 반복문 <br/>
* for - in 구문.

```javascript
    // Array 돌릴 때
    for value in intArray {
        sum += value
    }
    // Dictionary
    for (movie, director) in movieDict {
        print("\(director) directed \(movie)")
    }
```

* while

```javascript
    while beerVolume > 0 {
        print ("Cheers!")
        beerVolume -= sip
    }
```

* repeat - while 문 도 있음

##### 조건문 <br/>
* if - else

* switch - case : 기존 다른언어와 switch case 다른 부분은 여러 밸류를 동시에 비교할 수 있다는 점

```javascript
    switch birthYear {
    case 1992, 1980, 1968:
    print("You were born in the year of the monkey.")
    case 1991,1979,1967:
    print("You were born in the year of the goat.")
    default:
    print("You were born in the year of some other animal.")
    }
```

* guard : if문 보다 좋다. 왜? **Early Exit**

```javascript
//이런식으로 가능. 조건에 해당이 안될때는 break, return, continue등의 행동을 꼭 해줘야한다.
    for cha in Arr{
        guard cha == "isthere" else{
            continue
        }
        print("oh!")
    }
```

#### Functions

```javascript
    //return type이 없다면 쓰지 않는다.
    func functionName (parameterName: parameterType) -> returnType {
        statements to execute
        return object
    }
```

#### classes, Properties and method
* 기본적으로 사용하는 것은 똑같!

Level  |  Class | App/FrameWork | World
:-----:|:------:|:-----:|:-----:
 public | Y | Y | Y
 internal | Y | Y | N
 private | Y | N | N

 <br/><br/>
