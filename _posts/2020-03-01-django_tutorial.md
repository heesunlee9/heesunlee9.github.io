---
title:  "Django Tutorials"
excerpt: "Django Tutorials"

categories:
  - Blog
tags:
  - Blog
last_modified_at: 2019-04-13T08:06:00-05:00
---

# 03 Framework Django 기초
> 가상환경 켜기(뭐든지 OK)
> pip install django
> django-admin startproject [name]
> python manage.py startapp [name]

앱만들고 나서 프로젝트의 settings.py 가서 앱 등록

모델 만들기 models.py 
함수들 쓴이유. 원래는 유저이름으로 로그임하는데 유리는 유저이름 자리에 이메일 넣는다. 그래서 써준다.  (혼란스러움)

_create_user : 이 클래스 내에서만 사용!
create_user :  밖에서 호출가능 

> python manage.py makemigrations users
> python manage.py migrate


- 모델 만들기 models.py 
함수들 쓴이유. 원래는 유저이름으로 로그임하는데 유리는 유저이름 자리에 이메일 넣는다. 그래서 써준다.  (혼란스러움)

_create_user : 이 클래스 내에서만 사용!
create_user :  밖에서 호출가능 

> python manage.py makemigrations users
> python manage.py migrate

문제 생기면 삭제 후 위에 다시 
> rm db.sqlite3  
abstract 써서 모델에 이력이 잘못 넘겨질 수 있다. 장고의 문제임

user 앱의 admin.py 가서 모델 등록

과제: 
1. BaseUserManager 원래 코드 보는 거 어떻게 하나? 함수 호출할때 뭐 채울지 알려면 봐야함  
autopep8 설치 

2. ** 뭐임? 
3. 매직 메소드 



10 
bootstrap4.4
1. 템플릿 만들기
2. view 의 함수쓰기 
3. 프로젝트의 urls.py 에 등록
4. 개별 앱에 urls.py 는 따로 만들어야. 여기에는 view 안에 있는 함수 쓰기 

템플릿에 있는 name 필드 
이게 서버에 갔을 때 key 역할
name 필드 통해서 정보가 도착할 거다 

12 회원가입
username = request.POST['username']
딕셔너리는 키 없으면 에러난다. 기본값 넣어준다. 

14 
cdn 서비스 :  css, java 같이 외부 파일을 직접 안가져오고 웹사이트 주소로 가져옴
외부 링크 말고 우리가 직접만든 css  넣을 때 => static 폴더 만들기 여기서 css, js 넣고 관리 
settings.py 에서 앱, 스태틱파일 등록

템플릿(화면) -> 모델 -> form -> views -> url 
admin: 관리자화면 바꾸기
setting: 앱 등록

회원가입 
“bootstrap 4.4 themes free”
커멘드 + 슬래쉬 : 주석

login 에서 home으로 리다이렉트 할 때 user 의 url 이 아니라 
fc_community 의 urls.py 로 가야함 주의! 


- 어렵다. 
forms.py 에서 클래스 새로 만들고
login.html 가서 에러메시지 출력하게 함 

세션은 클라이언트 별로 관리됨
지금 이 코드 실행한 클라이언트는 누구? 같은 자세한거 관리할 필요 없음

validate_on_submit은 값이 들어왔는지만 본다. 
비밀번호를 검사해주는 건 없다. 

파이썬 original code 보기 
> python3.6 -m pip install -U autopep8


-------------- 모르겠는거 -----------------
찾아보기:
validators.py 처럼 파이썬 원래 코드 보는 방법? 

userid = form['userid'].data
password = field.data  왜 둘이 다름? 

raise 할 때 어떻게 알게 된거임? (8분 12)
=> 이미 ValidationError 라는 클래스가 validators.py 에 있다. 그
그래서 ValueError 라고 함  

후반부 
{% if form.password.errors %} // errors 는 이 안에서 발생하는 모든 에러를 가지고 있다. 
validator 안에 여러개 넣을 수 있었다. 여러개의 validaotor 의 유효성 검사 다 통과하지 못했다면 에러들이 다 추가가 되는데 
우리는 에러를 하나만 관리한다. 
{% endif %}
{{ form.password.errors.0 }} // 하나라도 에러가 있으면 첫번째(0) 에러를 출력하겠다. 






17 
04. 로그인 - 03. 로그인 만들기 - 2
로그아웃 후 홈으로 갈때는 fc_user 의 urls 에서 설정 
(fc_user 안에서 커버 할 수 있는 것만 하는 듯)
세션 이용하면 보안에 좋다. 클라이언트에는 세션 아이디 말고 다른게 없다. 자료는 다 서버에 있다. 
장고의 form 은 기존 form 태그를 제공하고 관리 해줌

25
05. 게시판 - 04. 게시판 만들기 - 4
부트 스트랩에 따르면 disabled 는 a 가 아니라 li 에 붙여야 함

27
06. 태그 - 01. 태그 만들기 - 1 - MN모델링
Many to many => M:N 구조 
작성자 write 에서 ForeignKey : 1:N 관계 
태그는 M:N => 장고는 편리하게 tag app 제공


글에 있는 태그 보여주기 태그 등록하기 후반부 어렵다 
{{ board.tags.all|join:", "}} join은 문자열 함수임 
문자열 사이 예를 들면 컴마 넣어줌 
다른 거 하면 앞에 대문자로도 만들 수 있음 

board 앱의 모델에서 tag 써놨으니 details.html 템플릿에서 이용할 수 있다. 
보드랑 태그가 연결되어 있다. board.tags 는 클래스고 값은 없음 
board.tags.all 함수 불러야 함 (??)

28
06. 태그 - 02. 태그 만들기 - 2
33강도 까다롭다 보드 생성하면 내부적으로 id 생긴다. 이 때 tag 추가 할 수 있음

29 
07. 배포 - 01. 배포를 위한 Django 설정
settings.py 에서 1. debug 모드로 바꾸기 2. 얼라우드 호스트( '*' 는 별로임) 3. STATIC ROOT 장고가 기능 제공해 줌. CSS 파일 같은 STATIC 파일 모아서 프로젝트의 하나의 디렉토리('static')에 자동으로 모아줌, 우리는 배포 서비스 안에서 경로를 지정함 4. pythona~에서 압축할때 sqlite은 옵션

30 
여기는 다시 볼 필요 있다.(설정, 명령어 치기)

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
