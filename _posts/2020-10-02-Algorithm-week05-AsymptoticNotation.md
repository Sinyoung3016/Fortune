---
layout: post
title: "[알고리즘] Asymptotic Notation for Complexity"
date: 2020-10-02 00:00:00
categories: [SOPHOMORE]
tags: [ALGORITHM]
last_modified_at: 2020-10-02
---

### Asymptotic Notation

<p>
: 알고리즘의 복잡도를 나타내기 위한 점근 표기법
<br>: 점근 표현의 계수는 1, n이 상당히 클 때의 상황에 대한 표현
</p>

__Big-Oh__

<p>
: upper bound를 의미. + 작을 수록 좋음.
<br>
<br>f(n) = O(g(n))
<br>n0보다 크거나 같은 모든 n에 대해,
<br>부등식 f(n) <= c*g(n)을 만족시키는 양의 정수 c와 n0이 존재.
</p>

<figure>
<center><img src="/Fortune/assets/sophomore/Algorithm/05-2.png" alt="Midnight" style="width:100%"></center>
</figure>

<br>

__Big-Omega__

<p>
: lower bound를 의미. + 클 수록 좋음.
<br>
<br>f(n) = Ω(g(n))
<br>n0보다 크거나 같은 모든 n에 대해,
<br>부등식 f(n) >= c*g(n)을 만족시키는 양의 정수 c와 n0이 존재.
</p>

<br>

__Big-Theta__

<p>
<br>f(n) = Θ(g(n))
<br>n0보다 크거나 같은 모든 n에 대해,
<br>부등식 c1*g(n) <= f(n) <= c2*g(n)을 만족시키는 양의 정수 c1, c2와 n0이 존재.
</p>

<br>
<br>



