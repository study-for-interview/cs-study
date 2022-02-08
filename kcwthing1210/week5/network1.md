# 🎁 REST, RESTFUL, REST API
# 📌 REST
## ✅ REST의 정의
- "REpresentational State Transfer"
- 자원을 이름(자원의 표현)으로 구분해 해당 자원의 상태(정보)를 주고 받는 모든 것
- 자원(resource)의 표현(representation)에 의한 상태 전달
    - 자원 : 해당 소프트웨어가 관리하는 모든 것 ( 문서, 그림, 데이터, 해당 소프트웨어 자체 등 )
    - 표현 : 그 자원을 표현하기 위한 이름 ( DB의 학생 정보가 자원이면, 'students'를 자원의 표현으로 정함 )
    - 상태 전달 : 데이터가 요청되는 시점에 자원의 상태를 전달한다. ( JSON 혹은 XML을 통해 데이터를 주고 받는 것이 일반적 )
- REST는 기본적으로 웹의 기존 기술과 HTTP 프로토콜을 그대로 활용하기 때문에, 웹의 장점을 최대한 활용할 수 있는 아키텍처 스타일
- REST는 네트워크 상에서 Client와 Server 사이의 통신 방식 중 하나

## ✅ REST 개념
- HTTP URI(Uniform Resource Identifier)를 통해 자원(Resource)을 명시하고, HTTP Method(POST, GET, PUT, DELETE)를 통해 해당 자원에 대한 CRUD Operation을 적용하는 것을 의미한다.
- 즉, REST는 자원 기반의 구조(ROA, Resource Oriented Architecture) 설계의 중심에 Resource가 있고 HTTP Method를 통해 Resource를 처리하도록 설계된 아키텍쳐를 의미한다.
- 웹 사이트의 이미지, 텍스트, DB 내용 등의 모든 자원에 고유한 ID인 HTTP URI를 부여한다.
- CRUD Operation
    - Create : 생성(POST)
    - Read : 조회(GET)
    - Update : 수정(PUT)
    - Delete : 삭제(DELETE)
    - HEAD: header 정보 조회(HEAD)

## ✅ REST의 장단점
### ✔ 장점
- HTTP 프로토콜의 인프라를 그대로 사용하므로 REST API 사용을 위한 별도의 인프라를 구출할 필요가 없다.
- HTTP 프로토콜의 표준을 최대한 활용하여 여러 추가적인 장점을 함께 가져갈 수 있게 해준다.
- HTTP 표준 프로토콜에 따르는 모든 플랫폼에서 사용이 가능하다.
- Hypermedia API의 기본을 충실히 지키면서 범용성을 보장한다.
- REST API 메시지가 의도하는 바를 명확하게 나타내므로 의도하는 바를 쉽게 파악할 수 있다.
- 여러가지 서비스 디자인에서 생길 수 있는 문제를 최소화한다.
- 서버와 클라이언트의 역할을 명확하게 분리한다.
### ✔ 단점
- 표준이 존재하지 않는다.
- 사용할 수 있는 메소드가 4가지 밖에 없다.
- HTTP Method 형태가 제한적이다.
- 브라우저를 통해 테스트할 일이 많은 서비스라면 쉽게 고칠 수 있는 URL보다 Header 값이 왠지 더 어렵게 느껴진다.
- 구형 브라우저가 아직 제대로 지원해주지 못하는 부분이 존재한다.
    - PUT, DELETE를 사용하지 못하는 점
    - pushState를 지원하지 않는 점

## ✅ REST의 구성 요소
### ✔ 자원(Resource) - URI

