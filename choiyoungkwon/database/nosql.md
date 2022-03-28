# Nosql

NoSQL은 Not Only SQL의 약자이다. 기본 RDBMS의 한계를 극복하기 위해 만들어진 새로운 형태의 데이터베이스다.

릴레이션이 아니므로 고정된 스키마가 없고 조인이 힘들다. 빅데이터를 다룰 때, RDBMS로만 트래픽을 감당하기 어려워졌고, 이를 해결하려고 NoSQL이 탄생했다. 

NoSQL은 분산 환경에서 대용량의 데이터를 빠르게 처리하기 위해서 개발되었다. 핵심은 **Horizontal Scalability(수평확장)과 High Availability(고가용성)**이다.

### RDBMS의 한계
많은 데이터량과 데이터 처리량이 계속적으로 증가한다면 RDBMS는 아래와 같은 문제점을 만난다.

- 스키마 문제 : 빅데이터를 RDB의 스키마에 맞춰 변경해서 넣으려면 매우 긴 시간의 down time이 발생
- 스케일업의 한계 : RDBMS는 애초부터 스케일 아웃을 염두에 두고 설계되지 않았다. 관계 모델과 트랜잭션의 연산, 일관성, 속성을 유지하면서 분산환경(스케일아웃)에서 RDBMS를 조작하는 것은 어렵다.

# 장/단점

### 장점
- 스키마가 없기 때문에 유연하다. 즉 언제든지 데이터를 조정하고 새로운 필드를 추가할 수 있다.
- 수직 및 수평적 확장(샤딩) 이 가능하므로 데이터베이스가 애플리케이션에서 발생시키는 모든 읽기 / 쓰기 요청 처리가 가능하다
- 데이터는 애플리케이션이 필요로 하는 형식으로 저장된다. 이렇게 하면 데이터를 읽어오는 속도가 빨라진다.

### 단점
- 데이터베이스 일관성에 약하다. 이 일관성을 가용성, 분할 용인, 속도와 맞바꾸었다
    - 분할 용인 : 네트워크 실패로 인하여 임의의 분할이 발생해도 시스템은 계속적으로 동작해야 한다. 임의의 메시지들의 손실 또는 시스템의 부분 실패에도 불구하고, 시스템은 지속적으로 동작
- key값에 대한 입출력만 지원한다.
- 스키마가 정해져 있지 않아, 데이터에 대한 규격화가 되어 있지 않다.
- 데이터가 여러 컬렉션에 중복되어 있어서 데이터를 UPDATE 하는 경우 모든 컬렉션에서 수행해야하기 때문에 느리다.
- 데이터 중복으로 인한 수정 작업의 번거로움

# CAP

분산형 구조는 일관성(Consistency), 가용성(Availability), 분산 허용(Partitioning Tolerance)의 3가지 특징을 가지고 있다. CAP 이론은 이 중 2가지만 만족할 수 있다는 이론이다. NoSQL은 대부분 이 CAP 이론을 따르고 있다.

- 일관성(Consistency) : 분산된 노드 중 어느 노드로 접근하더라도 데이터 값이 같아야 한다. (데이터 복제 중에 쿼리가 되는 일관성을 제공하지 않는 시스템의 경우 다른 데이터 값이 쿼리될 수 있다.)

- 가용성(Availability) : 클러스터링된 노드 중 하나 이상의 노드가 실패(Fail)라도 정상적으로 요청을 처리할 수 있는 기능을 제공한다.

- 분산 허용(Partition Tolerance): 클러스터링 노드 간에 통신하는 네트워크가 장애가 나더라도 정상적으로 서비스를 수행한다. 노드 간 물리적으로 전혀 다른 네트워크공간에 위치도 가능하다.
일반적으로 RDBMS는 일관성과 가용성을 만족한다. NoSQL은 가용성과 분산허용을 만족하는 제품군과 일관성과 분산허용을 만족하는 제품군으로 나눌 수 있다.


