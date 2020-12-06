---
layout: post
title: "[객체지향설계] Multiple Inheritance, Library and STL"
date: 2020-11-19 00:00:00
categories: [SOPHOMORE]
tags: [OBJECT_ORIENTED_PROGRAMMING]
last_modified_at: 2020-11-19
---

### Multiple Inheritance

<p>
: 하나 이상의 Base Class를 상속받는 것
<br>: Base1 과 Base2를 상속 받을 때, 두 클래스에 x변수가 있다면, 모호함을 가질 수 있음.
<br>&emsp; 따라서 Scope resolution operator(::)를 사용하려 모호함을 해결.
</p>

```{.cpp}
class Base1{
public:
  void func() {};
};

class Base2{
public:
  void func() {};
};

class Derived: public Base1, public Base2{
public:
};

int main(){
  Derived d;
  //d.func(); //error, ambigous
  d.Base1::func();
  d.Base2::func();
}
```

<p>* Diamond Problem</p>

```{.cpp}
class Animal{
protected:
  int age;
};

class Cat : public Animal { };
class Dog : public Animal { };

class DogCat : public Cat, public Dog {
//생성자 : Animal > Cat > Animal > Dog > DogCat

public:
  void setAge(){
    //age = 10; Error. ambigous
    Cat::age = 10;
  }
}

int main(){
  DogCat *dat = new DogCat();
  Animal *animal;

  //animal = dat; Error. ambigous
  animal = static_cast <Cat *> (dat);
  animal = (Cat *) dat;
}
```

<p>* Virtual Inheritance
<br> : 위의 Diamond Problem을 해결하기 위해, 상속을 받을 때 virtual 처리를 함.
</p>

```{.cpp}
class Animal{
protected:
  int age;
};

class Cat : public virtual Animal { };
class Dog : public virtual Animal { };

class DogCat : public Cat, public Dog {
//생성자 : Animal > Cat > Dog > DogCat

public:
  void setAge(){
    age = 10;
  }
}

int main(){
  DogCat *dat = new DogCat();
  Animal *animal = dat;
}
```

---

### File Input / Output

<p>
: 헤더파일 fstream 사용
</p>

__개행 문자 단위로 읽기__

```{.cpp}
#include <fstream>
#include <iostream>
#include <string>

int main(){
  std::ifstream in("test.txt");
  std::string s;

  if(in.is_open()){
    in >> s;
    std::cout << "Input text :: " << s << std::endl;
  }else{
    std::cout << Can't find the file" << std::endl;
  }

  in.close();

  return 0;
}
```

__Read Line 단위로 읽기__

```{.cpp}
#include <fstream>
#include <iostream>
#include <string>

int main(){
  std::ifstream in("testline.txt");
  char buf[100];

  if(!in.is_open()){
    std::cout << "Can't find the file" << std::endl;
  }

  while(in){
    in.getline(buf, 100);
    std::cout << buf << std::endl;
  }
  getchar();
  return 0;
}
```

__File Output__

```{.cpp}
#include <fstream>
#include <iostream>
#include <string>

int main(){
  std::ofstream out("testWrite.txt"); //Can OverWrite existing file
  std::string s;

  if(out.is_open()){
    out << "Write Test!";
  }

  return 0;
}

```

__File Output -Addition__

```{.cpp}
#include <fstream>
#include <iostream>
#include <string>

int main(){
  std::ofstream out("testWrite.txt", std::ios::app);
  //append 모드, 끝부분에 추가함.
  std::string s;

  if(out.is_open()){
    out << "Write Test!";
  }

  return 0;
}
```

__Operator Overloading__

```{.cpp}
#include <fstream>
#include <iostream>
#include <string>

class AnyString{
  std::String anyString;
  std::string getAnyString(){
    return "Stored String :: " + anyString;
  }
public:
  AnyString(const std::string& anyString) : anyString(anyString) {}

friend std::ofstream& operator<< (std::ofstream& o, AnyString& a);
};

std::ofstream& operator<< (std::ofstream& o, AnyString& a){
  o << a.getAnyString();
  return o;
}

int main(){
  std::ofstream out("testOverloading.txt");

  AnyString a("Hello");
  out << a << std::endl;

  return 0;
}
```

---

### Standard Template Library (STL)

<p>
* Container
<br>: Store objects
<br>* Iterator
<br>: Access the contents in the container
<br>* Algorithm
<br>: Define algorithms using iterators
</p>

#### Container

__Sequence Containers__

<p>순서가 있음</p>

<p>
* vector
<br>: 자동으로 확장 가능한 배열
<br>: 배열 중간에 삽입, 삭제가 느림.
</p>

