---

layout: post
title: "(CS) DB Review"
category: CS

---


# OS 리뷰
## 시작하면서
> DB 수업을 들은게 벌써 5년....수업자료도 사라지고 리뷰를 하려니 자료가 마땅치 않아서 이화여대, 정보처리기사, 생코 등등 여러 강좌를 참조하여 공부하였다. 두서없이 필요한 키워드만 정리하여 보기 매우 불편 할 수 있으니 양해 부탁드린다.

### DB
1. 스키마란?
    * 데이터베이스의 전체적인 논리적 설계를 의미, 데이터 관계, 성질 등이 갖는 제약조건에 관한 것을 총칭한다. 인스턴스에 의해 규정된다. DDL(Data Definition Language)로 정의된다. 테이블에 적재 될 데이터의 구조와 형식을 정의한다.
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
    <br/>
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

6. 관계 대수(Relational Algebra)
    * 집합연산자
        * Union(합집합)
            * 두 테이블에 속하는 튜플 전부
        * Intersection(교집합)
            * 공통으로 속하는 튜플 집합
        * Difference(차집합)
            * R-K일경우 R에는 속하지만 K에는 속하지 않는 튜플
        * Cartesian Product(곱집합)
            * RXK일 경우 R의 속성과 K의 속성을 다 곱해서 나올 수 있는 모든 경우의 수의 튜플을 테이블로 합쳐서 만들어준다.
    * 관계연산자
        * Selection(셀렉션)
            * 하나의 테이블에서 조건에 맞는 튜플로 분리해 내는 연산
            * SELECT * FROM 학생 where 점수>=70
            * σ(조건)(R) , R = 릴레이션 이름
        * Projection(프로젝션)
            * 속성을 선택하는 것, 수직적
            * π(속성리스트)(R)
        * Join(조인)
            * 두 개 이상의 릴레이션에서 조건에 맞는 조건을 속성이 들어있는 튜플을 접속하여 새로운 릴레이션을 생성하는 방법
            * R ⋈ 키속성 r = 키속성 s S (키속성 r = 릴레이션 R의 속성, 키속성 s = 릴레이션 S의 속성)
        * Division(디비전)
            * 두 개의 릴레이션 R과 K가 있을 때 K릴레이션의 모든 조건을 만족하는 경우 튜플들을 릴레이션 R에서 분리해 내어 프로젝션 하는 연산
            * R[속성r ÷ 속성s]S (속성r은 릴레이션 R의 속성, s는 릴레이션 S의 속성, 속성 r = 속성 s)

7. SQL(여기서부터 생코강좌)
    * 생성(DB, Table): `CREATE DATABASE 데이터베이스명 CHARACTER SET utf8 COLLATE utf8_general_ci;`
    * 삭제: `DROP DATABASE 데이터베이스명;`
    * 열람: `SHOW DATABASES;`
    * 선택: `USE 데이터베이스명`
    * 테이블
        * 생성
        ```sql
        CREATE TABLE `student` (
            `id`  tinyint NOT NULL ,
            `name`  char(4) NOT NULL ,
            `sex`  enum('남자','여자') NOT NULL ,
            `address`  varchar(50) NOT NULL ,
            `birthday`  datetime NOT NULL ,
            PRIMARY KEY (`id`)
        );
        ```
        * 스키마 열람: `DESC 테이블명`
        * 데이터 타입
            * CHAR, VARCHAR(데이터에 따라 저장용량 가변), TEXT, BLOB 정도 많이 쓴다.
            * INT, TINYINT도 많이쓴다.
            * ENUM(정해진 값중 하나만 입력되도록 정한다.)
        * 삽입: `INSERT INTO table_name VALUES (value1, value2, value3,...)`혹은 `INSERT INTO table_name (column1, column2, column3,...) VALUES (value1, value2, value3,...)`로 한다. 후자의 경우 순서에 딱 맞춰서 이뤄져야한다.
        * 변경: `UPDATE 테이블명 SET 컬럼1=컬럼1의 값, 컬럼2=컬럼2의 값 WHERE 대상이 될 컬럼명=컬럼의 값`
        * 삭제: `DELETE FROM 테이블명 [WHERE 삭제하려는 칼럼 명=값]`
        * 조회: 순서는 중요하다.
        ```sql
        SELECT 칼럼명1, 칼럼명2 
            [FROM 테이블명 ] 
            [GROUP BY 칼럼명] 
            [ORDER BY 칼럼명 [ASC | DESC]] 
            [LIMIT offset, 조회 할 행의 수]
        ```
            * `SELECT * FROM student LIMIT 0,1`: 0은 offset, 1은 row count를 의미해서 첫번째 행부터 1개 가지고 온다는 것을 의미한다. 
        * 그루핑: 특정 칼럼을 기준으로 데이터를 그루핑함
            * `SELECT sex FROM student GROUP BY sex;`
                * sex에 어떠한 형들이 들어있는지 쉽게 알 수 있음
            * `select sex,sum(distance), avg(distance) from student group by sex;`
                * sex를 기준으로 거리의 합과 평균을 구해줄 수 있다.
        * 정렬: 기준을 두어 그 기준대로 데이터를 정렬함
            * `SELECT * FROM 테이블명 ORDER BY 정렬의 기준으로 사용할 열 [DESC | ASC]`
        * index: 색인, 조회할 때 원하는 행을 빠르게 찾을 수 있게 준비해둔 데이터
            * 인덱스의 종류: Primary(각각의 행들에서 중복되지 않는 값들), normal(중복이 허용됨), unique(==Primary, 빠르지만 여러개를 지정할 수 있음), foreign, full text
            * 정의하기: 자주 조회되는 칼럼, 한번 조회할 때 오래걸리는 칼럼에서 사용한다. url처럼 데이터가 긴 경우에서는 인덱스를 사용하지말자
        * join: 데이터가 규모가 커지면서 하나의 테이블로 데이터를 유지하기 어려워 테이블을 분할하고 테이블간 관계를 부여한다. Join을 통해 하나의 테이블 처럼 결과값을 가져올 수있게 된다.
            * OUTER JOIN: 매칭되는 행이 없어도 결과 값을 가지고 오고 없을 경우 NULL로 표현한다.
                * LEFT JOIN: 가장 많이 사용하는 조인, 왼쪽에 있는 테이블을 기준으로 오른쪽 테이블의 데이터를 가지고 온다는 것을 의미
                    * `SELECT s.name, s.location_id, l.name AS address, l.distance  FROM student AS s LEFT JOIN location AS l ON s.location_id = l.id;`
                        * AS를 통해 테이블 마다 명칭을 붙여서 씀
                        * ON을 통해 테이블끼리 같은 데이터를 알려줌
                * RIGHT JOIN
            * INNER JOIN: 조인하는 두개의 테이블 모두에 데이터가 존재하는 행에 대해서만 결과를 가지고 온다. NULL로 뜬다면 데이터를 가지고 오지 않는다.

