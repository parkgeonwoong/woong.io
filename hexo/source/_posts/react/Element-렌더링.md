---
title: Element ë ëë§
date: 2022-01-20 20:21:28
tags:
categories:
  - React
  - Document
---

# ð Element ë ëë§

https://ko.reactjs.org/docs/rendering-elements.html

- ìë¦¬ë¨¼í¸ë React ì±ì ê°ì¥ ìì ë¨ì

- ë¸ë¼ì°ì  DOM ìë¦¬ë¨¼í¸ì ë¬ë¦¬ React ìë¦¬ë¨¼í¸ë ì¼ë° ê°ì²´ì´ë©°(plain object) ì½ê² ìì±í  ì ììµëë¤. React DOMì React ìë¦¬ë¨¼í¸ì ì¼ì¹íëë¡ DOMì ìë°ì´í¸íë¤

```jsx
<div id="root"></div>
```

<br>

- ì´ ìì ë¤ì´ê°ë ëª¨ë  ìë¦¬ë¨¼í¸ë¥¼ React DOMìì ê´ë¦¬íê¸° ëë¬¸ì ì´ê²ì âë£¨í¸(root)â DOM ë¸ëë¼ê³  ë¶ë¥¸ë¤

- React ìë¦¬ë¨¼í¸ë¥¼ ë£¨í¸ DOM ë¸ëì ë ëë§íë ¤ë©´ Â `[ReactDOM.render()](https://ko.reactjs.org/docs/react-dom.html#render)`ë¡ ì ë¬

- UIë¥¼ ìë°ì´í¸íë ì ì¼í ë°©ë²ì ìë¡ì´ ìë¦¬ë¨¼í¸ë¥¼ ìì±íê³  ì´ë¥¼ `ReactDOM.render()`ë¡ ì ë¬

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
