## 유저/커널 모드

 운영체제는 컴퓨터의 하드웨어를 관리하면서 하드웨어를 손쉽게 그리고 효율적으로 사용할 수 있는 abstraction을 제공한다.

운영체제에서 또 굉장히 중요한 용어가 바로 **커널(kernel)** 이다. 

커널은 운영체제의 핵심 부분이며 시스템의 모든 것을 완전하게 통제하는 기능을 한다.

 커널의 역할은 크게 3가지 정도로 볼 수 있는데 1. 보안 2. 자원 관리 3. 추상화 로 나눌 수 있다. 

 ![os 구조](https://user-images.githubusercontent.com/47075043/150730312-519f0fc1-0b67-45dd-989a-f7a8e2ec1786.png)

커널모드와 유저모드의 구조는 위와 같다. 

사용자가 직접적으로 하드웨어 장치를 제어한다면 큰 문제 발생할 수 있기 때문에 사용자 애플리케이션은 System Call 을 통해 직접적인 하드웨어 요청이나 중요한 시스템 요청을 한다. 

요청을 하면 유저 애플리케이션은 유저모드에서 커널모드로 잠시 전환 되었다가 커널모드에서 작업을 실행한뒤 응답을 유저 애플리케이션에 반환하면서 다시 유저모드로 되돌아가게 된다.

![os 듀얼 모드 전환](https://user-images.githubusercontent.com/47075043/150730689-d78b0c94-83f3-4b29-87ff-ab2b1a662a0e.png)

### 시스템 호출

커널이 자신을 보호하기 위해 만든 인터페이스이다. 
- 커널은 사용자나 응용 프로그램으로부터 컴퓨터 자원을 보호하기 위해 자원에 직접 접근하는 것을 차단한다.
따라서 자원을 이용하기 위해서는 시스템 호출이라는 인터페이스를 사용하여 접근하여야 한다.

특징
- 시스템 호출은 커널이 제공하는 시스템 자원의 사용과 연관된 함수이다.
- 응용 프로그램이 하드웨어 자원에 접근하거나 운영체제가 제공하는 서비스를 이용하려 할 때는 시스템 호출을 사용해야 한다.
- 운영체제는 커널이 제공하는 서비스를 시스템 호출로 제한하고 다른 방법으로 커널에 들어오지 못하게 막음으로써 컴퓨터 자원을 보호한다.
- 시스템 호출은 커널이 제공하는 서비스를 이용하기 위한 인터페이스이며, 사용자가 자발적으로 커널 영역에 진입할 수 있는 유일한 수단이다.

## 커널 종류

### 1. 단일형 구조 커널

- 모놀리틱 커널이라고도 하며 커널의 다양한 서비스 및 높은 수준의 하드웨어 추상화를 하나의 덩어리로 묶은 구조입니다.

- 단점 : 
    -모듈이 분리되어 있더라도 같은 주소, 메모리 공간 내에서 실행되기 때문에 코드의 집적도가 매우 조밀하며, 한 모듈의 버그가 시스템 전반을 다운 시킬 수 있습니다.

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FMRNDa%2Fbtq0DrDtZeE%2FqpmfUfNP9KtKrY7J8CCqi1%2Fimg.png)

### 2. 마이크로 커널

- 하드웨어 추상화에 대한 간결한 작은 집합을 제공하고 더 많은 기능은 서버라고 불리는 응용 소프트웨어를 통해 제공됩니다.

마이크로 커널은 하드웨어 위에 매우 간결한 추상화를 정의하며 기본 연산 집합과 운영체제 서비스를 구현한 스레드 관리, 주소 공간, 프로세스간의 통신이 작은 시스템 콜로 이루어져 있습니다.

일반적으로 커널이 제공하는 네트워킹과 같은 다른 서비스들은 사용자 공간 프로그램인 서버로 구현됩니다.

운영 체제는 서버를 다른 일반적인 프로그램 처럼 간단히 켜고 끌 수 있으며, 네트워킹 지원이 필요없는 경우 서버를 끄면 된다.

일반적으로는 마이크로 커널과 단일형 커널은 정반대의 모습을 지니고 있어 많이 대조된다.

- 장점 : 

    - 커널 서버들이 따로 구현됨 
	-  독립적인 개발, 유지, 보수 가능

- 단점 : 
    - IPC 의 속도가 느림
    - 서버들간의 통신, context switching이 필수적이기 때문에 전반적인 성능 저하

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FckZEVA%2Fbtq0A3pxGcM%2FDb05elEiNtplpXqyEykshK%2Fimg.png)

