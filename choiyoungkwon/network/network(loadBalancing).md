# 로드 밸런싱(Load Balancing)

부하분산 또는 로드 밸런싱은 컴퓨터 네트워크 기술의 일종으로 중앙처리장치 혹은 저장장치와 같은 컴퓨터 자원들에게 작업을 효율적으로 나누는 것을 의미한다.

서버에 가해지는 부하(=로드)를 분산(=밸런싱)해주는 장치 또는 기술이다.

사업의 규모가 확장되고, 클라이언트의 수가 늘어나게 되면 기존 서버만으로는 정상적인 서비스가 불가능하게 되는데, 이런 증가한 트래픽에 대처할 수 있는 방법은 크게 두 가지다.

- Scale up : 서버 자체의 성능을 높이는 것
- Scale out : 여러 대의 서버를 두는 것

Scale-out의 방식은 여러 대의 서버로 트래픽을 균등하게 분산해주는 로드밸런싱이 반드시 필요하다.

Scale-out의 장점
- 하드웨어 향상하는 비용보다 서버 한대 추가 비용이 더 적습니다.
- 여러 대의 Server 덕분에 무중단 서비스를 제공할 수 있습니다.
- 여러 대의 Server에게 균등하게 Traffic을 분산시켜주는 역할을 하는 것이 Load Balancer입니다.

# 로드 밸런싱의 종류

로드 밸런싱의 종류는 OSI 7계층에 따라 나뉩니다.

부하 분산에는 L4 로드밸런서와 L7 로드밸런서가 가장 많이 활용됩니다. 

그 이유는 L4 로드밸런서부터 포트(Port)정보를 바탕으로 로드를 분산하는 것이 가능하기 때문입니다. 한 대의 서버에 각기 다른 포트 번호를 부여하여 다수의 서버 프로그램을 운영하는 경우라면 최소 L4 로드밸런서 이상을 사용해야만 합니다.

![image](https://post-phinf.pstatic.net/MjAxOTEyMTBfNCAg/MDAxNTc1OTU1MzY3OTM2.nG91HOEOh6Sc1AuUgbN3O4pcnEI-rh24UKSrrrjkrcsg.VcG18MidW4az7Oh0RQfRPLDBHNRyGayE1BsQxDImL3Ig.JPEG/L4-%EB%A1%9C%EB%93%9C%EB%B0%B8%EB%9F%B0%EC%8B%B1.jpg?type=w1200)

- L4 로드밸런서는 네트워크 계층(IP, IPX)이나 트랜스포트 계층(TCP, UDP)의 정보를 바탕으로 로드를 분산합니다. IP주소나 포트번호, MAC주소, 전송 프로토콜에 따라 트래픽을 나누는 것이 가능합니다.

---

![image](https://post-phinf.pstatic.net/MjAxOTEyMTBfMjA1/MDAxNTc1OTU1MzgxODY5.odnG4CRES0e5bH7sOKyWRP1c8uO_XC4VX9A3HPeI1JQg.lNL2eJYbMz6NX1e5YFzfHDMQHn4YrdOJR2VYHmq5e1Ig.JPEG/L7-%EB%A1%9C%EB%93%9C%EB%B0%B8%EB%9F%B0%EC%8B%B1.jpg?type=w1200)

-  L7 로드밸런서의 경우 애플리케이션 계층(HTTP, FTP, SMTP)에서 로드를 분산하기 때문에 HTTP 헤더, 쿠키 등과 같은 사용자의 요청을 기준으로 특정 서버에 트래픽을 분산하는 것이 가능합니다. 

- 쉽게 말해 패킷의 내용을 확인하고 그 내용에 따라 로드를 특정 서버에 분배하는 것이 가능한 것입니다. 위 그림과 같이 URL에 따라 부하를 분산시키거나, HTTP 헤더의 쿠키값에 따라 부하를 분산하는 등 클라이언트의 요청을 보다 세분화해 서버에 전달할 수 있습니다. 또한 L7 로드밸런서의 경우 특정한 패턴을 지닌 바이러스를 감지해 네트워크를 보호할 수 있으며, DoS/DDoS와 같은 비정상적인 트래픽을 필터링할 수 있어 네트워크 보안 분야에서도 활용되고 있습니다.

![image](https://post-phinf.pstatic.net/MjAxOTEyMTBfMTUx/MDAxNTc1OTU2NzEwMzMy.SekjHws4oCgNmCkjYoiZg_pfAlBu2yC66wPkLq0JHbsg.Zn9aLJYZX7rbdEL-X4HRkVO4PCgDNanhQntuR-iGBwkg.PNG/%EC%9B%B9_1920_%E2%80%93_1.png?type=w1200)


# Load Balancing 알고리즘 종류

## - 라운드로빈 방식(Round Robin Method)
서버에 들어온 요청을 순서대로 돌아가며 배정하는 방식입니다. 클라이언트의 요청을 순서대로 분배하기 때문에 여러 대의 서버가 동일한 스펙을 갖고 있고, 서버와의 연결(세션)이 오래 지속되지 않는 경우에 활용하기 적합합니다.

## - 가중 라운드로빈 방식(Weighted Round Robin Method)
각각의 서버마다 가중치를 매기고 가중치가 높은 서버에 클라이언트 요청을 우선적으로 배분합니다. 주로 서버의 트래픽 처리 능력이 상이한 경우 사용되는 부하 분산 방식입니다. 예를 들어 A라는 서버가 5라는 가중치를 갖고 B라는 서버가 2라는 가중치를 갖는다면, 로드밸런서는 라운드로빈 방식으로 A 서버에 5개 B 서버에 2개의 요청을 전달합니다.

## - IP 해시 방식(IP Hash Method)
클라이언트의 IP 주소를 특정 서버로 매핑하여 요청을 처리하는 방식입니다. 사용자의 IP를 해싱해(Hashing, 임의의 길이를 지닌 데이터를 고정된 길이의 데이터로 매핑하는 것, 또는 그러한 함수) 로드를 분배하기 때문에 사용자가 항상 동일한 서버로 연결되는 것을 보장합니다. 

## - 최소 연결 방식(Least Connection Method)
요청이 들어온 시점에 가장 적은 연결상태를 보이는 서버에 우선적으로 트래픽을 배분합니다. 자주 세션이 길어지거나, 서버에 분배된 트래픽들이 일정하지 않은 경우에 적합한 방식입니다.

## - 최소 리스폰타임(Least Response Time Method)
서버의 현재 연결 상태와 응답시간(Response Time, 서버에 요청을 보내고 최초 응답을 받을 때까지 소요되는 시간)을 모두 고려하여 트래픽을 배분합니다. 가장 적은 연결 상태와 가장 짧은 응답시간을 보이는 서버에 우선적으로 로드를 배분하는 방식입니다.


참고 : 

https://dev.classmethod.jp/articles/load-balancing-types-and-algorithm/

https://m.post.naver.com/viewer/postView.nhn?volumeNo=27046347&memberNo=2521903