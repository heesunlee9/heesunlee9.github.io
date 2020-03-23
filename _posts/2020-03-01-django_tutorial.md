---
title:  "Django Tutorials"
excerpt: "Django Tutorials"

categories:
  - Blog
tags:
  - Blog
last_modified_at: 2019-04-13T08:06:00-05:00
---

함수들 쓴이유. 원래는 유저이름으로 로그인하는데 유리는 유저이름 자리에 이메일 넣는다. 그래서 써준다.  

_create_user : 이 클래스 내에서만 사용!
create_user :  밖에서 호출가능 

과제: 
1. BaseUserManager 원래 코드 보는 거 어떻게 하나? 함수 호출할때 뭐 채울지 알려면 봐야함  
autopep8 설치 

2. ** 뭐임? 
3. 매직 메소드 

# 03 Framework Django 기초
가상환경 켜기(뭐든지 OK)  
> pip install django  
> django-admin startproject [name]  
> python manage.py startapp [name]  
앱만들고 나서 프로젝트의 settings.py 가서 앱 등록

6.  
모델 만들기 models.py  

7.  
python3 manage.py makemigrations (모델 만들어줌)  
> python3 manage.py migrate    (db 만들어주거나 수정해줌)      
DB 수정하면 두 개 다시   

문제 생기면 아래로 삭제 후 위에 두 개 다시   
> rm db.sqlite3    
abstract 써서 모델에 이력이 잘못 넘겨질 수 있다. 장고의 문제임

DB 확인 
sqlite3 db.sqlite3
.schema fastcampus_fcuser
.q

8. admin  
python3 manage.py createsuperuser    
python3 manage.py runserver  

9.  
user 앱의 admin.py 가서 모델 등록(앱을 등록하는 거라고 봐도 무방)    
user 정보를 보기 쉽게 표현하기  
파이썬은 원래 클래스를 문자열로 바꾼 걸 어드민 페이지에 보여줌
어떻게 바꿀지 내장함수로 정의할 수 있다. 
예: 
def __str__(self):
  return self.username  

이 외에 admin 의 user 란에 표기하고 싶은 게 있으면 admin.py 에 추가 

app 이름 대신 별명 넣기
원래는 Fcusers 였다.  
편한 이름으로 수정 : models.py 의 class Meta: 의 verbose_name
복수형지형(영어얘기) : 원래도 복수형이었다. verbose_name_plural  

10. 회원가입  
templates 폴더 만들기 
register.html 만들기  
bootstrap4.4 홈피가서 css, js, 메타태그 복사 

body 에서 폼만들기 (참고)
부트스트랩에서는 그리드 사용중 - 컨테이너 만들기 
부트스트랩 -> components -> Forms 

view 의 함수쓰기   
프로젝트의 urls.py 에 등록 (앱 사이의 이동은 여기서) *  
개별 앱(fcuser) 에 urls.py 따로 만들기
여기에는 view 안에 있는 함수 쓰기  
예: 
path('fcuser/', include('fcuser.urls'))
path('register/', views.register) 이렇게 연결됨  

11. 
register.html : form 만들기
action="." 현재 페이지에서 요청 
csrf_token : 크로스 도메인 막는다. 암호화된 정보, 키를 숨겨놓는다. 요청을 검증해줌. 키가 없으면 잘못된 요청으로 간주, 거절함. 다른 데서 호출할 수도 있는 문제점 방지. 장고에서는 
반드시 써야 함 

input 태그에 name 필드가 없다. 
네임값이 있어야 서버로 들어왔을 때 key 역할
name 필드 통해서 정보가 도착할 거다 (이 칸을 뭘로 정의할 것인가?)

fcuser 의 views.py 로 돌아감
주소로 입력하거나(GET) 등록버튼 눌러서(POST) 회원가입 페이지에 들어올 수 있음

12. 회원가입코드작성  
username = request.POST['username'] 이렇게 했음
딕셔너리에서 키를 가져온다. 키가 없으면 에러가 날 거임  
나중에 username = request.POST.get('username', None) 으로 함  
기본값 None 넣어준다. 

비밀번호 불일치 체크하기 
# if password != re_password:
#  return HttpResponse('비밀번호가 다릅니다') => 화면이 바뀌니 불편
한 화면에 비밀번호 불일치 뜨게 바꾸기 
views.py 에서 추가, html 에 글자공간 만들기 

비밀번호 암호화 : make_password

