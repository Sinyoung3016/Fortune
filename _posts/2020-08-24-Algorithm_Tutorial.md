---
layout: post
title: "[ALGORITHM] Algorithm Tutorial(ing)"
date: 2020-08-24 00:00:00
categories: [STUDY]
tags: [ALGORITHM]
last_modified_at: 2020-08-24
---

<p>* 아래의 시간복잡도는 최악시간복잡도를 의미</p>

### Sort Algorithm

__1. Stable Sort__
<br> : 비교한 값이 같을 때, 서로 바뀌지 않는 정렬

|[Bubble Sort](https://ko.wikipedia.org/wiki/%EA%B1%B0%ED%92%88_%EC%A0%95%EB%A0%AC)|거품 정렬|O(n^2)|두 인접한 원소를 검사하여 정렬|
|[Insertion Sort](https://ko.wikipedia.org/wiki/%EC%82%BD%EC%9E%85_%EC%A0%95%EB%A0%AC)|삽입 정렬|O(n^2)|배열의 앞에서부터 차례대로 이미 정렬된 배열 부분과 비교하여, 자신의 위치를 찾아 삽입하며 정렬|
|[Merge Sort](https://ko.wikipedia.org/wiki/%ED%95%A9%EB%B3%91_%EC%A0%95%EB%A0%AC)|병합 정렬|O(nlogn)|분할정복, 정렬된 작은 배열을 합쳐서 다시 정렬|

<br>

__2. Unstable Sort__
<br> : 비교한 값이 같을 때, 서로 바뀌는 정렬

|[Selection Sort](https://ko.wikipedia.org/wiki/%EC%84%A0%ED%83%9D_%EC%A0%95%EB%A0%AC)|선택 정렬|O(n^2)|배열에서 최소값을 찾아 리스트 맨 앞의 값과 교체, 맨 앞을 제외한 배열을 같은 방법으로 반복하며 정렬|
|[Quick Sort](https://ko.wikipedia.org/wiki/%ED%80%B5_%EC%A0%95%EB%A0%AC)|퀵 정렬|O(n^2)|분할정복, pivot을 기준으로 왼쪽은 작게, 오른쪽은 크게 정렬하고 배열을 둘로 나눔. 이 방법을 반복해서 정렬 |
|[Heap Sort](https://ko.wikipedia.org/wiki/%ED%9E%99_%EC%A0%95%EB%A0%AC)|힙 정렬|O(nlogn)|분할정복, 최대힙을 구성하고 얻어진 가장 큰 값을 배열의 뒤에 추가하고 크기를 1씩 줄여가며 이 방법을 반복|

<p>* Heap = 이진트리 + 우선순위큐
<br>: 최소값이나 최댓값을 빠르게 찾아내기 위해 완전 이진 트리를 기반으로 하는 트리
<br>* MaxHeap : key(부모노드) >= key(자식노드)인 완전이진트리 <-> Min Heap
<br>* Heapify Algorithm(Max)
<br>: 특정 노드의 두 자식 중에서 더 큰 자식과 자신의 위치를 바꾸는 알고리즘(하나의 노드를 제외하고는 최대힙이 구성되어 있는 상태라고 가정)
</p>
<br>

__3. ELSE__

|[Bucket Sort](https://ko.wikipedia.org/wiki/%EB%B2%84%ED%82%B7_%EC%A0%95%EB%A0%AC)|버킷 정렬|O(n^2)|n개의 data로 n개의 버킷에 범위에 따라 추가. 버킷별로 정렬하고 합침.|
|[Radix Sort](https://ko.wikipedia.org/wiki/%EA%B8%B0%EC%88%98_%EC%A0%95%EB%A0%AC)|기수 정렬|O(dn) /d:data의 가장 큰 자리수|가장 낮은 자리수부터 비교하여 정렬|

<br>

### Brute Force

### Divide and Conquer

### Dynamic Programming

|Bottom-Up(Loop)|
|Top-Down(Recursion)|

### Greedy

### Parametric Search

### Computational Geometry(계산기하)

### Tree

### Graph : Shortest Path(최단경로)

|Folyd-Warshall|
|Dijkstra|
|Bellman-Ford|

### Graph : Topological Sort(위상정렬)

### Graph : Minimum Spanning Tree(최소신장트리)

|Kruskal|
|Prim|

### Graph : Strongly Connected Components(강연결요소)

### Graph : Network Flow(네크워크 플로우)

|Ford-Fulkerson|포드 펄커슨|
|Edmonds_Karp|에드몬드 카프|
|Dinic|디닉|
|Bipartite Matching|이분 매칭|
|Minimum Cost Maximum Flow|최소 비용 최대 유량|

### String Algorithm

|Knuth-Morris-Pratt|KMP|
|Boyer_Moore|보이어-무어|
|Suffix Array|접미사 배열|
|Aho-Corasick|아호코라식|


<br>
<br>



