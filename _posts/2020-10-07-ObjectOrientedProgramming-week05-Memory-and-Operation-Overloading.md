---
layout: post
title: "[객체지향설계] Memory Allocation, Qualifiers, and Operator Overloading"
date: 2020-10-07 00:00:00
categories: [SOPHOMORE]
tags: [OBJECT_ORIENTED_PROGRAMMING]
last_modified_at: 2020-10-07
---

### Memory Allocation and Deallocation

#### new and delete

<p>
: keyword new와 delete로 메모리를 할당하고 해지함.
<br>: malloc()과 free()로 동적메모리를 할당하고 해지함.
</p>

#### Heap and Stack

<p>
* Stack Allocation
<br>: 변수와 함수가 선언되어 있는 것
<br>: 선언의 크기를 컴파일러가 알고 있음.
<br>: return 되면 자동적으로 해지.
<br>
<br>* Heap Allocation
<br>: 메모리가 개발자에 의해 수동적으로 할당되고 해지됨 : new delete malloc() free()
<br>: 할당한 메모리를 해지하지 않으면, 메모리 누수가 일어남.
</p>

<br>

---

### Additional Qualifiers and KeyWords

#### static

<p>
* Static Data Member
<br>: 항상 메모리에 존재해 모든 객체들에게 공유.
<br>: 외부에서 초기화를 진행함.
<br>: scope operator '::'로 접근 가능.
</p>

```{.cpp}
class A{
  private :
    static int count;
  public :
    A(){++count;}
    A(const A&){++count;}
    A(A&&){++count;}
    ~A(){--count;}
};

int A::count = 0;           //static 변수 초기화
```

<p>
* Static Member Function
<br>: static Data Member를 외부에서 직접 접근하지 않으면서, 객체를 만들지 않고 함수를 불러올 수 있음.
<br>: scope operator '::'로 접근 가능.
<br>: 'this' 사용 불가. 따라서 일반 변수는 static 함수에 접근 불가.
</p>

```{.cpp}
class A{
  public :
    static void move(){
      std::cout<<"Move"<<std:endl;
    }
};

void main(){
  A a;
  a.move();     //위아래 둘다 가능
  A::move();
}
```

#### this

<p>
: 객체 자신을 의미함.(static function 사용 불가)
</p>

```{.cpp}
class Cat{
  public :
    Cat& eat(int food);
};

Cat& Cat::eat(int food){
  weight += food;
  return *this;
//return Cat > cat1의 주소 > cat1의 값
}

void main(){
  cat1.eat(3).eat(5);
// 결론적으로 8을 먹음.
}
```

```{.cpp}
class Cat{
  public :
    Cat& eat(int food);
};

Cat Cat::eat(int food){
  weight += food;
  return *this;
//return Cat > 임시 객체 반환
}

void main(){
  cat1.eat(3).eat(5);
// 결론적으로 3을 먹음.
}
```

#### const

<p>
: 절대 변경되지 말아야할 것을 지정.
</p>

```{.cpp}
Class A {
  public :
    int getCount() const {
      return count;
    }
};

void main(){
  A a;
  const A& b = a;
}

```

#### mutable

<p>
: const member function이 mutable keyword를 가진 member를 변경 가능.
<br> 대표적인 예시로, DNS을 이용하는 데, cache를 이용하는 방법이 있음.
</p>

```{.cpp}
class A {
  private:
    mutable int count;
  public:
    void incrementCount() const {
      ++count;
    }
};
```

#### explicit

```{.cpp}
class A {
  private:
    int data;
  public:
    A(int data):data(data){};
    int getData() const {
      return data;
    }
};

void incrementAndShow(A a){
  int temp = a.getData();
}

void main(){
  incrementAndShow(3);
}
```

<p>
: 일반적인 상황에서 위의 incrementAndShow함수는 오류가 없음. 컴파일러가 자의적으로 판단해 생성자를 불러오기 때문.
하지만 오류가 날 때 이를 확인할 수 없으므로, 위와 같은 상황을 대비하기 위해 explicit을 사용.
</p>

