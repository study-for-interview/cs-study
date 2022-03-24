# 트랜잭션(Transaction)이란 무엇인가?
 
**트랜잭션(Transaction)은 데이터베이스에서의 논리적 작업 단위이다.**

하나의 작업을 수행하기 위해 필요한 데이터베이스 연산 기능들을 모아놓은 것이며 분리되지 않도록 하여 작업의 완전성을 보장한다. 

트랜잭션을 통해서 데이터베이스의 회복과 병행 제어가 가능하다. 즉, 데이터베이스에서 오류가 발생하는 경우의 빠른 회복이나, 여러 사용자가 동시에 데이터베이스를 사용할 수 있도록 제어해주는 중요한 역할을 한다.  

데이터베이스의 연산을 SQL문으로 표현한다면, 하나의 작업을 수행하는 SQL문의 집합으로 생각할 수도 있다. 

# 트랜잭션의 특성

트랜잭션이 성공적으로 처리되기 위해서는 ACID라는 네 가지 성질을 만족해야 한다. 
 
## 1. 원자성 (Automicity) 

트랜잭션을 구성하는 연산은 반드시 모두 실행이 되거나 혹은 아예 실행되지 않아야 한다. 즉, 하나의 트랜잭션에서 일부 연산만 실행되면 안 된다.

따라서 실행 도중에 오류가 발생하여 작업을 완료하지 못하였다면, 트랜잭션 전체를 취소하여 수행 이전으로 돌아가야 한다. 

## 2. 일관성 (Consistency)

트랜잭션이 완료된 상태에서도 트랜잭션 이전의 상황과 동일하게 데이터의 일관성이 있어야 한다. 데이터에 모순이 있어서는 안 된다. 

은행 송금 기능을 생각해보면, 트랜잭션 수행 이전의 송금자와 수금자의 잔액 합이 수행 후에 달라지거나, 혹은 잔액을 나타내는 자료형이 정수형에서 문자열로 바뀌는 등의 모순이 발생하면 안 된다. 

## 3. 독립성, 격리성 (Isolation)

트랜잭션은 다른 트랜잭션에 간섭을 주거나 받지 않고 독립적으로 수행되어야 한다. 

둘 이상의 트랜잭션이 병행 실행되는 경우, 현재 수행 중인 트랜잭션이 완료되기 전에 현재 트랜잭션이 생성한 중간 연산 결과를 다른 트랜잭션이 접근하면 안 된다. 

독립성을 통해서, 사용자들은 여러 트랜잭션이 동시에 수행되고 있는 것처럼 느끼면서도 정확한 결과를 얻을 수 있게 된다. 

## 4. 지속성 (Durability)

트랜잭션이 성공적으로 완료되었을 때 그 결과는 영구적으로 반영되어야 한다. 시스템의 장애가 발생하더라도 결과는 데이터베이스에 그대로 남아있어야 하며, 지속성을 보장하기 위해서 회복 기능이 필요하다. 


# 트랜잭션의 연산

트랜잭션의 연산으로는 크게 Commit과 Rollback 두 가지가 있다. 

### 1. Commit 연산

Commit 연산은 하나의 트랜잭션이 성공적으로 종료된 후, 데이터베이스가 일관된 상태를 유지할 때 갱신 연산이 완료되었다고 트랜잭션 관리자에게 알려주고 결과를 최종적으로 데이터베이스에 반영하는 연산이다. 

### 2. Rollback 연산

Rollback 연산은 하나의 트랜잭션이 비정상적으로 종료되어 데이터베이스의 일관성을 잃었을 때 트랜잭션이 지금까지 실행한 연산의 결과가 취소되고 트랜잭션 수행 이전의 상태로 돌아가는 연산이다. 

Rollback을 하는 경우엔 해당 트랜잭션을 재시작하거나 폐기한다. 

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcJP2nH%2FbtrbIemBsy1%2FyQkjAG5WfK7NtqS7vKfak1%2Fimg.png)

# 트랜잭션의 상태

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbbYMDH%2FbtrbOsjZF2N%2Fle9kHXH4DkZIb67wbfoFw0%2Fimg.png)

### 1. 활성화(Active) : 트랜잭션이 작업을 시작하여 실행 중인 상태

### 2. 실패(Failed) : 트랜잭션에 오류가 발생하여 실행이 중단된 상태

### 3. 철회(Aborted) : 트랜잭션이 비정상적으로 종료되어 Rollback 연산을 수행한 상태

