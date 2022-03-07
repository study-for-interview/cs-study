# Graph

그래프는 노드와 그 노드를 연결하는 간선을 하나로 모아 놓은 자료구조입니다.

그래프 G는 G=(V,E)로 정의한다.

여기서 V는 공백이 아닌 노드(node) 또는 정점(vertex)의 유한 집합으로 이것만을 표현할 때는 V(G)라 표기하고, E는 상이한 두 정점을 잇는 간선(edge)의 유한 집합으로 이것만을 표현할 때는 E(G)라고 표기한다.

그래프는 **무방향 그래프(undirected)와 유방향 그래프(directed)**로 구분한다.

**무방향 그래프(undirected graph)**는 간선을 표현하는 두 정점의 쌍에 순서 즉 방향이 없는 그래프이다.

따라서 두 정점 V0과 V1을 잇는 간선 (V0, V1) 과 (V1,V0)은 똑같은 간선을 나타낸다. 보통 그래프라고 하면 이 무방향 그래프를 의미한다.
 
**유방향 그래프(directed graph)** 또는 방향 그래프는 **다이그래프(digraph)**라고도 하는데 모든 간선을 순서가 있는 두 정점의 쌍으로 표현하는 즉, 간선이 방향을 가진 그래프이다.

다이그래프에서는 하나의 간선 Vj -> Vk를 <Vj,Vk>로 표현하는데 Vj를 꼬리(tail), Vk(head)를 머리(head)라 한다. 따라서 <Vj,Vk>와 <Vk,Vj>는 서로 다르다.

# 그래프에서 사용하는 용어

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcjbjPd%2FbtqKgF6OzSD%2FU0a7BKCpfJlhx1iJzwsEy1%2Fimg.png)

- 정점(vertex) : 노드(node)라고도 하며 정점에는 데이터가 저장됩니다. (0, 1, 2, 3)
- 간선(edge): 링크(arcs)라고도 하며 노드간의 관계를 나타냅니다.
- 인접 정점(adjacent vertex) : 간선에 의해 연결된 정점으로 위에서 (정점0과 정점1은 인접 정점)
- 단순 경로(simple-path): 경로 중 반복되는 정점이 없는것, 같은 간선을 자나가지 않는 경로
- 차수(degree): 무방향 그래프에서 하나의 정점에 인접한 정점의 수 (정점 0의 차수는 3)
- 진출 차수(out-degree) : 방향그래프에서 사용되는 용어로 한 노드에서 외부로 향하는 간선의 수를 뜻합니다.
- 진입차수(in-degree) : 방향그래프에서 사용되는 용어로 외부 노드에서 들어오는 간선의 수를 뜻합니다.

## 그래프 구현 방법

그래프를 구현하는 방법에는 인접행렬(Adjacency Materix)와 인접리스트(Adjacency List)방식이 있습니다.

## 인접행렬 방식

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F7RFhy%2FbtqKkOhoYiE%2FSE3IQP2q0g3xd34EQZkjM1%2Fimg.png)

인접행렬은 그래프의 노드를 2차원 배열로 만든 것입니다. 완성된 배열의 모양은 1, 2, 3, 4, 5, 6의 정점을 연결하는 노드에 다른 노드들이 인접 정점이라면 1, 아니면 0을 넣어줍니다.

## 인접행렬 장점
1. 2차원 배열 안에 모든 정점들의 간선 정보를 담기 때문에 배열의 위치를 확인하면 두 점에 대한 연결 정보를 조회할 때 O(1) 의 시간 복잡도면 가능합니다. 
2. 구현이 비교적 간편합니다.


## 인접행렬 단점
1. 모든 정점에 대해 간선 정보를 대입해야 하므로 O(n²) 의 시간복잡도가 소요됩니다.
2. 무조건 2차원 배열이 필요하기에 필요 이상의 공간이 낭비됩니다.


## 인접리스트 방식

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FNlh1G%2FbtqKicb2Wub%2FsHWVSS6bn2FZdijEJVR2r1%2Fimg.png)

인접리스트란 그래프의 노드들을 리스트로 표현한것입니다. 주로 정점의 리스트 배열을 만들어 관계를 설정해줌으로써 구현합니다. 