입력받은 값 다 넣었는지 확인
빈문자열이거나 값이 없으면 에러 

13. 퀴즈. 이메일 필드 추가하기 
models.py -> template -> views.py 

14. static 파일 관리하기 
https://docs.microsoft.com/ko-kr/azure/cdn/cdn-overview
cdn 서비스 :  css, java 같이 외부 파일을 직접 안가져오고 웹사이트 주소로 가져옴

외부 링크 말고 우리가 직접만든 css  넣을 때는 
fc_community 레벨에서 static 폴더 만들기 
여기서 css, js 넣고 관리 

settings.py 맨 아래에서 앱, 스태틱파일 등록(지금은 그대로 사용)

CSS 같은 static 파일에 접근했을 때, 그게 어느 폴더 있는건지 알려줘야 함  
BASE_DIR : fc_community 프로젝트 주소임 
# STATICFILES_DIRS = [ 
#     os.path.join(BASE_DIR, 'static'), 
# ]

bootstrap 4.3 themes free 검색 -> Bootswatch
slate -> bootstrap.min.css
이걸 스태틱 폴더 안으로 
register.html 에가서 다음 추가 
<link rel="stylesheet" href="/static/bootstrap.min.css"/>

15. 세션이란(쿠키)  


16. 로그인 (5분 부터)
템플릿 -> 뷰(템플릿과 뷰를 연결) -> fcuser 의 url
username 으로 모델 정보 찾아 오기 

<중간 정리> 
템플릿(화면) -> 모델 -> form -> views -> url 
admin.py: 관리자화면 바꾸기
settings.py: 앱 등록

17. 로그인 - 03. 로그인 만들기 - 2 (어려움)
views.py : 세션 처리(키에 value 넣기)

중요  
login 에서 home으로 리다이렉트 할 때 user 의 urls.py(하위계층) 이 아니라   
fc_community 의 urls.py(상위계층) 로 가야함   

from fcuser.views import home
path('/', home)

views.py : home 에 추가 

def home(request):
  user_id = request.session.get('user') 

  if user_id:
    fcuser = Fcuser.objects.get(pk=user_id) # pk 를 user_id 로 하겠다고 내가 지정하는 거임
    return HttpResponse(fcuser.username)

  return HttpResponse('Home!')

## 세션 내부 동작
브라우저 - 개발자 도구 -> application tab -> 왼쪽 쿠키 -> sessionid
처음 서버에 저장했을 때 session id(브라우저 혹은 클라이언트의 식별자) 받았다. 그리고 이걸 쿠키에 저장했다. 
매 요청마다 session id 가 같이 가게 됨 

127.0.0.1:8000/ 이면 요청을 안 했으니까 (위의 코드 기준으로  )
session id 없음 

정상적인 로그인 후 -> session id 뜬다. 

세션 아이디 별로 세션 공간이 존재한다. 

18. 로그인, 퀴즈 - 세션 복습 
로그아웃 후 홈으로 갈때는 fc_user 의 urls 에서 설정 
(fc_user 안에서 커버 할 수 있는 것만 하는 듯)
세션 이용하면 보안에 좋다. 클라이언트에는 세션 아이디 말고 다른게 없다. 자료는 다 서버에 있다. 
장고의 form 은 기존 form 태그를 제공하고 관리 해줌

세션은 클라이언트 별로 관리됨
지금 이 코드 실행한 클라이언트는 누구? 같은 자세한거 관리할 필요 없음

## 로그아웃    
views.py 해주고
fcuser 의 urls.py 로 가서 path('logout/', views.logout)
127.0.0.1:8000/fcuser/logout/ 으로 확인 

19. 상속 
base.html 이거러 상속받아서 login.html 만들기 

20. 로그인 - form 활용 
원래는 template 의 register.html 에서 <form> 사용
장고에서 이런 필드를 만들고 관리해 줌 

아래 삭제 

<div class="form-group">
                <label for="username">Username</label>
                <input type="text" class="form-control" id="username" placeholder="username" name="username">
            </div>
            <div class="form-group">
                <label for="password">Password</label>
                <input type="password" class="form-control" id="password" placeholder="password" name="password">
            </div> -->

(중요 : 모델은 데이터가 뭐 있는지 정의, 폼은 데이터를 표현하는 형식)

forms.py 만들기  
클래스 새로 만들고   

views.py 로 이동 
def login(request):
  form = LoginForm()
  return render(request, 'login.html', {'form': form})