```{.cpp}
class A {
  private:
    int data;
  public:
    explicit A(int data):data(data){};
    int getData() const {
      return data;
    }
};

void incrementAndShow(A a){
  int temp = a.getData();
}

void main(){
  incrementAndShow(3); //오류 발생
}
```
<br>

---

### Operator Overloading

<p>
* member function : 첫번째 인자인 *this, 즉 자기자신은 생략.
<br>* nonmember function : 모든 인자를 매개변수로 입력.
</p>

<figure>
<center><img src="/Fortune/assets/sophomore/OOP/11.jpg" alt="Midnight" style="width:100%"></center>
</figure>

<figure>
<center><img src="/Fortune/assets/sophomore/OOP/12.jpg" alt="Midnight" style="width:100%"></center>
</figure>


#### member function

```{.cpp}
class A {
  public:
    int x, y;
    Vector operator+(const Vector &v){
      return Vector(x+v.x, y+v.y);
    }
};

void main(){
  Vector a(1,2);
  Vector b(3,4);
  Vector c;
  c = a + b;
}
```

#### nonmember function

```{.cpp}
class A {
  public:
    int x, y;
};

Vector operator+(const Vector &u, const Vector &v){
  return Vector(u.x+v.x, u.y+v.y);
}

void main(){
  Vector a(1,2);
  Vector b(3,4);
  Vector c;
  c = a + b;
}
```

__Member vs NonMember__
<p>
* private member에 접근 가능하다면, member function을 이용.
<br>* 첫번째 피연산자가 non-class 타입이면, nonmember function을 반드시 이용.
<br>* 첫번째 인자의 변환이 필요한 경우, nonmember function을 반드시 이용.
<br>=> member는 객체 안에서 이루어지니까
</p>

#### Assignment Operator

<p>
* Copy Assignment Operator
<br>: T& operator= (const T&) {return *this;}
<br>: 인자가 lvalue
<br>
<br>* Move Assignment Operator
<br>: T& operator= (T&&) {return *this;}
<br>: 인자가 rvalue
</p>

```{.cpp}
class A {
public:
  int x, y;
  A& operator= (const A& a) { //Copy
    if(this != &a){
      x = a.x;
      y = a.y;
    }
    return *this;
  }

  A& operator= (A&& a) { //Move
    x = a.x;
    y = a.y;
    return *this;
  }
};

int main(){
  A a(1,2);
  A b(2,3);
  a = b;      //copy : b==lvalue
  a = A(3,4); //move : A(3,4)==rvalue
}
```

#### std::cout <<

<p>
: 다양한 타입의 입력값을 가지고 있음.
</p>

```{.cpp}
#include <iostream>
#include <cstring>

class MyString {
  char * stringData;
  public:
    MyString(const char *c){
      stringData = new char[strlen(stringData)];
      strcpy(stringData, c);
    }
    char& operator[] (const int index) {
      return stringData[index];
    }
    friend std::ostream& operator<< (std::ostream& os, Mystring& ms);
};

std::ostream& operator<< (std::ostream& os, MyString& ms){
  os << ms.stringData;
  return os;
}

int main(){
  MyString ms("Hello");
  std::cout << ms[1] << std::endl;
  return 0;
}

//1. operator<< (std::cout, ms) return std::cout;
//2. operator<< (std::cout, std::endl); return 출력값;
```

#### Conversion Operators

<p>
: 객체가 다른 타입이랑 연산을 가능하게 함.
<br>: static이 아니며, return type이 없음.
<br>: explicit과 implicit일때 차이가 있음.
</p>

```{.cpp}
using namespace std::literals;

class Animal {
  public:
	explicit operator int() const {return 33;}
    operator std::string const {return "Animal"s;}
};

int main(){
  Animal a;

  int i(a);
  int k = static_cast<int>(a);
  //int k = a;는 implicit converion일때만 가능.
  //explicit conversion operator(static_cast)을 사용해 Animal -> int로 전환.

  std::string s(a);
  std::string t = a;
}

```
<br>
<br>



