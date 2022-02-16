---
title: 9. HTTP-인증헤더&쿠키
date: 2022-02-16 13:39:58
tags:
toc: true
categories:
  - http
---

# 📌 인증 헤더, 쿠키

- [📌 인증 헤더, 쿠키](#-인증-헤더-쿠키)
  - [✅ 인증](#-인증)
    - [🔸 Authorizaton](#-authorizaton)
    - [🔸 WWW-Authenticate](#-www-authenticate)
  - [✅ 쿠키](#-쿠키)
    - [예제 - 쿠키 미사용](#예제---쿠키-미사용)
    - [🔸 Stateless (무상태)](#-stateless-무상태)
    - [🔸 쿠키 상세 설명](#-쿠키-상세-설명)
    - [🔸 쿠키 - 생명 주기](#-쿠키---생명-주기)
    - [🔸 쿠키 - 도메인](#-쿠키---도메인)
    - [🔸 쿠키 - 경로](#-쿠키---경로)
    - [🔸 쿠키 - 보안](#-쿠키---보안)

참고 : [https://velog.io/@dnstlr2933/HTTP-헤더-일반헤더](https://velog.io/@dnstlr2933/HTTP-%ED%97%A4%EB%8D%94-%EC%9D%BC%EB%B0%98%ED%97%A4%EB%8D%94)

<!-- more -->

<br>

## ✅ 인증

### 🔸 Authorizaton

**클라이언트 인증 정보를 서버에 전달**

- Authorization: Basic xxxxxxxxxxxx
  - 인증하는 메커니즘마다 들어가는 값이 다르다

### 🔸 WWW-Authenticate

**리소스 접근시 필요한 인증 방법 정의**

- 리소스 접근시 필요한 인증 방법을 정의한다
- 401 Unauthorized 응답과 함께 사용한다
- WWW-Authenticate: `Newauth realm="apps", type=1, title="Login to\"apps\"", Basic realm="simple"`
  - 위와 같은 내용을 참고해서 요청하라는 뜻이다

<br>

## ✅ 쿠키

- Set-Cookie : 서버에서 클라이언트로 쿠키 전달 (응답)
- Cookie : 클라이언트가 서버에서 받은 쿠키를 저장하고, HTTP 요청시 서버로 전달

### 예제 - 쿠키 미사용

![](/images/httpCookie/Untitled.png)
위의 이유는?

### 🔸 Stateless (무상태)

- HTTP는 무상태(Stateless) 프로토콜이다
- 클라이언트와 서버가 요청과 응답을 주고 받고나면 연결이 끊어진다
- 클라이언트가 다시 요청하면 **서버는 이전 요청을 기억하지 못한다**
  - 로그인 정보 조차도 기억하지 못한다
- 클라이언트와 서버는 서로 **상태를 유지하지 않는다**

`대안` → 모든 요청에 사용자 정보 포함

모든 요청과 링크에 사용자를 포함해야 해서 복잡해진다

Q. 그럼 어떻게 정보를 기억하지?

A. 요청 할 때마다 정보를 같이 넘기자

- 모든 요청에 사용자 정보가 포함되도록 해야 한다
  - 보안 문제도 있고, 복잡하다
- 브라우저를 완전히 종료하고 다시 열면 또 복잡해진다
- 최종적인 대안으로 쿠키가 나왔다

![](/images/httpCookie/Untitled1.png)

- 자동으로 웹브라우저는 해당 서버에 요청을 보낼 때 마다 **쿠키 저장소를 항상 탐색**해서
  헤더에 포함해 서버에 보낸다

- 모든 요청에 쿠키 정보 자동 포함

![](/images/httpCookie/Untitled2.png)

<br>

### 🔸 쿠키 상세 설명

```jsx
set-cookie: **sessionId=abcde1234; expires**=Sat, 26-Dec-2020 00:00:00 GMT;
**path**=/; **domain**=.google.com; **Secure**
```

- 사용처

  - 사용자 로그인 세션 관리
    - 유저의 이름 등 보안상 문제로 → 서버에서 sessionkey 만들어서 → sessionId 치환
  - 광고 정보 트래킹

- 쿠키 정보는 항상 서버에 전송됨

  - 네트워크 트래픽 추가 유발
  - 최소한의 정보만 사용 (세션 id, 인증 토큰)
  - 서버에 전송하지 않고, 웹 브라우저 내부에 데이터를 저장하고 싶으면 웹 스토리지 (localStorage, sessionStorage) 참고

- 보안에 민감한 데이터는 저장하면 안됨 (주민번호, 신용카드 번호 등등)

<br>

### 🔸 쿠키 - 생명 주기

**Expires, max-age**

- Set-Cookie: expires=Sat, 26-Dec-2020 04:50:59 GMT
  - 만료일이 되면 쿠키를 삭제한다
- Set-Cookie: max-age=3600 (초단위이다)
  - 0이하의 수를 지정하게되면 삭제한다
- 세션 쿠키 : 만료날짜를 생략하면 브라우저 종료시 까지만 유지한다
- 영속 쿠키 : 만료날짜를 입력하면 해당 날짜까지 유지된다

<br>

### 🔸 쿠키 - 도메인

**Domain**

예) domain=example.org

- 명시 : 명시한 문서 기준 도메인 + 서브 도메인 포함
  - domain=example.org를 지정해서 쿠키 생성
    - example.org는 물론이고, dev.example.org도 쿠키 접근 한다
- 생략 : 현재 문서 기준 도메인만 적용한다
  - example.org에서 쿠키를 생성하고 domain지정을 생략
    - example.org에서만 쿠키가 접근하고
    - dev.example.org는 쿠키가 접근할 수 없다

<br>

### 🔸 쿠키 - 경로

예) path=/home

- 입력한 경로를 **포함한 하위 경로 페이지만 쿠키가 접근**
- 일반적으로 `path=/`(루트)로 지정한다
- 예)
  - path=/home 지정
  - /home --> o
  - /home/level1 --> o
  - /home/level1/level2 .. --> o
  - /hello --> x

<br>

### 🔸 쿠키 - 보안

**Secure, HttpOnly, SameSite**

- Secure
  - 기본적으로 쿠키는 http, https를 구분하지 않고 전송한다
  - Secure를 설정하면 https인 경우에만 전송한다
- HttpOnly
  - XSS 공격을 방지
  - 자바스크립트에서 접근 불가능하다 (document.cookie) , 원래는 접근 가능
  - HTTP 전송에만 사용
- SameSite
  - XSRF 공격을 방지한다
  - 요청 도메인과 쿠키에 설정된 도메인이 같은 경우에만 쿠키를 전송한다
