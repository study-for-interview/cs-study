# Hash Table

## 해시(Hash)/해시 함수(Hash Function)/해싱(Hashing)?

해시(Hash) 란 데이터를 다루는 기법 중 하나이며,**해시 함수(Hash Function)** 는 데이터를 효율적으로 관리하기 위해서 임의의 길이의 데이터를 고정된 길이의 데이터로 매핑하는 함수이다.

매핑전 원래 데이터의 값을 **키(key)**, 매핑 후 데이터의 값을 **해시값(Hash Value) 또는 해시코드** 라고 하며, 키(key)와 값(value)으로 매핑되는 과정 자체를 **해싱(Hashing)** 이라고 한다.

## 해시 테이블(Hash Table)

해시 테이블(Hash Table) 은 키(key)와 값(value)이 하나의 쌍을 이루는 데이터 구조이다.

즉, 키(key)와 배열의 인덱스(index)를 이용하여 키를 저장하는 자료구조이다. 해시 테이블은 해시 맵, 맵, 딕셔너리, 연관 배열 이라는 이름으로 알려져있다.

해시 테이블은 키를 **해시 함수(hash function)** 로 계산하여 그 값을 배열의 인덱스로 사용한다. 

이때, 해시 함수에 의해 반환된 데이터의 고유 숫자 값을 **해시값 또는 해시코드** 라고 한다. 

즉, key 값을 해시 함수를 통해서 배열의 인덱스로 바꿔주고, 그 자리에 데이터를 저장한다. 정리하면 다음과 같다.
```
원래 데이터의 값(Key) -> Hash Function -> Hash Function의 결과 = Hash Code
-> Hash Code를 배열의 Index 로 사용 -> 해당하는 Index에 data 넣기
```

## 예시)

이름을 키(key)로 하여 번호를 저장하는 해시 테이블은 다음과 같이 만들 수 있다. 전체 데이터 양을 10이라고 하면 John의 데이터를 저장할 때, 배열의 인덱스는 hashFunction("John") % 10을 통해 인덱스 값을 계산한다. 여기서는 인덱스 값은 2이다.
![image](https://upload.wikimedia.org/wikipedia/commons/thumb/7/7d/Hash_table_3_1_1_0_1_0_0_SP.svg/1280px-Hash_table_3_1_1_0_1_0_0_SP.svg.png)

이런식으로 데이터를 저장하다 보면 계산된 인덱스 값이 중복될 수가 있다. 예를 들어 저장하고자 하는 키가 정수이고 hash_function이key%10이다. 

전체 사이즈가10일때, key 1,11,21은 같은 인덱스 값을 가지게 된다. 충돌 (collision) 이라고한다.

![image](https://upload.wikimedia.org/wikipedia/commons/thumb/d/d0/Hash_table_5_0_1_1_1_1_1_LL.svg/1280px-Hash_table_5_0_1_1_1_1_1_LL.svg.png)

## 충돌(Collision)

충돌(Collision) 은 서로 다른 문자열이 Hash function을 통해 Hash 한 결과가 같은 경우 (중복되는 경우)이다.

충돌을 줄여주는 좋은 해시 함수를 사용하는 것이 좋다. 왜냐하면 충돌이 많아질 수록 탐색의 시간 복잡도가 O(1)에서 O(n)에 가까워지기 때문이다. 해결 방법은 다음과 같다.
- Separating Chaining - Linked List, Tree(Red-Black Tree)
- Open addressing - Linear Probing, Quadratic Probing, Double hashing

## 분리 연결법(Separating Chaining)
Separate Chaining이란 동일한 버킷의 데이터에 대해 자료구조를 활용해 추가 메모리를 사용하여 다음 데이터의 주소를 저장하는 것이다. 위의 그림과 같이 동일한 버킷으로 접근을 한다면 데이터들을 연결을 해서 관리해주고 있다. 실제로 Java8의 Hash테이블은 Self-Balancing Binary Search Tree 자료구조를 사용해 Chaining 방식을 구현하였다.

이러한 Chaining 방식은 해시 테이블의 확장이 필요없고 간단하게 구현이 가능하며, 손쉽게 삭제할 수 있다는 장점이 있다. 하지만 데이터의 수가 많아지면 동일한 버킷에 chaining되는 데이터가 많아지며 그에 따라 캐시의 효율성이 감소한다는 단점이 있다.

##  개방 주소법(Open Addressing)

Open Addressing이란 추가적인 메모리를 사용하는 Chaining 방식과 다르게 비어있는 해시 테이블의 공간을 활용하는 방법이다. Open Addressing을 구현하기 위한 대표적인 방법으로는 3가지 방식이 존재한다.

1. 선형 탐사(Linear Probing): 현재의 버킷 index로부터 고정폭 만큼씩 이동하여 차례대로 검색해 비어 있는 버킷에 데이터를 저장한다.

2. 제곱 탐사(Quadratic Probing): 해시의 저장순서 폭을 제곱으로 저장하는 방식이다. 예를 들어 처음 충돌이 발생한 경우에는 1만큼 이동하고 그 다음 계속 충돌이 발생하면 2^2, 3^2 칸씩 옮기는 방식이다.

3. 이중 해싱(Double Hashing Probing): 해시된 값을 한번 더 해싱하여 해시의 규칙성을 없애버리는 방식이다. 해시된 값을 한번 더 해싱하여 새로운 주소를 할당하기 때문에 다른 방법들보다 많은 연산을 하게 된다.

Open Addressing에서 데이터를 삭제하면 삭제된 공간은 Dummy Space로 활용되는데, 그렇기 때문에 Hash Table을 재정리 해주는 작업이 필요하다고 한다.

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FWR1fv%2FbtqL5APCcSa%2FBZN6wvxUXzJBEiOfOMLfR0%2Fimg.png)

## 리사이징(Resizing)
Separate changing에 경우, 버킷이 일정 수준으로 차 버리면 각 버킷에 연결되어 있는 List의 길이가 늘어나기 때문에, 검색 성능이 떨어지기 때문에 버킷의 개수를 늘려줘야 한다. 

또한 Open addressing의 경우, 고정 크기 배열을 사용하기 때문에 데이터를 더 넣기 위해서는 배열을 확장해야 한다. 이를 리사이징(Resizing)이라고 한다.

보통 두 배로 확장하는데, 확장하는 임계점은 현재 데이터 개수가 해시 버킷의 개수의 75%가 될 때이다. 

0.75라는 숫자는 load factor 라고 불린다. 리사이징은 더 큰 버킷을 가지는 array를 새로 만든 다음에, 다시 새로운 array에 hash를 다시 계산해서 복사해줘야 한다.

## 해시 테이블의 장점
- 적은 리소스로 많은 데이터를 효율적으로 관리할 수 있다.
    - 예) HDD, Cloud에 존재하는 많은 데이터들을 유한한 개의 해시(Hash)값으로 매핑하여 작은 크기의 캐쉬 메모리로 프로세스 관리가 가능하다.

