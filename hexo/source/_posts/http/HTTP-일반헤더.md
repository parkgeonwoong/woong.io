---
title: 7. HTTP 일반헤더
date: 2022-02-08 14:03:35
tags:
toc: true
categories:
  - http
---

# HTTP 헤더 - 일반 헤더

- [HTTP 헤더 - 일반 헤더](#http-헤더---일반-헤더)
    - [🔸 용도](#-용도)
  - [🔹 헤더 분류 (과거) - RFC2616](#-헤더-분류-과거---rfc2616)
    - [🔸 HTTP BODY](#-http-body)
  - [🔹 RFC723x 변화](#-rfc723x-변화)
    - [🔸 HTTP BODY](#-http-body-1)
- [✅ 표현](#-표현)
    - [🔸 Content-Type](#-content-type)
    - [🔸 Content-Encoding](#-content-encoding)
    - [🔸 Content-Language](#-content-language)
    - [🔸 Content-Length](#-content-length)
- [✅ 협상 (콘텐츠 네고시에이션)](#-협상-콘텐츠-네고시에이션)
    - [🔸 예시](#-예시)
    - [🔸 협상과 우선순위1](#-협상과-우선순위1)
    - [🔸 협상과 우선순위2](#-협상과-우선순위2)
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

<br>

참고: [https://velog.io/@dnstlr2933/HTTP-헤더-일반헤더](https://velog.io/@dnstlr2933/HTTP-%ED%97%A4%EB%8D%94-%EC%9D%BC%EB%B0%98%ED%97%A4%EB%8D%94)

<!-- more -->

<br>

### 🔸 용도

- HTTP 전송에 필요한 **모든 부가정보**가 들어간다
  - 메시지 바디의 내용, 메시지 바디의 크기, 압축, 인증, 요청 클라이언트, 서버 정보, 캐시관리 정보 등등...
- 표준 헤더가 매우 많다
- 필요 시 임의의 헤더를 추가할 수 있다
  - helloworld: hihi

<br>

## 🔹 헤더 분류 (과거) - RFC2616

![](/images/httpheader/Untitled.png)

- General 헤더 : 메시지 전체에 적용되는 정보
  - 예) Connection: close
- Request 헤더 : 요청정보
  - 예) 웹브라우저가 무엇인지
  - User-Agent: Mazilla/5.0 (Macintosh; .. )
- Response 헤더 : 응답 정보
  - 예) 요청을 처리하는 서버가 무엇인지
  - Server: Apache
- Entity 헤더 : 엔티티 바디 정보
  - 예) 메시지 바디의 타입 및 길이
  - Content-Type: text/html, Content-Length: 3423

<br>

### 🔸 HTTP BODY

![](/images/httpheader/Untitled1.png)

- 메시지 본문(msg body)은 엔티티 본문(entity body)을 전달하는데 사용한다
- 엔티티 본문은 요청이나 응답에서 **전달할 실제 데이터**
- 엔티티 헤더는 **엔티티 바디의 데이터를 해석할 수 있는 정보를 제공**한다

  - 데이터의 유형(html, json), 데이터의 길이, 압축 정보 등

- RFC2616 폐기 → RFC7230 등장

<br>

## 🔹 RFC723x 변화

- 엔티티(Entity) → 표현 (Representation)
- 표현 = representation Metadata + representation Data
- 표현 = 표현 메타데이터 + 표현 데이터

<br>

### 🔸 HTTP BODY

![](/images/httpheader/Untitled2.png)

- 메시지 본문(msg body)을 통해서 표현(Representation) 데이타 전달
- 메시지 본문 == 페이로드 (payload)
- 데이터를 실어나르는 데이타 부분을 페이로드라 한다
- **표현**은 **요청이나 응답에서 전달할 실제 데이터**
- **표현 헤더**는 **표현 데이터를 해석할 수 있는 정보를 제공**한다
  - 데이터 유형(html, json), 데이터 길이, 압축 정보 등등

참고로 표현 헤더는 표현 메타데이터와 페이로드 메시지를 구분해야한다

REST API 의 R이 표현이다

<br>

# ✅ 표현

- Content-Type : 표현 데이터의 형식
  - 의미 : 회원이라는 리소스를 html or json이라는 표현으로 전달할거야
- Content-Encoding : 표현 데이터의 압축 방식
- Content-Language : 표현 데이터의 자연 언어
  - 의미 : 이 언어가 한국어인지, 영어언지
- Content-Length : 표현 데이터의 길이
  - 자세히 따지면 표현 데이타의 길이는 표현대상과 무관한 정보로 사실 페이로드 헤더라고 구분해야 한다
- 표현헤더는 전송, 응답 둘다 사용한다

<br>

### 🔸 Content-Type

**표현 데이터의 형식 설명**

- 메시지 바디에 들어가는 데이터가 무엇인지 설명
- 미디어 타입, 문자 인코딩 등
- 예)
  - text/html; charset=utf-8
  - application/json
  - image/jpg

<br>

### 🔸 Content-Encoding

**표현 데이터 인코딩**

- **표현 데이터를 압축**하기 위해 많이 사용
- 데이터를 전달하는 곳에서 **압축 후 인코딩 헤더 추가**
- 데이터를 읽는 쪽에서 인코딩 헤더의 정보로 압축 해제
- 예)
  - gzip (압축)
  - deflate
  - identity (압축안하는것, 똑같다는뜻)

<br>

### 🔸 Content-Language

**표현 데이터의 자연언어**

- 표현 데이터의 자연 언어를 표현
  - ko, en, en-US 등등

<br>

### 🔸 Content-Length

**표현 데이터의 길이**

- 바이트 단위
- Transfer-Encoding(전송 코딩)을 사용하면 Content-Length를 사용하면 안된다
  - Transfer-Encoding안에 관련 정보들이 이미 전부 들어가있어서 추가적으로 사용하면 안된다

<br>

# ✅ 협상 (콘텐츠 네고시에이션)

- **클라이언트가 선호하는 표현 요청**
- Accept : 클라이언트가 선호하는 미디어 타입을 서버에 전달
- Accept-Charset : 클라이언트가 선호하는 문자 인코딩을 서버에 요청
- Accept-Encoding : 클라이언트가 선호하는 압축 인코딩을 서버에 요청
- Accept-Language : 클라이언트가 선호하는 자연언어를 서버에 요청

협상 헤더는 `요청`시에만 사용을 한다

→ 클라이언트가 서버에게 원하는 표현에게 달라고 요청하는 것, 서버는 원하는 데이터로 만드는 것

<br>

### 🔸 예시

![](/images/httpheader/Untitled3.png)

<br>

### 🔸 협상과 우선순위1

**Quality Values(q)**

- Quality Valuese(`q`)값을 사용한다
- 0~1 의 값을 사용하며, **클수록 높은 우선 순위**이다
- 생략하면 1
- Accept-Language: ko-KR,ko;q=0.9,en-US;q=0.8,en;q=0.7
  1. ko-KR;q=1 (뒤 부분 생략, 1로 설정된다)
  2. ko;q=0.9
  3. en-US;q=0.8
  4. en;q=0.7

![](/images/httpheader/Untitled4.png)

![](/images/httpheader/Untitled5.png)

<br>

### 🔸 협상과 우선순위2

**Quality Values(q)**

- **구체적인 것을 우선**시한다
- Accept: text/_, text/plain, text/pain;format=flowed, _/\*
  1. text/plain;format=flowed
  2. text/plain
  3. text/\*
  4. _/_

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
