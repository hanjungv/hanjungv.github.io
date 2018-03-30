---

layout: post
title: "(HTML) HTML overview[2/3]"
category: HTML

---


### Tag 소개(2/2)
* **a**, anchor
    - 주로 링크를 연결할 때 사용

```html
<a href = "https://hanjungv.github.io" target = "_blank" title="내 블로그 인뎅">이걸 누르면 이동할거야</a>
```
* **input**, 인풋
    * type의 종류는 매우 많다. 주로 많이 쓰는 것들은
        * text: 글 입력
        * password: 우리가 아는 패스워드의 모양으로 바꿔준다.
        * submit: submit버튼 처럼 사용이 가능하다.
        * date: 달력 모양으로 선택이 가능하다.
        * email: 이메일 형태의 입력이 가능해진다.
        * radio, checkbox: 선택지를 선택하는 방식의 차이. radio는 하나! checkbox는 여러개 선택이 가능하다.
        * hidden: 보이지 않는다. 굳이 UI가 필요하지 않지만 값을 넘겨줘야할 떄 사용한다.
        * file: file 업로드 할 때 사용
        * 등등의 type은 w3schools에서 확인이 가능하다.
    * 기본 값을 넣어두려면 value = "" 로 값을 넣어준다.
    * input tag는 한 줄로 입력이 된다. 여러 줄의 값을 받으려면 textarea를 사용해야 한다.
    * input type을 적절하게 사용하면 굳이 자바스크립트로 validation을 체크할 필요가 사라진다.
    * [내용이 너무 많으니 여기서 확인하자](http://www.w3schools.com/tags/tag_input.asp)

```html
//여러개 선택가능
<input type="checkbox" name="test" value="1">
<input type="checkbox" name="test" value="2">
<input type="checkbox" name="test" value="3">

//하나만 선택가능
<input type="radio" name="test" value="1">
<input type="radio" name="test" value="2">
<input type="radio" name="test" value="3">

//입력 불가
<input type="text" name="test" disabled>
//max, min 길이 지정
<input type="text" name="test" max = "40">
//반드시 채워져야 submit이 가능, 이 또한 validation을 쉽게 하는데 도움이 된다.
<input type="text" name="test" max = "40" required>
```

* **textarea**
    * rows, cols로 사이즈를 조절 할 수 있다.
    * 일부 브라우저에서 resize가 가능하게 되는데 css로 금지 가능하다.

```html
<textarea cols="50" rows="2" style = "resize:none;">default value</textarea>
```

* **select**, drop down list
    * select, option 태그를 이용하여 값을 전송

```html
<select name = 'color'>
    <option value = "red">red</option>
    <option value = "blue">blue</option>
    <option value = "green">green</option>
</select>
```

* **button**
* **lable**, 무언가의 이름

```html
<label>이름</label><input type = "text" name = "name">
```

 <br/><br/>
