# REST란

REST는 Representational State Transfer라는 용어의 약자로서 2000년도에 로이 필딩 (Roy Fielding)의 박사학위 논문에서 최초로 소개되었습니다.

 로이 필딩은 HTTP의 주요 저자 중 한 사람으로 그 당시 웹(HTTP) 설계의 우수성에 비해 제대로 사용되어지지 못하는 모습에 안타까워하며 **웹의 장점을 최대한 활용할 수 있는 아키텍처로써 REST를** 발표했다고 합니다.

즉, **자원(Resource)의 표현(Representation)에 의한 상태 전달**

    a. 자원(Resource)의 표현(representation)

    자원 : 해당 소프트웨어가 관리하는 모든 것. EX) 문서 , 그림 , 데이터, 해당  소프트웨어 자체 등

    자원의 표현 : 그 자원을 표현하기 위한 이름 Ex) DB의 학생 정보가 자원일 때, 'Student'를 자원의 표현으로 정한다. 

    b. 상태(정보) 전달

    데이터가 요청되어지는 시점에서 자원의 상태(정보)를 전달한다.


월드 와이트 웹(WWW)괴 같은 분산 하이퍼미디어 시스템을 위한 소프트웨어 개발 아키텍처의 한 형식
- REST는 기본적으로 웹의 기존 기술과 HTTP 프로토콜을 그대로 활용하기 때문에 웹의 장점을 최대한 활용할 수 있는 아키텍처 스타일이다.
- REST는 네트워크 상에서 Client와 Server 사이의 통신 방식 중 하나이다.

Rest의 구체적인 개념
**HTTP URI(Uniform Resource Identifier)를 통해 자원(Resource)를 명시하고, HTTP Method를 통해 해당 자원에 대한 CRUD Operation을 적용하는 것을 의미**한다.

- Rest는 자원 기반의 구조(ROA, Resource Oriented Architecture) 설계의 중심에 Resource가 있고 HTTP Method를 통해 Resource를 처리하도록 설계된 아키텍쳐를 의미한다.
- 웹 사이트의 이미지, 텍스트, DB 내용 등의 모든 자원에 고유한 ID인 HTTP URI를 부여한다.
- CRUD Operation
    - Create : 생성(Post)
    - Read : 조회(Get)
    - Update : 수정(Put)
    - Delete : 삭제(Delete)
    - Head : Header 정보 조회(HEAD)


## REST의 장단점
- 장점
    - Http 프로토콜의 인프라를 그대로 사용하므로 REST API 사용을 위한 별도의 인프라 구축을 할 필요가 없다.
    - Http 프로토콜의 표준을 최대한 활용하여 여러 추가적인 장점을 함께 가져갈 수 있게 해준다.
    - Http 표준 프로토콜에 따르는 모든 플랫폼에서 사용이 가능하다.
    - Hypermedia API의 기본을 충실히 지키면서 범용성을 보장한다.
    - Rest API 메시지가 의도하는 바를 명확하게 나타내므로 의도하는 바를 쉽게 파악할 수 있다.
    - 여러가지 서비스 디자인에서 생길 수 있는 문제를 최소화한다.
    - 서버와 클라이언트 역할을 명확하게 분리한다.
- 단점
    - 표준이 존재하지 않는다.
    - Http Method 형태가 제한적이다.
        - 예를 들어, 메일을 보내는 기능을 작성한다고 합시다. 단순히 보내는 기능 외에도 누구한테, 얼마나 많이, 시간을 예약해서 등 다양한 세부 기능들 또한 작성해야하는데, 이러한 여러 기능들을 구현하는데 제약이 발생할 수 있습니다.
    
## REST가 필요한 이유
    
- 애플리케이션 분리 및 통합
- 다양한 클라이언트의 등장
- 최근의 서버 프로그램은 다양한 브라우저와 안드로이드 폰 , 아이폰과 같은 모바일에서도 통신을 할 수 있어야한다.
- 이러한 멀티 플랫폼에 대한 지원을 위해 서비스 자원에 대한 아키텍처를 세우고 이용하는 방법을 모색한 결과, REST에 관심을 가지게 됨


