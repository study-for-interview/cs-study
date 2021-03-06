# 프로세스 상태

![image](https://media.geeksforgeeks.org/wp-content/uploads/20190604122001/states_modified.png)
프로세스 상태

- New (Create) - 이 단계에서 프로세스가 생성될 예정이지만 아직 생성되지 않은 상태이며 OS가 프로세스를 생성하기 위해 선택하는 것은 보조 메모리에 있는 프로그램입니다.

- Ready - 새로 만들기 -> 실행할 준비가 되었습니다. 프로세스가 생성된 후 프로세스는 준비 상태가 됩니다. 즉 프로세스가 메인 메모리에 로드됩니다. 여기에서 프로세스는 실행할 준비가 되었으며 실행을 위한 CPU 시간을 얻기 위해 기다리고 있습니다. CPU에서 실행할 준비가 된 프로세스는 준비된 프로세스를 위해 큐에 유지됩니다.

- Run - 프로세스는 실행을 위해 CPU에 의해 선택되고 프로세스 내의 명령은 사용 가능한 CPU 코어 중 하나에 의해 실행됩니다.

- Blocked or wait - 프로세스가 I/O에 대한 액세스를 요청하거나 사용자의 입력이 필요하거나 임계 영역(이미 획득한 잠금)에 대한 액세스가 필요할 때마다 차단 또는 대기 상태가 됩니다. 프로세스는 주 메모리에서 계속 대기하며 CPU가 필요하지 않습니다. I/O 작업이 완료되면 프로세스가 준비 상태가 됩니다.

- Terminated or completed - 프로세스가 종료 되고 PCB가 삭제됩니다.

- Suspend ready -  처음에 준비 상태에 있었지만 주 메모리에서 스왑되어(가상 메모리 항목 참조) 스케줄러에 의해 외부 저장소에 배치된 프로세스는 일시 중단 준비 상태에 있다고 합니다. 프로세스가 다시 주 메모리로 가져올 때마다 프로세스는 준비 상태로 다시 전환됩니다.

- Suspend wait or suspend blocked - suspend ready와 유사하지만 I/O 작업을 수행하던 프로세스를 사용하고 주 메모리가 부족하여 보조 메모리로 이동합니다.
작업이 완료되면 대기 모드로 전환될 수 있습니다.

<br>

# 프로세스 큐(Queue)
![image](https://user-images.githubusercontent.com/34755287/53879660-5ccdd500-4052-11e9-972d-11ba3faeb3e3.png)

프로세스는 수행하면서 상태가 여러 번 변하는데 이에 따라 서비스를 받아야하는 곳이 다르다. 

그리고 프로세스는 일반적으로 여러 개가 한 번에 수행되므로 그에 따른 순서가 필요하다. 이러한 순서를 대기하는 곳을 큐(queue)라고 부른다.

- Job Queue: 하드디스크에 있는 프로그램이 실행되기 위해 메인 메모리의 할당 순서를 기다리는 큐이다.
- Ready Queue: CPU 점유 순서를 기다리는 큐이다.
- Device Queue: I/O를 하기 위한 여러 장치가 있는데, 각 장치를 기다리는 큐가 각각 존재한다.

<br>

# 프로세스 스케줄링

## 프로세스 스케쥴링의 의미
     프로세스를 CPU에게 할당하는 과정

- 스케줄러의 종류
    
    ![image](https://blog.kakaocdn.net/dn/Agip3/btqQjnr5Aht/gpoM6F9C8nyOY6aPI4oY5k/img.png)

    - 장기 스케줄러

       > 작업 스케줄러라고도 부르며 어떤 프로세스를 준비 큐에 삽입할지를 결정하는 역할을 합니다.

       - 디스크에서 하나의 프로그램을 가져와 커널에 등록하면 프로세스가 되는데 이때 어떤 프로그램을 가져와 커널에 등록할지(준비큐에 등록할지) 결정합니다.

       - 장기 스케줄러는 메모리에 동시에 올라가 있는 프로세스의 수를 조절하는 역할을 합니다.

       - 장기 스케줄러는 수십 초 내지 수 분 단위로 가끔 호출되기 때문에 상대적으로 속도가 느린 것이 허용됩니다. 

       -  현대의 시분할 시스템에서 사용되는 운영 체제에는 일반적으로 장기 스케줄러를 두지 않는 경우가 대부분인데 과거에는 적은 양의 메모리를 많은 프로세스들에게 할당하면 프로세스당 메모리 보유량이 적어져 장기 스케줄러가 이를 조절하는 역할을 했지만 현대의 운영체제에서는 프로세스가 시작되면 장기 스케줄러 없이 바로 프로세스에 메모리를 할당해 준비 큐에 넣어주게됨.
       
       

    - 단기 스케줄러

       > CPU스케줄러라고도 하며 준비 상태의 프로세스 중에서 어떤 프로세스를 다음 번에 실행 상태로 만들 것인지를 결정합니다. 

        - 시분할 시스템에서 타이머 인터럽트가 발생하면 단기 스케줄러가 호출됩니다.
        - 일반적으로 스케줄러라 함은 단기 스케줄러를 의미하며 단기 스케줄러는 미리 정한 스케줄링 알고리즘에 따라 cpu를 할당 할 프로세스를 선택합니다.
        - 단기 스케줄러는 밀리 세컨트(ms) 이하의 시간 단위로 매우 빈번하게 호출되기 때문에 수행 속도가 충분히 빨라야 합니다.

        <hr>

        ![image](https://blog.kakaocdn.net/dn/Eh3sZ/btqQu5iYVgB/zV9REbJw0v8tCaWIFnmk61/img.png)

    - 중기 스케줄러

        > 너무 많은 프로스스에게 메모리를 할당해 시스템의 성능이 저하되는 경우 이를 해결하기 위해 메모리에 적재된 프로세스의 수를 동적으로 조절하기 위해 추가된 스케줄러 입니다. 
        -  프로세스 당 보유하고 있는 메모리량이 극도로 적어지게 되면 CPU 수행에 당장 필요한 프로세스의 주소 공간조차도 메모리에 올려놓기 어려운 상황이 발생

                -> 이런 경우 메모리에 올라와 있는 프로세스 중 일부로 부터 메모리를 통째로 빼앗아 그 내용을 디스크의 스왑 영역에 저장해 둡니다. 이와 같은 행위를 스왑 아웃(swap out)이라고 합니다.

                -> 디스크로 스왑 아웃시켜야 하는 경우 봉쇄 상태에 있는 프로세스들을 첫번째로 스왑 아웃 시킵니다. 이유는 봉쇄 상태의 프로세스들은 당장 CPU를 획득할 가능성이 없기 때문 입니다. 

                -> 봉쇄 상태의 프로세스들을 스왑 아웃시켜도 문제가 해결되지 않는 경우 중기 스케줄러는 타이머 인터럽트가 발생해 준비 큐로 이동하는 프로세스를 추가적으로 스왑아웃 시킵니다. 
                
        - 중기 스케줄러는 이러한 방식으로 장기 스케줄러와 마찬가지로 메모리에 올라와 있는 프로세스의 수를 조절하는 역할을 합니다.

        ※봉쇄상태 : 프로세스에게 CPU를 주어도 당장 명령을 실행할 수 없는 상태.

<br>
<hr>

# CPU 스케줄링

사용자 프로그램이 수행되는 과정을 보면 CPU 작업과 I/O 작업의 반복됩니다.

CPU 스케줄링은 CPU를 사용하는 패턴이 상이한 여러 프로그램이 동일한 시스템 내부에서 함께 실행되기 때문에 CPU자원을 효율적으로 사용하기 위해서 스케줄링 기법이 필요합니다.

### CPU 스케줄링 알고리즘
- 단기스케줄러에서 사용하며 준비 상태의 프로세스(Ready Queue)중에서 어떤 프로세스에게 CPU를 할당할지를 결정합니다.

CPU스케줄링 방식

    - 비선점형 방식 
        - CPU를 획득한 프로세스가 스스로 CPU를 반납하기 전까지 CPU를 빼앗기지 않는 방법

    - 선점형 방식
        - 프로세스가 CPU를 계속 사용하기를 원하더라도 강제로 빼앗을 수 있는 스케줄링 방법
        - 낮은 우선순위를 가진 프로세스보다 높은 우선순위를 가진 프로세스가 CPU를 선점하는 방식
    
    
### FCFS
<br>
특징

    - 비선점형(Non-Preemptive) 스케줄링
    - FCFS(First Come First Served) 스케줄링은 프로세스가 준비 큐에 도착한 시간 순서대로 CPU를 할당하는 방식
    -  CPU를 먼저 요청한 프로세스에게 CPU를 먼저 할당하고, 그 프로세스가 자발적으로 CPU를 반납할 때까지 CPU를 선점하지 않습니다.
    
    - 장점 : 
        - FIFO 큐를 사용하기 때문에 알고리즘 구현이 쉬운편이고, 배치시스템에 좋다.
    - 단점 :
        - 긴 작업이 짧은 작업을 오랫동안 기다리게 하는 경우도 있기 때문에 평균 대기시간이 길어진다.  
        또한, 중요하지 않은 작업이 중요한 작업을 기다리게 할 수 있다.

    즉, CPU 작업이 긴 프로세스가 먼저 도착할 경우 평균 대기시간이 길어지고 CPU 작업이 짧은 프로세스가 먼저 도착하게 되면 평균 대기시간은 짧아지게 됩니다.

<br>

### SJF
<br>
특징

    - 비선점형(Non-Preemptive) 스케줄링
    - CPU 버스트(작업시간)이 가장 짧은 프로세스에게 제일 먼저 CPU를 할당하는 방식입니다.
    - 기아 현상 발생 가능성 有

<br>

### SRTF(Shortest Remaining Time First)
<br>
특징

    - 새로운 프로세스가 도착할 때마다 새로운 스케줄링이 이루어진다.
    - 선점형 (Preemptive) 스케줄링
    - 현재 수행중인 프로세스의 남은 burst time 보다 더 짧은 CPU burst time 을 가지는 새로운 프로세스가 도착하면 CPU 를 뺏긴다.

    문제점 : 새로운 프로세스가 도달할 때마다 스케줄링을 다시하기 때문에 CPU burst time(CPU 사용시간)을 측정할 수가 없다.

<br>

### Priority scheduling
<br>
특징

    - 비선점형(Non-Preemptive) 스케줄링 + 선점형 (Preemptive) 스케줄링
    - 높은 우선순위를 가진 프로세스에게 CPU를 할당
    - 선점형 스케줄링(Preemptive) 방식 더 높은 우선순위의 프로세스가 도착하면 실행중인 프로세스를 멈추고 CPU 를 선점한다.
    - 비선점형 스케줄링(Non-Preemptive) 방식 더 높은 우선순위의 프로세스가 도착하면 Ready Queue 의 Head 에 넣는다.
    - 만약 우선순위가 같을 경우 FCFS 순서로 처리된다.


    문제점과 에이징 방법
    우선순위 알고리즘의 주요한 문제는 무한 정지와 기아상태 이다.

    예를 들어 실행 준비가 되었으나 우선순위가 높은 프로세스가 계속 들어오면 우선순위가 낮은 프로세스는 무한정 대기해야 하는 상황이 발생한다. 이러한 기다림을 해결하는 방법이 바로 에이징이다.   

    에이징은 매 분마다 대기 중인 프로세스의 우선순위를 1씩 증가시킨다.

    그러면 초기에 우선순위가 0이었단 프로세스가 대기중이면 프로세서를 점유중인 프로세스보다 우선순위가 높아지는 시점이 발생하여 무한 정지와 기아상태를 해결할 수 있다.

### RR(Round Robin)
<br>
특징

    - 선점형 (Preemptive) 스케줄링
    - 라운드 로빈 스케줄링(Round Robin Scheduling, RR)은 시분할 시스템을 위해 설계된 선점형 스케줄링의 하나로서, 프로세스들 사이에 우선순위를 두지 않고, 순서대로 시간단위(Time Quantum/Slice)로 CPU를 할당하는 방식의 CPU 스케줄링 알고리즘입니다.
    


<hr>

스케줄링의 성능 평가

스케줄링 기법의 성능을 평가하기 위해 여러 지표들이 사용되는데, 이들 지표들은 크게 시스템 관점과 사용자 관점으로 나누어볼 수 있다.

 

- 시스템 관점 : CPU활용도와 처리량

- 사용자 관점 : 소요시간, 대기시간, 응답 시간 등 기다리는 시간

 

1. CPU 활용도

    전체 시간 중에서 CPU가 일을 한 시간의 비율을 나타냅니다. CPU는 대부분의 시스템에서 하나만 존재하기 때문에 CPU가 일을 하지 않고 휴면상태에 머무르는 시간을 최대한 줄이는 것이 스케줄링의 중요한 목표 입니다. 

 

2. 처리량

    주어진 시간 동안 준비 큐에서 기다리고 있는 프로세스 중에서 몇 개를 끝마쳤는지를 나타냅니다. 즉 CPU의 서비스를 원하는 프로세스 중 몇개가 원하는 만큼의 CPU를 사용하고 이번 CPU 버스트를 끝내어 준비큐를 떠났는지를 측정하는 것이 처리량의 개념입니다. 처리량을 높이기 위해서는 CPU 버스트가 짧은 프로세스에게 우선적으로 CPU를 할당 하는것이 유리합니다.

 

3. 소요시간

    프로세스가 CPU를 요청한 시점부터 자신이 원하는 만큼 CPU를 다 쓰고 CPU 버스트가 끝날 때까지 걸린 시간을 뜻합니다. 이는 준비 큐에서 기다린 시간과 실제로 CPU를 사용한 시간의 합을 의미합니다. 

    예를 들어 CPU를 사용하다 I/O 연산을 위해 CPU를 자진 반납했다면 CPU를 사용하기 위해 준비 큐에 들어왔을 때 부터 CPU를 자진 반납하기 전까지 걸린 시간이 됩니다.

 

4. 대기 시간

    프로세스가 준비 큐에서 CPU를 얻기 위해 기다린 시간의 합을 의미합니다. 하나의 프로세스는 CPU를 할당받아 일을 하다 준비 큐에 대기하고, 다시 CPU를 할당받고 위의 과정을 작업을 마무리 할때까지 반복하는데 이때 준비큐에서 CPU를 받기 위해 대기한 시간의 합을 의미합니다.

 

5. 응답 시간

    준비 큐에 들어온 후 첫번째 CPU를 획득하기 까지 기다린 시간을 의미합니다.

 

<hr>
    참고 : 

    https://www.geeksforgeeks.org/process-schedulers-in-operating-system/?ref=lbp

    https://kosaf04pyh.tistory.com/191
    
    https://jhnyang.tistory.com/372

    https://kosaf04pyh.tistory.com/194?category=1032510
    