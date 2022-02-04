# HTTP
HTTP는 (Hyper Text Transfer Protocol , 하이퍼 텍스트 전송방식)

HTTP란 웹서버와 클라이언트 간의 문서를 교환하기 위한 통신 규약입니다.

Transfer라는 해석 그대로 데이터를 전송하겠다라는 의미로 앞에 Hypertext 가 붙은 이유는 하이퍼텍스트 기반으로 데이터를 전송하겠다는. 간단히 말해서 링크기반으로 데이터에 접속하겠다는 의미.

World Wide Web(WWW)의 분산되어 있는 Server와 Client 간에 Hypertext를 이용한 정보교환이 가능하도록 하는 통신 규약이다.

HTTP는 웹에서만 사용하는 통신 규약으로 TCP/IP 기반으로 한 지점에서 다른 지점 (보통 클라이언트와 서버)으로 요청과 응답을 전송한다.

1989년 Tim Berners Lee가 처음 설계 하였다.

# HTTP 특징
- HTTP 메시지는 HTTP Server와 HTTP Client에 의해서 해석된다.
- TCP/IP 프로토콜의 Application 계층에 위치해 있다.
- TCP(Transmission Control Protocol, 전송 제어 프로토콜)을 이용한다 (Default Port 80)

# HTTP 동작
![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fd6bEXX%2FbtqKGkgnKFI%2FAAOXxGeB86KiRWz0xUesc1%2Fimg.png)

- HTTP는 서버/클라이언트 모델을 따른다. 클라이언트에서 요청(Request)를 보내면 서버는 처리해서 응답(Response)한다. 
- 클라이언트 : 서버에 요청하는 클라이언트 소프트웨어가 설치된 컴퓨터. chrom, firefox, ie등의 클라이언트 소프트웨어를 이용한다. 클라이언트는 URI를 이용해서 서버에 접속하고, 데이터를 요청할 수 있다.
- 서버 :  클라이언트의 요청을 받아서, 요청을 해석하고 응답을 하는 소프트웨어가 설치된 컴퓨터. Apache, nginx, IIS, lighttpd 등이 서버 소프트웨어다.

# HTTP status code
모든 HTTP 응답 코드는 5개의 클래스(분류)로 구분된다. 상태 코드의 첫 번째 숫자는 응답의 클래스를 정의한다. 마지막 두 자리는 클래스나 분류 역할을 하지 않는다. 첫자리에 대한 5가지 값들은 다음과 같다:

- 1xx (정보): 요청을 받았으며 프로세스를 계속한다
- 2xx (성공): 요청을 성공적으로 받았으며 인식했고 수용하였다
- 3xx (리다이렉션): 요청 완료를 위해 추가 작업 조치가 필요하다
- 4xx (클라이언트 오류): 요청의 문법이 잘못되었거나 요청을 처리할 수 없다
- 5xx (서버 오류): 서버가 명백히 유효한 요청에 대해 충족을 실패했다

## 1xx (조건부 응답)
요청을 받았으며 작업을 계속한다.[1]

이 상태의 상태 코드는 상태-라인과 선택적 헤더(컴퓨터에서 출력될 때 각 페이지 맨 윗부분에 자동으로 붙는 부분)만을 포함하는 임시의 응답을 나타내고 빈 라인에 의해서 종결된다. HTTP/1.0이래로 어떤 1XX 상태 코드들도 정의 되지 않았다. 서버들은 1XX 응답을 실험적인 상태를 제외하고 HTTP/1.0 클라이언트(서버에 연결된 컴퓨터)로 보내면 안 된다.

- 100(계속): 요청자는 요청을 계속해야 한다. 서버는 이 코드를 제공하여 요청의 첫 번째 부분을 받았으며 나머지를 기다리고 있음을 나타낸다.
- 101(프로토콜 전환): 요청자가 서버에 프로토콜 전환을 요청했으며 서버는 이를 승인하는 중이다.
- 102(처리, RFC 2518)

