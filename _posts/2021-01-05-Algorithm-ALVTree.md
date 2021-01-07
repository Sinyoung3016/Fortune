---
layout: post
title: "[알고리즘] AVL Tree"
date: 2021-01-05 00:00:00
categories: [SOPHOMORE]
tags: [ALGORITHM]
last_modified_at: 2021-01-07
---

### AVL Tree(Adelson-Velskii, Landis Tree)

__이진탐색트리__
<p>
: 이진트리를 탐색용 자료구조로 사용하기 위해 원소 크기에 따라 노드 위치를 정의한 것
: 왼쪽 서브 트리 < 부모 노드 < 오른쪽 서브트리의 크기 관계를 가짐.
</p>

__AVL Tree__
<p>
: 대표적인 균형 이진탐색 트리
: 각 노드에서 왼쪽 서브트리의 높이와 오른쪽 서브트리의 높이의 차이가 1이하인 트리
</p>

<p>
* 왼쪽 서브 트리 높이(HL)와 오른쪽 서브 트리 높이(HR)의 차를 노드의 균형 인수(BF, Balance Factor)
* 균형인수를 항상 -1, 0, 1로 유지.
</p>

<figure>
  <center><img src="/Fortune/assets/Mogakco/1.png" alt="Midnight" style="width:100%"></center>
</figure>

<br>
<br>



