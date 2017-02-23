---

layout: post
title: "(ROR) ROR에서 mysql을 사용해보자"
category: ROR

---

### 서론
사실 mysql을 사용하는 것은 생각보다 많이 쉽다. <br/>
줄 몇줄 추가뿐.. 이 계기로 mysql과 sqlite3의 차이점을 찾아봤다 <br/>

### mysql vs sqlite3
* 둘에게 각각 적절한 사용처가 있을지 찾아보고 비교해야 한다.
* 위 [DBEngine 사이트](http://db-engines.com/en/system/Microsoft+SQL+Server%3BMySQL%3BSQLite)를 보면
<br/>

기준  | mysql | sqlite3 |
:-----:|:------:|:-----:
DBModel | 관계형 DBMS | 관계형 DBMS
License | open source | open source
server | FreeBSD / Linux / OSX / Solaris / Windows | server-less
xml support | yes | no
support language | Ada / C / C# / C++ / D / Delphi / Eiffel / Erlang / Haskell /Java / JavaScript (Node.js) / Objective-C / OCaml / Perl / PHP / Python / Ruby / Scheme / Tcl | Actionscript / Ada / Basic / C / C# / C++ / D / Delphi / Forth / Fortran / Haskell / Java / JavaScript / Lisp / Lua / MatLab / Objective-C / OCaml / Perl / PHP / PL / SQL / Python / R / Ruby / Scala / Scheme / Smalltalk / Tcl
Server-side scripts | yes | no

둘의 큰 차이점을 나타내는 부분은 server-less라는 점. 둘의 각각 상대적인 장점이 뭐가 있을 지 찾아봐야한다.

* 위 [링크](https://www.reddit.com/r/django/comments/4vmyrm/sqlite_vs_mysql_vs_postgresql_whats_best_for_my/)에서 보면 (물론 장고 프로젝트로 고민하는 사람이지만 루비도 같은 ORM이니)
	1. 가벼운 앱, 싱글 유저가 사용할 때는 sqlite3가 나쁘지는 않다.
	2. 서버를 따로 두고 싶으면 mysql
	3. 괜히 sqlite쓰다가 mysql로 넘어가려고 하지마라!
	4. 개발용, 혼자 쓸때만 sqlite를 써라. 제발 production에서 제발 제발 쓰지마라 제발
	5. mysql이 환경설정은 더 걸리겠지만 그래도 mysql써라
	등등의 의견이 있다. 크게 이견이 없이 단합되는것같다. 그러므로 앞으로 ROR개발을 할 때는 mysql을 사용하도록 하겠습니다.

### 만들어보기
* project를 만들었습니다.
* mysql2 gem을 추가한 뒤 $bundle install을 해줍니다.

~~~ruby
gem 'mysql2'
~~~
* mysql에 들어가 사용할 DB를 미리 만들겠습니다. 똑같이 sqltest로 이름을 하겠습니다. 아직 아무것도 없군요!
<img src = '/post_img/201702/23/1.png' width='300'/><br/>
<img src = '/post_img/201702/23/2.png' width='200'/><br/>

* 그리고 /config/database.yml 에서 환경을 설정해줍시다.

~~~ruby
default: &default
  adapter: mysql2
  host: localhost
  username: root
  socket: /tmp/mysql.sock
development:
  <<: *default
  database: sqltest
test:
  <<: *default
  database: sqltest
production:
  <<: *default
  database: sqltest
~~~

* 그리고 잘 저장되는지 보기 위해 model과 controller를 만들어 보겠습니다. model의 이름은 sqlmodel입니다.

~~~
$ rails g model sqlmodel tit:string
$ rails g controller home index add
~~~

* 컨트롤러와

~~~ruby
class HomeController < ApplicationController
  def index
    @allData = Sqlmodel.all
  end

  def add
    @s = Sqlmodel.new(tit:params[:tit])
    @s.save

    redirect_to :back
  end
end
~~~
* 뷰

~~~ html
<form action = '/home/add' method = 'get'>
  <input type = 'text' name = 'tit'>
  <button type = 'submit'>submit</button>
</form>

<% @allData.each do |p| %>
  <p><%= p.tit %></p>
<% end %>
~~~
내용을 쳐서 출력을 시켜보겠습니다. 잘 나오네요!<br/>
<img src = '/post_img/201702/23/3.png' width='300'/><br/>
터미널에서 보게 되면<br/>
<img src = '/post_img/201702/23/4.png' width='200'/><br/>
못보던게 생겼네요<br/>
<img src = '/post_img/201702/23/5.png' width='500'/><br/>
제 mysql에 잘 저장이 되는것을 볼 수 있습니다. **레일즈는 참 쉽군요**



 <br/><br/>
