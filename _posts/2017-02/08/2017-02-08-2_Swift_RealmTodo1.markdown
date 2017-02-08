---

layout: post
title: "(Swift) Realm 이용해서 Todo App 만들기[1]"
category: SWIFT

---

#### realm이란 데이터베이스를 처음 접했고 App설계 또한 처음입니다. 지적은 감사히 받고 반영시키겠습니다!

### Realm 이란?
* 모바일에 최적화된 데이터베이스
* SQLite나 CoreData보다 매우 빠른 속도
* Java, Objective-C, Swift, React Native, Xamarin등을 지원
    * Objective-C와 Swift를 동시 지원하지는 않는다고 한다.
    * 안드로이드, iOS 모두 적용가능
* 싱글톤 패턴

### 설치하기
* Realm에서 안내하는 설치 방법은 여러가지가 있다. 그 중 저는 Dynamic Framework로 설치를 해보겠습니다.
    * 이후 실제앱에서 라이브러리 버전 관리를 편리하게 하기 위해선 CocoaPods이 유리해보입니다.
    * [최신설치파일](https://realm.io/docs/swift/latest/)
* 다운 후 압축을 풀고 해당 버전 폴더를 열어주면 framework 파일이 두 개 있을 것입니다.
* 프로젝트를 만들어 주고 general에 가서 library에 저 두 파일을 추가해 줍니다.<br/>
<img src = '/post_img/201702/08/3.png' width='400'/><br/>
* 이런 모양이 될 것입니다.<br/>
<img src = '/post_img/201702/08/5.png' width='400'/><br/>
* 잘 적용되었다면 'RealmSwift'를 import 시켰을 때 에러가 발생하지 않을 것입니다.
* 모델을 만들어 보겠습니다. 만약 Realm Model Object가 없다면 [링크](https://hanjungv.github.io/2017-02-07-2_Swift_XCode_package_manager/) 에 들어가 설치를 하시는 것도 추천합니다.
* 그냥 swift 파일을 만들어도 괜찮습니다.<br/>
<img src = '/post_img/201702/08/7.png' width='600'/><br/>
* 만들었다면 이런 형식으로 나올 것입니다.<br/>
<img src = '/post_img/201702/08/9.png' width='600'/><br/>

### 모델 만들어보기

```javascript
// Task 코드
import Foundation
import RealmSwift
// 여기서 등장하는 dynamic! 뭔지 궁금하다면 앞의 글을 읽고오자.
class Task: Object {
    dynamic var name = ""
    dynamic var content = ""
    dynamic var createdDate = NSDate()
}
```

### 컨트롤러에서 임시로 object 만들어 저장하기, 지우기


```javascript
import UIKit
import RealmSwift

class ViewController: UIViewController {
    override func viewDidLoad() {
        super.viewDidLoad()
        //어디에 저장되어있는지 URL을 출력해보자
        print(Realm.Configuration.defaultConfiguration.fileURL!)
        removeAllTask()
        //Task를 임의로 만들어 줬다
        makeTask(name:"hanjung", content:"hi!jung")
        makeTask(name:"doyoon", content:"hi!doyoon")
        makeTask(name:"gaem", content:"hi!gaem")
        makeTask(name:"hibbah", content:"hi!hibbah")
        //query를 넣어서 불러오기, h로 이름이 시작하는 task를 가져와  result
        let result = makeQuery(query: "name BEGINSWITH 'h'")
        //결과를 출력해보자
        for task in result{
            print(task.name)
        }
    }
    func removeAllTask(){
        let realm = try! Realm()
        try! realm.write {
            realm.deleteAll()
        }
    }
    func makeTask(name:String, content:String){
        let task = Task()
        task.name = name
        task.content = content

        let realm = try! Realm()

        try! realm.write {
            realm.add(task)
        }
    }
    func removeTask(task: Results<Task>){
        let realm = try! Realm()
        try! realm.write {
            realm.delete(task)
        }
    }
    func makeQuery(query:String) -> Results<Task>{
        let realm = try! Realm()
        let allTask = realm.objects(Task.self)
        let queryResult = allTask.filter(query)
        return queryResult
    }
}

```

### 결과 화면
<img src = '/post_img/201702/08/10.png' width='900'/><br/>

#### 더 해야할 일
* CRUD 가능하게
* 테이블 뷰로 출력
* search 기능

 <br/><br/>
