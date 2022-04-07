# hashcode() & equals()

## equals()

Object 클래스에서 equals 메서드는 두 객체가 동일한지 검사하기 위해 사용된다.

즉, 2개의 객체가 가리키는 곳이 동일한 메모리 주소일 경우에만 동일한 객체가 된다.

equals는 재정의하기 쉬워보이지만 곳곳에 함정이 있다. 문제를 회피하는 가장 쉬운 길은 아예 재정의하지 않는 것이다.


### equals를 재정의하지 않아야 할 상황

- 각 인스턴스가 본질적으로 고유할 때
- 인스턴스의 논리적 동치성(logical equality)를 검사할 일이 없을 때
- 상위 클래스에서 재정의한 equals가 하위 클래스에도 들어맞을 때
- 클래스가 private이거나 package-private이고 equals 메서드를 호출할 일이 없을 때


그렇다면 equals를 재정의해야 할 때는 언제일까?

객체 식별성(object identity: 두 객체가 물리적으로 같은가)이 아니라 논리적 동치성을 비교하도록 확인해야 하는데, 상위 클래스의 equals가 논리적 동치성을 비교하도록 재정의되지 않았을 때다(주로 값 클래스 ex)String ).



### equals 메서드를 재정의할 때 반드시 따라야 할 Object 명세에 적힌 equals 메서드의 일반 규약

- 반사성(reflexive) : null이 아닌 모든 참조 값x에 대해 x.equals(x)는 true다.
- 대칭성(symmetric) : null이 아닌 모든 참조 값 x,y에 대해, x.equals(y)가 true면 y.equals(x)도 true다.
- 추이성(transitive) : null이 아닌 모든 참조 값 x,y,z에 대해 x.equals(y)와 y.equals(z)가 true면 x.equals(z)도 true다.
- 일관성(consistent) : null이 아닌 모든 참조 값 x,y에 대해, x.equals(y)를 반복해서 호출하면 항상 true 이거나 항상 false 이다
- null-아님 : null이 아닌 모든 참조 값 x에 대해, x.equals(null)은 false다.

정리

- 꼭 필요한 경우가 아니면 equals를 재정의하지 말자.
- 많은 경우에 Object의 equals가 프로그래머가 원하는 비교를 정확히 수행해준다.
- 재정의해야 할 때는 그 클래스의 핵심 필드 모두를 빠짐없이, 다섯 가지 규약을 확실히 지켜가며 비교해야 한다.

## hashcode()

hashCode 메소드는 객체의 해시코드 값을 리턴합니다.

이 메소드는 해시 테이블(java.util.HashMap 같은)을 사용할 때의 이점을 위해 제공됩니다.

hashCode 메소드의 일반 규약은 다음과 같습니다.

- 변경되지 않은 한 객체의 hashCode 메소드를 호출한 결과는 항상 똑같은 integer 값이어야 합니다.
    - 객체가 변경됐더라도 equals 메소드가 참고하는 정보가 변경되지 않았다면 hashCode 값은 달라지지 않습니다.
- equals 메소드가 같다고 판별한 두 객체의 hashCode 호출 결과는 똑같은 integer 값이어야 합니다.
- 그러나 java.lang.Object.equals 메소드가 다르다고 판별한 두 객체의 hashCode 값이 반드시 달라야 하는 것은 아닙니다.
    - 그러나 프로그래머는 동일하지 않은 객체에 대해 구별되는 정수 결과를 생성하면 해시 테이블의 성능이 향상될 수 있음을 알아야 합니다.

### equals를 재정의한 클래스는 hashCode도 재정의 해야한다.

- 그렇지 않으면 hashcode 일반 규약을 어기게 되어 해당 클래스의 인스턴스를 hashMap이나 HashSet 같은 컬렉션의 원소로 사용할 때 문제를 일으킬 것이다.

equals는 논리적 동치성 비교를 위해 물리적으로 다른 두 객체를 논리적으로는 같다고 할 수도 있다.

하지만 Object의 기본 hashcode 메서드는 이 둘이 전혀 다르다고 판단하여, 규약과 달리 서로 다른 값을 반환한다.

```java
    Map<User, String> map1 = new HashMap();
    map1.put(new User(20, "choi"), "1");
    
    System.out.println(map1.get(new User(20, "choi")));
```

위 코드는 map1.get 에서 결과로 "1"이 나와야 할 것 같지만 실제로는 null을 반환한다.

여기서는 2개의 서로 다른 객체가 사용되었다.

