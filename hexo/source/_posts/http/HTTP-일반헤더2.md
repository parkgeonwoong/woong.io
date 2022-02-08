---
title: 8.HTTP-일반헤더2
date: 2022-02-08 14:11:23
tags:
toc: true
categories:
  - http
---

- [✅ 전송 방식](#-전송-방식)
    - [🔸 단순 전송](#-단순-전송)
    - [🔸 압축 전송](#-압축-전송)
    - [🔸 분할 전송](#-분할-전송)
    - [🔸 범위 전송](#-범위-전송)
- [✅ 일반 정보](#-일반-정보)
    - [🔸 From](#-from)
    - [🔸 Referer](#-referer)
    - [🔸 User-Agent](#-user-agent)
    - [🔸 Server](#-server)
    - [🔸 Date](#-date)
- [✅ 특별한 정보 헤더](#-특별한-정보-헤더)
    - [🔸 Host](#-host)
    - [🔸 Location](#-location)
    - [🔸 Allow](#-allow)
    - [🔸 Retry-After](#-retry-after)

<!-- more -->

<br>

# ✅ 전송 방식

- 단순 전송
- 압축 전송
- 분할 전송
- 범위 전송

<br>

### 🔸 단순 전송

**Content-Length**

- 전달하고자 하는 message-body의 길이를 아는 경우

<br>

### 🔸 압축 전송

**Content-Encoding**

전달하고자 하는 표현 데이터를 압축해서 전달하되 **꼭** 표현 헤더에 `Content-Encoding`을 넣어줘서 해당 압축을 읽을 수 있도록 해야 한다

<br>

### 🔸 분할 전송

**Transfer-Encoding**

![](/images/httpheader/Untitled6.png)

- 바이트 단위로 쪼개서 분할해 보낸다

<br>

### 🔸 범위 전송

**Range, Content-Range**

어떤 데이터를 전달하다가 끊겼을 때, 끊긴 데이터만 범위로 지정해서 보내는 것

<br>

# ✅ 일반 정보

- From: 유저 에이전트의 이메일 정보
- Referer: 이전 웹 페이지 주소
- User-Agent: 유저 에이전트 애플리케이션 정보
- Server: 요청을 처리하는 오리진 서버의 소프트웨어 정보
- Date: 메시지가 생성된 날짜

<br>

### 🔸 From

**유저 에이전트의 이메일 정보**

- 검색 엔진 같은 곳에서 나의 사이트를 크롤링 하는등 접근하는 경우 해당 검색 엔진의 담당자에게 이메일로 연락하는 경우 등에 사용한다
- 요청에서 사용
- 거의 사용하지 않는다

<br>

### 🔸 Referer

**이전 웹페이지 주소**

- 현재 요청된 페이지의 이전 웹페이지 주소
- A → B로 이동하는 경우 B로 요청할 때 Referer: A를 포함해서 요청한다
- Referer를 사용해서 유입 경로 분석을 할 수 있다
- 요청에서 사용한다

<br>

### 🔸 User-Agent

**유저 에이전트 애플리케이션 정보**

- Mozilla/5.0 (Macintosh; Intel Mac OS X 11_1_0) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/87.0.4280.88 Safari/537.36
- 클라이언트의 애플리케이션 정보(웹 브라우저 정보 등등)
- 통계 정보로 활용
- 어떤 종류의 브라우저에서 장애가 발생하는지 파악이 가능하다
- 요청에서 사용한다

<br>

### 🔸 Server

**요청을 처리하는 ORIGIN서버의 소프트웨어 정보**

- Server: Apache/2.2.22 (Debian)
- server: nginx
- 최종적으로 응답을 처리해주는 서버이다
- 응답에서 사용

<br>

### 🔸 Date

**메시지가 발생한 날짜와 시간**

- Date: Tue, 15 Nov 1994 08:12:31 GMT
- 응답에서만 사용한다

<br>

# ✅ 특별한 정보 헤더

- Host : 요청한 호스트 정보 (도메인)
- Location : 페이지 리다이렉션
- Allow : 허용 가능한 HTTP 메서드
- Retry-After : 유저 에이전트가 다음 요청을 하기까지 기다려야 하는 시간

<br>

### 🔸 Host

- 요청에서 사용한다
- **필수**적으로 넣어야한다
- 하나의 서버가 여러 도메인을 처리해야 할 때
- 하나의 IP 주소에 여러 도메인이 적용되어 있을 때

```jsx
GET /search?q=hello&hl=ko HTTP/1.1
Host: www.google.com
```

- 가상호스트를 통해 여러 도메인을 한번에 처리할 수 있는 서버 실제 애플리케이션이 여러개 구동될 수 있다.

![](/images/httpheader/Untitled7.png)

<br>

### 🔸 Location

**페이지 리다이렉션**

- 웹 브라우저는 3xx 응답의 결과에 Location 헤더가 있으면, Location 위치로 **자동 이동**한다 (리다이렉트)
- 201 (Created) : Lcation값은 **요청에 의해 생성된 리소스 URI**
- 3xx (Redirection) : Location값은 요청을 **자동으로 리다이렉션하기 위한 대상 리소스**를 가리킨다

<br>

### 🔸 Allow

**허용 가능한 HTTP 메서드**

- 405(Method Not Allowed)에서 응답에 포함해야 한다
- Allow: GET, HEAD, PUT

만약 서버가 허용하지 않는 메서드 ex) `PATCH` 등이 온 경우 응답으로 405를 주면서 허용하는 메서드를 `Allow: GET, HEAD, PUT`으로 알려줘야 한다

<br>

### 🔸 Retry-After

**유저 에이전트가 다음 요청을 하기까지 기다려야하는 시간**

- 503 (Service Unavailable) : 서비스가 언제까지 불능인지 알려줄 수 있다
- Retry-After: Fri, 31 DEC 1999 23:59:59 GMT (날짜 표기)
- Retry-After: 120 (초 단위 표기)
