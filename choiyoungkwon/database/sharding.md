# Sharding&Master/Slave

# Replication(복제)

복제는 같은 데이터를 복사해서 여러 노드에 분산하는 방법이다.
복제에는 크게 마스터-슬레이브와 피어 투 피어 방식이 있다.

```
database node: 데이터베이스의 인스턴스를 말한다. main node는 쓰기, 그 외의 노드는 읽기 전용으로 사용되는 것이 전형적이다. main node를 변경했을 때 나머지 node들은 그에 따라 변하게 되는 구조다. 
```
## 마스터-슬레이브(master-slave)

마스터-슬레이브의 경우 여러 노드에 데이터를 복제하여 사용하는 방법이다. 

이 때 노드를 마스터 노드와 슬레이브 노드라고 부르며, 모든 쓰기는 마스터에서 행하고 읽기는 마스터나 슬레이브에서 처리 된다. 쓰기가 실행 될 경우, 데이터는 마스터에서 슬레이브로 복제된다.

읽기를 마스터 노드와 슬레이브 노드에서 처리하므로, 읽기가 많이 발생하는 작업에서 성능 효과를 얻게 된다. (더 많은 읽기 요청을 처리하고 싶다면 스케일 업을 하면 된다.)

만약 마스터 노드가 문제가 생기면 다른 슬레이브 노드가 마스터 노드가 되는 방식을 사용할 수도 있다. 이럴 경우 쓰기 작업(마스터가 실행하는)이 실패해도 빠르게 복구 가능하다.

그러나, 어쩔 수 없는 단점도 존재하는데, 바로 쓰기 작업을 통한 변경사항을 모든 슬레이브에게 업데이트 하기 전에 다른 클라이언트에서 읽기 작업을 실행하는 시나리오가 생길 수도 있다는 것이다. 이럴 경우 데이터의 일관성이 사라지게 된다. 

## 피어 투 피어 (peer-to-peer)

피어 투 피어 구조는 마스터를 두지 않고 모든 노드가 마스터이자 슬레이브가 되는 방법이다. 

모든 복제본의 가중치는 똑같고, 읽기/쓰기 작업 역시 모든 노드가 서로 동기화 되며 실행된다. 

그러나 역시 이 방식도 마스터-슬레이브 처럼 데이터 일관성을 해치는 경우가 발생한다. 서로 다른 클라이언트에서 서로 다른 노드의 같은 데이터에 읽기/쓰기 작업을 하는 경우가 될 것이다.

# 샤딩 (Sharding)

샤딩(sharding)은 horizontal partitioning(수평적)과 관련된 데이터베이스 설계 패턴이다. 

한 테이블의 row들을 여러 개의 서로 다른 테이블, 즉 파티션으로 분리하는 것을 말한다.

vertical partitioning의 경우 열 전체가 완전히 새로운 테이블로 분리되기 때문에, 테이블 내의 데이터들은 독립적이며 열과 행이 모두 달라진다.