## 2xx (성공)
이 클래스의 상태 코드는 클라이언트가 요청한 동작을 수신하여 이해했고 승낙했으며 성공적으로 처리했음을 가리킨다.

- 200(성공): 서버가 요청을 제대로 처리했다는 뜻이다. 이는 주로 서버가 요청한 페이지를 제공했다는 의미로 쓰인다.
- 201(작성됨): 성공적으로 요청되었으며 서버가 새 리소스를 작성했다.
- 202(허용됨): 서버가 요청을 접수했지만 아직 처리하지 않았다.
- 203(신뢰할 수 없는 정보): 서버가 요청을 성공적으로 처리했지만 다른 소스에서 수신된 정보를 제공하고 있다.
- 204(콘텐츠 없음): 서버가 요청을 성공적으로 처리했지만 콘텐츠를 제공하지 않는다.
- 205(콘텐츠 재설정): 서버가 요청을 성공적으로 처리했지만 콘텐츠를 표시하지 않는다. 204 응답과 달리 이 응답은 요청자가 문서 보기를 재설정할 것을 요구한다(예: 새 입력을 위한 양식 비우기).
- 206(일부 콘텐츠): 서버가 GET 요청의 일부만 성공적으로 처리했다.
- 207(다중 상태, RFC 4918)
- 208(이미 보고됨, RFC 5842)
- 226 IM Used (RFC 3229)

## 3xx (리다이렉션 완료)
클라이언트는 요청을 마치기 위해 추가 동작을 취해야 한다.[1]

- 300(여러 선택항목): 서버가 요청에 따라 여러 조치를 선택할 수 있다. 서버가 사용자 에이전트에 따라 수행할 작업을 선택하거나, 요청자가 선택할 수 있는 작업 목록을 제공한다.
- 301(영구 이동): 요청한 페이지를 새 위치로 영구적으로 이동했다. GET 또는 HEAD 요청에 대한 응답으로 이 응답을 표시하면 요청자가 자동으로 새 위치로 전달된다.
- 302(임시 이동): 현재 서버가 다른 위치의 페이지로 요청에 응답하고 있지만 요청자는 향후 요청 시 원래 위치를 계속 사용해야 한다.
- 303(기타 위치 보기): 요청자가 다른 위치에 별도의 GET 요청을 하여 응답을 검색할 경우 서버는 이 코드를 표시한다. HEAD 요청 이외의 모든 요청을 다른 위치로 자동으로 전달한다.
- 304(수정되지 않음): 마지막 요청 이후 요청한 페이지는 수정되지 않았다. 서버가 이 응답을 표시하면 페이지의 콘텐츠를 표시하지 않는다. 요청자가 마지막으로 페이지를 요청한 후 페이지가 변경되지 않으면 이 응답(If-Modified-Since HTTP 헤더라고 함)을 표시하도록 서버를 구성해야 한다.
- 305(프록시 사용): 요청자는 프록시를 사용하여 요청한 페이지만 액세스할 수 있다. 서버가 이 응답을 표시하면 요청자가 사용할 프록시를 가리키는 것이기도 하다.
- 307(임시 리다이렉션): 현재 서버가 다른 위치의 페이지로 요청에 응답하고 있지만 요청자는 향후 요청 시 원래 위치를 계속 사용해야 한다.
- 308(영구 리다이렉션, RFC에서 실험적으로 승인됨)

## 4xx (요청 오류)
4xx 클래스의 상태 코드는 클라이언트에 오류가 있음을 나타낸다.

