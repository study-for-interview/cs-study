# Queue

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FZce3U%2FbtqBDaOfGU5%2FRc2kR3Puqi3QiQa3o6CPL1%2Fimg.png)

Queue 의 사전적 의미는 1. (무엇을 기다리는 사람, 자동차 등의) 줄 , 혹은 줄을 서서 기다리는 것을 의미한다.

따라서 일상생활에서 놀이동산에서 줄을 서서 기다리는 것, 은행에서 먼저 온 사람의 업무를 창구에서 처리하는 것과 같이

선입선출(FIFO, First in first out) 방식의 자료구조를 말한다. 

Queue는 자료의 한 쪽 끝에서 자료가 삽입되고

그 반대쪽 끝에서 자료가 삭제되는 구조이다.

자료의 추가는 Enqueue, 삭제는 Dequeue라고 부른다.

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbcgPYi%2FbtqwDKdQQyr%2FsBgA4M4TkTR0D5MIZcFmr1%2Fimg.png)
![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FrNlZC%2FbtqwDtwExys%2F1sgSD1LAMvMnmPZryTwgbK%2Fimg.png)



연산 시간 복잡도
| 연산 | 시간복잡도 |
| --- | --- |
| Insertion | O(1) | 
| Deletion | O(1) | 
| Search | O(n) | 

# 큐의 활용 예시

큐는 주로 데이터가 입력된 시간 순서대로 처리해야 할 필요가 있는 상황에 이용한다.

- 우선순위가 같은 작업 예약 (프린터의 인쇄 대기열)
- 은행 업무
- 콜센터 고객 대기시간
- 프로세스 관리
- 너비 우선 탐색(BFS, Breadth-First Search) 구현
- 캐시(Cache) 구현


# Heap

힙 자료구조는 완전 이진 트리를 기초로 하는 자료구조입니다. 완전 이진트리는 마지막을 제외한 모든 노드에서 자식들이 꽉 채워진 이진트리를 말합니다.

![image](https://media.vlpt.us/images/emplam27/post/d33ee896-7638-4c80-a03d-219b1200534c/%ED%9E%99%20-%201.png)

그림과 같은 형태를 띄고있으며, 몇가지 특징들을 가지고 있습니다.

1. 힙은 **최대힙(Max heap)과 최소힙(Min Heap)**으로 나눠집니다. 최대힙은 부모노드의 값이 자식노드들의 값보다 항상 크고, 최소힙은 부모노드의 값이 자식노드의 값보다 항상 작습니다. (위 그림은 최대힙의 예시)
이러한 성질 때문에 항상 느슨한 정렬상태(반정렬 상태)를 유지합니다.

2. 힙은 중복값을 허용합니다. 힙은 최댓값 또는 최솟값을 쉽게 뽑기 위한 자료구조 임으로 중복을 허용합니다.

# 힙을 배열로 구현하기
힙은 대체적으로 배열로 구현됩니다. 완전이진트리를 기본으로 하기 때문에 비었는 공간이 없어 배열로 구현하기에 용이합니다.

아래 그림과 같이 루트노드를 배열의 0번 index에 저장하고, 각 노드를 기점으로 왼쪽 자식노드는 a[i∗2+1], 오른쪽 자식노드는 a[i∗2+2] 의 index에 저장됩니다. 또한 특정 index의 노드에서 부모노드는 a[(i−1)//2]로 찾을 수 있습니다.

![image](https://media.vlpt.us/images/emplam27/post/4a05c33e-2caf-4b28-964c-7019c13ff34b/%ED%9E%99%20-%20%EB%B0%B0%EC%97%B4%EB%A1%9C.png)

10 - 0번 , 10의 왼쪽 자식 노드인 9 -> 1,  오른쪽 자식노드인 5 -> 2번에 위치

# 삽입과 삭제로 깨진 힙을 재구조화하기(heapify)

최대힙의 부모노드는 항상 자식노드의 값보다 크다는 조건을 가지고 있습니다. 하지만 힙에서 삽입 또는 삭제가 일어나게 되면 경우에 따라 최대힙의 조건이 깨질 수 있습니다. 

이러한 경우에 최대힙의 조건을 만족할 수 있게 노드들의 위치를 바꿔가며 힙을 재구조화(heapify) 해주어야 합니다.

삽입과 삭제의 경우 모두 연산 자체는 O(1)로 작동하지만 heapify의 과정을 거치기 때문에 O(logn)의 시간복잡도를 가지게 됩니다.

## 삽입 과정 구현과정

새로운 노드가 삽입되었을 경우입니다. 새로운 노드는 가장 말단에 있는 노드의 자식 노드로 추가됩니다. 

이후, 부모노드와 비교하면서 재구조화 과정을 수행합니다. 삽입과정은 아래에서 위로 재구조화 과정이 이루어지게 됩니다.


![image](https://media.vlpt.us/images/emplam27/post/5afbb3d1-83b3-4fdb-98c9-5969296f43f0/%ED%9E%99%20-%20%EB%85%B8%EB%93%9C%20%EC%82%BD%EC%9E%85.png)

# 삭제 구현과정

삭제되었을 경우입니다.

루트노드가 삭제되면 가장 말단노드를 루트노드자리에 대체한 후 재구조화 과정을 수행합니다. 

힙으로 구현된 우선순위 큐에서도 가장 우선순위가 큰 루트노드를 주로 삭제합니다. 

삽입의 경우에는 가장 말단노드에 추가하여 재구조화 과정을 수행하면 됩니다. 삭제과정은 위에서 아래로 재구조화 과정이 이루어지게 됩니다.

![image](https://media.vlpt.us/images/emplam27/post/d9151cfd-aec6-4f48-87ce-30eef782feb1/%ED%9E%99%20-%20%ED%9E%99%20%EC%9E%AC%EA%B5%AC%EC%A1%B0.png)

# 힙이 아닌 배열을 힙으로 만들기(build heap)

heapify의 경우 기본적으로 힙을 만족하는 경우에서 삽입 또는 삭제가 발생할 때 O(logn)의 시간복잡도로 다시 힙으로 만드는 과정입니다. 

 build heap은 이와 다르게 아예 힙의 조건을 만족하지 않는 배열을 힙으로 만드는 과정입니다. 여러번의 heapify 과정을 거치기 때문에 결과적으로 시간복잡도는 O(nlogn)입니다.

## 재귀함수를 이용한 재구조

재귀함수 과정으로 아랫방향 재구조를 실행할 수 있습니다.아래 과정에서는 해당 재구조 방법을 사용하겠습니다.

## 구현과정

build heap의 과정은 가장 말단의 부모-자식 노드에서부터 시작합니다. 부모노드가 될 수 있는 노드들만을 골라서 진행한다고 생각하면 편할 것 같습니다. 

가장 뒤에서부터 heapify가 진행되기 때문에 그림의 4번과정 같은 경우를 보면 모든 자식트리들은 이미 힙의 구조를 만들고 있어 heapify가 가능해집니다.

![image](https://media.vlpt.us/images/emplam27/post/b7a8132a-ec63-447d-9b98-a880b06938cf/%ED%9E%99%20-%20%EB%B0%B0%EC%97%B4%EC%9D%84%20%ED%9E%99%EC%9C%BC%EB%A1%9C.png)


참고 : 

https://velog.io/@emplam27/%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0-%EA%B7%B8%EB%A6%BC%EC%9C%BC%EB%A1%9C-%EC%95%8C%EC%95%84%EB%B3%B4%EB%8A%94-%ED%9E%99Heap

