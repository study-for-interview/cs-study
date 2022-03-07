# 📌 버블정렬
버블 정렬은 그렇게 좋은 알고리즘이 아니라서 자주 사용되진 않는다.

- 버블 정렬은 먼저, 배열에서 2개의 아이템을 선택하고 비교한다.

![](https://images.velog.io/images/kcwthing1210/post/310cbfc6-ed38-425e-bedb-0ff0ac8270ac/image.png)

- 왼쪽이 오른쪽보다 크면 교환한다.

![](https://images.velog.io/images/kcwthing1210/post/022ed2fa-893f-4ab7-ab70-00735cf285be/image.png)

- 오른쪽으로 이동해서 프로세스를 반복한다.
  ![](https://images.velog.io/images/kcwthing1210/post/5c47bf03-6863-4805-b7d8-73d833b0bdf9/image.png)

- 아래 경우에는 5와 2로 시작하는데, 5는 2보다 크니까 교환한다.
  ![](https://images.velog.io/images/kcwthing1210/post/3d7322c1-00d6-4bce-bc23-480140f92a31/image.png)
  ![](https://images.velog.io/images/kcwthing1210/post/d1ac588a-3b9d-4f8f-8d89-c595336096b4/image.png)

- 이번엔 오른쪽으로 한 칸 이동해서 5와 6을 비교한다. 5가 더 작으니까 교환하지 않는다.

![](https://images.velog.io/images/kcwthing1210/post/da124418-975b-4b8e-90a6-6c5d44262a05/image.png)
- 다시 오른쪽으로 한 칸 이동해서 6이 3보다 큰지 비교한다. 크니까 교환한다.
  ![](https://images.velog.io/images/kcwthing1210/post/56a3383a-5a20-44b1-8cff-25af9c9b046b/image.png)
  ![](https://images.velog.io/images/kcwthing1210/post/831794b2-e915-4bdc-a1dd-5250816ba5e2/image.png)

- 또 오른쪽으로 한 칸 이동해서 6과 1을 비교한다. 6이 더 크니까 교환한다.
  ![](https://images.velog.io/images/kcwthing1210/post/ef43ab44-f84c-4556-9772-d92e3cb9de64/image.png)
  ![](https://images.velog.io/images/kcwthing1210/post/be28e9cb-5eda-4336-95d3-0cd3beaae325/image.png)

- 마지막으로 6이 4보다 크므로 교환한다.
  ![](https://images.velog.io/images/kcwthing1210/post/6110a05d-49b5-4e26-bd75-60036b8db283/image.png)
  ![](https://images.velog.io/images/kcwthing1210/post/06845e64-b8b7-4c3a-9f0f-189d4fb1d558/image.png)

여기까지 버블 정렬의 첫 번째 싸이클이 끝났다. 이렇게 더 큰 아이템이 끝까지 '버블'로 이동하기 때문에 '버블 정렬'이다. 그럼 마저 버블 정렬을 끝내보자.

- 다시 처음부터 비교해서 2는 5보다 크지 않으므로 교환하지 않는다.
  ![](https://images.velog.io/images/kcwthing1210/post/49691886-7962-43b8-9c1a-d9298adb92bc/image.png)
- 오른쪽으로 이동해서 5는 3보다 크므로 교환한다.
  ![](https://images.velog.io/images/kcwthing1210/post/8fc299d2-e4b6-4740-807d-c404d93902fd/image.png)
  ![](https://images.velog.io/images/kcwthing1210/post/4e67aa5c-78fa-4da4-85d1-c66b666362e9/image.png)

- 또 오른쪽으로 이동하고 5는 1보다 크므로 교환한다
  ![](https://images.velog.io/images/kcwthing1210/post/ff1fe5df-c606-444a-adeb-33e753a5c19f/image.png)
  ![](https://images.velog.io/images/kcwthing1210/post/561229f1-0a5e-41d2-aac6-4ec51f6a8b50/image.png)

- 다음 5는 4보다 크므로 교환한다.
  ![](https://images.velog.io/images/kcwthing1210/post/5cac5b44-e26c-4c3f-82bc-99264dd884a4/image.png)
  ![](https://images.velog.io/images/kcwthing1210/post/de667127-ab28-4257-9063-15ad5a7fdb60/image.png)

- 4가 올바른 위치에 도착했다.
  ![](https://images.velog.io/images/kcwthing1210/post/400671ce-0006-43bf-a245-998c4c44e4b1/image.png)

- 비교하고 교환하기의 반복이다. 아래가 버블 정렬이 끝났을 때의 모습이다.
  ![](https://images.velog.io/images/kcwthing1210/post/add6d552-bfb0-4311-9368-ac89413fff8c/image.png)

### ✅ 시간복잡도
그렇다면 버블 정렬의 시간 복잡도는 어떨까? 배열의 N-1의 아이템을 비교해야 한다. 아이템이 6개면 5번 비교해야 하고, 다음 싸이클에서도 비교하고 반복이다.
![](https://images.velog.io/images/kcwthing1210/post/1e9efeb2-b1d4-4692-9f6a-ede9ae652af1/image.png)

최악의 경우에는 모든 아이템을 교환해야 한다. 예를 들어, 작은 수에서 큰 수로 정렬하고 싶은데 배열이 큰 수에서 작은 수의 순으로 되어있는 경우이다. 따라서, 버블 정렬의 시간 복잡도는 O(n²)이다.
![](https://images.velog.io/images/kcwthing1210/post/86d3d70c-8edf-4a8b-aeea-e94349a61fc1/image.png)

# 📌 Selection Srot(선택 정렬)
## ✅ 동작방식
선택 정렬은 전체 아이템 중 가장 작은 아이템의 위치를 변수에 저장한다.

- 아래 배열에서 가장 작은 숫자는 5인데, 5보다 작은 숫자인 2가 있다.
  ![](https://images.velog.io/images/kcwthing1210/post/819a2acc-373f-452a-ae08-6d946dabd71e/image.png)

- 2의 위치를 변수에 저장하고 계속 체크하다가 1에 도착하면 해당 위치를 변수에 저장하고 싸이클을 끝낸다.
  ![](https://images.velog.io/images/kcwthing1210/post/c489d461-bf33-4839-a6e8-abe54376dd94/image.png)

![](https://images.velog.io/images/kcwthing1210/post/5bf6b6ed-ab64-4c41-bc20-346573adcd5c/image.png)

- 배열에서 가장 작은 숫자가 어디에 있는지 알아냈다.
  ![](https://images.velog.io/images/kcwthing1210/post/1ded612e-8d1e-48c5-b5de-a835a38653e7/image.png)

- 그럼 이제 가장 작은 숫자를 첫번째 아이템과 바꾼다.
  ![](https://images.velog.io/images/kcwthing1210/post/be6b572a-eada-4b09-8247-df62190e9457/image.png)

- 그리고 다음 사이클을 시작할 때 두 번째 아이템부터 시작한다. 1은 이미 정렬했으니 정렬되지 않은 부분에서 가장 작은 숫자를 찾는다.
  가장 작은 숫자 2를 찾고, 2는 이미 올바른 위치에 있으므로 교환하지 않는다.
  ![](https://images.velog.io/images/kcwthing1210/post/849e44cb-7647-40b0-b5fd-843f4408a950/image.png)

- 이 과정을 계속 반복한다.
  ![](https://images.velog.io/images/kcwthing1210/post/0c37c84b-86dc-4a9a-84e9-335cac93a143/image.png)

## ✅ 시간복잡도
선택 정렬의 시간 복잡도는 뭘까? 버블 정렬과 비슷하게 교환도 하고 비교도 한다. 또, 정렬되지 않은 배열에서 가장 작은 숫자를 찾으므로 N-1 비교를 하는 것이다. 이건 버블 정렬과 동일하다.

하지만 버블 정렬과 다르게 N 번의 교환을 하지 않는다. 선택 정렬에서는 매번 싸이클마다 한 번의 교환만 하면 된다. 즉, 선택 정렬은 버블 정렬보다 훨씬 낫다.

선택 정렬이 버블 정렬보다 2배 더 빠를 수도 있음에 불구하고 선택 정렬의 시간 복잡도 역시 O(n²)이다.

![](https://images.velog.io/images/kcwthing1210/post/7a02738b-0276-4f6c-8d12-034c395298be/image.png)

# 📌 Insertion Sort(삽입 정렬)
## ✅ 동작방식
- 앞에서 사용한 배열로 삽입 정렬을 해보면 인덱스 1번에서 시작한다.
  ![](https://images.velog.io/images/kcwthing1210/post/069a7d4a-ed54-4a59-be91-accac25cf3f6/image.png)
- 왼쪽에 2보다 큰 숫자가 있는지 살펴본다. 5가 2보다 크니까 교환한다.
  ![](https://images.velog.io/images/kcwthing1210/post/98d6d876-52bf-40d0-b70a-4866e3a64fd7/image.png)
  ![](https://images.velog.io/images/kcwthing1210/post/663afd49-e863-4256-a320-db1fa33bcaa1/image.png)

- 두 번째 싸이클은 6을 선택하고 왼쪽에 더 큰 숫자가 있는지 살펴본다. 없는 경우 계속 진행한다.

![](https://images.velog.io/images/kcwthing1210/post/1cedb609-77e2-414a-80e2-27ecbf248192/image.png)

- 세번째 사이클에서 3을 선택하고 왼쪽에 더 큰 숫자가 있는지 확인한다. 6이 3보다 크니까 교환한다.
  ![](https://images.velog.io/images/kcwthing1210/post/1b92cc0a-1d11-4cf1-8f6f-652c6321b033/image.png)
  ![](https://images.velog.io/images/kcwthing1210/post/c1271887-3700-4c2c-b962-27478146e137/image.png)

- 그리고 다시 3과 5를 비교한다. 5가 더 크니까 교환한다.

![](https://images.velog.io/images/kcwthing1210/post/81b36f0f-db20-42f8-b60d-dd9896619c29/image.png)
![](https://images.velog.io/images/kcwthing1210/post/5c7a6692-0c13-4cf9-a229-52a5e9f6b297/image.png)

- 그리고 다시 3과 2를 비교하는데 2가 3보다 크지 않으니까 2는 올바른 위치에 있다고 말할 수 있다.
  ![](https://images.velog.io/images/kcwthing1210/post/4b0dd6c0-1393-4671-8efe-8c7b5eeb3c41/image.png)
  ![](https://images.velog.io/images/kcwthing1210/post/e678495d-6122-4a84-9ecd-a78106e8679f/image.png)

## ✅ 시간복잡도
1과 4로 동일한 작업을 하면 끝난다. 삽입 정렬은 필요한 아이템만 스캔하고 선택 정렬은 전체 모든 아이템을 스캔하기 때문에 삽입 정렬은 선택 정렬보다 빠르다. 하지만, 삽입 정렬이 선택 정렬과 버블 정렬보다 빨라도 시간복잡도는 동일하게 O(n²)이다.

![](https://images.velog.io/images/kcwthing1210/post/049c64df-f9cd-4a8a-b895-45156f8300f3/image.png)

# 📌 삽입 정렬 vs 선택 정렬
최악/최고의 케이스는 자주 발생하지 않고 대부분 평균적인 경우에 속하기 때문에 최악의 시나리오가 아닌 평균 시나리오를 봐야한다.

그걸 감안하고 알고리즘들을 살펴보면 삽입 정렬, 선택 정렬 둘 다 평균적으로 최악의 경우 이차 시간복잡도를 가지고 있다. 그러나 삽입 정렬의 경우 O(n)이 최고의 시나리오에서 발생한다.
![](https://images.velog.io/images/kcwthing1210/post/952e9141-f3f4-458e-a6d2-b98fecb6bb45/image.png)

O(n)은 이차 시간복잡도와 비교해서 최고의 알고리즘이다.
![](https://images.velog.io/images/kcwthing1210/post/354c534c-89b7-44d2-830b-f506da1e8430/image.png)

이렇게 동일한 시간복잡도를 갖고있다 하더라도 매우매우 다르게 나타날 수 있다. 삽입, 선택 정렬은 작은 DB 기준으로는 훌륭한 알고리즘이다. 물론, 데이터가 커지면 커질수록 좀 느려지겠지만 그때 다른 걸 살펴봐야할 것이다.


# 📌 정리
Sorting은 정말 많은 개발자들이 관심을 갖는 주제고, 다들 한 번은 정렬을해 봤을 것이다. 그만큼 정말 중요하기 때문에 잘 알아둬야 한다.

버블 정렬은 잘 사용되지 않기 때문에 어떻게 해야 하는지까지 정확히 암기할 필요는 없지만 정렬이 뭔지, 정렬이 왜 복잡한지, 더 좋은 솔루션이 왜 필요한지를 이해할 수 있다.

- 버블 정렬
    - 인접한 원소끼리 비교하여 교환하는 방식
    - 셋 중에 제일 느리지만 단순함
- 선택 정렬
    - 최솟값을 찾아서 맨 앞으로 이동하는 방식
    - 버블 정렬보다 좋음
- 삽입 정렬
    - 앞에서부터 차례대로 이미 정렬된 부분과 비교하여 교환하는 방식
    - 셋 중에 제일 빠르지만 배열이 길어질수록 효율성이 떨어짐
    - 모두 시간 복잡도는 O(n²)
      선택 정렬과 삽입 정렬은 사용할 메모리가 제한적인 경우에 사용하면 좋음

# 🧩 Reference
- https://velog.io/@minji0801/%EB%B2%84%EB%B8%94%EC%A0%95%EB%A0%AC-vs-%EC%84%A0%ED%83%9D%EC%A0%95%EB%A0%AC-vs-%EC%82%BD%EC%9E%85%EC%A0%95%EB%A0%AC-%EC%B0%A8%EC%9D%B4-%EC%A0%9C%EB%8C%80%EB%A1%9C-%EC%95%8C%EA%B3%A0%EA%B0%80%EC%9E%90





꾸미.log

새 글 작성
thumbnail
꾸미.log

새 글 작성
thumbnail
병합 정렬, 퀵 정렬, 힙 정렬
통계
수정
삭제
kcwthing1210·약 1시간 전
자료구조
0
📌 병합정렬
📌 퀵 정렬
📌 힙정렬
🧩 Reference
O(n log n)인 정렬 알고리즘들
이 알고리즘은 최선으로나 평균적으로나 O(n log n)의 성능을 나타낸다.

최악의 상황에서도 병합정렬이나 힙정렬은 O( n log n)을 유지하는 반면 순수한 퀵 정렬은 오히려 O(n^2)로 뒤진다. 그래서 실제로는 퀵 정렬을 조금 개량해서 최악의 경우가 발생하지 않도록 코드를 짠다.

📌 병합정렬


대표적인 분할정복(Divide and Conquer) 알고리즘.

분할정복이란 말 그대로 문제를 분할 한 다음, 분할한 문제들 (sub-program)을 해결하고, 그 결과를 합쳐서 원래의 문제를 해결하는 것을 말한다.

마찬가지로 합병 정렬은 원소의 개수가 1 또는 0이 될 때 까지 두 부분으로 쪼개고 그 결과들을 크기를 비교하며 정렬하는 방식으로 병합해나간다.

성능은 퀵정렬보다 전반적으로 뒤떨어지고, 데이터 크기만한 메모리가 더 필요하지만, 최대의 장점은 데이터의 상태에 별 영향을 받지 않는다는 점이다.

정렬되어있는 두 배열을 더할 때 이 알고리즘을 사용하면 가장 빠르게 정렬된 상태로 합칠 수 있다.

📌 퀵 정렬


여기서 힙은 힙트리로, 여러개의 값 들 중 가장 크거나 작은 값을 빠르게 찾기 위해 만든 이진 트리이다. 짧게 힙이라고 부른다.

힙은 항상 완전 이진 트리의 형태를 띈다. 부모의 값은 항상 자식들의 값보다 크거나 (Max Heap) 작아야 (Min Heap) 한다는 규칙이 있다. 따라서 루트(뿌리) 노드에는 항상 데이터들 중 가장 큰 값 혹은 작은 값이 저장되어 있다.

힙 정렬의 방법은 아래와 같다.

배열의 원소들을 전부 힙에 삽입
가장 부모노드에 있는 값은 최댓값 혹은 최솟값이므로 루트를 출력하고 힙에서 제거
힙이 빌 때 까지 2의 과정을 반복
힙정렬은 추가적인 메모리를 전혀 필요로하지 않는다는 점과 최악의 경우에도 항상 O(n log n) 의 성능을 발휘한다는 장점이 있다.

📌 힙정렬


퀵정렬은 배열에 있는 수 중 사용자가 지정한 규칙대로 임의의 pivot을 잡고, 해당 pivot을 기준으로 작거나 같은 수를 왼쪽 파티션, 큰 수를 오른쪽 파티션으로 보낸다. 다시 왼쪽 파티션 구간에 한하여 pivot을 잡고 파티션을 나누고 오른쪽 파티션 구간에서도 pivot을 잡고 파티션을 나누는 과정을 반복하여 정렬시킨다.

이 알고리즘의 핵심은 pivot을 잡는 것인데, pivot을 해당 구간의 중앙값으로 잘 설정하면 시간복잡도 O(n log n)에 수행할 수 있지만, 만약 매 케이스마다 구간의 최댓값이나 최솟값으로 나눠버리면 O(n^2)의 수행시간을 갖게 된다.

현존하는 컴퓨터 아키텍처 상에서 비교연산자를 사용하여 구현된 정렬 알고리즘 중 가장 고성능인 알고리즘이다. 단, 데이터에 접근하는 시간이 오래 걸리는 외부 기억장소(하드디스크 등)에서 직접 정렬을 수행할 경우에는 병합 정렬이 더 빠른 것으로 알려져 있다.

🧩 Reference
https://butter-shower.tistory.com/17
profile
Onni
꿈꿈
이전 포스트
선택 정렬, 거품 정렬, 삽입 정렬
0개의 댓글
댓글을 작성하세요
댓글 작성
Powered by GraphCDN, the GraphQL CDN