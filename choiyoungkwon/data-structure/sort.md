# 정렬이란?
• 주어진 자료들을 어떤 기준에 의하여 크기 순서대로 나열한 것

• 정렬 알고리즘의 핵심 요소는 교환, 선택, 삽입이며 대부분의 정렬 알고리즘은 이 세가지 요소를 응용한 것입니다.

• 데이터를 정렬해야 하는 이유는 탐색을 효율적으로 하기 위해서 입니다.



# 선택 정렬 
선택 정렬 : 잘못된 위치에 들어가 있는 원소를 찾아 그것을 올바른 위치에 집어넣는 원소 교환으로 정렬을 하는 방법이다.

그래서 먼저 작은 원소를 찾아 첫 번째 위치에 있는 원소와 교환하고 다음에는 두 번째로 작은 원소를 찾아 두 번째 위치에 있는 원소와 교환한다. 이렇게 매번 나머지(a[i] ... a[n-1]) 원소 중에서 가장 작은 원소를 찾아 a[i] 원소와 교환하는 작업을 모든 원소가 올바른 위치에 있게 될 때까지 계속하면 원하는 오름차순 정렬이 된다.

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbOtV5X%2FbtqLW767SbK%2FGDrx33RNajdivKkJcip8Gk%2Fimg.png)

단순 선택 정렬 과정

```java
package chap06;
import java.util.Scanner;
// 단순 선택 정렬

class SelectionSort {
	// 배열 요소 a[idx1]과 a[idx2]의 값을 바꿉니다.
	static void swap(int[] a, int idx1, int idx2) {
		int t = a[idx1]; a[idx1] = a[idx2]; a[idx2] = t;
	}

	// 단순 선택 정렬
	static void selectionSort(int[] a, int n) {
		for (int i = 0; i < n - 1; i++) {
			int min = i;			// 아직 정렬되지 않은 부분에서 가장 작은 요소의 인덱스를 기록합니다.
			for (int j = i + 1; j < n; j++)
				if (a[j] < a[min])
					min = j;
			swap(a, i, min);		// 아직 정렬되지 않은 부분의 첫 요소와 가장 작은 요소를 교환합니다.
		}
	}

	public static void main(String[] args) {
		Scanner stdIn = new Scanner(System.in);

		System.out.println("단순 선택 정렬");
		System.out.print("요솟수：");
		int nx = stdIn.nextInt();
		int[] x = new int[nx];

		for (int i = 0; i < nx; i++) {
			System.out.print("x[" + i + "]：");
			x[i] = stdIn.nextInt();
		}

		selectionSort(x, nx);			// 배열x를 단순선택정렬

		System.out.println("오름차순으로 정렬했습니다.");
		for (int i = 0; i < nx; i++)
			System.out.println("x[" + i + "]＝" + x[i]);
	}
}
```


# 버블 정렬

버블 정렬은 배열을 검사하여 두 인접한 원소가 정렬 순서에 맞지 않으면 이들을 서로 교환하고 이것을 반복한다.

즉, 먼저 a[0]과 a[1]을 비교하여 정렬 순서에 맞지 않으면 서로 교환한다.

다음 a[1]과 a[2]를 다시 비교하여 순서에 맞지 않으면 교한하는데 이 과정을 a[n-2]와 a[n-1]이 될 때까지 반복한다.

이렇게 하면 가장 큰 원소가 배열의 n-1위치로 끌어 오르게(bubbled up) 된다.

그러나 이것은 배열 전체에 대한 첫 번째 패스이며 이 정렬은 다시 배열 처음부터 인접한 원소를 비교하여 순서가 맞지 않으면 교환하면서 검사하게 되는데 이 때는 마지막 비교가 a[n-3]과 a[n-2]가 된다.

왜냐하면 제일 큰 원소는 이미 위치 n-1에 선정되어 있기 때문이다.

이 과정은 마지막 패스로 a[0]과 a[1]을 비교하여 순서가 맞지 않으면 서로 교환할 때까지 계속한다.


