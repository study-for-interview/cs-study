# 🎁프로세스 동기화
## 📌 동기 VS 비동기
### ✔ 동기
- 메소드를 실행시킴과 동시에 반환 값이 기대되는 경우
- 요청을 하면 시간이 얼마가 걸리던지 요청한 자리에서 결과가 주어져야 한다.
- 요청과 결과가 한 자리에서 동시에 일어남
- A노드와 B노드 사이의 작업 처리 단위(transaction)를 동시에 맞춤
- ex) 해야할 일(task)가 빨래, 설거지, 청소 세 가지가 있다고 가정 했을 때, 동기적으로 처리한다면 빨래를 하고 설거지를 하고 청소

### ✔ 비동기
- 요청과 결과가 동시에 일어나지 않아도 됨.
- 요청한 그 자리에서 결과가 주어지지 않음
- 노드 사이의 작업 처리 단위를 동시에 맞추지 않아도 됨
- ex) 비동기적으로 일을 처리한다면 빨래, 설거지, 청소는 각각 대행 업체에 맡긴다. 셋 중 어떤 것이 먼저 완료될지는 알 수 없다. 일을 모두 마친 업체는 나에게 알려주기로 했으니 나는 다른 작업을 할 수 있다. 이 때는 백그라운드 스레드에서 해당 작업을 처리하는 경우의 비동기를 의미



# 프로세스 동기화
- 프로세스 동기화는 여러 프로세스가 공유하는 자원의 일관성을 유지하는 것이다. 가령 여러 프로세스가 동시에 하나의 공유된 자원에 접근하려고 할 때 이 프로세스들의 순서를 정하여 데이터의 일관성을 유지시켜주어야 한다.

- ex)
``` java
// Test.java
class Test {
	public static void main(String[] args) throws InterruptedException {
		BankAccount b = new BankAccount();
		Parent p = new Parent(b);
		Child c = new Child(b);
		p.start();   // start(): 쓰레드를 실행하는 메서드
		c.start();
		p.join();    // join(): 쓰레드가 끝나기를 기다리는 메서드
		c.join();
		System.out.println("balance = " + b.getBalance());
	}
}

// 계좌
class BankAccount {
	int balance;
	void deposit(int amount) {
		balance = balance + amount;
	}
	void withdraw(int amount) {
		balance = balance - amount;
	}
	int getBalance() {
		return balance;
	}
}

// 입금 프로세스
class Parent extends Thread {
	BankAccount b;
	Parent(BankAccount b) {
		this.b = b;
	}
	public void run() {   // run(): 쓰레드가 실제로 동작하는 부분(치환)
		for (int i = 0; i < 100; i++)
		  b.deposit(1000);
	}
}

// 출금 프로세스
class Child extends Thread {
	BankAccount b;
	Child(BankAccount b) {
		this.b = b;
	}
	public void run() {
		for (int i = 0; i < 100; i++)
		  b.withdraw(1000);
	}
}
```
- 여러 쓰레드가 하나의 공유 자원을 사용하여 동기화 문제를 해결하지 못하였기 때문에 원하는 값 안나올 수 있음
- 공통변수(common variable)에 대한 동시 업데이트(concurrent update) 때문에 나타나는 문제

## 📌 임계영역
### ✔ Critical Section(임계영역)
- 멀티 스레딩에 문제점에서 나오듯, 동일한 자원을 동시에 접근하는 작업(e.g. 공유하는 변수 사용, 동일 파일을 사용하는 등)을 실행하는 코드 영역을 Critical Section 이라 칭한다.

- 위 예제에서 공통 변수는 계좌의 잔액이다. 이에 접근하는 프로세스의 코드를 보면 다음과 같다. 이러한 공통변수 구역을 임계구역이라고 한다.
``` java
void deposit(int amount) {
  balance = balance + amount; //출금
}
void withdraw(int amount) {
  balance = balance - amount; //입금
}
```

### ✔Critical Section Problem(임계영역 문제)
- 프로세스들이 Critical Section 을 함께 사용할 수 있는 프로토콜을 설계하는 것이다.