User 클래스는 hashcode를 재정의하지 않았기 때문에 논리적 동치인 두 객체가 서로 다른 해시코드를 반환하여 두 번째 규약을 지키지 못한다.

그 결과 get메서드는 엉뚱한 해시 버킷에 가서 객체를 찾으려 한 것이다.

두 인스턴스를 같은 버킷에 담았더라도 get 메서드는 여전히 null을 반환한는데, HashMap은 해시코드가 다른 엔트리끼리는 동치성 비교를 시도조차 하지 않도록 최적화되어 있기 때문이다.


정리

- equals를 재정의할 때는 hashcode도 반드시 재정의해야 한다. 그렇지 않으면 프로그램이 제대로 동작하지 않을 것이다.
- 재정의한 hashcode는 Object의 API문서에 기술된 일반 규약을 따라야하며 서로 다른 인스턴스면 되도록 해시코드도 다르게 구현해야 한다.

# Thread Safe & Syncronized

### Thread Safe란

멀티 스레드 프로그래밍에서 일반적으로 어떤 함수나 변수, 혹은 객체가 여러 스레드로부터 동시에 접근이 이루어져도 프로그램의 실행에 문제가 없음을 뜻한다. 

보다 엄밀하게는 하나의 함수가 한 스레드로부터 호출되어 실행 중일 때, 다른 스레드가 그 함수를 호출하여 동시에 함께 실행되더라도 각 스레드에서의 함수의 수행 결과가 올바로 나오는 것으로 정의한다.

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=http%3A%2F%2Fcfile29.uf.tistory.com%2Fimage%2F233C013B565060CD383B6B)

Thread-safe를 지키기 위한 방법

1. Re-entrancy

 - 어떤 함수가 한 스레드에 의해 호출되어 실행 중일 때, 다른 스레드가 그 함수를 호출하더라도 그 결과가 각각에게 올바로 주어져야 한다.

2. Thread-local storage

 - 공유 자원의 사용을 최대한 줄여 각각의 스레드에서만 접근 가능한 저장소들을 사용함으로써 동시 접근을 막는다.

 - 이 방식은 동기화 방법과 관련되어 있고, 또한 공유상태를 피할 수 없을 때 사용하는 방식이다.

3. Mutual exclusion

 - 공유 자원을 꼭 사용해야 할 경우 해당 자원의 접근을 세마포어 등의 락으로 통제한다.

4. Atomic operations

 - 공유 자원에 접근할 때 원자 연산을 이용하거나 '원자적'으로 정의된 접근 방법을 사용함으로써 상호 배제를 구현할 수 있다.

## synchronized

synchronized를 이용한 동기화
가장 간단한 동기화 방법인 synchronized 키워드를 이용한 동기화에 대해서 알아보자.

이 키워드는 임계 영역을 설정하는데 사용되며 두 가지 방식이 있다.

메서드 전체를 임계 영역으로 지정

```java
public synchronized void calcSum(){}  // 임계 영역
```

첫번째 방법은 메서드 앞에 synchronized를 붙이는 것인데, synchronized를 붙이면 메서드 전체가 임계 영역으로 설정된다. 

쓰레드는 synchronized메서드가 호출된 시점부터 해당 메서드가 포함된 lock을 얻어 작업을 수행하다가 메서드가 종료되면 lock을 반환한다.

특정한 영역을 임계 영역으로 지정
```java
synchronized(객체의 참조변수){} // 임계 영역
```

두번째 방법은 메서드 내의 코드 일부를 블럭{}으로 감싸고 블럭 앞에 'synchronized(참조변수)'를 붙이는 것인데, 이때 참조변수는 락을 걸고자 하는 객체는 참조하는 것이어야 한다. 이 블록을 synchronized블록이라고 부르며, 이 블록의 영역 안으로 들어가면서부터 쓰레드는 지정된 객체의 lock을 얻게 되고, 이 블록을 벗어나면 lock을 반납한다.

두 방법 모두 lock의 획득과 반납이 모두 자동적으로 이루어지므로 우리가 해야 할 일은 그저 임계 영역만 설정해주는 것이다. 

모든 객체는 lock을 하나씩 가지고 있으며, 해당 객체의 lock을 가지고 있는 쓰레드만 임계 영역의 코드를 수행할 수 있다. 그리고 다른 쓰레드들은 lock을 얻을 때까지 기다리게 된다.
 
