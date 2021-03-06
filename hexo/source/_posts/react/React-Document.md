---
title: React-Document
date: 2022-01-16 20:15:52
tags:
categories:
  - React
  - Document
toc: true
---

# 📌React Document

[React - 사용자 인터페이스를 만들기 위한 JavaScript 라이브러리](https://ko.reactjs.org/)

- React는 사용자 인터페이스를 만들기 위한 JavaScript 라이브러리
  <br>

- [📌React Document](#react-document)
    - [✅ 선언형](#-선언형)
    - [✅ 컴포넌트 기반](#-컴포넌트-기반)
    - [✅ 간단한 컴포넌트](#-간단한-컴포넌트)
    - [✅ 상태를 가지는 컴포넌트](#-상태를-가지는-컴포넌트)
    - [✅ 외부 플러그인을 사용하는 컴포넌트](#-외부-플러그인을-사용하는-컴포넌트)
    - [✅ 리액트의 특징](#-리액트의-특징)
    - [✅ Create React APP](#-create-react-app)

<br>

<!-- more -->

### ✅ 선언형

- 상호작용이 많은 UI를 만들 때 → 어려움을 줄여줌
- 애플리케이션의 각 상태에 대해 → 뷰 만 설계
- 데이터가 변경됨에 따라 컴포넌트 → 갱신하고 렌더링

```markdown
**어떤 데이터가 변할 때마다 어떤 변화를 줄지 고민하는 것이 아니라
그냥 기존 뷰를 날려 버리고 처음부터 새로 렌더링하는 방식**

- 새롭게 리렌더링하면서 성능을 아끼고, 최적의 UX을 제공할 수 있을까?
  데이터 업데이트시 업데이트한 값을 수정하는 것이 아니라, render 함수를 또 다시 호출
  이때 render함수가 반환하는 결과를 DOM에 반영하지 않고, 이전에 render 함수가 만든 컴포넌트
  정보와 현재 컴포넌트를 비교하여 -> 둘의 차이를 최소한 연산으로 DOM 트리 업데이트
```

<br>

### ✅ 컴포넌트 기반

- `컴포넌트` : 스스로 상태를 관리하는 캡슐화
- 조합해 복잡한 UI를 만듬
- 컴포넌트 로직 → 템플릿 X, Javascript로 작성
- 다양한 형식의 데이터를 앱 안에서 전달, DOM과는 별개로 상태를 관리

```markdown
# 컴포넌트

- React 프로젝트에서 특정 부분이 어떻게 생길지 정하는 선언체
- 재사용이 가능한 API로 수 많은 기능들을 내장
- 컴포넌트 하나에서 해당 컴포넌트의 생김새와 작동 방식을 정의

# 렌더링

- 사용자 화면에 뷰를 보여 주는 것
```

<br>

### ✅ 간단한 컴포넌트

- React 컴포넌트는 `render( )` 메서드를 구현 → 데이터를 입력받아 화면에 표시할 내용을 반환하는 역할
- 컴포넌트로 전달된 데이터는 `render( )` 안에서 `this.props`를 통해 접근

```markdown
# render()

- 컴포넌트가 어떻게 생겼는지 정의하는 역할
- 뷰가 어떻게 생겼고, 어떻게 작동하는지에 대한 정보를 지닌 객체를 반환
```

<br>

### ✅ 상태를 가지는 컴포넌트

- 컴포넌트는 `this.props`를 이용해 → 입력 데이터 + 내부적인 상태 데이터를 가짐
- 이는 `this.state`로 접근할 수 있다.
- 컴포넌트의 상태 데이터가 바뀌면 → `render()`가 다시 호출되어 마크업 갱신

<br>

### ✅ 외부 플러그인을 사용하는 컴포넌트

- React는 다른 라이브러리나 프레임워크 함께 활용

<br>

### ✅ 리액트의 특징

- Virtual DOM을 사용하는 것
- DOM : 객체로 문서 구조를 표현하는 방법으로 XML, HTML로 작성
- Virtual DOM을 사용하면 → 실제 DOM에 접근하여 조작하는것이 아닌 추상화한 JS 객체를 구성하여 사용

```markdown
1. 데이터를 업데이트하면 전체 UI를 Virtual DOM에 리렌더링한다.
2. 이전 Virtual DOM에 있던 내용과 현재 내용을 비교한다
3. 바뀐 부분만 실제 DOM에 적용한다.
```

<br>

### ✅ Create React APP

```bash
npx create-react-app my-app
cd my-app
npm start
```
