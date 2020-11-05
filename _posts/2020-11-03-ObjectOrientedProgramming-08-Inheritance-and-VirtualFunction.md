---
layout: post
title: "[객체지향설계] Inheritance and Virtual Function"
date: 2020-11-03 00:00:00
categories: [SOPHOMORE]
tags: [OBJECT_ORIENTED_PROGRAMMING]
last_modified_at: 2020-11-04
---

### Inheritance

__class derived_class : base class__

<p>
: 존재하는 클래스의 모든 멤버를 포함하는 새로운 클래스를 만듬.
<br>: 코드를 재활용할 수 있으며, 다중 상속도 가능.
</p>

<p>
* Base Class : 상속하는 Original Class
<br>* Derived Class : 상속 받는 New Class
</p>

#### Type of Inheritance

<p>
: Base Class의 public과 protected 맴버만 상속이 가능.
<br> : 상속 접근 지정자는 public, protected, private 가능하며,
<br>&emsp; Derived Class에서 상속 접근 지정자와 Base Class의 맴버의 지정자 중에서
<br>&emsp; 가장 작은 접근 지정자를 사용.
</p>

<figure>
<center><img src="/Fortune/assets/sophomore/OOP/8-1.png" alt="Midnight" style="width:100%"></center>
</figure>

__public__

```{.cpp}
class Base{
public:
  void func1() {};
protected:
  void func2() {};
private:
  int x;
};

class Derived: public Base{
public:
  void func3() {
    func1(); //public
    func2(); //protected
    //x = 0; Base의 private
  }
};

int main(){
  Derived d;
  d.func1();
  d.func3();
  //d.func2(); Derived의 protected임
  //d.x = 0;   Base의 private임
}
```

__protected__

```{.cpp}
class Base{
public:
  void func1() {};
protected:
  void func2() {};
private:
  int x;
};

class Derived: protected Base{
public:
  void func3() {
    func1(); //protected
    func2(); //protected
    //x = 0; Base의 private
  }
};

int main(){
  Derived d;
  d.func3();
  //d.func1(); Derived의 protected임
  //d.func2(); Derived의 protected임
  //d.x = 0;   Base의 private임
}
```

__private__

```{.cpp}
class Base{
public:
  void func1() {};
protected:
  void func2() {};
private:
  int x;
};

class Derived: private Base{
public:
  void func3() {
    func1(); //private
    func2(); //private
    //x = 0; Base의 private
  }
};

int main(){
  Derived d;
  d.func3();
  //d.func1(); Derived의 private임
  //d.func2(); Derived의 private임
  //d.x = 0;   Base의 private임
}
```

#### Inheritance and Constructor, Destructor

<p>
: Default 값으로 생성자는 상속되지 않음,
<br>&emsp; using을 사용하면, 생성자를 상속받을 수 있음.
</p>

```{.cpp}
class Base {
public:
  Base(): {}
  Base(int a): x(a) {}
  Base(int a, int b): x(a), y(b) {}
private:
  int x, y;
};

class Derived : public Base {
public:
  using Base::Base;
  Derived(int a): Base(-a) {}
};

int main(){
  Derived d;
  Derived d(1);
  Derived d(1, 2);
}
```

<p>
* Construction order for derived constructor
<br> 1. Base class object
<br> 2. Data member
<br> 3. Derived constructor body
</p>

<p>
* Order of Construction
</p>

<figure>
<center><img src="/Fortune/assets/sophomore/OOP/8-2.png" alt="Midnight" style="width:100%"></center>
</figure>

```{.cpp}
class Base {
  std::string s;

public:
  Base() : s("Base") { std::cout << "Base Class" << std::endl; }
  void what() { std::cout << s << std::endl; }
};

class Derived : public Base {
  std::string s;

public:
  Derived() : s("Derived"), Base() { std::cout << "Derived Class" << std::endl; }
  void what() { std::cout << s << std::endl; }
};

int main(){
  Base p;   //Base Class
  p.what(); //Base

  Derived c;//Derived Class
  c.what(); //Derived

  return 0;
}
```

