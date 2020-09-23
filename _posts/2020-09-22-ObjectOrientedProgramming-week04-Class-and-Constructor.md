---
layout: post
title: "[객체지향설계] Class and Constructor"
date: 2020-09-23 00:00:00
categories: [SOPHOMORE]
tags: [OBJECT_ORIENTED_PROGRAMMING]
last_modified_at: 2020-09-23
---

### Class

#### Access Specifier

<p>
: 클래스 맴버에 대한 접근을 제어.
</p>

* Public
* Private : 클래스 내의 맴버와 클래스의 friends 만 맴버에 접근 가능
* Protected

#### struct

<p>
= Class
<br>그러나 struct의 맴버는 디폴트값으로 public, class는 private.
<br>따라서 아래의 class와 struct는 같음.
</p>

```{.cpp}
struct A {
  //member
};

class B {
  public :
    //member
};
```

#### const Member Function

<p>
: const 가 있는 함수는 객체의 값을 바꿀 수 없음.
</p>

```{.cpp}
class Counter{
  private :
    int count;
  public :
    void setCount(int givenCount) {
      count = givenCount;
    }
    int getCount() const {
      return count;
    }
    int incrementCount() const { //error
      count++;
    }
};
```

#### Type Members

<p>
: 가독성을 위해서, double을 Point로 사용할거라고 말하는 것.
</p>

```{.cpp}
class A{
  public :
    using Point = double;
    Point x;
    Point y;

    A() :x(1), y(2) {};
};
```

#### friend

<p>
: 클래스의 friend는 클래스의 private 맴버에 접근 가능한 함수/클래스.
</p>

```{.cpp}
Class A {
  private :
      int a;
      void funA();
      friend class B;
      friend void C;
};

Class B {
  private :
    int b;
};

void C (){ }
```

<p>
class B는 A의 private 맴버에 접근 가능
func C도 A의 private 맴버에 접근 가능.
그러나 단방향임, 절대 양방향이 아님.
</p>

<br>

---

### Constructors

<p>
: 초기화를 위해 자동 생성됨.
<br>* 클래스와 이름이 같음
<br>* return type 없음
<br>* overload 가능
<br>* 직접 호출 불가
</p>

<br>

#### Copy Constructor

__A (const A& a)__

<p>
* copy : source를 변화시키지 않고, destination에 같은 값을 가지고옴.
<br>* 메모리 관리를 통해, deep copy를 해야함 (shallow copy에 유의!)
<br>* default copy constructor는 deep copy를 지원하지 않음. 따라서 필요하면 만들어주어야해!
</p>

```{.cpp}
class A {
  private:
    int i;
    char * c;
  public:
    A(int givenI, char * givenC){
      i = givenI;
      c = new char[strlen(givenC) + 1];
      strcpy(c, givenC);
    }
    A(const A& copyA){                      //copy constuctor
      //deep
      i = copyA.i;
      c = new char[strlen(copyA.c) + 1];    //새로운 메모리 할당
      strcpy(c, copyA.c);

      //shallow
      //i = copyA.i;
      //c = copyA.c;                        //copyA.c의 메모리를 할당받고 있어, 수정되면 c도 같이 수정됨.
    }
};

A one;
A two(one);     //copy constructor
A three = one;  //copy constructor
```

#### Move Constructor

__A (A&& a)__

<p>
* move : destination에 source와 같은 값을 가지고 옴. 그러나 source가 변했을 수도 있음.
<br>*
</p>

```{.cpp}
class A {
  private:
    int i;
    char * c;
  public:
    A(const A&& moveA){     //move constuctor
      i = moveA.i;
      c = moveA.c;          //shallow copy
      moveA.c = nullptr;
    }
};

A one;
A two(std::move(one));     //move constructor
A three = std::move(one);  //move constructor
```


#### Constructor initializer Lists

<p>
: 변수들의 선언 순서대로 초기화, 리스트의 순서와는 관련 없음.
<br> * 생성과 동시에 초기화 될 때 필요. 따라서 const, reference가 사용.
</p>

```{.cpp}
class A {
  private:
    int first;
    char * second;
  public:
    A();
    A(int givenI, char * givenC);
    A(const A& a);
};

A::A(): second(NULL), first(20) { } //Initialized List, first 먼저 초기화됨.
```

#### Destructor

__~classname()__

<p>
: 객체 소멸 시 필요.
<br>* 영역 밖으로 나가면 자동 소멸됨. (함수, 프로그램, 지역변수, delete 부를 때)
<br>* 반환값과 인자도 없음.
<br>* default destructor은 delete를 불러오지 않음. 따라서 new를 이용하면, 반드시 개발자가 구현해야함.
</p>