### 4. 부분 완료(Partially commited) : 트랜잭션의 마지막 연산까지 실행하고 commit 요청이 들어온 직후의 상태. 최종 결과를 데이터베이스에 아직 반영하지 않은 상태.

### 5. 완료(Commited) : 트랜잭션이 성공적으로 종료되어 commit 연산을 실행한 후의 상태

# 트랙잭션 격리 수준
트랜잭션 격리수준(isolation level)이란 동시에 여러 트랜잭션이 처리될 때, 트랜잭션끼리 얼마나 서로 고립되어 있는지를 나타내는 것이다.

간단하게 말해 특정 트랜잭션이 다른 트랜잭션에 변경한 데이터를 볼 수 있도록 허용할지 말지를 결정하는 것이다.

격리수준은 크게 아래의 4개로 나뉜다.

- READ UNCOMMITTED
- READ COMMITTED
- REPEATABLE READ
- SERIALIZABLE

아래로 내려갈수록 트랜잭션간 고립 정도가 높아지며, 성능이 떨어지는 것이 일반적이다.
일반적인 온라인 서비스에서는 READ COMMITTED나 REPEATABLE READ 중 하나를 사용한다.
default (oracle = READ COMMITTED, mysql = REPEATABLE READ)

# READ UNCOMMITTED

- 각 트랜잭션에서의 변경 내용이 COMMIT이나 ROLLBACK 여부에 상관 없이 다른 트랜잭션에서 값을 읽을 수 있다.
- 정합성에 문제가 많은 격리 수준이기 때문에 사용하지 않는 것을 권장한다.
- 아래의 그림과 같이 Commit이 되지 않는 상태지만 Update된 값을 다른 트랜잭션에서 읽을 수 있다.