- 모든 자원에는 고유한 ID가 존재하고, 이 자원은 Server에 존재
- 자원을 구별하는 ID는 '/exgroups/:exgroup_id'와 같은 HTTP URI
- Client는 URI를 이용해 자원을 지정하고 해당 자원의 상태(정보)에 대한 조작을 Server에 요청
  ![](https://images.velog.io/images/kcwthing1210/post/3c4e0cdc-4cd8-4aed-9eb8-d8030bc764d5/image.png)
### ✔ 표현 ( Representation of Resource )

- Client와 Server가 데이터를 주고받는 형태로 JSON, XML, TEXT, RSS 등이 있다.
- JSON, XML을 통해 데이터를 주고 받는 것이 일반적



### ✔ 행위(Verb) - Method

HTTP 프로토콜의 Method를 사용합니다.
HTTP 프로토콜은 GET, POST, PUT, PATCH, DELETE의 Method를 제공합니다. ( CRUD )


## ✅ REST의 특징

### ✔ Server-Client (서버-클라이언트 구조)

- 자원이 있는 쪽이 Server, 자원을 요청하는 쪽이 Client가 됩니다.
- REST Server는 API를 제공하고 비즈니스 로직 처리 및 저장을 책임지고,
  Client는 사용자 인증이나 context( 세션, 로그인 정보 ) 등을 직접 관리하고 책임집니다.
- 역할을 확실히 구분시킴으로써 서로 간의 의존성을 줄입니다.

### ✔ Stateless (무상태)

- HTTP 프로토콜은 Stateless Protocol이므로 REST 역시 무상태성을 갖습니다.
- Client의 context를 Server에 저장하지 않습니다.
- 즉, 세션과 쿠키와 같은 context 정보를 신경쓰지 않아도 되므로 구현이 단순해집니다.
- Server는 각각의 요청을 완전히 별개의 것으로 인식하고 처리합니다.
- 각 API 서버는 Client의 요청만을 단순 처리합니다.
- 즉, 이전 요청이 다음 요청의 처리에 연관되어서는 안됩니다. ( DB에 의해 바뀌는 것은 허용 )
- Server의 처리 방식에 일관성을 부여하기 때문에 서비스의 자유도가 높아집니다.
### ✔ Cacheable (캐시 처리 기능)

- 웹 표준 HTTP 프로토콜을 그대로 사용하므로 웹에서 사용하는 기존의 인프라를 그대로 활용할 수 있습니다.
- 즉, HTTP가 가진 가장 강력한 특징 중 하나인 캐싱 기능을 적용할 수 있습니다.
- HTTP 프로토콜 표준에서 사용하는 Last-Modified Tag 또는 E-Tag를 이용해 캐싱을 구현합니다.
- 대량의 요청을 효율적으로 처리할 수 있습니다.
### ✔ Layered System (계층 구조)

- Client는 REST API Server만 호출합니다.
- REST Server는 다중 계층으로 구성될 수 있습니다.
- 보안, 로드 밸런싱, 암호화 등을 위한 계층을 추가하여 구조를 변경할 수 있습니다.
- Proxy, Gateway와 같은 네트워크 기반의 중간매체를 사용할 수 있습니다.
- 하지만 Client는 Server와 직접 통신하는지, 중간 서버와 통신하는지는 알 수 없습니다.
### ✔ Uniform Interface (인터페이스 일관성)

- URI로 지정한 Resource에 대한 요청을 통일되고, 한정적으로 수행하는 아키텍처 스타일을 의미합니다.
- HTTP 표준 프로토콜에 따르는 모든 플랫폼에서 사용이 가능며, Loosely Coupling(느슨한 결함) 형태를 갖습니다.
- 즉, 특정 언어나 기술에 종속되지 않음
### ✔ Self-Descriptiveness (자체 표현)

- 요청 메시지만 보고도 쉽게 이해할 수 있는 자체 표현 구조로 되어있습니다.


출처: https://dev-coco.tistory.com/97 [슬기로운 개발생활😃]


# 📌 REST API

## ✅ API( Application Programming Interface)란?
API는 응용 프로그램에서 사용할 수 있도록, 운영 체제나 프로그래밍 언어가 제공하는 기능을 제어할 수 있게 만든 인터페이스를 뜻합니다.
## ✅ REST API의 정의
REST의 특징을 기반으로 서비스 API를 구현한 것
최근 OpenAPI(누구나 사용할 수 있도록 공개된 API: 구글 맵, 공공 데이터 등), 마이크로 서비스(하나의 큰 어플리케이션을 여러 개의 작은 어플리케이션으로 쪼개어 변경과 조합이 가능하도록 만든 아키텍처) 등을 제공하는 기업 대부분은 REST API를 제공합니다.

## ✅ REST API의 특징
REST API의 가장 큰 특징은 각 요청이 어떤 동작이나 정보를 위한 것인지를 그 요청의 모습 자체로 추론이 가능한 것 입니다.

## ✅ REST API 디자인 가이드
첫 번째, URI는 정보의 자원을 표현해야 한다.
두 번째, 자원에 대한 행위는 HTTP Method(GET, POST, PUT, PATCH, DELETE)로 표현한다.
행위(Method)는 URI에 포함하지 않는다.

## ✅ REST API의 설계 규칙
- URI는 명사를 사용한다.(리소스명은 동사가 아닌 명사를 사용해야 한다.)
    - 아래와 같은 동사를 사용하지 말 것
        - /getAllUsers
        - /getUserById
        - /createNewUser
        - /updateUser
        - /deleteUser

- 슬래시( / )로 계층 관계를 표현한다.



-  URI 마지막 문자로 슬래시 ( / )를 포함하지 않는다.



-  밑줄( _ )을 사용하지 않고, 하이픈( - )을 사용한다.



-  URI는 소문자로만 구성한다.



-  HTTP 응답 상태 코드 사용
    - 1xx : 전송 프로토콜 수준의 정보 교환
    - 2xx : 클라어인트 요청이 성공적으로 수행됨
    - 3xx : 클라이언트는 요청을 완료하기 위해 추가적인 행동을 취해야 함
    - 4xx : 클라이언트의 잘못된 요청
    - 5xx : 서버쪽 오류로 인한 상태코드

- 클라이언트는 해당 요청에 대한 실패, 처리완료 또는 잘못된 요청 등에 대한 피드백을 받아야 한다.



-  파일확장자는 URI에 포함하지 않는다.

Ex) http://dev-coco.tistory.com/restapi/220/photo.jpg (X)

