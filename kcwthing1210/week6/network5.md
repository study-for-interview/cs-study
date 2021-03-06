# 🎁 TLS/SSL handshake

# 📌 TLS/SSL이란?
인터넷은 안전한 통신을 위하여 암호화를 사용한다. 암호화란 일반적인 평문을 알아볼 수 없도록 암호화 하여 암호문으로 만드는 과정이다. 이와 같은 과정을 웹 브라우저와 웹 서버에는 HTTPS를 사용하여 암호화를 한다.

HTTPS는 SSL(Secure Socket Layer)/TLS(Transport Layer Security) 전송기술을 사용한다. TCP,UDP와 같은 일반적인 인터넷 통신에 안전한 계층을 추가하는 방식이다. 그리고 이 기술을 구현하기 위해 웹 서버에서 설치하는 것이 SSL/TLS dlswmdtjdlek. TLS는 SSL의 개선 버전으로, 최신 인증서는 TLS를 사용하지면 편의적으로 SSL인증서라고 부른다.

# 📌 SSL HandShake
![](https://images.velog.io/images/kcwthing1210/post/e18733ad-be27-4335-ad02-2de94029edd7/image.png)

파란색 부분은 TCP layer의 3-way handshake로 HTTPS가 TCP기반 프로토콜이기 때문에 암호화 협상(SSL Handshake)에 앞서 연결을 생성하기 위해 실시하는 과정이고 아래 노란색 부분이 SSL HandShake 과정이다.


![](https://images.velog.io/images/kcwthing1210/post/8334e4b8-b302-43bf-9725-668d09ff51ab/image.png)

1. 클라이언트가 서버에 접속 (Client Hello)
   내가 접속하려는 사이트가 HTTPS를 사용하면 브라우저는 TCP연결을 위한 3-Way HandShake를 수행한 브라우저는 다음 정보를 Client Hello 단계에 보낸다
- 브라우저가 사용하는 SSL/TLS 버전 정보
- 브라우저가 지원하는 암호화 방식 모음(cipher suite)
    - cipher suite : 보안의 궁극적 목표를 달성하기 위해 사용하는 방식을 패키지 형태로 묶어놓은것
    - ![](https://images.velog.io/images/kcwthing1210/post/fb3a3034-c8fc-48ee-a315-99063ab07f45/image.png)
- 브라우저가 순간적으로 생성한 임의의 난수
- 만약 이전에 SSL 핸드 쉐이크가 완료된 상태라면, 그때 생성된 세션아이디
- 기타 확장 정보

2. 서버 (Server Hello) )서버 또한 위의 인사에 응답하며, 다음 정보를 클라이언트에 제공한다.

- 브라우저의 암호화 방식 정보 중에서, 서버가 지원하고 선택한 암호화 방식(cipher suite)
- 서버의 공개키가 담긴 SSL 인증서(인증서는 CA의 비밀키로 암호화되어 발급된 상태)
- 서버가 순간적으로 생성한 임의의 난수
- 클라이언트 인증서 요청(선택사항)

3. 클라이언트) 브라우저는 서버의 SSL 인증서가 믿을만한지 확인
   대부분의 브라우저에는 공신력 있는 CA들의 정보와 CA가 만든 공개키가 이미 설치되어 있다. 서버가 보낸 SSL 인증서가 정말 CA가 만든것인지 확인하기 위해 내장된 CA공개키로 암호화된 인증서를 복호화 해본다. 정상적으로 복호화 되었다면 CA가 발급한 것이 증명된다. 만약 등록된 CA가 아니거나, 등록된 CA가 만든 인증서처럼 꾸몄다며 이 과정에서 발각되어 브라우저 경고를 보낸다.

4. 클라이언트) 브라우저는 자신이 생성한 난수와 서버의 난수를 이용하여 premaster secret를 만든다.
   웹 서버 인증서에 딸려온 웹 사이트의 공개키로 이것을 암호화 하여 서버로 전송한다.

