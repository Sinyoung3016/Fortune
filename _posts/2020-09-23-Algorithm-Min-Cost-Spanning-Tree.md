---
layout: post
title: "[알고리즘] Min-Cost Spanning Tree"
date: 2020-09-23 00:00:00
categories: [SOPHOMORE]
tags: [ALGORITHM]
last_modified_at: 2020-09-23
---

### Minimum Cost Spanning Tree

__Spanning Tree__
<p>
: 그래프에서 모든 정점을 포함하는 트리로 그래프에서 일부 간선을 선택해서 만든 트리.
<br>* 최소 연결을 해야하기에, 정점의 수가 n이면, 간선의 수는 n-1.
<br>* 트리이므로 사이클은 포함하지 않고, 여러개 존재할 수 있음.
<br>* BFS, DFS 로도 신장 트리를 찾을 수 있음.
</p>

<br>

__Min-Cost Spanning Tree__

<p>
: MST, 네트워크에서 최소비용의 신장트리
<br>* 가중치가 다른 상황에서, 단순히 가장 적은 간선을 사용한다고, 최소 비용은 아님.
</p>

<p>
따라서, MST는
<br>* 간선의 가중치의 합이 최소
<br>* n개의 정점을 가지는 그래프에 대해, n-1개의 간선만을 사용.
<br>* 사이클이 포함되면 안됨.
</p>

<p>
최소 신장비용 알고리즘
<br>* Kruskal 크루스칼 : 희소그래프
<br>* Prim 프림 : 밀집그래프
<br>* Solin 솔린
</p>

<br>

---

### Kruskal Algorithm

__Greedy Algorithm__
<p>
: 문제를 해결하는 과정에서 그 순간순간마다 최적이라고 생각되는 결정을 하는 문제해결방식
<br>1. 앞의 선택이 이후의 선택에 영향을 주지 않아야 함.
<br>2. 문제에 대한 해결방법이, 부분 문제에서도 최적의 해결 방법이어야 함.
</p>

<br>

__Kruskal Algorithm__

<p>
: Greedy를 이용하여 네트워크의 모든 정점을 최소비용으로 연결하는 답을 찾는 알고리즘.
<br>: 가장 적은 비용으로 모든 노드를 연결하자
</p>

<p>
Union-find Algorithm : 사이클 확인
<br>Priority Queue
</p>

<p>
<br>1. 그래프의 간선들을 가중치의 오름차순으로 정렬.
<br>2. 사이클을 형성하지 않은 간선을 중 가장 작은 가중치를 가지는 간선을 선택.
<br>3. 해당 간선을 현재의 MST의 집합에 추가.
</p>

<figure>
<center><img src="/Fortune/assets/sophomore/Algorithm/lec04.jpg" alt="Midnight" style="width:100%"></center>
</figure>

---

### Prim Algorithm

<p>
: Greedy를 이용하여, 시작 정점에서부터 출발해 MST를 단계적으로 확장해나가는 방법.
<br>* 어떤 정점을 시작으로 해도 같은 트리가 형성.
</p>

<p>
Priority Queue
</p>

<p>
<br>1. 시작 단계에서 시작 정점을 priority Queue 에 넣음.
<br>2. 앞 단계에서 만들어진 MST 집합에 인접한 정점들 중, 가장 낮은 가중치로 연결된 정점을 선택.
<br>3. 위의 과정을 트리가 n-1개의 간선을 가질 때까지 반복.
</p>

<figure>
<center><img src="/Fortune/assets/sophomore/Algorithm/lec04-2.jpg" alt="Midnight" style="width:100%"></center>
</figure>

<br>
<br>



