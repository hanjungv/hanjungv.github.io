---

layout: post
title: "(SPRING) Spring CI, DI, AOP에 대해 알아보자"
category: SPRING 

---

## Spring IoC/DI, CI, AOP 에 대해 정리해보자

### IoC(Inversion of Control, 제어의 역전)/DI(Dependency Injection, 의존성 주입)

1. IoC(Inversion of Control)이란?
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
<br>
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
* `생성자`를 이용한 의존성 삽입(Constructor Injection)<br>
```java
class MovieList{
  public MovieList(MovieFind find){
    this.find = find;
  }
}
```

* `setter()`메서드를 이용한다(Setter injection)<br>
```java
class MovieList{
  private MovieFind find;
  public void setFind(Moviefind find){
    this.find = find;
  }
}
```

* 초기화 인터페이스를 통한 의존성 삽입(Interface Injection)<br>
이 방법은 스프링이 지원하지 않는 DI방식이라고 하여 넘어가도록 하겠습니다. 궁금하신 분은 참조 두번째 블로그에서 확인해보시면 될 것 같습니다.
<br>
DI Container에는 Spring Container(bean Factory), PicoContainer, Guice 등이 있다고 합니다.

### CI(Contiguous Integration, 지속적인 통합)


### AOP




### 참조
* [http://vandbt.tistory.com/43](http://vandbt.tistory.com/43)
* [http://www.nextree.co.kr/p11247/](http://www.nextree.co.kr/p11247/)



<br/><br/>