```{.cpp}
#include <iostream>
#include <vector>

int main(){
  std::vector<int> vec;
  vec.push_back(11);
  vec.push_back(22);
  vec.push_back(33);
  vec.push_back(44);

  for(int i = 0; i < vec.size(); i++)
    std::cout << "Vector element " << i + 1 << " : " << vec[i] << std::endl;

  for(std::vector<int>::iterator i = vec.begin(); i != vec.end(); ++i)
    std::cout << "Vector element :" << *i << std::endl;
    //*iterator를 통해 해당 위치의 값을 가지고 옴.

  for(auto element : vec) //auto :컴파일러가 판단해서 타입을 정함.
    std::cout << "Vector element :" << element << std::endl;

  return 0;
}
```

<p>
* list
<br> : double linked list
<br> : 삽입 삭제가 빠름.
<br> : 랜덤 접근이 느림.
</p>

```{.cpp}
#include <iostream>
#include <list>

int main(){
  std::list<char> list;
  list.push_back('A');
  list.push_back('b');
  list.push_back('c');
  list.push_back('3');

  for(std::list<char>::iterator i = list.begin(); i != list.end(); ++i)
    std::cout << *i << std::endl;
    //*iterator를 통해 해당 위치의 값을 가지고 옴.

  return 0;
}
```
<p>
* vector와 list의 차이
<br>: Vector 랜덤접근 가능
<br>> itr++, itr--, itr + 5
<br>: List 한칸씩 접근 가능
<br>> itr++, itr--
</p>

<p>
* deque
<br> : double ended queue
</p>

```{.cpp}
#include <iostream>
#include <deque>

int main(){
  std::deque<int> dq;
  dq.push_back(22);
  dq.push_back(33);
  dq.push_front(11);
  dq.push_front(44);

  std::cout << "Initial safe of dq :" << std::endl;
  for(const auto& element : dq)
    std::cout << "Deque element :" << element << std::endl;

  std::cout << "Remove first element :" << std::endl;
  dp.pop_front();
  for(const auto& element : dq)
      std::cout << "Deque element :" << element << std::endl;

  return 0;
}
```

<p>
* vector와 deque의 차이
<br>: deque가 더 빠르고, 더 많은 메모리를 필요로 함.
<br>: vector는 확장할 때마다, 삭제와 복사를 반복, 그러나 deque는 필요하면 추가함.
<br>: 포인터와 데이터를 저장할 메모리가 필요하며, 사용하지 않은 공간이 더 많음.
</p>

<figure>
<center><img src="/Fortune/assets/sophomore/OOP/9-1.png" alt="Midnight" style="width:100%"></center>
</figure>

__Associative Containers__

<p>: key를 사용하여 data에 접근.
<br>: key는 중복될 수 없음.
<br>: 자동 정렬이 되므로, 사용자 정의 클래스의 경우 기준을 만들어줘야함.</p>

<p>
* set
<br>: 저장되는 data가 key.
</p>

```{.cpp}
#include <iostream>
#include <set>
#include <string>

int main(){
  std::set<std::string> setOfNumbers;

  setOfNumbers.insert("first");
  setOfNumbers.insert("second");
  setOfNumbers.insert("third");
  setOfNumbers.insert("first");

  std::cout << "Set size = " << setOfNumbers.size() <<std::endl;

  for(std::set<std::string>::iterator i = setOfNumbers.begin(); i != setOfNumbers.end(); ++i)
    std::cout << *i <<std::endl;

  return 0;
}
```

```{.cpp}
#include <iostream>
#include <set>
#include <string>

struct CompMyInt;

class MyInt{
  int myInt;
public:
  MyInt(int i){
    myInt = i;
  }
  friend std::ostream& operator<<(std::ostream& os, MyInt& mi);
  friend CompMyInt;
};

std::ostream& operator<<(std::ostream& os, MyInt& mi){
  os << mi.myInt;
  return os;
}

struct CompMyInt{
  bool operator() (const MyInt& a, const MyInt& b){
    return a.myInt < b.myInt;
  }
};

int main(){
  std::set<MyInt, CompMyInt> setOfMyInt;

  MyInt a(10);
  MyInt b(90);
  MyInt c(3);
  MyInt d(1);

  setOfMyInt.insert(a);
  setOfMyInt.insert(b);
  setOfMyInt.insert(c);
  setOfMyInt.insert(d);

  std::cout << "Set Size = " << setOfMyInt.size() << std::endl;

  for(std::set<MyInt>::iterator i = setOfMyInt.begin(); i != setOfMyInt.end(); ++i){
    MyInt mi = *i;
    std::cout << mi << std::endl;
  }
  return 0;
}

```

<p>
* map
<br>: 저장되는 data가 pair로 key와 value로 되어있음.
</p>

<p>
* multiset/map
<br>: 중복되는 key를 허용.
</p>

__Derived Containers__
<p>
: stack, queue, priority_queue
</p>

<br>
<br>



