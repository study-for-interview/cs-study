## REST, RESTful, REST API ?

#### REST 란
> Representational State Transfer
~~~
간단하게 설명하자면, REST는 URI를 통해 자원을 명시하고
HTTP Method(POST, GET, PUT, DELETE)를 통해 해당 자원에 대한 CRUD Operation을 적용하는 것을 의미한다.
~~~
* 클라이언트와 서버의 통신 방식
* URI와 HTTP를 이용한, 통신 목적의 **아키텍처 스타일**(유형)
* 아키텍처 제작시 사용되는 가이드 정도의 의미로 사용되며 명확히 준수해야할 표준은 없다.

<br>

#### REST의 특징 (6가지 조건)
1. 일관된 인터페이스(Uniform interface)
    * URI 사용, HTTP 메소드 사용, RPC미호출 등의 **지정된 인터페이스**를 준수한다.

2. 클라이언트/서버 구조
    * 클라이언트는 서버에 요청 메시지를 전송하고
    * 서버는 요청에 대한 응답 메시지를 전송한다.

3. 무상태(stateless) - `Cookie&Session파일 참고`
    * 세션등 이전 상황(문맥) 없이도 통신할 수 있다.

4. 캐시가능(Cacheable)
    * 서버의 응답 메시지는 캐싱될 수 있다.

5. 계층화된 시스템(Layered system)
    * 계층별로 기능이 분리된다.
    * Client는 REST API Server만 호출한다.
    * 따라서 중간 계층의 기능(로드밸런싱, 서버증설, 인증 시스템 도입 등)이 변경되어도 통신에 영향이 없다.

6. 주문형 코드(code on demand)
    * 반드시 충족할 필요는 없는 조건이다.
    * 손쉬운 데이터 처리를 위해 서버는 클라이언트에서 실행될 스크립트를 전송할 수 있다.


<br>

#### Rest API
* REST 기반으로 서비스 API를 구현한것

<br>

#### RESTful
* REST를 따르는 시스템을 RESTful하다 라고 함
* REST API를 제공하는 웹 서비스를 RESTful하다고 할 수 있다.