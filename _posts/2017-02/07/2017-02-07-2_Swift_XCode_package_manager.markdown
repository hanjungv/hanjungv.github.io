---

layout: post
title: "(Swift) XCode 8.0 이상 package manager이용하기"
category: SWIFT

---

### XCode 8.0 미만에서..
* 8.0 미만 버전에서는 package manager를 지원해 줬음.
* 플러그인을 통해 개발에 편의를 제공했는데..
* 근데 Xcode extentions이 생기며 package manager가 사라짐

### Alcatraz - Package Manager

```
# package manager 설치
$ curl -fsSL https://raw.githubusercontent.com/supermarin/Alcatraz/deploy/Scripts/install.sh | sh

# 설치
$ gem install update_xcode_plugins

# 실행
$ update_xcode_plugins
$ update_xcode_plugins --unsign
```

#### 여기까지 하고 엑스코드 재실행하면 window->package manager가 보일것

```
# 다시복구하고 싶을 땐
$ update_xcode_plugins --restore
```

#### 저는 여기서 realm plugin을 받았습니다.

 <br/><br/>
