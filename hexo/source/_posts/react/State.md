---
title: State
date: 2022-01-23 23:27:44
tags:
toc: true
categories:
  - React
  - Document
---

# ๐ State

[State and Lifecycle - React](https://ko.reactjs.org/docs/state-and-lifecycle.html)

- props โ ์ปดํฌ๋ํธ๊ฐ ์ฌ์ฉ๋๋ ๊ณผ์ ์์ ๋ถ๋ชจ ์ปดํฌ๋ํธ๊ฐ ์ค์ ํ๋ ๊ฐ, props๋ฅผ ๋ฐ๊พธ๋ ค๋ฉด ๋ถ๋ชจ ์ปดํฌ๋ํธ์์ ๋ฐ๊พธ์ด ์ฃผ์ด์ผ ํ๋ค

- state โ ์ปดํฌ๋ํธ ๋ด๋ถ์์ ๋ฐ๋ ์ ์๋ ๊ฐ์ ์๋ฏธํ๋ค

```markdown
# state๋ ๋๊ฐ์ง ์ข๋ฅ

1. ํด๋์ค ์ปดํฌ๋ํธ -> state
2. ํจ์ ์ปดํฌ๋ํธ -> useState ํจ์๋ฅผ ํตํด ์ฌ์ฉํ๋ state
```

<br>

<!-- more -->

## โ ํด๋์คํ ์ปดํฌ๋ํธ์ state

```jsx
class Counter extends Component {
  constructor(props) {
    super(props);
    this.state = {
      number: 0,
    };
  }
```

- state๋ฅผ ์ค์ ํ  ๋ โ `constructor ๋ฉ์๋`๋ฅผ ์์ฑํ์ฌ ์ค์  โ ์ปดํฌ๋ํธ ์์ฑ์ ๋ฉ์๋

- ํด๋์คํ ์ปดํฌ๋ํธ โ constructor ์์ฑํ ๋ ๋ฐ๋์ โ `super(props)`๋ฅผ ํธ์ถ

- ์ด ํจ์๊ฐ ํธ์ถ๋๋ฉด โ ํ์ฌ ํด๋์ค ์ปดํฌ๋ํธ๊ฐ ์์๋ฐ๊ณ  ์๋ ๋ฆฌ์กํธ component ํด๋์ค๊ฐ ์ง๋ ์์ฑ์ ํจ์๋ฅผ ํธ์ถํด์ค๋ค

- `this.state` ๊ฐ์ ์ด๊น๊ฐ ์ค์  โ ์ปดํฌ๋ํธ์ state๋ ๊ฐ์ฒด ํ์

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

- render ํจ์ โ ํ์ฌ state๋ฅผ ์กฐํ โ this.state

- button ์์ onClick ๊ฐ props๋ก ๋ฃ์ด์ค โ ์ด๋ฒคํธ ์ค์  โ ํด๋ฆญ โ this.setState โ state ๊ฐ ๋ณ๊ฒฝ

<br>

### ๐ธ state ๊ฐ์ฒด ์์ ์ฌ๋ฌ ๊ฐ์ด ์์ ๋

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
        <h2>๋ฐ๋์ง ์๋ ๊ฐ: {fixedNumber}</h2>
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

### ๐ธ state๋ฅผ constructor์์ ๊บผ๋ด๊ธฐ

- state์ ์ด๊น๊ฐ ์ง์ ์ ์ํด constructor ๋ฉ์๋๋ฅผ ์ ์ธํ๋๋ฐ ๋ ๋ค๋ฅธ ๋ฐฉ์์ด ์๋ค.

```jsx
class Counter extends Component {
  state = {
    number: 0,
    fixedNumber: 0,
  };
  render() { ...} }
```

<br>

### ๐ธ this.setState์ ๊ฐ์ฒด ๋์  ํจ์ ์ธ์ ์ ๋ฌ

```jsx
onClick ={() => {
	this.setState({number: number + 1})
	this.setState({number: this.state.number + 1})
}
```

- this.setState๋ฅผ ๋ ๋ฒ ์ฌ์ฉํ์ฌ๋ ์ซ์๋ 1์ฉ ๋ํด์ง๋ค โ state ๊ฐ์ด ๋ฐ๋ก ๋ฐ๋์ง ์๊ธฐ ๋๋ฌธ

- ์ด์ ํด๊ฒฐ์ฑ โ this.setState์ ๊ฐ์ฒด ๋์ ์ ํจ์๋ฅผ ์ธ์๋ก ๋ฃ์ด์ค

```jsx
this.setState((prevState, props) => {
	return {
		// ์๋ฐ์ดํธ
}
```

- prevState โ ๊ธฐ์กด ์ํ, props โ ํ์ฌ ์ง๋๊ณ  ์๋ props ๊ฐ๋ฆฌํจ๋ค

```jsx
onClick={() => {
   this.setState((prevState) => ({
      number: prevState.number + 1,
}));
```

<br>

### ๐ธ this.setState ๋๋ ํ ํน์  ์์ ์คํ (์ฝ๋ฐฑ)

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
                console.log("setState ํธ์ถ");
                console.log(this.state);
              }
            );
          }}
        >