# 인터럽트

```
OS는 서로 다른 일을 하는 수많은 하드웨어를 사용한다. 이런 장치들은 동기적으로 구동되는데, 이는 각각 동작이 완료될 때 까지 기다려야하므로 "아무것도 하지 않으면서 바쁜 상태"로 많은 시간을 소비하게된다. 이 때, 인터럽트를 사용하여 한번에 하나의 명령만 수행할 수 있는 CPU의 한계성을 보완할 수 있다.
```
- 사전적인 의미로는 **방해하다, 중단시키다** 라는 뜻을 가진다
- OS적으로는 **CPU의 정상적인 프로그램 실행을 방해했다** 는 의미를 가진다.
- 프로그램을 실행하는 도중에 예기치 않은 상황이 발생할 경우, 현재 실행중인 작업을 중단하고 발생된 상황을 처리한 후, 다시 실행중인 작업으로 복귀하는 것

## 인터럽트의 종류

### 1. 외부 인터럽트
```
CPU 코어 외부에서 어떤 일이 발생한 것을 전기적인 신호로 CPU에게 통지하는 경우
```
- 정전•전원이상 인터럽트 : 정전 또는 전원공급의 이상으로 인한 인터럽트
- 기계고장 인터럽트 : CPU 및 기타 하드웨어의 오류로 인한 인터럽트
- 외부 인터럽트 : Timer 나 Operator 로 인한 인터럽트
- 입출력 인터럽트 : 입출력의 종료나 입출력의 오류로 인한 인터럽트

### 2. 내부 인터럽트
```
CPU 코어 외부에서 인터럽트를 거는 경우가 일반적이지만, CPU 내부에서 실행하면서 인터럽트에 걸리는 경우
```
- 프로그램 검사 인터럽트 : Divide by Zero , Overflow/underflow 등

### 3. 소프트웨어 인터럽트 (= Trap)
```
사용자가 프로그램을 실행시키거나 Supervisor(=OS) 를 호출하는 동작을 수행하는 경우
```
- SVC(SuperVisor Call) : OS 를 호출하는 동작을 수행하는 경우


## 인터럽트 동작순서
```
요청 -> 중단 -> 보관 -> 처리 -> 재개
```

처리 과정 

### 1. 현재 실행중인 명령의 메모리 주소를 포함한 부가 정보를 저장한다.

 CPU에서 명령이 실행될 때에는 CPU 내부에 있는 임시 기억장치인 레지스터에 데이터를 읽거나 쓰면서 작업을 한다.

이때 인터럽트가 발생하면 기존의 레지스터값들이 지워지게 되므로 CPU 내의 이러한 상태를  PCB에 저장한다.

```
PCB (프로세스 제어 블록)
PCB는 프로그램마다 하나씩 존재하는데, PCB에는 해당 프로그램의 어느 부분이 실행 중이였는지를 저장한다.
저장되는 내용은 실행중이던 코드의 메모리 주소, 레지스터 값, 하드웨어 상태 등이 저장된다.
```
![PCB 구성](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FRNifh%2Fbtq9NwJH0rX%2FejTzKyhYfLlFAp7DJIKX7K%2Fimg.png)


### 2. 인터럽트 처리 루틴 실행

 운영체제는 할 일을 쉽게 찾아가기 위해 **인터럽트 벡터(interrupt vector)** 를 가지고 있다. 인터럽트 백터란 인터럽트 종류마다 번호를 정해서 번호에 따라 처리해야 할 코드가 위치한 부분을 가리키는 자료구조를 말한다.

 
인터럽트 백터를 따라가면 실제 처리해야 할 코드는 **인터럽트 처리 루틴(Interrupt service routine)** 또는 **인터럽트 핸들러(Interrupt handler)** 라고 불리는 다른 곳에 정의된다.

```
인터럽트 처리 루틴(=Interrupt Service Routine, 인터럽트 핸들러)
해당 인터럽트를 처리하는 커널 함수를 말한다.
```

