[참고링크](https://gmlwjd9405.github.io/2018/08/28/algorithm-mst.html)

<br>

# 최소 신장트리 (MST: Minimum Spanning Tree)
* Prim MST
* ruskal MST

<br> <br><br>

## 신장트리 (Spanning Tree) 란?
* Spanning Tree = 신장 트리 = 스패닝 트리
* Spanning Tree는 그래프의 최소 연결 부분 그래프 이다.
* 최소 연결은 **간선의 수가 가장 적은** 이라는 뜻
* 사이클을 포함해서는 안된다.
* 따라서 Spanning Tree는 그래프에 있는 n개의 정점을 정확히 (n-1)개의 간선으로 연결 한다.
* 하나의 그래프에는 많은 신장 트리가 존재할 수 있다.
* 즉, 그래프에서 일부 간선만을 선택하여 만든 트리이다.
![img](https://gmlwjd9405.github.io/images/algorithm-mst/spanning-tree.png)

<br> <br> <br>

## 최소 신장 트리 (MST)
* Spanning Tree 중에서 사용된 간선들의 가중치 합이 최소인 트리
* 즉, 그래프에 있는 모든 정점들을 **가장 적은 수의 간선과 비용**으로 연결한 것을 나타냄

### Prim 알고리즘
![img](https://gmlwjd9405.github.io/images/algorithm-mst/prim-example.png)

<br> <br> 

### Kruskal 알고리즘
![img](https://gmlwjd9405.github.io/images/algorithm-mst/kruskal-example2.png)