# 📌 RESTFUL
![](https://images.velog.io/images/kcwthing1210/post/484b923c-c239-411a-b5dd-cbc878f1d722/image.png)

## ✅ RESTful이란
- RESTful은 일반적으로 REST라는 아키텍처를 구현하는 웹 서비스를 나타내기 위해 사용되는 용어이다.
- ‘REST API’를 제공하는 웹 서비스를 ‘RESTful’하다고 할 수 있다.
- RESTful은 REST를 REST답게 쓰기 위한 방법으로, 누군가가 공식적으로 발표한 것이 아니다.
- 즉, REST 원리를 따르는 시스템은 RESTful이란 용어로 지칭된다.
## ✅ RESTful의 목적
- 이해하기 쉽고 사용하기 쉬운 REST API를 만드는 것
- RESTful한 API를 구현하는 근본적인 목적이 성능 향상에 있는 것이 아니라 일관적인 컨벤션을 통한 API의 이해도 및 호환성을 높이는 것이 주 동기이니, 성능이 중요한 상황에서는 굳이 RESTful한 API를 구현할 필요는 없다.
## ✅ RESTful 하지 못한 경우
Ex1) CRUD 기능을 모두 POST로만 처리하는 API
Ex2) route에 resource, id 외의 정보가 들어가는 경우(/students/updateName)


# 🧩 REFERENCE
- https://gmlwjd9405.github.io/2018/09/21/rest-and-restful.html
- https://dev-coco.tistory.com/97 [슬기로운 개발생활😃]

# 🎁 Web Server VS WAS
# 📌 Web Server
## ✅ 정의