![image](https://media.vlpt.us/images/matisse/post/950e4322-a318-4015-b7c2-7526c8a457b0/image.png)

shards는 샤딩을 통해 나누어진 블록들을 말한다. 

샤딩은 데이터를 작은 덩어리(smaller chunks)로 쪼개는 것이고, 이 작은 덩어리를 logical **shards**라고 부른다. logical shards는 분리된 physical shard, 즉 database node에 뿌려진다.

shards들은 자립성이 강하기 때문에 같은 데이터나 컴퓨터 자원을 공유하지 않는다. (물론 reference table로 사용할 목적으로 각 shards에 특정 테이블을 복제할 수는 있다.)

# 장점

- 수평적 확장 horizontal scaling (=scaling out)이 가능하다
    - 서버의 하드웨어(RAM, CPU 등)를 업그레이드하는 수직적 확장과 다르게, 존재하는 stack에 machine을 추가하는 방식으로 능력을 향상시킬 수 있다.

- 쿼리 반응 속도를 빠르게 한다: 스캔 범위를 줄이기 때문이다.

- application을 신뢰할 수 있게 만든다.
    - outage가 생겼을 때, un-sharded 데이터베이스와 다르게 단일 shard에만 영향을 줄 확률이 높다. application이 일부라도 작동할 수 있도록 위험을 완화시켜준다.


# 단점

- 잘못 사용 했을 때 데이터 손실이 크다.
- 데이터가 한 쪽 샤드에 쏠려 샤딩이 무의미해질 수 있다.
- 한 번 쪼개게 되면, 다시 un-shared구조로 돌리기 어렵다.
- 모든 DB 엔진에서 지원되지 않을 수 있다.

# 구조

데이터가 맞는 shard에 들어가는 것이 중요하다. 그렇지 않으면 데이터를 잃거나 쿼리가 매우 느려진다. 보편적인 sharding 방법은 다음과 같다.

# Sharding 방법

# Key Based Sharding

hash based sharding이라고도 불린다.

새로운 데이터를 받아서 어느 shard로 갈지 결정하는 hash함수와 연결하는 방식이다.

hash 함수는 고객 이메일과 같은 데이터 조각을 Input으로 받아, hash value라는 완전히 다른 형태의 값을 Ouput으로 내보낸다. 

sharding의 관점에서 봤을 때 hash value는 들어오는 데이터가 저장될 shard를 결정하는 shard ID가 될 것이다.

![image](https://media.vlpt.us/images/matisse/post/246ac67b-84d4-4a6b-b601-130ff311dac2/image.png)

장점

- 이 전략의 가장 큰 장점은 hotspots를 방지하기 위해 데이터를 골고루 분배할 수 있고, 알고리즘적으로 분배하기 때문에 range나 directory와 다르게 모든 데이터가 어디에 위치하는지 말해주는 map을 가질 필요가 없다.

# Range Based Sharding

주어진 value의 범위를 기반으로 데이터를 쪼갠다. 데이터베이스에 어떤 브랜드의 카탈로그에 모든 상품에 대한 정보가 들어있다고 하자. 

이 방식을 적용하면, 몇몇 개의 shard를 만들고 가격 범위에 따라서 상품 정보를 저장하게 될 수 있을 것이다.

![image](https://media.vlpt.us/images/matisse/post/f8f64d2c-b878-4bf1-a743-6cb9a656d847/image.png)

장점

- 가장 큰 장점은 실행이 비교적 간단하다는 것이다. 모든 shard들은 다른 데이터를 가지고 있고, original 데이터베이스 뿐 아니라 서로가 똑같은 스키마를 가지게 된다. application code는 그저 데이터가 어떤 범위인지 읽고 그에 상응하는 shard에 쓰면 된다.

# Directory Based Sharding

이 sharding을 실행하기 위해서는 반드시 어떤 shard가 어떤 데이터를 갖고 있는지를 추적할 수 있는 shard key를 사용하는 lookup table을 만들고 유지해야 한다.

### lookup table

간단히 말하면 특정 데이터를 찾을 수 있는(where specific data can be found) 정적인 정보를 갖고 있는 테이블이다.

![image](https://media.vlpt.us/images/matisse/post/3ac00843-76bd-4fe8-9d97-34aac1d1b443/image.png)

장점

- 유연성(flexibility)이다. 

- range based sharding은 범위에 국한되고, key based sharding은 만들고 난 뒤 바꾸기 매우 어려운 hash 함수에 국한된다. 

- 반면 directory based sharding은 데이터를 쪼개기 위한 entry들은 어떤 시스템이나 알고리즘에 상관 없이 entry를 할당할 수 있도록 해준다. 동적으로 shard를 추가하는 것도 비교적 쉽다.


# 샤드를 사용하는 이유?

여러 복잡성 때문에, sharding은 대규모의 데이터를 다룰 때 주로 사용된다.

## 샤드를 고려해야할 상황

- 애플리케이션 데이터의 양이 단일 database node의 스토리지 한계를 초과했을 때
- 쓰기 & 읽기 양이 단일 노드나 read replica가 핸들링할 수 있는 수준을 넘어서서 반응이 느려졌을 때
- 하나의 database node 또는 read replica에 가능한 네트워크 대역폭을 초과해 반응 속도가 느려졌을 때

다른 옵션은 없을까?

sharding을 하기 전, 데이터베이스를 최적화할 수 있는 모든 다른 옵션들을 검토해야 한다. 옵션 들은 다음과 같다.

## setting up a remote database

monolithic 애플리케이션(모든 컴포넌트들이 같은 서버에 있는)을 작업한다면, 자신만의 머신으로 데이터베이스를 옮겨 퍼포먼스를 향상시킬 수 있다. 데이터베이스 테이블을 건들지 않기 때문에 sharding만큼 복잡하지 않지만, 나머지 인프라와는 별개로 데이터베이스를 수직 확장하는 것을 허용한다.

## Implementing caching

읽기 퍼포먼스가 문제라면, 캐싱도 좋은 방법이다. 이미 요청된 데이터들을 일시적으로 메모리에 저장하고, 나중에 접근할 때 훨씬 빠르게 접근할 수 있게 해준다.

## Creating one or more read replicas

읽기 퍼포먼스를 높여줄 다른 방법은 primary server에서 데이터를 카피해 한 개 이상의 secondary server를 만드는 것이다. 이렇게 하면 새로 쓰인 것들은 secondary로 카피되기 전에 primary로 가고, 읽기는 secondary에서만 발생한다.
읽기와 쓰기를 나누는 것은 한 개의 머신에서 너무 많이 로드하는 것을 방지해주고, 느려지거나 충돌이 생기는 것을 막아준다. computing resource, 즉 돈이 더 많이 들기 때문에 누군가에게는 제약이 될 수 있긴 하다.

## Upgrading to a larger server

대부분의 상황에서 더 많은 자원을 가진 머신으로 데이터베이스를 scaling up 하는 것은 sharding에 비해 공수가 적게 든다. replica를 만드는 것과 같이 서버를 업그레이드하는 것은 비용이 더 든다. 따라서 업그레이드가 베스트 옵션이라면 리사이징을 거쳐야할 것이다.

## 요약

sharding은 데이터베이스 수평 확장을 고려할 때 좋은 해결책이 될 수 있다. 하지만 복잡성과 잠재적 실패 지점을 만들 수도 있다. 

어떤 이에게는 필요할 수도 있지만, 다른 경우 sharding이 주는 이점보다 sharded architecture를 만들고 유지하는데 드는 시간과 비용이 압도적일 수도 있다.

---

참고 :
 
https://velog.io/@matisse/Database-sharding%EC%97%90-%EB%8C%80%ED%95%B4