- 400(잘못된 요청): 서버가 요청의 구문을 인식하지 못했다.
- 401(권한 없음): 이 요청은 인증이 필요하다. 서버는 로그인이 필요한 페이지에 대해 이 요청을 제공할 수 있다. 상태 코드 이름이 권한 없음(Unauthorized)으로 되어 있지만 실제 뜻은 인증 안됨(Unauthenticated)에 더 가깝다.[2]
- 403(Forbidden, 금지됨): 서버가 요청을 거부하고 있다. 예를 들자면, 사용자가 리소스에 대한 필요 권한을 갖고 있지 않다. (401은 인증 실패, 403은 인가 실패라고 볼 수 있음)
- 404(Not Found, 찾을 수 없음): 서버가 요청한 페이지(Resource)를 찾을 수 없다. 예를 들어 서버에 존재하지 않는 페이지에 대한 요청이 있을 경우 서버는 이 코드를 제공한다.
- 405(허용되지 않는 메소드): 요청에 지정된 방법을 사용할 수 없다. 예를 들어 POST 방식으로 요청을 받는 서버에 GET 요청을 보내는 경우, 또는 읽기 전용 리소스에 PUT 요청을 보내는 경우에 이 코드를 제공한다.

## 5xx (서버 오류)
서버가 유효한 요청을 명백하게 수행하지 못했음을 나타낸다.[1]

- 500(내부 서버 오류): 서버에 오류가 발생하여 요청을 수행할 수 없다.
- 501(구현되지 않음): 서버에 요청을 수행할 수 있는 기능이 없다. 예를 들어 서버가 요청 메소드를 인식하지 못할 때 이 코드를 표시한다.
- 502 (Bad Gateway, 불량 게이트웨이): 서버가 게이트웨이나 프록시 역할을 하고 있거나 또는 업스트림 서버에서 잘못된 응답을 받았다.
- 503(서비스를 사용할 수 없음): 서버가 오버로드되었거나 유지관리를 위해 다운되었기 때문에 현재 서버를 사용할 수 없다. 이는 대개 일시적인 상태이다.
- 504(게이트웨이 시간초과): 서버가 게이트웨이나 프록시 역할을 하고 있거나 또는 업스트림 서버에서 제때 요청을 받지 못했다.

# HTTP METHOD
```
HTTP 요청 메서드
HTTP는 요청 메서드를 정의하여, 주어진 리소스에 수행하길 원하는 행동을 나타냅니다. 간혹 요청 메서드를 "HTTP 동사"라고 부르기도 합니다. 각각의 메서드는 서로 다른 의미를 구현하지만, 일부 기능은 메서드 집합 간에 서로 공유하기도 합니다. 이를테면 응답 메서드는 안전하거나, 캐시 가능 (en-US)하거나, 멱등성을 가질 수 있습니다.
```
## GET
- GET 메서드는 특정 리소스의 표시를 요청합니다. GET을 사용하는 요청은 오직 데이터를 받기만 합니다.
## HEAD
- HEAD 메서드는 GET 메서드의 요청과 동일한 응답을 요구하지만, 응답 본문을 포함하지 않습니다.
## POST
- POST 메서드는 특정 리소스에 엔티티를 제출할 때 쓰입니다. 이는 종종 서버의 상태의 변화나 부작용을 일으킵니다.
## PUT
- PUT 메서드는 목적 리소스 모든 현재 표시를 요청 payload로 바꿉니다.
## DELETE
- DELETE 메서드는 특정 리소스를 삭제합니다.
## CONNECT
- CONNECT 메서드는 목적 리소스로 식별되는 서버로의 터널을 맺습니다.
## OPTIONS
- OPTIONS 메서드는 목적 리소스의 통신을 설정하는 데 쓰입니다.
## TRACE (en-US)
- TRACE 메서드는 목적 리소스의 경로를 따라 메시지 loop-back 테스트를 합니다.
## PATCH
- PATCH 메서드는 리소스의 부분만을 수정하는 데 쓰입니다.