임계 영역은 멀티쓰레드 프로그램의 성능을 좌우하기 때문에 가능하면 메서드 전체에 락을 거는 것보다 synchronized블록으로 임계 영역을 최소화해서 보다 효율적인 프로그램이 되도록 노력해야 한다.

synchronized를 이용한 동기화는 지정된 영역의 코드를 한번에 하나의 쓰레드가 수행하는 것을 보장한다.

# Immutable Object

불변 객체란
```
객체 지향 프로그래밍에 있어서 불변객체(immutable object)는 생성 후 그 상태를 바꿀 수 없는 객체를 말한다.

반대 개념으로는 가변(mutable) 객체로 생성 후에도 상태를 변경할 수 있다. 객체 전체가 불변인 것도 있고, C++에서 const 데이터 멤버를 사용하는 경우와 같이 일부 속성만 불변인 것도 있다. 또, 경우에 따라서는 내부에서 사용하는 속성이 변화해도 외부에서 그 객체의 상태가 변하지 않은 것 처럼 보인다면 불변 객체로 보기도 한다. 

예를 들어, 비용이 큰 계산의 결과를 캐시하기 위해 메모이제이션(Memoization)을 이용하더라도 그 객체는 여전히 불변하다고 볼 수있다. 불변 객체의 초기 상태는 대개 생성 시에 결정되지만 객체가 실제로 사용되는 순간까지 늦추기도 한다.

불변 객체를 사용하면 복제나 비교를 위한 조작을 단순화 할 수 있고, 성능 개선에도 도움을 준다. 하지만 객체가 변경 가능한 데이터를 많이 가지고 있는 경우엔 불변이 오히려 부적절한 경우가 있다. 이 때문에 많은 프로그래밍 언어에서는 불변이나 가변 중 하나를 선택할 수 있도록 하고 있다.
```

즉, 객체에 값을 할당하면 내부 데이터를 변경시킬 수 없다는 것입니다. 대표적인 예로 String이 있습니다.

String은 String str="a", str="ab" 이런 식으로 사용하기 때문에 값이 변경한다고 생각하여 불변객체가 아닌 것으로 착각하기 쉽습니다.

하지만 이것은 str가 처음에 참조하고 있는 "a"값이 "b"로 변경되는 것이 아니라 "b"라는 새로운 객체를 만들고 그 객체를 str이 참조하게 하는 것입니다.

장점

- 객체에 대한 신뢰도가 높아집니다. 객체가 한번 생성되어서 그게 변하지 않는다면 transaction 내에서 그 객체가 변하지 않기에 우리가 믿고 쓸 수 있기 때문입니다.
- 생성자, 접근메소드에 대한 방어 복사가 필요없습니다.
- 멀티스레드 환경에서 동기화 처리없이 객체를 공유할 수 있습니다.

단점

- 객체가 가지는 값마다 새로운 객체가 필요합니다. 따라서 메모리 누수와 새로운 객체를 계속 생성해야하기 때문에 성능저하를 발생시킬 수 있습니다.

# String
## String a = "" vs String a = new String("")
## String vs StringBuffer vs StringBuilder

StringBuilder와 StringBuffer는 무슨 차이가 있는가?

**먼저 String 과 StringBuilder,StringBuffer 와의 큰 차이점은 String은 불변(immutable)의 속성을 갖는다는 점입니다.**

String 객체를 생성하는 방법은 new 연산자를 이용하는 것과 리터럴을 이용한 방식이 있다.

리터럴을 이용하여 사용하면 String 값은 JVM 메모리 내의 Heap영역에 "String Constant Pool"에 저장되어 사용되지만,

new 연산자로 생성하면 같은 내용이라도 여러개의 객체가 각 Heap 영역을 차지한다.

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FkZQFx%2Fbtra8ApVg1L%2FFxmtImFyA8kLlAqL92GVfk%2Fimg.png)
![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FYtBko%2FbtraVEUCMqf%2FyRojOgC857AzkTdixRQGsK%2Fimg.png)

같은 "cat" 이라는 문자열이지만 리터럴로 생성한 cat1 과 cat2는 같은 객체를 참조하고 cat3은 다른 객체를 참조한다.

그래서 String으로 +와 같은 문자열 연산을 하게 될 경우 해당 문자열의 객체가 새로 생긴다.
 
하지만 StringBuilder와 StringBuffer는 가변성을 가지기 때문에 append()와 delete() 등의 API를 이용해서 동일 객체내에서 문자열을 변경하는 것이 가능합니다.

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FK5aEH%2FbtrbbTbqXQZ%2FDdJ2kzt8Yy0wYJFr3m9Exk%2Fimg.png)