## 인접리스트 장점
1. 정점들의 연결 정보를 탐색할 때 O(n) 의 시간이면 가능합니다. (n: 간선의 갯수)
2. 필요한 만큼의 공간만 사용하기때문에 공간의 낭비가 적습니다.

## 인접리스트 단점
1. 특정 두 점이 연결되었는지 확인하려면 인접행렬에 비해 시간이 오래 걸립니다. (배열보다 search 속도느림)
2. 구현이 비교적 어렵습니다.

---

## 다양한 그래프의 종류 

그래프는 구현되어진 특성에 따라 여러가지 종류로 나누어집니다. 대표적인 그래프의 유형은 아래와 같습니다.

### 무방향 그래프 

- 무방향 그래프는 두 정점을 연결하는 간선에 방향이 없는 그래프입니다.

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F0ZsjG%2FbtqKjcbPzFp%2FEmai2Mc2IWMIAENKHr4Is1%2Fimg.png)


### 방향 그래프
- 방향 그래프는 두 정점을 연결하는 간선에 방향이 존재하는 그래프입니다. 간선의 방향으로만 이동할 수 있습니다. 

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fbvvxel%2FbtqKkPUXTtY%2FpsdErjeixg2KkpZWHc9NqK%2Fimg.png)


### 가중치 그래프
- 가중치 그래프는 두 정점을 이동할때 비용이 드는 그래프입니다.

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FBVFRy%2FbtqKopgFBy3%2FSlXKIsNr2avTAKIyLnwuvk%2Fimg.png)

### 완전 그래프 
- 완전 그래프는 모든 정점이 간선으로 연결되어 있는 그래프입니다.

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FmPtuW%2FbtqKqyqTexj%2FUDBayShMmL3p8LGDl25uR1%2Fimg.png)


## 그래프의 탐색 

첫 정점에서부터 그래프에 존재하는 모든 정점들을 모두 한번씩 방문하는 것을 그래프 탐색이라고 합니다. 

그래프 탐색의 방법은 깊이 우성 탐색(DFS) 방식과 너비 우선 탐색(BFS)방식이 있습니다.

