---
layout: post
title:  "그래프" 
category: Algorithm
tags: [Algorithm]
comments: true
---



## 그래프



> **그래프**

- 자료구조의 일종
- **정점(Vertex)과 간선(Edge)을 가진다**
- **정점의 차수(degree)는 정점에 연결된 간선의 개수이다**
- G = (V,E)로 나타냄
  - V = {a, b, c, d, e}
  - E = {ab, ac, bd, cd, de}
- **인접**
  - 두 정점이 간선으로 연결되어 있으면 **인접**해있다고 말한다
- **경로**
  - 두 정점 사이의 간선들을 **경로**라고 말한다
  - ex) a와 d의 경로 : abd, acd
- **사이클**
  - 정점 A에서 다시 A로 돌아오는 경로를 **사이클**이라고 한다
- **단순 경로와 단순 사이클**
  - 경로/사이클에서 같은 정점을 재방문 하지 않는 경로/사이클
  - 특별한 말이 없으면 단순 경로/사이클을 의미한다

![Graph Basics](https://www.tutorialspoint.com/data_structures_algorithms/images/graph_basics.jpg)





> **directed 그래프와 undirected 그래프**
>
> ​	간선 간에 방향이 존재하는 것

![enter image description here](https://i.stack.imgur.com/5xkVt.png)



> **Multiple Edge**
>
> ​	정점 간에 경로가 1개 이상 존재하는 그래프를 **Multigraph**라 한다

![img](https://miro.medium.com/max/1536/1*gc_apWNe2s9lXzbvl_HTYg.png)



---



### 그래프의 구현



#### 1. 인접 행렬

- **정점의 개수를 V라고 하면 V*V 크기의 2차원 배열을 이용**

- 공간복잡도 : O(V^2)
- 한 정점과 연결된 모든 간선을 찾는 시간복잡도 : O(V)

![Adjacency Matrix Representation](https://media.geeksforgeeks.org/wp-content/uploads/adjacencymatrix.png)

#### 2. 인접 리스트

- **각각의 정점에 대하여 인접한 정점을 저장**
- **링크드 리스트 이용하여 구현**

- 공간복잡도 : O(E)
- 한 정점과 연결된 모든 간선을 찾는 시간복잡도 : O(차수)

![Adjacency List Representation of Graph](https://media.geeksforgeeks.org/wp-content/uploads/listadjacency.png)





> **인접 행렬 vs 인접 리스트**
>
> 정점 (u,v) 가 인접해 있는지 확인해보는 경우 
>
> 인접 행렬의 시간복잡도 : O(1)
>
> 인접 리스트의 시간복잡도 : O(E)
>
> 그 외 경우는 인접리스트가 성능적인 이점이 있다



####  3. 간선 리스트

- **배열을 이용해서 구현하며, 간선을 모두 저장한다**

- 각 간선의 앞 정점을 기준으로 정렬하고 개수를 센다

  ![img](https://t1.daumcdn.net/cfile/tistory/99CC644F5B963A4505)

![img](https://t1.daumcdn.net/cfile/tistory/9945E7445B96554108)

- E배열에서 i 정점과 연결된 간선을 찾기 위해서 i-1 정점의 갯수와 i정점의 갯수를 더한다

  ```java
  for(int i=1; i<vertices; i++){
  	cnt[i] = cnt[i-1] + cnt[i];  
  }
  ```

- **i 정점과 연결된 간선은 cnt[i-1] <= E[edge] < cnt[i] 에 존재하게 된다.**

<br>

 ref. <a href="https://livecoding.tistory.com/49"> 블로그 </a>

