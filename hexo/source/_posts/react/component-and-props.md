---
title: component와 props를 알아가보자
date: 2022-01-21 17:06:59
tags:
toc: true
categories:
  - React
  - Document
---

# 📌 Component와 Props

[Components와 Props - React](https://ko.reactjs.org/docs/components-and-props.html)

- 컴포넌트를 통해 UI를 재사용 가능한 개별적인 여러 조각으로 나누고, 각 조각을 개별적으로 살펴볼 수 있다.
- 개념적으로 컴포넌트는 JavaScript 함수와 유사.
- “props”라고 하는 임의의 입력을 받은 후, 화면에 어떻게 표시되는지를 기술하는 React 엘리먼트를 반환합니다.

<!-- more -->

<br>

## ✅함수 컴포넌트와 클래스 컴포넌트

```markdown
# 컴포넌트를 선언하는 방식 두가지

1. 함수 컴포넌트
2. 클래스형 컴포넌트

# 차이점

- 클래스형 컴포넌트 -> state 기능 및 라이프 사이클 기능을 사용가능
- 임의 메서드를 정의할 수 있다.
```

<br>

### 🔸 함수형 컴포넌트

- 컴포넌트를 정의하는 가장 간단한 방법 → JavaScript 함수를 작성

```jsx
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}
```

- 단점 → state와 라이프사이클 API의 사용 불가 → 해결점 → Hooks 기능 도입

<br>

### 🔸 클래스형 컴포넌트

- App.js

```jsx
import { Component } from "react";

class App extends Component {
  render() {
    const name = "React";
    return <div className="react">{name}</div>;
  }
}
```

- render 함수가 꼭 있어야 함
- 그 안에서 보여 주어야 할 JSX를 반환해야 한다

<br>

## ✅컴포넌트 렌더링

- React 엘리먼트는 사용자 정의 컴포넌트로도 나타낼수 있다.

```jsx
const element = <Welcome name="Sara" />;
```

<br>

- Props : React가 사용자 정의 컴포넌트로 작성한 엘리먼트를 발견하면 → JSX 어트리뷰트와 자식을 해당 컴포넌트에 단일 객체로 전달합니다. 이 객체를 props

```jsx
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}

const element = <Welcome name="Sara" />;
ReactDOM.render(
  element,
  document.getElementById('root')
);

1. <Welcome name="Sara" /> 엘리먼트로 ReactDOM.render()를 호출합니다.
2. React는 {name: 'Sara'}를 props로 하여 Welcome 컴포넌트를 호출합니다.
3. Welcome 컴포넌트는 결과적으로 <h1>Hello, Sara</h1> 엘리먼트를 반환합니다.
4. React DOM은 <h1>Hello, Sara</h1> 엘리먼트와 일치하도록 DOM을 효율적으로 업데이트합니다.
```

<br>

## ✅ 컴포넌트 합성

- 컴포넌트는 자신의 출력에 다른 컴포넌트를 참조할 수 있습니다.

```jsx
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}

function App() {
  return (
    <div>
      <Welcome name="Sara" />
      <Welcome name="Cahal" />
      <Welcome name="Edite" />
    </div>
  );
}

ReactDOM.render(<App />, document.getElementById("root"));
```

<br>

## ✅첫 컴포넌트 생성

- src/[new file].js

```jsx
const MyComponent = () => {
  return <div>First new Component</div>;
};

export default MyComponent;
```

- 일반 함수 vs 화살표 함수 차이 == this 값이 다르다
  - 일반 함수 → 자신이 종속된 객체를 this로 가리킨다
  - 화살표 함수 → 자신이 종속된 인스턴스(new)를 가리킨다

```jsx
const App = () => {
  return <MyComponent />;
};
```

<br>

## ✅Props

- properties 줄인 표현, 컴포넌트 속성을 설정할 때 사용하는 요소
- props 값은 해당 컴포넌트를 불러와 사용하는 부모 컴포넌트(App.js)에서 설정할 수 있다

```jsx
// MyComponent.js
const MyComponent = (props) => {
  return <div>My name {props.name}</div>;
};

export default MyComponent;
```

```jsx
// App.js
import MyComponent from "./MyComponent";

const App = () => {
  return <MyComponent name="⚛️React" />;
};

export default App;
```

<br>

### 🔸Props 기본값 설정 : defaultProps

```jsx
const MyComponent = (props) => {
  return <div>My name {props.name} 입니다</div>;
};

MyComponent.defaultProps = {
  name: "기본이름",
};

// App.js
const App = () => {
  return <MyComponent />;
};
```

<br>

### 🔸태그 사이의 내용을 보여주는 Children

- 컴포넌트 태그 사이의 내용을 보여주는 props children

```jsx
const App = () => {
  return <MyComponent>react</MyComponent>;
};
```

```jsx
const MyComponent = (props) => {
  return (
    <div>
      My name {props.name} 입니다 Children value {props.children}
    </div>
  );
};

MyComponent.defaultProps = {
  name: "기본이름",
};
```

<br>

### 🔸 비구조화 할당 문법

- props 키워드를 앞에다 붙이는데 이를 편하기 위해 → `비구조화 할당 문법` 사용

```jsx
const MyComponent = (props) => {
  const { name, children } = props;
  return (
    <div>
      My name {name} 입니다 <br />
      Children value {children}
    </div>
  );
};
```

- 비구조화 할당 문법 = 구조 분해 문법
- 함수의 파라미터 부분에도 사용 가능

```jsx
const MyComponent = ({ name, children }) => {
  return ( ... )
```

<br>

### 🔸 클래스형 컴포넌트 Props

- props 사용 시 → render 함수에서 this.props

```jsx
class MyComponent extends Component {
  static defaultProps = {
    name: "기본 이름",
  };
  static propTypes = {
    name: PropTypes.string,
    favoriteNumber: PropTypes.number.isRequired,
  };
  render() {
    const { name, favoriteNumber, children } = this.props;
    return (
      <div>
        My name {name} 입니다 <br />
        Children value {children}
        <br />
        좋아하는 숫자 {favoriteNumber}
      </div>
    );
  }
}
```
