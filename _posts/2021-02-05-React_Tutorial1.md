---
layout: post
title: "[REACT] React Tutorial"
date: 2021-02-05 00:00:00
categories: [STUDY]
tags: [REACT]
last_modified_at: 2021-02-05
---

From [https://ko.reactjs.org/](https://ko.reactjs.org/)

---

> React 사용자 인터페이스를 만들기 위한 JS 라이브러리

#### React

<p>
react는 UI를 만들기 위한 JS 라이브러리로, 상호작용이 많은 UI를 만들 때 유리.
</p>

<p>
react의 특징은 크게 3가지가 있다.
<br>JSX, Component, DOM
</p>

__JSX__
<p>
<br>react는 기본적으로 jsx(js + xml)을 사용.
<br>즉, js 안에서 html을 사용하는 방법.
<br>로직을 js로 작성하여 앱안에서 다양한 데이터를 다룰 수 있음.
</p>

__Component__

<p>
react는 컴포넌트 기반 라이브러리.
<br>하나의 html 파일이 아닌 여러개의 컴포넌트로 분할된 html을 추가하고
<br>제거하는 방식으로 view를 만들어 재사용성과 유지보수성이 좋다.
<br>(해당 부분의 파일만 수정하면 되니까, 다른 부분을 건드려 오류가 발생할 확률이 적다)
</p>

__Virtual DOM__

<p>
Virtual Document Object Model
<br>state와 props가 변화하면 render가 호출,
<br>가상 돔은 이 변화를 감지해서 업데이트를 시킴.
<br>그리고 나중에 실제 돔에 업데이트하며 한번에 변화들을 렌더링함.
<br>즉, 실제 돔에서 발생할 불필요한 연산들을 줄임.
</p>

#### Component

__간단한 컴포넌트__

<p>
react 컴포넌트는 render 메소드를 구현.
<br>이를 통해 데이터를 입력받아 화면에 내용을 반환.
<br>컴포넌트로 전달된 데이터는 render 안에서 this.props를 통해 접근 가능.
</p>

__상태를 가지는 컴포넌트__

<p>
props는 외부적인 입력 데이터를 다루지만, state로 내부적인 데이터에 접근 가능.
<br>컴포넌트의 this.state가 바뀌면 render가 다시 호출되어 마크업 갱신.
</p>

__외부 플러그인을 사용하는 컴포넌트__

<p>
props와 state를 사용하여, 어플리케이션 제작
<br>react는 유연, 따라서 다른 프레임워크나 라이브러리를 함께 사용 가능.
</p>

<br>
<br>