## REST 구성요소
1. 자원(Resource) : URI
    - 모든 자원에 고유한 ID가 존재하고, 이 자원은 Server에 존재한다.
    - 자원을 구별하는 ID는 "/groups/:group_id" 와 같은 HTTP URI 다.
    - Client는 URI를 이용해서 자원을 지정하고 해당 자원의 상태(정보)에 대한 조작을 Server에 요청한다.
2. 행위(Verb) : HTTP Method
    - HTTP 프로토콜의 Method를 사용한다.
    - HTTP 프로토콜은 GET,POST,PUT,DELETE 와 같은 메서드를 제공한다.
3. 표현(Representation of Resource)
    - Client가 자원의 상태(정보)에 대한 조작을 요청하면 Server는 이에 적절한 응답(Repersentation)을 보낸다.
    - REST에서 하나의 자원은 JSON, XML, TEXT, RSS 등 여러 형태의 Representation으로 나타내어 질 수 있다.
    - JSON 혹은 XML를 통해 데이터를 주고 받는 것이 일반적이다.

## REST 특징
1. Server-Client(서버 - 클라이언트 구조)
    - 자원이 있는 쪽이 Server, 자원을 요청하는 쪽이 Client가 된다.
        - REST Server : API를 제공하고 비즈니스 로직 처리 및 저장을 책임진다.
        - Client : 사용자 인증이나 context(세션, 로그인 정보) 등을 직접 관리하고 책임진다.
    - 서로 간 의존성이 줄어든다.

2. Stateless(무상태)
    - HTTP 프로토콜은 Stateless Protocol이므로 REST 역시 무상태성을 갖는다.
    - Client의 context를 Server에 저장하지 않는다.
        - 즉, 세션과 쿠키와 같은 context 정보를 신경쓰지 않아도 되므로 구현이 단순해진다.
    - Server는 각각의 요청을 완전히 별개의 것으로 인식하고 처리한다.
        - 각 API 서버는 Client의 요청만을 단순 처리한다.
        - 즉 , 이전 요청이 다음 요청의 처리에 연관되어서는 안된다.
        - 이전 요청이 DB를 수정하여 DB에 의해 바뀌는 것은 허용한다.
        - Server의 처리 방식에 일관성을 부여하고 부담이 줄어들며, 서비스의 자유도가 높아진다.

3. Cacheable(캐시 처리 가능)
    - 웹 표준 HTTP 프로토콜을 그대로 사용하므로 웹에서 사용하는 기존의 인프라를 그대로 활용할 수 있다.
        - HTTP가 가진 가장 강력한 특징 중 하나인 캐싱 기능을 적용할 수 있다.
        - HTTP 프로토콜 표준에서 사용하는 Last-Modified 태그나 E-Tag를 이용하면 캐싱 구현이 가능하다.
    - 대량의 요청을 효율적으로 처리하기 위해 캐시가 요구된다.
    - 캐시 사용을 통해 응답시간이 빨라지고 REST Server 트랜잭션이 발생하지 않기 떄문에 전체 응답시간, 성능, 서버의 자원 이용률을 향상 시킬 수 있다.

4. Layered System(계층화)
    - Client는 REST API Server만 호출한다.
    - REST Server는 다중 계층으로 구성 될 수 있다.
        - API Server는 순수 비즈니스 로직을 수행하고 그 앞단에 보안, 로드밸런싱, 암호화, 사용자 인증 등을 추가하여 구조상의 유연성을 줄 수 있다.
        - 또한 로드밸런싱 , 공유 캐시 등을 통해 확장성과 보안성을 향상 시킬 수 있다.
    - PROXY, 게이트웨이 같은 네트워크 기반의 중간 매체를 사용할 수 있다.
    
5. Code-On-Demand(optional)
    - Server로부터 스크립트를 받아서 Client에서 실행한다.
    - 반드시 충족할 필요는 없다.

6. Uniform Interface(인터페이스 일관성)
    - URI로 지정한 Resource에 대한 조작을 통일되고 한정적인 인터페이스로 수행한다.
    - HTTP 표준 프로토콜에 따르는 모든 플랫폼에서 사용이 가능하다.
        - 특정 언어나 기술에 종속되지 않는다.


