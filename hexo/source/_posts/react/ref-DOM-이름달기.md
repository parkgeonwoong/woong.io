---
title: ref-DOM ์ด๋ฆ๋ฌ๊ธฐ
date: 2022-02-19 16:27:46
tags:
toc: true
categories:
  - React
  - Document
---

# ๐ ref: DOM ์ด๋ฆ ๋ฌ๊ธฐ

[Forwarding Refs - React](https://ko.reactjs.org/docs/forwarding-refs.html)

> HTML์์ id๋ฅผ ์ฌ์ฉ โ DOM์ ์ด๋ฆ์ ๋ค๋ ๊ฒ ์ฒ๋ผ โ ๋ฆฌ์กํธ ํ๋ก์ ํธ ๋ด๋ถ์์ DOM์ ์ด๋ฆ์ ๋ค๋ ๋ฐฉ๋ฒ = ref ๊ฐ๋

<br>

- [๐ ref: DOM ์ด๋ฆ ๋ฌ๊ธฐ](#-ref-dom-์ด๋ฆ-๋ฌ๊ธฐ)
- [โ ref๋ ์ด๋ค ์ํฉ์์ ์ฌ์ฉํด์ผ ํ ๊น](#-ref๋-์ด๋ค-์ํฉ์์-์ฌ์ฉํด์ผ-ํ ๊น)
  - [๐น ํด๋์ค ์ปดํฌ๋ํธ ์์ ](#-ํด๋์ค-์ปดํฌ๋ํธ-์์ )
    - [๐ธ DOM์ ๊ผญ ์ฌ์ฉํด์ผ ํ๋ ์ํฉ](#-dom์-๊ผญ-์ฌ์ฉํด์ผ-ํ๋-์ํฉ)
- [โ ref ์ฌ์ฉ](#-ref-์ฌ์ฉ)
    - [๐ธ 1. ์ฝ๋ฐฑ ํจ์๋ฅผ ํตํ ref ์ค์ ](#-1-์ฝ๋ฐฑ-ํจ์๋ฅผ-ํตํ-ref-์ค์ )
    - [๐ธ 2. createRef๋ฅผ ํตํ ref ์ค์ ](#-2-createref๋ฅผ-ํตํ-ref-์ค์ )
- [โ ์ปดํฌ๋ํธ์ ref ๋ฌ๊ธฐ](#-์ปดํฌ๋ํธ์-ref-๋ฌ๊ธฐ)
    - [๐ธ ์ฃผ์](#-์ฃผ์)

<!-- more -->

<br>

# โ ref๋ ์ด๋ค ์ํฉ์์ ์ฌ์ฉํด์ผ ํ ๊น

- DOM์ ๊ผญ ์ง์ ์ ์ผ๋ก ๊ฑด๋๋ ค์ผ ํ  ๋

1. ์ปดํฌ๋ํธ ๋ง๋ค๊ธฐ
2. input์ ref ๋ฌ๊ธฐ
3. ๋ฒํผ์ ๋๋ฅผ ๋๋ง๋ค input์ ํฌ์ปค์ค ์ถ๊ฐ

## ๐น ํด๋์ค ์ปดํฌ๋ํธ ์์ 

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
        <button onClick={this.handleClick}>๊ฒ์ฆ</button>
      </div>
    );
  }
}

export default ValidationSample;
```

- input์ className ๊ฐ์ ๋ฒํผ์ ๋๋ฅด๊ธฐ ์ ์๋ ๋น์ด ์๋ ๋ฌธ์์ด์ ์ ๋ฌ โ ๋ฒํผ ๋๋ฅธ ํ์๋ ๊ฒ์ฆ ๊ฒฐ๊ณผ์ ๋ฐ๋ผ โ success / failure ๊ฐ์ ์ค์ 

- App ํจ์ ์ปดํฌ๋ํธ โ ํด๋์คํ ์ปดํฌ๋ํธ ์ ํ
- ์? โ ref๋ฅผ ์ฌ์ฉํ  ๊ฒ์ด๊ธฐ์ ๋ฐ๊ฟ์ค

```jsx
class App extends Component {
  render() {
    return <ValidationSample />;
  }
}
```

### ๐ธ DOM์ ๊ผญ ์ฌ์ฉํด์ผ ํ๋ ์ํฉ

- `state๋ง`์ผ๋ก ํด๊ฒฐํ  ์ ์๋ ๊ธฐ๋ฅ์ด ์๋ค
  - ํน์  input์ ํฌ์ปค์ค ์ฃผ๊ธฐ
  - ์คํฌ๋กค ๋ฐ์ค ์กฐ์ํ๊ธฐ
  - Canvas ์์์ ๊ทธ๋ฆผ ๊ทธ๋ฆฌ๊ธฐ ๋ฑ

<br>

# โ ref ์ฌ์ฉ

- ref ์ฌ์ฉํ๋ ๋ฐฉ๋ฒ 2๊ฐ์ง

### ๐ธ 1. ์ฝ๋ฐฑ ํจ์๋ฅผ ํตํ ref ์ค์ 

- ref๋ฅผ ๋ฌ๊ณ ์ ํ๋ ์์์ ref๋ผ๋ ์ฝ๋ฐฑ ํจ์๋ฅผ props๋ก ์ ๋ฌ
- ์ด ์ฝ๋ฐฑ ํจ์๋ ref ๊ฐ์ ํ๋ผ๋ฏธํฐ๋ก ์ ๋ฌ๋ฐ๋๋ค
- ํจ์ ๋ด๋ถ์์ ํ๋ผ๋ฏธํฐ๋ก ๋ฐ์ ref๋ฅผ ์ปดํฌ๋ํธ์ ๋ฉค๋ฒ ๋ณ์๋ก ์ค์ 

```jsx
<input
  ref={(ref) => {
    this.input = ref;
  }}
/>
```

- `this.input`์ input ์์์ DOM์ ๊ฐ๋ฆฌํจ๋ค. ref์ ์ด๋ฆ์ ์ํ๋ ๊ฒ์ผ๋ก ์์ ๋กญ๊ฒ ์ง์ 

### ๐ธ 2. createRef๋ฅผ ํตํ ref ์ค์ 

- ๋ฆฌ์กํธ์ ๋ด์ฅ๋ createRef ํจ์ ์ฌ์ฉ
- createRef ์ค์ ํ ๋ค ๋์ค์ ref๋ฅผ ์ค์ ํด ์ค DOM์ ์ ๊ทผํ๋ ค๋ฉด โ `this.input.current` ๋ฅผ ์กฐํ

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
    // ์ฝ๋ฐฑ this.input.focus();
  };

  handleFocus = () => {
    this.input.current.focus();
  };

  render() {
    return (
      <div>
        <input
          ref={this.input}
          // ์ฝ๋ฐฑ  ref={(ref) => (this.input = ref)}
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
        <button onClick={this.handleClick}>๊ฒ์ฆ</button>
      </div>
    );
  }
}
```

<br>

# โ ์ปดํฌ๋ํธ์ ref ๋ฌ๊ธฐ

- ์ปดํฌ๋ํธ ๋ด๋ถ์ ์๋ DOM์ ์ปดํฌ๋ํธ ์ธ๋ถ์์ ์ฌ์ฉํ  ๋ ์ด๋ค

```jsx
<MyComponent ref={(ref) => {this.myComponent=ref}}
```

- ์ด๋ ๊ฒ ํ๋ฉด MyComponent ๋ด๋ถ์ ๋ฉ์๋ ๋ฐ ๋ฉค๋ฒ ๋ณ์์๋ ์ ๊ทผ ๊ฐ๋ฅ
- ์ฆ ๋ด๋ถ์ ref์๋ ์ ๊ทผ ๊ฐ๋ฅ

1. ์คํฌ๋กค ๋ฐ์ค ์ปดํฌ๋ํธ ๋ง๋ค๊ณ 
2. ์คํฌ๋กค๋ฐ๋ฅผ ์๋๋ก ๋ด๋ฆฌ๋ ์์์ ๋ถ๋ชจ ์ปดํฌ๋ํธ์์ ์คํ

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

- ์ฌ๊ธฐ์ ์ปดํฌ๋ํธ ๋ฉ์๋ ์์ฑ ํ โ ์ปดํฌ๋ํธ์ ref ๋ฌ๊ณ  ๋ด๋ถ ๋ฉ์๋ ์ฌ์ฉ

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
          ๋งจ ๋ค์
        </button>
      </div>
    );
  }
}
```

### ๐ธ ์ฃผ์

- ์๋ก ๋ค๋ฅธ ์ปดํฌ๋ํธ๋ผ๋ฆฌ ๋ฐ์ดํฐ๋ฅผ ๊ต๋ฅํ  ๋ ref ๋ฅผ ์ฌ์ฉํ๋ค๋ฉด ์ด๋ ์๋ชป ์ฌ์ฉ!!
- ์ ์ง๋ณด์๊ฐ ๋ถ๊ฐ๋ฅ์ ๊ฐ๊น๊ฒ ๊ตฌ์กฐ๊ฐ ๊ผฌ์ฌ ๋ฒ๋ฆฐ๋ค
- ์ปดํฌ๋ํธ๋ผ๋ฆฌ ๋ฐ์ดํฐ๋ฅผ ๊ต๋ฅํ  ๋๋ ์ธ์ ๋ ๋ฐ์ดํฐ๋ฅผ ๋ถ๋ชจ โ ์์ ํ๋ฆ์ผ๋ก ๊ต๋ฅํด์ผ ํ๋ค
