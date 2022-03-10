# 이분탐색
* 검색 범위를 줄여나가면서 원하는 데이터를 검색하는 알고리즘
* 정렬된 리스트를 기반으로 데이터를 검색

<br> 

![img](https://blog.penjee.com/wp-content/uploads/2015/04/binary-and-linear-search-animations.gif)

<br> <br> 

## 이분탐색의 구현
* [일반적인 구현방법](https://namu.wiki/w/%EC%9D%B4%EC%A7%84%20%ED%83%90%EC%83%89?from=%EC%9D%B4%EB%B6%84%20%ED%83%90%EC%83%89)...
* 오름차순 정렬일때,
    * lower_bound : 탐색값보다 크거나 같은 첫번째 원소의 인덱스 (이상)
    * upper_bound : 탐색값보다 큰 첫번째 원소의 인덱스 (초과)
    * 구현이 쉬움, 예외처리가 쉬움

<br><br>

## lower_bound 구현 예시
~~~cpp
int lowerBoundEx(int l, int r){
    int s = l, e = r, mid;
    while(s<=e){
        mid = (s+e)/2;
        if(!isPossible(mid)) s = mid + 1;
        else e = mid - 1;
    }
    return s;
}
~~~

<br> <br> <br>

# 동적 계획법
* Dynamic Programming, DP
* 특정 범위까지의 값을 구하기 위해서 그것과 다른 범위까지의 값을 이용하여 효율적으로 값을 구하는 알고리즘 설계 기법
* 이전 결과값을 기억하고 다음 결과값 계산에서 이전 값들을 재활용하는 방법이다
* 다양한 알고리즘에서 시간복잡도를 줄이기 위해 사용되는 알고리즘
* 대표적인 예시
    * 피보나치 수열
    ~~~cpp
    // 탑다운DP
    int memo[100]{}; //메모이제이션 공간. 전역 변수이므로 0으로 초기화
    int fibonacci(unsigned int n) {
        if (n<=1) //0번째, 1번째 피보나치 수
            return n;
        if (memo[n]!=0) //메모가 있는지 확인(0으로 초기화되었으므로 0이 아니라면 메모가 쓰인 것임)
            return memo[n]; //메모 리턴
        memo[n]=fibonacci(n-1) + fibonacci(n-2); //작은 문제로 분할
        return memo[n];
    }
    ~~~

<br> <br>

## 메모이제이션 (Memoization)
* 동일한 계산을 반복해야 할 경우 한 번 계산한 결과를 메모리에 저장해 두었다가 꺼내 씀으로써 중복 계산을 방지할 수 있게 하는 기법
* 메모리라는 공간 비용을 투입해 계산에 소요되는 시간 비용을 줄이는 방식
* 캐싱(caching)

<br><br><br>

## 동적 계획법 구현방법
* Top-Down
    * 위에서 내려오는 것, 즉, 큰 문제부터 시작해서 계속 작은 문제로 분할해 가면서 푸는 것
    * 예시
    ~~~cpp
    int memo[100]{}; //메모이제이션 공간. 전역 변수이므로 0으로 초기화
    int fibonacci(unsigned int n) {
        if (n<=1) //0번째, 1번째 피보나치 수
            return n;
        if (memo[n]!=0) //메모가 있는지 확인(0으로 초기화되었으므로 0이 아니라면 메모가 쓰인 것임)
            return memo[n]; //메모 리턴
        memo[n]=fibonacci(n-1) + fibonacci(n-2); //작은 문제로 분할
        return memo[n];
    }
    ~~~

<br>

* Bottom-Up
    * 바닥에서 올라오는 것, 즉, 작은 문제부터 시작해서 작은 문제를 점점 쌓아 큰 문제를 푸는 것
    * 예시
    ~~~cpp
    int N;
    int arr[N+1]{}; // N 번째 피보나치 수열값

    int main(){
        // ...
        arr[1] = arr[2] = 1;
        for(int i=3; i<=N; i++){
            arr[i] = arr[i-1] + arr[i-2];
        }
        cout<<arr[N];
    }
    ~~~

<br> <br> <br>

## 동적 계획법 모델화 하기
* [해당글](https://www.secmem.org/blog/2020/10/24/dp/) 참고
* 동적 계획법은 대부분 그래프, 그 중에서도 사이클이 없는 유향 그래프(DAG) 로 모델화됨
* 동적 계획법을 모델화한 그래프를 이루는 요소는 다음과 같음
    * 정점: 문제에서의 특정 상황을 유일하게 결정지을 수 있는 변수들로 이루어진 상태
    * 간선: 상태간의 전이를 나타내는 점화식
    * 상태중에서 다른 상태와의 관계로 표현되지 않고 특정 상수를 답으로 가지게 되는 상태들도 존재하는데, 이들을 **기저 상태**라고 함
    * 위의 피보나치 Bottom-up 코드에서는 
        * **arr[N+1]** : 상태
        * **arr[1] = arr[2] = 1** : 기저 상태
        * **arr[i] = arr[i-1] + arr[i-2]** : 점화식
        
<br> <br>