### ✔ Requirements(해결을 위한 기본조건)
- Mutual Exclusion(상호 배제)
  프로세스 P1 이 Critical Section 에서 실행중이라면, 다른 프로세스들은 그들이 가진 Critical Section 에서 실행될 수 없다.
- Progress(진행)
  Critical Section 에서 실행중인 프로세스가 없고, 별도의 동작이 없는 프로세스들만 Critical Section 진입 후보로서 참여될 수 있다.
- Bounded Waiting(한정된 대기)
  P1 가 Critical Section 에 진입 신청 후 부터 받아들여질 때가지, 다른 프로세스들이 Critical Section 에 진입하는 횟수는 제한이 있어야 한다.



### ✔ 해결책
#### (1) Lock
- 하드웨어 기반 해결책으로써, 동시에 공유 자원에 접근하는 것을 막기 위해 Critical Section 에 진입하는 프로세스는 Lock 을 획득하고 Critical Section 을 빠져나올 때, Lock 을 방출함으로써 동시에 접근이 되지 않도록 한다.

- 한계
  다중처리기 환경에서는 시간적인 효율성 측면에서 적용할 수 없다.
#### (2) Semaphores(세마포)
- 세마포는 동기화를 위해 만들어진 소프트웨어로서, 대표적인 동기화 도구이다.

- 소프트웨어상에서 Critical Section 문제를 해결하기 위한 동기화 도구

``` java
class Semaphore {
  int value;      // number of permits
  Semaphore(int value) {
    // ...
  }
  void acquire() {
    value--;
    if (value < 0) {
      // add this process/thread to list
      // block
    }
  }
  void release() {
    value++;
    if (value <= 0) {
      // remove a process P from list
      // wakeup P
    }
  }
}
```
위 코드에서 acquire() 는 value값을 감소시키고 만약 value값이 0보다 작으면 이미 해당 임계구역에 어느 프로세스가 존재한다는 의미이므로 현재 프로세스는 접근하지 못하도록 막아야한다. 이를 list라는 기다리는 줄에 추가한 뒤 block을 걸어준다.(list는 일반적으로 큐로 되어있다.)

release() 는 value값을 증가시키고, 만약 value값이 0보다 같거나 작으면 임계구역에 진입하려고 대기하는 프로세스가 list에 남아있다는 의미이므로 그 중에서 하나를 꺼내어 임계구역을 수행할 수 있도록 해주어야 한다.

![](https://images.velog.io/images/kcwthing1210/post/ba54b82d-d11c-4ec0-ba1e-65434cba7d96/image.png)
세마포를 그림으로 나타내면 위와 같다. list는 실제로 큐로 볼 수 있다. acquire()에 의해 block되는 프로세스는 세마포 내부에 있는 큐에 삽입된 후, 다른 프로세스가 임계구역을 나오면서 release()를 호출하여 세마포 큐에 있는 프로세스를 깨워야 한다.(다시 ready queue로 보낸다.)

위에서 살펴본 것처럼 세마포는 일반적으로 Mutual exclusion을 위해 사용된다.

- ex )
  처음에 살펴본 은행계좌 문제에 세마포를 적용해보자. 위에서 임계구역은 BankAccount 클래스 내부의 입출력하는 부분인 것을 보았다. 여기에 세마포를 적용해보면 아래와 같다.
  이떄, value 값은 임계구역에 몇 개의 프로세스를 접근할 것인지 정하는 것과 같다. 지금은 임계 구역에 하나의 프로세스만 접근가능하기 때문에 1 로 초기화 한다.

