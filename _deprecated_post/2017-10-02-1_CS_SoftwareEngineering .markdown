---

layout: post
title: "(SE) Software Engineering 중간고사 문제풀기"
category: CS

---

## 소프트웨어 공학 정리

> [소공책 7판 링크, http://dinus.ac.id/repository/docs/ajar/RPL-7th_ed_software_engineering_a_practitioners_approach_by_roger_s._pressman_.pdf](http://dinus.ac.id/repository/docs/ajar/RPL-7th_ed_software_engineering_a_practitioners_approach_by_roger_s._pressman_.pdf) 를 함께 읽으면서 강의 프린트와 정리해보자..

### 일단 어떻게 해야할 지 공부해야 할 지 모르니 2015-2 중간고사를 정리해보자
> 이 정리는 책과 수업, 프린트로만 구성이 되어있다. 다른 내용이 포함되면 교수님이 싫어할 것 같아서..

1. 소프트웨어란 무엇일까? 3가지를 작성해보세요.
    1. 기대했던 feature과 function, performance를 제공해주는 `instructions(computer program)`이다.
    2. 프로그램이 정보를 적절하게 조작할 수 있게 하는 `Data Structure(자료구조)`를 제공합니다.
    3. operation과 program의 사용법을 작성해 놓은 `documentation`을 의미하빈다.
2. Legacy Software의 정의와 특성에 대하여 말해 보시오!
    * 정의: 이미 과거에 개발되었으며 계속해서 비즈니스 요구사항 및 플랫폼 변경사항을 충족하도록 수정되어온 S/W 입니다. 이 S/W는 비즈니스를 받치고 있지만 유지보수 비용이 엄청나고 때때로 확장이 불가능한 소프트 웨어입니다.
    * 왜 바뀌어야 하는가? 
        * S/W는 새로운 환경에 맞춰서 변해야 합니다. 데이터 베이스나, 시스템에 맞춰지기도 해야하고 네트워크에 따라 변경되기도 해야합니다.
        * 그리고 비즈니스 요구사항에 맞춰서 새롭게 개발되기도, 기능이 강화 되기도 해야합니다.
    * 이러한 바뀜(리팩토링)은 기존에 만들어져 있던 레거시 소프트웨어를 기반으로 생성, 업데이트를 하게 됩니다. 완전 새롭게 base부터 개발을 하는 경우는 실제 회사에서 거의 없습니다. 
3. Unified Process의 정의와 특징에 대하여 말하시오. 
<img src = "../../../post_img/201710/02/1.png"/>
    * 탄생하게 된 간략한 History: 90년대 객체지향적으로 분석하고 설계하는 특징을 가진 모델링 방법을 여러 사람들이 고안하게 되고 이렇게 탄생한 것이 `UML(Unified Modeling Language)`이다. UML은 객체 지향 엔지니어링을 지원하는데 필요한 기술들을 제공했지만 프로젝트 팀이 기술을 적용할 때 프로세스 프레임워크를 제공하지는 못했습니다. 그래서 누군가 들은 몇년을 고민한 끝에 엔지니어링 프레임워크인 `Unified Process(UP)`가 탄생시키게 된다.
    * 그럼 UP를 설명해보자
        1. UP의 시작단계는  `inception`입니다. 그 중 먼저 일어나는 것은 `communication`이다. 이 시기에 비즈니스 요구사항을 식별하고 시스템의 대략적인 아키텍쳐가 이시기에 제안 됩니다. 이후 communication을 계속해서 반복적으로 거치면서 점진적으로 계획이 수립되게 됩니다. 개요, 기능등을 수립하는 단계입니다.
        다음으로 `Planning`입니다. 자원을 식별하고 위험과 일정을 정의하고 기초를 수립합니다.
        2. 다음 단계는 `elaboration`입니다. 이 단계는 그림처럼 `planning` 및 `modeling`를 거치게 됩니다. 앞 단계에서 계획되었던 사례들을 구체화하고 확장하며 아키텍쳐 표현을 구체화 합니다. 이 과정에서 use case model, requirements model, design model, implementational model, deployment model 을 만든다고 합니다. 때때로 이 과정에서 executable architectural baseline을 생성한다고 합니다. 이것은 모든 기능을 제공하지는 않지만 약간의 기능들을 보여주게 됩니다.
        3. 세번째 단게는 `construction`입니다. 이 단계에서는 최종 사용자가 `use case`를 작동 할 수 있도록 소프트 웨어를 개발합니다. 이 단계에서 구현과 테스트가 이뤄지고 필수적으로 구현되어야 하는 기능들이 모두 소스코드로 이뤄지게 됩니다.
        4. 네번째 단계는 `transition`입니다. 이 단계에서는 개발의 후반부와 테스트가 모두 이뤄지게 됩니다. 또한 사용자에게 베타 테스트를 제공하며 결함과 변경사항을 모두 보고합니다. 이 단계가 끝나면 릴리즈가 되게 됩니다.
        5. 마지막 단계는 `production`입니다. 일반적으로 배포 단계에 속하게 됩니다. 배포 후 지속적으로 모니터링을 하게 되고 변경 요청과 결함 보고 등이 이뤄지게 됩니다. 

5. Java 간단한 빈칸 채워넣기. (객체를 생성할 줄 아는가에 대한 문제)
    * 실습문제


----

## 보류인 내용 
4. UML의 3요소에 대하여 말하라.
    * 먼저 UML은 1,2 단원 책에 자세히 나오지 않는다. 고로 교수님이 말씀하신 것만 정리해보자
    * UML과 관련해서 나왔던 내용
        * S/W를 디자인 한다 -> UML을 통해 클래스, attribute등 하나하나 세세하게 디자인한다. UML을 통해서 자동으로 해주는게 많당
        * `Structure` / `Functional` / `Behavior`을 기준으로 디자인 해야한다. Structure는 Component를 구성하고 제품을 만들게 된다. Structure를 잘못할 경우 형성된 구성에서 큰 Overhead가 발생할 수 있다. Functional은 그 일을 어떤 순서로 할지 나타내게 된다. Behavior는 Component자체에서 어떤 일을 할지를 의미하게 된다.
    * **근데 3요소는 어디에서 나오는 말인지 모르겠다.그래서 구글에 찾아보니 이게 뭔지 안나온다.띠용.**
6. UML 중 동적 요소를 표현하는 Diagram을 세 가지 이상 서술하라.
    * 안배웠는데...
    * 다이어그램의 종류에는 클래스, 객체, 유즈케이스, 상태, 시퀀스 등등..
    * 동적 요소를 나타내는 다이어그램에는 타이밍, 시퀀스, 활동, 통신, 교류개요, 타이밍 등이 있다고 한다.
7. 요구사항 분석에서 가장 많이 쓰이는 2가지 방법을 말하시오.
    * Requirement는 5장이다.
8. Function Transition in Atomic Model 그림이 주어지고 각 함수들의 이름, 사용하는 변수 or DEVS Function, 함수의 역할에 대하여 자세하게 설명하시오.
    * ?
9. 해당 Sequence Diagram이 주어지고 State Diagram으로 그리는 문제
    * 이 또한 아직 배우지 않은 내용이다.
10. Sequence Diagram이 주어지고, 해당 일을 수행하는 Request_Msg과 Result_Msg.java를 작성하시오.
11. Hospital System에 대한 각 Actor와 Use Case의 리스트가 주어지고, System Boundary를 포함하여 Use-case Diagram을 작성하는 문제.


<br/><br/>