![image](https://blog.kakaocdn.net/dn/cFgEJ6/btqKmoJkq5a/pwm3O8T4rERuL4wSTrkgnK/img.gif)

## DFS (Depth First Search)
DFS의 기본 작동 방식은 stack을 이용해서 갈 수 있는 만큼 최대한 깊이 가고, 더 이상 갈 곳이 없다면 이전 정점으로 돌아간다는 것이다.

stack과 recursive function을 이용하여 구현한다.

### 그래프를 인접 행렬로 표현할 경우
```java
void dfs(int x)
{
    check[x] = true;
    
    for(int i = 1; i <= V ; i++)
    {
    	if(graph[x][i] == 1 && !check[i])
        	dfs(i);
    }
}
```

## DFS의 시간 복잡도
DFS 하나에 for loop을 V 만큼 돌기 때문에, O(V) 시간이 필요함.

**정점을 방문할 때 마다 DFS를 부르는데, V개의 정점을 모두 방문하므로**
DFS의 전체 시간복잡도 = V * O(V) = O(V^2)

### 그래프를 인접 리스트로 표현할 경우

```C
void dfs(vector<int> *graph, bool *check, int x) 
{

    check[x] = true;
    
    for(int i = 0; i < graph[x].size(); i++)
    {
    	int next = graph[x][i];
        if(!check[next])
        	dfs(next);
    }
}
```

## DFS의 시간 복잡도

DFS는 총 V번 부르게 된다. 그러나, 인접 행렬로 구현한 경우와 달리 인접 리스트로 구현한 DFS는 **DFS 하나당 각 정점에 연결되어 있는 간선의 개수만큼 탐색을 하게 되어 DFS 하나의 수행 시간이 일정하지 않다.**

전체 DFS가 다 끝난 이후를 생각해 보면, DFS가 다 끝났을 시점에는 모든 정점을 한번씩 방문하고, 모든 간선을 한번씩 검사하게 되므로 O(V+E)의 시간이 걸린다고 말할 수 있다.

따라서, 인접리스트로 구현할 경우 DFS의 시간 복잡도는 O(V+E)이다.

## BFS (Breadth First Search)

BFS의 기본 작동 방식은 queue를 이용하여 지금 위치에서 갈 수 있는 것들을 모두 큐에 넣는 방식이다. 이때, queue에 넣을 시점에 해당 노드를 방문했다고 체크해야 한다. (DFS는 일단 들어가서 체크함)

BFS는 queue와 while loop을 이용하여 구현한다.

### 그래프를 인접 행렬로 표현한 경우

```c
void BFS(int V, int start)
{
    queue<int> q;
    bool check[V+1] = {false};
    
    check[start] = true;
    q.push(start);
    
    while(!q.empty())
    {
    	int now = q.front();
        q.pop();
        
        for(int i = 1; i <= V; i++)
        {
        	if(graph[now][i] == 1 && !check[i])
            {
            	check[i] = true;
                q.push(i);
            }
        }
    }
}
```

### BFS의 시간 복잡도

시간 복잡도를 계산할 때 가장 핵심이 되는 코드는 if(graph[now][i] == 1 && !check[i]) 부분이다.

정점 하나당 for loop으로 인해 해당 코드가 실행하는데 O(V)의 시간이 걸린다. 게다가, 이 for loop은 while loop을 통해 모든 정점을 한 번씩 방문할 때마다 실행되므로 V번 반복 실행된다.

따라서, 인접 행렬로 구현할 경우 BFS의 시간 복잡도 = V * O(V) = O(V^2) 이다.


### 그래프를 인접 리스트로 표현한 경우

```c
void BFS(vector<int> *graph,int V, int start)
{
    queue<int> q;
    bool check[V+1] = {false};
    
    check[start] = true;
    q.push(start);
    
    while(!q.empty())
    {
    	int now = q.front();
        q.pop();
        
        for(int i = 0; i < graph[now].size(); i++)
        {
            int next = graph[now][i];
            if(!check[next])
            {
            	check[next] = true;
                q.push(next);
            }
        }
    }
}
```
### BFS의 시간 복잡도
연결 리스트를 바탕으로 구현된 DFS의 시간 복잡도를 구할 때와 비슷한 논리로 시간 복잡도를 구할 수 있다.

인접 행렬을 이용할 때와 마찬가지로 시간 복잡도의 핵심이 되는 부분은 if(graph[now][i] == 1 && !check[i]) 부분인데, 이 부분이 반복 횟수가 일정하지 않은 for loop안에 들어가 있다.

BFS가 끝난 뒤를 생각해 보면, 해당 라인은 모든 간선에 대해서 한 번씩 비교할 것이기 때문에 총 E번 반복할 것이고, 각 정점을 한 번씩 모두 방문하여 V의 시간이 걸릴 것이다.

따라서, 인접 리스트로 구현한 BFS의 시간 복잡도는 O(V+E) 이다.


# Tree

트리 (Tree)란 노드들이 나무 가지처럼 연결된 비선형 계층적 자료구조입니다.

![IMAGE](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FeeoNuG%2Fbtq1Eo7t7Xk%2F0bPk7BzhiruKSsgtiubvK0%2Fimg.png)

트리는 또한 트리 내에 다른 하위 트리가 있고 그 하위 트리 안에는 또 다른 하위 트리가 있는 재귀적 자료구조이기도 합니다.

컴퓨터의 direcory구조가 트리 구조의 대표적인 예가 될 수 있습니다.

## 트리 구조에서 사용되는 기본 용어

![IMAGE](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcA6btV%2Fbtq1z5fVwht%2F96SGFKq5O3QtaUBabJKibK%2Fimg.png)

### 노드 (Node)

- 트리를 구성하고 있는 기본 요소
- 노드에는 키 또는 값과 하위 노드에 대한 포인터를 가지고 있음.
- A, B, C, D, E, F, G, H, I, J

### 간선 (Edge)

- 노드와 노드 간의 연결선

### 루트 노드 (Root Node)

- 트리 구조에서 부모가 없는 최상위 노드
- root node : A

### 부모 노드 (Parent Node)

- 자식 노드를 가진 노드
- H, I에 부모 노드는 D

### 자식 노드 (Child node)

- 부모 노드의 하위 노드
- 노드 D의 자식 노드는 H, I

### 형제 노드 (Sibling node)

- 같은 부모를 가지는 노드
- H, I는 같은 부모를 가지는 형제 노드

### 외부 노드(external node, outer node), 단말 노드 (terminal node), 리프 노드(leaf node)

- 자식 노드가 없는 노드
- H, I, J, F, G

### 내부 노드 (internal node, inner node), 비 단말 노드 (non-terminal node), 가지 노드 (branch node)

- 자식 노드 하나 이상 가진 노드
- A, B, C, D, E

### 깊이 (depth)

- 루트에서 어떤 노드까지의 간선(Edge) 수
- 루트 노드의 깊이 : 0
- D의 깊이 : 2

### 높이 (height)

- 어떤 노드에서 리프 노드까지 가장 긴 경로의 간선(Edge) 수
- 리프 노드의 높이 : 0
- A 노드의 높이 : 3

### 노드의 레벨(level) 
- 트리의 특정 깊이를 가지는 노드의 집합

### 노드의 차수(degree)
- 하위 트리 개수 / 간선 수 (degree) = 각 노드가 지닌 가지의 수


# 트리의 특징

- 그래프의 한 종류이다. ‘최소 연결 트리’ 라고도 불린다.

- 하나의 루트 노드와 0개 이상의 하위 트리로 구성되어 있습니다.

- 데이터를 순차적으로 저장하지 않기 때문에 비선형 자료구조입니다.

- 트리내에 또 다른 트리가 있는 재귀적 자료구조입니다.

- 단순 순환(Loop)을 갖지 않고, 연결된 무방향 그래프 구조입니다.

- 노드 간에 부모 자식 관계를 갖고 있는 계층형 자료구조이며 모든 자식 노드는 하나의 부모 노드만 갖습니다.

- 노드가 n개인 트리는 항상 n-1개의 간선(edge)을 가집니다.


# Binary Tree (이진 트리)

루트 노드를 중심으로 두 개의 서브 트리(큰 트리에 속하는 작은 트리)로 나뉘어 진 형태.  두 서브 트리도 모두 이진 트리어야 한다. 


## Full Binary Tree (전 이진 트리)
    -   1) 전 이진트리는 모든 노드가 0개 또는 2개의 자식 노드를 갖는 트리이다.