5. 서버) 서버는 사이트의 비밀키로, 브라우저가 보낸 premaster secret값을 복호화 한다.
   복호화 한 값을 master secret값으로 저장한다. 이것을 사용하여 방금 브라우저와 만들어진 연결에 고유한 값을 부여하기 위한 session key를 생성한다. 세션 키는 대칭키 암호화에 사용할 키이다. 이것으로 브라우저와 서버 사이에 주고받는 데이터를 암호화 하고 복호화 한다.

6. 서버/클라이언트) SSL handshake를 종료하고 HTTPS통신을 시작한다.
   브라우저와 서버는 SSL handshake가 정상적으로 완료하였고, 이제는 웹상에서 데이터를 세션키를 사용하여 암호화/복호화 하며 https 프로토콜을 통해 주고받을 수 있다. https통신이 완료되는 시점에서 서로에게 공유된 세션키를 폐기한다. 만약 세션이 유지되고 있다면 브라우저는 SSL handshake요청이 아닌 세션ID만 서버에게 알려주면 된다. 이부분은 1번에서 업급 되었다.


# Reference
- https://aws-hyoh.tistory.com/entry/HTTPS-%ED%86%B5%EC%8B%A0%EA%B3%BC%EC%A0%95-%EC%89%BD%EA%B2%8C-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-3SSL-Handshake
- https://brunch.co.kr/@sangjinkang/38

# 🎁 로드밸런싱


![](https://images.velog.io/images/kcwthing1210/post/83849c66-1c87-4376-b45f-70bc59ba0c32/image.png)

부하분산 또는 로드 밸런싱은 컴퓨터 네트워크 기술의 일종으로 중앙처리장치 혹은 저장장치와 같은 컴퓨터 자원들에게 작업을 나누는 것을 의미한다.

서버에 가해지는 부하(=로드)를 분산(=밸런싱)해주는 장치 또는 기술이다.

사업의 규모가 확장되고, 클라이언트의 수가 늘어나게 되면 기존 서버만으로는 정상적인 서비스가 불가능하게 되는데, 이런 증가한 트래픽에 대처할 수 있는 방법은 크게 두 가지다.

Scale up : 서버 자체의 성능을 높이는 것
Scale out : 여러 대의 서버를 두는 것
Scale-out의 방식은 여러 대의 서버로 트래픽을 균등하게 분산해주는 로드밸런싱이 반드시 필요하다.

# 📌 로드 밸런싱 알고리즘
## ✔ 라운드로빈
서버에 들어온 요청을 순서대로 돌아가며 배정하는 방식
서버와의 연결이 오래 지속되지 않는 경우 적합하다.

## ✔ 가중 라운드로빈 방식
각 서버에 가중치를 매기고 가중치가 높은 서버에 요청을 우선적으로 배정하는 방식
서버의 트래픽 처리 능력이 다른 경우 사용한다.

## ✔ 최소 연결 방식
요청이 들어온 시점에 가장 적은 연결 상태를 보이는 서버에 트래픽을 배정하는 방식.
서버에 분배된 트래픽들이 일정하지 않은 경우에 적합하다.

## ✔ IP 해시 방식
클라이언트의 IP주소를 특정 서버로 매핑하여 요청을 처리하는 방식
사용자가 항상 동일한 서버로 연결된다.

# 📌 L4 로드 밸런싱
트랜스포트 계층에서 로드를 분산한다.

TCP, UDP 포트 정보를 바탕으로 한다.

데이터 안을 보지 않고 패킷 레벨에서만 로드를 분산하기 때문에 속도가 빠르고 효율이 높음

섬세한 라우팅이 불가능하지만 L7로드 밸런서보다 저렴하다.

# 📌 L7 로드 밸런싱
애플리케이션 계층에서 로드를 분산한다.

HTTP 헤더, 쿠키 등과 같은 사용자 요청을 기준으로 특정 서버에 트래픽을 분산하는 것이 가능하다. 즉, 패킷 내용을 확인하고 그 내용에 따라 로드를 특정 서버에 분배하는 것이 가능
특정 기능을 하는 요청이 들어오면 그 요청을 처리하는 서버로 보내는,,,

더 섬세한 라우팅이 가능하고, 비정상적인 트래픽을 필터링 할 수 있다.

패킷의 내용을 복호화 해야하기 때문에 더 많은 비용이 든다.