![image](https://user-images.githubusercontent.com/47075043/152278830-d33d7073-188a-4fb0-a2c8-bb978aea8cd3.png)


# HTTP와 HTTPS의 차이

## HTTP의 약점
HTTP는 주로 다음과 같은 약점을 가지고 있습니다.

- 평문(암호화 하지 않은) 통신이기 때문에 도청이 가능하다.
- 통신 상대를 확인하지 않기 때문에 위장이 가능하다.
- 완전성을 증명할 수 없기 때문에 변조가 가능하다.

이 약점은 다른 암호화 하지 않는 프로토콜에도 공통되는 문제입니다.

HTTPS는 Hypertext Transfer Protocol over Secure Socket Layer의 약자로 즉 SSL(Secure Socket Layer)을 이용한 Http 통신 방식을 의미합니다. 

SSL은 전자상거래에서의 데이터 보안을 위해서 개발한 통신 레이어다. SSL은 표현계층의 프로토콜로 응용 계층 아래에 있기 때문에, 어떤 응용 계층의 데이터라도 암호화해서 보낼 수 있다.

HTTP의 치명적인 단점. 보안

HTTP는 웹을 지탱하는 심플한 기술이지만 치명적인 단점이 있습니다. 브라우저와 웹서버가 통신함에 있어서 주고 받는 데이터가 암호화 되지 않고 생 날것 그대로 전송 되어진다는 점 입니다.

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FUqLgw%2FbtqLuDeP686%2FO7aq2MYIld7q9ZQLBjEL80%2Fimg.png)

웹서버와 브라우저가 통신하는 중간에 해커가 도청하게 된다면 날 것 그대로의 중요한 정보들을 탈취 할 수 있습니다.

만약 이러한 데이터가 로그인 기능에서 사용하는 아이디, 비밀번호와 같은 데이터라면 치명적일 수 있고 뿐만 아니라 정상적인 데이터를 중간에서 악의적으로 변조시킬 수도 있습니다.

HTTP는 기본적으로 평문 데이터 전송을 원칙으로 하기 때문에 개인의 프라이버시가 오가는 서비스들(전자상거래, 전자메일, 사내문서)에 사용하기 힘들다.

HTTPS는 SSL 레이어위에 HTTP를 통과 시키는 방식이다. 즉 평문의 HTTP 문서는 SSL 레이어를 통과하면서 암호화 돼서 목적지에 도착하고, 목적지에서는 SSL 레이어를 통과하면서 복호화 돼서 웹 브라우저에 전달된다.

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FDAZVM%2FbtqLve6XJeG%2FppMN3FyI26rz5wsHCk0WAk%2Fimg.png)

간혹 HTTPS를 하나의 프로토콜로 인식하기도 하는데, HTTP와 SSL은 전혀 다른 계층의 프로토콜콜의 조합이다. HTTPS over SSL로 보는게 좀더 정확한 시각이다. 거의 모든 웹 서버와 웹 브라우저와 HTTP 기반의 툴들 - wget, curl, ab 기타등등 - 이 SSL을 지원한다.


## SSL, 인증서, 인증기관(CA)

SSL(Secure Sockets Layer)은 암호화 통신과 그 암호화 통신에 사용되는 키를 공유할 수 있도록 하는 기술입니다. 이 때 등장하는것이 인증기관입니다. 인증기관은 CA(Certificate Authority)라고 하는데, 인증기관은 암호화시 사용되는 키를 담은 인증서를 발급하고 관리합니다.

웹 서버를 운영하는 웹사이트(네이버, 구글, 티스토리..)는 암호화키를 생성하여 자신이 하나는 보관하고 하나는 인증기관에게 넘겨 인증서를 발급 받습니다. 

인증기관은 인증서를 발급 및 관리해주는 대신 돈을 받습니다.
발급된 인증서는 인증기관 본인이 보관합니다. 

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FqYsuS%2FbtqLsbpmca6%2F4UviZpbNnXY9Ozkm1lhkd0%2Fimg.png)

## HTTPS 통신과정

HTTPS 통신 과정
인증기관에 인증서를 의뢰할 때 통신시 사용할 암호화 키와 자신의 웹사이트 주소를 넘겨주었고 이를 바탕으로 인증기관은 인증서를 만들어 보관했습니다.

여기서 한가지 알아야 할 사실이 있는데, 브라우저는 이미 인증기관 목록을 가지고 있습니다.
브라우저를 개발하는 기업에서 브라우저를 개발할 때 인증기관 목록을 넣어두기 때문입니다. 
즉 인터넷 익스플로러와 구글의 크롬 등에는 인증기관 목록이 담겨있는 것이지요.

