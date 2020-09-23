---
layout: post
title: "[알고리즘] DFS and BFS"
date: 2020-09-17 00:00:00
categories: [SOPHOMORE]
tags: [ALGORITHM]
last_modified_at: 2020-09-17
---

### Depth First Search

__DFS__
<p>
깊이 우선 탐색
<br>: 임의의 노드에서 시작해, 다음 분기로 넘어가기 전에 해당 분기를 완벽하게 탐색하는 방법.
<br>* Stack과 Recursive으로 구현.
<br>* Tree Traversal이 DFS의 종류.
</p>

<p>
* 모든 노드를 방문하고자 할 때 사용.
<br>* 백트래킹, 미로찾기에 사용.
<br>* 트리의 깊이가 매우 크거나, 무한대가 될 때는 사용 X.
</p>

<br>

__DFS with Stack__

```{.java}
public class DFS_stack {
    private int numOfVertex;
    private boolean[] visited;
    private LinkedList<Integer>[] headOfAdjacencyList;

    public DFS_stack(int numOfVertex) {
        this.numOfVertex = numOfVertex;
        this.visited = new boolean[numOfVertex];
        this.headOfAdjacencyList = new LinkedList[numOfVertex];
        for (int i = 0; i < numOfVertex; i++)
            headOfAdjacencyList[i] = new LinkedList<>();
    }

    public void push(int tail, int head) {
        headOfAdjacencyList[tail].add(head);
    }

    private void DFS(int start) {
        Stack<Integer> stack = new Stack<>();
        visited[start] = true;
        stack.push(start);

        while (!stack.isEmpty()) {
            int target = stack.peek();
            Iterator<Integer> e = headOfAdjacencyList[target].iterator();
            while (e.hasNext()) {
                int value = e.next();
                if (!visited[value]) {
                    this.visited[value] = true;
                    stack.push(value);
                    break;
                }
            }
            if (!e.hasNext()) stack.pop();
        }
    }
}
```

<br>

__DFS with Recursive__

```{.java}
public class DFS_recursive {
    private int numOfVertex;
    private boolean[] visited;
    private LinkedList<Integer>[] headOfAdjacencyList;

    public DFS_recursive(int numOfVertex) {
        this.numOfVertex = numOfVertex;
        this.visited = new boolean[numOfVertex];
        this.headOfAdjacencyList = new LinkedList[numOfVertex];
        for (int i = 0; i < numOfVertex; i++)
            headOfAdjacencyList[i] = new LinkedList<>();
    }

    public void push(int tail, int head) {
        headOfAdjacencyList[tail].add(head);
    }

    private void DFS(int start) {
        visited[start] = true;
        Iterator<Integer> e = headOfAdjacencyList[start].iterator();

        while(e.hasNext()) {
            int target = e.next();
            if (!visited[target])
                DFS(target);
        }
    }
}
```

<br>

### Breadth First Search

__BFS__
<p>
너비 우선 탐색
<br>* 임의의 노드에서 시작해, 인접한 노드를 먼저 탐색하는 방법
<br>* Queue로 구현.
</p>

<p>
* 두 노드사이의 최단 경로, 임의의 경로를 찾고 싶을 때 사용.
<br>* 간선의 가중치가 같은 경우, 최단 경로를 구할 때
<br>* 간선의 가중치가 다른 경우, 최단 경로를 구할 때 = 다익스트라 알고리즘
</p>

<p>
* 지구상의 모든 친구 관계를 그래프로 표현한 후, A와 B 사이에 존재하는 경로를 찾고 싶을 때,
<br>* DFS는 모든 친구 관계를 살펴봄.
<br>* BFS는 A와 가까운 친구부터 살펴봄.
</p>

<br>

__BFS with Queue__

```{.java}
public class BFS_queue {

    private int numOfVertex;
    private boolean[] visited;
    private LinkedList<Integer>[] headOfAdjacencyList;

    public BFS_queue(int numOfVertex) {
        this.numOfVertex = numOfVertex;
        this.visited = new boolean[numOfVertex];
        this.headOfAdjacencyList = new LinkedList[numOfVertex];
        for (int i = 0; i < numOfVertex; i++)
            headOfAdjacencyList[i] = new LinkedList<>();
    }

    public void push(int tail, int head) {
        headOfAdjacencyList[tail].add(head);
    }

    private void BFS(int start) {
        Queue<Integer> queue = new LinkedList<>();
        visited[start] = true;
        queue.offer(start);

        while (!queue.isEmpty()) {
            int target = queue.poll();
            Iterator<Integer> e = headOfAdjacencyList[target].iterator();
            while (e.hasNext()) {
                int element = e.next();
                if (!visited[target]) {
                    queue.offer(element);
                    visited[target] = true;
                }
            }
        }
    }
}

```

<br>

__Time Complexity__

||Adjacency List|Adjacency Matrix|
|DFS|O(|V| + |E|)|O(V^2)|
|BFS|O(|V| + |E|)|O(V^2)|

<p>
* 단순 검색에 있어서는, BFS가 더 빠름.
</p>

<br>
<br>



