# 🎁 Cors

# 📌 CORS란?

- Cross-Origin Resource Sharing
- 교차 출처 리소스 공유
- “교차 출처”라고 하는 것은 “다른 출처”를 의미
- CORS 관련 이슈는 모두 CORS 정책을 위반했기 때문에 발생하는 것이다
- CORS라는 방어막이 존재하기 때문에 우리가 이 곳 저 곳에서 가져오는 리소스가 안전하다는 최소한의 보장을 받을 수 있는 것이다.

## ✅ 출처(Origin)란?
![](https://images.velog.io/images/kcwthing1210/post/98ff9a71-5888-4e97-9c03-96502c382e77/image.png)

- 출처는 Protocol과 Host, 그리고 위 그림에는 나와있지 않지만 :80, :443과 같은 포트 번호까지 모두 합친 것을 의미한다.
- 즉, 서버의 위치를 찾아가기 위해 필요한 가장 기본적인 것들을 합쳐놓은 것이다.
- 출처 내의 포트 번호는 생략이 가능한데, 이는 각 웹에서 사용하는 HTTP, HTTPS 프로토콜의 기본 포트 번호가 정해져있기 때문이다.

## ✅ 같은 출처와 다른 출처의 구분

- URL의 구성 요소 중 Scheme, Host, Port, 이 3가지만 동일
- https://evan-moon.github.io:80라는 출처를 예로 들면 https:// 이라는 스킴에 evan-moon.github.io 호스트를 가지고 :80번 포트를 사용하고 있다는 것만 같다면 나머지는 전부 다르더라도 같은 출처로 인정

- URL	같은 출처	이유
  https://evan-moon.github.io/about	O	스킴, 호스트, 포트가 동일
  https://evan-moon.github.io/about?q=안뇽	O	스킴, 호스트, 포트가 동일
  https://user:password@evan-moon.github.io	O	스킴, 호스트, 포트가 동일
  http://evan-moon.github.io	X	스킴이 다름
  https://api.github.io	X	호스트가 다름
  https://evan-moon.naver.com	X	호스트가 다름
  https://evan-moon.github.com	X	호스트가 다름
  https://evan-moon.github.io:8000	?	브라우저의 구현에 따라 다름

중요한 사실 한 가지는 이렇게 출처를 비교하는 로직이 서버에 구현된 스펙이 아니라 브라우저에 구현되어 있는 스펙이라는 것이다.

만약 우리가 CORS 정책을 위반하는 리소스 요청을 하더라도 해당 서버가 같은 출처에서 보낸 요청만 받겠다는 로직을 가지고 있는 경우가 아니라면 서버는 정상적으로 응답을 하고, 이후 브라우저가 이 응답을 분석해서 CORS 정책 위반이라고 판단되면 그 응답을 사용하지 않고 그냥 버리는 순서인 것이다.

![](https://images.velog.io/images/kcwthing1210/post/c18851c2-324f-4cf2-8595-0579f39ea07d/image.png)
서버는 CORS를 위반하더라도 정상적으로 응답을 해주고, 응답의 파기 여부는 브라우저가 결정한다

즉, CORS는 브라우저의 구현 스펙에 포함되는 정책이기 때문에, 브라우저를 통하지 않고 서버 간 통신을 할 때는 이 정책이 적용되지 않는다. 또한 CORS 정책을 위반하는 리소스 요청 때문에 에러가 발생했다고 해도 서버 쪽 로그에는 정상적으로 응답을 했다는 로그만 남기 때문에, CORS가 돌아가는 방식을 정확히 모르면 에러 트레이싱에 난항을 겪을 수도 있다.



## ✅ CORS의 필요성
출처가 다른 두 개의 어플리케이션이 마음대로 소통할 수 있는 환경은 꽤 위험한 환경이다.

애초에 클라이언트 어플리케이션, 특히나 웹에서 돌아가는 클라이언트 어플리케이션은 사용자의 공격에 너무나도 취약한 친구라는 사실을 잊지말자. 당장 브라우저의 개발자 도구만 열어도 DOM이 어떻게 작성되어있는지, 어떤 서버와 통신하는지, 리소스의 출처는 어디인지와 같은 각종 정보들을 아무런 제재없이 열람할 수 있지 않은가?

최근에는 자바스크립트 소스 코드를 난독화해서 읽기 어렵다고 하지만, 난독화는 어디까지나 난독화일 뿐이지 암호화가 아니다. 그리고 아무리 난독화되어있다고 해도 사람이 바로 이해할 수 없는 정도도 아닌데다가, 소스 코드를 직접 볼 수 있다는 것 자체가 보안적으로 상당히 취약한 부분이다. 심지어 아직까지도 소스 코드의 난독화가 안되어 개발자 도구만 열면 <script> 태그 안에 날 것 그대로의 소스 코드가 떡하니 노출되는 사이트들도 많다.

이런 상황 속에서 다른 출처의 어플리케이션이 서로 통신하는 것에 대해 아무런 제약도 존재하지 않는다면, 악의를 가진 사용자가 소스 코드를 쓱 구경한 후 CSRF(Cross-Site Request Forgery)나 XSS(Cross-Site Scripting)와 같은 방법을 사용하여 여러분의 어플리케이션에서 코드가 실행된 것처럼 꾸며서 사용자의 정보를 탈취하기가 너무나도 쉬워진다.





# 📌 CORS 동작 과정

기본적으로 웹 클라이언트 어플리케이션이 다른 출처의 리소스를 요청할 때는 HTTP 프로토콜을 사용하여 요청을 보내게 되는데, 이때 브라우저는 요청 헤더에 Origin이라는 필드에 요청을 보내는 출처를 함께 담아보낸다.

``` http
Origin: https://evan-moon.github.io
```
이후 서버가 이 요청에 대한 응답을 할 때 응답 헤더의 Access-Control-Allow-Origin이라는 값에 “이 리소스를 접근하는 것이 허용된 출처”를 내려주고, 이후 응답을 받은 브라우저는 자신이 보냈던 요청의 Origin과 서버가 보내준 응답의 Access-Control-Allow-Origin을 비교해본 후 이 응답이 유효한 응답인지 아닌지를 결정한다.

기본적인 흐름은 이렇게 간단하지만, 사실 CORS가 동작하는 방식은 한 가지가 아니라 세 가지의 시나리오에 따라 변경되기 때문에 여러분의 요청이 어떤 시나리오에 해당되는지 잘 파악한다면 CORS 정책 위반으로 인한 에러를 고치는 것이 한결 쉬울 것이다.

### ✔ Preflight Request
- 일반적으로 우리가 웹 어플리케이션을 개발할 때 가장 마주치는 시나리오
- 이 시나리오에 해당하는 상황일 때 브라우저는 요청을 한번에 보내지 않고 예비 요청과 본 요청으로 나누어서 서버로 전송
- 이때 브라우저가 본 요청을 보내기 전에 보내는 예비 요청을 Preflight라고 부르는 것이며, 이 예비 요청에는 HTTP 메소드 중 OPTIONS 메소드가 사용된다.
- 예비 요청의 역할은 본 요청을 보내기 전에 브라우저 스스로 이 요청을 보내는 것이 안전한지 확인하는 것이다.

  ![](https://images.velog.io/images/kcwthing1210/post/05787eb1-16b2-4304-901b-a3f9a6b2f4c8/image.png)

우리가 자바스크립트의 fetch API를 사용하여 브라우저에게 리소스를 받아오라는 명령을 내리면 브라우저는 서버에게 예비 요청을 먼저 보내고, 서버는 이 예비 요청에 대한 응답으로 현재 자신이 어떤 것들을 허용하고, 어떤 것들을 금지하고 있는지에 대한 정보를 응답 헤더에 담아서 브라우저에게 다시 보내주게 된다.

이후 브라우저는 자신이 보낸 예비 요청과 서버가 응답에 담아준 허용 정책을 비교한 후, 이 요청을 보내는 것이 안전하다고 판단되면 같은 엔드포인트로 다시 본 요청을 보내게 된다. 이후 서버가 이 본 요청에 대한 응답을 하면 브라우저는 최종적으로 이 응답 데이터를 자바스크립트에게 넘겨준다.

대부분의 경우 이렇게 예비 요청, 본 요청을 나누어 보내는 프리플라이트 방식을 사용하기는 하지만, 모든 상황에서 이렇게 두 번씩 요청을 보내는 것은 아니다. 조금 까다로운 조건이기는 하지만 어떤 경우에는 예비 요청없이 본 요청만으로 CORS 정책 위반 여부를 검사하기도 한다.


### ✔ Simple Request
- 예비 요청을 보내지 않고 바로 서버에게 본 요청을 보낸 후, 서버가 이에 대한 응답의 헤더에 Access-Control-Allow-Origin과 같은 값을 보내주면 그때 브라우저가 CORS 정책 위반 여부를 검사하는 방식
  -즉, 프리플라이트와 단순 요청 시나리오는 전반적인 로직 자체는 같되, 예비 요청의 존재 유무만 다르다.

![](https://images.velog.io/images/kcwthing1210/post/63e85b68-c929-4dc9-8a62-19d01618e78b/image.png)

- 하지만 아무 때나 단순 요청을 사용할 수 있는 것은 아니고, 특정 조건을 만족하는 경우에만 예비 요청을 생략할 수 있다.
    - 요청의 메소드는 GET, HEAD, POST 중 하나여야 한다.
    - Accept, Accept-Language, Content-Language, Content-Type, DPR, Downlink, Save-Data, Viewport-Width, Width를 제외한 헤더를 사용하면 안된다.
    - 만약 Content-Type를 사용하는 경우에는 application/x-www-form-urlencoded, multipart/form-data, text/plain만 허용된다.
- 대부분의 HTTP API는 text/xml이나 application/json 컨텐츠 타입을 가지도록 설계되기 때문에 사실 상 이 조건들을 모두 만족시키는 상황을 만들기는 그렇게 쉽지 않은 것이 현실이다.

### ✔ Credentialed Request

- 인증된 요청을 사용하는 방법
- 이 시나리오는 CORS의 기본적인 방식이라기 보다는 다른 출처 간 통신에서 좀 더 보안을 강화하고 싶을 때 사용하는 방법
- 기본적으로 브라우저가 제공하는 비동기 리소스 요청 API인 XMLHttpRequest 객체나 fetch API는 별도의 옵션 없이 브라우저의 쿠키 정보나 인증과 관련된 헤더를 함부로 요청에 담지 않는다. 이때 요청에 인증과 관련된 정보를 담을 수 있게 해주는 옵션이 바로 credentials 옵션이다.
  ![](https://images.velog.io/images/kcwthing1210/post/e8557a79-990f-4ad1-86ce-a0d99343303b/image.png)
- 브라우저는 인증 모드가 include일 경우, 모든 요청을 허용한다는 의미의 *를 Access-Control-Allow-Origin 헤더에 사용하면 안된다고 이야기하고 있다.
- 이처럼 요청에 인증 정보가 담겨있는 상태에서 다른 출처의 리소스를 요청하게 되면 브라우저는 CORS 정책 위반 여부를 검사하는 룰에 다음 두 가지를 추가하게 된다.
    - Access-Control-Allow-Origin에는 *를 사용할 수 없으며, 명시적인 URL이어야한다.
    - 응답 헤더에는 반드시 Access-Control-Allow-Credentials: true가 존재해야한다.

## ✅ CORS를 해결할 수 있는 방법

### ✔ Access-Control-Allow-Origin 세팅하기
CORS 정책 위반으로 인한 문제를 해결하는 가장 대표적인 방법은, 그냥 정석대로 서버에서 Access-Control-Allow-Origin 헤더에 알맞은 값을 세팅해주는 것이다.

이때 와일드카드인 *을 사용하여 이 헤더를 세팅하게 되면 모든 출처에서 오는 요청을 받아먹겠다는 의미이므로 당장은 편할 수 있겠지만, 바꿔서 생각하면 정체도 모르는 이상한 출처에서 오는 요청까지 모두 받아먹겠다는 오픈 마인드와 다를 것 없으므로 보안적으로 심각한 이슈가 발생할 수도 있다.

그러니 가급적이면 귀찮더라도 Access-Control-Allow-Origin: https://evan.github.io와 같이 출처를 명시해주도록 하자.

이 헤더는 Nginx나 Apache와 같은 서버 엔진의 설정에서 추가할 수도 있지만, 아무래도 복잡한 세팅을 하기는 불편하기 때문에 소스 코드 내에서 응답 미들웨어 등을 사용하여 세팅하는 것을 추천한다. Spring, Express, Django와 같이 이름있는 백엔드 프레임워크의 경우에는 모두 CORS 관련 설정을 위한 세팅이나 미들웨어 라이브러리를 제공하고 있으니 세팅 자체가 어렵지는 않을 것이다.

### ✔ Webpack Dev Server로 리버스 프록싱하기
사실 CORS를 가장 많이 마주치는 환경은 바로 로컬에서 프론트엔드 어플리케이션을 개발하는 경우라고 해도 과언이 아니다. 백엔드에는 이미 Access-Control-Allow-Origin 헤더가 세팅되어있겠지만, 이 중요한 헤더에다가 http://localhost:3000 같은 범용적인 출처를 넣어주는 경우는 드물기 때문이다.

프론트엔드 개발자는 대부분 웹팩과 webpack-dev-server를 사용하여 자신의 머신에 개발 환경을 구축하게 되는데, 이 라이브러리가 제공하는 프록시 기능을 사용하면 아주 편하게 CORS 정책을 우회할 수 있다.

```js
module.exports = {
  devServer: {
    proxy: {
      '/api': {
        target: 'https://api.evan.com',
        changeOrigin: true,
        pathRewrite: { '^/api': '' },
      },
    }
  }
}
```

이렇게 설정을 해놓으면 로컬 환경에서 /api로 시작하는 URL로 보내는 요청에 대해 브라우저는 localhost:8000/api로 요청을 보낸 것으로 알고 있지만, 사실 뒤에서 웹팩이 https://api.evan.com으로 요청을 프록싱해주기 때문에 마치 CORS 정책을 지킨 것처럼 브라우저를 속이면서도 우리는 원하는 서버와 자유롭게 통신을 할 수 있다. 즉, 프록싱을 통해 CORS 정책을 우회할 수 있는 것이다.





# 🧩 Reference
- https://evan-moon.github.io/2020/05/21/about-cors/

# 🎁 JWT 

# 📌 JWT란?
- Json Web Token
- Json 포맷을 이용하여 사용자에 대한 속성을 저장하는 Claim 기반의 Web Token
- T는 토큰 자체를 정보로 사용하는 Self-Contained 방식으로 정보를 안전하게 전달한다.

![](https://images.velog.io/images/kcwthing1210/post/124febfc-8675-4399-b784-e785a1430fa8/image.png)

애플리케이션이 실행될 때, JWT를 static 변수와 로컬 스토리지에 저장하게 된다. static 변수에 저장되는 이유는 HTTP 통신을 할 때마다 JWT를 HTTP 헤더에 담아서 보내야 하는데, 이를 로컬 스토리지에서 계속 불러오면 오버헤드가 발생하기 때문이다. 클라이언트에서 JWT를 포함해 요청을 보내면 서버는 허가된 JWT인지를 검사한다. 또한 로그아웃을 할 경우 로컬 스토리지에 저장된 JWT 데이터를 제거한다. (실제 서비스의 경우에는 로그아웃 시, 사용했던 토큰을 blacklist라는 DB 테이블에 넣어 해당 토큰의 접근을 막는 작업을 해주어야 한다.)

# 📌 JWT 구조
![](https://images.velog.io/images/kcwthing1210/post/321a6744-a868-4705-ac5f-71c0334c21f5/image.png)

### ✔ Header(헤더)

- 토큰의 헤더는 typ과 alg 두 가지 정보로 구성된다.
- alg: 헤더(Header)를 암호화 하는 것이 아니고, Signature를 해싱하기 위한 알고리즘을 지정하는 것이다.
- typ: 토큰의 타입을 지정 ex) JWT
  alg: 알고리즘 방식을 지정하며, 서명(Signature) 및 토큰 검증에 사용
  ex) HS256(SHA256) 또는 RSA
  {
  "alg": "HS256",
  "typ": JWT
  }



### ✔ PayLoad(페이로드)

- 토큰의 페이로드에는 토큰에서 사용할 정보의 조각들인 클레임(Claim)이 담겨 있다.

- 클레임은 총 3가지로 나누어지며, Json(Key/Value) 형태로 다수의 정보를 넣을 수 있다.

#### (1) 등록된 클레임(Registered Claim)

- 등록된 클레임은 토큰 정보를 표현하기 위해 이미 정해진 종류의 데이터
- 모두 선택적으로 작성이 가능하며 사용할 것을 권장한다.
- 또한 JWT를 간결하게 하기 위해 key는 모두 길이 3의 String이다. 여기서 subject로는 unique한 값을 사용하는데, 사용자 이메일을 주로 사용한다.

  - iss: 토큰 발급자(issuer)
  - sub: 토큰 제목(subject)
  - aud: 토큰 대상자(audience)
  - exp: 토큰 만료 시간(expiration), NumericDate 형식으로 되어 있어야 함 ex) 1480849147370
  - nbf: 토큰 활성 날짜(not before), 이 날이 지나기 전의 토큰은 활성화되지 않음
  - iat: 토큰 발급 시간(issued at), 토큰 발급 이후의 경과 시간을 알 수 있음
  - jti: JWT 토큰 식별자(JWT ID), 중복 방지를 위해 사용하며, 일회용 토큰(Access Token) 등에 사용

#### (2) 공개 클레임(Public Claim)

공개 클레임은 사용자 정의 클레임으로, 공개용 정보를 위해 사용된다. 충돌 방지를 위해 URI 포맷을 이용하며, 예시는 아래와 같다.

{
"https://mangkyu.tistory.com": true
}


#### (3) 비공개 클레임(Private Claim)

비공개 클레임은 사용자 정의 클레임으로, 서버와 클라이언트 사이에 임의로 지정한 정보를 저장한다. 아래의 예시와 같다.

{
"token_type": access
}

# 📌 동작 과정
![](https://images.velog.io/images/kcwthing1210/post/dd743a21-d910-49eb-9d73-df80cedb475f/image.png)

1. 사용자가 id와 password를 입력하여 로그인을 시도합니다.
2. 서버는 요청을 확인하고 secret key를 통해 Access token을 발급합니다.
3. JWT 토큰을 클라이언트에 전달 합니다.
4. 클라이언트에서 API 을 요청할때  클라이언트가 Authorization header에 Access token을 담아서 보냅니다.
5. 서버는 JWT Signature를 체크하고 Payload로부터 사용자 정보를 확인해 데이터를 반환합니다.
6. 클라이언트의 로그인 정보를 서버 메모리에 저장하지 않기 때문에 토큰기반 인증 메커니즘을 제공합니다.
   인증이 필요한 경로에 접근할 때 서버 측은 Authorization 헤더에 유효한 JWT 또는 존재하는지 확인한다.
   JWT에는 필요한 모든 정보를 토큰에 포함하기 때문에 데이터베이스과 같은 서버와의 커뮤니케이션 오버 헤드를 최소화 할 수 있습니다.
   Cross-Origin Resource Sharing (CORS)는 쿠키를 사용하지 않기 때문에 JWT를 채용 한 인증 메커니즘은 두 도메인에서 API를 제공하더라도 문제가 발생하지 않습니다.
   일반적으로 JWT 토큰 기반의 인증 시스템은 위와 같은 프로세스로 이루어집니다.
   처음 사용자를 등록할 때 Access token과 Refresh token이 모두 발급되어야 합니다.

# 📌 JWT 장단점 및 고려사항

### ✔ 장점
- 사용자 인증에 필요한 모든 정보는 토큰 자체에 포함하기 때문에 별도의 인증 저장소가 필요없다
- 분산 마이크로 서비스 환경에서 중앙 집중식 인증 서버와 데이터베이스에 의존하지 않는 쉬운 인증 및 인가 방법을 제공
- 토큰이 올바르게 서명되었는지 확인하는 것은 CPU 사이클을 필요로하며 IO 또는 네트워크 액세스가 필요하지 않으며 최신 웹 서버 하드웨어에서 확장하기가 쉽다.


### ✔ 단점

- Self-contained: 토큰 자체에 정보를 담고 있으므로 양날의 검이 될 수 있다.
- 토큰 길이: 토큰의 페이로드(Payload)에 3종류의 클레임을 저장하기 때문에, 정보가 많아질수록 토큰의 길이가 늘어나 네트워크에 부하를 줄 수 있다.
- Payload 인코딩: 페이로드(Payload) 자체는 암호화 된 것이 아니라, BASE64로 인코딩 된 것이다. 중간에 Payload를 탈취하여 디코딩하면 데이터를 볼 수 있으므로, JWE로 암호화하거나 Payload에 중요 데이터를 넣지 않아야 한다.
- Stateless: JWT는 상태를 저장하지 않기 때문에 한번 만들어지면 제어가 불가능하다. 즉, 토큰을 임의로 삭제하는 것이 불가능하므로 토큰 만료 시간을 꼭 넣어주어야 한다.
- Tore Token: 토큰은 클라이언트 측에서 관리해야 하기 때문에, 토큰을 저장해야 한다.




# 🧩 Reference
- http://www.opennaru.com/opennaru-blog/jwt-json-web-token/
- https://mangkyu.tistory.com/56 [MangKyu's Diary]