![image](https://nesoy.github.io/assets/posts/img/2019-05-08-21-09-02.png)

### READ UNCOMMITTED 문제
 - DIRTY READ현상 발생할 수 있음
    - 트랜잭션이 작업이 완료되지 않았는데도 다른 트랜잭션에서 볼 수 있게 되는 현상

# READ COMMITTED
- RDB에서 대부분 기본적으로 사용되고 있는 격리 수준이다.
- Dirty Read와 같은 현상은 발생하지 않는다.

- 실제 테이블 값을 가져오는 것이 아니라 Undo 영역에 백업된 레코드에서 값을 가져온다.

![image](https://nesoy.github.io/assets/posts/img/2019-05-08-21-18-08.png)

### READ COMMITTED에서 발생할 수 있는 문제
![image](https://nesoy.github.io/assets/posts/img/2019-05-08-21-25-41.png)

- 트랜잭션-1이 Commit한 이후 아직 끝나지 않는 트랜잭션-2가 다시 테이블 값을 읽으면 값이 변경됨을 알 수 있다.
- 하나의 트랜잭션내에서 똑같은 SELECT 쿼리를 실행했을 때는 항상 같은 결과를 가져와야 하는 REPEATABLE READ의 정합성에 어긋난다.
- 이러한 문제는 주로 입금, 출금 처리가 진행되는 금전적인 처리에서 주로 발생한다.
    - 데이터의 정합성은 깨지고, 버그는 찾기 어려워 진다.

# REPEATABLE READ

- MySQL에서는 트랜잭션마다 트랜잭션 ID를 부여하여 트랜잭션 ID보다 작은 트랜잭션 번호에서 변경한 것만 읽게 된다.
- Undo 공간에 백업해두고 실제 레코드 값을 변경한다.
    - 백업된 데이터는 불필요하다고 판단하는 시점에 주기적으로 삭제한다.
    - Undo에 백업된 레코드가 많아지면 MySQL 서버의 처리 성능이 떨어질 수 있다.
- 이러한 변경방식은 MVCC(Multi Version Concurrency Control)라고 부른다.

![image](https://nesoy.github.io/assets/posts/img/2019-05-08-21-52-08.png)

# REPEATABLE READ에서 발생할 수 있는 문제

### 1. UPDATE 부정합

```sql
START TRANSACTION; -- transaction id : 1
SELECT * FROM Member WHERE name='junyoung';

    START TRANSACTION; -- transaction id : 2
    SELECT * FROM Member WHERE name = 'junyoung';
    UPDATE Member SET name = 'joont' WHERE name = 'junyoung';
    COMMIT;

UPDATE Member SET name = 'zion.t' WHERE name = 'junyoung'; -- 0 row(s) affected
COMMIT;
```
이 상황에서 최종 결과는 name = joont가 된다.

REPETABLE READ이기 때문에, 2번 트랜잭션에서 name = joont로 변경하고 COMMIT을 하면 name = junyoung의 내용을 언두로그에 남겨놔야 한다.

그래야 1번 트랜잭션에서 일관되게 데이터를 보는 것을 보장해줄 수 있기 때문이다.

이 상황에서 아래 구문에서 UPDATE 문을 실행하게 되는데, UPDATE의 경우 변경을 수행할 로우에 대해 잠금이 필요하다.

하지만 현재 1번 트랜잭션이 바라보고 있는 name = junyoung 의 경우 레코드 데이터가 아닌 언두영역의 데이터이고, 언두영역에 있는 데이터에 대해서는 쓰기 잠금을 걸 수가 없다.

그러므로 위의 UPDATE 구문은 레코드에 대해 쓰기 잠금을 시도하려고 하지만 name = junyoung인 레코드는 존재하지 않으므로, 0 row(s) affected가 출력되고, 아무 변경도 일어나지 않게 된다.

그러므로 최종적으로 결과는 name = joont가 된다. 자이언티로 바뀌지 않는다.

### 2. PHANTOM READ

- 한 트랜잭션 내에서 같은 쿼리를 두 번 실행했는데, 첫 번째 쿼리에서 없던 유령(Phantom) 레코드가 두 번째 쿼리에서 나타나는 현상을 말한다.
- 이를 방지하기 위해서는 쓰기 잠금을 걸어야 한다.

REPETABLE READ 이하에서만 발생하고(SERIALIZABLE은 발생하지 않음), INSERT에 대해서만 발생한다.
아래와 같은 상황에서 재현될 수 있다.    

```sql
START TRANSACTION; -- transaction id : 1 
SELECT * FROM Member; -- 0건 조회

    START TRANSACTION; -- transaction id : 2
    INSERT INTO MEMBER VALUES(1,'joont',28);
    COMMIT;

SELECT * FROM Member; -- 여전히 0건 조회 
UPDATE Member SET name = 'zion.t' WHERE id = 1; -- 1 row(s) affected
SELECT * FROM Member; -- 1건 조회 
COMMIT;
```
REPETABLE READ에 에 의하면 원래 출력되지 않아야 하는데 UPDATE 문의 영향을 받은 후 부터 출력된다.


![image](https://nesoy.github.io/assets/posts/img/2019-05-08-22-14-18.png)

# SERIALIZABLE
가장 단순하고 가장 엄격한 격리수준이다.

InnoDB에서 기본적으로 순수한 SELECT 작업은 아무런 잠금을 걸지않고 동작하는데,
격리수준이 SERIALIZABLE일 경우 읽기 작업에도 공유 잠금을 설정하게 되고, 이러면 동시에 다른 트랜잭션에서 이 레코드를 변경하지 못하게 된다.

이러한 특성 때문에 동시처리 능력이 다른 격리수준보다 떨어지고, 성능저하가 발생하게 된다.

# 트랜잭션과 Lock

MySQL에서 사용되는 잠금은 크게 **스토리지 엔진 레벨과 MySQL 엔진 레벨로** 나눠볼 수 있다. 

MySQL 엔진 레벨의 잠금은 모든 스토리지 엔진에 영향을 미치게 되지만 스토리지 엔진 레벨의 잠금은 스토리지 엔진 간 상호 영향을 미치지 않는다. 

- MySQL 엔진 레벨
    - 글로벌 락
    - 테이블 락
    - 메타데이터 락
    - 네임드 락 (유저 레벨 락)
- 스토리지 엔진 레벨(InnoDB)
    - 레코드 락
    - 갭 락
    - 넥스트 키 락
    - 자동 증가 락

## 글로벌 락 

FLUSH TABLES WITH READ LOCK 명령으로 획득할 수 있고, 가장 범위가 큰 잠금이다. 서버 전체에 영향을 미친다.

한 세션에서 글로벌 락을 획득하면 다른 세션에서 SELECT를 제외한 대부분의 DDL 문장이나 DML 문장을 실행하는 경우 글로벌 락이 해제될 때까지 대기 상태로 남는다.

### 백업 락

위 SQL문으로 실행된 글로벌 락은 READ LOCK을 모두 걸어버려서 모든 변경 작업을 멈추는데, InnoDB 스토리지 엔진의 트랜잭션 기능이 있기 때문에 굳이 변경을 막을 필요가 없다.

이는 뒤에서 설명이 되는 Transaction ID를 이용한 읽기로 다른 수정사항에 영향을 미치지 않는 것을 의미하는 것 같다.

위와 같은 상황에서 안정적인 백업을 위해 가벼운 글로벌 락인 백업 락을 도입했다.

데이터베이스 및 테이블 등 모든 객체 생성 및 변경, 삭제 불가 REPAIR TABLE과 OPTIMIZE TABLE 명령 불가 사용자 관리 및 비밀번호 변경 불가 일반적인 테이블의 데이터는 변경 가능 

### 백업(Backup) vs 복제(Replica)

백업과 복제 비슷한 개념이지만 다르다. 백업은 복제를 하는 행위, 데이터를 복구하기 위한 목적에 의미가 있으며, 복제는 소스 서버의 데이터를 또 다른 서버인 레플리카 서버에 복사하여 이전시키는 의미이다.

백업은 백업을 참조해 복구하는 용도, 복제는 그 자체를 쓰는 것.


## 테이블 락

테이블 락은 개별 테이블 단위로 설정되는 잠금이며, 명시적 방법, 묵시적 방법이 있다.

- 명시적 방법
    - LOCK TABLES table_name [ READ | WRITE ]명령으로 table_name테이블을 잠글 수 있다.
    - UNLOCK TABLES 명령으로 잠금을 하제할 수 있다.
- 묵시적 방법
    - 쿼리 실행 시 자동으로 잠금, 해제
    - MyISAM, MEMORY
        - 테이블의 데이터 변경
- InnoDB
    - InnoDB 테이블은 레코드 기반의 잠금을 제공하기 때문에 단순 데이터 변경 쿼리로는 테이블 락이 설정되지 않는다.
    - 스키마를 변경하는 DDL 쿼리의 경우에만 테이블 락이 설정된다.

## 네임드 락(유저 레벨 락)

GET_LOCK()함수를 이용해 임의의 문자열에 대해 잠금을 설정할 수 있다. 

자주 사용되지 않는 방식이며, DB 서버 1대에 5대의 웹 서버가 접속해서 서비스 하는 상황처럼 동기화 과정이 중요한 경우 네임드 락을 이용해 쉽게 처리 가능하다.

### 문자열로 잠금을 건다?
처음에는 문자열로 잠금을 건다는 것이 이해가 안됐다. 해당 문자열을 잠가서 막아버리는 것일까 생각했는데, 단순하게 문자열 자체에 의미를 두어 같은 상황을 만들지 않는 용도로 생각하게 됐다.

예를 들면 특정 유저가 동일 작업을 하는 것을 방지하기 위해 트랜잭션 시 GET_LOCK("user_name")으로 LOCK을 걸어 동일한 user는 해당 작업을 잠금시켜 버린다.

## 메타데이터 락

메타데이터 락은 데이터베이스 객체(테이블이나 뷰 등)의 이름이나 구조를 변경하는 경우에 획득하는 잠금이다. 

자동으로 획득, 해제하는 잠금이다. RENAME TABLE tab_a TO tab_b 같이 테이블의 이름을 변경하는 경우 자동으로 두 테이블 모두 잠금을 설정한다.

## 레코드락 

레코드 자체만을 잠그는 것이다. InnoDB 스토리지 엔진은 특이하게 레코드 자체가 아니라 인덱스의 레코드를 잠근다. 인덱스가 없는 테이블이더라도 내부적으로 자동 생성된 클러스터 인덱스를 이용해 설정한다.

- 보조 인덱스에 의한 변경 작업
    - 넥스트 키 락
    - 갭 락
- PK 또는 유니크 인덱스에 의한 변경 작업
    - 갭에 대해서 잠그지 않고 레코드 자체에 대해서만 잠금

## 갭 락

레코드와 바로 인접한 레코드 사이의 간격만을 잠그는 것이다. 

레코드와 레코드 사이의 간격에 새로운 레코드가 생성(INSERT)되는 것을 제어하는 것이다. 갭 락 그 자체보다는 넥스트 키 락의 일부로 자주 사용된다.

## 넥스트 키 락
레코드 락과 갭 락을 합쳐 놓은 형태의 잠금이다. 
STATEMENT 포맷의 바이너리 로그를 사용하는 MySQL 서버에서는 REPEATABLE READ 격리 수준을 사용해야 한다. 또한 innodb_locks_unsafe_for_binlog 시스템 변수가 비활성화(0)되면 변경을 위해 검색하는 레코드에는 넥스트 키 락 방식으로 잠금이 걸린다.

InnoDB의 갭 락이나 넥스트 키 락은 바이너리 로그에 기록되는 쿼리가 레플리카 서버에서 실행될 때 소스 서버에서 만들어낸 결과와 동일한 결과를 만들어 내도록 보장하는 것이 주목적이다.

의외로 이로 인해 데드락이나 블로킹이 자주 발생한다. 가능하다면 로그 포맷을 ROW 형태로 바꿔서 넥스트 키 락이나 갭 락을 줄이는 것이 좋다.

# db 충돌 개선 전략

database에 접근해서 데이터를 수정할 때 동시에 수정이 일어나 충돌이 일어날 수 있습니다. 우리는 이런 상황을 해결할 수 있도록 코딩을 진행해야합니다. 어떻게 해결할 수 있을까요 ?

첫번째, 테이블의 row에 접근시 Lock을 걸고 다른 Lock이 걸려 있지 않을 경우에만 수정을 가능하게 할 수 있습니다.

두번째, 수정할 때 내가 먼저 이 값을 수정했다고 명시하여 다른 사람이 동일한 조건으로 값을 수정할 수 없게 하는 것입니다.

## 비관적 락(pessimistic lock)

트랜잭션에서 변경하려는 레코드에 대해 락을 획득하고 쿼리를 수행하는 방식 (같은 레코드를 변경하려는 경우가 많을 것이라고 비관적인 생각을 하기 때문에 비관적 락)

비관적 락이란 트랜잭션이 시작될 때 Shared Lock 또는 Exclusive Lock을 걸고 시작하는 방법입니다. 

즉, Shared Lock을 걸게 되면 write를 하기위해서는 Exclucive Lock을 얻어야하는데 Shared Lock이 다른 트랜잭션에 의해서 걸려 있으면 해당 Lock을 얻지 못해서 업데이트를 할 수 없습니다. 

수정을 하기 위해서는 해당 트랜잭션을 제외한 모든 트랜잭션이 종료(commit) 되어야합니다.

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F5wxW6%2Fbtq9hyUsNAt%2FKtepF9HSKgm19t3G9RRoVK%2Fimg.png)

1. Transaction_1 에서 table의 Id 2번을 읽음 ( name = Karol )

2. Transaction_2 에서 table의 Id 2번을 읽음 ( name = Karol )

3. Transaction_2 에서 table의 Id 2번의 name을 Karol2로 변경 요청 ( name = Karol 
)

4. 하지만 Transaction 1에서 이미 shared Lock을 잡고 있기 때문에 Blocking

5. Transaction_1 에서 트랜잭션 해제 (commit)

6. Blocking 되어있었던 Transaction_2의 update 요청 정상 처리

이렇듯 Transaction을 이용하여 충돌을 예방하는 것이 바로 비관적 락(Pessimistic Lock)입니다.

## 낙관적 락(optimistic lock)
트랜잭션에서 락 없이 일단 쿼리 수행을 하고 마칠 때 서로 다른 트랜잭션에서 충돌이 있었는지 확인하고 문제가 있으면 충돌이 난 트랜잭션을 롤백하는 방식 (같은 레코드를 변경하려는 경우가 거의 없을 것이라고 낙관적인 생각을 하기 때문에 낙관적 락)

이 특징은 DB에서 제공해주는 특징을 이용하는 것이 아닌 Application Level에서 잡아주는 Lock입니다. 

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FINtDF%2Fbtq9hzFPQQU%2FIvsEoEH3yYXqL1irPPs4W1%2Fimg.png)


# 트랜잭션을 사용할 때 주의할 점

트랜잭션은 꼭 필요한 최소의 코드에만 적용하는 것이 좋다. 

즉 트랜잭션의 범위를 최소화하라는 의미다. 

일반적으로 데이터베이스 커넥션은 개수가 제한적이다. 

그런데 각 단위 프로그램이 커넥션을 소유하는 시간이 길어진다면 사용 가능한 여유 커넥션의 개수는 줄어들게 된다. 

그러다 어느 순간에는 각 단위 프로그램에서 커넥션을 가져가기 위해 기다려야 하는 상황이 발생할 수도 있는 것이다.

# 트랜잭션 전파

트랜잭션의 propagation 설정이란
```
Spring에서 사용하는 어노테이션 '@Transactional'은 해당 메서드를 하나의 트랜잭션 안에서 진행할 수 있도록 만들어주는 역할을 합니다. 

이때 트랜잭션 내부에서 트랜잭션을 또 호출한다면 스프링에서는 어떻게 처리하고 있을까요? 새로운 트랜잭션이 생성될 수도 있고, 이미 트랜잭션이 있다면 부모 트랜잭션에 합류할 수도 있을 것입니다. 

진행되고 있는 트랜잭션에서 다른 트랜잭션이 호출될 때 어떻게 처리할지 정하는 것을 '트랜잭션의 전파 설정'이라고 부릅니다.
```

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbAVbyb%2Fbtq7XrDkI2p%2F3EcaWlKwohOv0OOobFQL4K%2Fimg.png)

전파 설정 옵션

트랜잭션의 전파 설정은 '@Transactional'의 옵션 'propagation'을 통해 설정할 수 있습니다. 각 옵션은 아래와 같습니다.

## REQUIRED (기본값)

부모 트랜잭션이 존재한다면 부모 트랜잭션으로 합류합니다. 부모 트랜잭션이 없다면 새로운 트랜잭션을 생성합니다.

중간에 롤백이 발생한다면 모두 하나의 트랜잭션이기 때문에 진행사항이 모두 롤백됩니다.

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbkPsKW%2Fbtq7Xs3kagK%2Fz1O92fn0Spuik8MoT4nRA1%2Fimg.png)

## REQUIRES_NEW

무조건 새로운 트랜잭션을 생성합니다. 각각의 트랜잭션이 롤백되더라도 서로 영향을 주지 않습니다.

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbQ2CTZ%2Fbtq7Y4ATdH6%2F4fm4xVfiJHKSyL9u0KBnd0%2Fimg.png)

