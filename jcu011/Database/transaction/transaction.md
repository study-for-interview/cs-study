# 트랜잭션
* [참고 블로그1](https://elanddba.tistory.com/13)
* [참고 블로그2](https://sabarada.tistory.com/121)
* [참고 블로그3](https://joont92.github.io/db/%ED%8A%B8%EB%9E%9C%EC%9E%AD%EC%85%98-%EA%B2%A9%EB%A6%AC-%EC%88%98%EC%A4%80-isolation-level/)

<br> <br>

## 트랜잭션이란 ?

트랜잭션(Transaction)이란, 데이터베이스의 상태를 변화시키기 해서 수행하는 작업의 단위를 뜻한다.

데이터베이스의 상태를 변화시킨다는 것은 SQL을 이용하여 데이터베이스를 접근 하는 것을 의미한다.





<br> <br> <br>

## 트랜잭션의 특성 (ACID)

ACID(원자성, 일관성, 고립성, 지속성)는 

데이터베이스 트랜잭션이 안전하게 수행된다는 것을 보장하기 위한 성질을 가리키는 약어이다.

<br>

* 원자성(**A**tomicity): 트랜잭션이 데이터베이스에 모두 반영되던가, 아니면 전혀 반영되지 않아야 함 ex) 항공 티켓 주문
* 일관성(**C**onsistency): 트랜잭션이 실행을 성공적으로 완료하면 언제나 일관성 있는 데이터베이스 상태로 유지하는 것을 의미
* 격리성(**I**solation): 둘 이상의 트랜잭션이 동시에 실행되고 있을 경우, 어떤 트랜잭션이라도 다른 트랜잭션의 연산에 끼어들 수 없음
* 영구성(**D**urability): 트랜잭션이 성공적으로 완료됬을 경우, 결과는 영구적으로 반영되어야 한다는 점





<br> <br> <br>

## 트랜잭션 로그

모든 트랜잭션과 관련된 로그는 트랜잭션 로그 파일에 기록된다.

`데이터 일관성 유지` , `데이터베이스 복구 가능` 을 위함

<br>

#### Roll Back 이란 ?
~~~
데이터 변경이 가해지는 쿼리가 실행 되면 트랜잭션 로그에 기록된다. 
그런데 해당 트랜잭션이 완전히 끝나지 못하게 되면, 해당 작업은 변경 전 상태로 되돌아간다.
~~~

<br>

#### Roll Forward 란 ?
~~~
트랜잭션 로그에는 데이터 변경 처리가 완벽히 끝난 것으로 기록되어 있으나 
해당 내용이 데이터 파일에 미처 반영되지 못했을 때 
트랜잭션 로그 내용을 참조해 데이터 변경 작업이 실제 데이터 파일에 반영된다.
~~~

<br>

* 트랜잭션 로그 예시
    ![](https://t1.daumcdn.net/cfile/tistory/2641B83C578471C915)
    ```
    1번 트랜잭션은 체크포인트 전에 완전히 끝났기 때문에 트랜잭션의 모든 내용이 실제 데이터 파일에 기록되었다.
    따라서 요구되는 복구 작업이 없다.
    ```
    ```
    2번 트랜잭션은 트랜잭션 진행 중간에 체크포인트를 한 번 만났고 시스템 장애 전에 트랜잭션이 완료되었다.
    그래서 시스템 장애 후 다시 시작했을 때 Roll Forward하여 트랜잭션 로그 파일을 보고 실제 데이터 파일에 기록한다.
    ```
    ```
    3번 트랜잭션은 체크포인트를 거친 후 시스템 장애가 났을 때 트랜잭션이 완료되지 않았다.
    따라서 시스템을 재시작 하였을 때 Roll back되어 트랜잭션 수행 전 상태로 돌아간다.
    ```
    ```
    4번 트랜잭션은 실제 데이터 파일에 기록되지는 않았지만 시
    스템 장애 전에 트랜잭션이 완료되어 트랜잭션 로그 파일에 해당 기록이 남아있다. 
    따라서 시스템 재시작 후 Roll Forwrd 된다.
    ```
    ```
    5번 트랜잭션은 실제 데이터 파일에 기록되지도 않았고 
    시스템 장애 시 트랜잭션이 완료되지 않았기 때문에 복구할 작업이 없다.
    ```


<br><br><br>

## 트랜잭션 Lock

Lock이란 트랜잭션 처리의 순차성을 보장하기 위한 방법이다.

DBMS마다 Lock을 구현하는 방식과 세부적인 방법이 다를 수 있다.

Lock의 종류로는 **공유(Shared) Lock**과 **베타(Exclusive) Lock**이 있다. 

공유락은 다른 말로 **Read Lock**이라고 불리며 베타락은 **Write Lock**이라고도 불린다.

<br>

#### Lock의 종류
* 공유 잠금(Shared Lock) : Select
    ```
    공유 Lock은 데이터를 읽을 때 사용되어지는 Lock이다. 
    이런 공유 Lock은 공유 Lock 끼리는 동시에 접근이 가능하다. 
    즉, 하나의 데이터를 읽는 것은 여러 사용자가 동시에 할 수 있다는 것이다.
    하지만 공유 Lock이 설정된 데이터에 베타 Lock을 사용할 수는 없다.
    ```
* 배타적 잠금(Exclusive Lock) : Insert, Update, Delete
    ```
    베타 Lock은 데이터를 변경하고자 할 때 사용되며, 트랜잭션이 완료될 때까지 유지된다.
    베타락은 Lock이 해제될 때까지 다른 트랜잭션(읽기 포함)은 해당 리소스에 접근할 수 없다.
    또한 해당 Lock은 다른 트랜잭션이 수행되고 있는 데이터에 대해서는 접근하여 함께 Lock을 설정할 수 없다.
    ```

<br> <br>

#### Lock의 설정 범위(Level)

테이블과 행(row) 범위의 락 설정이 일반적으로 많이 쓰임

**1. 데이터베이스**
* 데이터베이스 범위의 lock은 전체 데이터베이스를 기준으로 lock 하는 것 즉, 1개의 세션만이 DB의 데이터에 접근이 가능
* 해당 기능은 일반적으로는 사용하지 않음 (DB의 소프트웨어 버전을 올린다던지 주요한 DB의 업데이트에 사용)

<br>

**2. 파일**
* 데이터베이스 파일을 기준으로 lock을 설정. 
* 파일 이란 테이블, row 등과 같은 실제 데이터가 쓰여지는 물리적인 저장소
* 해당 범위의 Lock은 잘 사용되지는 않음

<br>

**3. 테이블**
* 테이블 수준의 Lock은 테이블을 기준으로 Lock을 설정
* 이는 테이블의 모든 행을 업데이트 하는 등의 전체 테이블에 영향을 주는 변경을 수행할 때 유용
* 즉, DDL구문과 함께 사용되며 DDL Lock이라고도 한다.
* DDL은 데이터 구조를 정의하는데 사용되는 명령어임. (Create, Alter, Drop, Rename, Truncate)

<br>

**4. 페이지와 블럭**
* 파일의 일부인 페이지와 블록을 기준으로 Lock을 설정합니다. 잘 사용되지는 않음

<br>

**5. 컬럼**
* 컬럼 기준의 Lock은 컬럼을 기준으로 Lock을 설정할 수 있음
* 하지만 이 형식은 Lock 설정 및 해제의 리소스가 많이 들기 때문에 일반적으로 사용되지는 않음
* 지원하는 DBMS도 많지 않음

<br>

**6. 행(Row)**
* 행 수준의 Lock은 1개의 행(Row)를 기준으로 Lock을 설정
* DML에 대한 Lock으로 **가장 일반적으로 사용하는 Lock**입니다.
* DML은 데이터를 조회하거나 검색하기 위한 명령어임. (Select, Insert, Update, Delete)

<br> <br>

#### 블로킹(Blocking)
~~~
블로킹은 Lock간(베타 - 베타, 베타 - 공유)의 경합이 발생하여 특정 Transaction이 작업을 진행하지 못하고 멈춰선 상태를 뜻함. 
공유락 끼리는 블로킹이 발생하지 않지만 베타락은 블로킹을 발생시킨다. 
블로킹을 해소하기 위해서는 이전의 트랜잭션이 완료(커밋 OR 롤백)되어야 한다. 
뒤에 들어온 트랜잭션은 이전 트랜잭션이 마무리되어야 이후 진행이 가능하며 이런 경합은 성능에 좋지 않은 영향을 미친다. 
따라서 경합을 최소화 할 필요가 있음
~~~





<br><br><br>

## 트랜잭션 격리수준 (Transaction Isolation Level)

트랜잭션 격리수준(isolation level)이란 

동시에 여러 트랜잭션이 처리될 때, 트랜잭션끼리 얼마나 서로 고립되어 있는지를 나타내는 것

* 개별 트랜젝션이 독립되려면?
한 트랜젝션이 있을때 그 트랜젝션내에서 변경된 내용만을 다루어야 함
다른 트랜젝션에 의해 변경된 데이터에 대해서는 영향을 받지 않아야 함

* 동시에 여러 트랜젝션이 처리될 때 독립성or격리성에 대한 단계를 나눈것


#### 격리 수준
* 격리 수준은 크게 4가지로 나뉜다.
* 아래로 내려갈수록 트랜잭션간 고립 정도가 높아지며, 성능이 떨어지는 것이 일반적이다.
* 일반적인 온라인 서비스에서는 READ COMMITTED나 REPEATABLE READ 중 하나를 사용한다.
    (oracle = READ COMMITTED, mysql = REPEATABLE READ)

1. READ UNCOMMITTED
2. READ COMMITTED
3. REPEATABLE READ
4. SERIALIZABLE

<br> <br>

#### Dirty Read, Non-Repeatable Reads, Phantom Reads

1. Dirty Read
READ UNCOMMITED 상황에서 발생할 수 있는 문제.
커밋되지 않은 수정중인 데이터를 다른 트랜젝션에서 읽을때 발생한다.
Dirty Read 예시
    1. `트랜젝션A`의 격리수준이 READ UNCOMMITED일때
    2. `트랜젝션A`에서 사원1의 이름을 Jack에서 Tom으로 바꿈
    3. `트랜젝션B`에서 사원1의 이름을 조회하면 Tom이 조회됨
        > `트랜젝션A`에서 변경사항을 커밋하지 않았음에도 격리수준에 의해 `트랜젝션B`에서 변경된 내용이 출력됨
    이를 더티 리드(Dirty Read)라고 한다
    `트랜젝션A`에서 문제가 발생해 사원1의 데이터가 Rollback이 되어도
    `트랜젝션B`에서는 이전에 조회한 Tom으로 로직을 수행하기 때문에 논리적 오류가 발생할 수 있는 문제가 있음

<br>

2. Non-Repeatable Reads
한 트랜젝션내에서 같은 쿼리를 2번 수행할때, 
한번의 쿼리 수행후 다른 트랜젝션이 값을 수정하거나 삭제하면 2번째 쿼리는 앞의 쿼리와는 다른 결과를 반환할 수 있으므로
일관되지 않은 상황이 발생되는 것

<br>

3. Phantom Reads
한 트랜젝션에서 일정한 범위의 레코드를 여러번 읽어 올때
첫번째 쿼리에서는 없던 유령의 레코드가 두번째 쿼리에서 나타나는 현상

<br> <br>

#### READ UNCOMMITTED
어떤 트랜잭션의 변경내용이 COMMIT이나 ROLLBACK과 상관없이 다른 트랜잭션에서 보여진다.
한 트랜젝션에 의해 바뀐 데이터가 커밋이 되지 않아도 다른 트랜젝션에서 그냥 그대로 읽어올 수 있는 것

<br>

#### READ COMMITTED
어떤 트랜젝션에 의해 바뀐 데이터중 Commit이 확정된 데이터만 다른 트랜젝션에서 조회할 수 있음

<br>

#### REPEATABLE READ
먼저 발생한 트랜젝션이 읽은 데이터를 다른 트랜젝션에서 **업데이트**하거나 **삭제**할 수 없도록 방지
같은 트랜젝션 내에서 쿼리를 여러번 날려도 일관성이 있는 결과 반환을 기대할 수 있음

<br>

#### SERIALIZABLE
REPEATABLE READ와 동일하지만 업데이트와 삭제에 더하여 추가(insert)까지 방지해 줌
따라서 완벽하게 트랜젝션 read에 대한 일관성을 보장해 줄 수 있음

<br>

#### (추가내용)Isolation.DEFAULT
**Spring Framework**에서 Isolation.DEFAULT라는 격리도 추가로 제공하는데
사용하는 RDBMS에서 설정한 Isolation Level을 따르게 해줌

![](https://miro.medium.com/max/1400/1*UJQm5Oze6e9pgZxaK1xaBg.png)


<br><br>