login.html 로 이동
{{ form }} 으로 테스트 장고가 자동으로 생성해 준 태그들이어서
 클래스이런게 정확히 들어있지 않음
 에러처리 자동으로 추가됨 - 꼭 항목들 다 추가되야 한다고 
 마음에 안듬 - 예를 들면 비밀번호가 plaintext 임 

login.html 
{{ form.as_p }} : 하나의 필드를 하나의 p 로 감싸기
{{ form.as_table }} (잘 안씀)

반복문 으로 라벨지정
                    <label for="{{ field.id_for_label }}">{{ field.label }}</label>
                    <input type="{{ field.field.widget.input_type }}" class="form-control" id="{{ field.id_for_label }}" 
                        placeholder="{{ field.label }}" name="{{ field.name }}"/>

forms.py 로 가서 CharField 안에 자세한 거 집어 넣음


21. 로그인 - form 활용하기 2
value 검증과정 
그 전에 로그인 동작하게 만들기 

login.html에서 에러처리 추가 
다음 : form 안에 에러정보 있다. 에러 나면 form 안에 에러정보 들어감
지금까지의 유효성 검사(is_valid는) 값이 
있는지 없는지만 본다. 

추가 검증은 forms.py 의 def clean(self):
cleaned_data = super.clean() : 먼저 들어있던 데이터를 없애줌

super() 로 기존 data 안에 먼저 만들어져 있던 Clean 함수 호출 
만약에 값이 없었다면(값 입력을 안한 거라면) 여기서 실패 처리 되서 나갔을 거다. 

form 에서 이렇게 하면 views.py 가 깔끔해 진다. 

views.py 로 돌아가서 form 검증 부분 추가 


22. 게시판 만들기 - 1
board app 만들기 
templates 폴더와 안의 파일 만들기 
프로젝트의 urls.py 추가 
board.urls 추가 
views.py 함수 만들기

데이터 가져와서 보여주기 
models.py 
writer = models.ForeignKey('fcuser.Fcuser', on_delete=models.CASCADE)
on_delete 는 반드시 해야함 
writer 가 가리키고 있는 모델(fcuser) 가 삭제되면 writer
어떻게 함?  
CASCADE : writer 도 삭제 
기타 
SET_NULL : 
SET_DEFAULT : 

밑에도 수정 

board 의 views.py 로, board_list(request 만듦)

board_list.html 에서 {{ board }} 출력 

(settings 에서 앱 추가 + makemigrations + admin.py 에서 추가 )

어드민 에서 글쓰기 => 작성자는 foreign key, 누군가를 가리킴. 우리는 fc 모델(유저 네임)이 
나오게 됨 


board_list.html
{% for board in boards %}
아래에 값 채워 놓음 

- base.html 은 프로젝트 당 한 개만 
만들 수 있다. 

23. 게시판 만들기 - 2
board_write.html 만들기 
로그인에서 사용했던 폼 복사 

forms.py 만들기 
clean 으로 검증은 따로 안함. 기본적으로 있는 게 검증은 해줬으니까 
form.is_valid() 하는 것 같다.  
fcuser 의 forms.py 에서는 추가로 할게 있어서 했다. 

views.py 로 
board_write() 추가 
board 의 urls.py 에 추가 

board_write.html 에서 추가 
<textarea class="form-control" name="{{ field.name }}" placeholder="{{ field.label }}"></textarea>  
form-control 은 부트스트랩 부분임 

views.py 로 돌아가서  
board_write() 에서 유저 포함해서 정보 넘기는 거 추가 
writer 정보는 세션에 있다. 

POST 할 꺼면 받은 정보를 넘겨야 함  


board_detail.html 만듦
post 안할 거니 토큰, 반복문, form-group 삭제 
볼 수만 있게 함. 필요없는거 안쓴다. 

urls.py
path('detail/<int:pk>/', views.board_detail)

views.py 로 
위에 int 가 board_detail(request, pk) 로 
들어가게 됨. 주소로 부터 pk 입력받음 
int 라는 숫자는 pk 라는 변수명으로 받는다. 

board_detail.html
에서 board.title, board.contents 쓸 수 있다. 넘겨줬으니까 

24. 게시판 만들기 - 예외 처리 
없는 글 넣었다. 
로그인 안하고 글쓰려고 한다. 

fcuser -> forms.py 
board -> views.py 
board_detail()
board_write() : 유저 검사

25. 게시판 - 04. 게시판 만들기 - 4
paging / 
글을 여러 개 쓸 것 

