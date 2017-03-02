---

layout: post
title: "(ROR) LiveSearch 구현하기"
category: ROR

---

### LiveSearch가 뭘까?
<img src = '/post_img/201703/01/1.gif' height='400'><br/>
**이런거를 LiveSearch라 한다.**

### LiveSearch 할 때 사용한 거
* Ruby on rails
* AJAX
* JSON / JS

### 만들어보기

#### 먼저 환경설정

~~~
# 먼저 mysql에서 사용할 디비를 만들고
mysql> create databases liveSearch2

# 프로젝트를 만들겠습니다. 이렇게 치면 mysql 환경으로 자동설정 됩니다.
$ rails new liveSearch -d mysql

# 프로젝트에 와서 database.yml 에서 database: liveSearch2로 바꾸기

# 컨트롤러는 3개만 만들겠습니다. 검색하는 search / 추가하는 add
$ rails g controller home index add search

# 사용할 모델도 만들고
$ rails g model post title:string writer:string

# 그리고 마이그레이션
$ bundle exec rake db:migrate
~~~
그리고 route설정을 해주고 bootstrap도 사용하겠습니다.

#### 컨트롤러 보기

~~~ ruby
class HomeController < ApplicationController
  def index
    @posts = Post.all
  end

  def search
    # puts params.inspect
    @queryPosts = Post.where("title LIKE ?","%#{params[:query]}%")
    render json: @queryPosts
  end

  def add
      newPost = Post.new(title: params[:title], writer: params[:writer])
      newPost.save
      redirect_to :back
  end
end
~~~

* index 에서는 모든 내용을 보여주고 내용도 추가해준다.
* search는 where문으로 검색해서 json 형태로 전달하게 된다.
* add는 내용물 추가하기

#### 뷰 보기. style과 script가 한 곳에 있는 점 양해해주세요..

~~~ html
<style>
    .eachpost{
      border: 1px solid #c84646;width:300px; margin:10px auto; border-radius:10px
    }
    .eachpost span{
      word-break: break-all;
    }
</style>
<div class = 'container' style = 'margin:20px;'>
  <div class = 'container'>
    <h1># LIVE SEARCH FORM </h1>
    <!--입력 부분-->
    <form action = '/home/add' method = 'post'>
      <input type = 'text' name = 'title' id = 'title' class = 'form-control' placeholder="제목" style = 'margin:5px'/>
      <input type = 'text' name = 'writer' id = 'writer' class = 'form-control' placeholder="작성자"  style = 'margin:5px' />
      <button class = 'btn bnt-default' type = 'submit' style = 'margin:5px'>제출</button>
    </form>
  </div>
  <div class = 'container' style = 'margin-top:30px;'>
    <!--검색 부분-->
    <input type = 'text' name = 'query' class = 'form-control' id = 'query' placeholder="검색" style = 'width: 300px;margin:auto;'/>
    <!--출력 부분. 처음에 모든것 출력. 이후에는 넘어온 json파일 dom객체로 출력-->
    <div id = 'searchResult'>
      <% @posts.each do |post| %>
        <div class = 'container eachpost'>
          <span>제목 : <%=post.title%></span><br/>
          <span>작성자 : <%=post.writer%></span>
        </div>
      <% end %>
    </div>
  </div>
</div>
<script>
    // ajax 부분
    $("#query").keyup(function(){
      val = this.value;
      $.ajax({
          method: "POST",
          url: "/home/search",
          dataType: "JSON",
          data: { query:val },
          success : function(data) {
              $("#searchResult").empty();
              for(i = 0; i< Object.keys(data).length; i++){
                  $("#searchResult").append("<div class = 'container eachpost'><span>제목 : "
                      +data[i].title+"</span><br/><span>작성자 : "+data[i].writer+"</span></div>");
              }
          },
          error : function(xhr, status, error) {
              alert("에러발생");
          }
      })
    });
</script>
~~~

> 이런식으로 하게 되면 liveSearch 가 가능하다. JSON객체를 ROR에서 만지는 것에 대해 좀 더<br/>
정확하게 알아볼 필요가 있다. ㅠㅠ



<br/><br/>
