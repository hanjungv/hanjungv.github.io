---

layout: post
title: "(CS) DB Review"
category: CS

---


# OS 리뷰
## 시작하면서
> DB 수업을 들은게 벌써 5년....수업자료도 사라지고 리뷰를 하려니 자료가 마땅치 않아서 이화여대 등등 여러 대학강좌를 참조하여 공부하였다. 두서없이 필요한 키워드만 정리하여 보기 매우 불편 할 수 있으니 양해 부탁드린다.

### 정리시작
1. 스키마란?
    * 데이터베이스의 전체적인 논리적 설계를 의미, 데이터 관계, 성질 등이 갖는 제약조건에 관한 것을 총칭한다. 인스턴스에 의해 규정된다. DDL(Data Definition Language)로 정의된다.
    * 3-level DB구조에 기반
        * 외부 스키마(external schema)
            * 개개 사용자 관점에서 정의한 디비 스키마
            * 전체 DB의 한 논리적인 부분
            * subschema
        * 개념 스키마(conceptual schema)
            * 범 기관적인 관점에서 정의
            * 모든 응용에 대한 전체적인 통합적인 데이터 구조, 데이터 뮤결성 규칙
            * schema
        * 내부 스키마(internal schema)
            * 저장장치 관점에서의 DB 스키마
            * 저장 구조를 정의
    * 카탈로그(딕셔너리)
        * 시스템에 정의된 모든 객체들의 정의나 명세를 수록
        * DBA가 관리하는 도구이다.
```
STUDENT
number INTEGER
Name CHAR(10)
YEAR INTEGER
ADDRESS CHAR(44)
DEPT CHAR(44)
```
이런식으로 다 정의 되어있으면 개념스키마
```
STUDENT
number INTEGER
DEPT CHAR(44)
```
이런식으로 필요한 것들을 뽑아서 사용하면 외부 스키마
```
STORED-STUDENT LENGTH = 81
prefix BYTE(4) OFFSET = 0
....
```
이런식으로 실제 스토리지 관점에서 작성 된게 내부 스키마

2. E-R 모델이란?
    * Entity-Relationship Model
    * 개념적 단계에서 개체내의 관계, 개체와 개체 사이의 사상 관계를 표현하는데 쓰이며 사용자 관점에서 가장 좋은 도구로 많이 사용되는 모델이다.
    <img src= "../../../post_img/201710/04/1.png"/>
    * 개체 관계에는 아시다시피 1:1, 1:N, N:M 등이 있다.

3. 데이터 정규화란?
    * 관계형 데이터 베이스 설계에서 중복을 최소화하게 데이터를 구조화 하는 프로세스를 정규화라고 한다.
    * 1NF(Normal Form), 2NF, 3NF, BCNF, 4NF, 5NF, 6NF가 있으며 보통 3NF가 되면 '정규화 되었다'라고 한다. 
    * 1NF: 행과 열의 순서에 영향을 받지 않으며 모든 항목에 값이 있어야 한다.(NULL 안됨!) 또한 중복 기능 열이 없어야한다.
    * 2NF: 정적인 데이터에서 한 필드가 다른 필드를 정의할 수 있을 때 첫번째 그림보다 두번째 그림이 옳은 그림이다.
    <img src= "../../../post_img/201710/04/2.png"/>
    <img src= "../../../post_img/201710/04/3.png"/>
    * 3NF: 계산열 제거, 계산이 가능한 열은 제거한다.
        * 만약 생년월일, 나이, 주민등록번호를 모두 가지고 있다면 주민등록번호 하나면 나이와 생년월일을 계산할 수 있게된다.고로 나이와 생년월일 attribute를 제거한다.
    * 3NF 테이블의 대부분이 삽입, 변경, 삭제 이상이 없으며, 3NF 테이블의 대부분이 BCNF, 4NF, 5NF이다.(그러나 일반적으로 6NF는 아니다.)라고 한다.

4. 후보키, 기본키(Primary Key), 대체키(Alternate Key), 외래키(Foreign Key), 슈퍼키(Super Key)
    * 유일성: 릴레이션으로 입력되는 모든 튜플을 유일하게 구별할 수 있는 성질
    * 최소성: 가장 적은 개수의 어트리뷰트로 구성될 수 있는 성질
    * 이러한 특징을 가지고 있는 속성(Attribute)의 집합을 `후보키`라 한다.
    * PK는 후보키 중 설계자에 의해 선택된 한개의 키를 의미, 중복되지 않으며 NULL값을 가질 수 없다.
    * 후보키 중 PK를 제외한 나머지 후보키는 `대체키(Alternate Key)`이다.
    * `외래키(Foreign Key)`는 각 테이블끼리 관계를 맺어줄 때 사용한다. 
    * `슈퍼키(Super Key)`는 최소성 없이 단지 튜플을 식별하기 위해 두개 이상의 속성들의 집합으로 만들어진 키를 의미한다.

5. 무결성 제약사항 3가지 설명(도메인, 개체, 참조)
    1. 도메인 무결성이란?
        * 데이터베이스 테이블에서 주어진 속성으로 입력되는 모든 값은 그 속성으로 정의되거나 제약된 도메인 영역에 있어야 된다는 것을 의미. 
        * 만약 성별을 나타내는 곳에서 'M', 'W'만 입력하게 되어있는데 'X'같이 다른 데이터가 들어올 경우를 방지해야함
    2. 개체(Entity) 무결성이란?
        * 하나의 개체 릴레이션에서는 중복된 튜플이 있으면 안된다는 제약을 의미한다.
        * 튜플을 삭제, 갱신, 삽입 하고 나서도 그 전후의 관계가 의미적으로 이상이 없음을 규정하는 것
    3. 참조(Reference) 무결성이란?
        * 각 테이블끼리 관계되는 정보의 정확성을 유지하는가를 규정하는 것으로 외래키에 의해 유지된다.

## 참조
* [https://ko.wikipedia.org/wiki/%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4_%EC%A0%95%EA%B7%9C%ED%99%94](https://ko.wikipedia.org/wiki/%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4_%EC%A0%95%EA%B7%9C%ED%99%94)
* [https://www.youtube.com/watch?v=vOWqGCWKg2I&list=PL6i7rGeEmTvr9xsX7aajidZVEwmkDra9W&index=8](https://www.youtube.com/watch?v=vOWqGCWKg2I&list=PL6i7rGeEmTvr9xsX7aajidZVEwmkDra9W&index=8)
* [https://blog.lael.be/post/71](https://blog.lael.be/post/71)

<br/><br/>
