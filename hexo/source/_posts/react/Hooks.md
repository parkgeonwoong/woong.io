---
title: Hooks
date: 2022-02-23 14:57:49
tags:
toc: true
categories:
  - React
  - Document
---

# 📌Hooks

[Hook의 개요 - React](https://ko.reactjs.org/docs/hooks-intro.html)

- [📌Hooks](#hooks)
- [✅ useState](#-usestate)
  - [🔹 useState 여러 번 사용하기](#-usestate-여러-번-사용하기)
- [✅ useEffect](#-useeffect)
  - [🔹 마운트될 때만 실행하고 싶을 때](#-마운트될-때만-실행하고-싶을-때)
  - [🔹 특정 값이 업데이트될 때만 실행하고 싶을 때](#-특정-값이-업데이트될-때만-실행하고-싶을-때)
  - [🔹 뒷정리하기](#-뒷정리하기)
- [✅ useReducer](#-usereducer)
  - [🔹 인풋 상태 관리하기](#-인풋-상태-관리하기)
- [✅ useMemo](#-usememo)
- [✅ useCallback](#-usecallback)
- [✅ useRef](#-useref)
    - [🔸 로컬 변수 사용하기](#-로컬-변수-사용하기)
- [✅ 커스텀 Hooks 만들기](#-커스텀-hooks-만들기)

<br>

<!-- more -->

```markdown
# 정리

1. Hooks은 react 모듈에서 불러온다

2. **useState** = 상태관리

3. **useEffect** = 렌더링될 때마다 특정 작업 수행 설정

- callback 호출로 나타낸다
- 업데이트는 보여주고 싶지 않을 때 -> 두번째 파라미터 [ ]
- 특정 값만 보여주고 싶을 때 -> [검사하고 싶은 값 ]

4. **useReducer** = 다양한 상태 업데이트

- 리듀서 함수 만들기 (state, action= type 스위치, return)
- 상태, dispatch(리듀서 함수 호출)

5. **useCallback** = 만들어놨던 함수를 재사용

- [] -> 처음 렌더링될때 만 생성
- [ 바뀌는 값 ]

6. **useRef** = ref를 쉽게 사용

- current

7. **custom Hook** = 여러 컴포넌트에서 비슷한 기능 공유
```

<br>

# ✅ useState

- useState 함수의 파라미터에는 = `상태의 기본값`
- 이 함수가 호출되면 배열을 반환 → (`상태 값` , `상태를 설정하는 함수`)

```jsx
import { useState } from "react";

const Counter = () => {
  const [value, setValue] = useState(0);

  return (
    <div>
      <p>
        현재 카운터 값 <b>{value}</b>
      </p>
      <button onClick={() => setValue(value + 1)}>+1</button>
      <button onClick={() => setValue(value - 1)}>-1</button>
    </div>
  );
};

export default Counter;
```

## 🔹 useState 여러 번 사용하기

```jsx
import { useState } from "react";

const Info = () => {
  const [name, setName] = useState("");
  const [nickname, setNickname] = useState("");

  const OnChangeName = (e) => {
    setName(e.target.value);
  };

  const OnChnageNickname = (e) => {
    setNickname(e.target.value);
  };

  return (
    <div>
      <div>
        <input value={name} onChange={OnChangeName}></input>
        <input value={nickname} onChange={OnChnageNickname}></input>
      </div>
      <div>
        <div>
          <b>이름:</b> {name}
        </div>
        <div>
          <b>닉네임:</b> {nickname}
        </div>
      </div>
    </div>
  );
};

export default Info;
```

<br>

# ✅ useEffect

- 리액트 컴포넌트가 **렌더링될 때마다 특정 작업을 수행하도록 설정**할 수 있는 Hook

```jsx
import { useState, useEffect } from "react";

const Info = () => {
  const [name, setName] = useState("");
  const [nickname, setNickname] = useState("");

  useEffect(() => {
    console.log("렌더링이 완료");
    console.log({
      name,
      nickname,
    });
  });

...
```

## 🔹 마운트될 때만 실행하고 싶을 때

- useEffect에서 설정한 함수를 컴포넌트가 화면에 **맨 처음 렌더링될 때만 실행**하고, 업데이트될 때는 실행하지 않으려면 → 함수의 두번째 파라미터로 `비어 있는 배열`을 넣어주면 된다

```jsx
useEffect(() => {
  console.log("렌더링이 완료");
  console.log({
    name,
    nickname,
  });
}, []);
```

## 🔹 특정 값이 업데이트될 때만 실행하고 싶을 때

- value값이 바뀔 때만 특정 작업 수행 → 두번째 파라미터로 전달되는 배열 안에 검사하고 싶은 값

```jsx
useEffect(() => {
  console.log("렌더링이 완료");
  console.log({
    name,
    nickname,
  });
}, [name]);
```

## 🔹 뒷정리하기

- useEffect는 기본적으로 렌더링되고 난 직후마다 실행되며, 두 번째 파라미터 배열에 무엇을 넣는지에 따라 실행되는 조건이 달라진다
- 뒷정리 함수 → 컴포넌트가 언마운트되기 전이나 업데이트 직전에 어떠한 작업을 수행하고 싶을 때

```jsx
useEffect(() => {
  console.log("effect");
  console.log(name);
  return () => {
    console.log("cleanUp");
    console.log(name);
  };
}, [name]);
```

```jsx
const App = () => {
  const [visible, setVisible] = useState(false);

  return (
    <div>
      <button
        onClick={() => {
          setVisible(!visible);
        }}
      >
        {" "}
        {visible ? "숨기기" : "보이기"}{" "}
      </button>
      <hr />
      {visible && <Info />}
    </div>
  );
};
```

- 렌더링될 때마다 뒷정리 함수가 계속 나타나는 것을 확인
- 뒷정리 함수가 호출될 때는 업데이트되기 직전의 값을 보여줌

<br>

# ✅ useReducer

- useState보다 더 **다양한 컴포넌트 상황에 따라 다양한 상태를 다른 값으로 업데이트**해 주고 싶을 때 사용하는 Hook
- `리듀서`는 현재 상태, **업데이트를 위해 필요한 정보를 담은** `액션 값`을 전달받아 새로운 상태를 반환하는 함수
- 리듀서 함수에서 새로운 상태를 만들 때는 반드시 불변성을 시켜 주어야 한다

```jsx
function reducer(state, action) {
	return {...} // 불변성을 지키면서 업데이트한 새로운 상태를 반환
}

// 액션 값 형태
{
	type: "INCREMENT"
}
```

- 예시

```jsx
import { useReducer } from "react";

function reducer(state, action) {
  // action.type에 따라 다른 작업 수행
  switch (action.type) {
    case "INCREMENT":
      return { value: state.value + 1 };
    case "DECREMENT":
      return { value: state.value - 1 };
    default:
      return state;
  }
}

const UseReducer = () => {
  const [state, dispatch] = useReducer(reducer, { value: 0 });

  return (
    <div>
      <p>
        현재 카운터 값 <b>{state.value}</b>
      </p>
      <button onClick={() => dispatch({ type: "INCREMENT" })}>+1</button>
      <button onClick={() => dispatch({ type: "DECREMENT" })}>-1</button>
    </div>
  );
};

export default UseReducer;
```

- `useReducer` (리듀서 함수, 해당 리듀서의 기본값)
- 이 Hook을 사용하면 `state값` = 현재 가리키고 있는 상태, `dispatch` = 액션을 발생시키는 함수
- dispatch(action)과 같은 형태로, 함수 안에서 파라미터로 액션 값을 넣어 주면 리듀서 함수가 호출되는 구조

- useReducer 가장 큰 장점 → 컴포넌트 업데이트 로직을 컴포넌트 바깥으로 빼낼 수 있다는 것

## 🔹 인풋 상태 관리하기

```jsx
import { useReducer } from "react";

function reducer(state, action) {
  return {
    ...state,
    [action.name]: action.value,
  };
}

const InfoReducer = () => {
  const [state, dispatch] = useReducer(reducer, {
    name: "",
    nickname: "",
  });
  const { name, nickname } = state;

  const OnChange = (e) => {
    dispatch(e.target);
  };

  return (
    <div>
      <div>
        <input name="name" value={name} onChange={OnChange}></input>
        <input name="nickname" value={nickname} onChange={OnChange}></input>
      </div>
      <div>
        <div>
          <b>이름:</b> {name}
        </div>
        <div>
          <b>닉네임:</b> {nickname}
        </div>
      </div>
    </div>
  );
};

export default InfoReducer;
```

<br>

# ✅ useMemo

- `useMemo`를 사용하면 **함수 컴포넌트 내부에서 발생하는 연산을 최적화**할 수 있다
- 예로 리스트에 숫자를 추가하면 숫자들의 평균을 보여 주는 컴포넌트 작성

```jsx
import { useState } from "react";

const getAverage = (numbers) => {
  console.log("평균값 계산중..");
  if (numbers.length === 0) return 0;
  const sum = numbers.reduce((a, b) => a + b);
  return sum / numbers.length;
};

const Average = () => {
  const [list, setList] = useState([]);
  const [number, setNumber] = useState("");

  const onChange = (e) => {
    setNumber(e.target.value);
  };

  const onInsert = (e) => {
    const nextList = list.concat(parseInt(number));
    setList(nextList);
    setNumber("");
  };
  return (
    <div>
      <input value={number} onChange={onChange}></input>
      <button onClick={onInsert}>등록</button>
      <ul>
        {list.map((value, index) => (
          <li key={index}>{value}</li>
        ))}
      </ul>
      <div>
        <b>평균값: </b> {getAverage(list)}
      </div>
    </div>
  );
};

export default Average;
```

- 이렇게 하면 숫자를 등록할 때뿐만 아니라 인풋 내용이 수정될 때도 우리가 만든 함수 getAverage 함수가 호출됨 → 인풋 내용이 바뀔 때는 평균값을 다시 계산할 필요 없음
- useMemo Hook을 사용하여 최적화
- 렌더링하는 과정에서 **특정 값이 바뀌었을 때만 연산을 실행하고 ([바뀌는 값]) , 원하는 값이 바뀌지 않았다면 이전에 연산했던 결과를 다시 사용하는 방식**

```jsx
const Average = () => {
  const [list, setList] = useState([]);
  const [number, setNumber] = useState("");

  const onChange = (e) => {
    setNumber(e.target.value);
  };

  const onInsert = (e) => {
    const nextList = list.concat(parseInt(number));
    setList(nextList);
    setNumber("");
  };

  const avg = **useMemo**(() => getAverage(list), [list]);

  return ( ... )
```

<br>

# ✅ useCallback

- 주로 **렌더링 성능을 최적화해야 하는 상황**에서 사용
- 이 Hook을 사용하면 **만들어 놨던 함수를 재사용**할 수 있다
- 예로 방금 구현한 onChange, onInsert 함수 선언을 컴포넌트가 리렌더링될 때마다 새로 만들어진 함수를 사용하게 된다 → 컴포넌트 갯수가 많아지면 최적해 주는 것이 좋다

```jsx
const Average = () => {
  const [list, setList] = useState([]);
  const [number, setNumber] = useState("");

  const onChange = useCallback( (e) => {
    setNumber(e.target.value);
  }, **[]**); // 컴포넌트가 처음 렌더링될 때만 함수 생성

  const onInsert = useCallback((e) => {
    const nextList = list.concat(parseInt(number));
    setList(nextList);
    setNumber("");
  }, **[nubmer, list]**); **// number 혹은 list가 바뀌었을 때만 함수 생성**
...
```

- `useCallback (생성하고 싶은 함수, 배열)` → 이 배열에는 어떤 값이 바뀌었을 때 함수를 새로 생성해야 하는지 명시하는 것
- 함수 내부에서 상태 값에 의존해야 할 때는 그 값을 반드시 두 번째 파라미터 안에 포함
  - 예로 onInsert는 기존의 number, list를 조회해서 nextList를 생성하기 때문에 배열 안에 꼭

<br>

# ✅ useRef

- `useRef` Hook은 **함수 컴포넌트에서 ref를 쉽게 사용**할 수 있도록 해준다

```jsx
const Average = () => {
  const [list, setList] = useState([]);
  const [number, setNumber] = useState("");
  **const inputEl = useRef(null);**

  const onChange = useCallback((e) => {
    setNumber(e.target.value);
  }, []); // 컴포넌트가 처음 렌더링될 때만 함수 생성

  const onInsert = useCallback(
    (e) => {
      const nextList = list.concat(parseInt(number));
      setList(nextList);
      setNumber("");
      **inputEl.current.focus();**
    },
    [number, list]
  ); // number 혹은 list가 바뀌었을 때만 함수 생성

  const avg = useMemo(() => getAverage(list), [list]);

  return (
    <div>
      <input value={number} onChange={onChange} **ref={inputEl}**></input>
```

### 🔸 로컬 변수 사용하기

- 컴포넌트 로컬 변수를 사용해야 할 때도 useRef를 사용
- `로컬 변수` : 렌더링과 상관없이 바뀔 수 있는 값을 의미

<br>

# ✅ 커스텀 Hooks 만들기

- **여러 컴포넌트에서 비슷한 기능을 공유할 경우**, 이를 Hook으로 작성하여 로직을 재사용 가능

```jsx
// 커스텀 Hook
import { useReducer } from "react";

function reducer(state, action) {
  return {
    ...state,
    [action.name]: action.value,
  };
}

export default function useInputs(initialForm) {
  const [state, dispatch] = useReducer(reducer, initialForm);
  const onChange = (e) => {
    dispatch(e.target);
  };
  return [state, onChange];
}
```

```jsx
import useInputs from "./useInputs";

const InfoReducer = () => {
  const [state, onChange] = useInputs({
    name: "",
    nickname: "",
  });
  const { name, nickname } = state;

  return (
    <div>
      <div>
        <input name="name" value={name} onChange={onChange}></input>
        <input name="nickname" value={nickname} onChange={onChange}></input>
      </div>
      <div>
        <div>
          <b>이름:</b> {name}
        </div>
        <div>
          <b>닉네임:</b> {nickname}
        </div>
      </div>
    </div>
  );
};

export default InfoReducer;
```