board_list.html 하단 <이전-1/1-다음>
pagination justify-content-center


views.py 로 오기 
장고 : paginator 제공 


def board_list(request): 
    all_boards = Board.objects.all().order_by('-id') # - is a reverse order, -id means 'from newest post to older post'
    page = int(request.GET.get('p', 1))   
    # GET : get 형태로 받을 거임 
    # p : p 라는 값으로 받을 거임, 없으면 첫 번째 page 로 지정 
    page 번호 받기
    paginator = Paginator(all_boards, 2)      # 2: 한페이지에 2개 씩 나오게 함
    boards = paginator.get_page(page) 
    return render(request, 'board_list.html', {'boards':boards})

이렇게 하고 게시판 확인하면 
6(마지막으로 써놓은 글 번호)
5 
이렇게 보인다. 왜? 페이지 value 를 따로 넘기지 않았음. 
그러면 첫번째 페이지가 됐을 거고. 처음 두 개가 보이게 됨. 그래서 맨 위에 있는 두 가지 나왔음(??)

 
기존에는 boards 가 queryset 형태였는데 지금은 아님 

board_list.html 
하단의 페이지정보, 링크 추가

주소와 페이지 변하기 관찰  

왼쪽 페이지가 없는 상태에서 '이전으로' 누르면 주소에 ../# 뜸 

<a class="page-link disabled" href="#">이전으로</a> 이거 때문에 

'다음으로' 누르면 .../?p=2
  page = int(request.GET.get('p', 1))
  

왼쪽 가기 없을 때 disable 안되는 문제 
<a class="page-link disabled" href="#">이전으로</a>

부트 스트랩에 따르면 disabled 는 a 가 아니라 li 에 붙여야 함

validate_on_submit은 값이 들어왔는지만 본다. 
비밀번호를 검사해주는 건 없다. 

파이썬 original code 보기 
> python3.6 -m pip install -U autopep8

26. 보완
홈페이지에서 버튼들 
fcuser -> home.html
fcuser -> views.py 

from django.http import HttpResponse

return HttpResponse(fcuser.username)
return HttpResponse('Home!')

로그인을 하면 회원가입 버튼이 아니라 로그아웃 버튼이 보이게 
views.py 의 코드를 템플릿 안으로 옮길 수 있다. 
원래 

def home(request):
user_id = request.session.get('user')
<!-- # if user_id:
#  fcuser - Fcuser.objects.get(pk=user_id) -->

return render(request, 'home.html')

<수정 후>
home.html
<!-- {% if request.session.user %}
{% else %} -->

게시물 링크
board_list.html 글쓰기 버튼 
board_write.html 돌아가기 버튼
board_detail.html 돌아가기 버튼

한 개의 게시글을 보고 싶을 때 
board_list.html 

-------------- 모르겠는거 -----------------
찾아보기:
validators.py 처럼 파이썬 원래 코드 보는 방법? 

userid = form['userid'].data  
password = field.data  왜 둘이 다름? 

raise 할 때 어떻게 알게 된거임? (8분 12)
=> 이미 ValidationError 라는 클래스가 validators.py 에 있다. 그
그래서 ValueError 라고 함  

후반부 
<!-- {% if form.password.errors %} // errors 는 이 안에서 발생하는 모든 에러를 가지고 있다. 
validator 안에 여러개 넣을 수 있었다. 여러개의 validaotor 의 유효성 검사 다 통과하지 못했다면 에러들이 다 추가가 되는데 
우리는 에러를 하나만 관리한다. 
{% endif %}
{{ form.password.errors.0 }} 
// 하나라도 에러가 있으면 첫번째(0) 에러를 출력하겠다.  -->



27. 태그 - 01. 태그 만들기 - 1 - 
작성자 write 에서 ForeignKey : 1:N 관계 : 한 명이 여러 개 쓸 수 있으니까

MN모델링
Many to many => M:N 구조 
태그는 M:N => 장고는 편리하게 tag app 제공 + board 에 추가 

> python manage.py startapp tag 

tag -> models.py 
admin.py 

board -> models.py
tags = models.ManyToManyField('tag.Tag', verbose_name='tag')

settings.py 에서 앱추가 

migrate & migrations

admin 가서 확인 (태그를 만들고 개별 글에서 추가 가능 )