### 3. 인터럽트 당하기 직전으로 복원

 인터럽트 처리 루틴을 통해 해당되는 인터럽트 처리를 완료하고 나면 PCB에 저장한 수행중이던 원래 수행하던 작업으로 돌아가 중단되었던 일을 계속해서 수행한다.

# 데드락
```
Deadlock (= 교착 상태)
일련의 프로세스들이 서로가 가진 자원을 기다리며 Block 된 상태
```

Deadlock 발생의 4가지 조건
```
Mutual Exclusion (상호 배제)
- 매 순간 하나의 프로세스만이 자원을 사용할 수 있음

No Preemption (비선점)
- 프로세스는 자원을 스스로 내놓을 뿐 강제로 빼앗기지 않음

Hold and Wait (점유 대기)
- 자원을 가진 프로세스가 다른 자원을 기다릴 때, 보유 자원을 놓지 않고 
갖고 있음

Circular Wait (순환 대기)
- 자원을 기다리는 프로세스간, 사이클이 형성되어야함
```

데드락의 처리

자원 할당 시, 데드락의 4가지 조건 중, 어느 하나가 만족되지 않도록 하는 것

```
상호 배제 (Mutual Exclusion) 부정
- 여러 개의 프로세스가 공유 자원을 사용할 수 있도록 한다

비선점 (No Preemption) 부정
- Save & Restore 이 가능한 자원에서 선점(Preemption)을 허용한다

점유 대기 (Hold and Wait) 부정
- 프로세스 시작 시, 모든 자원을 할당한다
- 자원이 필요한 경우, 보유 자원을 놓는다

순환 대기 (Circular Wait) 부정
- 할당 순서를 정하여, 정해진 순서대로 자원을 할당한다
```

Deadlock Avoidance (교착상태회피)

- 자원 요청에 대한 부가적인 정보를 이용하여, 데드락의 가능성이 없는 경우에만 자원 할당

```
자원 할당 그래프 (Resource Allocation Graph)

- 각 자원의 타입이 한 개 씩 있는 경우 (Single Instance)
- 프로세스와 자원의 요청 및 할당 관계를 표시함
- Circular Wait 조건을 발견하기 위한 목적으로 사용
- 사이클을 형성 (단, 자원이 사이클을 형성하는 프로세스 외의 다른 프로세스들에게도 점유 당하고 있다면 제외) 한다면 데드락이 발생하는 경우
 

은행원 알고리즘 (Banker's Algorithm)

- 각 자원의 타입이 여러개 있는 경우 (Multiple Instance)
- 프로세스가 자원을 요구할 때, 시스템이 자원을 할당한 후 안정 상태로 남아있게 되는지를 사전에 검사하여 교착상태를 회피하는 방법
- 알고리즘을 이용해 안정 상태 인지 확인하고 안정 상태라면 자원을 할당하고 그렇지 않으면 다른 프로세스들이 자원을 해제할 때까지 대기
- 할당할 수 있는 자원의 수와 사용자의 수가 일정해야하고, 항상 불안정 상태를 방지해야 하므로 자원 이용도가 낮다는 단점을 지님
```

Deadlock Detection & Recovery (데드락 감지 및 회복)

데드락 발생은 허용하되, 그에 대한 감지를 하여 데드락 발견시 회복함
```
Detection
- Single Instance 의 경우 자원할당 그래프
- Multiple Instance 의 경우 Banker's Algorithm

Recovery
 - Process Termination
     - 데드락에 연관된 모든 프로세스를 죽임
 - Resource Preemption
     - 비용을 최소화할 Victim 프로세스를 선정하여 자원을 빼앗음
```

Deadlock Ignore
데드락을 시스템이 책임지지 않음

```
- 데드락이 매우 드물게 발생하므로, 데드락에 대한 조치 자체가 더 큰 overhead 일 수 있음
- 만약, 시스템에서 데드락이 발생한 경우, 프로그래머가 직접 process를 죽이는 방법으로 대처
- UNIX, Windows 등 대부분의 OS 가 채택
```



참고 : 

https://zangzangs.tistory.com/106#recentEntries

https://hibee.tistory.com/264

https://hibee.tistory.com/301