---

layout: post
title: "(CSS) transform"
categories: CSS

---

<h5>transform을 통해 이동(translate), 회전(rotate), 크기변경(scale), 기울임(skew)등의 효과를 줄 수 있다.</h5>

### 여러가지 웹 브라우저에서의 사용법

* 사용법

```css
.container{
    transform:rotate(7deg);
    ms-transform:rotate(7deg); /* IE 9 */
    -moz-transform:rotate(7deg); /* Firefox */
    -webkit-transform:rotate(7deg); /* Safari and Chrome */
    -o-transform:rotate(7deg); /* Opera */
}
```

* translate : 현재위치에서 X축 혹은 Y축으로 이동시키는 것

```css
.translate:active{
	/*X축 Y축으로 얼만큼 이동 시킬 것인지*/
	transform:translate(32px,32px);
	/*X축으로 얼만큼 이동 시킬 것인지*/
	transform:translateX(32px);
	/*Y축으로 얼만큼 이동 시킬 것인지*/
	transform:translateY(32px);
}
```

* rotate : 현재위치에서 회전시킨다(deg, turn 단위로 나타낼 수 있음)

```css
.rotate:active{
	transform:rotate(150deg);
	transform:rotate(0.5turn);
}
```

* scale : 현재 크기에서 몇 배의 크기로 변경 시킬지

```css
.scale:active{
	/*X, Y 축으로 몇 배 확장 시킬 것인지*/
	transform:scale(2,2);
	/*X축으로 몇 배 확장 할지*/
	transform:scaleX(2);
	/*Y축으로 몇 배 확장 할지*/
	transform:scaleY(2);
}
```

* skew(not standard) : 비튼 형태 ⇒ 비표준형태, 개발을 멈춘 상태, 앞으로 어떻게 될 지 모르므로 사용은 하지 않기로 하는게 좋다.

```css
.skew:active{
	/*X축을 기준으로 30도 비튼 형태*/
	transform:skewX(30deg);
	/*Y축을 기준으로 30도 비튼 형태*/
	transform:skewY(30deg);
}
```
<br/><br/>
