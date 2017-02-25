---

layout: post
title: "(ROR) ActiveRecord, validation과 Callback[2/3]"
category: ROR

---

##### 레일즈 가이드를 참조했습니다. 5.0.1 기준입니다.[링크](http://guides.rubyonrails.org/active_record_basics.html)

#### validation
1. Controller : 유지가 힘들다. 컨트롤러는 간결하게 유지를 해야한다는 컨셉을 지키자!
2. DB : 테스트 및 관리가 힘들다. 하지만 그 DB를 다른곳에서 사용한다면 좋은 방법이다.
3. 클라이언트 : 자바스크립트 단으로 관리를 한다. 만약 자바스크립트에 문제가 생기면? 그대로 통과해 버릴 수 있게 된다. <br/>사용자에게 바로 결과를 보여줄 때 사용가능
4. Model : 테스트, 유지보수에 편하다! 우회적으로 접근하는 것도 막게 된다. 레일즈에서 이에 해당하는 헬퍼를 제공한다.

> validation은 create, save, update 할 때 수행하게 된다. .new를 한 시점이 아니라 .save를 할 때

##### 에러확인하기
validation을 걸었을 때 error가 발생한다면 errors에 내용이 담기게 된다. 에러가 없다면 [] 빈 상태일 것이다.

~~~ruby
class Person < ApplicationRecord
  validates :name, presence: true
end
>> p = Person.create
>> p.errors
#=> {name: ["can't be blank"]}
~~~

##### validation helper
~~~ruby
# acceptance : 약관 동의
validates :are_you_sure, acceptance: true   #사용자 동의를 받을 수 있다

# validates_assciated : 모델관계입증, 대신 한 곳에서만 입증해야 한다. 양쪽을 한다면 무한 루프를 돌 거임
class Library < ApplicationRecord
  has_many :books
  validates_associated :books
end

# confimation : 입력재확인
validates :email, confirmation: true
# 이런식으로 사용하게 되면 뷰에서는 이런식으로 써줘야한다.
# <%= text_field :person, :email %>
# <%= text_field :person, :email_confirmation %>
# exclusion
validates :name, exclusion:{in: %w(admin root)} # 이런식으로 하면 name에 admin / root 는 안된다
# format
validates :legacy_code, format: { with: /\A[a-zA-Z]+\z/, message: "only allows letters" } #이런식으로 정규식과 사용할 수 있다.
# inclusion
validates :size, inclusion: { in: %w(small medium large), message: "%{value} is not a valid size" } #set을 만들어 저기서만 선택하게 함
# length
validates :name, length: { minimum: 2 }
validates :bio, length: { maximum: 500 }
validates :password, length: { in: 6..20 }
validates :registration_number, length: { is: 6 }
# numericality : 숫자만 받아
validates :games_played, numericality: { only_integer: true } # 여기서는 수 중에 정수만 받게
# presence
# absence
# uniqueness : 중복확인
# validates_with
# validates_each
~~~

 <br/><br/>
