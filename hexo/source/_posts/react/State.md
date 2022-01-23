---
title: State
date: 2022-01-23 23:27:44
tags:
toc: true
categories:
  - React
  - Document
---

# 📌 State

[State and Lifecycle - React](https://ko.reactjs.org/docs/state-and-lifecycle.html)

- props → 컴포넌트가 사용되는 과정에서 부모 컴포넌트가 설정하는 값, props를 바꾸려면 부모 컴포넌트에서 바꾸어 주어야 한다

- state → 컴포넌트 내부에서 바뀔 수 있는 값을 의미한다

```markdown
# state는 두가지 종류

1. 클래스 컴포넌트 -> state
2. 함수 컴포넌트 -> useState 함수를 통해 사용하는 state
```

<br>

<!-- more -->

## ✅ 클래스형 컴포넌트의 state

```jsx
class Counter extends Component {
  constructor(props) {
    super(props);
    this.state = {
      number: 0,
    };
  }
```

- state를 설정할 때 → `constructor 메서드`를 작성하여 설정 → 컴포넌트 생성자 메서드

- 클래스형 컴포넌트 → constructor 작성할때 반드시 → `super(props)`를 호출

- 이 함수가 호출되면 → 현재 클래스 컴포넌트가 상속받고 있는 리액트 component 클래스가 지닌 생성자 함수를 호출해준다

- `this.state` 값에 초깃값 설정 → 컴포넌트의 state는 객체 형식

```jsx
render() {
    const { number } = this.state;
    return (
      <div>
        <h1>{number}</h1>
        <button
          onClick={() => {
            this.setState({ number: number + 1 });
          }}
        >
          +1
        </button>
      </div>
    );
  }
```

- render 함수 → 현재 state를 조회 → this.state

- button 안에 onClick 값 props로 넣어줌 → 이벤트 설정 → 클릭 → this.setState → state 값 변경

<br>

### 🔸 state 객체 안에 여러 값이 있을 때

```jsx
class Counter extends Component {
  constructor(props) {
    super(props);
    this.state = {
      number: 0,
      fixedNumber: 0,
    };
  }
  render() {
    const { number, fixedNumber } = this.state;
    return (
      <div>
        <h1>{number}</h1>
        <h2>바뀌지 않는 값: {fixedNumber}</h2>
        <button
          onClick={() => {
            this.setState({ number: number + 1 });
          }}
        >
          +1
        </button>
      </div>
    );
  }
}
```

<br>

### 🔸 state를 constructor에서 꺼내기

- state의 초깃값 지정을 위해 constructor 메서드를 선언했는데 또 다른 방식이 있다.

```jsx
class Counter extends Component {
  state = {
    number: 0,
    fixedNumber: 0,
  };
  render() { ...} }
```

<br>

### 🔸 this.setState에 객체 대신 함수 인자 전달

```jsx
onClick ={() => {
	this.setState({number: number + 1})
	this.setState({number: this.state.number + 1})
}
```

- this.setState를 두 번 사용하여도 숫자는 1씩 더해진다 → state 값이 바로 바뀌지 않기 때문

- 이에 해결책 → this.setState에 객체 대신에 함수를 인자로 넣어줌

```jsx
this.setState((prevState, props) => {
	return {
		// 업데이트
}
```

- prevState → 기존 상태, props → 현재 지니고 있는 props 가리킨다

```jsx
onClick={() => {
   this.setState((prevState) => ({
      number: prevState.number + 1,
}));
```

<br>

### 🔸 this.setState 끝난 후 특정 작업 실행 (콜백)

```jsx
<button
          onClick={() => {
            this.setState((prevState) => ({
              number: prevState.number + 1,
            }));
            this.setState(
              {
                number: number + 1,
              },
              () => {
                console.log("setState 호출");
                console.log(this.state);
              }
            );
          }}
        >
```

<br>

## ✅ 함수 컴포넌트 useState

- 함수 컴포넌트는 state 사용 할 수 없었다 → useState 함수를 사용해 state 사용 가능

- Hooks를 사용

- Hooks 사용 전에 `배열 비구조화 할당`

```jsx
const array = [1, 2];
const one = array[0];

// 배열 비구조화 할당
const [one, two] = array;
```

<br>

### 🔸 useState 사용하기

- useState 함수의 인자에는 `상태의 초깃값`을 넣어줌
- useState에서는 꼭 객체가 아니라 값의 형태는 자유다
- 함수를 호출하면 배열이 반환
  - 배열 첫 번째 원소 : `현재상태`
  - 배열 두 번째 원소 : 상태를 바꾸어 주는 함수 → `Setter` 함수

```jsx
import { useState } from "react";

const Say = () => {
  const [message, setMessage] = useState("");
  const onClickEnter = () => setMessage("안녕히하세요!");
  const onClickLeave = () => setMessage("안녕히 가세요~");

  return (
    <div>
      <button onClick={onClickEnter}>입장</button>
      <button onClick={onClickLeave}>퇴장</button>
      <h1>{message}</h1>
    </div>
  );
};

export default Say;
```

<br>

### 🔸 한 컴포넌트에서 useState 여러 번 사용

```jsx
import { useState } from "react";

const Say = () => {
  const [message, setMessage] = useState("");
  const onClickEnter = () => setMessage("안녕히하세요!");
  const onClickLeave = () => setMessage("안녕히 가세요~");

  const [color, setColor] = useState("black");

  return (
    <div>
      <button onClick={onClickEnter}>입장</button>
      <button onClick={onClickLeave}>퇴장</button>
      <h1 style={{ color }}>{message}</h1>
      <button style={{ color: "red" }} onClick={() => setColor("red")}>
        Red
      </button>
      <button style={{ color: "green" }} onClick={() => setColor("green")}>
        Green
      </button>
      <button style={{ color: "blue" }} onClick={() => setColor("blue")}>
        Blue
      </button>
    </div>
  );
};

export default Say;
```

<br>

## ✅ state를 사용할 때 주의사항

- state 값을 바꿀 때 → setState 혹은 useState를 통해 전달받은 세터 함수를 사용해야 한다
- 배열이나 객체를 업데이트해야 할 때는 어떻게 해야 할까?
  - 배열이나 객체 사본을 만들고 그 사본에 값을 업데이트한 후 → 사본 상태를 세터함수를 통해 업데이트