![IMAGE](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdSwyWw%2Fbtq9KmfrOlf%2F37ctrWKZKRSQJEZA7C9UMK%2Fimg.png)

## Complete Binary Tree (완전 이진트리)
    - 완전 이진트리는 마지막 레벨을 제외 하고 모든 레벨이 완전히 채워져 있다.
   - 마지막 레벨은 꽉 차 있지 않아도 되지만, 노드가 왼쪽에서 오른쪽으로 채워져야 한다.
   - 마지막 레벨 h에서 1~2h-1 개의 노드를 가질 수 있다.
   - 완전 이진 트리는 배열을 사용해 효율적으로 표현 가능하다.

![IMAGE](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fb7BofG%2Fbtq9Eilu1J5%2F0HNO2KiWkBxTvERSJGHla0%2Fimg.png)

## Binary Search Tree (이진 탐색 트리)
    - 이진 탐색 트리의 노드에 저장된 키(key)는 유일하다.
    - 부모의 키가 왼쪽 자식 노드의 키보다 크다.
    - 부모의 키가 오른쪽 자식 노드의 키보다 작다.
    - 왼쪽과 오른쪽 서브 트리도 이진 탐색 트리이다.

![IMAGE](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcycePn%2Fbtq9IZY6CZx%2FT5jBed5A535HHx1GwnJLWk%2Fimg.png)

### 이진 탐색 트리의 특징

이진 탐색 트리는 기존 이진트리보다 탐색이 빠르다. 

이진 탐색 트리의 탐색 연산은 트리의 높이(height)가 h라면 O(h)의 시간 복잡도를 갖는다.

### 이진 탐색 트리의 탐색(Search)

- 과정
    - 루트 노드의 키와 찾고자 하는 값을 비교한다. 찾고자 하는 값이라면 탐색을 종료한다.
    - 찾고자 하는 값이 루트 노드의 키보다 작다면 왼쪽 서브 트리로 탐색을 진행한다.
    - 찾고자 하는 값이 루트노드의 키보다 크다면 오른쪽 서브트리로 탐색을 진행한다. 

![IMAGE](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FpEBxn%2Fbtq9ReoXZUX%2F7zobmK5yQPPupKqGRgdHcK%2Fimg.png)

과정에 따라 무조건 **트리의 높이(H) 이하의 탐색이** 이루어진다.