## 태그를 게시글에 연결하기 - 까다로움!
글에 있는 태그 보여주기 
{{ board.tags.all|join:", "}} join은 문자열 함수임 
문자열 사이 예를 들면 컴마 넣어줌 
다른 거 하면 앞에 대문자로도 만들 수 있음 

태그를 화면에 보여주기
board_detail.html 에서 {{ board.tags }}
model에 tags 를 써놔서 board_detail.html 에서도 tags 를 쓸 수 있음. 

board 앱의 모델에서 tag 써놨으니 board_details.html 템플릿에서 이용할 수 있다. 

보드랑 태그가 연결되어 있다. board.tags 는 클래스고 value는 없음
tag -> models.py 의 Tag 클래스에서 
field 가 엄청 많을 때 어떻게 보여줘야 할지 난감 

board.tags는 함수모음에 가깝다. 

{{ board.tags.all }} 
결과 : <QuerySet [<Tag: 태그1>, <Tag: 태그2>]>

{% for tag in board.tags.all %}
                    {{ tag.name }},
                {% endfor %}
결과 : 태그1, 태그2, 


마지막 컴마를 없애고 싶다. 
{{ board.tags.all|join:", " }}
join 은 문자열 함수인데 인자 value를 
컴마value 로 넣으면 리스트안에 있는 값 사이사이에 컴마를 넣어줌 

all 안에 있는 value 하나 하나 사이에 컴마를 넣어준다. (맨마지막에는 , 안들어간다. )

| 바 뒤에 넣고 싶은 거 넣을 수 있다. 

28. 태그 - 02. 태그 만들기 - 2 - 태그 생성 
board_write.html 
컴마로 구분해서 태그 넣으면 , 를 구분자로 하여 저장 

forms.py 
까다롭다 보드 생성하면 내부적으로 id 생긴다. 이 때 tag 추가 할 수 있음

tags.py -> forms.py 
이전에 form 을 이용해서 template 을 만들었기 때문에 이번에도 그렇게 

board -> views.py 
board_write()
태그가 원래 있는 태그면 가져오고 
없으면 넣어간다. 


가지고 오는 거는 Tag.objects.get(pk=pk)

생성은 이렇게 
for tag in tags: 
a = Tag(
  name=asdf
)
a.save()

어려움. 이해 안 됨
조건이 아니라 기본값을 넣고 싶을 때
태그에 이름과 작성자가 있을 때 이렇게 할 수도 있다. 

_tag, created = Tag.objects.get_or_create(name=tag, writer=writer)
name 이 tag 인 걸 가져온다. 없으면 만든다. 
name, writer 까지 있을 때는 name 은 있어도 writer 는 없으면 태그가 생긴다. 

