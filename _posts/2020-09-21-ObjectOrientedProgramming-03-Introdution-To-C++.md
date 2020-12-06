---
layout: post
title: "[객체지향설계] Introduction To C++"
date: 2020-09-21 00:00:00
categories: [SOPHOMORE]
tags: [OBJECT_ORIENTED_PROGRAMMING]
last_modified_at: 2020-09-21
---

> C++ = C + OOP + Generic Programming

### Namespace

<p>
: 식별자의 범위를 지정.
<br>* global scope or nested inside another Namespace
<br>* doesn't terminate with a semicolon
<br>* Instance X
</p>

<p>* Aliaz name</p>

```{.cpp}
namespace boksinyoung{
  void name();
}

namespace bsy = boksinyoung;
```

<p>
* Unnamed namespace is supported. and Using like static (해당 파일 안에서만)
</p>

```{.cpp}
namespace {
  void program();
  class functionA {};
}
```

<p>
* 여러 파일에서 같은 namespace를 정의하면 override가 아닌 span됨.
</p>

```{.cpp}
//header1.h
namespace code{
  int x;
  void program();
}

//header2
#include "header1.h";
namespace code{
  void store();
}
```

<p>
* Global namespace and Scope
</p>

```{.cpp}
#include <iostream>

int a = 10;

namespace N{

  int a = 100;
  void f(){
    int a = 1000;
    std::cout<< a <<std::endl;    //prints 1000
    std::cout<< N::a <<std:endl;  //prints 100
    std::cout<< ::a <<std:endl;   //prints 10
  }
}

int main(){
  N::f();
  system("pause");
}

```

<br>

### Pointer

<p>* Pointers</p>

```{.cpp}
int arr[10];
int *pa = arr;

int i;
int *pi = &i;
```

<p>* Pointer and Array</p>

```{.cpp}
int a[10];
int *p;

p = a;
a = p; //X

p++;
a++;   //X
```

<p>* Call by Value</p>

```{.cpp}
#include <iosteam>
using namespace std;

void increment(int x){
  ++x; //계산된 값은 안에서만
}

int main(){
  int x = 10;
  cout<< x <<endl; //10

  increment(x);
  cout<< x <<endl; //10

  return 0;
}
```

<p>* Call by Pointer</p>

```{.cpp}
#include <iosteam>
using namespace std;

void increment(int *x){
  ++*x; //메모리에서 수정했기 때문.
}

int main(){
  int x = 10;
  cout<< x <<endl; //10

  increment(&x);
  cout<< x <<endl; //11

  return 0;
}
```

<br>

### Reference

<p>: alternative name</p>

<p>* Pointer</p>

```{.cpp}
#include <iostream>

int change_val(int *p){
  *p = 3;
  return 0;
}

int main(){
  int num = 5;
  std::cout<< num <<std:endl; //5
  change_val(&num);
  std::cout<< num <<std.endl; //3
  return 0;
}
```

<p>* Reference</p>

```{.cpp}
#include <iostream>

int change_val(int &p){
  p = 3;
  return 0;
}

int main(){
  int num = 5;
  std::cout<< num <<std:endl; //5
  change_val(num);
  std::cout<< num <<std.endl; //3
  return 0;
}
```

<p>
* initialized when declared
</p>

```{.cpp}
int a = 1024;
int &ref = a;         // r-value에 변수만 가능
const int &iref = 4   // 상수취급하면 다능.

int b = 3;
ref = b;      //a = 3 자동 업데이트

int c = ref;  //c = 3 값만 줌.
```

<p>* Difference with Pointer and Reference</p>

```{.cpp}
int num = 1024;
int &ref = num;
int *p = &num;

ref++; //1024 + 1
p++    //error
```

<p>* Reference with Array</p>

```{.cpp}
int a[4] = {1,2,3,4};
int (&aref) [4] = a;

aref[0] = 10;
aref[1] = 20;

int b[2][2] = {1,2,3,4};
int (&bref)[2][2] = b;
```

<p>* Reference with Function</p>

```{.cpp}
class A {
  int x;
  int& return_ref_x() { return x; }   //return ref
  int return_x() { return x; }        //return int
  void status_x() { std::cout<< x <<std::endl; }
};

int main(){
  A a(5);
  a.status_x();               //5

  int& c = a.return_ref_x();  //ref c = ref x = a
  c = 2;
  a.status_x();               //2

  int d = a.return_ref_x();   //int d = value of ref x
  d = 1;
  a.status_x();               //2 변화X

  int& e = a.return_x();      //ref e = 상수 => error
  e = 2;
  a.status_x();
  //const int& e = a.return_x(); 로 처리해줘야 함.

  int f = a.return_x();       //int f = int x
  f = 1;
  a.status_x();               //2 변화 X

}
```

<br>
<br>



