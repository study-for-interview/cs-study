# 📌 절차지향
![](https://images.velog.io/images/kcwthing1210/post/b1d05813-76a2-4986-9fc2-21e34d2fe2ea/image.png)
## ✅ 특징

- 초기의 프로그래밍 방식으로, 일이 진행 순서대로 프로그래밍 하는 방법( 데이터의 흐름에 기반한 프로그래밍 )
- 순차적인 처리가 중요하며 프로그램 전체가 유기적으로 연결되도록 만드는 프로그램 기법
- 함수로 부터 데이터를 받아서 기능을 구현하는 방식
- 컴퓨터의 작업 처리방식과 유사하여 상대적으로 더 빠르다.
- 순서와 흐름을 먼저 세우고 필요한 자료구조와 함수들을 설계하는 방식.
- '프로그램이 무슨일을 하는가?' 라는 사고에서 비롯된 개념(기능적 가치)
- 상위로부터 하위로 쪼개 나가는 방식 때문에 Top-down방식이라고도 함(큰 문제를 해결하기 위해 몇개의 작은 문제들로 나누어 해결)
## ✅ 단점

- 각 코드의 순서가 민감하게 연결되어있어, 규모가 커지고 복잡도가 올라갈 수록 유지보수 및 분석에 어려움이 있다.

# 📌 객체지향
-  'JAVA', 'C++', 'Python' 등 최근언어는 모두 적용
   ![](https://images.velog.io/images/kcwthing1210/post/56f30253-a246-4075-b719-3b8a6718bcca/image.png)

- 모든 데이터를 객체로 취급하고, 객체가 처리 요청을 받았을 때, 객체 내부의 기능을 사용해 처리하는 방법
- 함수보다 데이터를 표현하는 객체 중심으로 프로그래밍하며 객체간의 유기적인 동작을 한다.
- 자료구조와 이를 중심으로 한 모듈들을 먼저 설계한 다음에 실행 순서와 흐름을 짜는 방식
- '현실세계의 어떤 대상을 모델링 하는가?'의 관점으로 바라본 프로그래밍 기법
- 객체들을 조합하여 큰 문제를 해결하는 Bottom-up방식을 지향함(작은 문제를 해결 해결할 수 있는 객체를 만든 후 이를 조합하여 큰 문제를 해결)
- 독립성/신뢰성 높게 만들어 놓으면 이후 재사용가능 -> 개발기간, 비용이 줄어듦

## ✅ 단점
- 처리 속도가 상대적으로 느리다.
- 설계에 많은 시간이 소요된다.

# 📌 함수형 프로그래밍
- 클로저, 하스켈, 리스프
  ![](https://images.velog.io/images/kcwthing1210/post/9fd888b0-ead6-43ee-a9ba-144cf09c6b2d/image.png)

## ✅ 특징
- 함수 자체가 일급객체가되는 프로그래밍 기법. (객체지향에서는 클래스(또는 Object)가 일급객체이다.)
- 일급 객체란 다른 요소들과 아무런 차별이 없는 객체를 뜻함.
- 상태값을 지니지 않는 함수들의 연속. (객체지향에서는 프로그램에서 상호작용하는 객체들의 집합)
- 값의 연산 및 결과 도출 중심으로 코드작성이 이루어짐.
- 함수는 인자로 받은 값을 별도로 저장하지 않고, 간결한 과정으로 처리하고 매핑하는데 목적을 둠.
- 객체지향보다 코드가 간결하여 사이드이펙트를 미연에 방지한다.
- 데이터형에 구애받지 않는다.


## ✅ 명령형과 선언형 자바스크립트 비교

- 명령형

```javascript
function mult2 (arr){
    let results = []
    for(let i=0; i<arr.length; i++{
    	results.push(arr[i]*2);
    }
    return result
}
```
- 선언형

```javascript
function mult2(arr){
    return arr.map((v) => item *2);
}
```

-  위에서 보는바와 같이 명령형(절차/객체 지향)은 어떻게(HOW) 하는지 차근차근 풀어쓰는 반면 선언형(함수형) 프로그래밍은 무엇(What)을 할것인가를 짧게 나타낸다.

![](https://images.velog.io/images/kcwthing1210/post/cf364fac-ef6f-47a6-afa9-de8ba40a0e36/image.png)

# 🧩 Reference
- https://develaniper-devpage.tistory.com/92

![](https://images.velog.io/images/kcwthing1210/post/7d6b30ae-4382-45a2-ad91-02c977c0bec6/image.png)

# 📌 JVM
- 자바 가상 머신
- Java Virtual Machine

## ✅ JVM의 기능

1. 자바 프로그램이 어느 기기, 어느 운영체제 상에서도 실행될 수 있게 만들어 줍니다. => WORA

2. 자바 프로그램의 메모리를 효율적으로 관리 & 최적화해 줍니다.


과거의 모든 프로그램은 운영체제에 맞게 작성되었습니다. 같은 프로그램이지만 윈도우, 리눅스, 맥 등 사용하는 운영체제에 따라 다르게 작성되어야만 했습니다. 게다가 프로그램이 사용하는 메모리도 개발자가 일일이 관리해줘야만 했습니다. 그러던 중 JVM이 등장합니다. JVM 덕분에 개발자는 앞서 말한 귀찮은 작업들을 하지 않아도 되게 됩니다.

## ✅ 가비지 컬렉션(Garbage Collection)

JVM이 메모리를 관리하는 프로세스를 지칭하는 용어입니다. 자바 프로그램 상에서 사용하지 않은 메모리를 지속적으로 찾아 제거함으로써 효율적인 메모리 관리를 가능케 합니다.


# 📌 JRE
![](https://images.velog.io/images/kcwthing1210/post/d1b3a279-49a6-41d9-b42a-a9fc43884201/image.png)
- 자바 런타임 환경
-  Java Runtime Environment
- JRE는 JVM 이 자바 프로그램을 동작시킬 때 필요한 라이브러리 파일들과 기타 파일들을 가지고 있다. JRE는 JVM의 실행환경을 구현했다고 할 수 있다.
- 클래스 로더, 클래스 라이브러리를 통해 작성한 자바 코드를 라이브러리와 결합한 후 JVM에 넘겨 실행시킵니다. JRE는 그 자체로 특별한 기능을 한다기보다는 JVM이 원활하게 잘 작동할 수 있도록 환경을 맞춰주는 역할을 합니다.

## ✅ 자바 8의 메모리 관리

자바 메모리는 힙, 스택, 메타 스페이스로 구성되어 있습니다.

· 힙 - 자바가 변수 내용을 저장하는 장소

· 스택 - 자바가 함수 실행 및 변수 참조를 저장하는 장소

· 메타 스페이스(과거 펌젠) - 자바가 클래스 정의와 같이 프로그램에서 변화하지 않는 정보를 저장하는 장소

# 📌 JDK
![](https://images.velog.io/images/kcwthing1210/post/d7043556-cc4b-4f1f-b188-ae9bc31bba3e/image.png)
- 자바 개발 키트
-  Java Development Kit

우리가 일반적으로 자바를 공부하기 위해 설치하는 게 바로 이 JDK입니다. JDK를 설치하면 JRE가 자동으로 설치됩니다. JDK는 JRE를 포함하고 있고, JRE는 JVM을 포함하고 있습니다. 따라서 JDK를 설치하면 JRE, JVM이 자동으로 다 설치됩니다.

자바로 개발을 하지 않는 일반 사용자들은 자바로 만든 프로그램을 실행만 하면 되기 때문에 JRE만 설치해도 됩니다. 그러나 자바로 뭔가를 만들어보고 싶은 사람은 JDK를 설치해야 합니다.

JDK에는 JRE에는 없는 "자바 컴파일러(javac, java compiler)"를 포함하고 있습니다. 컴파일러란 우리가 작성한 자바 문법을 컴퓨터가 이해할 수 있게 바꿔주는 해석기 같은 존재입니다. 실제로 .java 파일을 만들어서 실행(빌드)하면 컴파일 작업을 거쳐 .class 라는 파일이 자동으로 생성됩니다. 아래 강의를 보시면 더 잘 이해하실 수 있습니다.

# 📌 자바 컴파일 과정
![](https://images.velog.io/images/kcwthing1210/post/090471a3-2e3f-4f50-b05a-c773c40b5179/image.png)
1. 모든 소스코드는 .java포맷의 파일로 작성된다.

2. javac 컴파일러는 자바코드를 .class파일로 컴파일한다. 이 때, .class파일은 JVM이 이해할 수 있는 바이트코드(bytecode)로 이루어진다.

3. JVM의 인터프리터와 JIT 컴파일러는 바이트코드를 각 OS가 실행할 수 있는 기계어로 변환시킨다.

4. 프로세서는 기계어에 따라 동작을 수행한다.

# 🧩 Reference
- https://m.blog.naver.com/duqrlwjddns1/221770110714
- ![](https://images.velog.io/images/kcwthing1210/post/fb7ba894-c6f7-4305-bc95-18e38335d825/image.png)
- https://93jpark.tistory.com/54


## JVM의 메모리 구조
![](https://images.velog.io/images/kcwthing1210/post/95e13964-bf6b-4ba2-91c1-682e4bda86d0/image.png)

> 1. 메서드 영역
     프로그램 실행 중 어떤 클래스가 사용되면 JVM은 해당 클래스파일을 읽어서 분석하여 클레스에 대한 정보(클래스데이터) 와 클래스변수 저장
2. 호출스택 ( Call Stack)
   메서드의 작업에 필요한 메모리 공간 제공, 메서드가 작업을 마치면 할당되었던 메모리공간은 반환
3. 힙(Heap)
   인스턴스 변수 생성

#### 호출스택 흐름
![](https://images.velog.io/images/kcwthing1210/post/a5ff2004-4d22-44e8-953a-e389f2bccad1/image.png)


![](https://images.velog.io/images/kcwthing1210/post/e450da50-ad83-4e6f-8145-3a462628a89e/image.png)

> 호출스택의 특징
- 메서드가 호출되면 수행에 필요한 만큼의 메모리를 스택에 할당받음
- 메서드가 수행을 마치면 메모리를 반환하고 스택에서 제거 됨
- 호출스택의 제일 위에 있는 메서드가 현재 실행 중인 메서드
- 아래에 있는 메서드가 바로 위의 메서드를 호출한 메서드


## 객체지향
#### 객체란?
- 주변에 있는 사물이나 생명체 같은 모든것들을 말한다. 프로그래밍에서의 객체는 데이터의 분산을 막기 위해 데이터와 기능을 하나로 묶은 그룹이라고 볼 수있다.

#### 객체지향언어란?
- 객체를 만들고 객체를 사용하는 프로그래밍 방법
- 프로그램을 그저 데이터와 처리방법으로 나누는게 아니고, 다수의 "객체"를 만들고, 이들이 서로 상호작용을 통해 만들어지는 방식


oop(핵심개념)
1. 캡슐화
   ![](https://images.velog.io/images/kcwthing1210/post/ac9965bf-7ed2-4e5c-8f2d-97d1d3ff9903/image.png)
- 캡슐화는 관련이 있는 변수와 함수를 하나의 클래스로 묶고 외부에서 쉽게 접근하지 못하도록 은닉
- 객체에 직접적인 접근을 막고 객체가 제공하는 필드와 메소드를 통해서만 접근이 가능합니다.(주로 Getter,Setter 이용)

``` java
public class member {

	private String id;
	private String pw;

	//getter
	public String getId() {
		return id;
	}
	public String getPw() {
		return pw;
	}
	//setter
	public void setId(String id) {
		this.id = id;
	}
	public void setPw(String pw) {
		this.pw = pw;
	}
}
```
- member 클래스의 모든 변수는 private으로 접근제어자 선언을 해놓았기 때문에 member 클래스 내부에서만 접근이 가능
- 접근을 위해 setter와 getter 라는 장치를 만들어 내부에서 접근가능
2. 상속
- 상위 클래스의 모든걸 하위 클래스가 모두 이어 받는것 입니다. 즉, 부모가 자식에게 유전자를 물려주듯이 부모의 특징을 자식에게 모두 물려줍니다.
3. 추상화
- 구체적인 사물들의 공통적인 특징을 파악해서 이를 하나의 개념(집합)으로 다루는 수단
- 사물들의 공통된 특징, 즉 추상적 특징을 파악해 인식의 대상으로 삼는 행위

![](https://images.velog.io/images/kcwthing1210/post/dce5f956-5376-427a-955a-9b7c6bc6ead9/image.png)


4. 다형성
- 객체들의 타입이 다르면 똑같은 메세지가 전달되더라도 서로 다른 동작을 하는 것


![](https://images.velog.io/images/kcwthing1210/post/4d0dd9b1-7dde-4131-8272-d3300340edd7/image.png)

#### 객체지향 언어의 장점
1. 재사용성
   상속을 통해 프로그래밍시 코드의 재사용을 높일 수 있음.

2. 생산성 향상
   잘 설계된 클래스를 만들어서 독립적인 객체를 사용함으로써 개발의 생산성을 향상시킬 수 있음.

3. 자연적인 모델링
   우리 일상생활의 모습의 구조가 객체에 자연스럽게 녹아들어 있기 때문에 생각하고 있는 것을 그대로 자연스럽게 구현할 수 있다.

4. 유지보수의 우수성
   프로그램 수정시 추가, 수정을 하더라도 캡슐화를 통해 주변 영향이 적기때문에 유지보수가 쉽다. 

# 📌 GC (Garbage Collecton)
- 더이상 사용하지 않는 객체 등을 메모리에서 해제(삭제)하는 JVM의 작업
- Java 프로세스가 동작하는 과정에서 GC는 불필요한 또는 더이상은 사용하지 않는 객체들을 메모리에서 제거함으로써, Java 프로세스가 한정된 메모리를 효율적으로 사용할 수 있게 해준다.

- 또한 JVM에서 GC의 스케줄링을 담당함으로서 Java 프로그래머들에게는 메모리를 관리해야하는 부담을 줄여주게된다. 즉, 일반적인 개발 작업간에는 메모리 할당/해제를 직접 프로그래밍하지 않아도 된다는 이야기다.

JVM의 GC에 대해서 알기 위해서는 우선 JVM 메모리 구조에 대해서 알아야 한다

## ✅ JVM Heap 메모리 구조
![](https://images.velog.io/images/kcwthing1210/post/e09c1455-e0f2-47a5-b14c-f5153fbcae67/image.png)
- Java 메모리의 각 영역에서 GC가 발생하면, 사용하지 않는(참조가 존재하지 않는) 객체들은 메모리에서 제거된다.

## ✅ GC 동작과정
![](https://images.velog.io/images/kcwthing1210/post/8cd5b592-f9df-46d8-910b-b623ebd44ecf/image.png)

- 처음 생성된 객체 new Model(); 는 Young Generation 영역의 일부인 Eden 영역에 위치하게된다. 그리고 Minor GC가 발생하게 되면, 사용하지 않는 다시말하면 다른 곳에서 참조되지 않는 객체는 메모리에서 제거된다.

- Eden 영역에서 살아남은 객체는 Young Generation 영역의 또다른 일부인 Survivor 영역으로 이동하게된다. Survivor 영역은 Survivor1 영역과 Survivor2 영역으로 구성되어 있는데, Minor GC가 발생할 때마다 Survivor1 영역에서 Survivor2 영역으로 또는 Survivor2 영역에서 Survivor1 영역으로 객체가 이동하게되며, 이 과정에서 더이상 참조되지 않는 객체는 메모리에서 제거된다.
- Minor GC가 발생하는 동안 Survivor1, Survivor2 영역을 오가며 살아남은 객체들은 최종적으로 Old Generation 영역으로 옮겨지며, Old Generation 영역에 있다가 미사용된다고 식별되는 객체들은 Full GC를 통해 메모리에서 제거된다.