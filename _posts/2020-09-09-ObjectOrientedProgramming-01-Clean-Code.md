---
layout: post
title: "[객체지향설계] Clean Code"
date: 2020-09-10 00:00:00
categories: [SOPHOMORE]
tags: [OBJECT_ORIENTED_PROGRAMMING]
last_modified_at: 2020-09-10
---

### Clean Code

#### Naming

* Meaningful names
* Intention revealing names
* Pronounceable names : 이름이 길더라도 의미가 있고 발음하기 쉬운 이름
<figure>
<center><img src="/Fortune/assets\sophomore\OOP\01.jpg" alt="Midnight" style="width:100%"></center>
</figure>

* Avoid encoding : 형변환이 있을 수 있으므로 타입은 변수명에 X
<figure>
<center><img src="/Fortune/assets\sophomore\OOP\02.jpg" alt="Midnight" style="width:100%"></center>
</figure>

* Add meaningful context
<figure>
<center><img src="/Fortune/assets\sophomore\OOP\03.jpg" alt="Midnight" style="width:100%"></center>
</figure>

<br>

#### Functions

* Small(lines)
* Do one thing
* One level of abstraction : 추상화 레벨을 맞춰라

<figure>
<center><img src="/Fortune/assets\sophomore\OOP\04.jpg" alt="Midnight" style="width:100%"></center>
</figure>

* Descriptive names : 역할을 나타낼 수 있는 이름을 사용
* Reduce number of arguments : wrapping objects

<figure>
<center><img src="/Fortune/assets\sophomore\OOP\05.jpg" alt="Midnight" style="width:100%"></center>
</figure>

<br>

#### Comments

: 주석을 잘 쓸 바에는 코드를 잘 써라
<br>: 꼭 필요하다면 최소화 해라

<figure>
<center><img src="/Fortune/assets\sophomore\OOP\06.jpg" alt="Midnight" style="width:100%"></center>
</figure>

<br>

#### Error Handling

* Use Exceptions, not returning codes
* Extract Try/Catch blocks

<figure>
<center><img src="/Fortune/assets\sophomore\OOP\07.jpg" alt="Midnight" style="width:100%"></center>
</figure>

* Don't return Null : return Collections.emptyList() or Optional.empty();

<br>

#### Class

* Small(One responsibility)

<br>
<br>



