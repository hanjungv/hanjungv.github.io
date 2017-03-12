---

layout: post
title: "(ROR) Asset pipeline"
category: ROR

---

### Asset pipeline
* 먼저 Asset 이란 image, js, css 등 rails에 속하는 file들을 의미한다
* Asset pipeline은 세가지의 역할을 하게 된다.
    * asset들을 precompile(이 과정에서 scss->css도 이뤄짐)
    * 여러개의 asset들을 합치고
    * 여러 asset들을 압축해서 요청 request를 줄이게 된다.
* 개발자들은 app/assets를 주로 이용한다.

#### manifest
* 레일즈 프로젝트를 만들게 되면 ```application.js / application.css``` 파일들을 디폴트로 만들어주게 된다. 이를 manifest파일이라한다.
* directives를 통해 포함할 에셋들을 사용할 수 있게 된다.

### 사용할 때
* 사용하는 것은 매우 쉽다. 사용하고 싶은 asset들을 모두 asset경로로
두기만 하면 된다.

* 이미지를 불러올 때

```css
background-image: url('/assets/5.png'); //이렇게 사용한다
background-image: url('/app/assets/images/5.png') // 이건 아님
```
* helper method 를 사용할 때

```Ruby
audio_path("horse.wav")   # => /audios/horse.wav
audio_tag("sound")        # => <audio src="/audios/sound" />
font_path("font.ttf")     # => /fonts/font.ttf
image_path("edit.png")    # => "/images/edit.png"
image_tag("icon.png")     # => <img src="/images/icon.png" alt="Icon" />
video_path("hd.avi")      # => /videos/hd.avi
video_tag("trailer.ogg")  # => <video src="/videos/trailer.ogg" />
```

* 꼭 application.js manifest를 이용하지 않아도 된다.

~~~js
//test.js 파일을 새로 만들고
//= require test1
//= require test2
~~~

~~~html
<!--해당 html파일에서 이렇게 하게 되면 test1, test2를 사용할 수 있게 된다.-->
<%= javascript_include_tag("test") %>
~~~

참조 : [http://rorlab.org/rblogs/152](http://rorlab.org/rblogs/152)

<br/><br/>
