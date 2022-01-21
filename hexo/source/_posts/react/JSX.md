---
title: JSX
date: 2022-01-18 23:54:05
tags:
categories:
  - React
  - Document
toc: true
---

# 📌JSX

[Hello World - React](https://ko.reactjs.org/docs/hello-world.html)

- [📌JSX](#jsx)
  - [✅ JSX 소개](#-jsx-소개)
  - [✅ JSX에 표현식 포함하기](#-jsx에-표현식-포함하기)
  - [✅ JSX문법](#-jsx문법)
  - [✅ 기초 사용법](#-기초-사용법)
    - [🔸 If문 사용](#-if문-사용)
    - [🔸 AND &&](#-and-)
    - [🔸 OR ||](#-or-)
    - [🔸 인라인 스타일링](#-인라인-스타일링)

<br>

<!-- more -->

- src/APP.js 불러오기
- import로 불러오는 기능을 브라우저에서도 사용하기 위해 번들러를 사용
  - 번들 : 파일을 묶듯이 연결하는 것. 대표적인 것 → 웹팩, Parcel, browserify

```jsx
function App() {
  return (
			....
)}
```

- function 키워드를 사용하여 컴포넌트를 만들었다 → 함수 컴포넌트라고 부른다.

<br>

## ✅ JSX 소개

```jsx
const element = <h1>Hello, world!</h1>;
```

- JavaScript를 확장한 문법이다.
- React ‘엘리먼트’를 생성한다.

- JSX 장점
  - 보기 쉽고 익숙하다 → JS만 사용한 코드와 JSX 비교
  - 높은 활용도 → HTML 태그를 사용하고 컴포넌트도 JSX안에서 작성할 수 있다.

```markdown
# ReactDOM.render

- 컴포넌트를 페이지에 렌더링하는 역할
- react-dom 모듈을 불러와 사용

# 함수의 파라미터

ReactDOM.render(페이지에 렌더링할 내용 JSX형태, JSX를 렌더링할 document 내부 요소 설정)

# React.StrictMode

- 레거시 기능들을 사용하지 못하게 하는 기능
- 옛날 기능을 사용했을 때 경고를 출력
```

<br>

## ✅ JSX에 표현식 포함하기

```jsx
const name = "Josh Perez";
const element = <h1>Hello, {name}</h1>;

ReactDOM.render(element, document.getElementById("root"));
```

- JSX의 중괄호 안에는 유효한 모든 javaScript 표현식을 넣을 수 있다
- 컴파일이 끝나면, JSX 표현식이 정규 JavaScript 함수 호출이 되고 JavaScript 객체로 인식

<br>

## ✅ JSX문법

- 감싸인 요소
  - 리액트 컴포넌트에서 요소 여러 개를 왜 하나의 요소로 꼭 감싸야 하는가? <div>
  - Virtual DOM에서 컴포넌트 변화를 감지해 낼 때 효율적으로 비교할 수 있도록 컴포넌트 내부는 하나의 DOM 트리 구조로 이루어져야 한다는 규칙
  - 또는 리액트 v16 도입된 Fragment 기능 사용

<br>

## ✅ 기초 사용법

- src/index.js에서 직접 고쳐도 되지만 모듈을 분리해 실행만 하게
- src/App.js에서 수정해보자

```jsx
import "./App.css";

function App() {
  const name = "React";
  return (
    <div>
      <h1>{name} 안녕? </h1>
      <h2>React Document</h2>
    </div>
  );
}

export default App;
```

<br>

### 🔸 If문 사용

- **<div> if (어쩌구) {저쩌구} </div>** 이게 안된다는 소리
- JSX안에서 쓰는 삼항 연산자 → **조건문 ? 조건문 참일때 실행할 코드 : 거짓일 때 실행할 코드**

```jsx
function App() {
  const name = "React";
  return <div>{name === "React" ? <h1>check</h1> : null}</div>;
}
```

<br>

### 🔸 AND &&

- 조건이 맞으면 뜨고 안맞으면 안뜨게
- && 연산자로 조건부 렌더링 할 수 있는 이유 → 리액트에서 false를 렌더링할 때는 null과 마찬가지로 아무것도 나타나지 않기 때문

```jsx
function App() {
  const name = "React";
  return <div>{name === "React" && <h1>react</h1>}</div>;
}
```

<br>

### 🔸 OR ||

- undefined만 반환하여 렌더링하는 상황을 만들때

```jsx
function App() {
  const name = undefined;
  return <div>{name || <h1>react</h1>}</div>;
}
```

<br>

### 🔸 인라인 스타일링

- 리액트에서 DOM 요소에 스타일을 적용할 때는 문자열 형태로 넣는 것이 아니라 객체 형태로 넣어주어야 한다.
- 카멜 표기법 → background-color X → backgroundColor
- JSX에는 class가 아닌 className으로 설정해 주어야 한다. (APP.css에서 설정하고 )

```jsx
function App() {
  const name = "React";
  return (
    <div
      style={{
        backgroundColor: "black",
        color: "aqua",
        fontSize: "48px",
        fontWeight: "bold",
      }}
    >
      {name}
    </div>
  );
}
```

```jsx
function App() {
  const name = "React";
  const style = {
    backgroundColor: "black",
    color: "aqua",
    fontSize: "48px",
    fontWeight: "bold",
  };
  return <div style={style}>{name}</div>;
}
```

<br>

- 주석

```jsx
function App() {
  const name = "React";
  return (
    <div>
      {/* 이렇게  주석 */}
      <div
        className="react" // 이렇게 할수도 있넹
      >
        {name}
      </div>
    </div>
  );
}
```
