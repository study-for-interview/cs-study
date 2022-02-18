# Load Balancing과 AWS의 Load Balancer
[출처 블로그1](https://dev.classmethod.jp/articles/load-balancing-types-and-algorithm/)
[출처 블로그2](https://no-easy-dev.tistory.com/entry/AWS-ALB%EC%99%80-NLB-%EC%B0%A8%EC%9D%B4%EC%A0%90)

## 로드 밸런싱(Load balancing)이란?
```
부하분산 또는 로드 밸런싱(load balancing)은 컴퓨터 네트워크 기술의 일종으로 
둘 혹은 셋이상의 중앙처리장치 혹은 저장장치와 같은 컴퓨터 자원들에게 작업을 나누는 것을 의미한다.

즉, 여러 서버가 작업을 분산 처리 하는것을 로드 밸런싱이라고 한다.
가용성 및 응답시간을 최적화 시킬 수 있다.

* 가용성(Availability) : 서버와 네트워크, 프로그램 등의 정보 시스템이 정상적으로 사용 가능한 정도
```

<br> <br>

## 로드 밸런서(LB: Load balancer)란 ?
```
하나의 인터넷 서비스가 발생하는 트래픽이 많을 때,
여러 대의 서버가 분산 처리하여 서버의 로드율 증가, 부하량, 속도 저하 등을 고려하여
적절히 분산 처리하여 해결해주는 서비스

즉, 로드 밸런싱 기술을 제공하는 서비스이다.
```

* 아래의 그림처럼 사용자가 많을때 트래픽이 하나의 서버로 몰리지 않도록 적절하게 분배시켜주는 역할을 한다.
    ![](2022-02-14-04-08-01.png)


<br> <br>

## AWS 로드 밸런서의 종류
```
AWS 서비스를 사용하다보면 자주 접하게 되는 서비스가 로드 밸런싱이다.
AWS의 로드 밸런서(LB: Load balancer)는 OSI 7 계층 중 어느 계층에서 동작하는지에 따라 
NLB(Network LoadBalancer)와 ALB(Application LoadBalancer)로 나눌 수 있다. 
기존에는 CLB(Classic LoadBalancer)도 있었지만, 현재에는 거의 사용하지 않고 주로 NLB 또는 ALB를 사용하고 있다.
```

* NLB(`L4 LB`) : **Transport 계층**을 사용, IP 주소와 포트 번호 부하 분산이 가능
* ALB(`L7 LB`) : **Application 계층**을 사용, URL 또는 HTTP 헤더에서 부하 분산이 가능
* L4, L7은 OSI 7계층에서 Layer 4, Layer 7을 나타내며 각각 Transport계층, Application계층에 해당함

* 참고: OSI 7계층
    ![](2022-02-14-03-50-48.png)

<br>

## AWS LB: ALB와 NLB 차이점
> 직접 사용해봐야 차이점을 느낄 수 있을것 같음

### ALB
1. ALB는 L7단의 로드 밸런서를 지원합니다.
2. ALB는 HTTP/HTTPS 프로토콜의 헤더를 보고 적절한 패킷으로 전송합니다.
3. ALB는 IP주소 + 포트번호 + 패킷 내용을 보고 스위칭합니다.
4. ALB는 IP 주소가 변동되기 때문에 Client에서 Access 할 ELB의 DNS Name을 이용해야 합니다.
5. ALB는 L7단을 지원하기 때문에 SSL 적용이 가능합니다.

### NLB
1. NLB는 L4단의 로드 밸런서를 지원합니다.
2. NLB는 TCP/IP 프로토콜의 헤더를 보고 적절한 패킷으로 전송합니다.
3. NLB는 IP + 포트번호를 보고 스위칭합니다.
4. NLB는 할당한 Elastic IP를 Static IP로 사용이 가능하여 DNS Name과 IP주소 모두 사용이 가능합니다.
5. NLB는 SSL 적용이 인프라 단에서 불가능하여 애플리케이션에서 따로 적용해 주어야 합니다.



![](2022-02-14-03-59-16.png)
