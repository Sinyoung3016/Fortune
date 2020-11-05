---
layout: post
title: "[알고리즘] Topological Sort"
date: 2020-11-05 00:00:00
categories: [SOPHOMORE]
tags: [ALGORITHM]
last_modified_at: 2020-11-05
---

### Topological Sort

<p>
: 순서가 있는 작업을 차례로 수행해야 할 때, 순서를 결정하는 알고리즘.
<br>: 사이클이 존재하지 않는 그래프에서만 적용 가능.
<br> DAG = Directed Acyclic Graph
<br>: 하나의 방향 그래프에서 여러 위상 정렬이 가능.
<br>: 위상 정렬의 과정에서 그래프에 남아있는 정점 중에 진입차수가 0인 정점이 없다면,
정렬이 중단되고, 해당 문제는 실행이 불가능한 문제가 됨.
</p>

<p>
1. 진입 차수가 0인 정점을 큐에 삽입.
<br>2. 큐에서 선택된 정점과 여기에 부속된 모든 간선을 삭제.
<br>3. 위의 과정을 반복해서 모든 정점이 선택, 삭제되면 알고리즘 종료.
</p>

<p>
Queue
</p>

<br>
<br>



