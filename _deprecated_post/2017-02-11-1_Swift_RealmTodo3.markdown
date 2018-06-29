---

layout: post
title: "(Swift) Realm 이용해서 Todo App 만들기[3]"
category: SWIFT

---

#### realm이란 데이터베이스를 처음 접했고 App설계 또한 처음입니다. 지적은 감사히 받고 반영시키겠습니다!

### 모델 관리하기
* 먼저 RealmController와 TaskController를 따로 둬 관리했습니다. 귀찮으니 한번에...

~~~
// RealmController.swift
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
    // 만들기
    static func makeTask(task: Task){
        try! realm.write {
            realm.add(task)
        }
    }
    // 모두 지우기
    static func removeAllTask(){
        try! realm.write {
            realm.deleteAll()
        }
    }
    // 선택한 것 지우기
    static func removeSelectedTask(task: Task){
        try! realm.write {
            realm.delete(task)
        }
    }
    // task update
    static func updateTask(name:String, content:String, taskId: Int){
        let RealTask = realm.objects(Task.self).filter("id == 0").first
        try! realm.write {
            RealTask?.name = name
            RealTask?.content = content
        }
    }
    // query에 해당하는 task배열 반환
    static func getQueryResult(query: NSPredicate) -> [Task]{
        let result = realm.objects(Task.self).filter(query)
        var resultTask = [Task]()
        for task in result{
            resultTask.append(task)
        }
        return resultTask
    }
    // 모든 task date 반환
    static func returnTotalTask() -> [Task]{
        var rtTotalTask = [Task]()
        let TotalTask = realm.objects(Task.self)
        for task in TotalTask{
            rtTotalTask.append(task)
        }
        return rtTotalTask
    }
}
~~~

~~~
// TaskController.swift
class TaskController{
    private static var appDelegate: AppDelegate{
        return UIApplication.shared.delegate as! AppDelegate
    }
    // count 반환
    static func count() -> Int{
        return appDelegate.task.count
    }
    // task 만들기
    static func makeTask(name:String, content:String){
        let task = Task()
        task.name = name
        task.content = content
        task.id = Task.autoIncrement()
        RealmController.makeTask(task: task)
        appDelegate.task.append(task)
    }
    // 해당 task 반환
    static func getTask(index: Int) -> Task{
        return appDelegate.task[index]
    }
    // 모든 task 지우기
    static func removeAllTask(){
        RealmController.removeAllTask()
        appDelegate.task.removeAll()
    }

    static func removeSelectedTask(index: Int){
        RealmController.removeSelectedTask(task: appDelegate.task[index])
        appDelegate.task.remove(at: index)
    }

    static func updateTask(name:String, content:String, taskId:Int){
        RealmController.updateTask(name:name, content:content, taskId: taskId)
        //상당히 무거운 방법인 것 같다..
        appDelegate.task.removeAll()
        RealmController.getData(taskList: &appDelegate.task)
    }

    static func getQueryResult(query:NSPredicate){
        let result = RealmController.getQueryResult(query: query)
        appDelegate.task = result
        for a in appDelegate.task{
            print(a.name)
        }
    }

    static func resetTotalTask(){
        appDelegate.task = RealmController.returnTotalTask()
    }
}

~~~



### 내용 추가하기
* 먼저 스토리 보드에서 네비게이션 바에 + 버튼을 넣고 그 버튼을 누를 때 Make ViewController로 이동하게 했습니다.

~~~
//TaskTableViewController.swift
@IBAction func AddButton(_ sender: Any) {
    let Controller = storyboard?.instantiateViewController(withIdentifier: "MakeViewController") as! MakeViewController
    navigationController?.pushViewController(Controller, animated: false)
}
~~~

* MakeViewController에 textView와 textField를 만들고 입력을 받아 데이터를 넣어주겠습니다. 이후 submit을 누르면 추가가 될 것입니다.

~~~
//MakeViewController.swift
class MakeViewController: UIViewController{
    @IBOutlet weak var NameTextField: UITextField!
    @IBOutlet weak var ContentTextView: UITextView!
    @IBAction func saveTask(_ sender: Any) {
        if let Name = NameTextField.text{
            if let Content = ContentTextView.text{
                TaskController.makeTask(name: Name, content: Content)
                let _ = navigationController?.popViewController(animated: false)
            }
        }
    }
    override func viewDidLoad() {
        super.viewDidLoad()
        ContentTextView.layer.borderColor = UIColor.black.cgColor
    }
}
~~~

