---
layout: post
title: "[REACT] React Tutorial -Main Concept"
date: 2021-02-05 00:00:00
categories: [STUDY]
tags: [REACT]
last_modified_at: 2021-02-11
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

<p>
this.setState({comments})는 this.state.comments에만 영향 줌.
</p>

```{.js}
constructor(props) {
    super(props);
    this.state = {
      posts: [],
      comments: []
    };
  }

componentDidMount() {
    fetchPosts().then(response => {
      this.setState({
        posts: response.posts
      });
    });

    fetchComments().then(response => {
      this.setState({
        comments: response.comments
      });
    });
  }
```

---

<p>
캡슐화로 모든 컴포넌트는 각자에 대해 독립적임,
state와 관련된 컴포넌트 이외에는 접근 불가.
<br>부모는 data를 자식에게 props로 전달 가능.
이러한 방식을 하향식 또는 단방향식 데이터 흐름이라고 함.
DOM이 트리 구조이기에 모든 데이터는 자신의 아래에 있는 컴포넌트에만 영향을 줌.
</p>

### 6. Event 처리

<p>
React의 이벤트를 camelCase로 표현.
<br>JSX을 이용해 함수로 이벤트 핸들러를 전달.
</p>

```{.js}
<button onClick={activateLasers}>
  Activate Lasers
</button>
```

<p>
함수의 기본 동작을 막기 위해서,
<br>html에서는 return false로 해결 가능.
<br>그러나 React에서는 preventDefault가 필수적.
</p>

```{.js}
function ActionLink() {
  function handleClick(e) {
    e.preventDefault();
    console.log('The link was clicked.');
  }

  return (
    <a href="#" onClick={handleClick}>
      Click me
    </a>
  );
}
```

<p>
일반적으로 이벤트 핸들러는 해당 함수 또는 클래스의 내부에 메소드로 만듬.
</p>

<p>
JS에서 기본적으로 클래스 메소드는 바인딩이 되어있지 않음.
<br>onClick={this.handleClick}과 같이 ()표기가 없이 메소드를 참조할 때, 바인딩이 필수.
</p>

<p>
퍼블릭 클래스 필드 문법은 create react app에 기본으로 설정되어있음.
</p>

```{.js}
class LoggingButton extends React.Component {
  // 이 문법은 `this`가 handleClick 내에서 바인딩되도록 합니다.
  handleClick = () => {
    console.log("bind");
  }

  render() {
    return (
      <button onClick={this.handleClick}>
        Click me
      </button>
    );
  }
}
```

<p>
이벤트 핸들러에 인자 전달도 가능
</p>

### 7. 조건부 렌더링

<p>
원하는 동작을 캡슐화 하는 컴포넌트를 만들 수 있음.
이를 통해 앱의 상태에 따라서 일부 컴포넌트만 렌더링 가능.
</p>

```{.js}
class LoginControl extends React.Component {
  constructor(props) {
    super(props);
    this.handleLoginClick = this.handleLoginClick.bind(this);
    this.handleLogoutClick = this.handleLogoutClick.bind(this);
    this.state = {isLoggedIn: false};
  }

  handleLoginClick() {
    this.setState({isLoggedIn: true});
  }

  handleLogoutClick() {
    this.setState({isLoggedIn: false});
  }

  render() {
    const isLoggedIn = this.state.isLoggedIn;
    let button;
    if (isLoggedIn) {
      button = <LogoutButton onClick={this.handleLogoutClick} />;
    } else {
      button = <LoginButton onClick={this.handleLoginClick} />;
    }

    return (
      <div>
        <Greeting isLoggedIn={isLoggedIn} />
        {button}
      </div>
    );
  }
}

ReactDOM.render(
  <LoginControl />,
  document.getElementById('root')
);
```

<p>
중괄호와 논리연산자로 조건문을 인라인으로 표현 가능
</p>

```{.js}
function Mailbox(props) {
  const unreadMessages = props.unreadMessages;
  return (
    <div>
      <h1>Hello!</h1>
      {unreadMessages.length > 0 &&
        <h2>
          You have {unreadMessages.length} unread messages.
        </h2>
      }
    </div>
  );
}
```