## REST API의 개념

### REST API란

- API(Application Programming Interface)란
    - 데이터와 기능의 집합을 제공하여 컴퓨터 프로그램간 상호작용을 촉진하며, 서로 정보를 교환 가능 하도록 하는 것
- REST API의 정의
    - REST 기반으로 서비스 API를 구현한 것
    - 최근 Open API(누구나 사용할 수 있도록 공개된 API : 구글 맵, 공공 데이터 등) , 마이크로 서비스(하나의 큰 애플리케이션을 여러 개의 작은 애플리케이션으로 쪼개어 변경과 조합이 가능하도록 만든 아키텍처) 등을 제공하는 업체 대부분은 REST API를 제공한다.

### REST API의 특징
    - 사내 시스템들도 REST 기반으로 시스템을 분산해 확장성과 재사용성을 높여 유지보수 및 운용을 편리하게 할 수 있다.
    - REST는 HTTP 표준을 기반으로 구현하므로, HTTP를 지원하는 프로그램 언어로 클라이언트, 서버를 구현할 수 있다.
    - 즉, REST API를 제작하면 델파이 클라이언트 뿐 아니라, 자바, C#, 웹 등을 이용해 클라이언트를 제작할 수 있다.

### REST API 디자인 가이드

- REST API 설계 시 가장 중요한 항목은 다음의 2가지로 요약할 수 있습니다.

        첫 번째, URI는 정보의 자원을 표현해야 한다.
        두 번째, 자원에 대한 행위는 HTTP Method(GET, POST, PUT, DELETE)로 표현한다.


### REST API 중심 규칙

1. URI는 정보의 자원을 표현해야 한다. (리소스명은 동사보다는 명사를 사용)
        
        GET /members/delete/1

위와 같은 방식은 REST를 제대로 적용하지 않은 URI입니다. URI는 자원을 표현하는데 중점을 두어야 합니다. delete와 같은 행위에 대한 표현이 들어가서는 안됩니다.

2. 자원에 대한 행위는 HTTP Method(GET, POST, PUT, DELETE 등)로 표현

위의 잘못 된 URI를 HTTP Method를 통해 수정해 보면
        
        DELETE /members/1

으로 수정할 수 있겠습니다.
회원정보를 가져올 때는 GET, 회원 추가 시의 행위를 표현하고자 할 때는 POST METHOD를 사용하여 표현합니다.

회원정보를 가져오는 URI

    GET /members/show/1 (x)

    GET /members/1 (o)

회원을 추가할 때

    GET /members/insert/2 (x) - GET 메서드는 리소스 생성에 맞지 않습니다.

    POST /members/2 (o)


### URI 설계 시 주의할 점

1. 슬래시 구분자(/)는 계층 관계를 나타내는 데 사용
```
    http://restapi.example.com/houses/apartments
    http://restapi.example.com/animals/mammals/whales
```

2. URI 마지막 문자로 슬래시(/)를 포함하지 않는다.

URI에 포함되는 모든 글자는 리소스의 유일한 식별자로 사용되어야 하며 URI가 다르다는 것은 리소스가 다르다는 것이고, 역으로 리소스가 다르면 URI도 달라져야 합니다.

REST API는 분명한 URI를 만들어 통신을 해야 하기 때문에 혼동을 주지 않도록 URI 경로의 마지막에는 슬래시(/)를 사용하지 않습니다.

```
http://restapi.example.com/houses/apartments/ (X)
http://restapi.example.com/houses/apartments (0)
```


3. 하이픈(-)은 URI 가독성을 높이는데 사용

URI를 쉽게 읽고 해석하기 위해, 불가피하게 긴 URI경로를 사용하게 된다면 하이픈을 사용해 가독성을 높일 수 있습니다.

4. 밑줄(_)은 URI에 사용하지 않는다.

글꼴에 따라 다르긴 하지만 밑줄은 보기 어렵거나 밑줄 때문에 문자가 가려지기도 합니다. 이런 문제를 피하기 위해 밑줄 대신 하이픈(-)을 사용하는 것이 좋습니다.(가독성)



5. URI 경로에는 소문자가 적합하다.