![image](https://blog.kakaocdn.net/dn/KDI4J/btqLRjHZxpn/0GRLRpplz7KqS8POOpKQ51/img.gif)

버블 정렬

# 버블 정렬의 시간복잡도

비교 횟수

- 최상, 평균, 최악 모두 일정
- n-1, n-2, ... 2, 1 번 = n(n-1)/2

교환 횟수

- 입력 자료가 역순으로 정렬 되어 있는 최악의 경우, 한 번 교환하기 위하여 3번의 이동(SWAP 함수의 작업)이 필요하므로 (비교 횟수 *3 )번 = 3n(n-1) /2
- 입력 자료가 이미 정렬 되어 있는 최상의 경우, 자료의 이동이 발생하지 않는다.


# 삽입 정렬
단순 삽입 정렬은 선택한 요소를 그보다 더 앞쪽의 알맞은 위치에 삽입하는 작업을 반복하여 정렬하는 알고리즘 입니다.

단순 삽입 정렬은 2번째 요소부터 선택하여 진행합니다.

4는 6보다 앞에 위치해야 하므로 앞쪽에 삽입합니다.

다음 3번째 요소인 1을 선택해 앞쪽에 삽입합니다. 그 이후에도 계속해서 같은 작업을 수행합니다.

그림에서 볼 수 있듯이 정렬된 부분과 아직 정렬되지 않은 부분에서 배열이 다시 구성된다고 생각하면서 작업을 n-1번 반복하면 정렬을 마치게 됩니다.

- 아직 정렬되지 않은 부분의 첫 번째 요소를 정렬된 부분의 알맞은 위치에 삽입합니다.

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fd19jSV%2FbtqL39i1onn%2FzKGzHSeLRPuWmkfeAwcVR1%2Fimg.png)

단순 삽입 정렬의 시간 복잡도

이렇게 구현한 단순 삽입 정렬 알고리즘은 떨어져 있는 요소들이 서로 뒤바뀌지 않아 안정적입니다.

요소의 비교횟수와 교환 횟수는 n^2 / 2 회이므로 시간복잡도는 O(n^2) 입니다.


# 병합 정렬

병합 정렬은 배열을 앞부분과 뒷부분으로 나누어 각각 정렬한 다음 병합하는 작업을 반복하여 정렬을 수행하는 알고리즘입니다.