_tag, created = Tag.objects.get_or_create(name=tag, defaults={'
wr'})
name 이 없어서 태그를 만들때 디폴트 값을 줄수 있다. (나중에 나옴)

_tag : 태그 클래스 변수
created : 태그가 새로 생긴건지. 기존에 있던 건지 표시 

created 를 _ 로 바꿈
_는 사용하지 않는 변수로 만들 때 씀

tag 를 board 에다 추가 하려면 보드가 이미 만들어져 있어야 한다. 
보드 먼저 만들고 tag 처리 

board 가 생성되서 저장되면 id 가 생성된다. (pk 로 사용했던거. 리스트로 정렬 할 때 id 사용)
id 값이 생성된 뒤에 사용할 수 있다. 

글쓰기 할 때 있는 태그와 없는 태그를 같이 써서 실험 
admin 에 가보면 없던 태그가 생성되어 있고, 내가 쓴 태그들에 표시가 되어 있다. 

29. 배포 - 01. 배포를 위한 Django 설정
settings.py 에서   
1. DEBUG = False     
2. ALLOWED_HOSTS = [  
  'alghost.pythonanywhere.com'
]  
pythonanywhere 가입한 아이디입력   
이 주소 이외로 접속하면 에러임     
'*' : 모든 주소로 다 받기는 비추  


3. STATICFILES_DIRS 은 주석처리  
장고가 기능 제공해 줌. CSS 파일 같은 STATIC 파일 모아서 프로젝트의 하나의 디렉토리(예: 'static')에 자동으로 모아줌, 모든 다음 우리는 배포 서비스 안에서 경로를 지정함 
STATIC_ROOT = os.path.join(BASE_DIR, 'static') 

4. pythonanywhere로 이동
Files -> upload files
프로젝트 압축. sqlite 넣을지는 옵션



30. pythonanywhere 에 배포하기
> open bash console here
> upzip fc_community.zip
> virtualenv 만들고 켜기 
> pip install django
> cd fc_community
> 스태틱 파일 수집 
> python manage.py collectstatic (스태틱 파일 모으기)
> python manage.py migrate 
> exit


> web -> manual configuration -> python3.7 -> 'code' 에서 소스코드의 경로 쓰기 예: /home/alghost/fc_community
> WSGI configuration file : 이 파일 보고 웹에서 실행 할 수 있도록 설정 
>> below~ 위에는 주석 처리
>> ++ Django ++ 부분을 해제 
> path 알맞게 수정
> os.environ['DJANGO_SETTINGS_MODULE'] = 'fc_community.settings'
> 저장, 뒤로 가기 
> 'virtualenv' 에서 경로 설정 : /home/alghost/fc_env
> 'static files' 에서 : /static/, /home/alghost/fc_community/static/ 순으로 입력 
> 주소로 접속하기 



# 04 Framework Django 실전
06. DRF - 01. 백엔드와 프론트엔드
단점: 결과가 다 페이지여서 답 할 때마다 페이지를 그리게 된다.
목표 : 프론트엔드와 벡앤드 분리 완전분리는 아님. 리액트 같은 건 안쓰고 제이쿼리 사용 

# 08 Flask 기초 
작은 프로젝트, 챗봇 용으로 

pip install Flask

set virtualenv 

Run
FLASK_APP=app.py flask run

View - Controller - Model(with DB)


## Flask-SQLAlchemy 
DB에서 데이터 가져올 때 SQL 씀 
Flask Alchemy 는 이부분 대신해 준다. 
sql alchemy 를 이용하면 db 를 편하게 다룰 수 있다. 

> pip install flask-sqlalchemy

sqlite: 하나의 파일을 지정해서 그 파일을 db로 쓴다. 
현재 폴더를 절대경로로 쓸 거다 

> SQLALCHEMY_COMMIT_ON_TEARDOWN
비즈니스 로직이 끝났을 때 반영하지 않은게 있으면 반영해라

TEARDOWN: 사용자가 정보 요청해서 원하는 답 해줬다. 이 상태가 TEARDOWM, 즉 사용자 요청의 끝 

끝날 떄 마다 COMMIT 하기 
일단 동작들을 쌓아 놓는다. 
Commit 하면 실제 DB 에 반영한다.

__ tablename__ = 'test_table'
으로 모델과 table 연결가능 

>python app.py
db.sqlite 가 만들어짐 

sql 내부를 볼 수 있는 프로그램 설치 안되어 있을 거다
> sqlite3 [name of your db]

# jinja
template 을 다루기 위한 라이브러리
Flask 에서 Jinja 이용하고 있다. 
우리가 직접 jinja 를 다루지는 않는다. 

> python3 -m pip install Pillow

Chapter 02. 기능 만들기, 회원가입 - 01. 모델 만들기, 회원
dependency 문제 주의

bootstrap 에서 제공하는 코드는 class 가 지정되어 있다. 
대신 form group 이랑 form control 지정해야 예쁜거 나옴 


Chapter 02. 기능 만들기, 회원가입 - 03. 컨트롤러 만들기, 회원

0:48
get 요청 하면 화면이 보인다 
post  요청 해서 등록 버튼 누르면 정보 가져올 수 있다.  

@app.route 에 있는 주소에 대해서 기본적으로  GET만 허용됨


## flask WTF
쓰는 이유 : 폼관리 
> pip install Flask-WTF

html 에 <form> 쓰지 않고
파이썬 코드로 form 에 해당하는 걸 만들면 
이걸 템플릿에 전달해서 쓴다. 

장점
1) validation
2) csrf 라는 보호기법 

forms.py 에서 form 만들고 
1) app.py에 돌아감 

csrf: 시크릿 키 가지고 암호화된 해쉬 값 만들어 낸다. 
이 해쉬 값 가지고 검증 한다. 

2) 템플릿 고친다. 
{{ form.userid.label("아이디 ") }} 이런 식으로 쓰면 
자체적으로 유효성 검사해 준다. 

3) 다시 app.py 로 돌아와서 고친다. 



Chapter 02. 기능 만들기, 회원가입 - 05. Flask-WTF을 활용한 Validation - 2
해쉬값 자동으로 전달하게 해줄려고 {{ form.csrf_token }} 적어줌 

