---

layout: post
title: "(SPRING) Spring CI, DI, AOP에 대해 알아보자"
category: SPRING 

---

## Spring IoC/DI, CI, AOP 에 대해 정리해보자

### IoC(Inversion of Control, 제어의 역전)/DI(Dependency Injection, 의존성 주입)

1. IoC(Inversion of Control)이란?<br>
제어의 역전이란 프레임워크에 제어의 권한을 넘김으로써 클라이언트 코드가 신경써야할 일을 줄이는 전략입니다.
잘 와닿지 않아 좀 더 검색을 해보니 더 잘 설명해주는 말이 있었습니다.

> 프레임워크의 중요한 특성은 사용자가 정의한 메소드가 사용자의 어플리케이션 코드가 호출 하기보다 종종 프레임워크로 부터 호출 되어 진다는 것이다.  프레임워크는 종종 어플리케이션의 행위를 재배치 하고, 순서를 정하는 메인프로그램의 역할을 담당한다. 역전된 제어는 프레임워크가 확장된 뼈대를 제공하는 힘을 제공한다. 사용자는 특정 어플리케이션을 위한 커스터마이즈된 알고리즘 메소드를 프레임워크에 전달한다.  - Ralph Johnson and Brian Foote 

<br>
프레임워크는 추상화된 설계와 많은 내장된 행위를 감싸고 있습니다. 그것을 이용하기 위해서는 작성한 클래스, 서브 클래스 들을 프레임워크 여러 부분에 삽입을 해야하고 그 후 프레임워크는 그 코드를 호출합니다.

<br>
프레임워크에서 이 제어권을 갖는 곳은 `Container`(스프링에서는 `bean Factory`)입니다. 컨테이너에서 객체의 생성, 맹명주기 관리 등 모든 것을 맡아서 관리하게 됩니다.

2. DI(Dependency Injection)이란?
DI는 클래스 사이의 의존관계를 빈 설정 정보를 바탕으로 컨테이너가 자동으로 연결해주는 것을 말합니다. 
의존 정보만 입력해준다면 Object reference를 외부(Container)로부터 주입 받아 실행 시에 동적으로 의존 관계를 생성 해 줄 수 있습니다.
<br>
* Ioc/DI가 적용되지 않은 경우<br>

```java
public class Foo{
  private Bar bar;
  public Foo(){
    bar = new SubBar();
  }
}
```

* IoC/DI가 적용된 경우
<br>

```xml
<beans>  
    <bean id="bar" class="kr.co.nextree.SubBar">
    <bean id="foo" class="kr.co.nextree.Foo">
        <property name="bar" ref="bar"/>
    </bean>
</beans>  
```

```java
public class Foo {  
    private Bar bar;

    public void setBar(Bar bar) {
        this.bar = bar;
    }
}
```

<br>
이렇게 작성할 경우 결합도(Coupling)는 낮추면서 유연성, 확장성을 증가 시킬 수 있습니다.
<br>
3. DI의 세가지 유형

3-1. `생성자`를 이용한 의존성 삽입(Constructor Injection)<br>
```java
class MovieList{
  public MovieList(MovieFind find){
    this.find = find;
  }
}
```

3-2. `setter()`메서드를 이용한다(Setter injection)<br>
```java
class MovieList{
  private MovieFind find;
  public void setFind(Moviefind find){
    this.find = find;
  }
}
```

3-3. 초기화 인터페이스를 통한 의존성 삽입(Interface Injection)<br>
이 방법은 스프링이 지원하지 않는 DI방식이라고 하여 넘어가도록 하겠습니다. 궁금하신 분은 참조 두번째 블로그에서 확인해보시면 될 것 같습니다.
<br>
DI Container에는 Spring Container(bean Factory), PicoContainer, Guice 등이 있다고 합니다.

### CI(Continuous Integration, 지속적인 통합)
CI란 개발자가 각각 개발한 소스코드들의 통합 빌드의 과정을 특정 시점이 아니라 주기적으로 수행함으로써 통합에서 발생하는 오류를 사전에 해결하고 시간을 줄이기 위한 기법을 말하게 됩니다.

#### CI 적용을 위한 4가지 영역
* 형상관리 항목에 대한 선정과 형상관리 구성 방식 결정
단순히 형상관리 도구(SVN, Git 등등)을 사용한다고 CI의 전제 조건을 만족하는 것이 아닙니다.<br>
단순히 소스코드, 설정파일 뿐 아니라 빌드, 배포시 포함되어야 하는 항목들도 존재 합니다.<br>
그리고 이러한 것들이 어떠한 구조로 포함되어야 할 지도 결정해야 합니다.

* 단위테스트 / 통합테스트 방식
테스트는 SW제품의 품질을 균일하게 유지하려는 목적이 있습니다. 테스트를 통해 기능적인 문제를 제거하고 안정적인 소프트웨어 개발을 할 수 있을 것 입니다. 하지만 테스트가 많아질 수록 CI를 수행하는 시간이 길어질 것이고 배포시간이 길어지는 단점이 있을 수 있습니다.<br>

* 비기능 속성(품질 속성) 관리 방식
* 빌드/배포 자동화 방식

#### CI 시스템 구축을 위한 핵심 구성요소
* CI server
  * Jenkins, Travis CI 등
* SCM(Source Code Management)
  * Git, SVN 등
* Built Tool
  * Maven, Gradle, Ant 등
* Test Tool
  * Junit, Mocha

### AOP




### 참조
* [http://vandbt.tistory.com/43](http://vandbt.tistory.com/43)
* [http://www.nextree.co.kr/p11247/](http://www.nextree.co.kr/p11247/)
* [http://www.nextree.co.kr/p10799/](http://www.nextree.co.kr/p10799/)
* [http://asfirstalways.tistory.com/303](http://asfirstalways.tistory.com/303)

<br/><br/>