![IMAGE](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcCqfHf%2FbtraWTLm543%2FNcSMHY59841c8fSIJYu8uk%2Fimg.png)

String은 값을 변경하면 hashCode 값이 변경되는데 StringBuilder는 값이 변경되어도 hashCode 값은 변경되지 않는다.


그럼 StringBuilder와 StringBuffer의 차이점은 무엇일까?

바로 **동기화**의 차이이다.

StringBuilder의 append 메서드

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FI0eqe%2Fbtra6HixCDF%2FXZbiEBsLgdQUoUQTXbBsf1%2Fimg.png)


StringBuffer의 append 메서드

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fctvl5c%2Fbtra35qurT2%2FDAOhhwVTDGVEYbnVkHT3zK%2Fimg.png)

StringBuffer의 append에는 synchronized 키워드가 보이는데 바로 해당 메서드 전체를 임계영역으로 지정해서 동기화를 보장해준다는 것이다. 

때문에 멀티스레드 환경에서 안전하다.

반대로 StringBuilder에서는 동기화를 보장하지 않기 때문에 싱글스레드나 동기화를 고려하지 않아도 되는경우 사용 할 수 있다.

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FuJWgC%2Fbtra8AXNadU%2Feh4TEaCkGmzdU19FYgJbK1%2Fimg.png)

# Java 컬렉션
# List
## ArrayList vs LinkedList
List
- 리스트는 순서가 있는 엘리먼트의 모임으로 배열과는 다르게 빈 엘리먼트는 절대 허용하지 않는다.
- 리스트는 배열이 가지고 있는 인덱스라는 장점을 버리고 대신 빈틈없는 데이터의 적재 라는 장점을 취함
- 리스트에서 인덱스는 몇 번째 데이터인가 정도(순서)의 의미를 가진다. (배열-Array에서의 인덱스는 값에 대한 유일무이한 식별자)


![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbxSQdR%2FbtqTyBzXfTx%2FJg0RdLWPPDZhnPv2ywDZ3k%2Fimg.png)

ArrayList는 index가 있고, LinkedList는 각 원소마다 앞,뒤 원소의 위치값을 가지고 있다.

이러한 각각의 특징은 조회, 삽입, 삭제시에 성능의 차이를 발생시킨다.

### ArrayList
ArrayList는 기본적으로 배열을 사용한다. 하지만 일반 배열과 차이점이 존재한다.

일반 배열은 처음에 메모리를 할당할 때 크기를 지정해주어야 하지만,

ArrayList는 크기를 지정하지 않고 동적으로 값을 삽입하고 삭제할 수 있다.

 
- 조회
   - ArrayList는 각 데이터의 index를 가지고 있고 무작위 접근이 가능하기 때문에, 해당 index의 데이터를 한번에 가져올 수 있다.

- 데이터 삽입과 삭제
    - 데이터의 삽입과 삭제시 ArrayList는 그만큼 위치를 맞춰주어야 한다.
    - 위의 사진으로 예를들면 5개의 데이터가 있을 때 맨 앞의 2를 삭제했다면 나머지 뒤의 4개를 앞으로 한칸씩 이동해야 한다.
    - 삽입과 삭제가 많다면 ArrayList는 비효율적이다.

LinkedList

- LinkedList는 내부적으로 양방향의 연결 리스트로 구성되어 있어 참조하려는 원소에 따라 처음부터 정방향 또는 역순으로 순회 가능
(배열의 단점을 보완하기 위해 LinkedList가 고안되었다.)

- 조회
    - LinkedList는 순차적 접근이기 때문에 검색의 속도가 느리다.

- 데이터 삽입과 삭제
    - LinkedList는  데이터를 추가·삭제시 가리키고 있는 주소값만 변경해주면 되기 때문에 ArrayList에 비해 상당히 효율적이다.
    - 위의 사진으로 예를들면 2번째 값을 삭제하면 1번째 노드가 3번째 노드를 가리키게 하기만 하면 된다.


조회시에는 ArrayList가 우위에 있지만,

삽입/삭제 시에는 LinkedList가 뛰어난 성능을 보여준다.

소량의 데이터를 가지고 사용할 때는 사실 큰 차이가 없지만,
정적인 데이터를 활용하면서 조회가 빈번하다면 ArrayList를 사용하는 것이 좋고,
동적으로 추가/삭제 요구사항이 빈번하다면 LinkedList를 사용하는 것이 좋다.


