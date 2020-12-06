---
layout: post
title: "[객체지향설계] Advanced to Template"
date: 2020-12-05 00:00:00
categories: [SOPHOMORE]
tags: [OBJECT_ORIENTED_PROGRAMMING]
last_modified_at: 2020-12-05
---

### Variadic Template

<p>
: 가변 인자를 받는 Template
<br>: 이때 가변 인자는 Parameter pack(...)을 사용.
</p>

#### Variadic Function

```{.cpp}
#include <stdarg.h> //필수 헤더로 메크로를 제공.

double average(int count, ...){
    va_list ap; //stack에 pointer선언
    int j;
    double sum = 0;

    va_start(ap, count); //ap 초기화
    for(j = 0; j < count; j++)
        sum += va_arg(ap, int); //포인터를 int크기만큼 이동시키면서, 메모리의 값을 받아옴.

    va_end(ap);
    return sum/count;
}

int main(){
    printf("%f", average(4,1,2,3,7));
    return 0;
}
```

#### Parameter Packs

<p>
* non type template parameter pack
<br>: type... Args

<br>* Type template parameter pack
<br>: typename... Args or class... Args

<br>* Function parameter pack
<br>: Args... args
</p>

```{.cpp}
template <int...ls> //int형으로 여러개를 받음.

template <typename...Ts> //여러 타입을 받을 수 있음.
template <class... Ts>

template <typename... Ts> void func(Ts... args)
```

#### sizeof operator

_sizeof...(args)_

<p>
: 가변 인자의 인자가 몇개 인지 개수를 반환해주는 연산자
</p>

#### Variadic Template Example

```{.cpp}
template <typename T, T... Values>
class Integer_sequence{
public:
  using const_iterator = const T*;
  std::size_t size() const{
    return sizeof...(Values);
  }
  T operator [] (int i) const { return Values_[i]; }
  //꺽쇠도 오버라이드 해주어야함.

  const_iterator begin() const {
    return &Values_[0];
  }
  const_iterator end() const {
    return &Values_[size()];
  }
private:
  T Values_[sizeof...(Values)] = {Values...};
};

int main(){
  Integer_sequence<std::size_t, 1, 2, 3, 4, 5> seq;
  seq.size(); //5
  seq[0];     //1
  for(auto i : seq) { std::cout << i << "\n"; }
  //해당 반복문을 위해서 클래스에 begin과 end가 필요.
}
```

```{.cpp}
template <typename T>
void printArg(T arg){
  std::cout << arg << std::endl;
  //재귀문의 초기값
}

template <typename T, typename... Types>
void printArg(T arg, Types... args){
  std::cout << arg << ",";
  printAtg(args...);
}

int main(){
  printArgs(9, "A", 1.0);
}
```

---

### Fold Expression

<p>
: 재귀 대신 사용하는 연산자

<br>* op : binary operator
<br>* E : parameter pack에 확장되는 표현
<br>* I : parameter pack에 확장되지 않는 표형
</p>

<figure>
<center><img src="/Fortune/assets/sophomore/OOP/10.png" alt="Midnight" style="width:100%"></center>
</figure>

```
using namespace std::string_literals;

template <typename T, typename...Args>
auto sum(T x, Args...args){
  return x + (... + args); //binary left fold expression
}
 n
int main(){
  auto x = sum(42.5, -1.0, 0.5);
  //((42.5 + (-1.0)) + 0.5)
}
```
---

### Functor = Function Object

<p>
: 함수와 비슷한 역할을 하지만 Object로 구현.
<br>: 유연성이 있으며 상태를 저장할 수 있다는 장점이 있음.
<br> : STL에 주로 사용.

<br> : 함수 호출에 대한 operator overloading시, 항상 member function으로
</p>

```{.cpp}
struct LessThan {
  bool operator() (double x, double y) const {
    return x < y;
  }
};

void main(){
  double x = 1.7;
  double y = 2.3;
  LessThan lessThan; //Functor
  bool result = lessThan(x, y);
}
```

```{.cpp}
class IsGreater {
public:
  IsGreater(int threshold) : threshold_(threshold) {}
  bool operator()(int x) const {
  return x > threshold_;
  }
private:
  int threshold_;
};

void main(){
  IsGreater isGreater(5);     //생성자
  int x = 3;
  bool result = isGreater(x); //functor
}
```

#### Function vs Functor

```{.cpp}
int increment(int x) {return (x+1);}
int main(){
  int arr[] = {1,2,3,4,5};
  int n = sizeof(arr)/sizeof(arr[0]);

  std::transform(arr, arr+n, arr, increment);
  //arr부터 arr+n까지 increment함수를 실행하서 arr에 저장.
  //이때 실행되는 함수는 인자를 하나만 받음.

  for(int i = 0; i < n; i++)
    std::cout << arr[i] << " ";
  //2 3 4 5 6

  return 0;
}
```

<p>
Function은 하드 코딩의 특징을 지님.
<br>(increment에서 매직넘버를 사용)
<br>따라서 위의 상황에서 인자를 두개를 받아서 처리할 수도 있지만,
<br>저 상황에서 transform함수는 인자를 1개만 받는 함수를 대상으로만 실행됨.
<br> 따라서 위와 같은 상황을 Functor로 유연하게 처리가능.
</p>

```{.cpp}
class increment{
int num;
public:
  increment(int x) : num(x) {}
  int operator() (int arr_num) const {
    return num + arr_num;
  }
};

int main(){
  int arr[] = {1,2,3,4,5};
  int n = sizeof(arr)/sizeof(arr[0]);
  int to_add = 5;

  std::transform(arr, arr+n, arr, increment(to_add));

  for(int i = 0; i < n; i++)
    std::cout << arr[i] << " ";
  //6 7 8 9 10

  return 0;
}
```

---

### Tailing Return Type

_std::decltype_

<p>
: Template를 사용시 여러개의 type을 사용할 때, 반환값에 따라 반환 타입이 달라질 수 있음.
</p>

```{.cpp}
template <typename FirstType, typename SecondType>
auto AddArbitrary(FirstType t1, SecindType t2) -> decltype(t1 + t2){
  return t1 + t2;
}

int main(){
  AddArbitrary(10.0, 'C');
  std::string s1 = "A";
  std::string s2 = "B";
  AddArbitrary(s1, 'C');
  AddArbitrary(s1, s2);
  AddArbitrary("A", 'C');
}
```

<br>
<br>



