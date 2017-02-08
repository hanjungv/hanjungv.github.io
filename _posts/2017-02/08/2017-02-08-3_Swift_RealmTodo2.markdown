---

layout: post
title: "(Swift) Realm 이용해서 Todo App 만들기[2]"
category: SWIFT

---

#### realm이란 데이터베이스를 처음 접했고 App설계 또한 처음입니다. 지적은 감사히 받고 반영시키겠습니다!

### 테이블뷰에 결과 띄우기
* 먼저 만들어 놓은 ViewController는 지우고 RealmController를 만들어 여기서 realm을 관리하겠습니다.
* 스토리 보드 내용은 따로 수정하셔야 합니다!
* Task는 AppDelegate에 놓아 shared하며 사용하겠습니다.
* AppDelegate 부분입니다. 일부분 코드입니다.

```javascript
class AppDelegate: UIResponder, UIApplicationDelegate {
    var window: UIWindow?
    var task = [Task]()

    func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool {
        RealmController.getData(taskList: &task)
        return true
    }
```

* TableViewController 부분 코드입니다.

```javascript
import UIKit
import RealmSwift

class TaskTableViewController: UITableViewController {

    var TaskList:[Task]?

    override func viewDidLoad() {
        super.viewDidLoad()
        // AppDelegate에 이는 task를 복사해서 사용
        let appDelegate = UIApplication.shared.delegate as! AppDelegate
        TaskList = appDelegate.task
    }

    // MARK: - Table view data source
    override func numberOfSections(in tableView: UITableView) -> Int {
        return 1
    }

    override func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
        if let count = TaskList?.count{
            return count
        } else{
            return 0
        }
    }
    //일단 이름만 라벨로 띄워 보겠습니다.
    override func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
        let cell = tableView.dequeueReusableCell(withIdentifier: "taskTableCell", for: indexPath)
        cell.textLabel?.text = TaskList?[indexPath.row].name
        return cell
    }

    override func tableView(_ tableView: UITableView, didSelectRowAt indexPath: IndexPath) {
        tableView.deselectRow(at: indexPath, animated: false)
    }
}

```

* RealmController 부분 코드입니다.

```javascript
import Foundation
import RealmSwift

class RealmController: NSObject{

    private static var realm: Realm {
        return try! Realm()
    }

    static func getData(taskList: inout [Task]){
        let obj = realm.objects(Task.self)
        for list in obj{
            taskList.append(list)
        }
    }

    static func makeTask(name:String, content:String){
        let task = Task()
        task.name = name
        task.content = content

        try! realm.write {
            realm.add(task)
        }
    }
}
```

### 스토리 보드 / 디렉토리
<img src = '/post_img/201702/08/storyboard.png' height ='400'/>
<img src = '/post_img/201702/08/dir.png' height ='400'/><br/>

### 결과 화면
<img src = '/post_img/201702/08/11.png' width='400'/><br/>

#### 더 해야할 일
* CRUD 가능하게
* search 기능

 <br/><br/>