따라서 브라우저는 웹서버와 통신하기 이전에 인증기관 리스트를 확인하여 인증기관에 현재 자신이 통신하려는 웹서버의 인증서가 있는지 확인하고 있으면 인증서를 받습니다.

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fse8OE%2FbtqLxvNpVSI%2FUB8g7CzO8fKPqwCl0lyh30%2Fimg.png)

인증서에는 웹서버가 인증서를 발급할때 첨부했던 암호화키가 들어있으므로 이것을 가지고 데이터를 암호화하여 웹서버와 통신합니다. 웹서버는 최초 인증서를 발급할 때 사용했던 자신의 암호화키로 복호화 하면 됩니다.

제 3자인 인증기관이 암호화 키를 인증서에 담아 관리하는 SSL을 이용하기 때문에 암호화 키를 분배하는 과정에서 탈취 당하지 않을 수 있으며, 분배된 암호화 키를 통해 암호화 통신을 할 수 있는 것입니다.

# HTTP1.0 과 HTTP1.1 차이
## HTTP 1.0
- HTTP는 원래 0.9v 부터 시작되었다고 하지만, 사실상 1.0버전이 상용화 되어 1996년부터 사용되기 시작했다.
- HTTP 1.0은 단순히 open/operation/close 방식을 취하고 있는 단순한 구조이다.
- TCP Connection당 하나의 URL만 fetch하며, 매번 request/response가 끝나면 연결이 끊기므로 필요할 때마다 다시 연결해야하는 단점이 있어 속도가 현저히 느리다.
- URL의 크기가 작고 한번에 가져올 수 있는 데이터의 양이 제한되어 있다.

## HTTP 1.0의 단점
- HTTP 1.0에서는 open/close를 위한 flow의 제한으로 대역폭이 적게 할당되어 연결되는데, 이로 인해 congestion information이 자주 발생하고 disconnect가 반복적으로 나타나게 된다.
- 반복되는 disconnect 현상으로 인해 한 서버에 계속해서 접속을 시도하게 되면 과부하가 걸리고 성능이 떨어지게 되는 문제가 발생한다.
- 이런 문제를 해결하기 위해 HTTP 1.1이 등장한 것이다.
 

## HTTP 1.1
- HTTP의 인터넷에서 impact를 줄이고 cache를 두어 인터넷 프로토콜 수행이 빠르게 될 수 있도록 성능을 향상하고 있다.
- multiple request에 대한 처리가 가능하고 request/response가 파이프라인 방식으로 진행이 가능하다.