### DetailView 보여주기
* tableView에서 선택을 할 때 DetailViewController를 푸시해줍니다.

~~~
// TaskTableViewController.swift
override func tableView(_ tableView: UITableView, didSelectRowAt indexPath: IndexPath) {
    let controller = storyboard?.instantiateViewController(withIdentifier: "DetailViewController") as! DetailViewController
    controller.task = TaskController.getTask(index: indexPath.row)
    navigationController?.pushViewController(controller, animated: true)
}
~~~

* 그리고 DetailView에서는 넘겨받은 task의 정보를 출력해줍니다. 이 DetailView에서는 Edit버튼이 있습니다. 이것을 누를 경우 수정을 합니다.

~~~
class DetailViewController: UIViewController {
    var task:Task?
    @IBOutlet weak var TitleLabel: UILabel!
    @IBOutlet weak var ContentLabel: UILabel!
    @IBOutlet weak var CreatedAtLabel: UILabel!
    //Edit 버튼 눌렀을 때.
    @IBAction func taskEdit(_ sender: UIButton!) {
        let controller = storyboard?.instantiateViewController(withIdentifier: "EditViewController") as! EditViewController
        controller.task = self.task
        navigationController?.pushViewController(controller, animated: true)
    }
    override func viewDidLoad() {
        super.viewDidLoad()
        TitleLabel.text = task?.name
        ContentLabel.text = task?.content
        if let CreatedAt = task?.createdDate{
            CreatedAtLabel.text = "\(CreatedAt)"
        }
    }
}
~~~

### 수정하기
* 저는 taskId를 넘겨줘 filter를 한 후 그 object를 수정하는 형태로 하였습니다.

~~~
// EditViewController.swift
class EditViewController: UIViewController {
    @IBOutlet weak var NameTextField: UITextField!
    @IBOutlet weak var ContentTextView: UITextView!
    var task: Task?
    @IBAction func editSubmit(_ sender: UIButton!) {
        if let name =  NameTextField.text{
            if let content = ContentTextView.text{
                if let task = task{
                    TaskController.updateTask(name: name, content: content, taskId: task.id)
                }
            }
        }
        let _ = navigationController?.popToRootViewController(animated: false)
    }
    override func viewDidLoad() {
        super.viewDidLoad()
        NameTextField.text = task?.name
        ContentTextView.text = task?.content
    }    
}
~~~

### 검색하기
* tableView에 textField를 넣고 이에 해당되는 값들을 즉시 불러오겠습니다.
* 검색값이 있을 땐 query문을 검색하여 결과를 띄우고 아닐 때는 다시 원래대로 값을 불러오는 형태로 구현했습니다.
* 이런식으로 구현할 때 부담이 없게 하기 위해선 여러 기법이 필요할 것 같습니다.

~~~
// TaskTableViewController.swift
@IBOutlet weak var SearchTextField: UITextField!
func textField(_ textField: UITextField, shouldChangeCharactersIn range: NSRange, replacementString string: String) -> Bool {
    DispatchQueue.main.asyncAfter(deadline: .now() + 0.1 ){
        if (self.SearchTextField.text?.characters.count)! > 0 {
            let pridicate = NSPredicate(format: "name CONTAINS [c] %@", textField.text!)
            TaskController.getQueryResult(query: pridicate)
            self.tableView.reloadData()
        } else{
            TaskController.resetTotalTask()
            self.tableView.reloadData()
        }
    }
    return true
}
~~~


### 스토리 보드 / 디렉토리
<img src = '/post_img/201702/11/3.png' width='200'/><br/>
<img src = '/post_img/201702/11/4.png' width='1000'/>

### 결과 화면
<img src = '/post_img/201702/11/1.png' width ='300'/>
<img src = '/post_img/201702/11/2.png' width ='400'/><br/>

#### 더 해야할 일
* realm browser에서 보기, document가 아닌 다른 곳에 저장해보기

 <br/><br/>
