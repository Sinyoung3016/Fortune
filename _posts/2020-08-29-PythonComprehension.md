---
layout: post
title: "[PYTHON] Python Comprehension"
date: 2020-08-29 00:00:00
categories: [SOPHOMORE]
tags: [PYTHON]
last_modified_at: 2020-08-29
---

From [https://mingrammer.com/introduce-comprehension-of-python/](https://mingrammer.com/introduce-comprehension-of-python/)
<br>With Python

---

__Comprehension__
<p>: iterable한 객체를 생성하기 위한 방법</p>

---

### List Comprehension

```{.python}
evens = [x * 2 for x in range(11)]
#[0, 2, 4, 6, 8, 10, 12, 14, 16, 18, 20]

norm = [ x / 10 for x in evens]
#[0.0, 0.2, 0.4, 0.6, 0.8, 1.0, 1.2, 1.4, 1.6, 1.8, 2.0]

from math import sqrt
non_sqr = [x for x in range(11) if sqrt(x)**2 != x]
#[2, 3, 5, 6, 7, 8, 10]

# nested LC
pair = [(e, n) for e in range(2) for n in range(3)]
#[(0, 0), (0, 1), (0, 2), (1, 0), (1, 1), (1, 2)]

solutions = [(x, y, z) for x in range(1, 10) for y in range(x, 20) for z in range(y, 30) if x**2 + y**2 == z**2]
#[(3, 4, 5), (5, 12, 13), (6, 8, 10), (8, 15, 17), (9, 12, 15)]

# 행렬을 일차원화 시킴
matrix = [ [1,2,3,4], [5,6,7,8], [9,10,11,12] ]
flatten = [e for r in matrix for e in r]

# 'char'.join(list or tuple or string) : 리스트에서 문자열로 이때 공백사이에 char가 들어감
word = 'mathematics'
without_vowels = ''.join([c for c in word if c not in ['a','e','i','o','u']])
#mthmtcs

```

---

### Set Comprehension

```{.python}
no_primes_list = [j for i in range(2, 9) for j in range(i*2,20,i)]
#[4, 6, 8, 10, 12, 14, 16, 18, 6, 9, 12, 15, 18, 8, 12, 16, 10, 15, 12, 18, 14, 16]

no_primes_set = {j for i in range(2, 9) for j in range(i*2,50,i)}
#{4, 6, 8, 9, 10, 12, 14, 15, 16, 18}
```
---

### Dict Comprehension(hashtable, map)

```{.python}
#생성01 : zip(), 여러개의 순차 자료형을 튜플로 만들고 튜플을 원소로 하는 리스트 생성.
class_num = ['01','02','03','04']
scores = [80,90,50,60]
score_dict = {key : value for key, value in zip(class_num, scores)}

#생성02
score_tuples = [('01',80),('02',90),('03',50),('04',60)]
score_dict = {t[0]:t[1] for t in score_tuples}

#{'01': 80, '02': 90, '03': 50, '04': 60}
```

---

### Generator Expression
<p>: Generator은 iterator의 특별한 형태로, GE를 통해 생성가능.
<br> * yield를 통해 메모리를 효율적으로 사용 가능.
<br> * 계산 결과 값이 필요할 때 까지 계산을 늦출 수 있음.
<br> * LC와 비슷한 틀을 가지지만 ()로 괄호를 처리.
<br> * yield를 통해, 이를 반환하고 멈춤.
<br> * for문 또는 next를 통해 다시 불러올 때, yield 다음부터 진행 그리고 다시 yield에서 멈춤
</p>

<br>

<p>LC와 GE의 차이점</p>

```{.python}
def sleep_func(x):
    print("sleep")
    time.sleep(1)
    return x

# LC : 먼저 list의 모든 값을 먼저 수행
list = [sleep_func(x) for x in range(3)]
for i in list:
    print(i)

print("----")

# GE : for문이 돌 때 수행
gen = (sleep_func(x) for x in range(3))
for i in gen:
    print(i)

```

<figure>
<center><img src="/Fortune/assets/Python/PC/01.png" alt="Midnight" style="width:100%"></center>
</figure>

<p>Generator</p>

```{.python}
def sleep_func_gen(x):
    print("sleep")
    time.sleep(1)
    yield x

for r in range(3):
    for x in sleep_func_gen(r):
        print(x)

print("----")

for r in range(3):
    print(next(sleep_func_gen(r)))

print("----")

for r in range(3):
    print(sleep_func_gen(r))

```

<figure>
<center><img src="/Fortune/assets/Python/PC/02.png" alt="Midnight" style="width:100%"></center>
</figure>

<p>Generator Expression</p>

```{.python}
gen = (x**2 for x in range(5))
print(sum(gen))

print("----")

gen = (x**2 for x in range(5))
for i in range(5):
  print(next(gen))

print("----")

print(sum(gen))
```

<figure>
<center><img src="/Fortune/assets/Python/PC/03.png" alt="Midnight" style="width:100%"></center>
</figure>

<br>
<br>