``` java 
import java.util.concurrent.Semaphore;  // 세마포를 사용하기 위해 파일 가장 위에 추가해야 한다.

class BankAccount {
	int balance;

	Semaphore sem;
	BankAccount() {   // BankAccount 클래스의 생성자가 호출되면 세마포를 만든다.
		sem = new Semaphore(1);  // value 값을 1로 초기화한다.
	}

	void deposit(int amount) {
		try {
			sem.acquire();   // 임계구역에 들어가기를 요청한다.
		} catch (InterruptedException e) {}
	    /* 임계 구역 */  
		int temp = balance + amount;
		System.out.print("+");
		balance = temp;

		sem.release();   // 임계구역에서 나간다.
	}
	void withdraw(int amount) {
		try {
			sem.acquire();
		} catch (InterruptedException e) {}
	    /* 임계 구역 */  
		int temp = balance - amount;
		System.out.print("-");
		balance = temp;

		sem.release();
	}
	int getBalance() {
		return balance;
	}
}
```
- 세마포는 mutual exclusion뿐 아니라 ordering을 하기 위해서도 사용한다. 즉, 프로세스의 실행 순서를 원하는 순서로 설정 할 수 있다.

![](https://images.velog.io/images/kcwthing1210/post/4e41bb58-1eb1-4a29-b504-0e7acbc0c081/image.png)

예를 들어, 프로세스가 P1, P2 두 개가 있다고 가정하자. 원하는 순서는 P1, P2 순으로 실행하기를 원한다. 그러면 아래와 같이 설정해줄 수 있다.
먼저, 세마포로 감싼 구역에 들어갈 수 있는 프로세스 개수를 정하는 value값을 0으로 설정한다.
- sem value = 0;

1. P1이 먼저 실행된 경우
   Section 1 이전에 아무런 동작이 없으므로 바로 수행한다.
   sem.release() 를 만나면 value값을 1 증가시키고, 세마포 큐에 있는 프로세스를 깨워주는데 현재에는 큐에 프로세스가 없으므로 아무 동작도 하지 않는다.
   P2가 실행된다.
   P2의 sem.acquire() 를 만나면 현재 value값은 1이고 이를 1감소시키면 0이 된다. value = 0이면 block을 하지 않으므로, 무사히 Section 2가 수행된다.
2. P2가 먼저 실행된 경우
   Section 2 이전에 sem.acquire() 가 있으므로 이를 수행하는데, 현재 value값은 0이고 이를 1 감소 시키면 -1 이 된다. value값이 음수면 해당 프로세스를 block시킨다.(세마포 큐에 삽입한다.)
   P1이 실행되면 Section 1이 바로 수행된다.
   sem.release() 를 만나면 value값을 1 증가시키고, 세마포 큐에 있는 P2 프로세스를 깨워준다.(현재 value = 0)
   P2의 Section 2가 수행된다.
   위에서 두 가지 경우를 살펴보았듯이, P1, P2 둘 중 어느 것을 먼저 실행하여도 결과적으로 P1 -> P2 순서로 수행하는 것을 알 수 있다.

ex) java
```
class BankAccount {
	int balance;

	Semaphore sem, semOrder;
	BankAccount() {
		sem = new Semaphore(1);
		semOrder = new Semaphore(0);   // Ordeing을 위한 세마포
	}

	void deposit(int amount) {
		try {
			sem.acquire();
		} catch (InterruptedException e) {}
		int temp = balance + amount;
		System.out.print("+");
		balance = temp;
		sem.release();
		semOrder.release();   // block된 출금 프로세스가 있다면 깨워준다.
	}
	void withdraw(int amount) {
		try {
			semOrder.acquire();   // 출금을 먼저하려고 하면 block한다.
			sem.acquire();
		} catch (InterruptedException e) {}
		int temp = balance - amount;
		System.out.print("-");
		balance = temp;
		sem.release();
	}
	int getBalance() {
		return balance;
	}
}
```


- 종류
    - 카운팅 세마포
      가용한 개수를 가진 자원 에 대한 접근 제어용으로 사용되며, 세마포는 그 가용한 자원의 개수 로 초기화 된다. 자원을 사용하면 세마포가 감소, 방출하면 세마포가 증가 한다.
    - 이진 세마포
      MUTEX 라고도 부르며, 상호배제의 (Mutual Exclusion)의 머릿글자를 따서 만들어졌다. 이름 그대로 0 과 1 사이의 값만 가능하며, 다중 프로세스들 사이의 Critical Section 문제를 해결하기 위해 사용한다.

