---

layout: post
title: "(ROR) ActiveRecord, Association과 query[3/3]"
category: ROR

---

##### 레일즈 가이드를 참조했습니다. 5.0.1 기준입니다.[링크](http://guides.rubyonrails.org/active_record_basics.html)
##### 계속적으로 공부하면서 업데이트 하도록 하겠습니다ㅠㅠ 이제 개강이라

### Association
* 주로 단 방향 형태이다. 종류를 살펴보자
    * belongs_to ( ~에 의존하고 있다하는 것을 표현 )
    <br/><img src = '/post_img/201702/26/1.png' width=500/><br/>
    * has_one ( 종속적이지만 하나만 가져야하는 경우! belongs_to와 반대 )
    <br/><img src = '/post_img/201702/26/2.png' width=500/><br/>
    * has_many ( 종속적인데 여러개를 가질 수 있는 경우! belongs_to와 반대 )
    <br/><img src = '/post_img/201702/26/3.png' width=500/><br/>
    * has_many :through ( M:N관계를 나타낼 때 사용, 중간테이블을 놓고 바인딩 시킴 )
    <br/><img src = '/post_img/201702/26/4.png' width=500/><br/>
    * has_one :through (거~의안씀)
    <br/><img src = '/post_img/201702/26/5.png' width=500/><br/>
    * has_and_belongs_to_many ( 중간 테이블의 존재를 없애버려 이렇게 사용하게 됨 )
    <br/><img src = '/post_img/201702/26/6.png' width=500/><br/>
    * self-join
...기본적인 내용은 여기까지

### Query
* 데이터베이스에서 객체 가져오기
    * 단일 객체 가지고 오기

    ~~~ruby
    # find
    client = Client.find(10) # id가 10인 client를 찾아서 반환
    client = Client.find([1, 10]) # id가 1이나 10인 client를 찾아서 반환
    # take : 어떤 데이터를 가져올 지 정하지 않고 가지고 옴
    client = Client.take(2) # 아무거나 두개 가지고 와
    # first / last : 첫번째, 마지막. order시킨 후 가지고 올 수 있다.
    client = Client.first
    client = Client.last
    # find_by : 주어진 조건에 맞는 첫번째 레코드를 반환
    Client.find_by first_name: 'Lifo' # first_name이 Lifo인 친구를 반환
    ~~~
    * 여러개의 객체를 가지고 오기

    ~~~ruby
    # 만약 여러사람들에게 모두 동일한 행동을 할 때 이런식으로 하면 매우 느릴 것. 추후에는 메모리가 부족하게 될 것
    User.all.each do |user|
      NewsMailer.weekly(user).deliver_now
    end
    # find_each : find_each는 각 레코드를 하나의 객체로 만들어 호출하게 됩니다. default는 1000개 입니다.
    User.find_each(batch_size: 5000) do |user| # 여기서 batch_size: 는 몇개를 하나의 객체로 만들어 호출할 지를 나타내게 됩니다.
      NewsMailer.weekly(user).deliver_now
    end
    User.find_each(start: 2000, finish: 10000) do |user| # 기본 키가 2000이상 10000이하인 사용자에게만 호출되게 됩니다.
      NewsMailer.weekly(user).deliver_now
    end
    # find_each를 사용하면 속도를 꽤 높일 수 있는 요인이 된다.
    ~~~
* 조건문

~~~ruby
# where을 통해 넘겨받은 여러개의 조건에 맞는 Client를 배열로 반환합니다.
Client.where("orders_count = ? AND locked = ?", params[:orders], false)
# 이런식의 입력보다는
Client.where("orders_count = #{params[:orders]}")
# 이런식을 선호해주시길 바랍니다.
Client.where("orders_count = ?", params[:orders])
~~~
* 순서 만들기

~~~ruby
> order
Client.order(created_at: :desc)
Client.order(created_at: :asc)
# OR
Client.order("created_at DESC")
Client.order("created_at ASC")
# 복수의 필드를 할 때는
Client.order(orders_count: :asc, created_at: :desc)
# OR
Client.order("orders_count ASC, created_at DESC")
~~~


* scoping
* none
* merge
<br/><br/>