- 배열의 인덱스(index)를 사용해서 검색, 삽입, 삭제가 빠르다. (평균 시간복잡도 : O(1))
    - 인덱스를 사용해서 배열의 검색이 빠르다는 것은 당연한 소리이다. 하지만 삽입, 삭제는 왜 O(1)인가?
    - 여기서의 인덱스는 데이터만의 고유한 위치이기 때문에 만약 삽입이나 삭제를 한다고 해도 다른 데이터로 채울 필요가 없다. 즉, 삽입이나 삭제할 때 데이터를 이동할 필요가 없기 때문이다.

- 키(key)와 해시값(Hash)이 연관성이 없어 보안에도 많이 사용된다.

- 데이터 캐싱(Data Caching)에 많이 사용된다.
    - get(key), put(key)에 캐시 로직을 추가하면 자주 hit하는 데이터를 바로 찾을 수 있다.

- 중복을 제거하는데 유용하다.

## 해시 테이블의 단점
- 충돌
- 공간 복잡도가 커진다.
- 순서가 있는 배열에는 어울리지 않는다.
- 해시 함수 의존도가 높아진다.

## 해시테이블 시간 복잡도

키값이 배열의 인덱스로 변환되기 때문에 탐색,저장,삭제가 빠르다. 평균 시간 복잡도가 O(1)이다.


||평균적인 경우|최악의 경우|
|---|---|---|
|탐색|	O(1)|	O(N)|
|삽입|	O(1)|	O(N)|
|삭제|	O(1)|   O(N)|

## HashMap, HashTable, ConcurrentHashMap

위에 나열된 클래스들은 Map 인터페이스를 구현한 콜렉션들입니다. 이 콜렉션들은 비슷한 역할을 하는것 같으면서도 다르게 구현되어 있습니다. 기본적으로 Map 인터페이스를 구축한다면 <key, value>구조를 가지게 됩니다.

- Hashtable
    - Hashtable은 put, get과 같은 주요 메소드에 synchronized 키워드가 선언 되어 있습니다. 또한 key, value에 null을 허용하지 않습니다.
    - HashTable은 동기화를 위해 synchronized 키워드를 이용해서 메서드 전체에 락을 겁니다. 이 방법은 편하고 안전한 반면에 Scalability(확장성)가 떨어집니다.

**자바에서 Hashtable 주요 메서드인 get 코드**

메서드 전체에 synchronized를 이용해서 락을 건다.

![image](https://user-images.githubusercontent.com/47075043/154895652-912ae1e6-2765-40d5-b084-365ec451608f.png)



- HashMap
    - HashMap은 주요 메소드에 synchronized 키워드가 없습니다. 또한 Hashtable과 다르게 key, value에 null을 입력할 수 있습니다.

- ConcurrentHashMap
    - HashMap을 thread-safe 하도록 만든 클래스가 ConcurrentHashMap입니다. 하지만 HashMap과는 다르게 key, value에 null을 허용하지 않습니다.
    - ConcurrentHashMap은 내부적으로 여러 개의 세그먼트를 두고 각 세그먼트마다 별도의 락을 가지고 있습니다.

**자바에서 ConcurrentHashMap 주요 메서드 중 하나인 putVal 코드**

메서드 전체가 아닌 일부분에 synchronized를 이용해서 락을 건다.

![image](https://user-images.githubusercontent.com/47075043/154896517-5bcbe017-1f50-4245-aa9c-2bd852c6c292.png)

## 결론

|| 	Hashtable	|HashMap	|ConcurrentHashMap|
|---|---|---|---|
|thread-safe(synchronized)|	O|	X|	O|
|반환값	|Enumeration|	Fail-Fast Iterator|	Fail-Safe Iterator|
|성능 순위|	3|	1|	2|
|key, value에 null 허용|	X|	O|	X|
|사용할 상황|	X	|단일 스레드에서만 map을 사용하는 경우|	멀티 스레드 환경에서 map을 사용하는 경우|

MultiThread 환경에서 동기화 처리가 필요하다면 ConcurrentHashMap을 사용하는 것이 안정적이다. 동기화가 필요하지 않은 경우라면 그냥 HashMap을 사용하자. Hashtable은 Thread-Safe 하긴 하나 느리다는 단점이 있다.

참고 : 

https://hee96-story.tistory.com/48

https://mangkyu.tistory.com/102 

https://www.youtube.com/watch?v=n3qKw8OVnaY

https://j-i-y-u.tistory.com/30

https://118k.tistory.com/656
