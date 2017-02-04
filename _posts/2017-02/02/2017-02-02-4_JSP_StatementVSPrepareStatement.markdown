---

layout: post
title: "(JSP) Statement vs PrepareStatement"
categories: JSP

---

### 차이점

* Statement 인터페이스는 Connection 객체에 의해 프로그램이 리턴되는 객체에 의해 구현되는 메소드 집합을 정의
* Statement는 Connection 클래스의 createStatement()메소드를 호출함으로써 얻어진다.
* Statement는 생성이 되면 statement 객체의 executeQuery()메소드를 호출해서 SQL질의를 실행시킬 수 있다.
* PrepareStatement는 Connection객체의 PrepareStatement()메소드를 사용해서 생성한다.
* SQL문장이 미리 컴파일이 되고 실행시간 동안 인수를 위한 공간을 확보할수 있다는 점에서 statement 문과 다르다.
* 동일한 질의를 여러번 하거나 많은 데이터를 다룰때, 인수가 많을때 사용하는 것이 좋습니다.
* 각각의 인수에 대해 위치홀더(placeholder)를 사용하여 SQL문장을 정의할 수 있게 해줍니다. 위치 홀더는 물음표(?)로 표현됩니다.
* Statement / PrepareStatement는 반드시 try-catch문을 실행한다. 또는 throw처리

### PreparedStatement 객체의 장점

* 미리 컴파일이 되기 때문에 쿼리의 수행속도가 빠릅니다.
* 동일한 질의문을 여러번 바꾸어서 여러번 사용할 때, 많은 데이터를 다룰 때, 인수가 많을때 사용하기 좋습니다.
* Statement는 쿼리 실행시 작은따옴표(‘)가 있을 경우 작은따옴표를 두개로 표시해야합니다.(‘’), 그러나 PreparedStatement는 자동으로 처리해주기 때문에 편리

```java
ps = conn.prepareStatement("insert into ReviewRequestSupportLink set "+"review_request=?,support=?");
ps.setString(1, id);
ps.setString(2, additional_support[i]);
ps.execute();
```

* 이런식으로 첫번째 두번째 들어갈 인자들을 결정

<br/><br/>
