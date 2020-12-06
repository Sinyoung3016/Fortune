---
layout: post
title: "[객체지향설계] Introduction to Template"
date: 2020-12-05 00:00:00
categories: [SOPHOMORE]
tags: [OBJECT_ORIENTED_PROGRAMMING]
last_modified_at: 2020-12-05
---

### Templates

<p>
: Generic programming
</p>

### Class Templates

_template<parameter_list> class_declaration_

<p>
: 실제 사용되는 시점에 코드로 변환이 됨.
<br>따라서 정의할 때는 문법 체크, 그리고 실제 활용되는 시점에서는 들어오는 타입 체크.
</p>

<p>
* 가능한 parameter
<br>: non type -상수
<br>: type
<br>: Template
<br>: parameter pack
</p>

```{.cpp}
template <typename T, int size> class CustomArray{
  T array_[size];
};

CustomArray<float, 100> myArray;
```

#### Class Template Default Parameter

```{.cpp}
template <typename T = int, int size = 2>
struct MyArray {
  T data[size];
};

void main(){
  MyArray<> a;            //int data[2]
  MyArray<double> b;      //double data[2]
  MyArray<double, 10> c;  //double data[10]
}
```

#### Qualified Dependent Names

<p>
: qualified는 specified scope을 정하는 것을 의미
<br>: typename 키워드를 통해서, type과 value에서의 모호함을 줄임.
</p>

```{.cpp}
//이때의 scope을 통해 type을 의미

template <class T> classs Vector{
public:
  using Coordinate = typename T::Coordinate;
  using Distance = typename T::Distance;

  Vector(const std::vector<Coordinate>& coords):
    coords_(coords) {}

  Distance squaredLength() const {
    Distance d = Distance(0);
    for(typename std::vector<Coordinate>::const_iterator i = coords_.begin();
      i != coords_.end(); i++){
        typename std::vector<Coordinate>::value_type x = *i;
        d += x * x;
    }
      return d;
  }
private:
  std::vector<Coordinate> cords_;
};

```

```{.cpp}
template <typename T>
int func(){
  T::t *p;
  return 0;
}
class A {
public:
  const static int t = 2;
};
class B {
public:
  using t = int;
};

void main(){
  func<A>();  // 2*p
  func<B>();  // int*p
}

```

#### Class Template Parameter Deduction

<p>
: template parameter는 생성자의 인자를 통해 추론 가능.
<br>이때, template parameter가 하나도 없어야 함.
</p>

```
std::tuple t(42, 'a')   -> tuple(int, char)
std::tuple <int> t(1,2) -> error 발생
```

---

### Function Templates

_template<parameter_list> function_declaration_

<p>
* 가능한 parameter
<br>: non type -상수
<br>: type
<br>: Template
<br>: parameter pack
</p>

```{.cpp}
template<typename T> T max(T x, T y);
template<typename T> T max(T x, T y){
  return x > y ? x : y;
}
```

#### Template Function Overload Resolution

<p>
1. nontemplate 함수 중에서 parameter가 일치
<br>2. template 함수 중에서 parameter가 일치
<br>3. 암시적 형변환을 통해 접근할 수 있는 함수(입력값은 int형이지만, double형 매개변수의 함수에)
<br>
<br>중복되거나 애매한 경우, 적절한 함수가 없는 경우 에러발생
</p>

```{.cpp}
template <typename T>
T max(T x, T y){
  return x > y ? x : y;
}

void func(int i, int j, double x, double y){
  double z = max(x, y);
  int k = max(i, j);
  z = max(i, x);            //error
  z = max<double> (i, x);   //call max<double>
}
```

#### Qualified Dependent Name

```{.cpp}
template <typename T>
void func(const T& x){
  std::vector<T> v(42, x);
  for(typename std::vector<T>::const_iterator i = v.begin(); i != v.end(); ++i){
    typename std::vector<T>::value_type x = *i;
  }
}
```

<p>
아래와 같은 애매함을 줄이기 위해 typename이 필요.
</p>

```{.cpp}
template <typename T> void func(){
  T::foo* x;
}

struct ContainsType{
  using foo = int;
};
struct ContainsValue{
  static int foo;
};

int main(){
  func<ContainsValue>();    //foo * x 곱셈
  func<ContainsType>();     //int * x pointer
}
```

---

### Template Specialization

<p>
: 구현이 달라야하는 template의 경우
<br>
<br>* Explicit Specialization : parameter을 모두 다 지정
<br>* Partial Specialization : 일부의 parmeter를 지정
<br>
<br>Class templates는 둘 다 사용 가능, Func는 explicit만 사용 가능.
</p>


#### Explicit Specialization

_Template <> declaration_

<p>
: 모든 parameter를 특정값으로 지정
</p>

#### Partial Specialization

_template <parameter_list> class_key class_name <argument_list> declaration_

<p>
: 일부 parameter를 특정값으로 지정
</p>

```{.cpp}
template <class T>
std::ostream& printPointee
(std::ostream& out, const T* p){
  return out << *p << "\n";
}

//explicit function
template <>
std::ostream& printPointee<void>
(std::ostream& out, const void* p){
  return out << *static_cast<const char *>(p) << "\n";
}

int main(){
  int i = 42;
  const int* ip = &i;
  char c = 'A';
  const void* vp = &c;
  printPointee(std::cout, ip);
  printPointee(std::cout, vp);
}
```

```{.cpp}
template <typename T>
struct is_void : std::false_type{};
template <>
struct is_void<void> : std::true_type{};

int main(){
  is_void<char>::value; //0
  is_void<int>::value;  //0
  is_void<void>::value; //1
}
```

```{.cpp}
template <typename T, typename V>
struct Animal{
  Animal() { std::cout << "unspecified version" << std::endl; }
};

template <typename T>
struct Animal<int, T>{
  Animal() { std::cout << "partial version" << std::endl; }
};

template <>
struct Animal<int, int>{
  Animal() { std::cout << "explicit version" << std::endl; }
};

int main(){
  Animal<double, float> any1;
  Animal<int, bool> any2;
  Animal<int, int> any3;
}
```

<br>
<br>