- 단점
    - Busy Waiting(바쁜 대기)
      Spin lock이라고 불리는 Semaphore 초기 버전에서 Critical Section 에 진입해야하는 프로세스는 진입 코드를 계속 반복 실행해야 하며, CPU 시간을 낭비했었다. 이를 Busy Waiting이라고 부르며 특수한 상황이 아니면 비효율적이다. 일반적으로는 Semaphore에서 Critical Section에 진입을 시도했지만 실패한 프로세스에 대해 Block시킨 뒤, Critical Section에 자리가 날 때 다시 깨우는 방식을 사용한다. 이 경우 Busy waiting으로 인한 시간낭비 문제가 해결된다.
    - Deadlock(교착상태)
      세마포가 Ready Queue 를 가지고 있고, 둘 이상의 프로세스가 Critical Section 진입을 무한정 기다리고 있고, Critical Section 에서 실행되는 프로세스는 진입 대기 중인 프로세스가 실행되야만 빠져나올 수 있는 상황을 지칭한다.


#### (3) 모니터
고급 언어의 설계 구조물로서, 개발자의 코드를 상호배제 하게끔 만든 추상화된 데이터 형태이다.
공유자원에 접근하기 위한 키 획득과 자원 사용 후 해제를 모두 처리한다. (세마포어는 직접 키 해제와 공유자원 접근 처리가 필요하다. )


## 🧩 Reference
- https://private.tistory.com/24
- https://velog.io/@codemcd/%EC%9A%B4%EC%98%81%EC%B2%B4%EC%A0%9COS-8.-%ED%94%84%EB%A1%9C%EC%84%B8%EC%8A%A4-%EB%8F%99%EA%B8%B0%ED%99%94-1#32-ordering

# 🎁 메모리 관리 전략

## 📌메모리 관리 배경
각각의 프로세스 는 독립된 메모리 공간을 갖고, 운영체제 혹은 다른 프로세스의 메모리 공간에 접근할 수 없는 제한이 걸려있다. 단지, 운영체제 만이 운영체제 메모리 영역과 사용자 메모리 영역의 접근에 제약을 받지 않는다.

## 📌 프로세스 바인딩
프로세스의 메모리 범위를 결정하는 것을 바인딩(Binding)이라고 하며, 바인딩을 수행하는 시점에 따라 다음과 같이 분류할 수 있다.

### ✔ Compile-Time Binding
- 프로그램을 컴파일 할 때 메모리 범위를 결정.
- 범위가 달라지면 재컴파일 해야한다.
- 다른 프로그램의 메모리 범위가 겹치지 않도록 프로그래머가 주의해야 함.
- 도스 시절에나 쓰던 방식.
### ✔ Load-Time Binding
- 프로그램이 램에 적재되기 전에 BASE와 LIMIT을 결정.
- 다른 프로그램의 메모리 범위가 겹치지 않도록 운영체제가 관리함.
- 현대 시스템에 채택됨.
### ✔ Run-Time Binding
- 실행중에 운영체제에 의해 다른 메모리 주소로 옮겨질 수 있음.
- 적재시간 바인딩을 기본적으로 포함함.
- 특수한 하드웨어가 필요함.


## 📌 스와핑
### ✔ 정의
-  메모리의 관리를 위해 사용되는 기법. 표준 Swapping 방식으로는 round-robin 과 같은 스케줄링의 다중 프로그래밍 환경에서 CPU 할당 시간이 끝난 프로세스의 메모리를 보조 기억장치(e.g. 하드디스크)로 내보내고 다른 프로세스의 메모리를 불러 들일 수 있다.