# Map
## HashTable vs HashMap vs LinkedHashMap vs TreeMap
## HashMap vs ConcurrentHashMap

위에 나열된 클래스들은 Map 인터페이스를 구현한 콜렉션들입니다. 이 콜렉션들은 비슷한 역할을 하는것 같으면서도 다르게 구현되어 있습니다. 기본적으로 Map 인터페이스를 구축한다면 <key, value>구조를 가지게 됩니다.

### Hashtable
Hashtable은 put, get과 같은 주요 메소드에 synchronized 키워드가 선언 되어 있습니다. 또한 key, value에 null을 허용하지 않습니다.
HashTable은 동기화를 위해 synchronized 키워드를 이용해서 메서드 전체에 락을 겁니다. 이 방법은 편하고 안전한 반면에 Scalability(확장성)가 떨어집니다.
자바에서 Hashtable 주요 메서드인 get 코드

메서드 전체에 synchronized를 이용해서 락을 건다.

![image](https://user-images.githubusercontent.com/47075043/154895652-912ae1e6-2765-40d5-b084-365ec451608f.png)

### HashMap

HashMap은 주요 메소드에 synchronized 키워드가 없습니다. 또한 Hashtable과 다르게 key, value에 null을 입력할 수 있습니다.

### ConcurrentHashMap

HashMap을 thread-safe 하도록 만든 클래스가 ConcurrentHashMap입니다. 하지만 HashMap과는 다르게 key, value에 null을 허용하지 않습니다.
ConcurrentHashMap은 내부적으로 여러 개의 세그먼트를 두고 각 세그먼트마다 별도의 락을 가지고 있습니다.
자바에서 ConcurrentHashMap 주요 메서드 중 하나인 putVal 코드

메서드 전체가 아닌 일부분에 synchronized를 이용해서 락을 건다.

![image](https://user-images.githubusercontent.com/47075043/154896517-5bcbe017-1f50-4245-aa9c-2bd852c6c292.png)

MultiThread 환경에서 동기화 처리가 필요하다면 ConcurrentHashMap을 사용하는 것이 안정적이다. 동기화가 필요하지 않은 경우라면 그냥 HashMap을 사용하자. Hashtable은 Thread-Safe 하긴 하나 느리다는 단점이 있다.

### TreeMap

TreeMap은 키로 정렬된다. “키 정렬”의 개념을 이해하기 위해 다음의 예제를 확인하자.

```java
class Dog {
	String color;
 
	Dog(String c) {
		color = c;
	}
	public boolean equals(Object o) {
		return ((Dog) o).color.equals(this.color);
	}
 
	public int hashCode() {
		return color.length();
	}
	public String toString(){	
		return color + " dog";
	}
}
 
public class TestTreeMap {
	public static void main(String[] args) {
		Dog d1 = new Dog("red");
		Dog d2 = new Dog("black");
		Dog d3 = new Dog("white");
		Dog d4 = new Dog("white");
 
		TreeMap<Dog, Integer> treeMap = new TreeMap<Dog, Integer>();
		treeMap.put(d1, 10);
		treeMap.put(d2, 15);
		treeMap.put(d3, 5);
		treeMap.put(d4, 20);
 
		for (Entry<Dog, Integer> entry : treeMap.entrySet()) {
			System.out.println(entry.getKey() + " - " + entry.getValue());
		}
	}
}

//// OUTPUT ////
// Exception in thread "main" java.lang.ClassCastException: collection.Dog cannot be cast to java.lang.Comparable
// 	at java.util.TreeMap.put(Unknown Source)
// 	at collection.TestHashMap.main(TestHashMap.java:35)
```
TreeMap은 키로 정렬되기 때문에, 키 객체는 다른 키 객체과 비교가 가능해야만 한다. 

그러므로, 키 객체는 Compariable Interface를 구현해야만 한다.

예를 들면, String은 Comparable Interface를 구현하고 있기 때문에 TreeMap의 키로 사용할 수 있다.

### LinkedHashMap

LinkedHashMap은 HashMap의 subclass이다. 그 말인 즉슨, HashMap의 모든 특징을 상속받는다는 말이다. 

HashMap과 LinkedHashMap의 큰차이점은 키쌍을 매핑했을때 순서 입니다.

HashMap은 순서대로 저장이 되지 않습니다.

반면, LinkedHashMap은 순서대로 저장 됩니다.