<p>
JS에서 true && expression은 항상 expression,
false && expression은 항상 무시.
</p>

<p>
삼항연산자로, if else구문 인라인으로 표현,
복잡하면 컴포넌트로 분리할 수 있음.
</p>

### 8. List와 Key

<p>
map()메소드는 배열의 요소에 대해 주어진 함수를 호출한 결과를 모아 새로운 배열을 반환.
</p>

<p>
map을 사용하기 위해서는 각 요소에 고유값인 key를 지정해줘야 함.
같은 리스트 안의 형제 요소들 사이에서 고유해야함.
</p>

### 9. Form

<p>
html에서 form 엘리먼트는 사용자 입력을 기반으로 자신의 state를 관리하고 업데이트.
하지만 react에서는 state는 컴포넌트 state에 속하며, setState()에 의해 업데이트 됨.
</p>

<p>
state를 "신뢰가능한 단일 출처"로 만들어 두 요소를 결합 가능.
<br>제어 컴포넌트를 이용해 react 컴포넌트로 폼에 발생하는 사용자 입력값을 제어.
<br>주로 value attribute를 단일 출처로 사용.
</p>

```{.js}
class NameForm extends React.Component {
  constructor(props) {
    super(props);
    this.state = {value: ''};

    this.handleChange = this.handleChange.bind(this);
    this.handleSubmit = this.handleSubmit.bind(this);
  }

  handleChange(event) {
    this.setState({value: event.target.value});
  }

  handleSubmit(event) {
    alert('A name was submitted: ' + this.state.value);
    event.preventDefault();
  }

  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <label>
          Name:
          <input type="text" value={this.state.value} onChange={this.handleChange} />
        </label>
        <input type="submit" value="Submit" />
      </form>
    );
  }
}
```

<p>
다중 입력도 제어 가능.
</p>

```{.js}
class Reservation extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      isGoing: true,
      numberOfGuests: 2
    };

    this.handleInputChange = this.handleInputChange.bind(this);
  }

  handleInputChange(event) {
    const target = event.target;
    const value = target.type === 'checkbox' ? target.checked : target.value;
    const name = target.name;

    this.setState({
      [name]: value
    });
  }

  render() {
    return (
      <form>
        <label>
          Is going:
          <input
            name="isGoing"
            type="checkbox"
            checked={this.state.isGoing}
            onChange={this.handleInputChange} />
        </label>
        <br />
        <label>
          Number of guests:
          <input
            name="numberOfGuests"
            type="number"
            value={this.state.numberOfGuests}
            onChange={this.handleInputChange} />
        </label>
      </form>
    );
  }
}
```


### 10. State 끌어올리기

<p>
동일한 데이터에 대한 변경사항을 여러 컴포넌트에 반영할 때,
가장 가까운 공통 조상으로 state를 끌어올림.
</p>

<p>
업데이트를 유도하는 메소드를 자식 컴포넌트의 props로 넣어주는 방식을 사용.
</p>

### 11. 합성과 상속

<p>
합성을 통해 코드를 재사용하는 것을 추천.
상속은 따로 쓰지 않음.
</p>

<p>
컴포넌트에 다른 컴포넌트를 담기.
<br>어떤 자식 엘리먼크가 들어올지 예상할 수 없으면, children props를 사용.
해당 태그 안의 엘리먼트를 의미.
</p>

### 12. React로 사고하기.

<p>
1. UI를 컴포넌트 계층 구조로 나누기
<br>2. React로 정적인 버전 만들기(props만을 이용)
<br>3. UI state에 대한 최소한의 표현 찾아내기
<br>&ensp;(부모로부터 전달되는가? 시간이 지나도 변하지 않은가? 다른 state나 props로 계산이 가능한가?,
state가 아님.)
<br>4. state가 어디 있어야 할지 찾기(단방향)
<br>5. 역방향 데이터 흐름 추가하기
</p>

<br>
<br>