- 웹 브라우저 클라이언트로부터 HTTP 요청을 받아들이고 HTML 문서와 같은 웹 페이지를 반환
- 서버란 클리어은트(사용자)가 웹 브라우저에서 어떠한 페이지 요청을 하면 웹 서버에서 그 요청을 받아 정적콘텐츠(단순 HTML 문서,CSS, javascript, 이미지, 파일 등 즉시 응답가능한 컨텐츠 )를 제공하는 서버이다.
- 웹서버가 동적 컨텐츠 요청을 받으면 WAS 에게 해당 요청을 넘겨주고, SAS에서 처리한 결과를 클라이어트에게 전달해주는 역할도 한다.

## ✅ 사용자 요청 처리 과정

![](https://images.velog.io/images/kcwthing1210/post/8da9a5c9-2a85-4893-90e6-750603b222b3/image.png)

# 📌 WAS

## ✅ 정의
- 인터넷 상에서 HTTP 프로토콜을 통해 사용자 컴퓨터나 장치에 애플리케이션을 수행해주는 미들웨어로서, 주로 동적 서버 컨텐츠를 수행하는 것으로 웹 서버와 구별이 되며, 주로 데이터베이스 서버와 같이 수행
- 웹 서버와 웹 컨테이너가 합쳐진 형태
    - 웹 컨테이너 : 웹 서버가 보낸 JSP, PHP 등의 파일을 수행할 결과를 다시 웹 서버로 보내주는 역할을 한다.
- 웹 서버 단독으로 처리할 수 없는 데이터베이스의 조회나 다양한 로직 처리가 필요한 동적 컨텐츠를 제공
- 사용자의 다양한 요구에 맞춰 웹 서비스를 제공 할 수 있음
- JSP, Servlet구동환경을 제공해주기 때문에 웹 컨테이너 혹은 서블릿 컨테이너라고도 불린다.
- 대표적인 WAS 종류 : Tomcat

## ✅ 요청 처리 과정
![](https://images.velog.io/images/kcwthing1210/post/31a72b1a-622d-4c45-b11f-aabc6e7d17a4/image.png)

# 📌 Web Service Architecture
웹 어플리케이션은 요청 처리 방식에 따라 다양한 구조를 가질 수 있다.

- 클라이언트 -> Web Server -> DB
- 클라이언트 -> WAS -> DB
- 클라이언트 -> Web Server -> WAS -> DB

![](https://images.velog.io/images/kcwthing1210/post/e0ee06ab-f19b-45c7-91a9-3945fa4b57e3/image.png)

### ✔ 클라이언트 -> Web Server -> WAS -> DB 동작과정

1. Web Server는 웹 브라우저 클라이언트로부터 HTTP 요청을 받는다.
2. Web Server는 클라이언트 요청을 WAS에 보낸다.
3. WAS는 관련된 Servlet을 메모리에 올린다.
4. WAS는 web.xml을 참고하여 해당 Servlet에 대한 Thread를 생성한다. (Thread Pool이용)
5. HttpServletRequest와 HttpServletResponse객체를 생성하여 Servlet에 전달한다.
   5-1. Thread는 Servlet의 service()메서드를 호출한다.
   5-2. service() 메서드는 요청에 맞게 doGet() 또는 doPost() 메서드를 호출한다.
6. protected doGet(HttpServletRequest request, HttpServletResponse response)
7. doGet() 또는 doPost() 메서드는 인자에 맞게 생성된 적절한 동적 페이지를 Response객체에 담아 WAS에 전달한다.
8. WAS는 Response객체를 HttpResponse형태로 바꾸어 Web Server에 전달한다.
9. 생성된 Thread를 종료하고, HttpServletRequest와 HttpServletResponse객체를 제거한다.

# ❗ Q&A
#### Q. WAS만 써도 되나요?
A. WAS는 DB 조회 및 다양한 로직을 처리하는데 집중해야 한다. 따라서 단순한 정적 컨텐츠는 웹서버에게 맡기며 기능을 분리시켜 서버 부하를 방지한다. 만약 WAS가 정적 컨텐츠 요청까지 처리하면, 부하가 커지고 동적 컨텐츠 처리가 지연되면서 수행 속도가 느려지고 이로 인해 페이지 노출시간이 늘어나는 문제가 발생하여 효율성이 크게 떨어진다.
웹 서버를 WAS 앞에 두고 필요한 WAS들을 Wev Server에 플러그인 형태로 설정하면 더욱 효율적인 분산 처리가 가능하다.

#### Q. 근데 왜 Tomcat이 아닌 Apache Tomcat인가요?
A. 정적 컨텐츠를 처리하는 웹 서버에는 Apache가 있고, 동적 컨텐츠를 처리하는 WAS 서버는 Tomcat이 있는데 Tomcat은 Apache Tomcat이라는 이름으로 많이 사용되어 혼란스러울 것이다. 붙여서 쓰는 이유는 2008년 릴리즈된 Tomcat 5.5버전부터 정적 컨텐츠를 처리하는 기능이 추가 되었는데, 이 기능이 순수 Apache를 사용하는 것에 비해 성능적 차이가 전혀 없으며 Tomcat이 Apache의 기능을 포함하고 있기때문에 Apache Tomcat이라고 부르고 있다.

# 🧩 Reference
- https://codechasseur.tistory.com/25

# 🎁 COOKIE & SESSION
# 📌 COOKIE
## ✅ 배경
- 로그인을 통해 볼 수 있는 서비스. 장바구니 서비스. 등등 클라이언트가 정보를 유지하는 Stateful한 성격의 서비스가 점점 많아졌다.
  정보를 유지할 수 없는 Connectionless, Stateless의 성격을 가진 HTTP의 단점을 해결하기 위해 쿠키라는 개념이 도입되었다.

## ✅ 쿠키(Cookie)란?
- 웹 서버가 브라우저에게 지시하여 사용자의 로컬 컴퓨터에 파일 또는 메모리에 저장하는 작은 기록 정보 파일
- 파일에 담긴 정보는 인터넷 사용자가 같은 웹사이트를 방문할 때마다 읽히고 수시로 새로운 정보로 바뀔 수 있습니다.

ex ) 방문했던 사이트에 다시 방문 하였을 때 아이디와 비밀번호 자동 입력
ex ) 팝업창을 통해 "오늘 이 창을 다시 보지 않기" 체크

## ✅ 쿠키(Cookie) 구성요소
### ✔ Name
쿠키의 이름
### ✔ Value
쿠키의 저장된 값
### ✔ Expires
쿠키가 언제 삭제되는지 결정합니다.
ex) expires="Wdy, DD−Mon−YYYY HH:MM:SS GMT"
쿠키에 만료일이 포함되어 있으면 영구적 쿠키로 간주.
Max-Age를 통해 지정된 만료일이 되면 디스크에서 쿠키가 제거.
### ✔ Domain
쿠키가 사용되는 도메인을 지정.
ex) domain=nesoy.github.io
이 값이 현재 탐색 중인 도메인과 일치하지 않을 경우, “타사 쿠키”로 간주되며 브라우저에서 거부.
이렇게 하여 한 도메인에서 다른 도메인에 대한 쿠키를 사용하지 못하게 설정.
### ✔ Path
쿠키를 반환할 경로를 결정
### ✔ ex) path=/
도메인의 루트 경로로 이동할 경우 쿠키가 전송
### ✔ Secure
보안 연결 설정
### ✔ HttpOnly
Http외에 다른 통신 사용 가능 설정.