![image](https://user-images.githubusercontent.com/40616436/79342851-9d439600-7f68-11ea-9a1c-80782d6cbb6e.png)

## Conection

## HTTP 1.0

- Http1.0 발표 이후 클라이언트와 서버간의 요청과 응답을 어떻게 하면 좀 더 빨리할 수 있을 지 연구가 이루어졌는데, 이 때, 대표적으로 만들어진 방법이 Persistent Connection(Keep-alive), Pipelining 기법이다.

- 위에서 살펴본 바와 같이 초창기(1.0)에는 요청 때마다 TCP 연결을 3-way handshake 방식으로 맺어야 했다.
    - syn, syn-ack, ack

- 만약, 5개의 오브젝트를 가진 하나의 웹 페이지가 있다면 클라이언트와 서버 사이에는 총 5번의 3-way handshake가 이루어진다. 즉, 5번의 연결을 끊었다가 연결하는 것이다.
    - 초반에는 해당 방법이 그리 큰 문제가 되지 않았지만, 웹 사이트의 콘텐츠가 늘어나면서(이미지와 같은) TCP 연결의 재사용이 필요하게 되었다. 이 때 나온 기술이 Psersistent Connection(Keep-alive)이다

![image](https://user-images.githubusercontent.com/40616436/79683535-bc427080-8265-11ea-84c5-a00e32a07a37.png)

- Psersistent Connection(Keep-alive)는 연결을 지속하며 클라이언트와 서버 통신이 이루어진다.
    - 이를 지원하는 클라이언트는 서버에게 HTTP 요청 시, 요청 Message내 헤더에 다음 헤더를 추가한다.
        - connection: keep-alive
    - 서버에서는 클라이언트의 요청을 받아 TCP 연결을 HTTP 응답 이후 끊지 않고 계속 사용하겠다라는 약속으로 동일한 헤더를 HTTP 응답에 포함한다.

- Persistent Connection을 사용하면 서버의 단일 시간 내의 TCP 연결의 수를 그만큼 적게 함으로써 CPU나 메모리 자원을 절약할 수 있고, 네트워크 혼잡을 줄일 수 있다.

## HTTP 1.1

- HTTP 1.1에서는 굳이 Connection 헤더를 사용하지 않아도, 모든 요청과 응답은 기본적으로 Persistent Connection을 지원하도록 되어 있어 필요 없을 경우에만(HTTP 응답 완료 후 TCP 연결을 끊어야하는 경우) Connection 헤더를 사용했다.

- HTTP 1.1에서는 클라이언트와 서버간의 요청과 응답 효율성을 개선하기 위해 HTTP Pipelining이 등장하였다.

![image](https://user-images.githubusercontent.com/40616436/79683817-8b633b00-8267-11ea-894c-e5a0ba367f8c.png)

- HTTP 1.0에서는 HTTP 요청들의 연결을 반복적으로 끊고 맺음으로서 서버 리소스 적으로 비용을 요구한다.

- HTTP 1.1에서는 다수의 HTTP Request들이 각각의 서버 소켓에 Write 된 후, Browser는 각 Request들에 대한 Response들을 순차적으로 기다리는 문제를 해결하기 위해 여러 요청들에 대한 응답 처리를 뒤로 미루는 방법을 사용한다.

- 즉, HTTP 1.1에서 클라이언트는 각 요청에 대한 응답을 기다리지 않고, 여러 개의 HTTP Request를 하나의 TCP/IP Packet으로 연속적으로 Packing해서 요청을 보낸다.

- Pipelining이 적용되면 하나의 Connection으로 다수의 Request와 Response를 처리할 수 있게끔 Network Latency를 줄일 수 있는 것이다.

# HTTP 1.1 vs HTTP 2.0 vs HTTP 3.0

HTTP 1.1 의 단점으로 HOL이 있다.

http/1.1의 connection 당 하나의 요청 처리를 개선하는 방법 중 파이프라이닝이 존재하고 connection을 통해 다수개의 파일을 요청/응답 받는 기법입니다.

![IMAGE](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbSb1v1%2FbtqSIZ8ZjMp%2FR4ifT6EIUyZAaDmGbLwMTK%2Fimg.png)
 
하지만 위 그림처럼 하나의 TCP 연결에서 3개의 이미지 (a.png, b.png, c.png)를 요청한 경우 첫 번째 이미지를 요청하고 응답이 지연되면 2, 3번째 이미지는 대기하게 되는데 이런 현상을 HTTP의 HOL(head of line blocking)이라고 부릅니다.

- RTT (round trip time) 증가
     - 하나의 connection에 하나의 요청을 처리하면서 매 요청별로 connection이 연결되기 때문에 TCP 상에서 동작하는 HTTP 특성상 3- way handshake가 반복적으로 일어나 불필요한 RTT 증가와 네트워크 지연을 일으켜 성능을 저하시킨다 
- 무거운 header 구조 (ex. 쿠키)
    - 헤더에 많은 메타 정보를 저장한다
    - 매 요청시마다 중복된 header값을 전송하게 되며 해당 domain에 설정된 cookie 정보도 매 요청시 마다 헤더에 포함되어 전송된다.
    - 전송하는 값보다 헤더 값이 더 큰 경우도 있다.

HTTP/1.1 단점 해결 방법

1. Image spriting 이미지 스프라이트 (여러 개의 이미지를 하나의 이미지로 합쳐서 관리하는 이미지)

    이미지 파일 요청 횟수를 줄이기 위해 여러 아이콘을 하나의 큰 이미지를 만든다음 css에서 해당 이미지 좌표값을 지정해 표시한다. 
ex) 이미지 하나를 가지고 여러 아이콘을 만드는 방법 (각도, 방향 조절)

2. Domain Sharing

    최신 브라우저들은 http/1.1 단점을 극복하기 위해 다수의 connection을 생성해서 병렬로 요청을 보내기도 한다. 
    브라우저 별로 domain 당 connection 개수 제한이 존재해서 근본 해결책은 아니다. 

3. Minify css/ javascript: 코드 축소시킴, 스크립트, 스타일 시트를 html문서 하단, 상단에 각각 위치시킴 

4. SPDY 등장 

    근본적으로 문제 해결 X

    구글은 Latency 관점에서 http고속화한 스피디라는새 프로토콜을 구현했다.
HTTP 통한 전송을 재정의하여 구현

# HTTP 2.0

- Multiplexed Streams
    - 한 커넥션으로 동시에 여러 개의 메세지 주고 받음. 응답 순서에 상관없이 stream으로 주고 받음
    - http/1.1의 connection keep-alive, pipelining 개선시킴 

- Stream Prioritization
    - 요청한 리소스간 우선 순위를 설정하여 의존성 있는 파일의 수신이 늦어지는 경우 브라우저 렌더링이 늦어지는 문제 해결 

- Server Push
    - 서버는 클라이언트가 요청하지 않은 리소스 보내줄 수 있음
    - http/1.1에서 클라이언트는 요청한 html문서 수신 후 해석하면서 필요한 리소스를 재 요청하는데, http/2에서는 server push  기법을 이용해서 요청하지 않은 리소스를 push하여 클라이언트의 추가적인 요청을 최소화하여 성능 향상을 시킨다
    - push_promise라고 부른다.

![IMAGE](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FxXlDL%2FbtqSEKq3TjD%2FANu4fKX4LOtv4l98PjZtJ1%2Fimg.png)


- header compression
    - header 정보를 압축하기 위해 header table과 huffman encoding 기법을 사용하는데 이를 hpack 압축방식이라 한다
    - 클라이언트가 여러 번 요청을 보낼 때 http/1.1은 헤더에 중복 값이 존재해도 그대로 중복 전송한다. http/2에서는 static/dynamic 테이블 개념을 이용해 중복 header를  검출하고 중복된 헤더는 index값만 전송하고 나머지는 huffman encoding으로 인코딩하여 전송한다.

## HTTP/2의 단점

하지만 HTTP2는 여전히 TCP를 이용하기 때문에 Handshake의 RTT(Round Trip Time)로인한 Latency(지연시간), TCP의 HOLB 문제는 해결 할 수 없다.

# HTTP/3.0 - with QUIC

앞서 보았듯이 2.0에서 http 의 HOL(head-of-line) 문제를 해결하였다.
하지만 TCP에 기반을 둔 headof line 블록킹 문제가 남아있었다.

![image](https://media.vlpt.us/images/seeker1207/post/26110caf-4403-441d-9873-0893c8f54f16/image.png)

2.0에서는 하나의 연결안에서 여러개의 스트림이 전송되는데 여기서 하나의 패킷이 빠지거나 없어지면 없어진 패킷을 다시 전송하고 목적지에 도달하는 동안 전체 TCP 연결이 중단되게 된다. 

TCP 자체가 신뢰성 이 보장된 프로토콜이기 때문에 이와 같은 문제가 발생하게 되었다.

그래서 TCP를 이용하는 한 이 이슈를 고치는 것은 쉽지 않다고 판단되었고 그래서 UDP를 이용하면서도 TCP의 혼잡제어나 신뢰성을 보장하는 장점을 살리는 방안을 고민하게 되었다.

![IMAGE](https://media.vlpt.us/images/ziyoonee/post/57c9fce5-b940-4729-849b-75521aa5d440/http3-1-1.png)

그래서 QUIC 프로토콜이 등장하게 되었다. UDP가 데이터 전송의 신뢰성을 보장하지 않지만 UDP위에 새로운 전송계층을 추가함으로써 TCP에 존재하는 패킷 재전송, 혼잡 제어, 속도 제어 등 여러 기능들을 제공한다.

또한 QUIC은 위에서 언급된 TCP의 HOL block 문제도 해결했다.

![image](https://media.vlpt.us/images/seeker1207/post/d8c54946-9202-42ca-a39f-06c4c78f51ed/image.png)

이렇게 각 스트림을 스트림 식별자로 식별하면서 독립적인 스트림을 갖게
하면 스트림 중 하나에서 어떤 패킷이 손실되더라도 해당 스트림만 멈추게 된다.

또한 QUIC는 0-RTT, 1-RTT 핸드쉐이크를 둘다 제공 하기 때문에 기존의 3-way handshake로 발생되는 시간을 줄여준다.

- RTT 감소로인한 지연시간 단축
QUIC은 TCP를 사용하지 않기 때문에 통신을 시작할 때 번거로운 3 Way Handshake 과정을 거치지 않아도 된다. 
- 클라이언트가 보낸 요청을 서버가 처리한 후 다시 클라이언트로 응답해주는 사이클을 RTT(Round Trip Time)이라고 하는데, TCP는 연결을 생성하기 위해 기본적으로 1 RTT가 필요하고, 여기에 TLS를 사용한 암호화까지 하려고 한다면 TLS의 자체 핸드쉐이크까지 더해져 총 3 RTT가 필요하다.

![image](https://evan-moon.github.io/95f5c7e411d0b7f96d182abe284be551/gcp-cloud-cdn-performance.gif)

반면 QUIC은 첫 연결 설정에 1 RTT만 소요된다. 그 이유는 **연결 설정에 필요한 정보와 함께 데이터도 보내버리기 때문**이다. 클라이언트가 서버에 어떤 신호를 한번 주고, 서버도 거기에 응답하기만 하면 바로 본 통신을 시작할 수 있다는 것이다.

단, 클라이언트가 서버로 첫 요청을 보낼 때는 서버의 세션 키를 모르는 상태이기 때문에 목적지인 서버의 Connection ID를 사용하여 생성한 특별한 키인 초기화 키(Initial Key)를 사용하여 통신을 암호화 한다.

그리고 한번 연결에 성공했다면 서버는 그 설정을 캐싱해놓고 있다가, 다음 연결 때는 캐싱해놓은 설정을 사용하여 바로 연결을 성립시키기 때문에 0 RTT만으로 바로 통신을 시작할 수도 있다. 이런 점들 때문에 QUIC은 기존의 TCP+TLS 방식에 비해 지연시간을 더 줄일 수 있었던 것이다.

TCP Fast Open + TLS 1.3 으로 구현이 되긴하지만 주고 받는 데이터가 큰 경우 QUIC가 유리하다.


![image](https://media.vlpt.us/images/seeker1207/post/995a49b5-68f9-4faf-b9b8-b5d8a8b1906c/image.png)

![image](https://media.vlpt.us/images/seeker1207/post/9d546558-5f5c-47f6-aa4f-00cbb7d763b8/image.png)

# 참고

https://ko.wikipedia.org/wiki/HTTP_%EC%83%81%ED%83%9C_%EC%BD%94%EB%93%9C

https://developer.mozilla.org/ko/docs/Web/HTTP/Methods

https://medium.com/@sandeep4.verma/http-1-to-http-2-to-http-3-647e73df67a8

https://haerang94.tistory.com/207

https://velog.io/@ziyoonee/HTTP1-%EB%B6%80%ED%84%B0-HTTP3-%EA%B9%8C%EC%A7%80-%EC%95%8C%EC%95%84%EB%B3%B4%EA%B8%B0

https://velog.io/@seeker1207/HTTP-0.9%EC%97%90%EC%84%9C-HTTP-3.0%EA%B9%8C%EC%A7%80

https://evan-moon.github.io/2019/10/08/what-is-http3/#3-way-handshake