#### UpCasting and DownCasting

<p>
* UpCasting
<br>: (derived => base) class pointer or reference
<br>: Always safe
<br>: 묵시적
</p>

```{.cpp}
int main(){
  Base p;
  Derived c;

  Base *pc = &c;
  pc->what();   //Base의 what이 실행.

  return 0;
}
```

<p>
* DownCasting
<br>: (base => derived) class pointer or reference
<br>: Not Always safe
<br>: 명시적 = static_cast or dynamic_cast
</p>

```{.cpp}
int main(){
  Base p;
  Derived c;

  Derived *cp = &p; //DownCasting은 무조건 컴파일 오류
  cp->what();

  return 0;
}
```

```{.cpp}
int main(){
  Base p;
  Derived c;

  Base *xx = &c;    //UpCasting
  Derived *yy = static_cast<Derived *> xx; //DownCasting, 사용자가 오류가 없다고 확신.
  cp->what();

  return 0;
}
```

```{.cpp}
int main(){
  Base p;
  Derived c;

  Base *xx = &c;    //UpCasting
  Derived *yy = dynamic_cast<Derived *> xx; //DownCasting, 오류 발생, virtual function으로 해결 가능.
  cp->what();

  return 0;
}
```

---

### Virtual Functions

<p>
* Run Time Polymorphism
<br>: 런타임(dynamic) 중에 발생하는 다형성을 의미,
<br>: 런타임 중에 주어진 타입에 맞게 다형 함수를 호출
</p>

<p>
* Virtual Function
<br>: 다형성을 가지는 맴버 함수를 의미
<br>: 참조와 포인터로 가상 함수를 호출할 때, 호출되는 실제 기능은 참조된 객체의 동적 유형
<br>: Base 함수에서 virtual을 선언하면, 자동으로 상속되므로,
<br>&emsp; 따로 선언할 필요 없으며, 오버라이드 가능.
</p>

<p>
따라서 Base 함수에서는 virtual을 선언하고, 상속 받는 함수에 대해서는 override를 선언.
<br>(override를 선언하면, 실수를 줄일 수 있음.)
</p>

<p>
* Polymorphism Class
<br>: 가상 함수를 가지고 있는 클래스를 의미
<br>: 해당 클래스의 포인터에는 virtual function table pointer가 존재하며,
<br>&emsp; 테이블이 Runtime Type Info가 들어있음.
</p>

```{.cpp}
Class Employee {
public:
  virtual void showInfo() { std::cout << "Employee" << std::endl; }
};

class Manager : public Employee {
public:
  void showInfo() override { std::cout << "Manager" << std::endl; }
};

class Intern : public Employee {
public:
  void showInfo() override { std::cout << "Intern" << std::endl; }
};

int main(){

  Employee** employList = new Employee* [4];
  employList[0] = new Intern();
  employList[1] = new Manager();
  employList[2] = new Intern();
  employList[3] = new Manager();

  employList[0]->showinfo();    //Intern
  employList[1]->showinfo();    //Manager
  employList[2]->showinfo();    //Intern
  employList[3]->showinfo();    //Manager

  return 0;
}

//virtual이 없었으면, Employee가 4번 출력
```

#### Destructors and Virtual Functions

<p>
: 상속 하는 destructors도 virtual 처리를 해야함.
<br>: 상속 받는 부분만 destruct하고 나머지를 반환하지 않으면, 메모리 누수가 생길 수 있음.
</p>

```{.cpp}
class Parent {
public:
  Parent() { std::cout << "Parent Constructor" << std::endl; }
  virtual ~Parent() { std::cout << "Parent Destructor" << std::endl; }
};

class Child : public Parent {
public:
  Child() { std::cout << "Child Constructor" << std::endl; }
  ~Child() { std::cout << "Child Destructor" << std::endl; }
};

int main(){
  { Child c; }
  {
    Parent *p = new Child();
    delete p;
  }
  return 0;
}

//P C / C C / C D / P D
//P C / C C / C D / P D
//virtual없으면, 선언된 Parent만 다루기 때문에  P C / C C / P D
```

