# index

인덱스는 데이터베이스 테이블에 대한 검색 성능의 속도를 높여주는 자료 구조입니다. 

만약 우리가 책에서 원하는 내용을 찾는다고 하면, 책의 모든 페이지를 찾아 보는것은 오랜 시간이 걸린다. 그렇기 때문에 책의 저자들은 책의 맨 앞 또는 맨 뒤에 색인을 추가하는데, 데이터베이스의 index는 책의 색인과 같다.

데이터베이스에서도 테이블의 모든 데이터를 검색하면 시간이 오래 걸리기 때문에 데이터와 데이터의 위치를 포함한 자료구조를 생성하여 빠르게 조회할 수 있도록 돕고 있다.

인덱스를 활용하면, 데이터를 조회하는 SELECT 외에도 UPDATE나 DELETE의 성능이 함께 향상된다. 그러한 이유는 해당 연산을 수행하려면 해당 대상을 조회해야만 작업을 할 수 있기 때문이다.


# 인덱스(index)의 장단점 

장점
- 테이블을 조회하는 속도와 그에 따른 성능을 향상시킬 수 있다.
- 전반적인 시스템의 부하를 줄일 수 있다.

단점
- 인덱스를 관리하기 위해 DB의 약 10%에 해당하는 저장공간이 필요하다.
- 인덱스를 관리하기 위해 추가 작업이 필요하다.
- 인덱스를 잘못 사용할 경우 오히려 성능이 저하되는 역효과가 발생할 수 있다.

만약 CREATE, DELETE, UPDATE가 빈번한 속성에 인덱스를 걸게 되면 인덱스의 크기가 비대해져서 성능이 오히려 저하되는 역효과가 발생할 수 있다. 

그러한 이유 중 하나는 DELETE와 UPDATE 연산 때문이다. 

앞에서 설명한대로, UPDATE와 DELETE는 기존의 인덱스를 삭제하지 않고 '사용하지 않음' 처리를 해준다고 하였다. 

만약 어떤 테이블에 UPDATE와 DELETE가 빈번하게 발생된다면 실제 데이터는 10만건이지만 인덱스는 100만 건이 넘어가게 되어, SQL문 처리 시 비대해진 인덱스에 의해 오히려 성능이 떨어지게 될 것이다.

# 인덱스 자료구조

## 해시 테이블(hash table)

해시 테이블은 (Key, Value)로 데이터를 저장하는 자료구조 중 하나로 빠른 데이터 검색이 필요할 때 유용하다. 

해시 테이블은 Key값을 이용해 고유한 index를 생성하여 그 index에 저장된 값을 꺼내오는 구조이다.

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FRpMoO%2FbtqKMzdg9TX%2FXYkGt2kqE0hr9rqhHx3o3K%2Fimg.png)

해시 테이블을 사용하는 db 인덱스는 값이 1이라도 달라지면 완전 다른 해시 값을 생성하게 되는데, 해시가 등호(=) 연산에만 특화되고 부등호( < , > ) 연산이 자주 사용되는 데이터베이스 검색을 위해서는 해시 테이블이 적합하지 않다.

예를 들어 "나는"으로 시작하는 모든 데이터를 검색하기 위한 쿼리문은 인덱스의 혜택을 전혀 받지 못하게 된다. 이러한 이유로 데이터베이스의 인덱스에서는 B+Tree가 일반적으로 사용된다.

## B+Tree

B+Tree는 DB의 인덱스를 위해 자식 노드가 2개 이상인 B-Tree를 개선시킨 자료구조이다. B+Tree는 모든 노드에 데이터(Value)를 저장했던 BTree와 다른 특성을 가지고 있다.

- 리프노드(데이터노드)만 인덱스와 함께 데이터(Value)를 가지고 있고, 나머지 노드(인덱스노드)들은 데이터를 위한 인덱스(Key)만을 갖는다.

- 리프노드들은 LinkedList로 연결되어 있다.

- 데이터 노드 크기는 인덱스 노드의 크기와 같지 않아도 된다.


