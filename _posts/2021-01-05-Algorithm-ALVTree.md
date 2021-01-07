---
layout: post
title: "[알고리즘] AVL Tree"
date: 2021-01-05 00:00:00
categories: [SOPHOMORE]
tags: [ALGORITHM]
last_modified_at: 2021-01-07
---

Reference [https://blog.naver.com/diddnjs02/222001565301](https://blog.naver.com/diddnjs02/222001565301)

---

### AVL Tree(Adelson-Velskii, Landis Tree)

__이진탐색트리__
<p>
: 이진트리를 탐색용 자료구조로 사용하기 위해 원소 크기에 따라 노드 위치를 정의한 것
<br>: 왼쪽 서브 트리 < 부모 노드 < 오른쪽 서브트리의 크기 관계를 가짐.
</p>

__AVL Tree__
<p>
: 대표적인 균형 이진탐색 트리
<br>: 각 노드에서 왼쪽 서브트리의 높이와 오른쪽 서브트리의 높이의 차이가 1이하인 트리
</p>

<p>
* 왼쪽 서브 트리 높이(HL)와 오른쪽 서브 트리 높이(HR)의 차를 노드의 균형 인수(BF, Balance Factor)
<br>* 균형인수를 항상 -1, 0, 1로 유지.
</p>

<figure>
  <center><img src="/Fortune/assets/Mogakco/1.png" alt="Midnight" style="width:100%"></center>
</figure>

__비AVL 트리__

<figure>
  <center><img src="/Fortune/assets/Mogakco/2.png" alt="Midnight" style="width:100%"></center>
</figure>

__AVL 트리의 회전 연산__
<p>
: AVL트리에서의 삽입,삭제는 균형을 맞춰주는 재구성 작업이 추가됨.
</p>

<p>
* 단순회전(Single Rotation)
<br>: 한번 회전 (LL회전 또는 RL회전)
<br>* 이중회전(Double Rotation)
<br>: 두번 회전 (LR회전 또는 RL회전)
</p>

<figure>
  <center><img src="/Fortune/assets/Mogakco/3.png" alt="Midnight" style="width:100%"></center>
  <figcaption>LL회전</figcaption>
</figure>

<figure>
  <center><img src="/Fortune/assets/Mogakco/4.png" alt="Midnight" style="width:100%"></center>
  <figcaption>LR회전</figcaption>
</figure>

<br>
<br>



