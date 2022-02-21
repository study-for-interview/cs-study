# Array

# 배열이란? 

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fbd43Xq%2FbtqCdhsqTEm%2FOY443quFrvrViVQY5DeunK%2Fimg.png)

## 배열의 성질

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbswV64%2FbtqCgmM4qgo%2FSUhmz0ZfBsKYA5XEAd9PsK%2Fimg.png)

1. 배열은 메모리 상에 원소를 연속하게 배치한 자료구조로 k번째 원소의 위치를 바로 계산할 수 있습니다. 

    시작 주소에서 k칸 만큼 오른쪽으로 가면 되기 떄문입니다.

    그래서 k번째 원소를 찾거나 변경하기 위한 시간복잡도는 O(1)로 표기할 수 있습니다.

2. 두번째로 메모리는 다른 자료구조와 다르게 추가적으로 메모리의 양이 거의 없습니다.

3. 메모리상에 데이터들이 붙어 있기 때문에 cache hit rate가 높습니다.

4. 메모리 상에 연속한 구간을 잡아야 하니 할당에서 다소 제약이 있습니다.

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fcnlfnn%2FbtqCdhlGlh5%2FmqKZZnSI9FpyRLRF33XGhK%2Fimg.png)

---

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbvsHZp%2FbtqCewJsHRP%2F3FeObO6upMoMCo95fiEZX0%2Fimg.png)

---

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FD9NxG%2FbtqCd1QmACM%2FhGYKL6iWx2WYIR9UZVNeV0%2Fimg.png)

---

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fds4SmU%2FbtqCeu5WvL4%2FmmErDdR3Qxj8WrlphG53kk%2Fimg.png)

임의의 위치에 원소를 추가하는 과정은 O(N)이 됩니다.

보면 5번에 15를 추가했는데, 이렇게 되면 그 뒤의 원소들을 전부 한 칸씩 밀어야해서 O(N)이 필요하게 됩니다. 

---

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fc4Aqqr%2FbtqCjem2z8D%2FlP4CwXtkFYzXWspi0uYChK%2Fimg.png)

 임의의 위치에 원소를 제거하는 것도 O(N)이 됩니다. 2번 원소를 지웠다고 치면 그 이후에 있던 모든 원소들을 한 칸씩 땡겨와야해서 그렇습니다. 
 
 2번 원소만 비워두면 안되냐고 생각하실수도 있지만 그렇게 되면 더 이상 메모리 상에 원소가 연속해서 존재하지 않기 때문에 배열의 정의에도 위배되고 또 k번째 원소를 O(1)에 찾을 수가 없게 됩니다.

자료구조 배열의 특징 정리 

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Ftj322%2FbtqCimMm5pG%2FvjcWEbEPEdztFkQak5Nx60%2Fimg.png)

# Array(배열)의 장/단점

## 장점
- Index를 통해 원소에 O(1) 시간복잡도 만에 빠르게 접근할 수 있다.

## 단점
- 새로운 원소를 삽입하고 삭제하는데 O(N) 시간복잡도가 걸려 느리다.

- 연속된 메모리 상에 원소들이 존재하므로 처음 배열을 선언한 크기만큼 데이터를 저장하지 않는다면 메모리 낭비가 발생한다.
- 예를 들어, 배열 선언시 배열의 크기를 10으로 선언했는데 3개의 원소에만 데이터를 저장했을 경우 7개의 원소는 비어있게 되므로 7개 원소가 차지하는 메모리 공간만큼 낭비가 발생하게 된다.


## 배열을 언제 사용해야 좋을까?

    - 데이터 개수가 확실하게 정해져 있을 때 데이터 저장을 위한 자료구조로 선택하면 좋다.

    - 또한, 삽입/삭제 작업이 적을 때 사용하면 좋다.

    - 마지막으로 배열에 저장된 데이터를 검색하는 작업이 많을 때 사용하면 좋다.(인덱스로 빠르게 검색 가능)

---


출처 : 

https://blog.encrypted.gg/927?category=773649

https://choheeis.github.io/newblog//articles/2020-12/data-structure-array

