---
layout: post
title: "[알고리즘] Shortest Path"
date: 2020-10-16 00:00:00
categories: [SOPHOMORE]
tags: [ALGORITHM]
last_modified_at: 2020-11-05
---

### Single Source Shortest Path

<p>
: 단일 출발지 최단 경로
<br>: 하나의 출발지에서 다른 모든 정점까지의 최단경로
<br>* Dijkstra's : 음의 가중치를 허용하지 않음
<br>* Bellman-Ford : 음의 가중치를 허용
</p>

__Dijkstra's Algorithm__

<p>
: 첫 정점에 기준으로 연결되어 있는 정점을 추가해가며, 최단 거리를 갱신하는 알고리즘.
<br>: 최단 거리는 여러 개의 최단 거리로 이루어져있고, 이전까지의 최단 거리 정보를 그대로 사용하기에 DP 문제임.
</p>

<p>
1. 설정한 출발 노드를 기준으로 각 노드의 최소 비용을 저장.
<br>2. 방문하지 않은 노드 중에서 가장 비용이 적은 노드를 선택
<br>3. 해당 노드를 거쳐서 특정노드로 이동하는 경우를 고려하여 최소비용 갱신.
</p>

<figure>
<center><img src="/Fortune/assets/sophomore/Algorithm/lec7-1.jpg" alt="Midnight" style="width:100%"></center>
</figure>

__Bellman-Ford Algorithm__

<p>
: 모든 간선을 탐색하면서, 간선이 잇는 출발 정점이 한 번이라고 방문한 정점이면,
<br>해당 간선이 잇는 정점의 거리를 비교해서 갱신하고 이를 반복하는 알고리즘.
<br>: 음수 가중치가 사이클을 형성할 때는 사용할 수 없음
<br>: 해당 탐색을 n-1번 했을 때의 결과와 n번 했을 때의 결과가 같음
<br>= 사이클이 없음
</p>

<p>
1.모든 정점에 도달하는 가중치를 무한대로 초기화함.
<br>2. 해당 간선을 사용했을 때의 경로의 가중치를 비교하고 갱신.
<br>3. 정점의 개수 -1번 반복.
</p>

<p>
다익스트라의 경우, 가중치가 양수만 존재하므로, 비용은 항상 증가함.
<br>따라서 그리디하게 탐색해도 좋은 결과를 얻음.
<br>그러나 음수 가중치가 존재한다면, 돌아갔을 때
<br>더 작은 값을 얻을 수 있으므로 벨만 포드를 사용.
</p>

<figure>
<center><img src="/Fortune/assets/sophomore/Algorithm/lec7-3.jpg" alt="Midnight" style="width:100%"></center>
</figure>

<p>
* n번째와 n-1번째가 같지 않으므로 음의 사이클의 존재를 알 수 있음.
<br>* 음의 사이클이 존재 = 최소 경로를 알 수 없음.
</p>


---

### All Pairs Shortest Path

<p>
: 모든 쌍의 최단 경로
<br>: 모든 정점이 출발점이 되어 모든 정점에 대해 최단 경로를 구하는 것
<br>* Shortest Paths and Matrix Multiplication
<br>* Floyd-Warshall
</p>

__Floyd-Warshall Algorithm__

<p>
: 경유하는 정점을 기준으로 최단 거리를 구함.
<br>: 모든 정점에 대한 경로를 구하므로, 저장하는 자료구조는 2차원 배열을 이용.
<br>: 간선의 가중치가 음수인 경우에도 사용가능, 또한 DP에 의거한 알고리즘.
</p>

<p>
1. 2차원 배열을 만들고, 그래프의 간선의 정보를 저장
2. 경유지를 전부 순회하여, 2차원 테이블을 업데이트
</p>

<figure>
<center><img src="/Fortune/assets/sophomore/Algorithm/lec7-2.jpg" alt="Midnight" style="width:100%"></center>
</figure>

<br>
<br>