## 정렬을 마친 배열의 병합
![image](https://blog.kakaocdn.net/dn/7jGlG/btqLZJ0aMEH/HdJDlHGTI3khHkK81kquz0/img.png)

사진처럼 배열 a,b 가 있다고 가정했을때 두 배열을 정렬하여 저장할 배열 c에 병합 정렬하는 과정입니다.

배열 a,b,c를 스캔할 때 선택한 요소의 인덱스는 pa,pb,pc 입니다.

이 인덱스를 저장한 변수를 지금부터 커서라고 하겠습니다. (처음에는 첫요소를 선택하기 때문에 모두 0으로 초기화)

1. 배열 a에서 선택한 요소(a[pa])와 배열 b에서 선택한 요소(a[pb])를 비교하여 작은 값을 c[pc]에 저장합니다. 그런 다음 커서 pc와 작은 값이 존재하는 배열의 커서를 한칸 옮기고 다시 pa와 pb를 비교하여 작은 값을 저장하는 과정을 반복 합니다. 커서 pa 가 a의 끝에 다다르거나 커서 pb가 b의 끝에 다다르면 이 작업을 종료합니다.

2. while문의 실행 조건은 1의 과정을 통해 하나의 배열은 모두 배열c로 복사되고 나머지 하나의 배열은 아직 복사하지 않은 요소가 남아 있습니다. 남아 있는 배열은 커서를 한칸씩 진행하면서 나머지 요소를 배열 c에 복사합니다.

병합에 필요한 시간 복잡도는 O(n)입니다.

# 병합 정렬

정렬을 마친 배열의 병합을 응용하여 분할 정복법에 따라 정렬하는 알고리즘을 병합 정렬이라고 합니다.

![image](https://blog.kakaocdn.net/dn/yqMlr/btqL3vfzLZ1/FsBdkKDJ18hCC2xsHhkxeK/img.png)

사진은 병합 정렬 과정을 간단히 나타낸 것으로, 먼저 배열을 앞부분과 뒷부분을 나눕니다.

여기서는 배열의 길이가 12이기 때문에 6개의 배열로 각각 나눕니다.

나눈 두 배열을 각각 정렬을 하고 병합하면 배열 모두를 정렬할 수 있습니다.

![image](https://blog.kakaocdn.net/dn/bv4Z6p/btqLYNIw7rd/RqJW2TVtqt1KPDnOtg1KV1/img.png)

이 때 앞뒤에 놓인 6개의 요소를 정렬할 때는 그냥 정렬하는 것이 아니라 다시 병합 정렬을 적용합니다.

예를 들어 뒷부분은 위 사진처럼 정렬합니다. 여기서 만들어지는 [9,0,1]과 뒷 부분[5,2,3]도 같은 순서에 따라 정렬합니다.

배열 병합의 시간 복잡도는 O(n)이고 데이터의 요소 개수가 n개 일 때, 병합 정렬의 단계는 log n 만큼 필요하므로 전체 시간 복잡도는 O(n log n)이라고 할 수 있습니다. 

# 퀵 정렬

퀵 정렬은 피벗을 기준으로 목록을 큰 값과 작은 값으로 나누어 가며 정렬합니다.

- 분할 정복 알고리즘의 하나로, 평균적으로 매우 빠른 수행 속도를 자랑하는 정렬 방법
    - 합병 정렬(merge sort)과 달리 퀵 정렬은 리스트를 비균등하게 분할한다.
- 분할 정복(divide and conquer) 방법
    - 문제를 작은 2개의 문제로 분리하고 각각을 해결한 다음, 결과를 모아서 원래의 문제를 해결하는 전략이다.
    - 분할 정복 방법은 대개 순환 호출을 이용하여 구현한다.

## 정렬 과정 설명
    - 리스트 안에 있는 한 요소를 선택한다. 이렇게 고른 원소를 피벗(pivot) 이라고 한다.
    - 피벗을 기준으로 피벗보다 작은 요소들은 모두 피벗의 왼쪽으로 옮겨지고 피벗보다 큰 요소들은 모두 피벗의 오른쪽으로 옮겨진다. (피벗을 중심으로 왼쪽: 피벗보다 작은 요소들, 오른쪽: 피벗보다 큰 요소들)
    - 피벗을 제외한 왼쪽 리스트와 오른쪽 리스트를 다시 정렬한다.
        - 분할된 부분 리스트에 대하여 순환 호출 을 이용하여 정렬을 반복한다.
        - 부분 리스트에서도 다시 피벗을 정하고 피벗을 기준으로 2개의 부분 리스트로 나누는 과정을 반복한다.
    - 부분 리스트들이 더 이상 분할이 불가능할 때까지 반복한다.
        - 리스트의 크기가 0이나 1이 될 때까지 반복한다.
        
![image](https://gmlwjd9405.github.io/images/algorithm-quick-sort/quick-sort-concepts.png)

## 퀵 정렬(quick sort) 알고리즘의 구체적인 개념

- 하나의 리스트를 피벗(pivot)을 기준으로 두 개의 비균등한 크기로 분할하고 분할된 부분 리스트를 정렬한 다음, 두 개의 정렬된 부분 리스트를 합하여 전체가 정렬된 리스트가 되게 하는 방법이다.
- 퀵 정렬은 다음의 단계들로 이루어진다.
    - 분할(Divide): 입력 배열을 피벗을 기준으로 비균등하게 2개의 부분 배열(피벗을 중심으로 왼쪽: 피벗보다 작은 요소들, 오른쪽: 피벗보다 큰 요소들)로 분할한다.
    - 정복(Conquer): 부분 배열을 정렬한다. 부분 배열의 크기가 충분히 작지 않으면 순환 호출 을 이용하여 다시 분할 정복 방법을 적용한다.
    - 결합(Combine): 정렬된 부분 배열들을 하나의 배열에 합병한다.
    - 순환 호출이 한번 진행될 때마다 최소한 하나의 원소(피벗)는 최종적으로 위치가 정해지므로, 이 알고리즘은 반드시 끝난다는 것을 보장할 수 있다.

![image](https://gmlwjd9405.github.io/images/algorithm-quick-sort/quick-sort.png)

## 퀵 정렬 특징
- 장점
    - 속도가 빠르다.
        - 시간 복잡도가 O(nlog₂n)를 가지는 다른 정렬 알고리즘과 비교했을 때도 가장 빠르다.
    
    - 추가 메모리 공간을 필요로 하지 않는다.
        - 퀵 정렬은 O(log n)만큼의 메모리를 필요로 한다.
- 단점
    - 정렬된 리스트에 대해서는 퀵 정렬의 불균형 분할에 의해 오히려 수행시간이 더 많이 걸린다.
    
    - 퀵 정렬의 불균형 분할을 방지하기 위하여 피벗을 선택할 때 더욱 리스트를 균등하게 분할할 수 있는 데이터를 선택한다.
        - EX) 리스트 내의 몇 개의 데이터 중에서 크기순으로 중간 값(medium)을 피벗으로 선택한다.

## 퀵 정렬 시간복잡도

- 최선의 경우
    - 비교 횟수

![image](https://gmlwjd9405.github.io/images/algorithm-quick-sort/sort-time-complexity-etc1.png)

- 순환 호출의 깊이

    - 레코드의 개수 n이 2의 거듭제곱이라고 가정(n=2^k)했을 때, n=2^3의 경우, 2^3 -> 2^2 -> 2^1 -> 2^0 순으로 줄어들어 순환 호출의 깊이가 3임을 알 수 있다. 이것을 일반화하면 n=2^k의 경우, k(k=log₂n)임을 알 수 있다.
    - k=log₂n

- 각 순환 호출 단계의 비교 연산
    - 각 순환 호출에서는 전체 리스트의 대부분의 레코드를 비교해야 하므로 평균 n번 정도의 비교가 이루어진다.
    - 평균 n번
- 순환 호출의 깊이 * 각 순환 호출 단계의 비교 연산 = nlog₂n
- 이동 횟수
    - 비교 횟수보다 적으므로 무시할 수 있다.
- 최선의 경우 T(n) = O(nlog₂n)

- 최악의 경우
    - 리스트가 계속 불균형하게 나누어지는 경우 (특히, 이미 정렬된 리스트에 대하여 퀵 정렬을 실행하는 경우)

![image](https://gmlwjd9405.github.io/images/algorithm-quick-sort/sort-time-complexity-etc2.png)

- 비교 횟수
    - 순환 호출의 깊이
        - 레코드의 개수 n이 2의 거듭제곱이라고 가정(n=2^k)했을 때, 순환 호출의 깊이는 n임을 알 수 있다.
        - n
- 각 순환 호출 단계의 비교 연산
    - 각 순환 호출에서는 전체 리스트의 대부분의 레코드를 비교해야 하므로 평균 n번 정도의 비교가 이루어진다.
    - 평균 n번
- 순환 호출의 깊이 * 각 순환 호출 단계의 비교 연산 = n^2
- 이동 횟수
    - 비교 횟수보다 적으므로 무시할 수 있다.

- 최악의 경우 T(n) = O(n^2)

- 평균
    - 평균 T(n) = O(nlog₂n)
    - 시간 복잡도가 O(nlog₂n)를 가지는 다른 정렬 알고리즘과 비교했을 때도 가장 빠르다.
    - 퀵 정렬이 불필요한 데이터의 이동을 줄이고 먼 거리의 데이터를 교환할 뿐만 아니라, 한 번 결정된 피벗들이 추후 연산에서 제외되는 특성 때문이다.


# 힙 정렬

**힙 정렬은** 힙 트리구조를 이용하는 정렬 알고리즘 입니다.

- 완전 이진 트리의 일종으로 우선순위 큐를 위하여 만들어진 자료구조
- 최댓값, 최솟값을 쉽게 추출할 수 있는 자료구조
![image](https://gmlwjd9405.github.io/images/data-structure-heap/types-of-heap.png)

## 완전 이진 트리의 일종으로 우선순위 큐를 위하여 만들어진 자료구조

- 최대 힙 트리나 최소 힙 트리를 구성해 정렬을 하는 방법
- 내림차순 정렬을 위해서는 최대 힙을 구성하고 오름차순 정렬을 위해서는 최소 힙을 구성하면 된다.

- 과정 설명
    - 정렬해야 할 n개의 요소들로 최대 힙(완전 이진 트리 형태)을 만든다.
        - 내림차순을 기준으로 정렬
    - 그 다음으로 한 번에 하나씩 요소를 힙에서 꺼내서 배열의 뒤부터 저장하면 된다.
    - 삭제되는 요소들(최댓값부터 삭제)은 값이 감소되는 순서로 정렬되게 된다.

# 힙 정렬(heap sort)의 시간복잡도

- 시간복잡도를 계산
    - 힙 트리의 전체 높이가 거의 log₂n(완전 이진 트리이므로)이므로 하나의 요소를 힙에 삽입하거나 삭제할 때 힙을 재정비하는 시간이 log₂n만큼 소요된다.
    - 요소의 개수가 n개 이므로 전체적으로 O(nlog₂n)의 시간이 걸린다.
    - T(n) = O(nlog₂n)

---

정렬 알고리즘 시간복잡도 비교

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FsZPG3%2FbtqLRktpJYz%2FfccUnXkcKw50vRDF4wiHbk%2Fimg.png)


- 단순(구현 간단) 하지만 비효율적인 방법
    - 삽입 정렬, 선택 정렬, 버블 정렬
- 복잡하지만 효율적인 방법
    - 퀵 정렬, 힙 정렬, 합병 정렬, 기수 정렬

---


# java에서의 Arrays.sort() vs Collections.sort() 

## Arrays.sort()

- Arrays.sort()에 char, int, boolean 등 과 같은 primitve(기본형) 타입과 reference(참조) 타입의 배열을 인자로 전달해서 사용할 수 있습니다. (배열만 사용 가능)

- 메서드에 매개변수로 Comparator를 받는 경우는 Comparable인터페이스에서 구현한 정렬 기준 외에 개발자가 정의한 다른 기준을 적용하고 싶을 때 사용합니다. (리터럴 타입의 배열은 사용할 수 없습니다.)

# Arrays.sort() 내부에서 사용하는 정렬 알고리즘

## 1. primitive(기본형) 타입의 배열인 경우

기본형 타입의 배열인 경우는 DualPivotQuicksort를 사용합니다.

![image](https://user-images.githubusercontent.com/47075043/156969163-f9af0831-0d29-4bf0-abd5-a53d5a8e73f8.png)

일반적인 Quicksort의 경우 1개의 Pivot으로 정렬을 수행하지만 DualPivotQuicksort는 피벗을 2개 사용해서 정렬을 수행합니다.

- Quicksort는 최악의 경우 O(N²), 평균적으로 O(NlogN)의 시간 복잡도를 가집니다.

- DualPivotQuicksort은 랜덤 데이터에 대해 일반적인 Quicksort보다 나은 시간 복잡도를 보장하지만, 여전히 최악의 경우 시간복잡도 O(NlogN)를 완전히 보장하지는 못합니다.

그러므로 만약에 정렬 알고리즘 문제 등등과 같이 시간 복잡도 O(NlogN)을 보장하는 정렬 코드를 작성해야 한다면 기본형 타입의 배열을 Arrays.sort()로 정렬하는 것은 다시 한번 생각해보셔야 할 것입니다.

사실 내부 로직을 깊게 파고들면 배열의 크기에 따라서 적용되는 정렬이 달라지지만 Arrays.sort()를 단순하게 사용하는 경우라면 나중에 필요에 의해서 소스코드를 분석해보는 것을 추천드립니다.

## 2. reference(참조) 타입의 배열인 경우

참조 타입의 배열인 경우는 TimSort를 사용합니다.

![image](https://user-images.githubusercontent.com/47075043/156970030-b1cb40cd-7f7f-41d0-9b7c-02bb28da84b4.png)

ComparableTimSort 클래스의 sort() 메서드를 사용하는 것을 알 수 있습니다.

22라인의 legacyMergeSort는 27라인의 주석을 보면 향후 릴리스 될 버전에서는 제거될 예정이므로 ComparableTimSort클래스의 sort()메서드를 사용한다고 생각하시면 됩니다.

TimSort는 다른 프로그래밍 언어에서도 사용하고 있는 정렬방법으로 삽입 정렬(Insertion)과 병합 정렬(Merge)을 섞어서 정렬을 수행합니다.

TimSort의 시간 복잡도는 삽입 정렬과 병합 정렬의 장점을 가지고 있습니다.

***정렬 별 시간 복잡도***
![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbmKuuA%2FbtqZjvn8RAc%2FzJC9msKw7oNJR4ohF4iN1k%2Fimg.png)

위의 표를 보시면 TimSort는 최선의 상태에서는 삽입 정렬의 시간 복잡도O(N)를 최악의 경우에는 병합 정렬의 시간 복잡도 O(N*logN)을 가집니다.

최악의 경우에도 O(N*logN) 시간 복잡도를 가지는 정렬 알고리즘이 필요하다면 Arrays.sort()가 TimSort를 수행할 수 있도록 primitive타입의 배열보단 reference타입의 배열을 사용해야 합니다.

# Collections.sort()

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fc9uKnH%2FbtqZRsvVk6t%2Fbgvz8fIlleO3vu5R7IGFPk%2Fimg.png)

API 공식문서에서 Collections.sort()를 찾아보시면 위와 같이 2가지로 오버로딩 돼있습니다.

List객체를 파라미터로 받는 경우는 제네릭 타입인 클래스가 Comparable를 구현하고 있어야 사용 가능합니다.

Comaparator를 파라미터로 받는 경우에는 제네릭 타입 클래스가 Comparable을 구현하고 있지 않아도 사용할 수 있습니다.

이러한 경우에는 Comparator 인터페이스에 구현된 정렬 기준으로 정렬이 수행됩니다.


## Collections.sort() 내부 정렬 알고리즘

![image](https://user-images.githubusercontent.com/47075043/156970333-85a8028c-6dd9-47b9-bfb4-108e3adb4fcf.png)

list.sort()를 타고 들어가면 아래와 같이 Arrays.sort()가 실행되는 걸 볼 수 있습니다.

즉, Collections.sort()에서는 List객체를 Object배열로 변환해서 Arrays.sort()를 실행해서 정렬을 수행합니다.

Arrays.sort() 내부를 살펴보면 다음과 같이 TimSort.sort()를 실행하는 걸 볼 수 있습니다.

![image](https://user-images.githubusercontent.com/47075043/156970494-fafd817b-3293-4a1d-8717-ebcfac5f37c8.png)

legacyMergeSort() 메서드는 추후 릴리즈 될 버전에서는 사라질 것이므로 실제로 내부 소스는 파라미터로 받은 Comparator가 null이면 sort()를 null이 아니면 TimSort.sort()를 실행합니다.

sort() 메서드를 찾아가 보면 위에 Arrays.sort()에서 설명했던 ComparableTimSort.sort()를 실행합니다.

ComparableTimSort.sort()와 TimSort.sort()는 동일한 TimSort알고리즘을 수행하며 Comparator와 Comparable 둘 중 정렬 기준이 되는 객체에 따라서 수행하는 클래스명이 달라질 뿐입니다.

---

## 정리

결국 정렬을 수행하기 위해서 사용되는 메서드는 Arrays.sort()입니다.

그러나 어떤 타입의 배열을 받느냐에 따라서 실행되는 정렬 알고리즘이 달라지는 것입니다.

표로 정리하면 다음과 같습니다.

![imaege](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F4kKcq%2FbtqZZUmO3Ww%2FSyf5J0svlO6EzLv9bzfA1K%2Fimg.png)

---

참고 :

자료구조와 C(도서)

Do It 자료구조와 함께 배우는 알고리즘 입문(자바 편)

gmlwjd9405.github.io/2018/05/06/algorithm-bubble-sort.html

[Arrays.sort() vs Collections.sort()](https://codingnojam.tistory.com/38)