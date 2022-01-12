# 🎁 스케줄러 
## 📌 장기스케줄러
✔  역할
- 메모리는 한정되어 있는데 많은 프로세스들이 한꺼번에 메모리에 올라올 경우, 대용량 메모리(일반적으로 디스크)에 임시로 저장된다. 이 pool 에 저장되어 있는 프로세스 중 어떤 프로세스에 메모리를 할당하여 ready queue 로 보낼지 결정하는 역할을 한다.
    - ex) 지금 수행해야 할 job이 10개이지만 메모리에는 6개의 job만 올릴수 있는 상황일때, 10개중 어떤 스케줄러를 선택할지 결정


![](https://images.velog.io/images/kcwthing1210/post/db16867a-2a56-4cd3-aab3-f887aab4b904/image.png)

✔ 특징
- 메모리와 디스크 사이의 스케줄링을 담당.
- 프로세스에 memory(및 각종 리소스)를 할당(admit)
- degree of Multiprogramming 제어
  (실행중인 프로세스의 수 제어)
- 프로세스의 상태
- new -> ready(in memory)
- 가상 메모리의 발달로 time sharing system 에서는 장기 스케줄러가 없다.
    - ex) 메모리 허용범위가 6개라면 10개 중 6개의 프로세스를 고르는게 아닌 실행 준비가 되면 메모리로 10개가 다올라온다.

## 📌 단기스케줄러
✔  역할
- 실행이 준비된 프로세스들 중 하나를 선별해 CPU에게 할당
    - ex)장기 스케줄러에 의해 6개의 job이 메모리에 있을때, 6개 중 실제 CPU가 수행할 프로세스를 결정