### ✔ 특징
![](https://images.velog.io/images/kcwthing1210/post/4dcf5e67-41d9-4736-a17d-a0e613c23c1e/image.png)

- swap-in : 주 기억장치(RAM)으로 불러오는 과정
- swap-out : 보조 기억장치로 내보내는 과정
- swap 에는 큰 디스크 전송시간이 필요하기 때문에 현재에는 메모리 공간이 부족할때 Swapping 이 시작된다.

### ✔ 디스패처
- 스와핑에 의해 작업이 메모리에 적재되어 있지 않을 가능성이 생겼으므로, 실행할 작업이 메모리 적재되어 있는지 검사하는 프로그램

- 메모리에 적재되어 있는지 검사하고, 메모리에 없다면 이미지를 재적재

### ✔ 단점
- 문맥교환 비용의 증가

고전적 스와핑은 보조 기억장치에 작업을 백업하기 때문에, 기억장치의 속도가 느리면 스와핑의 속도도 같이 느려졌습니다. 스와핑은 문맥교환시에 발생하므로 문맥교환의 비용이 대폭 증가한 것과 같습니다. 이것은 짧은 주기의 라운드 로빈 시스템에서 매우 치명적입니다.

- 시스템 처리율 감소 :

그리고 스와핑에만 매달리는 바람에 작업을 수행할 시간이 부족하므로 시스템의 처리율도 감소합니다.

- 재배치 이슈 :

스와핑에 의해 보조기억장치로 날아간 작업이 다시 돌아와야 할 때 BASE 레지스터를 어떻게 할것인지에 대한 고민도 필요합니다. 이전과 같은 장소로 배치된다면 좋겠지만, 항상 그것이 보장되어 있는 것은 아닙니다. Run-Time Binding이 허용되는 시스템이라면 좋겠지만, 모든 시스템이 이를 지원하는 것도 아닙니다.

## 📌 메모리 할당의 분류
### ✔ 단편화
- 프로세스들이 메모리에 적재되고 제거되는 일이 반복되다보면, 프로세스들이 차지하는 메모리 틈 사이에 사용 하지 못할 만큼의 작은 자유공간들이 늘어나게 되는데, 이것이 단편화 이다. -

- 종류
    - 외부 단편화: 메모리 공간 중 사용하지 못하게 되는 일부분. 물리 메모리(RAM)에서 사이사이 남는 공간들을 모두 합치면 충분한 공간이 되는 부분들이 분산되어 있을때 발생한다고 볼 수 있다.
    - 내부 단편화: 프로세스가 사용하는 메모리 공간 에 포함된 남는 부분. 예를들어 메모리 분할 자유 공간이 10,000B 있고 Process A 가 9,998B 사용하게되면 2B 라는 차이 가 존재하고, 이 현상을 내부 단편화라 칭한다.

### ✔ 외부 단편화 해결
-  압축 : 외부 단편화를 해소하기 위해 프로세스가 사용하는 공간들을 한쪽으로 몰아, 자유공간을 확보하는 방법론 이지만, 작업효율이 좋지 않다.
- 외부 단편화는 애초에 연속적 할당에서만 발생하므로, 비연속적 할당 방식인 페이징을 사용하여 외부 단편화를 방지

### ✔ 연속적 메모리 할당

#### (1) 고정 크기 할당
![](https://images.velog.io/images/kcwthing1210/post/d71561b2-e3e2-49eb-b4b6-7f01f80ec502/image.png)

- 메모리를 동일한 크기로 자른 뒤, 각 프로세스마다 블럭 하나만 주는 방식
- 전체 메모리가 N분할 되었다면 적재될 수 있는 프로세스도 최대 N개이므로 다중 프로그래밍 정도는 블럭의 개수와 같으며, 모든 프로세스는 할당된 메모리 크기가 서로 같다.
- 현대에서는 사용되지 않는 방식



#### (2) 동적 크기 할당
![](https://images.velog.io/images/kcwthing1210/post/0804a81a-d69f-4754-b17f-2c405b4179f7/image.png)
- 고정 할당과 달리 각 프로세스에게 할당된 메모리 크기가 다를 있음
- 고정 할당과 달리 할당과 해제를 반복하다보면, 중간중간에 생기는 제대로 사용할 수 없는 빈 공간인 외부 단편화(External Fragmentation)라는 문제를 발생
- 각각의 단편화의 크기는 작을지라도, 전부 모으면 새로운 프로세스를 하나 더 적재할 수 있을만큼 커지기 때문에 동적 할당의 고질적인 단점
- 종류
  - 최초 적합
  ![](https://images.velog.io/images/kcwthing1210/post/d780e61c-33e1-4483-8fc7-ef2dbc63599d/image.png)
    - 처음으로 만난 적당한 빈 공간에 프로세스를 적재
    - 처음으로 만난 빈 공간에 바로 할당해주면 되므로, 다른 두 방식보다 시간복잡도가 낮음

    - 최적 접합
    ![](https://images.velog.io/images/kcwthing1210/post/4a562079-0661-4325-b08f-2ede04bea57f/image.png)
    	- 최적 적합(Best-Fit)은 적당한 빈 슬롯 중 가장 작은 공간에 프로세스를 적재
        - 모든 빈 공간을 탐색해야 하므로 시간복잡도가 높으며, 매우 작은 크기의 빈공간을 생성
    
    - 최악 접합
    ![](https://images.velog.io/images/kcwthing1210/post/02998eb2-775b-4885-85e9-5d7085cc47f6/image.png)
    	- 적당한 빈 슬롯 중 가장 큰 공간에 프로세스를 적재 
        - 모든 빈 공간을 탐색해야 하므로 시간복잡도가 높으며, 매우 큰 크기의 빈공간을 생성




### ✔ 비연속적 메모리 할당
#### Paging(페이징)
- 하나의 프로세스가 사용하는 메모리 공간이 연속적이어야 한다는 제약을 없애는 메모리 관리 방법이다.
- 외부 단편화와 압축 작업을 해소 하기 위해 생긴 방법론으로, 물리 메모리는 Frame 이라는 고정 크기로 분리되어 있고, 논리 메모리(프로세스가 점유하는)는 페이지라 불리는 고정 크기의 블록으로 분리된다.(페이지 교체 알고리즘에 들어가는 페이지)

- 페이징 기법을 사용함으로써 논리 메모리는 물리 메모리에 저장될 때, 연속되어 저장될 필요가 없고 물리 메모리의 남는 프레임에 적절히 배치됨으로 외부 단편화를 해결할 수 있는 큰 장점이 있다.

- 하나의 프로세스가 사용하는 공간은 여러개의 페이지로 나뉘어서 관리되고(논리 메모리에서), 개별 페이지는 순서에 상관없이 물리 메모리에 있는 프레임에 mapping 되어 저장된다고 볼 수 있다.

- 단점 : 내부 단편화 문제의 비중이 늘어나게 된다. 예를들어 페이지 크기가 1,024B 이고 프로세스 A 가 3,172B 의 메모리를 요구한다면 3 개의 페이지 프레임(1,024 * 3 = 3,072) 하고도 100B 가 남기때문에 총 4 개의 페이지 프레임이 필요한 것이다. 결론적으로 4 번째 페이지 프레임에는 924B(1,024 - 100)의 여유 공간이 남게 되는 내부 단편화 문제가 발생하는 것이다.


#### Segmentation(세그멘테이션)
- 페이징에서처럼 논리 메모리와 물리 메모리를 같은 크기의 블록이 아닌, 서로 다른 크기의 논리적 단위인 세그먼트(Segment)로 분할 사용자가 두 개의 주소로 지정(세그먼트 번호 + 변위) 세그먼트 테이블에는 각 세그먼트의 기준(세그먼트의 시작 물리 주소)과 한계(세그먼트의 길이)를 저장

- 단점 : 서로 다른 크기의 세그먼트들이 메모리에 적재되고 제거되는 일이 반복되다 보면, 자유 공간들이 많은 수의 작은 조각들로 나누어져 못 쓰게 될 수도 있다.(외부 단편화)


## 🧩 Reference
- https://aerocode.net/389#%ED%8E%98%EC%9D%B4%EC%A7%80-%ED%85%8C%EC%9D%B4%EB%B8%94-%EA%B5%AC%EC%A1%B0
 