validate_on_submit() : 그 값 유효성 검사도 해줌
이거 쓰면 POST/GET 검사, 값 가져오기, 값 있는지 검사 세개 안해도 됨 

WTF 쓰면 좋음점
코드가 의미단위로 분리됨

폼은 폼대로 
밸리데이션도 쉽게 가져다 쓸 수 있다. 
미리 만들어진 폼을 템플릿에서 가져다 쓸 수 있다. 

경로 바뀌면 
플라스크 설정 안에서 경로 변경하고
html 와서 또 변경해야 할 일 생긴다. 
이걸 안할려고 url_for 씀 

플라스크 기초 : 17 
분리안하면 나쁜점
응답 줄때마다 페이지 새로 그림 

요즘 추세: 백엔드와 프론트엔드 분리 
백엔드는 데이터만 보냄 

장고 실전: 20: restful API
백엔드와 프론트엔드가 데이터 주고받을 때의 protocol

REST, RESTful API(규약임)
https://docs.microsoft.com/ko-kr/azure/architecture/best-practices/api-design

REST API는 
리소스 중심으로 디자인 됨. 
 
(REST 안따라도 동작은 한다. 대신 Restful 하지 않다라고 함
왠만하면 지키는게 좋다.)

- URI 형태로 주소 나옴
- Json 형태로 리소스 반환
- 메서드: GET(가져오기), POST(생성 과 다른 기능), PUT(업데이트, 특히 전체대체), PATCH(부분대체), DELETE
- 리소스 중심으로 URI 구성하세요. 리소스 URI 는 컬렉션/항목/컬렉션  이정도의 depth 까지만 
- 주소는 명사형으로 ( create-order 는 동작도 있어서 비추)
- 동작은 http에서 지원하는 메서드로 지원하세요

플라스크 키초 24. ajax & jquery

지금 REST API 만들고 있다. 
api 활용하려면 ajax 사용해야 함 

## ajax : Asynchronous JavaScript And XML. 
비동기로 서버에 요청할 수 있다. 
기존에는 1) 주소 쓰거나 2) FORM 만들어 웹 서버에 요청
이러면 웹 페이지 매번 새로 그려야 함 
웹페이지 받지말고 

웹페이지는 이미 있는 상태에서 리소스 형태의 데이터를 받는다. 
이 데이터 가지고 화면 그린다. 백그라운드 작업함 

## jquery
ajax 를 편하게 쓸 수 있드록 도와주는 라이브러리 
순수 자바스크립트는 할게 많다. 하나의 엘리먼트 지정, 이벤트
jquery편하고 쉽게 작성 
장점: 셀렉터 쓸 수 있다. 내용 바꿔치기 가능 

# 05 장고 프로젝트 - 1 
02
주석 잘짜는 방법도 있다. 
PEP8 - style Guide for pyrhon code 
PEP 20 
PEP 3156(비동기 IO) 
/ flake 8(파이썬 파일의 스타일 검사)
> pip3 install flake8 

PRIMARY KEY 
DJANGO 에는 기본키로 id 가 디폴트로 지정되어 있다. 

07
왜 User 모델 확장해야 하나? 
모델 커스텀 위해서 
방법: 네 개 중 AbstractUser 쓸거다(내장유저 + 변형)

로그인 기능을 검증하기 위해서

1) superuser 를 만들거나 
2) 파이썬 shell 들어가서 import user, user objects, create 해서 유저 만든다. 
우리는 1) 한다. 

createsuperuser 를 굳 이 왜하는지 이해 안됨 


ERRORS:
auth.User.groups: (fields.E304) Reverse accessor for 'User.groups' clashes with reverse accessor for 'User.groups'.

프로젝트의 settings.py 에서 

해결 : AUTH_USER_MODEL = 'users.User'
[앱이름][클래스 이름] 추가 

쿠키: 서버 메모리에 저장안됨
세션: 서버 메모리에 저장됨 , 사용자 정보 노출 안됨 
세션은 클라이언트에 쿠키로 저장된다. 

1. 코드에 프로젝트 이름 넣지 말것 
2. 배포시 debug = false 로 (true 면 시크릿키, 코드 볼 수 있다.)


1. 추상클래스 만들기  class Meta:
2. 앱을 모듈화 하면 유지보수 쉽다. 
이미지 필드 사용하때는  필로우 설치해야 함 
사이트 들어가서 설치해도 됨 



## 댓글 모델링 (칼럼 - 필드)

