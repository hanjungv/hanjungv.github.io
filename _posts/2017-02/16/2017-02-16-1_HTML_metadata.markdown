---

layout: post
title: "(HTML) <meta> Tag란?"
category: HTML

---

### 메타태그란 무엇인가?
> 메타태그란 data에 대한 정보를 나타내는 태그이다.<br/>
물론 일부는 아니겠지만 우리는 서비스를 만들고 그 서비스를 최대한 노출 시키고 싶을 것이다.
<br/>그럼 그 페이지에서 어떤 내용이 중요한 줄 알고 노출을 시키지?

#### 메타태그에는 어떤게 있을까?

```html
<head>
    // html5 부터 나온 태그, UTF-8로 HTML문서를 인코딩 하자!라는 의미
    // 습관적으로 쓰게 되어있다.
    <meta charset="UTF-8">
    // 기타 페이지 설명 태그, 이부분을 잘 작성해주자.
    <meta name="description" content="지금 이 페이지에 관한 설명. 검색해서 나오는 설명에 해당하는 부분">
    <meta name="keywords" content="페이지와 관련된 키워드, 한정, 블로그, HTML">
    <meta name="author" content="작성자를 적자 HanJung">
    // 모바일에서 많이 사용되는 태그, 꽉차게 보여주자
    <meta name="viewport" content="width=device-width, initial-scale=1.0">

    //그리고 이런 것들도 있다. 30초마다 refresh 시키자.
    <meta http-equiv="refresh" content="30">
</head>
```

#### 여기 까지는 기본적인 내용이다. 그럼 조금 더 나아가서는?
> open-graph tag, twitter tag 들을 써보는건 어떤가?

* 요즘은 페이스북, 카카오톡, 트위터 등에 링크를 공유하게 되면 그 링크대신 사진과 글귀가 나온다. <br/><br/>
<img src = '/post_img/201702/16/1.png' width='300'/>
<img src = '/post_img/201702/16/2.png' width='300'/><br/>

* 각 회사마다 이를 이용하기 위해 meta tag를 정의했다.
* open graph는 카카오톡, 페이스북 등이 이를 사용한다.

```html
<meta property="og:title" content="test"/>
<meta property="og:type" content="article"/>
<meta property="og:url" content="https://hanjungv.github.io/"/>
<meta property="og:description" content="설명을 적어보자!"/>
<meta property="og:image" content="/post_img/201702/16/1.png"/>
<meta property="og:image:width" content="1200" />
<meta property="og:image:height" content="627" />
```

* 그럼 트위터는 어떻게 할까? [링크](https://dev.twitter.com/cards/markup)

```html
<meta name="twitter:card" content="summary">
<meta name="twitter:url" content="https://hanjungv.github.io/">
<meta name="twitter:title" content="test">
<meta name="twitter:description" content="설명을 적어보자!">
<meta name="twitter:image" content="/post_img/201702/16/1.png">
```
이런 태그들을 이용하면 원하는 정보를 뽑아 그대로 출력시킬 수 있다.


#### 조금 더~ 나아가서는???
* 설명(description)은 간결하고 그 페이지를 명확하게 나타내주는 글로(1~2줄)
* 가능하다면 페이지마다 다르게하자. 그게 정체성을 더 나타낼 것
* description을 수정한다면 바로 웹페이지에 반영되지 않는다. 주기적으로 업데이트가 되는 시점 이후에 반영이 된다고한다.

 <br/><br/>
