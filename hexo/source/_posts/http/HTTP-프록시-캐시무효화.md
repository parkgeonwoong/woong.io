---
title: 11. HTTP-프록시 캐시무효화
date: 2022-02-17 13:57:20
tags:
toc: true
categories:
  - http
---

- [✅ 프록시 서버](#-프록시-서버)
  - [🔹 원(origin) 서버 직접 접근](#-원origin-서버-직접-접근)
  - [🔹 프록시 캐시 도입](#-프록시-캐시-도입)
    - [Cache-Control](#cache-control)
- [✅ 캐시 무효화](#-캐시-무효화)
    - [🔸 no-cache vs mush-revalidate](#-no-cache-vs-mush-revalidate)

<br>

참고 : [https://velog.io/@dnstlr2933/HTTP-헤더캐시와-조건부-요청](https://velog.io/@dnstlr2933/HTTP-%ED%97%A4%EB%8D%94%EC%BA%90%EC%8B%9C%EC%99%80-%EC%A1%B0%EA%B1%B4%EB%B6%80-%EC%9A%94%EC%B2%AD)

<!-- more -->

<br>

# ✅ 프록시 서버

## 🔹 원(origin) 서버 직접 접근

![](/images/httpCache/Untitled10.png)

- 예시로, 대략 0.5초 가량 기다려야 해당 이미지를 다운 → 더 많은 시간이 걸릴 수 있다

➡️ 이를 해결하기 위해 `프록시 캐시` 도입

## 🔹 프록시 캐시 도입

![](/images/httpCache/Untitled11.png)

### Cache-Control

- Cache-Control: `public`
  - 응답이 public 캐시에 저장되어도 된다
- Cache-Control: `private`
  - 응답이 해당 사용자만을 위한 것이다, **private 캐시에 저장**해야 한다(기본값)
- Cache-Control: `s-maxage`
  - 프록시 캐시에만 적용되는 `max-age`이다
- Age: 60 (HTTP 헤더)
  - 원 서버에서 응답 후 프록시 캐시 서버내에 머무는 시간(초)

<br>

# ✅ 캐시 무효화

**확실한 캐시 무효화 응답**

통장 잔고, 비밀번호 등 개인정보에 해당하는 정보로 절대 캐시에 보관해서는 안되는 데이터를 캐시에 보관하는 것을 막기위해 넣어야 하는 헤더이다. 충분히 넣어줘야 한다

- Cache-Control: no-cache, no-store, must-revalidate
- Pragma: no-cache
  - (HTTP 1.0 하위 호환을 위해서)

**Cache-Control: no-cache**

- 데이터는 캐시해도 되지만, **항상 원 서버에 검증**하고 사용 (이름에 주의 - 캐시를 안하는것 아니다 !)

**Cache-Control: no-store**

- 데이터에 민감한 정보가 있으므로 저장하면 안된다
- 메모리에서 사용하고 최대한 빨리 삭제
- no-cache와 함께 조합

**Cache-Control: must-revalidate**

- **캐시 만료 후 최초 조회시 원 서버에 검증**해야한다
- **원 서버에 접근 실패시 반드시 오류가 발생**해야 한다 - 504(Gateway Timeout)
- must-revalidate는 캐시유효 시간이라면 캐시를 사용한다

**Pragma: no-cache**

- HTTP/1.0 버전인 경우 Cache-Control을 모르므로 하위호환을 위해 사용

### 🔸 no-cache vs mush-revalidate

![](/images/httpCache/Untitled12.png)

- 그런데 프록시 서버에서 연결에 장애가 발생하면??

![](/images/httpCache/Untitled13.png)

- 만약 은행 잔고 데이터라면? → 이전의 잔고 데이터가 나올 수 있어 보안상 문제
- 그래서 사용하는 것 → must-revalidate

![](/images/httpCache/Untitled14.png)