```

<br>

## โ ํจ์ ์ปดํฌ๋ํธ useState

- ํจ์ ์ปดํฌ๋ํธ๋ state ์ฌ์ฉ ํ  ์ ์์๋ค โ useState ํจ์๋ฅผ ์ฌ์ฉํด state ์ฌ์ฉ ๊ฐ๋ฅ

- Hooks๋ฅผ ์ฌ์ฉ

- Hooks ์ฌ์ฉ ์ ์ `๋ฐฐ์ด ๋น๊ตฌ์กฐํ ํ ๋น`

```jsx
const array = [1, 2];
const one = array[0];

// ๋ฐฐ์ด ๋น๊ตฌ์กฐํ ํ ๋น
const [one, two] = array;
```

<br>

### ๐ธ useState ์ฌ์ฉํ๊ธฐ

- useState ํจ์์ ์ธ์์๋ `์ํ์ ์ด๊น๊ฐ`์ ๋ฃ์ด์ค
- useState์์๋ ๊ผญ ๊ฐ์ฒด๊ฐ ์๋๋ผ ๊ฐ์ ํํ๋ ์์ ๋ค
- ํจ์๋ฅผ ํธ์ถํ๋ฉด ๋ฐฐ์ด์ด ๋ฐํ
  - ๋ฐฐ์ด ์ฒซ ๋ฒ์งธ ์์ : `ํ์ฌ์ํ`
  - ๋ฐฐ์ด ๋ ๋ฒ์งธ ์์ : ์ํ๋ฅผ ๋ฐ๊พธ์ด ์ฃผ๋ ํจ์ โ `Setter` ํจ์

```jsx
import { useState } from "react";

const Say = () => {
  const [message, setMessage] = useState("");
  const onClickEnter = () => setMessage("์๋ํํ์ธ์!");
  const onClickLeave = () => setMessage("์๋ํ ๊ฐ์ธ์~");

  return (
    <div>
      <button onClick={onClickEnter}>์์ฅ</button>
      <button onClick={onClickLeave}>ํด์ฅ</button>
      <h1>{message}</h1>
    </div>
  );
};

export default Say;
```

<br>

### ๐ธ ํ ์ปดํฌ๋ํธ์์ useState ์ฌ๋ฌ ๋ฒ ์ฌ์ฉ

```jsx
import { useState } from "react";

const Say = () => {
  const [message, setMessage] = useState("");
  const onClickEnter = () => setMessage("์๋ํํ์ธ์!");
  const onClickLeave = () => setMessage("์๋ํ ๊ฐ์ธ์~");

  const [color, setColor] = useState("black");

  return (
    <div>
      <button onClick={onClickEnter}>์์ฅ</button>
      <button onClick={onClickLeave}>ํด์ฅ</button>
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

## โ state๋ฅผ ์ฌ์ฉํ  ๋ ์ฃผ์์ฌํญ

- state ๊ฐ์ ๋ฐ๊ฟ ๋ โ setState ํน์ useState๋ฅผ ํตํด ์ ๋ฌ๋ฐ์ ์ธํฐ ํจ์๋ฅผ ์ฌ์ฉํด์ผ ํ๋ค
- ๋ฐฐ์ด์ด๋ ๊ฐ์ฒด๋ฅผ ์๋ฐ์ดํธํด์ผ ํ  ๋๋ ์ด๋ป๊ฒ ํด์ผ ํ ๊น?
  - ๋ฐฐ์ด์ด๋ ๊ฐ์ฒด ์ฌ๋ณธ์ ๋ง๋ค๊ณ  ๊ทธ ์ฌ๋ณธ์ ๊ฐ์ ์๋ฐ์ดํธํ ํ โ ์ฌ๋ณธ ์ํ๋ฅผ ์ธํฐํจ์๋ฅผ ํตํด ์๋ฐ์ดํธ
