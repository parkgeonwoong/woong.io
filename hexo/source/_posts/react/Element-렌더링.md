---
title: Element 렌더링
date: 2022-01-20 20:21:28
tags:
categories:
  - React
  - Document
---

# 📌 Element 렌더링

https://ko.reactjs.org/docs/rendering-elements.html

- 엘리먼트는 React 앱의 가장 작은 단위

- 브라우저 DOM 엘리먼트와 달리 React 엘리먼트는 일반 객체이며(plain object) 쉽게 생성할 수 있습니다. React DOM은 React 엘리먼트와 일치하도록 DOM을 업데이트한다

```jsx
<div id="root"></div>
```

<br>

- 이 안에 들어가는 모든 엘리먼트를 React DOM에서 관리하기 때문에 이것을 “루트(root)” DOM 노드라고 부른다

- React 엘리먼트를 루트 DOM 노드에 렌더링하려면  `[ReactDOM.render()](https://ko.reactjs.org/docs/react-dom.html#render)`로 전달

- UI를 업데이트하는 유일한 방법은 새로운 엘리먼트를 생성하고 이를 `ReactDOM.render()`로 전달

<br>

```jsx
function tick() {
  const element = (
    <div>
      <h1>Hello, world!</h1>
      <h2>It is {new Date().toLocaleTimeString()}.</h2>
    </div>
  );
  ReactDOM.render(element, document.getElementById("root"));
}

setInterval(tick, 1000);
```