### 이진 탐색 트리의 삽입(insert)
1. 삽입할 값을 루트 노드와 비교해 같다면 오류를 발생한다( 중복 값 허용 X )

2. 삽입할 값이 루트 노드의 키보다 작다면 왼쪽 서브 트리를 탐색해서 비어있다면 추가하고, 비어있지 않다면 다시 값을 비교한다.

3. 삽입할 값이 루트노드의 키보다 크다면 오른쪽 서브트리를 탐색해서 비어있다면 추가하고, 비어있지 않다면 다시 값을 비교한다.

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FczCET0%2Fbtq9Ov57XGz%2F7HO8dK5PcnF24WwHYwjOOK%2Fimg.png)

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdpBA2w%2Fbtq9RdRgKoI%2Flf9C3qqbPZtLCFYNSnJGXk%2Fimg.png)

### 이진 탐색 트리의 삭제(delete)

이진 탐색 트리에서 특정 노드를 삭제할 때 아래와 같은 3가지 상황을 나누어 구현해야 한다.

1. 삭제하려는 노드가 단말 노드(leaf node) 일 경우
    - 자식이 없는 단말 노드의 삭제는 간단하다. 삭제할 노드의 부모 노드가 있다면 부모 노드의 자식 노드를 NULL로 만들고, 삭제할 노드를 삭제(메모리 해제) 해주면 된다.

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FHjtkT%2Fbtq92w3hhp7%2Fpfi0hfaay4sj9MFMRU5rM0%2Fimg.png)

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcI7WrE%2Fbtq91NjTATG%2FCte5zTOlJJGjiNVgDO7SHK%2Fimg.png)

2. 삭제하려는 노드의 서브 트리가 하나인 경우(왼쪽 혹은 오른쪽 서브 트리)

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fc2iif8%2Fbtq9Y5ZSC52%2FH5CewcVD4MvdsLBxI9QPm1%2Fimg.png)

삭제하려는 노드의 서브 트리가 하나인 경우도 간단하다. 삭제할 노드의 자식노드를 삭제할 노드의 부모노드가 가리키게 하고 해당 노드를 삭제하면 된다. 

3. 삭제하려는 노드의 서브 트리가 두 개인 경우
![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FFa6xf%2Fbtq91pDx9u5%2FOiTC9pKYBxmjasKKTtzuK0%2Fimg.png)

이 경우 두 가지 방법을 사용할 수 있다.

1) 삭제할 노드 왼쪽 서브 트리의 가장 큰 자손을 해당 노드의 자리에 올린다.

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbcTUrX%2Fbtq92Q1tw0m%2FtyYJcuLUtWj7kD5k3qAeMK%2Fimg.png)

2) 삭제할 노드 오른쪽 서브 트리의 가장 작은 자손을 해당 노드의 자리에 올린다.

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbI3IEY%2Fbtq9Rc54r92%2FnDvEWCXdq9qVmYaYiHKAAK%2Fimg.png)


# Trie