데이터베이스의 인덱스 컬럼은 부등호를 이용한 순차 검색 연산이 자주 발생될 수 있다. 

이러한 이유로 BTree의 리프노드들을 LinkedList로 연결하여 순차검색을 용이하게 하는 등 BTree를 인덱스에 맞게 최적화하였다. (물론 Best Case에 대해 리프노드까지 가지 않아도 탐색할 수 있는 BTree에 비해 무조건 리프노드까지 가야한다는 단점도 있다.)

이러한 이유로 비록 B+Tree는 O(log2n) 의 시간복잡도를 갖지만 해시테이블보다 인덱싱에 더욱 적합한 자료구조가 되었다.

# Primary Index vs Secondary Index

# Clustered index, Non-Clustered index

Database에서 index의 구조는 크게 Clustered 와 NonClustered로 나뉜다. 

## Clustered

클러스터 형 인덱스는 데이터가 테이블에 물리적으로 저장 되는 순서를 정의(설정)한다.

즉, 클러스터 형 인덱스는 특정 컬럼을 기준으로 데이터들을 정렬시킨다. 

아래 테이블은 id가 클러스터 형 인덱스로 지정되었으며, id 값을 기준으로 데이터들이 정렬되어있는 것을 확인할 수 있다.

![image](https://user-images.githubusercontent.com/49560745/107177426-2c98c900-6a15-11eb-9c47-087fc3212da1.png)

테이블 데이터는 오직 한 가지의 방법으로만 정렬되기 때문에 오직 테이블 당 하나의 클러스터 형 인덱스만 존재할 수 있다. 즉, 정렬 기준으로 오직 하나의 컬럼만을 선택할 수 있다.

Database에서 primary key의 제약조건(constraint)은 클러스터 된 인덱스를 자동으로 생성하기 때문에 우리가 일반적으로 테이블을 생성할 때 특정 컬럼에 primary key를 지정했다면, 자료가 자동으로 정렬되는 것이다.

primary key를 설정하지 않은 테이블에 무작위로 데이터를 insert하고, 테이블을 조회하면 뒤죽박죽인 테이블을 보게될 것이다.

## 그래서 왜 Clustered 인가 ?Permalink

위 테이블에 Name : 넬 , Birth : 1980 데이터를 ID : 2  에 추가한다면, 테이블의 상태는 아래와 같을 것이다.

![image](https://user-images.githubusercontent.com/49560745/107177819-150e1000-6a16-11eb-8792-0ede78e71ecb.png)

이것이 바로 Clustered이다. 순서는 오직 하나의 컬럼으로 결정되기 때문에 중간에 새로운 데이터가 삽입된다면 이후의 모든 컬럼을 한 칸씩 이동시켜줘야한다. index가 군집화 되어있기 때문이다.

만약, id : 2 이후에 만개 혹은 그 이상의 데이터가 있다고 생각해보자. Insert 에 소모되는 비용이 어마어마할 것이다. 그렇기 때문에 Primary Key 값을 어떤 컬럼으로 선택하는가에 따라 Database의 성능이 좌우된다.

이처럼 Clustered index는 검색 속도를 향상시킨다는 장점이 있지만, 새로운 데이터를 삽입할 때는 많은 비용이 소모되는 단점 또한 존재한다.

## Clustered 인덱스의 구조

![image](https://user-images.githubusercontent.com/49560745/107186321-6246ad80-6a27-11eb-9025-9714c451189e.png)

Clustered 인덱스의 구조이다. Data Page 의 데이터들이 순차적으로 정렬되어있다. 그리고 Leaf level 과 DataPage가 동일한 구조를 갖는다.

클러스터드 인덱스는 어떤경우 사용 해야 할까?
- 테이블 데이터가 자주 업데이트 되지 않는 경우

- 항상 정렬 된 방식으로 데이터를 반환해야하는 경우
    - 테이블은 정렬되어있기 때문에 ORDER BY 절을 활용해 모든 테이블 데이터를 스캔하지 않고 원하는 데이터를 조회할 수 있다.

- 읽기 작업이 월등히 많은 경우, 이때 매우 빠르다.

[참고] Clustered는 pk 값으로 자동 생성되는 것과 별개로 설정을 통해 테이블내에서 원하는대로 생성할 수 있다.

예를들어, 위 테이블을 Birth를 기준으로 Clustered 인덱스를 생성한다면 결과는 아래와 같다.
![image](https://user-images.githubusercontent.com/49560745/107182509-3b38ad80-6a20-11eb-9bc1-510a147c0836.png)

## Non-Clustered index

논 클러스터 형 인덱스는 말 그대로 클러스터 형의 반대인 군집화 되어있지 않은 인덱스 타입이다. 

그렇기 때문에 테이블에 저장 된 물리적인 순서에 따라 데이터를 정렬하지 않는다. 즉, 순서대로 정렬되어 있지 않다.

그리고 논 클러스터 형 인덱스는 테이블 데이터와 함께 테이블에 저장되는 것이 아니라 별도의 장소에 저장된다. 마치, 위 책에서 index 페이지를 따로 나눈것 처럼 말이다. 그뿐만 아니라 하나의 테이블에 여러개의 논 클러스터 형 인덱스를 설정할 수 있다.

논 클러스터 형의 예시는 아래와 같다. NonClustered 인덱스는 데이터의 행에 독립적이며, 인덱스 키 값과 데이터 행을 가리키는 포인터가 존재한다.

![image](https://user-images.githubusercontent.com/49560745/107178655-f446ba00-6a17-11eb-8f5d-06217ad3d901.png)

테이블의 ID 키 값과 포인터인 Address를 통해 실제 데이터에 접근한다.

ID : 4 에 해당하는 가수의 이름을 알고 싶다면, 120번지로 이동하고, Name을 확인하면 된다. 그림에서 볼 수 있듯이 Clustered와의 차이는 순차적으로 index가 정렬되었지 않다는 점이다.

## Non-Clustered 인덱스의 구조

![image](https://user-images.githubusercontent.com/49560745/107187245-0bda6e80-6a29-11eb-8053-9f7e8de7a9c9.png)

Non-Clustered 인덱스의 구조이다. Clustured 구조와는 다르게 Leaf Level과 Data Page가 구분된다. 그리고 Data Page의 데이터는 정렬 되어있지 않다.

어떤 경우에 생성해야할까?

- where절이나 Join 절과 같이 조건문을 활용하여 테이블을 필터링 하고자할 때
- 데이터가 자주 업데이트 될 때
- 특정 컬럼이 쿼리에서 자주사용 될 때

## 요약

|Clustered|	Non-Clustered|
|---|---|
|항상 순서를 유지한다	|순서와 상관 없다|
|한 테이블당 하나만 존재한다 (테이블 인덱스)	|한 테이블에 여러개 생성할 수 있다
|범위 검색에 유리하다 (군집화!)	|index를 저장할 추가적인 공간이 필요하다|
|데이터가 많아 질수록 Insert 성능이 나빠진다	|Insert시 추가 작업 (인덱스 생성) 필요하다|

- Clustered 인덱스는 테이블당 오직 한개만 존재한다. 반면에 Non-Clustered 형은 테이블 당 여러개의 인덱스를 생성할 수 있다.

- Clustered 인덱스는 오직 테이블을 정렬한다. 그러므로 별도의 공간을 필요로하지 않는다. Non-Clustered 인덱스는 저장되는 별도의 공간(약 10%)이 필요하다.

- Clustered 인덱스는 통상적으로 데이터를 찾는데 추가적인 스텝을 거치지 않기 때문에 Non-Clustered 인덱스보다 속도가 빠르다.

- Clustered 인덱스는 데이터를 삽입할 때, 모든 테이블에 존재하는 데이터들의 순서를 유지해야하므로 많은 비용이 발생한다. Non-Clustered는 별도의 공간에 인덱스를 생성해야하기 때문에 추가작업이 필요하다.

# Composite Index(결합 인덱스)

결합 인덱스란 인덱스를 생성할 때 두 개 이상의 컬럼을 합쳐서 인덱스를 만드는 것을 말합니다.

주로 단일 컬럼으로는 나쁜 분포도를 가지지만 여러 개의 컬럼을 합친다면 좋은 분포도를 가지고, Where절에서 AND 조건에 많이 사용되는 컬럼들을 결합 인덱스로 구성합니다.

## 결합 인덱스 컬럼 선택

1. where절에서 and 조건으로 자주 결합되어 사용되면서 각각의 분포도 보다 두 개 이상의 컬럼이 결합될 때 분포도가 좋아지는 컬럼들 

2. 다른 테이블과 조인의 연결고리로 자주 사용되는 컬럼들

3. order by에서 자주 사용되는 컬럼들

4. 하나 이상의 키 컬럼 조건으로 같은 테이블의 컬럼들이 자주 조회될 때

## 결합 인덱스의 컬럼 순서 결정
결합 인덱스를 만들 때 결합 인덱스를 구성하는 컬럼들의 배열 순서는 아주 중요하기에 신중하게 결정하여야 합니다. 

컬럼의 순서를 잘못 배열하면 결합 인덱스의 발동 확률이 매우 낮아질 수 있기 때문입니다. 

만약 select 문의 where절에 결합 인덱스의 첫 번째 컬럼을 조건에 사용하였다면 그 질의문은 결합 인덱스를 사용할 수 있습니다. 

하지만 개발자가 결합 인덱스의 두번째 컬럼만을 where 절에 조건으로 사용하고 결합 인덱스를 사용하고자 했다면 실행계획은 인덱스를 사용하지 못합니다. 

따라서 쿼리문 작성 시 결합 인덱스를 사용하고자 한다면 반드시 결합 인덱스의 컬럼 중 선행하는 컬럼부터 조건에 지정하여 사용하여야 합니다. 

조건은 컬럼 전체를 순서대로 사용할 수도 있고, 아니면 선행하는 일부 컬럼을 순서대로 사용할 수 있습니다. 

### 결합 인덱스 컬럼의 설정 시 고려해야 할 우선순위
1. where절 조건에 많이 사용되는 컬럼이 우선시

2. Equal('=')로 사용되는 컬럼 우선

3. 분포도가 좋은 컬럼을 우선

4. 자주 이용되는 순서대로 결합 인덱스 컬럼의 순서 결정

## 결합 인덱스 사용 예시 

### 결합 인덱스 생성
```
create index emp_pay_idx on emp_pay(급여년월, 급여코드, 사원번호);
```
emp_pay 테이블에서 급여년월, 급여코드, 사원번호 컬럼으로 emp_pay_idx라는 결합 인덱스를 생성하였습니다.


### 결합 인덱스 사용

```
select * from emp_pay where 급여년월 = '202107';
select * from emp_pay where 급여년월 = '202107' and 급여코드 ='정기급여';
select * from emp_pay where 급여년월 = '202107' and 급여코드 = '정기급여' and 사원번호 = '20210401';
```

select 문장의 where 절에서는 다음과 같은 조건 조합에서 인덱스가 사용되게 됩니다.

### 결합 인덱스가 사용되지 않을 때

```
select * from emp_pay where 급여코드 = '정기급여';
select * from emp_pay where 사원번호 = '20210401';
select * from emp_pay where 사원번호 = '20210401' and 급여코드 = '정기급여';
```

위와 같이 where 조건문을 나열할 때 결합 인덱스의 첫 번째 컬럼인 급여년월의 조건식이 없으면 B*Tree 구조인 결합 인덱스를 검색할 수 없기 때문에 결합 인덱스가 무용지물이 되니 주의하여야 합니다.


---

 참고 : 

https://mangkyu.tistory.com/96

https://gwang920.github.io/database/clusterednonclustered/

https://coding-factory.tistory.com/755


