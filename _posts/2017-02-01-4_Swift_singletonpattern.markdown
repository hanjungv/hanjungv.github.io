---

layout: post
title: "(Swift) 싱글톤 패턴이란?"
categories: SWIFT

---

* 먼저 OOP에서 클래스에 속하는 각 객체를 인스턴스(instance)라고 함
-	싱글톤 패턴이란?
	* 싱글톤 패턴은 OOP의 패턴중 하나 입니다. 싱글톤 클래스는 한번에 여러개의 인스턴스를 가질수 없습니다.
	* 인스턴스가 여러 개 있을 때 문제가 되는 오디오나 카메라, 로그인, 로그아웃 등에 문제가 생기지 않기 위해 구현되는 방법이다.
- Pitchperfect 앱 일부분을 보면

```objective-c
let session = AVAudioSession.sharedInstance()
try! session.serCategory(AVAudioSessionCategoryPlayAndRecord, with: .defaultToSpeakr)
```

여기서는 내부메서드를 사용하여 싱글톤 패턴을 구현합니다.<br/>
오디오가 동시에 여러군데에서 사용되어야 하지 않아야 하므로 싱글톤 형태로 오디오 세션을 구현해줍니다.

- 그럼 직접 구현해야할 때는?

```objective-c
class YourClassName{
	static var instance: YourClassName = YourClassName()
	private init(){

	}
}
```

* 일반적으로 많이 쓰는 구현방법. init에 private이 걸려있어 직접 선언 안됨. 동시 호출도 안됨