#### Pure Virtual Function

__virtual void func() = 0;__

<p>
: 인터페이스 또는 추상클래스
<br>: 하나 이상의 순수 가상 함수를 포함하므로, 반드시 오버라이드 해야함.
</p>

```{.cpp}
class Animal {
public:
  virtual void eat() const = 0;
};

class Cat : public Animal {
public:
  virtual void eat() const override { };
};

class Dog : public Animal {
public:
  virtual void eat() const override { };
};
```

#### How Virtual Function is Invoked

<p>
: 폴리모르픽 클래스의 포인터를 생성하면, 포인터 메모리 첫부분에
해당 클래스의 virtual table을 가르키는 주소가 주어짐.
해당 테이블에는 클래스의 가상 함수 주소가 주어져 있음.
</p>

<p>
: 상속 받은 경우, 각각 클래스의 virtual table이 생성되고,
상속 받은 클래스의 가상 테이블에 주어진 가상 함수의 주소는
override를 받은 경우, 상속 받은 클래스의 함수를
안 받은 경우, Base 클래스의 함수를 가르킴.
</p>

<figure>
<center><img src="/Fortune/assets/sophomore/OOP/8-3.png" alt="Midnight" style="width:100%"></center>
</figure>

---

### Virtual, DownCasting, and dynamic_cast

<p>
<br>dynamic_cast는 런타임시 컴파일러가 캐스팅을 확인하게 함.
<br>따라서 폴리모르픽 클래스를 다룰 때 사용.
<br>만약에 유효하지 않으면, nullptr를 반환.
</p>

```{.cpp}
class Base {
  std::string s;

public:
  Base() : s("Base") { std::cout << "Base Class" << std::endl; }
  void what() { std::cout << s << std::endl; }
};

class Derived : public Base {
  std::string s;

public:
  Derived() : s("Derived"), Base() { std::cout << "Derived Class" << std::endl; }
  virtual void what() { std::cout << s << std::endl; }
  //virtual이 dynamic_cast로 런타임 중 타입을 확인하게 함.
};

int main(){
  Base p;
  Derived c;

  Base *xx = &c;
  Derived *yy = dynamic_cast<Derived*>(&p);
    //downCasting, 이때 RTTI를 사용하여 타입을 확인.
  assert(yy == nullptr); //(디버깅) 유효하지 않으므로, nullptr반환
  yy-what(); //예외발생, 그러나 nullptr로 실행 프로그램을 보호.

  return 0;
}
```

---

### Inheritance and Security

<p>
* static_cast
<br>&emsp;: 컴파일시에 전환
<br>&emsp;: fast
</p>

<p>
* dynamic_cast
<br>&emsp;: 런타임시에 전환
<br>&emsp;: RunTime Type Information을 요구
<br>&emsp;: slow - 추가적인 검증을 하니까.
</p>

```{.cpp}
class B {
  virtual ~B() {}
  inr m_B;
};

class D : public B {
  virtual ~D() {}
  inr m_D;
};

B *pB = new B();
D *pD = static_cast<D*>(pB);  //badCasting
pD->m_D;
```

|B 메모리|D 메모리|
|---|---|
|vftptr for B|vftptr for D|
|int m_B|int m_P|
||int m_D|

<p>
따라서 생성된 객체 B는 int m_D를 포함하지 않으므로,
<br>casting 후, pD에서 m_D를 불러온다는 것은 memory corruption으로 이어짐.
<br>즉 해당 위치의 이상한 값을 반환.
</p>

<p>
이를 막기 위한 방법 중, 모든 casting을 dynamic으로 바꾸어서 타입을 체크하는 방법을 생각할 수 있음.
근데, 가상함수가 있는 폴리모르픽 클래스가 아니면, 포인터가 가르키는 가상 테이블이 없어서,
다른 맴버값을 가져오게 되고 결국 런타임 오류가 남.
따라서 불가능. 일일히 폴리모르픽인지 아닌지 확인도 불가능.
</p>

<br>
<br>



