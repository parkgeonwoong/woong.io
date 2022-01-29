---
title: 3. HTTP 기본
date: 2022-01-29 15:44:59
tags:
toc: true
categories:
  - http
---

# 📌 HTTP 기본

- [📌 HTTP 기본](#-http-기본)<!-- no toc -->
- [✅ 모든 것이 HTTP](#-모든-것이-http)
- [✅ 클라이언트-서버 구조](#-클라이언트-서버-구조)
- [✅ 무상태 프로토콜 = stateless](#-무상태-프로토콜--stateless)
- [✅ 비연결성](#-비연결성)
- [✅ HTTP 메시지](#-http-메시지)
- [✅ 단순하고 확장 가능](#-단순하고-확장-가능)

<br>

이미지 참고 : [https://velog.io/@dnstlr2933/HTTP](https://velog.io/@dnstlr2933/HTTP)

<!-- more -->

<br>

```markdown
# HTTP 정리

- HTTP 메시지에 모든 것을 전송
- HTTP/1.1을 기준으로 학습
- 클라이언트 서버 구조
- 무상태 프로토콜
- HTTP 메시지
- 단순함, 확장 가능
- 현재 HTTP 시대
```

<br>

# ✅ 모든 것이 HTTP

- HTML, TEXT
- IMAGE, 음성, 영상, 파일
- JSON, XML (API)
- 거의 모든 형태의 데이터를 전송할 수 있다
- 서버간에 데이터를 주고받을 때도 대부분 http 사용

HTTP/1.1 → 가장 많이 사용하며, 그 이상은 개선 버전일 뿐이다

- TCP : HTTP/1.1, HTTP/2
- UDP : HTTP/3

<br>

### 🔸 HTTP 특징

- 클라이언트 서버 구조
- 무상태 프로토콜, 비연결성
- HTTP 메시지
- 단순함, 확장 가능

<br>

# ✅ 클라이언트-서버 구조

- Request Response 구조
- 클라이언트는 서버에 요청을 보내고 → 응답을 대기
- 서버가 요청에 대한 결과를 만들어서 → 응답

**클라이언트와 서버를 구별**하게 된것이 핵심

구별함으로써 각각 자신의 서비스가 독립적으로 발전할 수 있게 되었다

서버 → 비즈니스 로직, 데이터 등

클라이언트 → UI, 사용성

<br>

# ✅ 무상태 프로토콜 = stateless

- `Stateful` → 상태유지, 서버가 클라이언트의 상태를 보존하는 것
- `Stateless` → 서버가 클라이언트의 상태를 보존 X
  - 장점 : 서버 확장성 높음 (스케일 아웃 : 수평 확장에 유리)
  - 단점 : 클라이언트가 추가 데이터 전송

<br>

### 🔸 stateful, stateless 차이

- 상태 유지
  - 중간에 다른 점원으로 바뀌면 안된다 (상태 정보를 미리 알려줘야 가능)
- 무상태
  - 중간에 다른 점원으로 바뀌어도 된다
  - 갑자기 고객이 증가해도 점원을 대거 투입 가능
  - 갑자기 클라이언트 요청 증가해도 서버를 대거 투입 가능
  - 무상태는 응답 서버를 쉽게 바꿀 수 있다 → 무한한 서버 증설 가능

![](/images/httpBase/Untitled.png)

![](/images/httpBase/Untitled1.png)

![](/images/httpBase/Untitled2.png)

<br>

### 🔸 Stateless 한계

- 모든 것을 무상태로 설계 할 수는 없다
- 무상태
  - 예) 로그인이 필요 없는 단순한 서비스 소개 화면
- 상태 유지
  - 예) 로그인
- 로그인한 사용자의 경우 로그인 했다는 상태를 서버에 유지
- 일반적으로 브라우저 쿠키와 서버 세션등을 사용해 상태 유지
- 상태 유지는 최소한만 사용
- 데이터를 많이 보내야 한다

<br>

# ✅ 비연결성

![](/images/httpBase/Untitled3.png)

- 이렇듯 연결을 유지해놓으면 → 서버의 자원이 계속해서 소모된다

- HTTP는 기본이 연결을 유지하지 않는 모델
- 일반적으로 초 단위의 이하의 빠른 속도로 응답
- 예) 웹 브라우저에서 계속 연속해서 검색 버튼을 누르지 않는다
- 서버 자원을 매우 효율적으로 사용할 수 있음

<br>

### 🔸 비 연결성 한계와 극복

- TCP/IP 연결을 새로 맺어야 함 - 3 way handshake 시간 추가
- 웹 브라우저로 사이트를 요청하면 HTML, JS, CSS, image 등 많은 자원이 함께 다운로드
- 지금은 HTTP 지속 연결로 문제 해결
- HTTP/2, 3에서 더많은 최적화

![](/images/httpBase/Untitled4.png)

![](/images/httpBase/Untitled5.png)

<br>

### 🔸 무상태를 기억하자

- 정말 같은 시간에 딱 맞추어 발생하는 대용량 트래픽
  - 예시) 선착순 이벤트, 명절 KTX 예약, 수강 신청

어떻게든 상태유지를 줄여서 무상태로 만들어서 순식간에 대응하기 위한 서버를 늘릴수 있도록 해야한다

따라서 첫 페이지는 아무런 상태도 필요없는 html로 이루어진 페이지를 놔두고 그 안에 이벤트 참여 버튼을 두게 하여서 조금이나마 한번에 덜 몰려오도록 설계

<br>

# ✅ HTTP 메시지

![](/images/httpBase/Untitled6.png)

<br>

### 🔸 http 메시지의 공식 스펙

```markdown
HTTP - message = start-line
\*( headerCRLF )
CRLF
[ message-body ]
```

<br>

## 🔹 시작 라인 (Start-line)

### 🔸 요청 메시지 (request-line)

```markdown
**GET /search?q=hello&hl=ko HTTP/1.1**
Host: www.google.com
```

- **HTTP 메서드** (GET: 조회)
- **요청 대상** (/search?q=hello&hl=ko)
- **HTTP Version**

상세히 설명하면

요청 메시지 - `HTTP 메서드`

- 종류 : GET, POST, PUT, DELETE
- 서버가 수행해야 할 동작 지정
  - GET : 리소스 조회
  - POST : 요청 내역 처리

요청 메시지 - `요청 대상`

- absolute-path[?query] (절대경로[?쿼리])
- 절대경로= "/" 로 시작하는 경로

<br>

### 🔸 응답 메시지 (status-line)

```markdown
**HTTP/1.1 200 OK**
Content-Type: text/html;charset=UTF-8
Content-Length: 3423

<html>
 <body>...</body>
</html>
```

- **HTTP 버전**
- **HTTP 상태 코드:** 요청 성공, 실패를 나타냄
  • 200: 성공
  • 400: 클라이언트 요청 오류
  • 500: 서버 내부 오류
- **이유 문구:** 사람이 이해할 수 있는 짧은 상태 코드 설명 글

<br>

## 🔹 HTTP 헤더

![](/images/httpBase/Untitled7.png)

<br>

### 🔸 HTTP 헤더 용도

- HTTP 전송에 필요한 모든 부가 정보
  - 메시지 바디의 내용, 크기, 압축, 인증, 요청 클라이언트 정보, 서버 애플리케이션 정보, 캐시
- 표준 헤더가 너무 많다
- 필요시 임의의 헤더 추가 가능
- **즉, 메시지 바디 빼고 필요한 메타 데이터 정보 다 있다**

<br>

## 🔹 HTTP 메시지 바디

- 실제 전송할 데이터
- HTML 문서, 이미지, 영상, JSON 등 → byte로 표현할 수 있는 모든 데이터 전송 가능

<br>

# ✅ 단순하고 확장 가능

- HTTP는 단순하다
- HTTP 메시지도 매우 단순하다
- 크게 성공하는 표준 기술은 → 단순하지만 확장 가능한 기술