## MANDATORY

부모 트랜잭션에 합류합니다. 만약 부모 트랜잭션이 없다면 예외를 발생시킵니다.

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbwjNlq%2Fbtq7VxxwxpR%2FNI1gWSlnahZFbatww8Qwv1%2Fimg.png)

## NESTED

부모 트랜잭션이 존재한다면 중첩 트랜잭션을 생성합니다. 중첩된 트랜잭션 내부에서 롤백 발생시 해당 중첩 트랜잭션의 시작 지점 까지만 롤백됩니다. 중첩 트랜잭션은 부모 트랜잭션이 커밋될 때 같이 커밋됩니다.

부모 트랜잭션이 존재하지 않는다면 새로운 트랜잭션을 생성합니다.

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbMpI6s%2Fbtq7VXJujZK%2F7JpZ1DNEUr28PmrQ2lQsVK%2Fimg.png)

## NEVER

트랜잭션을 생성하지 않습니다. 부모 트랜잭션이 존재한다면 예외를 발생시킵니다.

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F6DNjl%2Fbtq7ZyIe9X3%2FsL2id4v3vko0QgsXpWs9j1%2Fimg.png)


## SUPPORTS

부모 트랜잭션이 있다면 합류합니다. 진행중인 부모 트랜잭션이 없다면 트랜잭션을 생성하지 않습니다.

## NOT_SUPPORTED

부모 트랜잭션이 있다면 보류시킵니다. 진행중인 부모 트랜잭션이 없다면 트랜잭션을 생성하지 않습니다.


---

참고 :

https://rebro.kr/162?category=484170

https://jeong-pro.tistory.com/241

https://joont92.github.io/db/%ED%8A%B8%EB%9E%9C%EC%9E%AD%EC%85%98-%EA%B2%A9%EB%A6%AC-%EC%88%98%EC%A4%80-isolation-level/

https://nesoy.github.io/articles/2019-05/Database-Transaction-isolation

https://velog.io/@fortice/MySQL-%ED%8A%B8%EB%9E%9C%EC%9E%AD%EC%85%98-%EC%9E%A0%EA%B8%88Lock#0-%EA%B3%B5%EC%9C%A0-%EC%9E%A0%EA%B8%88shared-lock--%EB%B2%A0%ED%83%80-%EC%9E%A0%EA%B8%88exclusive-lock

https://sabarada.tistory.com/175


