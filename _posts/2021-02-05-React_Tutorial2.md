---
layout: post
title: "[REACT] React Tutorial -Main Concept"
date: 2021-02-05 00:00:00
categories: [STUDY]
tags: [REACT]
last_modified_at: 2021-02-05
---

From [https://ko.reactjs.org/](https://ko.reactjs.org/)

---

<p>React 공식 문서의 주요 개념</p>

<ol>
<li>Hello world</li>
<li>JSX 소개</li>
<li>Element 렌더링</li>
<li>Component와 Props</li>
<li>State와 생명주기</li>
<li>Event 처리하기</li>
<li>조건부 렌더링</li>
<li>List와 Key</li>
<li>Form</li>
<li>State 끌어올리기</li>
<li>합성과 상속</li>
<li>React로 생각하기</li>
</ol>

---

### 1. Hello World

```{.js}
ReactDOM.render(
  <p>Hello World</p>,
  document.getElementById('root')
);
```

### 2. JSX 소개

<p>
JSX는 JS를 확장한 문법으로, react Element를 생성.
</p>

### 3. Element 렌더링

<p>
Element = React 앱의 가장 작은 단위
<br>화면에 표현할 내용을 기술하는 일반 객체.
<br>Element는 Component의 구성 요소.
<br>React DOM은 Element와 일치하도록 DOM을 업데이트.
</p>

```{.html}
<div id='root'></div>
```

<p>
이 안에 들어가는 모든 element를 ReactDOM에서 관리하므로 'root' DOM노드라고 부름.
react Element를 루트 DOM 노드에 렌더링 하려면,
ReactDOM.render() 메소드를 사용.
</p>

```{.js}
const element = <p>Hello World</p>;
ReactDOM.render(
  element,
  document.getElementById('root')
);
```

<p>
Element는 특정 시점의 UI를 보여줌.
<br>Element는 const, 즉 불변객체이므로,
변화를 위해서는 새로운 Element를 생성하고 이를 render 메소드로 전달하면서 UI를 업데이트.
</p>

### 4. Components and Props

<p>
컴포넌트를 통해 UI를 여러 부분으로 나누고, 개별적으로 살펴볼 수 있음.
</p>

<p>
컴포넌트 렌더링 중, jsx attribute와 자식을 발견하면,
<br>해당 컴포넌트에 단일 객체로 전달 = props
<br>props는 읽기 전용으로 수정이 불가능.
모든 컴포넌트는 props를 다룰때, 반드시 순수함수처럼 동작.
하지만 UI는 동적이므로, state를 이용하여 이 부분을 해결가능.
</p>

### 5. State and LifeCycle

<p>
클래스 컴포넌트에서만 state를 사용할 수 있음.
해당 컴포넌트 내부에서 일어나므로, 캡슐화의 기능을 함.
</p>

<p>
생명주기는 컴포넌트가 생성되고 사라지는 주기를 의미.
해당 시기마다 생명주기 메소드를 사용하여, 필요한 코드를 작동시킬 수 있음.
</p>

#### State 올바르게 사용하기

<p>
State는 직접 수정이 불가능, 대신 setState()를 사용.
직접 지정이 가능한 경우는, constructor 뿐.
</p>

<p>
State 업데이트는 비동기적일 수 있음.
따라서 해당 state '값'에 의존하면 안됨.
아래가 옳은 방식으로, 첫번째 괄호의 인자는 이전 상태의 인자를 의미함.
</p>

```{.js}
// Wrong
this.setState({
  counter: this.state.counter + this.props.increment,
});

//Correct
this.setState((state, props) => ({
  counter: state.counter + props.increment
}));
```
<p>
State 업데이트는 병합 가능.
</p>

---

<p>
캡슐화로 모든 컴포넌트는 각자에 대해 독립적임,
state와 관련된 컴포넌트 이외에는 접근 불가.
<br>부모는 data를 자식에게 props로 전달 가능.
이러한 방식을 하향식 또는 단방향식 데이터 흐름이라고 함.
DOM이 트리 구조이기에 모든 데이터는 자신의 아래에 있는 컴포넌트에만 영향을 줌.
</p>

### 6. Event 처리

<br>
<br>