내 생각 
댓글 번호 (PK)
유저 - 글쓴이번호 (relation)
내용  - textfield
최초 작성일 - date time field 
업데이트 날짜  - date time field 

모범답안
username = CharField(max_length=30, Null=False) // 유저이름 무조건 줘야 함 
email = CharField(max_length=50, Null=True)
content = TextField(max_length=200, Null=False)

class Comment(models.Model):
username = models.CharField(max_length=30, ...)
email  = models.CharField(max_length=59..)
content = models.TextField(max_length=200, ...)

- model relationship
many-to-one(댓글 : 글)
매니투매니는 인스타의 해쉬태그





# 06 장고 프로젝트 - 2
01. 기초
첫번째 프로젝트 먼저하고 이거 하는 거 추천
이유: 첫번째는 함수 만들고 두번째는 클래스 주로 만드는 데, 
함수 만들어 보고 나서 클래스 주로 만드는 게 낫다. 

크롬써라 

setting.py 에 장고관련 세팅 가능 

모델링은 팀장님이나 CTO 가 할 거임 . 신입이 할 수도 있다. 
필드, 타입 

장고에서는 아이디 따로 부여 안해도 pK 생김 

relation - pk 뭐임? 
파이썬 디버깅하려면 파이썬 익스텐선 설치해야 함 

# 07 장고 프로젝트 - 3
2020/02/20 

## pipenv 
쓰면 pip와 env 동시에 쓸 수 있다. 
가상환경 자동으로 만들어줌
파이썬 공식에서도 권장하고 싶음 (지금은 아님) 
requirement txt 등 프로젝트에 사용되는 라이브러리 자동으로 알아서 챙겨줌 

## homebrew 
맥은 기본으로 설치 할것 
윈도우 : https://brew.sh/index_ko 에서 복사에서 설치 
리눅스 : sudo apt install linuxbrew-wrapper 

> brew install pipenv 
(이거 설치 자체는 다른데서 해도 ok)
> 실행 : pipenv shell 이나 pipenv run
(강의에는 가상환경 안켜고 하다가 pylint 설치 후 가상환경 켜짐 - 나는 설치하고 바로 켬)

> pipenv install django 
(virtualenv 는 자동설치됨)

> django-admin startproject . 
. : (현재 폴더에 생성)

프로젝트 폴더 만들고
add workspace folder

setting.py 에서 랭귀지랑 시간대 바꿈

> python manage.py runserver
> admin 쓰려면 python manage.py migrate 
(마이그레잇 안했을 땐 어드민 로그인에 이상한거 누르면 에러 처리 안됨. 설치하니 에러처리는 해줌)

3대 db : oracle DB, MYSQL(무료), MS SQL 

mysql 설치(mac)
> brew update
> brew install mysql 
> brew list

윈도우 : https//dev.mysql.com/downloads/ (커뮤니티 서버)

> mysql_secure_installation (질문들 답함) - 6분 
no -> yes -> yes -> yes -> yes

서버 시작 
> mysql.server start

접속
> mysql -uroot -p
 
> cd test_db (DB 있는 데로 이동) 
> mysql -uroot -p < employees.sql
에러날거다 (sql 에서 113 줄에 ./ 추가 해야 함)
show databases; 로 확인 
> django-admin startapp fastadmin
settings.py 가서 INSTALLED_APPS += [] 로 추가 

## mysqlclient 
'패키지' 설치 (장고 공식문서에 있음) 
아래 세개는 선택 
> brew info openssl 
> export LDFLAGS="-L/usr/local/opt/openssl/lib"
> export CPPFLAGS="-I/usr/local/opt/openssl/include"
> pipenv install mysqlclient 

settings.py
DATABASES 에서 설정 바꾸기 

기존 : models.py 에 정의해서 db 고도화 

지금 : 외부 데이터를 장고에 넣어서 쓴다. 

<기존 디비를 장고로 마이그레이션 하기 >

> python manage.py inspectdb > fastadmin/models.py 
(이 파일에 데이터가 구조화 되서 보일거임)
> python manage.py makemigrations

(혹시 이거 해야 하는 거 아닌가? 
python manage.py makemigrations users
python manage.py migrate)


warning 무시해도 됨 

어드민에 클래스를 골라서 뿌려주는 작업
admin.py 바꾸기 (자료 참고) 
python manage.py runserver

관리자계정만들어야 함 
> python manage.py runserver createsuperuser

EMPLOYEES 가 보여야 함 
안보이면 시간차 두고 다시 들어오기 
