# 트리 (Tree)

* 비선형 자료구조
* 그래프의 한 종류로 **사이클**이 없는 **연결 그래프**이다.
* 간선의 개수는 항상 N+1개 이다. (N: 노드의 개수)

* DAG의 한 종류이기도 함

<br> 

<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/f/f7/Binary_tree.svg/200px-Binary_tree.svg.png" alt="img" style="zoom:150%;"/>





<br> <br> <br> 

## 트리 용어

<img src="https://w.namu.la/s/606aecc8b8a27d42129f3e13c6db9a871a4566cd88c123689585256281efb5dde5b35f4e516572f0e5f0e419f0ae2be3aedf7a9c8dbb1756d1bf635a48da67ec0cdf0725d4e7bcd081fb91d7dd1a17d74023cb5171e586302cc533d80b4f8427ccc326f389d8d9ead7f19218586e1eae" alt="4-14-2"/>

<br> 

* 루트 노드(root node): 부모가 없는 노드, 트리는 하나의 루트 노드만을 가진다.
* 리프 노드(leaf node): 자식이 없는 노드, 단말 노드 또는 잎 노드
* 내부(internal) 노드: 단말 노드가아닌 노드, 차수가 2이상인 노드이다.
* 간선(edge): 노드를 연결하는 선
* 형제(sibling): 같은 부모를 가지는 노드
* 노드의 크기(size): 자신을 포함한 모든 자손 노드의 개수
* 노드의 깊이(depth): 루트에서 어떤 노드에 도달하기 위해 거쳐야 하는 간선의 수
* 노드의 레벨(level): 트리의 특정 깊이를 가지는 노드의 집합
* 노드의 차수(degree): 하위 트리 개수 / 간선 수 (degree) = 각 노드가 지닌 가지의 수
* 트리의 차수(degree of tree): 트리의 최대 차수
* 트리의 높이(height): 루트 노드에서 가장 깊숙히 있는 노드의 깊이




<br> <br> <br> 


### 이진 트리 (Binary Tree)

부모 노드 밑의 **자식 노드 개수(=차수, degree)를 최대 2개로 제한**하는, 트리의 가장 간단한 형태.

<img src="https://ww.namu.la/s/80babca3318fe49e11009da782d4a7b3969bf17517764fe7dab69b05e0477ba3f057a995cd00c2434b4c964cd08ba76267c879cea21db822565ccd8a50252dae5a99699e3e2842382aeaddd2cfdcc933ad270be195bfb69e31d7195ff47567d7" alt="external/upload...." />

<br> 

#### 이진트리의 종류

<img src="https://t1.daumcdn.net/cfile/tistory/992164335A05B1E21E" alt="img" style="zoom:80%;" />

<br> 

- **정 이진 트리(full binary tree)**

  모든 트리의 자식은 0개나 2개로, 홀수 개의 자식노드를 가진 부모노드가 없는 트리이다.

- **완전 이진 트리(complete binary tree)** 

  부모, 왼쪽 자식, 오른쪽 자식 순으로 채워지는 트리이다.

  즉, 트리의 원소를 왼쪽에서 오른쪽으로 하나씩 빠짐없이 채워나간 형태이다. 

- **포화 이진 트리(perfect binary tree)**

  정 이진 트리이면서 완전 이진 트리인 경우이다.

  모든 리프 노드의 높이가 같고 리프 노드가 아닌 노드는 모두 2개의 자식을 갖는다. 

  또한, 모든 포화 이진 트리는 정 이진 트리이다.

<br> 

#### 이진 트리 순회 방법

- 중위 순회(In-order traversal): 왼쪽 자손, 자신, 오른쪽 자손 순서로 방문하는 순회 방법.
- 전위 순회(Pre-order traversal): 자신, 왼쪽 자손, 오른쪽 자손 순서로 방문하는 순회 방법.
- 후위 순회(Post-order traversal): 왼쪽 자손, 오른쪽 자손, 자신 순서로 방문하는 순회 방법.
- 너비 우선 순회(Breadth-First traversal)라고도 한다. 노드를 레벨 순서로 방문하는 순회 방법. 위의 세 가지 방법은 **스택**을 활용하여 구현할 수 있는 반면 레벨 순서 순회는 **큐**를 활용해 구현할 수 있다.

<img src="https://ww.namu.la/s/8e72dc2a70a4523d258bba6ff2edb2ef2b9240ed67133d1c5a2fd14de683af1d2a462f989102399598c1ca60d425651ea37c3acb14441e0b922b25e82ea9179efcbee8df6f9c8e9a79a8e04dbcb5ff4982f2349a640363e8d1bf7a48742f25e5" alt="external/sites.g..." style="zoom:80%;"/>

<br> 

위의 트리를 순회하면 다음과 같다.

- In-order: 1 3 4 6 7 8 10 13 14
- Pre-order: 8 3 1 6 4 7 10 14 13
- Post-order: 1 4 7 6 3 13 14 10 8
- Level-order(BFS): 8 3 10 1 6 14 4 7 13



<br> <br> <br> 

## 유명한 트리 자료 구조

- [자가 균형 이진 탐색 트리](https://ko.wikipedia.org/wiki/자가_균형_이진_탐색_트리)
- [AVL 트리](https://ko.wikipedia.org/wiki/AVL_트리)
- [레드-블랙 트리](https://ko.wikipedia.org/wiki/레드-블랙_트리)
- [스플레이 트리](https://ko.wikipedia.org/w/index.php?title=스플레이_트리&action=edit&redlink=1)