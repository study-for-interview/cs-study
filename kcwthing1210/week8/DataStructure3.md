
# 🎁 그래프

# ✅ 그래프란?
그래프는 정점과 간선으로 이루어진 자료구조입니다. 정확히는 정점(Vertex)간의 관계를 표현하는 조직도라고 볼수도 있겠습니다. 그런면에서 트리는 그래프의 일종인 셈입니다. 다만 트리와는 달리 그래프는 정점마다 간선이 없을수도 있고 있을수도 있으며 루트 노드, 부모와 자식이라는 개념이 존재하지 않습니다. 또한 그래프는 네트워크 모델 즉, 객체와 이에 대한 관계를 나타내는 유연한 방식으로 이해할 수 있습니다. 실생활에서 다양한 예를 그래프로 표현할 수 있습니다. 대표적으로 지하철 노선도, 도심의 도로등이 있습니다. 이런식으로 활용할 수 있는 방법이 많기에 문제도 다양하게 출제를 할 수 있습니다. 그래프는 알고리즘에서 굉장히 많이 사용됩니다. 특히 그래프를 순회하는 방식인 DFS와 BFS를 잘 알아두어야 합니다.

## ✅ 그래프에서 사용하는 용어
![](https://images.velog.io/images/kcwthing1210/post/2b912d0e-7a1c-4fbf-bc50-3cd2b5471677/image.png)

- 정점(vertice) : 노드(node)라고도 하며 정점에는 데이터가 저장됩니다. (0, 1, 2, 3)
- 간선(edge): 링크(arcs)라고도 하며 노드간의 관계를 나타냅니다.
- 인접 정점(adjacent vertex) : 간선에 의해 연결된 정점으로 위에서 (정점0과 정점1은 인접 정점)
- 단순 경로(simple-path): 경로 중 반복되는 정점이 없는것, 같은 간선을 자나가지 않는 경로
- 차수(degree): 무방향 그래프에서 하나의 정점에 인접한 정점의 수 (정점 0의 차수는 3)
- 진출 차수(out-degree) : 방향그래프에서 사용되는 용어로 한 노드에서 외부로 향하는 간선의 수를 뜻합니다.
- 진입차수(in-degree) : 방향그래프에서 사용되는 용어로 외부 노드에서 들어오는 간선의 수를 뜻합니다.

## ✅ 그래프 구현 방법

그래프를 구현하는 방법에는 인접행렬(Adjacency Materix)와 인접리스트(Adjacency List)방식이 있습니다. 두개의 구현 방식은 각각의 상반된 장단점을 가지고 있는데 대부분 인접리스트 형식을 많이들 사용합니다.

### ✔ 인접행렬 방식
![](https://images.velog.io/images/kcwthing1210/post/73d1a003-3e2d-42ed-b25a-0536529135c3/image.png)

인접행렬은 그래프의 노드를 2차원 배열로 만든 것입니다. 완성된 배열의 모양은 1, 2, 3, 4, 5, 6의 정점을 연결하는 노드에 다른 노드들이 인접 정점이라면 1, 아니면 0을 넣어줍니다.

#### 인접행렬 장점
1. 2차원 배열 안에 모든 정점들의 간선 정보를 담기 때문에 배열의 위치를 확인하면 두 점에 대한 연결 정보를 조회할 때 O(1) 의 시간 복잡도면 가능합니다.
2. 구현이 비교적 간편합니다.

인접행렬 단점
1. 모든 정점에 대해 간선 정보를 대입해야 하므로 O(n²) 의 시간복잡도가 소요됩니다.

2. 무조건 2차원 배열이 필요하기에 필요 이상의 공간이 낭비됩니다.

### ✔ 인접리스트 방식
![](https://images.velog.io/images/kcwthing1210/post/2229f28c-ceb5-4447-9383-a759f7d695a4/image.png)

인접리스트란 그래프의 노드들을 리스트로 표현한것입니다. 주로 정점의 리스트 배열을 만들어 관계를 설정해줌으로써 구현합니다.


#### 인접리스트 장점
1. 정점들의 연결 정보를 탐색할 때 O(n) 의 시간이면 가능합니다. (n: 간선의 갯수)
2. 필요한 만큼의 공간만 사용하기때문에 공간의 낭비가 적습니다.


#### 인접리스트 단점
1. 특정 두 점이 연결되었는지 확인하려면 인접행렬에 비해 시간이 오래 걸립니다. (배열보다 search 속도느림)

2. 구현이 비교적 어렵습니다.

## ✅ 다양한 그래프의 종류
그래프는 구현되어진 특성에 따라 여러가지 종류로 나누어집니다. 대표적인 그래프의 유형은 아래와 같습니다.

### ✔ 무방향그래프
![](https://images.velog.io/images/kcwthing1210/post/c7180fff-79e6-4753-8d74-be8f385ac945/image.png)

무방향 그래프는 두 정점을 연결하는 간선에 방향이 없는 그래프입니다.



### ✔ 방향그래프
![](https://images.velog.io/images/kcwthing1210/post/2a0bf5bd-f26d-4b6b-8a0d-e0e45caa1fad/image.png)

방향 그래프는 두 정점을 연결하는 간선에 방향이 존재하는 그래프입니다. 간선의 방향으로만 이동할 수 있습니다.



### ✔ 가중치그래프
![](https://images.velog.io/images/kcwthing1210/post/55d04f45-eb7f-4f05-b0f9-64c219c0d45a/image.png)

가중치 그래프는 두 정점을 이동할때 비용이 드는 그래프입니다.



### ✔ 완전그래프
![](https://images.velog.io/images/kcwthing1210/post/3c660290-f251-40d8-8ccf-48f60cdd6c82/image.png)

완전 그래프는 모든 정점이 간선으로 연결되어 있는 그래프입니다.

## ✅ 그래프의 탐색
첫 정점에서부터 그래프에 존재하는 모든 정점들을 모두 한번씩 방문하는 것을 그래프 탐색이라고 합니다. 그래프 탐색의 방법은 깊이 우성 탐색(DFS) 방식과 너비 우선 탐색(BFS)방식이 있습니다.

![](https://images.velog.io/images/kcwthing1210/post/7036d900-9dc0-4e78-a7f8-5e25725ab466/%EA%B7%B8%EB%9E%98%ED%94%84%ED%83%90%EC%83%89.gif)

### ✔ 깊이 우선탐색(DFS)
깊이 우선탐색 DFS는 갈 수 있는 만큼 최대한 깊이 가고, 더 이상 갈 곳이 없다면 이전 정점으로 돌아가는 방식으로 그래프를 순회하는 방식입니다. 간단히 재귀호출을 사용하여 구현하거나 스택을 사용하여 구현합니다.



### ✔ 넓이 우선탐색(BFS)
넓이 우선탐색 BFS는 시작정점을 방문한 후 시작 정점에 인접한 모든 정점을 방문한 후 시작 정점에 인접한 모든 정점들을 우선방문하는 방법입니다. 일반적으로 QUEUE를 사용해서 지금 위치에서 갈 수 있는 것들을 모두 큐에 넣는 방식으로 구현합니다.


# 🧩 Reference
- https://coding-factory.tistory.com/610

# 🎁 트리 
# 📌 트리 (Tree)
- 노드들이 나무 가지처럼 연결된 비선형 계층적 자료구조
- 트리는 다음과 같이 나무를 거꾸로 뒤집어 놓은 모양과 유사
  ![](https://images.velog.io/images/kcwthing1210/post/dd691cc0-f331-4364-bc0f-0b4cef75818e/image.png)
- 트리는 또한 트리 내에 다른 하위 트리가 있고 그 하위 트리 안에는 또 다른 하위 트리가 있는 재귀적 자료구조
- ex) 컴퓨터의 direcory구조
  ![](https://images.velog.io/images/kcwthing1210/post/c29db310-3d0b-4ae8-949c-09c731a004d6/image.png)


## ✅ 트리 구조에서 사용되는 기본 용어
![](https://images.velog.io/images/kcwthing1210/post/da632aa2-de7f-4dfb-9d42-d4971fd78058/image.png)

- 노드 (Node)

    - 트리를 구성하고 있는 기본 요소
    - 노드에는 키 또는 값과 하위 노드에 대한 포인터를 가지고 있음.
      A, B, C, D, E, F, G, H, I, J

- 간선 (Edge)

    - 노드와 노드 간의 연결선
- 루트 노드 (Root Node)

    - 트리 구조에서 부모가 없는 최상위 노드
    - root node : A
- 부모 노드 (Parent Node)

    - 자식 노드를 가진 노드
    - H, I에 부모 노드는 D
- 자식 노드 (Child node)

    - 부모 노드의 하위 노드
    - 노드 D의 자식 노드는 H, I
- 형제 노드 (Sibling node)

    - 같은 부모를 가지는 노드
    - H, I는 같은 부모를 가지는 형제 노드
- 외부 노드(external node, outer node), 단말 노드 (terminal node), 리프 노드(leaf node)

    - 자식 노드가 없는 노드
    - H, I, J, F, G
- 내부 노드 (internal node, inner node), 비 단말 노드 (non-terminal node), 가지 노드 (branch node)

    - 자식 노드 하나 이상 가진 노드
    - A, B, C, D, E
- 깊이 (depth)

    - 루트에서 어떤 노드까지의 간선(Edge) 수
    - 루트 노드의 깊이 : 0
    - D의 깊이 : 2
- 높이 (height)

    - 어떤 노드에서 리프 노드까지 가장 긴 경로의 간선(Edge) 수
    - 리프 노드의 높이 : 0
    - A 노드의 높이 : 3


![](https://images.velog.io/images/kcwthing1210/post/9089225d-e293-4bbb-8d2f-ec81b3bfc087/image.png)

- Level

    - 루트에서 어떤 노드까지의 간선(Edge) 수
- Degree

    - 노드의 자식 수
    - Leaf node의 degree : 0; A의 degree : 2
- Path
    - 한 노드에서 다른 한 노드에 이르는 길 사이에 놓여있는 노드들의 순서
    - A & H 경로 : A-B-D-H
- Path Length

    - 해당 경로에 있는 총노드의 수
    - A & H 경로 길이 : 4
- Size

    - 자신을 포함한 자손의 노드 수
    - 노드 B의 size : 6
- Width

    - 레벨에 있는 노드 수
    - Level 2 width : 4
- Breadth

    - 리프 노드의 수
    - Breadth : 5
- Distance

    - 두 노드 사이의 최단 경로에 있는 간선(Edge)의 수
    - D와 J의 Distance : 3
- Order

    - 부모 노드가 가질 수 있는 최대 자식의 수
    - Order 3 : 부모 노드는 최대 3명의 자식을 가질 수 있다.


## ✅ 특징
- 하나의 루트 노드와 0개 이상의 하위 트리로 구성되어 있습니다.
- 데이터를 순차적으로 저장하지 않기 때문에 비선형 자료구조입니다.
- 트리내에 또 다른 트리가 있는 재귀적 자료구조입니다.
- 단순 순환(Loop)을 갖지 않고, 연결된 무방향 그래프 구조입니다.
- 노드 간에 부모 자식 관계를 갖고 있는 계층형 자료구조이며 모든 자식 노드는 하나의 부모 노드만 갖습니다.
- 노드가 n개인 트리는 항상 n-1개의 간선(edge)을 가집니다.
  ![](https://images.velog.io/images/kcwthing1210/post/1da8312c-7b24-4f4a-b419-2138f19b494c/image.png)

### ✔ 트리가 아닌경우
- 루트 노드가 2개(2, 8) 있으므로 트리가 아닙니다
  ![](https://images.velog.io/images/kcwthing1210/post/eaf6de45-a1a7-48b5-9eb2-fbde3ccbf64f/image.png)

- 노드 6에는 2명의 부모 노드(8,5)가 있고 사이클(2-8-6-5)이 형성되므로 트리가 아닙니다.
  ![](https://images.velog.io/images/kcwthing1210/post/09771afe-2a1c-4800-8789-832119fc4686/image.png)

## ✅ 트리 종류
### ✔ 편향 트리 (skew tree)

- 모든 노드들이 자식을 하나만 가진 트리
- 왼쪽 방향으로 자식을 하나씩만 가질 때 left skew tree, 오른쪽 방향으로 하나씩만 가질 때 right skew tree라고 함.
  ![](https://images.velog.io/images/kcwthing1210/post/e5d071e1-ce3b-4a86-bf60-3fb71536ab2b/image.png)

### ✔ 이진트리 (Binary Tree)

- 각 노드의 차수(자식 노드)가 2 이하인 트리

### ✔ 이진 탐색 트리 (Binary Search Tree, BST)

- 순서화된 이진 트리
- 노드의 왼쪽 자식은 부모의 값보다 작은 값을 가져야 하며 노드의 오른쪽 자식은 부모의 값보다 큰 값을 가져야 함.
### ✔ m 원 탐색 트리(m-way search tree)

- 최대 m개의 서브 트리를 갖는 탐색 트리
- 이진 탐색 트리의 확장된 형태로 높이를 줄이기 위해 사용함.
### ✔ 균형 트리 (Balanced Tree, B-Tree)

- m원 탐색 트리에서 높이 균형을 유지하는 트리
- height-balanced m-way tree라고도 함.


## ✅ 사용 사례
### ✔ 계층 적 데이터 저장

트리는 데이터를 계층 구조로 저장하는 데 사용됩니다.
예를 들어 파일 및 폴더는 계층적 트리 형태로 저장됩니다.
효율적인 검색 속도

효율적인 삽입, 삭제 및 검색을 위해 트리 구조를 사용합니다.
### ✔ 힙(Heap)

힙도 트리로 된 자료 구조입니다.
### ✔ 데이터 베이스 인덱싱

데이터베이스 인덱싱을 구현하는데 트리를 사용합니다.
예) B-Tree, B+Tree, AVL-Tree..
### ✔ Trie

사전을 저장하는 데 사용되는 특별한 종류의 트리입니다.


# 📌 Trie
## ✅ 트라이(Trie)란?
![](https://images.velog.io/images/kcwthing1210/post/d296cd9a-5cad-4677-8cbc-471ca080a918/image.png)

- 트라이(Trie)는 문자열을 저장하고 효율적으로 탐색하기 위한 트리 형태의 자료구조이다.

- 우리가 검색할 때 볼 수 있는 자동완성 기능, 사전 검색 등 문자열을 탐색하는데 특화되어있는 자료구조라고 한다.

- 래딕스 트리(radix tree) or 접두사 트리(prefix tree) or 탐색 트리(retrieval tree)라고도 한다. 트라이는 retrieval tree에서 나온 단어이다.

- 예를 들어 'Datastructure'라는 단어를 검색하기 위해서는 제일 먼저 'D'를 찾고, 다음에 'a', 't', ... 의 순서로 찾으면 된다. 이러한 개념을 적용한 것이 트라이(Trie)이다.

## ✅ 트라이(Trie) 장단점
- 트라이(Trie)는 문자열 검색을 빠르게 한다.

- 문자열을 탐색할 때, 하나하나씩 전부 비교하면서 탐색을 하는 것보다 시간 복잡도 측면에서 훨씬 더 효율적이다.

- 각 노드에서 자식들에 대한 포인터들을 배열로 모두 저장하고 있다는 점에서 저장 공간의 크기가 크다는 단점도 있다. (메모리 측면에서 비효율적일 수 있음!)

## ✅ 예제를 통한 트라이(Trie)의 이해
'abc', 'ab', 'car' 단어들을 'abc'부터 트라이에 저장한다고 가정해보자.

![](https://images.velog.io/images/kcwthing1210/post/aab1ecfa-70cf-443d-b00a-078344ee7182/image.png)

1. 'abc' 트라이(Trie)에 삽입

- 첫 번째 문자는 'a'이다. 초기에 트라이 자료구조 내에는 아무것도 없으므로 Head의 자식노드에 'a'를 추가해준다.
- 'a'노드에도 현재 자식이 하나도 없으므로, 'a'의 자식노드에 'b'를 추가해준다.
- 'c'도 마찬가지로 'b'의 자식노드로 추가해준다.
- 'abc' 단어가 여기서 끝남을 알리기 위해 현재 노드에 abc라고 표시한다. (Data)

![](https://images.velog.io/images/kcwthing1210/post/bb278fd8-3aef-457b-84bc-0dc8085f12b4/image.png)

2. 'ab' 트라이(Trie)에 삽입

- 현재 Head의 자식노드로 'a'가 이미 존재한다. 따라서 'a'노드를 추가하지 않고, 기존에 있는 'a'노드로 이동한다.
- 'b'도 'a'의 자식노드로 이미 존재하므로 'b'노드로 이동한다.
- 'ab' 단어가 여기서 끝이므로 현재 노드에 ab를 표시한다.
  ![](https://images.velog.io/images/kcwthing1210/post/0697c9dd-bd1b-43a5-b6ab-56b19a8c4b19/image.png)

3. 'car' 트라이(Trie)에 삽입

- Head의 자식노드로 'a'만 존재하고, 'c'는 존재하지 않는다. 따라서 'c'를 자식노드로 추가한다.
- 'c'의 자식노드가 없으므로 마찬가지로 'a'를 추가한다.
- 'a'의 자식노드가 없으므로 마찬가지로 'r'을 추가한다.
- 'car' 단어가 여기서 끝이므로 현재 노드에 car를 표시한다.
  ![](https://images.velog.io/images/kcwthing1210/post/a0493dc2-2545-4784-ba40-1e2905fdfe41/image.png)

## ✅ 트라이(Trie)에서 문자열 탐색
위에서 트라이 자료구조에 데이터를 삽입해보았는데, 이를 바탕으로 트라이에서 문자열 탐색을 진행해보려 한다.
![](https://images.velog.io/images/kcwthing1210/post/f8a873f8-8569-4cbf-8418-0c8806d180b1/image.png)
1. 위의 트라이에 'abc' 문자열이 있는지 탐색해보자.

- Head의 child에 'a'가 존재 --> 'a'노드(key='a')로 이동
- 'a'노드의 child에 'b'가 존재 --> 'b'노드(key='b')로 이동
- 'b'노드의 child에 'c'가 존재 --> 'c'노드(key='c')로 이동
- 문자열 탐색이 완료됨 --> 현재 노드('c'노드)에 Data값이 존재! --> 따라서 'abc'라는 문자열이 존재함을 알 수 있음

2. 'ca'라는 문자열이 있는지 탐색해보자.

- Head의 child에 'c'가 존재 --> 'c'노드(key='c')로 이동
- 'c'노드의 child에 'a'가 존재 --> 'a'노드(key='a')로 이동
- 문자열 탐색이 완료됨 --> 현재 노드('a'노드)에 Data값이 없음! --> 따라서 'ca'라는 문자열은 존재 X


# 🧩 Reference
- https://yoongrammer.tistory.com/68
- https://velog.io/@kimdukbae/%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0-%ED%8A%B8%EB%9D%BC%EC%9D%B4-Trie



