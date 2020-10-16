---
layout: post
title: "[객체지향설계] Exception and Class Diagram"
date: 2020-10-16 00:00:00
categories: [SOPHOMORE]
tags: [OBJECT_ORIENTED_PROGRAMMING]
last_modified_at: 2020-10-16
---

### Exception

<p>
std:exception
<br>정수형의 오버플로우는 보안 문제를 일으킬 수 있음.
</p>

#### Throw, Try and Catch

```{.cpp}
bool funcA(){
  int c;
  std::cin >> c;
  if(c < 0) throw std::out_of_range("Invaild Input");
  return true;
}

void main(){
  try{
    funcA();
  }
  catch(std::out_of_range& e){
    std::cout << "Exception : " << e.what() << std::endl;
  }
}
```

<br>

#### Various Exception Types

<p>
: 인자로 들어온 예외가 예외 타입과 같은 경우, 예외 처리를 함.
</p>

```{.cpp}
#include <iostream>
#include <string>

int throwException(int c){
  if(c == 1) throw std::string("string type");
  else if(c == 2) throw 2;
  else if(c == 3) throw "Hello world";
  else if(c == 4) throw 'X';
  return 0;
}

int main(){
  int c;
  while(1){
    std::cin >> c;
    try{
      throwException(c);
    }catch(std::string& s){
      std::cout << "String type : " << s << std::endl;
    }catch(int x){
      std::cout << "Int type : " << x << std::endl;
    }catch(char x){
      std::cout << "Char type : " << x << std::endl;
    }catch(const char* s){
      std::cout << "String Literal type : " << s << std::endl;
    }
  }
}
```

<br>

#### Stack Unwinding

<p>
: 예외가 없는 일반적인 함수 호출은 스택에서 pop하면서, return함.
<br>하지만 만약 예외가 발생하면, Handler를 바로 찾아감.
<br>하지만 Handler를 실행하기 전에, 함수가 stack에 쌓인 순서대로 destructor는 반드시 부름.
</p>

```{.cpp}
#include <iostream>
#include <stdexcept>

class Test{
public:
  Test(char id) : id_(id){}
  ~Test() { std::cout << "Destructor execution :" << _id << std::endl; }

private:
  char _id;
};

int funcB(){
  Test r("B");
  throw std::runtime_error("Exception from funcB\n");
  std::cout << "Executed in B" << std::endl;
}

int funcA(){
  Test r("A");
  funcB();
  std::cout << "Executed in A" << std::endl;
  return 0;
}

void main(){
  try{
    funcA();
  }catch(std::exception& e){
    std::cout << "Exception : " << e.what(); << std::endl;
  }
}

//Destructor execution : B
//Destructor execution : A
//Exception : Exception from funcB

```

#### Catch All

<p>
: 처리되지 않은 예외는 에러가 발생하므로, 모든 타입의 예외를 받음
</p>

```{.cpp}
int funcA(){
  throw std::runtime_error("Exception from funcB\n");
}

void main(){
  try{
    funcA();
  }catch(std::runtime_error& e){
    std::cout << "Exception : " << e.what(); << std::endl;
  }catch(...){
       std::cout << "Default Exception : " << std::endl;
  }
}
```

#### noexcept

<p>
: 유저와 컴파일러에게 예외가 생기지 않음을 암시, 코드가 간단해지고, 최적화 가능.
<br>noexcept이 선언된 함수에 예외를 생성하면, 오류가 남.
</p>

```{.cpp}
int funcA() noexcept {
  ...
  return 0;
}
```

#### Rethrowing

<p>
: 동일한 예외를 상위 함수에 던져줌.
</p>


```{.cpp}
int funcA(){
  throw std::runtime_error("Exception");
  return 0;
}

int funcB(){
  try{
      funcA();
  }catch(std::runtime_error& e){
      std::cout << "Exception from A"<< std::endl;
      throws;
  }
}

void main(){
  try{
    funcB();
  }catch(std::runtime_error& e){
    std::cout << "Catch Rethrowed Exception from B" << std::endl;
  }catch(...){
       std::cout << "Default Exception" << std::endl;
  }
}

//Exception from A
//Catch Rethrowed Exception from B

```
<br>

---

### UML and Class Design

#### UML : Unified Modeling Language

<p>
: 소프트웨어 공학에서 사용되는 표준화된 범용 모델링 언어로 시스템 디자인을 시각화.
</p>

#### Class Diagram

<p>
: 여러 클래스간의 관계를 도식화 -> 전체적인 모델링
</p>

<figure>
<center><img src="/Fortune/assets/sophomore/OOP/13.jpg" alt="Midnight" style="width:100%"></center>
</figure>

<br>
<br>