8. 트랜잭션(다시돌아와서)
    * 트랜잭션은 데이터베이스에서 일어나는 연산의 집합이다.
    * 하나의 논리적 기능을 수행하기 위한 작업의 단위이다.
    * 데이터베이스의 상태를 하나의 일관된 상태에서 다른 일관된 상태로 변화시킨다.
    * 하나의 트랜잭션은 완료(Commit)되거나 복귀(Rollback)되어야 한다. 
    * 특징
        1. 원자성(Atomicity): 트랜잭션은 분리해서 일할 수 없고, 따라서 일부의 완료라는 것은 존재하지 않는다. 데이터베이스에 모두 반영되든지 전형 반영되지 않아야한다.
        2. 일관성(Consistency): 실행 전과 후가 같아야 한다는 성질이다. 데이터베이스의 무결성이 유지되어야한다.
        3. 독립성(isolation): 격리성, 트랜잭션이 실행되는 중간에 다른 트랜잭션 연산이 침범하지 못하는 성질이다.
        4. 영속성(Durability): 지속성, 계속성. 변화된 상태는 지속해서 유지되어야한다.

9. 암호화기법
    1. 공통키 방식(대칭형 암호화 알고리즘)
        * A에서 key를 가지고 암호화 시켜서 B에 전달하면 B에서 key를 가지고 해독해서 본다.
        * 이때 키는 같은 키를 가지고 있고 이 방식을 공통키 방식이라고 한다.
        * 이때 송신측에서 key가 유출된다면 모든게 무너져 버린다.
    2. 공개키 방식(비대칭형 암호화 알고리즘 )
        * B에서는 공개키와 비밀키를 갖는다. 두 개가 있어야 반드시 해독된다.
        * A에서는 공개키만 갖고 공개키를 통해 암호화를 하고 이 암호화 한 데이터를 공개키와 비밀키 두개를 이용해서 해독해서 본다. 

10. 트리거
    * 선언적 형태의 무결성 규정은 무결정 규정 위반시 취소 외에 다른 조치를 명세하고자 할 때 트리거를 사용한다.
    * 트리거는 트리거 조건식에 따라 메세지를 전달하거나 데이터를 자동으로 갱신할 수 있도록 함수나 명령문을 수행하게 된다.

11. 병행제어란?
    * 여러 사용자가 동시에 디비에 액세스하게 되면 많은 트랜잭션들이 동시에 발생하게 된다. 이러한 트랜잭션이 일관성을 갖고 제대로 처리되기 위해서는 직렬성이 보장되어야 하는데 이러한 직렬성 보장을 위한 일련의 방법(중지, 지연) 등을 병행제어라한다.
    * 데이터베이스의 공유도를 최대화 하고 일관성을 유지하고자한다. 
    * 로킹(Locking): Lock를 소유하고 있어야만 사용가능해진다.

## 참조
* [https://ko.wikipedia.org/wiki/%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4_%EC%A0%95%EA%B7%9C%ED%99%94](https://ko.wikipedia.org/wiki/%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4_%EC%A0%95%EA%B7%9C%ED%99%94)
* [https://www.youtube.com/watch?v=vOWqGCWKg2I&list=PL6i7rGeEmTvr9xsX7aajidZVEwmkDra9W&index=8](https://www.youtube.com/watch?v=vOWqGCWKg2I&list=PL6i7rGeEmTvr9xsX7aajidZVEwmkDra9W&index=8)
* [https://blog.lael.be/post/71](https://blog.lael.be/post/71)
* [http://blog.daum.net/amajerry/28](http://blog.daum.net/amajerry/28)
<br/><br/>
