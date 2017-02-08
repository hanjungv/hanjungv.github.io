---

layout: post
title: "(Swift) CocoaPods란?"
category: SWIFT

---

### CocoaPods 이란?
> CocoaPods is a dependency manager for Swift and Objective-C Cocoa projects.

* CocoaPods는 Cocoa project의 의존성 매니저, 라이브러리들을 쉽게 관리할 수 있게 된다.
* 노드의 package를 관리하는 json 파일과 비슷한 느낌

#### 설치
* 루비가 선행으로 설치 되어야 함

```
$ sudo gem install cocoapods
```

* 해당 Xcode 프로젝트에서

```
$ pod init
// 이 명령어를 실행하게되면 Podfile이 생성되게 된다. 여기서 관리를 하게 된다.
```

* init을 하게 되면 app.xcworkspace가 생기게 되는데 여기서 원하는 library를 import해서 사용하면 된다.

* 그 pod파일을 이용하여 실제 프로젝트와 연결

```
$ pod install
```

 <br/><br/>
