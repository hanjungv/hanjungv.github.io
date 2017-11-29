---

layout: post
title: "(CS) 인터넷 프로그래밍(JSP) 리뷰"
category: CS
---


# 마지막으로 학교에서 보는 마지막 기말고사 
> 정말로 이제는 졸업을 하게 되는것 같다. (야호!) 학교에서 보는 마지막 기말고사 시험이 될 것 같다. JSP를 전전회사에서 사용해보고 처음 사용하는 것이지만 그때보다 좀 더 별로인것 같다. 하지만 시험에 나오니 준비를 해보자.

## 5장 JSP 기본
스크립팅 요소, 지시어, JSP 액션 태그 사용법을 익히는 단원이라고 한다.

1. 스크립틀릿, 익스프레션
스크립틀릿은 `_jspService()`메소드에서 실행되는 java code 기술부 입니다.
익스프레션은 변수, 상수, 반환값을 가지는 메소드, 연산식의 결과를 출력하는 구문이다. 세미콜론을 사용할 수 없다. 내장 객체의 out.print()와 같은 역할을 하게 된다.

```jsp
<!-- %사이에 자바 코드를 작성하면 변환해줍니다. -->
<%
int total=0;
for(int cnt = 1; i<=10; i++){
  total+=cnt;
}
%>
<%=total%>
```

2. 선언부와 주석
선언은 `<%! %>` 사이에 클래스의 멤버변수, 메서드, 이너 클래스 등을 선언합니다. 
주석 부는 `<%-- comments --%>` 입니다. 밑 예제를 살펴보겠습니다.

```jsp
HTML주석과 JSP주석 소스 확인하기
<!-- HTML 주석 <%-- JSP 주석 --%> -->
<%-- JSP 주석 <!--HTML 주석 --> --%>
```
이렇게 사용하여 소스를 출력해 볼 경우

```
HTML주석과 JSP주석 소스 확인하기
<!--HTML 주석 -->
```

로 출력되게 된다. 

3. JSP 지시어 page
`<%@ page 속성1="속성값1" 속성2="속성값2"…. %>`
import를 제외한 속성은 무조건 한번만 사용할 수 있게 됩니다.
  * language: language는 jsp파일 내에서 사용할 스크립트 언어 선언(`<%@ page language="java"%>`)
  * extends :  extends는 jsp파일을 서블릿으로 변환할 떄 상속하게 되는 부모 클래스 지정(`<% page extends="packageName.aa.bb.cc"%>`)
  * session: session true는 클라이언트의 지속적인 정보를 유지하는 세션을 사용하겠다고 하는 것(`<%@ page session="true"%>`)
  * buffer: buffer는 out 객체에 출력할 내용을 저장할 버퍼의 사용여부를 지정(`<%@ page buffer="10kb"%>`),  헤더정보를 수정할 필요가 있거나 완곡한 에러메세지를 전달하려고 할 때 사용된다.
  * autoFlush: buffer가 다 채워졌거나 응답처리 서블릿이 종료되었을 때 버퍼의 내용이 전송되고 buffer가 비워진다.
  * isThreadSafe: 쓰레드를 생성하여 `_jspService()` 메서드를 사용할지의 여부
  * info: 해당 페이지 설명. `getServeletInfo()`로 정보를 불러올 수 있다.
  * errorPage: 예외를 처리할 페이지를 지정해주는 것이다. 예외가 생기면 예외객체를 이 페이지로 전달해주게 된다. web.xml에서 exception-type에 따라서 location(에러를 처리할 페이지)을 지정해 줄 수 있다.
  * contentType, pageEncoding: client로 전송할 타입, 인코딩 방식 지정(`<%@page contentType="text/html;charset=utf-8" pageEncoding="utf-8"%>`)



<br/><br/>