```{.cpp}
class A {
  private:
    int i;
    char * c;
  public:
    A(int givenI, char * givenC);   //Constructor
    ~A();                           //Destructor
};

A::A(int givenI, char * givenC){
  i = givenI;
  c = new char[strlen(givenC) + 1];
  strcpy(c, givenC);
}

A::~A(){
  delete []c; //'new' 생성자에서 만든 메모리를 정리.
}
```

<br>

### Practice

__Copy__

```{.cpp}
#define _CRT_SECURE_NO_WARNINGS
#include <iostream>
#include <string.h>
#include <vector>

class Animal {
	char* name;
	int age;
public:
	Animal(int age_, const char* name_) {
		age = age_;
		name = new char[strlen(name_) + 1];
		strcpy(name, name_);
	}
	Animal(const Animal& a) {
		age = a.age;
		name = new char[strlen(a.name) + 1];
		strcpy(name, a.name);
		std::cout << "Copy constructor is invoked!!\n";
	}
	~Animal() {
		std::cout << "Destructor!!" << std::endl;
		delete[] name;
	}
	void printAnimal() {
		std::cout << "Name: " << name << " Age: "
			<< age << std::endl;
	}
};

int main() {
	Animal A = Animal(10, "Jenny");

	A.printAnimal();

	std::vector<Animal> vec;

	std::cout << "-----1st push-----\n";
	vec.push_back(A);
	std::cout << "-----2nd push-----\n";
	vec.push_back(A);
	std::cout << "-----3rd push-----\n";
	vec.push_back(A);
	std::cout << "-----4th push-----\n";
	vec.push_back(A);
	std::cout << "-----5th push-----\n";
	vec.push_back(A);

	A.printAnimal();
	vec[0].printAnimal();
	vec[1].printAnimal();
	vec[2].printAnimal();
	vec[3].printAnimal();
	vec[4].printAnimal();

	return 0;
}

```

<figure>
<center><img src="/Fortune/assets/sophomore/OOP/09.jpg" alt="Midnight" style="width:100%"></center>
</figure>

<br>

__Copy and Move__

```{.cpp}
#define _CRT_SECURE_NO_WARNINGS
#include <iostream>
#include <string.h>
#include <vector>

class Animal {

	char* name;
	int age;
public:
	Animal(int age_, const char* name_) {
		age = age_;
		name = new char[strlen(name_) + 1];
		strcpy(name, name_);
	}
	Animal(const Animal& a) {
		age = a.age;
		name = new char[strlen(a.name) + 1];
		strcpy(name, a.name);
		std::cout << "Copy constructor is invoked!!\n";
	}
	Animal(Animal&& a) noexcept {                         //실행중에 예외가 없음을 컴파일러에게 알려줌
		age = a.age;
		name = a.name;
		std::cout << "Move constructor is invoked!!\n";
		a.name = nullptr;                                 //Shallow copy가 일어나는 변수에 nullptr를 넣어줌
	}
	~Animal() {
		std::cout << "Destructor!!" << std::endl;
		if (name) delete[] name;                          //메모리 할당에 관련된 변수가 nullptr인지 확인하고 delete
	}
	void printAnimal() {
		std::cout << "Name: " << name << " Age: "
			<< age << std::endl;
	}
};

int main() {
	Animal A(10, "Jenny");

	A.printAnimal();

	std::vector<Animal> vec;

	std::cout << "-----1st push-----\n";
	vec.push_back(A);
	std::cout << "-----2nd push-----\n";
	vec.push_back(A);
	std::cout << "-----3rd push-----\n";
	vec.push_back(A);
	std::cout << "-----4th push-----\n";
	vec.push_back(A);
	std::cout << "-----5th push-----\n";
	vec.push_back(A);

	A.printAnimal();
	vec[0].printAnimal();
	vec[1].printAnimal();
	vec[2].printAnimal();
	vec[3].printAnimal();
	vec[4].printAnimal();

	return 0;
}
```

<figure>
<center><img src="/Fortune/assets/sophomore/OOP/10.jpg" alt="Midnight" style="width:100%"></center>
</figure>

<p>
* Copy만 존재할 경우, deep으로 그만큼의 new를 만듬. 따라서 성능저하가 이루어짐.
<br>그래서 shallow를 수행하는 Move를 정의해, 불필요한 메모리할당을 줄임.
</p>

<br>
<br>



