---
layout: post
title: "[알고리즘] Union-Find Algorithm"
date: 2020-09-17 00:00:00
categories: [SOPHOMORE]
tags: [ALGORITHM]
last_modified_at: 2020-09-17
---

[lab03](https://github.com/Sinyoung3016/Fortune_In_Sophomore/tree/master/AL02_Java/AL03)

### Pair-wise Disjoint Sets

__Disjoint Set__
<p>
: 다른 집합과 중복되는 원소가 없는 집합을 다루는 자료구조, 즉 하나의 원소는 반드시 하나의 집합에만 속함. 이를 상호 배타적이라고 함.
</p>


<br>

__기본 연산__

<p>
1. 초기화 : 각각의 원소를 하나의 집합으로 표현.(초기에는 원소의 개수만큼 집합이 존재)
<br>2. find(i) ; 원소 i가 속해있는 집합을 찾아, 반환한다.
<br>3. union(s1, s2) : 겹치는 원소가 없는 두 집합을 하나로 합한다.
</p>

<p>
A = {0, 1}
B = {2, 3, 4}
C = {5, 6}

union(A, C) = {0, 1, 5, 6}
find(3) = B
</p>

<br>

__Disjoint Set 표현__

<p>
* 트리구조를 통한, 1차원 배열로 표현
<br>* 각 원소는 부모원소를 가르키며, 루트는 -1을 값으로 가짐.
<br>* 루트의 배열의 인덱스는 집합의 이름으로 사용.
</p>

<br>

---

### Union Find Algorithm

__Union__

<p>
* Weighting Rule :
<br>트리의 크기를 이용해, 높이를 최소화 하는 방법으로
<br>일반적으로 트리의 크기가 큰 쪽이 트리의 높이가 클것이라고 가정.(예외도 존재)
<br>트리의 크기가 큰 쪽에 트리의 크기가 작은 트리를 붙인다.
<br>따라서 트리의 크기를 루트에 음수 값으로 저장하는 방법을 사용.
</p>

```{.java}
    public void union(int a, int b){
        a = find(a);
        b = find(b);

        if(a == b) return;
        if(tree[a] < tree[b]) {//값이 작다 == 큰 트리를 의미
            tree[a] += tree[b];
            tree[b] = a;
        }
        else{
            tree[b] += tree[a];
            tree[a] = b;
        }
    }
```

<br>

__Find__

<p>
* Collapsing Rule :
<br>트리의 노드를 최대한 높지 않게 유지한다면, find에 유리.
<br>따라서 find를 하면서 경로상의 노드들을 루트의 자식으로 만드는 것.
</p>

```{.java}
    public int find(int a){
        if(tree[a] < 0) return a; //root
        return tree[a] = find(tree[a]);
        //부모에서 자식으로 내려가면서, root와 연결시킴.
    }
```

<br>

<figure>
<center><img src="/Fortune/assets/sophomore/Algorithm/lec03.jpg" alt="Midnight" style="width:100%"></center>
</figure>

<br>
<br>



