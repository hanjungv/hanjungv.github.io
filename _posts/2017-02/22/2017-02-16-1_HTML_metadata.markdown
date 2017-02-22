---

layout: post
title: "(ROR) Ruby Hash란?"
category: ROR

---

### Hash란?
> 다른 언어에서는 Dictionary라는 이름으로 많이 만나봤을 것.<br/>
unique한 key와 value를 가진다. 앞으로 ruby를 하면서 자주 만나게 될 것

* 선언 법을 보자. 밑의 6개의 예제가 있는데 6개 모두 동일한 의미를 갖게 된다.
~~~ruby
def home
	grades = {:jo => 30, :ho => 40}
	puts grades[:jo]

	grades2 = {"jo" => 30,"ho" => 40}
	puts grades2["jo"]

	grades3 = Hash["jo",30, "ho",40]
	puts grades3["jo"]

	grades4 = Hash[[["jo",30],["ho",40]]]
	grades4["jo"] = 20
	puts grades4.keys

	grades5 = Hash["jo" => 30, "ho" => 40]
	puts grades5["jo"]

	grades6 = Hash.new()
	grades6["jo"] = 30
	grades6["ho"] = 40
	puts grades6["jo"]
end
~~~

* 이런식으로도 사용할 수 있다. 예제
~~~ruby
def home2
    person  = { 1 => {"name" => "hanjung" , "from" => 199, "to" => 2012},
            2 => {"name" => "minjung" , "from" => 1919, "to" => 2020},
            3 => {"name" => "jungjung", "from" => 1111, "to" => 202020} }
    (1..3).each do |p|
        puts "#{person[p]["name"]} 그리고 #{person[p]["from"]} ~ #{person[p]["to"]}"
    end
end
~~~

* 참조
[https://docs.ruby-lang.org/en/2.0.0/Hash.html](https://docs.ruby-lang.org/en/2.0.0/Hash.html)

 <br/><br/>