## ✅ 쿠키(Cookie) 종류

![](https://images.velog.io/images/kcwthing1210/post/1395a084-6a5d-4e0f-bf17-cbbabd0fb421/image.png)

## ✅ Cookie의 동작 순서
1. 클라이언트가 페이지를 요청한다. (사용자가 웹사이트 접근)
2. 웹 서버는 쿠키를 생성한다.
3. 생성한 쿠키에 정보를 담아 HTTP 화면을 돌려줄 때,
   같이 클라이언트에게 돌려준다.
4. 넘겨 받은 쿠키는 클라이언트가 가지고 있다가(로컬 PC에 저장)
5. 다시 서버에 요청할 때 요청과 함께 쿠키를 전송한다.
6. 동일 사이트 재방문시 클라이언트의 PC에 해당 쿠키가 있는 경우,
   요청 페이지와 함께 쿠키를 전송한다.



## ✅ 쿠키(Cookie) 단점
- 쿠키에 대한 정보를 매 헤더(Http Header)에 추가하여 보내기 때문에 상당한 트랙픽을 발생시킵니다.
- 결제정보등을 쿠키에 저장하였을때 쿠키가 유출되면 보안에 대한 문제점도 발생할 수 있습니다.

# 📌 SESSION
![](https://images.velog.io/images/kcwthing1210/post/736ce2aa-10c0-4fa5-93b2-1569cc874909/image.png)

## ✅ 배경
- 쿠키의 트래픽 문제와 쿠키를 변경하는 보안적 이슈를 해결하기 위해 등장하였습니다.
## ✅ 세션(HTTP Session)이란?
- HTTP Session id를 식별자로 구별하여 데이터를 사용자의 브라우저에 쿠키형태가 아닌 접속한 서버 DB에 정보를 저장 합니다.
- 클라이언트는 HTTP Session id를 쿠키로 메모리 저장된 형태로 가지고 있습니다.
- 메모리에 저장하기 때문에 브라우저가 종료되면 사라지게 됩니다.
## ✅ 세션(HTTP Session) 절차
1. 클라이언트가 서버에 Resource를 요청합니다.
2. 서버에서는 HTTP Request를 통해 쿠키에서 Session id를 확인을 한 후에 없으면 Set-Cookie를 통해 새로 발행한 Session-id 보냅니다.
3. 클라이언트는 HTTP Request 헤더에 Session id를 포함하여 원하는 Resource를 요청을 합니다.
4. 서버는 Session id를 통해 해당 세션을 찾아 클라이언트 상태 정보를 유지하며 적절한 응답을 합니다.

# 📌 쿠키와 세션의 차이
### ✔ 저장 위치
쿠키는 클라이언트(브라우저)에 메모리 또는 파일에 저장하고, 세션은 서버 메모리에 저장된다.
### ✔ 보안
쿠키는 클라이언트 로컬(local)에 저장되기도 하고 특히 파일로 저장되는 경우 탈취, 변조될 위험이 있고, Request/Response에서 스나이핑 당할 위험이 있어 보안이 비교적 취약하다. 반대로 Session은 클라이언트 정보 자체는 서버에 저장되어 있으므로 비교적 안전하다.
### ✔ 라이프 사이클
쿠키는 앞서 설명한 지속 쿠키의 경우에 브라우저를 종료하더라도 저장되어 있을 수 있는 반면에 세션은 서버에서 만료시간/날짜를 정해서 지워버릴 수 있기도 하고 세션 쿠키에 세션 아이디를 정한 경우, 브라우저 종료시 세션아이디가 날아갈 수 있다.
### ✔ 속도
쿠키에 정보가 있기 때문에 쿠키에 정보가 있기 때문에 서버에 요청시 헤더를 바로 참조하면 되므로 속도에서 유리하지만, 세션은 제공받은 세션아이디(Key)를 이용해서 서버에서 다시 데이터를 참조해야하므로 속도가 비교적 느릴 수 있다.

# ❗ Q&A
#### Q. 세션을 쓰면되는데 굳이 쿠키를 사용하는 이유?

A. 세션이 쿠키에 비해 보안도 높은 편이나 쿠키를 사용하는 이유는
세션은 서버에 저장되고, 서버자원을 사용하기 때문에 사용자가 많을 경우 소모되는 자원이 상당하다.
이러한 자원관리 차원에서 쿠키와 세션을 적절한 요소 및 기능에 병행 사용하여,
서버 자원의 낭비를 방지하며 웹사이트의 속도를 높일 수 있다.



# 🧩 Reference
- https://nesoy.github.io/articles/2017-03/Session-Cookie
  -https://jeong-pro.tistory.com/80 [기본기를 쌓는 정아마추어 코딩블로그]
- https://hahahoho5915.tistory.com/32 [넌 잘하고 있어]

