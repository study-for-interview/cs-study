# 이분 탐색 (Binary Search) 알고리즘

```
정렬되어 있는(이분 탐색의 주요 조건) 배열에서 데이터를 찾으려 시도할 때, 
순차탐색처럼 처음부터 끝까지 하나씩 모든 데이터를 체크하여 값을 찾는 것이 아니라
탐색 범위를 절반씩 줄여가며 찾아가는 Search 방법이다.
```
## 이분 탐색이란?
이분 탐색(Binary Search)은 결정 문제(Decision Problem)의 답이 이분적일 때 사용할 수 있는 탐색 기법입니다. 이때 결정 문제란 답이 Yes or No인 문제를 의미하며 (이분 탐색 문제에서는) 보통 1개의 parameter를 가집니다.

1 ~ 50까지 오름차순 정렬된 카드 더미에서 28번 카드를 찾는 문제를 예시로 이분 탐색을 알아보겠습니다. 

편의상 첫 번째 카드부터 i번째 카드는 v[i], 28은 val로 표기하겠습니다.

이 경우 **결정 문제를 "v[i] >= val인가?"로 잡으면 결정 문제의 답은 i가 증가함에 따라 F, F, ..., F, T, T, ..., T와 같이 분포**함을 알 수 있습니다. 

이때 **우리가 찾고자 하는 값은 처음으로 v[i] >= val인 지점, 즉 처음 결정 문제가 True가 되는 i**값입니다.

**이렇게 결정 문제의 parameter(이 경우 i)에 대해 결정 문제의 답이 두 구간으로 나뉘는 것을 "이분적이다"라고 하며 이런 경우 이분 탐색을 사용**해 결정 문제의 답이 달라지는 경계를 찾을 수 있습니다.

이분 탐색의 아이디어는 경계를 포함하는 구간 [lo, hi]을 잡은 뒤 구간의 길이를 절반씩 줄여나가며 lo, hi이 경계 지점에 위치하도록 하는 것입니다. 이분 탐색이 끝난 뒤엔 lo의 다음 칸은 hi(즉, lo + 1 == hi)이며 Check(lo) != Check(hi)입니다. 이때 Check(x)는 결정 문제의 parameter가 x일 때 결정 문제의 답을 의미합니다.

위의 예시에선 [1, 50] -> [25, 50] -> ... -> [27, 28]로 lo, hi를 줄여나간 뒤 hi = 28을 찾아주면 됩니다. 

**이분 탐색은 구간의 범위가 클 때 특히 효과적입니다.** 

만약 카드가 100만장 있었다고 하면 특정 카드를 하나하나 앞에서부터 찾으면 최대 100만번의 연산이 필요하지만, 이분 탐색을 이용하면 2^20 >= 1,000,000이기 때문에 최대 20번의 연산으로 원하는 카드를 찾을 수 있습니다.

+) 많은 최적화 문제는 이분 탐색으로 풀 수 있습니다. 최적화 문제란 어떤 조건(Check(x))을 만족하는 x의 최댓값 또는 최솟값을 찾는 문제를 말합니다. 이 경우 Check(x)가 x에 대해 이분적이면 이분 탐색을 사용할 수 있습니다.

# 구현 방법

이분 탐색의 구현은 Check(lo) != Check(hi)가 되도록 lo, hi의 초기값을 잘 설정해준 뒤 **lo + 1 < hi**인 동안 mid = (lo + hi) / 2를 구해서 **Check(lo) == Check(mid)라면 lo = mid를, Check(hi) == Check(mid)라면 hi = mid**를 해주면 됩니다.

우선 초기 상태의 lo, hi가 Check(lo) != Check(hi)이기 때문에 결정 문제의 답이 바뀌는 경계는 [lo, hi] 내에 있음이 보장됩니다.

이제 lo + 1 < hi인 동안 [lo, hi]를 [lo, mid] 또는 [mid, hi]로 줄여나가는데, 이 경우 Check(lo), Check(hi)는 바뀌지 않습니다. 

이유는 Check(lo) == Check(mid)라면 lo = mid를, Check(hi) == Check(mid)라면 hi = mid를 하기 때문입니다. 

또한 lo + 1 < hi이기 때문에 lo와 hi의 사이에는 무조건 한 개 이상의 칸이 있으며, mid는 항상 lo < mid < hi를 만족합니다. 

따라서 구간의 길이는 매번 절반씩 줄어들며 언젠간 lo + 1 == hi가 되어서 반복문을 탈출하게 됩니다.

(반복문을 탈출했다면 lo + 1 >= hi인데 lo < mid < hi인 mid를 대입하기 때문에 lo < hi이고, 두 조건을 만족하는 lo, hi는 lo + 1 == hi인 경우밖에 없습니다)

이분 탐색이 끝나면 lo, hi는 결정 문제의 답이 바뀌는 경계에 위치하게 되며, 만약 결정 문제 답의 분포가 F~T인데 정답이 가장 큰 F라면 lo를, 가장 작은 T라면 hi를 출력해주면 됩니다.

1. 경계를 포함하도록, 즉 Check(lo) != Check(hi)가 되도록 [lo, hi]를 잡음

![image](https://github.com/jinhan814/blog_image/blob/main/binary_search/fig1.png?raw=true)

2. Check(lo) == mid라면 lo = mid, 아니라면 hi = mid를 반복
![image](https://github.com/jinhan814/blog_image/blob/main/binary_search/fig2.png?raw=true)


![image](https://github.com/jinhan814/blog_image/blob/main/binary_search/fig3.png?raw=true)

3. lo + 1 == hi가 되면 탈출, lo, hi는 경계에 위치
![image](https://github.com/jinhan814/blog_image/blob/main/binary_search/fig4.png?raw=true)

# 시간 복잡도

처음부터 끝까지 원하는 값을 찾을 때까지 탐색을 계속하는 **순차 탐색은 Worst Case일 때 O(n)이라는 Time Complexity**를 보여준다.

10만개의 데이터가 있다면 무려 10만번을 탐색해야 하는 것이다.

그러나, **Binary Search는 탐색 대상을 절반씩 계속해서 줄여나가기 때문에, Worst Case일 때에도 탐색의 횟수가 log2n** 이 되므로 

10만개의 데이터가 있다고 하더라도 약 16번 정도로 탐색을 끝낼 수 있다.

 

**Time Complexity는 O(log n)**이다.


참고 : 

https://www.acmicpc.net/blog/view/109


출처: https://satisfactoryplace.tistory.com/39 [만족]