|분류|	사례|	설명|
|---|---|---|
|C + A|	RDBMS	|시스템 다운에도 메시지 손실 방지, 트랜잭션이 필요한 경우 필수|
|C + P|	몽고DB,HBase| 모든 노드가 함께 퍼포먼스를 내용 성능 위주의 구조|
|A + P|	카산드라| 비동기화된 서비스 스토어에 적합|

# 저장방식에 따른 분류

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FkKtTE%2FbtrmgFa2t9M%2FXBfLBPrksvVoRFbqVJr4EK%2Fimg.png)

## 키-값 저장소(key-value)

Key와 Value으로 구성된 배열구조의 데이터베이스로 가장 단순한 구조
특징

- 기본적인 패턴으로 Key, Value가 하나의 묶음으로 저장되는 구조이기 때문에 속도가 빠르며 분산 저장에 용이하다
- 값에 모든 데이터 타입이 허용가능하다.
- Key는 중복될 수 없고 이 Unique Key에 각각 하나의 Value를 가지고 있는 형태가 된다. 데이터를 조회 및 입력할 때, Key를 가지고 접근할 수 있다.

### 언제 사용하는게 좋을지?
- 성능 향상을 위해 RDBMS 에서 캐싱 (Redis)
- 장바구니 같은 웹애플리케이션에서 일시적인 속성 추적
- 이미지나 오디오 파일 같은 대용량 객체 저장

종류
- Redis
- AWS DynamoDB
- Riak

## 그래프 저장소(graph)

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbahF1q%2FbtrmhYHobAJ%2F6rpBdOtD83ncgkcxb3D6G0%2Fimg.png)

- 노드와 관계로 구성된 데이터베이스로 근접한 객체를 모델링할 목적으로 설계
특징

### 특징
- RDBMS보다 성능이 좋고 유연하며 유지보수에 용이한것으로 특징
- Social Networks, Network diagrams 등에 사용

종류
- Neo4j
- Blazegraph
- OrientDB

## 컬럼 저장소(column)

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FWTgcL%2FbtrmgRhYoXd%2Ffoo83XzJL6JzzPb0A5Dzl1%2Fimg.png)

- Key, Value와 유사한 형태이다. 단지 데이터가 내부적으로 Key를 기준으로 Sorting되서 저장되는 점이 차이가 있다. Order by를 제공하지 않는 NoSQL에서 다양한 방법으로 활용할 수 있다는 장점이 있다.
- 컬럼과 로우로 구성된 데이터베이스로 컬럼은 이름과 값으로 구성되고 로우는 각기 다른 컬럼으로 구성이 가능

## 문서 저장소(document)

- Key, Value에서 확장된 형태이다. 저장되는 Value의 타입으로 Document라는 구조화된 데이터 타입(JSON, XML 등)이 사용된다. 복잡한 계층 구조를 잘 표현할 수 있다는 점이 장점이다. 제품에 따라 Sorting, Join, Grouping 등 RDB와 같은 추가 기능이 지원되기도 하다. 앞으로 정리할 MongoDB가 이 종류에 해당되며 여러 기능이 제공된다.
- JSON 기반으로 통신을 하는 HTTP 웹 서버의 경우 편리하게 데이터를 사용할 수 있다.
- NoSQL데이터베이스 중 가장 인기가 높다

특징
- 계층적 트리 데이터 방식으로 저장
- _id : PK, RowID를 가짐
- 컬럼 없음 , Schema 없음

### 언제 사용하면 좋을지?
- 대용량 데이터를 읽고 쓰는 웹 사이트용 벡엔드 지원
- JSON 데이터 구조를 사용하는 애플리케이션
- 비정규화된 중첩 구조의 데이터를 사용하는 애플리케이션

종류
- MongoDB
- Azure Cosmose DB
- Couch DB
- MarkLogin
- OrientDB


---
참고 : 

https://sjh836.tistory.com/97

https://sujl95.tistory.com/83