![image](https://media.vlpt.us/images/kimdukbae/post/50497c5d-1598-48ad-b7cd-e60b2df366da/image.png)

- 트라이(Trie)는 문자열을 저장하고 효율적으로 탐색하기 위한 트리 형태의 자료구조이다.

- 우리가 검색할 때 볼 수 있는 자동완성 기능, 사전 검색 등 문자열을 탐색하는데 특화되어있는 자료구조라고 한다.

- 래딕스 트리(radix tree) or 접두사 트리(prefix tree) or 탐색 트리(retrieval tree)라고도 한다. 트라이는 retrieval tree에서 나온 단어이다.

- 예를 들어 'Datastructure'라는 단어를 검색하기 위해서는 제일 먼저 'D'를 찾고, 다음에 'a', 't', ... 의 순서로 찾으면 된다. 이러한 개념을 적용한 것이 트라이(Trie)이다.

## Trie 장단점

- 트라이(Trie)는 문자열 검색을 빠르게 한다.

- 문자열을 탐색할 때, 하나하나씩 전부 비교하면서 탐색을 하는 것보다 시간 복잡도 측면에서 훨씬 더 효율적이다.

- 각 노드에서 자식들에 대한 포인터들을 배열로 모두 저장하고 있다는 점에서 저장 공간의 크기가 크다는 단점도 있다. (메모리 측면에서 비효율적일 수 있음!)

## 예시

![image](https://media.vlpt.us/images/kimdukbae/post/9b4e8997-8c66-4509-9349-cf336b6e8a27/image.png)

1. 'abc' 트라이(Trie)에 삽입
    - 첫 번째 문자는 'a'이다. 초기에 트라이 자료구조 내에는 아무것도 없으므로 Head의 자식노드에 'a'를 추가해준다.
    - 'a'노드에도 현재 자식이 하나도 없으므로, 'a'의 자식노드에 'b'를 추가해준다.
    - 'c'도 마찬가지로 'b'의 자식노드로 추가해준다.
    - 'abc' 단어가 여기서 끝남을 알리기 위해 현재 노드에 abc라고 표시한다. (Data)
![image](https://media.vlpt.us/images/kimdukbae/post/ff402294-b59d-4866-910e-2b3ba4c423cb/image.png)

2. 'ab' 트라이(Trie)에 삽입
    - 현재 Head의 자식노드로 'a'가 이미 존재한다. 따라서 'a'노드를 추가하지 않고 기존에 있는 'a'노드로 이동한다.
    - 'b'도 'a'의 자식노드로 이미 존재하므로 'b'노드로 이동한다.
    - 'ab' 단어가 여기서 끝이므로 현재 노드에 ab를 표시한다.
![image](https://media.vlpt.us/images/kimdukbae/post/8d819895-5389-4b31-8b6b-a133e4ab3396/image.png)

3. 'car' 트라이(Trie)에 삽입
    - Head의 자식노드로 'a'만 존재하고, 'c'는 존재하지 않는다. 따라서 'c'를 자식노드로 추가한다.
    - 'c'의 자식노드가 없으므로 마찬가지로 'a'를 추가한다.
    - 'a'의 자식노드가 없으므로 마찬가지로 'r'을 추가한다.
    - 'car' 단어가 여기서 끝이므로 현재 노드에 car를 표시한다.
![image](https://media.vlpt.us/images/kimdukbae/post/8d819895-5389-4b31-8b6b-a133e4ab3396/image.png)

# 트라이(Trie)에서 문자열 탐색

![image](https://media.vlpt.us/images/kimdukbae/post/bc255f08-81f6-4031-8ac6-ca8f465ca7a3/image.png)

1. 위의 트라이에 'abc' 문자열이 있는지 탐색

    - Head의 child에 'a'가 존재 --> 'a'노드(key='a')로 이동
    - 'a'노드의 child에 'b'가 존재 --> 'b'노드(key='b')로 이동
    - 'b'노드의 child에 'c'가 존재 --> 'c'노드(key='c')로 이동
    - 문자열 탐색이 완료됨 --> 현재 노드('c'노드)에 Data값이 존재! --> 따라서 'abc'라는 문자열이 존재함을 알 수 있음

2. 'ca'라는 문자열이 있는지 탐색
    - Head의 child에 'c'가 존재 --> 'c'노드(key='c')로 이동
    - 'c'노드의 child에 'a'가 존재 --> 'a'노드(key='a')로 이동
    - 문자열 탐색이 완료됨 --> 현재 노드('a'노드)에 Data값이 없음! --> 따라서 'ca'라는 문자열은 존재 X

## 시간 복잡도

- 제일 긴 문자열의 길이를 L 총 문자열들의 수를 M이라 할 때 시간복잡도는 아래와 같습니다.
    - 생성시 시간복잡도: O(M*L), 모든 문자열들을 넣어야하니 M개에 대해서 트라이 자료구조에 넣는건 가장 긴 문자열 길이만큼 걸리니 L만큼 걸려서 O(M*L)만큼 걸립니다. 물론 삽입 자체만은 O(L)만큼 걸립니다.
    - 탐색시 시간복잡도: O(L), 트리를 타고 들어가봤자 가장 긴 문자열의 길이만큼만 탐색하기 때문에 O(L)만큼 걸립니다.

--- 

참고 : 

https://yoongrammer.tistory.com/68

https://coding-factory.tistory.com/610

https://gmlwjd9405.github.io/2018/08/12/data-structure-tree.html

https://velog.io/@kimdukbae/%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0-%ED%8A%B8%EB%9D%BC%EC%9D%B4-Trie
