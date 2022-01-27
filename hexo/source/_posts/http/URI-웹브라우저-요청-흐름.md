---
title: 2. URI 웹브라우저 요청 흐름
date: 2022-01-27 13:27:56
tags:
toc: true
categories:
  - http
---

# 📌 URI와 웹 브라우저 요청 흐름

- [📌 URI와 웹 브라우저 요청 흐름](#-uri와-웹-브라우저-요청-흐름)
- [✅ URI](#-uri)
  - [🔹 URL 문법 분석](#-url-문법-분석)
    - [🔸 scheme](#-scheme)
    - [🔸 userinfo](#-userinfo)
    - [🔸 host](#-host)
    - [🔸 path](#-path)
    - [🔸 query](#-query)
    - [🔸 fragment](#-fragment)
- [✅ 웹 브라우저 요청 흐름](#-웹-브라우저-요청-흐름)
    - [🔸 HTTP 메시지 전송](#-http-메시지-전송)

<br>

이미지 참고: [https://velog.io/@dnstlr2933/HTTP-웹-기본학습#uri와-웹-브라우저-요청-흐름](https://velog.io/@dnstlr2933/HTTP-%EC%9B%B9-%EA%B8%B0%EB%B3%B8%ED%95%99%EC%8A%B5#uri%EC%99%80-%EC%9B%B9-%EB%B8%8C%EB%9D%BC%EC%9A%B0%EC%A0%80-%EC%9A%94%EC%B2%AD-%ED%9D%90%EB%A6%84)

<!-- more -->

<br>

# ✅ URI

- Uniform Resource Identifier
- **URI는 locator, name 둘다 또는 추가로 분류될 수 있다**

![](/images/url/url.png)

- URI → URL + URN
- Uniform : 리소스 식별하는 통일된 방식
- Resource : 자원, URI로 식별할 수 있는 모든 것(제한 없음)
- Identifier : 다른 항목과 구분하는데 필요한 정보

- `URL` - locator : 리소스가 있는 위치를 지정
- `URN` - Name : 리소스에 이름을 부여
- 위치는 변할 수 있지만, 이름은 변하지 않는다
- URI == URL 같은 의미라고 볼 수 있다

<br>

## 🔹 URL 문법 분석

`scheme://[userinfo@]host[:port][/path][?query][#fragment]`

`https://www.google.com/search?q=hello&hl=ko`

- 프로토콜 : https
- 호스트명 : www.google.com
- 포트번호 : 443
- 패스 : /search
- 쿼리 파라미터 : q=hello&hl=ko

<br>

### 🔸 scheme

- 주로 프로토콜 사용
- 프로토콜 : 어떤 방식으로 자원에 접근할 것인가 하는 약속 규칙
- http → 80, https → 443, 포트는 생략 가능
- https는 http에 보안 추가

<br>

### 🔸 userinfo

- 거의 사용하지 않는것으로 URL에 사용자 정보를 포함해서 인증할 때 사용한다

<br>

### 🔸 host

- 호스트명
- 도메인명 또는 IP주소를 직접 사용

<br>

### 🔸 path

- 리소스 경로로 계층적 구조를 갖는다
- /home/file.jpg

<br>

### 🔸 query

- key=value 형태
- ?로 시작, &로 추가 가능 → ?keyA=valueA&keyB=valueB
- query parameter, query string으로 불린다

<br>

### 🔸 fragment

- html 내부 북마크 등에 사용
- 서버에 전송하는 정보 아님

<br>

# ✅ 웹 브라우저 요청 흐름

![](/images/url/url1.png)

[https://velog.io/@dnstlr2933/HTTP-웹-기본학습#uri와-웹-브라우저-요청-흐름](https://velog.io/@dnstlr2933/HTTP-%EC%9B%B9-%EA%B8%B0%EB%B3%B8%ED%95%99%EC%8A%B5#uri%EC%99%80-%EC%9B%B9-%EB%B8%8C%EB%9D%BC%EC%9A%B0%EC%A0%80-%EC%9A%94%EC%B2%AD-%ED%9D%90%EB%A6%84)

- 웹에 위와 같은 URL을 입력하게 되면 `HTTP 요청 메시지`가 생성된다

```markdown
GET/search?q=hello&hl=ko HTTP/1.1
Host: www.google.com
```

<br>

### 🔸 HTTP 메시지 전송

![](/images/url/url2.png)

생성된 패킷의 모습

![](/images/url/url3.png)

과정은

![](/images/url/url4.png)

TCP/IP패킷에 전송 데이터로 http 메시지가 들어간 모습이다

이 패킷이 인터넷 망을 돌다가 원하는 IP주소에 도착하게 되면 해당 **서버는 요청 패킷을 받아서 TCP/IP패킷은 벗겨버리고 전송 데이터인 HTTP메시지를 확인**하게 된다

- http메시지를 확인한 서버는 `HTTP 응답 메시지`를 다시 클라이언트에게 전달하게 된다

```markdown
HTTP/1.1 200 OK
Content-Type: text/html;charset=UTF-8
Content-Length: 3423

<html>
  <boldy>...</body>
</html>
```

<br>

요청 패킷을 받은 구글서버는 위와 같은 **http 응답 메시지**를 만들고

다시 **TCP/IP 패킷을 씌워서** `응답패킷`을 인터넷 망에 올려서 전달해준다

최종적으로 요청패킷을 보냈던 웹브라우저(클라이언트)는 응답 패킷을 받고 해당 패킷의 HTTP 메시지를 열어서

HTTP 메시지 안에 들어있는 html 내용물을 웹 브라우저 상에 띄어서 보게 된다