![](https://images.velog.io/images/kcwthing1210/post/cd205f5a-fd02-4260-94e0-474e2da31556/image.png)

✔  특징
- CPU 와 메모리 사이의 스케줄링을 담당.
- Ready Queue 에 존재하는 프로세스 중 어떤 프로세스를 running 시킬지 결정.
- 프로세스에 CPU 를 할당(scheduler dispatch)
- 프로세스의 상태
    - ready -> running -> waiting -> ready
      ![](https://images.velog.io/images/kcwthing1210/post/4ef17a43-e945-4f4a-aa0a-7a6d87937029/image.png)
    - ex) A라는 프로세스가 수행되었다가 사용자의 입력을 기다려야 하는 상황 -> 기다리는 동안 CPU가 수행할 프로세스를 B로 교체 -> 이후 사용자가 입력 완료 후에 B에서 다시 A로 교체



## 📌 중기스케줄러
✔  역할
- 여유 공간 마련을 위해 프로세스를 통째로 메모리에서 디스크로 쫓아냄 (swapping)
    - ex) 장기 스케줄러에 의해 10개 프로그램 중 6개를 올렸으나, 6개가 CPU가 감당하기엔 너무 많을때, 이 6개 중 어떤 프로세스를 내려 보낼지 결정


    ![](https://images.velog.io/images/kcwthing1210/post/08ef8d07-334c-49a2-b9c0-335e6217bb0e/image.png)

✔ 특징
- 프로세스에게서 memory 를 deallocate
- degree of Multiprogramming 제어
- 현 시스템에서 메모리에 너무 많은 프로그램이 동시에 올라가는 것을 조절하는 스케줄러.
- 우선순위가 낮거나 일정 시간 동안 활성화 되지 않았던 프로세스를 내림
- 이렇게 필요에 따라 프로세스를 내리고 (swapping out), 다시 올리고 (swapping in) 하는 과정을 Swapping이라고 함 -> 중기 스케줄러를 Swapper라고 부르기도 함
- 프로세스의 상태
    - ready -> suspended
    - Suspended(stopped) : 외부적인 이유로 프로세스의 수행이 정지된 상태로 메모리에서 내려간 상태를 의미한다. 프로세스 전부 디스크로 swap out 된다. blocked 상태는 다른 I/O 작업을 기다리는 상태이기 때문에 스스로 ready state 로 돌아갈 수 있지만 이 상태는 외부적인 이유로 suspending 되었기 때문에 스스로 돌아갈 수 없다.

## 🧩 References
- https://jhnyang.tistory.com/372

# 🎁 CPU 스케줄러

스케줄링 대상은 Ready Queue 에 있는 프로세스들이다.

## 📌 선점형(preemptive) vs 비선점형(non-preemptive)
스케줄링은 다음과 같은 때에 일어난다.

- Running → Waiting 상태 : ( ex. I/O 요청, 자식프로세스 종료 - wait() 요청을 통해 종료 )
- Running → Terminate 상태 : ( ex. 부모프로세스의 종료 )
- Running → Ready 상태 : ( ex. 인터럽트 발생 )
- Waiting → Ready 상태 : ( ex. I/O 완료 )

✔ 비선점형
- Time-slice 가 없는 스케줄링
- CPU를 사용중인 프로세스가 자율적으로 반납하도록 하는 방식
- 따라서 프로세스가 자율적으로 CPU를 반납하는 시점에서 사용한다. [ 1, 2 번 시점 ]
  ![](https://images.velog.io/images/kcwthing1210/post/629e1927-8c37-41f2-93aa-04a417a35caf/image.png)

✔ 선점형
- 낮은 우선순위를 가진 프로세스보다 높은 우선순위를 가진 프로세스가 CPU를 선점하는 방식
- OS가 스케줄링의 알고리즘에 따라 적당한 프로세스에게 CPU를 할당하고, 필요시에는 회수하는 방식
- 일반적으로 3, 4 번 시점에서 사용하지만, 상황에 따라 1, 2 에서도 스케줄링이 가능하다.

![](https://images.velog.io/images/kcwthing1210/post/5be726f5-dc49-447e-8b7b-7501f50c1938/image.png)

## 📌 CPU 스케줄링 알고리즘의 목적
- No starvation : 각각의 프로세스들이 오랜시간동안 CPU를 할당받지 못하는 상황이 없도록 한다.
- Fairness : 각각의 프로세스에 공평하게 CPU를 할당해준다.
- Balance : Keeping all parts of the system busy

✔ Batch System [일괄처리 시스템]
: 온라인처럼 일에 대한 요청이 발생했을 때, 즉각적으로 처리하는 것이 아닌 일정기간 또는 일정량을 모아뒀다가 한번에 처리하는 방식

Throughput : 시간당 최대의 작업량을 낸다.
Turnaround time : 프로세스의 생성부터 소멸까지의 시간을 최소화한다.
CPU utilization : CPU가 쉬는 시간이 없도록 한다.

✔ Interactive System [대화형 시스템]
: 온라인과 같이 일에 대한 요청에 대해 즉각적으로 처리하여 응답을 받을 수 있는 시스템

Response time : 즉각적으로 처리해야하는 시스템이므로 요청에 대해 응답시간을 줄이는 게 중요하다.

✔ Time Sharing System
: 각 프로세스에 CPU에 대한 일정시간을 할당하여 주어진 시간동안 프로그램을 수행할 수 있게하는 시스템

Meeting deadlines : 데이터의 손실을 피하며, 끝내야하는 시간 안에 도달해야한다.
Predictability : 멀티미디어 시스템에서의 품질이 저하되는 부분을 방지해야한다.


## 📌 FCFS(First Come First Served)

✔ 특징
- 먼저 온 고객을 먼저 서비스해주는 방식, 즉 먼저 온 순서대로 처리.
- 비선점형(Non-Preemptive) 스케줄링
- 일단 CPU 를 잡으면 CPU burst 가 완료될 때까지 CPU 를 반환하지 않는다. 할당되었던 CPU 가 반환될 때만 스케줄링이 이루어진다.

✔ 문제점
- convoy effect
  소요시간이 긴 프로세스가 먼저 도달하여 효율성을 낮추는 현상이 발생한다.

## 📌 SJF(Shortest - Job - First)
✔ 특징
- 다른 프로세스가 먼저 도착했어도 CPU burst time 이 짧은 프로세스에게 선 할당
- 비선점형(Non-Preemptive) 스케줄링

✔ 문제점
- starvation
  효율성을 추구하는게 가장 중요하지만 특정 프로세스가 지나치게 차별받으면 안되는 것이다. 이 스케줄링은 극단적으로 CPU 사용이 짧은 job 을 선호한다. 그래서 사용 시간이 긴 프로세스는 거의 영원히 CPU 를 할당받을 수 없다.

## 📌 SRTF(Shortest Remaining Time First)
✔ 특징
- 새로운 프로세스가 도착할 때마다 새로운 스케줄링이 이루어진다.
- 선점형 (Preemptive) 스케줄링
- 현재 수행중인 프로세스의 남은 burst time 보다 더 짧은 CPU burst time 을 가지는 새로운 프로세스가 도착하면 CPU 를 뺏긴다.

✔ 문제점
starvation
- 새로운 프로세스가 도달할 때마다 스케줄링을 다시하기 때문에 CPU burst time(CPU 사용시간)을 측정할 수가 없다.

## 📌 Priority Schduling(우선 순위 스케줄링)
✔ 특징
- 우선순위가 가장 높은 프로세스에게 CPU 를 할당하는 스케줄링이다. 우선순위란 정수로 표현하게 되고 작은 숫자가 우선순위가 높다.
- 선점형 스케줄링(Preemptive) 방식
  더 높은 우선순위의 프로세스가 도착하면 실행중인 프로세스를 멈추고 CPU 를 선점한다.
- 비선점형 스케줄링(Non-Preemptive) 방식
  더 높은 우선순위의 프로세스가 도착하면 Ready Queue 의 Head 에 넣는다.

✔ 문제점
- starvation
  무기한 봉쇄(Indefinite blocking)
  실행 준비는 되어있으나 CPU 를 사용못하는 프로세스를 CPU 가 무기한 대기하는 상태

✔ 해결책
aging
아무리 우선순위가 낮은 프로세스라도 오래 기다리면 우선순위를 높여주자.

## 📌 Round Robin(RR)

✔ 특징
- 현대적인 CPU 스케줄링
- 각 프로세스는 동일한 크기의 할당 시간(time quantum)을 갖게 된다.
  할당 시간이 지나면 프로세스는 선점당하고 ready queue 의 제일 뒤에 가서 다시 줄을 선다.
- RR은 CPU 사용시간이 랜덤한 프로세스들이 섞여있을 경우에 효율적
- RR이 가능한 이유는 프로세스의 context 를 save 할 수 있기 때문이다.

✔ 장점
- Response time이 빨라진다.
  n 개의 프로세스가 ready queue 에 있고 할당시간이 q(time quantum)인 경우 각 프로세스는 q 단위로 CPU 시간의 1/n 을 얻는다. 즉, 어떤 프로세스도 (n-1)q time unit 이상 기다리지 않는다.
- 프로세스가 기다리는 시간이 CPU 를 사용할 만큼 증가한다.
  공정한 스케줄링이라고 할 수 있다.

✔ 주의할 점
설정한 time quantum이 너무 커지면 FCFS와 같아진다. 또 너무 작아지면 스케줄링 알고리즘의 목적에는 이상적이지만 잦은 context switch 로 overhead 가 발생한다. 그렇기 때문에 적당한 time quantum을 설정하는 것이 중요하다.


## 🧩 References
- https://github.com/JaeYeopHan/Interview_Question_for_Beginner/tree/master/OS#round-robin

- https://velog.io/@byunji_jump/%EC%9A%B4%EC%98%81%EC%B2%B4%EC%A0%9C-%EC%8A%A4%EC%BC%80%EC%A4%84%EB%9F%AC

- https://hyunah030.tistory.com/4