URI 경로에 대문자 사용은 피하도록 해야 합니다.

 대소문자에 따라 다른 리소스로 인식하게 되기 때문입니다. RFC 3986(URI 문법 형식)은 URI 스키마와 호스트를 제외하고는 대소문자를 구별하도록 규정하기 때문이지요.

6) 파일 확장자는 URI에 포함시키지 않는다.

http://restapi.example.com/members/soccer/345/photo.jpg (X)

REST API에서는 메시지 바디 내용의 포맷을 나타내기 위한 파일 확장자를 URI 안에 포함시키지 않습니다. Accept header를 사용하도록 합니다.
```
GET / members/soccer/345/photo HTTP/1.1 Host: restapi.example.com Accept: image/jpg
```

## 리소스 간의 관계를 표현하는 방법

REST 리소스 간에는 연관 관계가 있을 수 있고, 이런 경우 다음과 같은 표현방법으로 사용합니다.
```
/리소스명/리소스 ID/관계가 있는 다른 리소스명

ex) GET : /users/{userid}/devices (일반적으로 소유 ‘has’의 관계를 표현할 때)
```

만약에 관계명이 복잡하다면 이를 서브 리소스에 명시적으로 표현하는 방법이 있습니다. 예를 들어 사용자가 ‘좋아하는’ 디바이스 목록을 표현해야 할 경우 다음과 같은 형태로 사용될 수 있습니다.

```
GET : /users/{userid}/likes/devices (관계명이 애매하거나 구체적 표현이 필요할 때)
```


## 자원을 표현하는 Colllection과 Document
Collection과 Document에 대해 알면 URI 설계가 한 층 더 쉬워집니다. DOCUMENT는 단순히 문서로 이해해도 되고, 한 객체라고 이해하셔도 될 것 같습니다. 

컬렉션은 문서들의 집합, 객체들의 집합이라고 생각하시면 이해하시는데 좀더 편하실 것 같습니다. 컬렉션과 도큐먼트는 모두 리소스라고 표현할 수 있으며 URI에 표현됩니다.

예를 살펴보도록 하겠습니다.
http:// restapi.example.com/sports/soccer

위 URI를 보시면 sports라는 컬렉션과 soccer라는 도큐먼트로 표현되고 있다고 생각하면 됩니다. 좀 더 예를 들어보자면

http:// restapi.example.com/sports/soccer/players/13

sports, players 컬렉션과 soccer, 13(13번인 선수)를 의미하는 도큐먼트로 URI가 이루어지게 됩니다. 

여기서 중요한 점은 컬렉션은 복수로 사용하고 있다는 점입니다. 좀 더 직관적인 REST API를 위해서는 컬렉션과 도큐먼트를 사용할 때 단수 복수도 지켜준다면 좀 더 이해하기 쉬운 URI를 설계할 수 있습니다.


## RESTful의 개념

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbcCEiL%2FbtqK7zXImuF%2FEDuc2kuFbDcW7XP45i52k0%2Fimg.png)

### RESTful이란

- RESTful은 일반적으로 REST라는 아키텍처를 구현하는 웹 서비스를 나타내기 위해 사용되는 용어이다.
    - 'REST API'를 제공하는 웹서비스를 'RESTful'하다고 할 수 있다.
    - RESTful은 REST를 REST답게 쓰기 위한 방법으로, 누군가 공식적으로 발표한 것이  아닌 REST원리를 따르는 시스템은 RESTful이란 용어로 지칭된다.

- RESTful의 목적
    - 이해하기 쉽고 사용하기 쉬운 REST API를 만드는 것
    - RESTful한 API를 구현하는 근본적인 목적이 성능 향상에 있는 것이 아니라 일관적인 컨벤션을 통한 API의 이해도 및 호환성을 높이는 것이 주 동기이니, 성능이 중요한 상황에서는 굳이 RESTful 한 API를 구현할 필요는 없다.

- RESTful 하지 못한 경우
    1. CRUD 기능을 모두 POST로만 처리하는 API
    2. route에 resource, id 외의 정보가 들어가는 경우(/Students/updateName)


참고

https://gmlwjd9405.github.io/2018/09/21/rest-and-restful.html

https://meetup.toast.com/posts/92





