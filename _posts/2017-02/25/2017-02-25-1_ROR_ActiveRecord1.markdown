---

layout: post
title: "(ROR) ActiveRecord, 개념과 CRUD[1/3]"
category: ROR

---

##### 레일즈 가이드를 참조했습니다. 5.0.1 기준입니다.[링크](http://guides.rubyonrails.org/active_record_basics.html)

### ROR에서의 개략적인 MVC 바라보기
1. model : ActiveRecord
2. view : Layout & rendering / Form Helper
3. Controller : ActionController

### 먼저 루비의 꽃 ActiveRecord 부터 천천히 보자
> ActiveRecord란 RBDMS의 테이블을 ORM(Object Relational Mapping)해서 SQL을 직접 사용하지 않고 데이터를 조작하게 해준다.
<br/>레일즈에서 ActiveRecord는 ORM Framework로써 **모델과 데이터, 상속, 연관관계등을 나타내며 저장이전에 검증하기 등을 객체지향적으로 수행한다**
<br/>실제로 ORM은 Configuration 코드가 상당히 많이 필요하게 되는데 레일즈는 **convention(관례)** 로 이를 편하게 해버린다.
<br/>[ActiveRecord pattern의 설명](https://www.martinfowler.com/eaaCatalog/activeRecord.html)은 여기에 있다.

#### CRUD
* create

~~~ruby
# 세게 다 같은 작동을 하지만 필자는 3번을 선호.
user = User.create(name: "David", occupation: "Code Artist")
# 혹은
user = User.new
user.name = "David"
user.occupation = "Code Artist"
user.save
# 혹은
user = User.new(name:"David", occupation:"Code Artist")
user.save
~~~
* read

~~~ruby
# 다읽거나
users = User.all
# 첫번째만 보거나
user = User.first
# find_by를 써서 해당 하는 값을 찾거나
david = User.find_by(name: 'David')
# where를 써서 찾을 수도 있습니다. 여기서는 만들어진 순서대로 내림차순 정렬을 했네요
users = User.where(name: 'David', occupation: 'Code Artist').order(created_at: :desc)
~~~
* update

~~~ruby
# 이름으로 찾아서 바꿔주기
user = User.find_by(name: 'David')
user.name = 'Dave'
user.save
# 아니면 전부 업데이트 시켜버리기. 여기서는 로그인 시도 횟수를 한정시켜 버렸네요
User.update_all "max_login_attempts = 3, must_change_password = 'true'"
~~~
* destroy

~~~ruby
# 삭제하기
user = User.find_by(name: 'David')
user.destroy
~~~

##### validation 과 Callback, Association과 query문은 다음페이지에

 <br/><br/>
