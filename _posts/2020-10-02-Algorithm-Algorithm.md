---
layout: post
title: "[알고리즘] Algorithm and Performance"
date: 2020-10-02 00:00:00
categories: [SOPHOMORE]
tags: [ALGORITHM]
last_modified_at: 2020-10-02
---

### Algorithm

<p>
: 지시대로 실행하여 특정한 일을 달성하려는 명령어들의 유한집합.
</p>

__알고리즘의 조건__

<p>
* 입력, Input
<br>&emsp;: 0개 이상이며, 일반적으로 외부에서 주어짐. 입력없이 자체적으로 가지고 있는 자료를 활용해서 일을 할 수도 있음.
<br>* 출력, Output
<br>&emsp;: 1개 이상이며, 알고리즘은 원하는 결과를 얻고자 하는 것이므로 반드시 필요.
<br>* 명확성, Definiteness
<br>&emsp;: 알고리즘의 신뢰도
<br>* 유한성, Finiteness
<br>&emsp;: 명령을 유한 개수만큼 실행하고, 하고자하는 일이 달성되어야 함. 종료되지 않으면, 알고리즘이 아님. 예를 들어 OS.
<br>* 유효성, Effectiveness
<br>&emsp;: 명령 하나하나는 컴퓨터가 쉽게 간단히 짧은 시간내에 실행할 수있는 것. 적분과 같이 긴 시간이 필요한 일을 하는 것을 하나의 명령으로 표현하는 것은 유효한 명령이 아님.
</p>

---

### Performance

<p>
* 알고리즘 성능의 주요 판단 기준 : 시간과 공간
<br>
<br>* 성능 측정 (Measurement) : 특정 컴퓨터에서 시간과 공간을 실제로 측정
<br>* 성능 분석 (Analysis) : 사용할 컴퓨터와 무관하게 필요한 시간과 공간을 이론적으로 추정
</p>

__Space Complexity__

<p>
: 프로그램이 실행을 마칠 때까지 필요한 메모리의 양
<br>
<br>* 크기가 고정된 공간, 컴파일 시 결정
<br>&emsp;: 프로그램 코드의 크기 + 크기가 정해지는 변수나 상수
<br>* 크기가 가변적인 공간, 실행되며 동적으로 결정
<br>&emsp;: 인스턴스의 특성(입출력의 개수, 값의 크기) + 재귀함수가 실행될 때, 추가로 필요한 공간.
<br>
<br>=> 공간 복잡도는 크기가 가변적인 공간이 중요.
</p>

<br>

__Time Complexity__

<p>
: 프로그램 실행에 필요한 시간
<br>
<br>* 프로그램의 실행 시간을 의미, 컴파일 시간은 상관 X.
<br>* 연산의 개수를 세서, 분석.
</p>

<figure>
<center><img src="/Fortune/assets/sophomore/Algorithm/05-1.png" alt="Midnight" style="width:100%"></center>
</figure>

<p>
* 시간복잡도의 실용적 관점.
<br>&emsp;: 측정이 아닌 추정을 하려는 것, n의 값이 매우 큰 상황을 고려해야함.
<br>* 특정 입력 데이터가 시간복잡도에 영향을 줄 수 있음.
<br>* 최선, 최악, 평균적인 경우를 고려할 필요 있음.
</p>

<br>
<br>



