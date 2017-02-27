---

layout: post
title: "(ROR) RESTful URL 설계하기"
category: ROR

---

### URL이 중요한 이유
* 로직 설계의 첫걸음
* SEO
* 공개 후 변경 비용이 크게 된다.

### REST(Representational State Transfer)이란?
> 장비간 통신을 SOAP, RPC 등 복잡한 방법 대신 HTTP를 이용한다.<br/>
웹사이트의 이미지, 텍스트, 파일 등에 고유한 URI를 부여하여 관리하게 된다.<br/>
**원격 서버의 리소스(데이터)에 대한 상태 교환. 웹의 장점을 최대한 살리는 방향으로 가자!하는것이 목적**<br/>
지키는게 좋다. 지키는게 좋다. 지키는게 좋다. 지키는게 좋다.

#### RESTful == 'REST의 원칙을 따르는..'

### REST 원칙의 구성요소
* 메서드 : HEAD, GET, POST, PUT/PATCH, delete
* 리소스 : Article, Comment
* 메세지 : HTTP 상태 코드 및 본문

### RESTful하게 설계 하는 것은 뭘까?
* 적절한 HTTP 메서드를 사용한다.
    * 불러올 땐 GET / 변경할 땐 POST, PUT(PATCH), DELETE
* HTTP 메서드 오버라이드
    * 일부 브라우저, 프록시에는 GET, POST만 사용이 가능할 수 있다.
    * 그럴 땐 힌트를 주자. XHTTP등..
* 리소스는 명사로 표현하자. 리소스는 단 두가지다. 컬렉션과 인스턴스

/ | 표현 | GET | POST | PUT | DELETE
:---:|:---:|:---:|:---:|:---:
콜렉션 | /articles | 글 목록 | 글 저장 | 없음 | 글 전체 삭제?
인스턴스 | /articles/:id | id글 조회 | 없음 | id글 수정 | id글 삭제
* 복수형 리소스이름, 일관된 대소문자

~~~
GET /articles (o)
GET /article (x,선호하지 않아)
~~~
* 관계를 노출할 땐 리소스 중첩

~~~
GET /tags/:id/articles (o)
GET /tags?1?submodel = articles (x,선호하지 않아)
~~~
* 컬렉션과 인스턴스를 조회할 때 복잡한 것은 ?로

~~~
GET /articles?q=Lorem
GET /articles?page=2
~~~
* 알맞은 HTTP에러 코드를 사용한다.
    * 200 : 성공
    * 201 : 리소스 생성 성공. created
    * 204 : 삭제 같은것을 할 때 사용
    * 304 : 캐시된 리소스 대비 서버 리소스의 변경이 없을 때
    * 400 : Bad request
    * 401 : 인증 필요
    * 403 : 권한부족. forbidden
    * 404 : 요청한 리소스가 없음. Not found

### ROR과 REST
> ROR에서는 리소스 기반으로 RESTful하게 라우팅을 설정하는 방법을 제공합니다.<br/>
저는 resources :photos 란 한 줄을 라우팅에 입력했을 뿐인데 이 7가지를 알아서 다 만들어주게 되죠.

HTTP 메서드 | 경로	| 컨트롤러#액션 | 목적
:---:|:---:|:---:|:---:
GET|	/photos	| photos#index	| 모든 사진 목록을 표시
GET|	/photos/new| 	photos#new	| 사진을 1개 생성하기 위한 HTML 양식을 반환
POST|	/photos| 	photos#create	| 사진을 1개 생성
GET|	/photos/:id	| photos#show	| 특정 사진을 보여줌
GET|	/photos/:id/edit	| photos#edit	| 사진 편집용의 HTML 양식을 반환
PATCH/PUT|	/photos/:id	| photos#update	| 특정 사진을 갱신
DELETE|/photos/:id	| photos#destroy	|특정 사진을 삭제

* 여러개를 한꺼번에 할 때는 **resources :photos, :books, :videos** 이렇게 쓰세요!

* namespace로 그룹을 묶을 수 있습니다. 이 때는

~~~ ruby
namespace :admin do
  resources :posts, :comments
end
~~~
HTTP 메서드	|경로|	컨트롤러#액션|	네임 스페이스 헬퍼
:---:|:---:|:---:|:---:
GET|	/admin/posts	|admin/posts#index	|admin_posts_path
GET|	/admin/posts/new	|admin/posts#new|	new_admin_post_path
POST|	/admin/posts	|admin/posts#create	|admin_posts_path
GET|	/admin/posts/:id|	admin/posts#show	|admin_post_path(:id)
GET|	/admin/posts/:id/edit	|admin/posts#edit|	edit_admin_post_path(:id)
PATCH/PUT|	/admin/posts/:id	|admin/posts#update|	admin_post_path(:id)
DELETE|	/admin/posts/:id|	admin/posts#destroy	|admin_post_path(:id)

* 중첩되는 resources에는

~~~ ruby
# 관계가 이런식으로 되어있고
class Magazine < ActiveRecord::Base
  has_many :ads
end
class Ad < ActiveRecord::Base
  belongs_to :magazine
end
# 이럴 때는 이렇게 중첩해서 적어준다.
resources :magazines do
  resources :ads
end
~~~

HTTP 메서드 |	경로	|컨트롤러#액션	|목적
:---:|:---:|:---:|:---:
GET|	/magazines/:magazine_id/ads|	ads#index	|잡지 1권에 포함되는 광고를 모두 표시한다.
GET	|/magazines/:magazine_id/ads/new|	ads#new	|어떤 잡지에 광고를 추가할 수 있는 HTML 양식을 반환한다.
POST	|/magazines/:magazine_id/ads	|ads#create	|어떤 잡지 1권에 잡지용의 광고를 하나 추가한다.
GET	|/magazines/:magazine_id/ads/:id	|ads#show	|어떤 잡지 1권에 포함되는 광고를 하나 보여준다.
GET	|/magazines/:magazine_id/ads/:id/edit|	ads#edit|	어떤 잡지 1권에 포함되는 광고 하나를 수정할 수 있는 HTML 양식을 반환한다.
PATCH/PUT	|/magazines/:magazine_id/ads/:id	|ads#update	|어떤 잡지 1권에 포함되는 광고 하나를 갱신한다.
DELETE	|/magazines/:magazine_id/ads/:id	|ads#destroy	|어떤 잡지 한권에 포함되는 광고를 하나 삭제한다.

* 꼭 7개 이어야 하는 보장은 없습니다. 여기서 더 추가를 하려면 member block을 이용하게 됩니다.

~~~ ruby
resources :photos do
  member do
    get 'preview'
  end
end
~~~

#### RORLAB 유튜브 [강좌](https://www.youtube.com/watch?v=XuhFsEPkTOc)와 [가이드](http://guides.rubyonrails.org/routing.html)를 참조했습니다.

<br/><br/>
