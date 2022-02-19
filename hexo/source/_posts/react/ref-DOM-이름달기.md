---
title: ref-DOM 이름달기
date: 2022-02-19 16:27:46
tags:
toc: true
categories:
  - React
  - Document
---

# 📌 ref: DOM 이름 달기

[Forwarding Refs - React](https://ko.reactjs.org/docs/forwarding-refs.html)

> HTML에서 id를 사용 → DOM에 이름을 다는 것 처럼 → 리액트 프로젝트 내부에서 DOM에 이름을 다는 방법 = ref 개념

<br>

<!-- more -->

<br>

# ✅ ref는 어떤 상황에서 사용해야 할까

- DOM을 꼭 직접적으로 건드려야 할 때

1. 컴포넌트 만들기
2. input에 ref 달기
3. 버튼을 누를 때마다 input에 포커스 추가

## 🔹 클래스 컴포넌트 예제

```jsx
import React, { Component } from "react";
import "./ValidationSample.css";

class ValidationSample extends Component {
  state = {
    password: "",
    clicked: false,
    validated: false,
  };

  handleChange = (e) => {
    this.setState({
      password: e.target.value,
    });
  };

  handleClick = () => {
    this.setState({
      clicked: true,
      validated: this.state.password === "0000",
    });
  };

  render() {
    return (
      <div>
        <input
          type="password"
          value={this.state.password}
          onChange={this.handleChange}
          className={
            this.state.clicked
              ? this.state.validated
                ? "success"
                : "failure"
              : ""
          }
        ></input>
        <button onClick={this.handleClick}>검증</button>
      </div>
    );
  }
}

export default ValidationSample;
```

- input의 className 값은 버튼을 누르기 전에는 비어 있는 문자열을 전달 → 버튼 누른 후에는 검증 결과에 따라 → success / failure 값을 설정

- App 함수 컴포넌트 → 클래스형 컴포넌트 전환
- 왜? → ref를 사용할 것이기에 바꿔줌

```jsx
class App extends Component {
  render() {
    return <ValidationSample />;
  }
}
```

### 🔸 DOM을 꼭 사용해야 하는 상황

- `state만`으로 해결할 수 없는 기능이 있다
  - 특정 input에 포커스 주기
  - 스크롤 박스 조작하기
  - Canvas 요소에 그림 그리기 등

<br>

# ✅ ref 사용

- ref 사용하는 방법 2가지

### 🔸 1. 콜백 함수를 통한 ref 설정

- ref를 달고자 하는 요소에 ref라는 콜백 함수를 props로 전달
- 이 콜백 함수는 ref 값을 파라미터로 전달받는다
- 함수 내부에서 파라미터로 받은 ref를 컴포넌트의 멤버 변수로 설정

```jsx
<input
  ref={(ref) => {
    this.input = ref;
  }}
/>
```

- `this.input`은 input 요소의 DOM을 가리킨다. ref의 이름은 원하는 것으로 자유롭게 지정

### 🔸 2. createRef를 통한 ref 설정

- 리액트에 내장된 createRef 함수 사용
- createRef 설정한 뒤 나중에 ref를 설정해 준 DOM에 접근하려면 → `this.input.current` 를 조회

```jsx
class ValidationSample extends Component {
  input = React.createRef();

  state = {
    password: "",
    clicked: false,
    validated: false,
  };

  handleChange = (e) => {
    this.setState({
      password: e.target.value,
    });
  };

  handleClick = () => {
    this.setState({
      clicked: true,
      validated: this.state.password === "0000",
    });
    this.handleFocus();
    // 콜백 this.input.focus();
  };

  handleFocus = () => {
    this.input.current.focus();
  };

  render() {
    return (
      <div>
        <input
          ref={this.input}
          // 콜백  ref={(ref) => (this.input = ref)}
          type="password"
          value={this.state.password}
          onChange={this.handleChange}
          className={
            this.state.clicked
              ? this.state.validated
                ? "success"
                : "failure"
              : ""
          }
        ></input>
        <button onClick={this.handleClick}>검증</button>
      </div>
    );
  }
}
```

<br>

# ✅ 컴포넌트에 ref 달기

- 컴포넌트 내부에 있는 DOM을 컴포넌트 외부에서 사용할 때 쓴다

```jsx
<MyComponent ref={(ref) => {this.myComponent=ref}}
```

- 이렇게 하면 MyComponent 내부의 메서드 및 멤버 변수에도 접근 가능
- 즉 내부의 ref에도 접근 가능

1. 스크롤 박스 컴포넌트 만들고
2. 스크롤바를 아래로 내리는 작업을 부모 컴포넌트에서 실행

```jsx
class ScrollBox extends Component {
  render() {
    const style = {
      border: "1px solid black",
      height: "300px",
      weight: "300px",
      overflow: "auto",
      position: "relative",
    };

    const innerStyle = {
      width: "100%",
      height: "650px",
      background: "linear-gradient(white, black)",
    };
    return (
      <div
        style={style}
        ref={(ref) => {
          this.box = ref;
        }}
      >
        <div style={innerStyle}></div>
      </div>
    );
  }
}
```

```jsx
class App extends Component {
  render() {
    return (
      <div>
        <ScrollBox />
      </div>
    );
  }
}
```

- 여기서 컴포넌트 메서드 생성 후 → 컴포넌트에 ref 달고 내부 메서드 사용

```jsx
class ScrollBox extends Component {
  scrollToBottom = () => {
    const { scrollHeight, clientHeight } = this.box;
    this.box.scrollTop = scrollHeight - clientHeight;
  };

  render() {
		... }
```

```jsx
class App extends Component {
  render() {
    return (
      <div>
        <ScrollBox
          ref={(ref) => {
            this.scrollBox = ref;
          }}
        />
        <button
          onClick={() => {
            this.scrollBox.scrollToBottom();
          }}
        >
          맨 뒤에
        </button>
      </div>
    );
  }
}
```

### 🔸 주의

- 서로 다른 컴포넌트끼리 데이터를 교류할 때 ref 를 사용한다면 이는 잘못 사용!!
- 유지보수가 불가능에 가깝게 구조가 꼬여 버린다
- 컴포넌트끼리 데이터를 교류할 때는 언제나 데이터를 부모 ↔ 자식 흐름으로 교류해야 한다
