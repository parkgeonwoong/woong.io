---
title: Hooks
date: 2022-02-23 14:57:49
tags:
toc: true
categories:
  - React
  - Document
---

# πHooks

[Hookμ κ°μ - React](https://ko.reactjs.org/docs/hooks-intro.html)

- [πHooks](#hooks)
- [β useState](#-usestate)
  - [πΉ useState μ¬λ¬ λ² μ¬μ©νκΈ°](#-usestate-μ¬λ¬-λ²-μ¬μ©νκΈ°)
- [β useEffect](#-useeffect)
  - [πΉ λ§μ΄νΈλ  λλ§ μ€ννκ³  μΆμ λ](#-λ§μ΄νΈλ -λλ§-μ€ννκ³ -μΆμ-λ)
  - [πΉ νΉμ  κ°μ΄ μλ°μ΄νΈλ  λλ§ μ€ννκ³  μΆμ λ](#-νΉμ -κ°μ΄-μλ°μ΄νΈλ -λλ§-μ€ννκ³ -μΆμ-λ)
  - [πΉ λ·μ λ¦¬νκΈ°](#-λ·μ λ¦¬νκΈ°)
- [β useReducer](#-usereducer)
  - [πΉ μΈν μν κ΄λ¦¬νκΈ°](#-μΈν-μν-κ΄λ¦¬νκΈ°)
- [β useMemo](#-usememo)
- [β useCallback](#-usecallback)
- [β useRef](#-useref)
    - [πΈ λ‘μ»¬ λ³μ μ¬μ©νκΈ°](#-λ‘μ»¬-λ³μ-μ¬μ©νκΈ°)
- [β μ»€μ€ν Hooks λ§λ€κΈ°](#-μ»€μ€ν-hooks-λ§λ€κΈ°)

<br>

<!-- more -->

```markdown
# μ λ¦¬

1. Hooksμ react λͺ¨λμμ λΆλ¬μ¨λ€

2. **useState** = μνκ΄λ¦¬

3. **useEffect** = λ λλ§λ  λλ§λ€ νΉμ  μμ μν μ€μ 

- callback νΈμΆλ‘ λνλΈλ€
- μλ°μ΄νΈλ λ³΄μ¬μ£Όκ³  μΆμ§ μμ λ -> λλ²μ§Έ νλΌλ―Έν° [ ]
- νΉμ  κ°λ§ λ³΄μ¬μ£Όκ³  μΆμ λ -> [κ²μ¬νκ³  μΆμ κ° ]

4. **useReducer** = λ€μν μν μλ°μ΄νΈ

- λ¦¬λμ ν¨μ λ§λ€κΈ° (state, action= type μ€μμΉ, return)
- μν, dispatch(λ¦¬λμ ν¨μ νΈμΆ)

5. **useCallback** = λ§λ€μ΄λ¨λ ν¨μλ₯Ό μ¬μ¬μ©

- [] -> μ²μ λ λλ§λ λ λ§ μμ±
- [ λ°λλ κ° ]

6. **useRef** = refλ₯Ό μ½κ² μ¬μ©

- current

7. **custom Hook** = μ¬λ¬ μ»΄ν¬λνΈμμ λΉμ·ν κΈ°λ₯ κ³΅μ 
```

<br>

# β useState

- useState ν¨μμ νλΌλ―Έν°μλ = `μνμ κΈ°λ³Έκ°`
- μ΄ ν¨μκ° νΈμΆλλ©΄ λ°°μ΄μ λ°ν β (`μν κ°` , `μνλ₯Ό μ€μ νλ ν¨μ`)

```jsx
import { useState } from "react";

const Counter = () => {
  const [value, setValue] = useState(0);

  return (
    <div>
      <p>
        νμ¬ μΉ΄μ΄ν° κ° <b>{value}</b>
      </p>
      <button onClick={() => setValue(value + 1)}>+1</button>
      <button onClick={() => setValue(value - 1)}>-1</button>
    </div>
  );
};

export default Counter;
```

## πΉ useState μ¬λ¬ λ² μ¬μ©νκΈ°

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
          <b>μ΄λ¦:</b> {name}
        </div>
        <div>
          <b>λλ€μ:</b> {nickname}
        </div>
      </div>
    </div>
  );
};

export default Info;
```

<br>

# β useEffect

- λ¦¬μ‘νΈ μ»΄ν¬λνΈκ° **λ λλ§λ  λλ§λ€ νΉμ  μμμ μννλλ‘ μ€μ **ν  μ μλ Hook

```jsx
import { useState, useEffect } from "react";

const Info = () => {
  const [name, setName] = useState("");
  const [nickname, setNickname] = useState("");

  useEffect(() => {
    console.log("λ λλ§μ΄ μλ£");
    console.log({
      name,
      nickname,
    });
  });

...
```

## πΉ λ§μ΄νΈλ  λλ§ μ€ννκ³  μΆμ λ

- useEffectμμ μ€μ ν ν¨μλ₯Ό μ»΄ν¬λνΈκ° νλ©΄μ **λ§¨ μ²μ λ λλ§λ  λλ§ μ€ν**νκ³ , μλ°μ΄νΈλ  λλ μ€ννμ§ μμΌλ €λ©΄ β ν¨μμ λλ²μ§Έ νλΌλ―Έν°λ‘ `λΉμ΄ μλ λ°°μ΄`μ λ£μ΄μ£Όλ©΄ λλ€

```jsx
useEffect(() => {
  console.log("λ λλ§μ΄ μλ£");
  console.log({
    name,
    nickname,
  });
}, []);
```

## πΉ νΉμ  κ°μ΄ μλ°μ΄νΈλ  λλ§ μ€ννκ³  μΆμ λ

- valueκ°μ΄ λ°λ λλ§ νΉμ  μμ μν β λλ²μ§Έ νλΌλ―Έν°λ‘ μ λ¬λλ λ°°μ΄ μμ κ²μ¬νκ³  μΆμ κ°

```jsx
useEffect(() => {
  console.log("λ λλ§μ΄ μλ£");
  console.log({
    name,
    nickname,
  });
}, [name]);
```

## πΉ λ·μ λ¦¬νκΈ°

- useEffectλ κΈ°λ³Έμ μΌλ‘ λ λλ§λκ³  λ μ§νλ§λ€ μ€νλλ©°, λ λ²μ§Έ νλΌλ―Έν° λ°°μ΄μ λ¬΄μμ λ£λμ§μ λ°λΌ μ€νλλ μ‘°κ±΄μ΄ λ¬λΌμ§λ€
- λ·μ λ¦¬ ν¨μ β μ»΄ν¬λνΈκ° μΈλ§μ΄νΈλκΈ° μ μ΄λ μλ°μ΄νΈ μ§μ μ μ΄λ ν μμμ μννκ³  μΆμ λ

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
        {visible ? "μ¨κΈ°κΈ°" : "λ³΄μ΄κΈ°"}{" "}
      </button>
      <hr />
      {visible && <Info />}
    </div>
  );
};
```

- λ λλ§λ  λλ§λ€ λ·μ λ¦¬ ν¨μκ° κ³μ λνλλ κ²μ νμΈ
- λ·μ λ¦¬ ν¨μκ° νΈμΆλ  λλ μλ°μ΄νΈλκΈ° μ§μ μ κ°μ λ³΄μ¬μ€

<br>

# β useReducer

- useStateλ³΄λ€ λ **λ€μν μ»΄ν¬λνΈ μν©μ λ°λΌ λ€μν μνλ₯Ό λ€λ₯Έ κ°μΌλ‘ μλ°μ΄νΈ**ν΄ μ£Όκ³  μΆμ λ μ¬μ©νλ Hook
- `λ¦¬λμ`λ νμ¬ μν, **μλ°μ΄νΈλ₯Ό μν΄ νμν μ λ³΄λ₯Ό λ΄μ** `μ‘μ κ°`μ μ λ¬λ°μ μλ‘μ΄ μνλ₯Ό λ°ννλ ν¨μ
- λ¦¬λμ ν¨μμμ μλ‘μ΄ μνλ₯Ό λ§λ€ λλ λ°λμ λΆλ³μ±μ μμΌ μ£Όμ΄μΌ νλ€

```jsx
function reducer(state, action) {
	return {...} // λΆλ³μ±μ μ§ν€λ©΄μ μλ°μ΄νΈν μλ‘μ΄ μνλ₯Ό λ°ν
}

// μ‘μ κ° νν
{
	type: "INCREMENT"
}
```

- μμ

```jsx
import { useReducer } from "react";

function reducer(state, action) {
  // action.typeμ λ°λΌ λ€λ₯Έ μμ μν
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
        νμ¬ μΉ΄μ΄ν° κ° <b>{state.value}</b>
      </p>
      <button onClick={() => dispatch({ type: "INCREMENT" })}>+1</button>
      <button onClick={() => dispatch({ type: "DECREMENT" })}>-1</button>
    </div>
  );
};

export default UseReducer;
```

- `useReducer` (λ¦¬λμ ν¨μ, ν΄λΉ λ¦¬λμμ κΈ°λ³Έκ°)
- μ΄ Hookμ μ¬μ©νλ©΄ `stateκ°` = νμ¬ κ°λ¦¬ν€κ³  μλ μν, `dispatch` = μ‘μμ λ°μμν€λ ν¨μ
- dispatch(action)κ³Ό κ°μ ννλ‘, ν¨μ μμμ νλΌλ―Έν°λ‘ μ‘μ κ°μ λ£μ΄ μ£Όλ©΄ λ¦¬λμ ν¨μκ° νΈμΆλλ κ΅¬μ‘°

- useReducer κ°μ₯ ν° μ₯μ  β μ»΄ν¬λνΈ μλ°μ΄νΈ λ‘μ§μ μ»΄ν¬λνΈ λ°κΉ₯μΌλ‘ λΉΌλΌ μ μλ€λ κ²

## πΉ μΈν μν κ΄λ¦¬νκΈ°

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
          <b>μ΄λ¦:</b> {name}
        </div>
        <div>
          <b>λλ€μ:</b> {nickname}
        </div>
      </div>
    </div>
  );
};

export default InfoReducer;
```

<br>

# β useMemo

- `useMemo`λ₯Ό μ¬μ©νλ©΄ **ν¨μ μ»΄ν¬λνΈ λ΄λΆμμ λ°μνλ μ°μ°μ μ΅μ ν**ν  μ μλ€
- μλ‘ λ¦¬μ€νΈμ μ«μλ₯Ό μΆκ°νλ©΄ μ«μλ€μ νκ· μ λ³΄μ¬ μ£Όλ μ»΄ν¬λνΈ μμ±

```jsx
import { useState } from "react";

const getAverage = (numbers) => {
  console.log("νκ· κ° κ³μ°μ€..");
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
      <button onClick={onInsert}>λ±λ‘</button>
      <ul>
        {list.map((value, index) => (
          <li key={index}>{value}</li>
        ))}
      </ul>
      <div>
        <b>νκ· κ°: </b> {getAverage(list)}
      </div>
    </div>
  );
};

export default Average;
```

- μ΄λ κ² νλ©΄ μ«μλ₯Ό λ±λ‘ν  λλΏλ§ μλλΌ μΈν λ΄μ©μ΄ μμ λ  λλ μ°λ¦¬κ° λ§λ  ν¨μ getAverage ν¨μκ° νΈμΆλ¨ β μΈν λ΄μ©μ΄ λ°λ λλ νκ· κ°μ λ€μ κ³μ°ν  νμ μμ
- useMemo Hookμ μ¬μ©νμ¬ μ΅μ ν
- λ λλ§νλ κ³Όμ μμ **νΉμ  κ°μ΄ λ°λμμ λλ§ μ°μ°μ μ€ννκ³  ([λ°λλ κ°]) , μνλ κ°μ΄ λ°λμ§ μμλ€λ©΄ μ΄μ μ μ°μ°νλ κ²°κ³Όλ₯Ό λ€μ μ¬μ©νλ λ°©μ**

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

# β useCallback

- μ£Όλ‘ **λ λλ§ μ±λ₯μ μ΅μ νν΄μΌ νλ μν©**μμ μ¬μ©
- μ΄ Hookμ μ¬μ©νλ©΄ **λ§λ€μ΄ λ¨λ ν¨μλ₯Ό μ¬μ¬μ©**ν  μ μλ€
- μλ‘ λ°©κΈ κ΅¬νν onChange, onInsert ν¨μ μ μΈμ μ»΄ν¬λνΈκ° λ¦¬λ λλ§λ  λλ§λ€ μλ‘ λ§λ€μ΄μ§ ν¨μλ₯Ό μ¬μ©νκ² λλ€ β μ»΄ν¬λνΈ κ°―μκ° λ§μμ§λ©΄ μ΅μ ν΄ μ£Όλ κ²μ΄ μ’λ€

```jsx
const Average = () => {
  const [list, setList] = useState([]);
  const [number, setNumber] = useState("");

  const onChange = useCallback( (e) => {
    setNumber(e.target.value);
  }, **[]**); // μ»΄ν¬λνΈκ° μ²μ λ λλ§λ  λλ§ ν¨μ μμ±

  const onInsert = useCallback((e) => {
    const nextList = list.concat(parseInt(number));
    setList(nextList);
    setNumber("");
  }, **[nubmer, list]**); **// number νΉμ listκ° λ°λμμ λλ§ ν¨μ μμ±**
...
```

- `useCallback (μμ±νκ³  μΆμ ν¨μ, λ°°μ΄)` β μ΄ λ°°μ΄μλ μ΄λ€ κ°μ΄ λ°λμμ λ ν¨μλ₯Ό μλ‘ μμ±ν΄μΌ νλμ§ λͺμνλ κ²
- ν¨μ λ΄λΆμμ μν κ°μ μμ‘΄ν΄μΌ ν  λλ κ·Έ κ°μ λ°λμ λ λ²μ§Έ νλΌλ―Έν° μμ ν¬ν¨
  - μλ‘ onInsertλ κΈ°μ‘΄μ number, listλ₯Ό μ‘°νν΄μ nextListλ₯Ό μμ±νκΈ° λλ¬Έμ λ°°μ΄ μμ κΌ­

<br>

# β useRef

- `useRef` Hookμ **ν¨μ μ»΄ν¬λνΈμμ refλ₯Ό μ½κ² μ¬μ©**ν  μ μλλ‘ ν΄μ€λ€

```jsx
const Average = () => {
  const [list, setList] = useState([]);
  const [number, setNumber] = useState("");
  **const inputEl = useRef(null);**

  const onChange = useCallback((e) => {
    setNumber(e.target.value);
  }, []); // μ»΄ν¬λνΈκ° μ²μ λ λλ§λ  λλ§ ν¨μ μμ±

  const onInsert = useCallback(
    (e) => {
      const nextList = list.concat(parseInt(number));
      setList(nextList);
      setNumber("");
      **inputEl.current.focus();**
    },
    [number, list]
  ); // number νΉμ listκ° λ°λμμ λλ§ ν¨μ μμ±

  const avg = useMemo(() => getAverage(list), [list]);

  return (
    <div>
      <input value={number} onChange={onChange} **ref={inputEl}**></input>
```

### πΈ λ‘μ»¬ λ³μ μ¬μ©νκΈ°

- μ»΄ν¬λνΈ λ‘μ»¬ λ³μλ₯Ό μ¬μ©ν΄μΌ ν  λλ useRefλ₯Ό μ¬μ©
- `λ‘μ»¬ λ³μ` : λ λλ§κ³Ό μκ΄μμ΄ λ°λ μ μλ κ°μ μλ―Έ

<br>

# β μ»€μ€ν Hooks λ§λ€κΈ°

- **μ¬λ¬ μ»΄ν¬λνΈμμ λΉμ·ν κΈ°λ₯μ κ³΅μ ν  κ²½μ°**, μ΄λ₯Ό HookμΌλ‘ μμ±νμ¬ λ‘μ§μ μ¬μ¬μ© κ°λ₯

```jsx
// μ»€μ€ν Hook
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
          <b>μ΄λ¦:</b> {name}
        </div>
        <div>
          <b>λλ€μ:</b> {nickname}
        </div>
      </div>
    </div>
  );
};

export default InfoReducer;
```
