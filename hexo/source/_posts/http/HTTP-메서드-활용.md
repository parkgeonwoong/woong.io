---
title: HTTP 메서드 활용
date: 2022-02-03 13:21:17
tags:
toc: true
categories:
  - http
---

# 📌 HTTP 메서드 활용

- [📌 HTTP 메서드 활용](#-http-메서드-활용)
- [✅ 클라이언트에서 서버로 데이터 전송](#-클라이언트에서-서버로-데이터-전송)
  - [🔹 클라이언트에서 서버로 데이터를 전송하는 4가지 상황](#-클라이언트에서-서버로-데이터를-전송하는-4가지-상황)
    - [1. 정적 데이터 조회](#1-정적-데이터-조회)
    - [2. 동적 데이터 조회](#2-동적-데이터-조회)
    - [3. HTML Form 데이터 전송](#3-html-form-데이터-전송)
    - [4. HTTP API 데이터 전송](#4-http-api-데이터-전송)
- [✅ HTTP API 설계 예시](#-http-api-설계-예시)
  - [🔹 API 설계 - POST 기반 등록](#-api-설계---post-기반-등록)
    - [🔸 POST - 신규 자원 등록 특징](#-post---신규-자원-등록-특징)
  - [🔹 API 설계 - PUT 기반 등록](#-api-설계---put-기반-등록)
    - [🔸 PUT - 신규 자원 등록 특징](#-put---신규-자원-등록-특징)
  - [🔹 HTML FORM 사용](#-html-form-사용)
  - [🔹 참고하면 좋은 URI 설계 개념](#-참고하면-좋은-uri-설계-개념)

참고: [https://velog.io/@dnstlr2933/HTTP-Method](https://velog.io/@dnstlr2933/HTTP-Method)

<br>

<!-- more -->

# ✅ 클라이언트에서 서버로 데이터 전송

데이터 전달 방식은 크게 2가지가 있다

- **쿼리 파라미터를 통한 데이터 전송**
  - GET
  - 주로 정렬 필터 (검색어)
- **메시지 바디를 통한 데이터 전송**
  - POST, PUT, PATCH
  - 회원 가입, 상품 주문, 리소스 등록, 리소스 변경

<br>

## 🔹 클라이언트에서 서버로 데이터를 전송하는 4가지 상황

### 1. 정적 데이터 조회

- 이미지, 정적 텍스트 문서
- 조회는 GET 사용
- 정적 데이터는 일반적으로 쿼리 파라미터 없이 리소스 경로로 단순하게 조회 가능

### 2. 동적 데이터 조회

- 주로 검색, 게시판 목록에서 정렬 필터 (검색어)
- 조회 조건을 줄여주는 필터, 조회 결과를 정렬하는 정렬 조건에 주로 사용
- 조회는 GET 사용
- GET은 쿼리 파라미터 사용해서 데이터를 전달

![](/images/httpmethod2/Untitled.png)

[https://catsbi.oopy.io/e43388ef-bc41-4f44-986c-010c12b596dd](https://catsbi.oopy.io/e43388ef-bc41-4f44-986c-010c12b596dd)

### 3. HTML Form 데이터 전송

- POST 전송 - 저장

![](/images/httpmethod2/Untitled1.png)

- 이렇게 클라에서 만들고 전송 버튼을 누르면 웹 브라우저가 `HTTP 요청 메시지`를 생성

- GET 전송 - 조회

![](/images/httpmethod2/Untitled2.png)

- 파일이나 이미지 같은 자료는 어떻게 전송되는가?

![](/images/httpmethod2/Untitled3.png)

- multipart/form-data 는 말 그대로 input에 type들을 여러 개 쓸 때 사용한다
- boundary(`---XXX`)를 통해 username, age, file등을 구분 해서 보낸다
- 파일 업로드 같은 바이너리 데이터 전송시 사용

```markdown
# HTML Form 데이터 전송 정리

HTML Form submit시 POST 전송
예) 회원가입, 상품주문, 댓글, 데이터 변경 등

Content-Type : application/x-www-form-urlencoded 사용 - form의 내용을 메시지 바디를 통해서 전송 (key=value, 쿼리 파라미터 형식) - 전송 데이터를 url endcoding 처리
예) abc김 -> abc%EA%9B%80

HTML From은 GET 전송도 가능하다

Content-Type : multipart/form-data - 파일 업로드 같은 바이너리 데이터 전송시 사용한다 - 다른 종류의 여러 파일과 폼의 내용을 함께 전송 할 수 있다 (그래서 multipart)

**HTML Form 전송은 GET, POST만 지원한다**
```

<br>

### 4. HTTP API 데이터 전송

![](/images/httpmethod2/Untitled4.png)

- 바로 데이터를 위와 같은 형식으로 만들어서 데이터를 전달하면 된다

- 서버 to 서버
  - 백엔드 시스템 통신
- 앱 클라이언트
  - 아이폰, 안드로이드
- 웹 클라이언트
  - HTML에서 Form 전송 대신 JS 통한 통신에 사용 (AJAX)
  - 예) React, Vue 같은 웹 클라이언트와 API 통신
- POST, PUT, PATCH : 메시지 바디를 통해 데이터 전송
- GET : 조회, 쿼리 파라미터로 데이터 전달
- Content-Type: application/json을 주로 사용
  - Text, XML, JSON 등등

<br>

# ✅ HTTP API 설계 예시

회원 관리를 예시로 API를 다양한 방법으로 설계해보자

- HTTP API → 컬렉션
  - POST 기반 등록
  - 예) 회원 관리 API 제공
- HTTP API → 스토어
  - PUT 기반 등록
  - 예) 정적 컨텐츠 관리, 원격 파일 관리
- HTML FORM 사용
  - 웹 페이지 회원 관리
  - GET, POST만 지원

<br>

## 🔹 API 설계 - POST 기반 등록

- **회원 목록 /members → GET**
  - 회원 정렬조건이나 검색 조건이 필요하면 쿼리 파라미터를 설계하면 된다.
- **회원 등록 /members → POST**
- **회원 조회 /members/{id} → GET**
  - 계층적 구조로 되어있어 컬렉션 안의 특정 아이디를 조회한다고 볼 수 있어 가독성도 높다.
- **회원 수정 /members/{id} → PATCH, PUT, POST**
  - PUT은 덮어쓰기고 PATCH는 부분적 업데이트이기에 회원 정보 수정은 PATCH가 좋다.
  - 하지만, 수정이 전부 다 변경해줘야 하는 경우(ex: 게시판 글 수정하기)에는 PUT을 쓰는게 좋을 수도 있다.
- **회원 삭제 /members/{id} → DELETE**

<br>

### 🔸 POST - 신규 자원 등록 특징

- **클라이언트는 등록될 리소스의 URI를 모른다.**

  - _회원 등록 /members → POST_
  - _POST /members_

- **서버가 새로 등록된 리소스 URI를 생성해준다.**

  - HTTP/1.1 201 Created
    Location: `/members/100`

- **컬렉션(Collection)**
  - _서버가 관리하는 리소스 디렉토리_
  - _서버가 리소스의 URI를 생성하고 관리_
  - _여기서 컬렉션은 /members_

<br>

## 🔹 API 설계 - PUT 기반 등록

- 파일 목록 /files → GET
- 파일 조회 /files/{filename} → GET
- 파일 등록 /files/{filename} → PUT
- 파일 삭제 /files/{filename} → DELETE
- 파일 대량 등록 /files → POST
  - POST는 상황에 맞게 쓸 수 있다. 이번 경우에는 대량 등록을 위해 사용

<br>

### 🔸 PUT - 신규 자원 등록 특징

등록을 위해 POST 대신 → PUT을 사용. 어떤 차이점???

- **클라이언트가 리소스 URI를 알고 있어야 한다**
  - 파일 등록 /files/{filename} -> PUT
  - PUT /files/start.jpg
- **클라이언트가 직접 리소스의 URI를 지정한다**
- **스토어(store)**
  - 클라이언트가 관리하는 리소스 저장소
  - 클라이언트가 리소스의 URI를 알고 관리한다
  - 여기서 스토어는 **/files**

<br>

## 🔹 HTML FORM 사용

- HTML FORM은 GET, POST만 지원한다
- AJAX 같은 기술을 사용해서 해결 가능하다 → 회원 API 참고
- 순수 HTML + HTML FORM은 **GET, POST만 지원**하므로 제약이 있다

- 회원 목록 /members → **GET**
- 회원 등록 폼 /members/**new** → **GET**
- 회원 등록 /members/**new**, /members → **POST**
- 회원 조회 /members/{id} → **GET**
- 회원 수정 폼 /members/{id}/**edit** → **GET**
- 회원 수정 /members/{id}/**edit**, /members/{id} → **POST**
- 회원 삭제 /members/{id}/**delete** → **POST**

- **컨트롤 URI**
  - GET, POST만 지원하므로 제약이 있다
  - 이런 제약을 해결하기 위해 `동사로 된 리소스 경로`를 사용한다
  - 위에서는 POST의 /new, /edit, /delete가 컨트롤 URI이다
  - HTTP 메서드로 해결하기 애매한 경우 사용한다 (HTTP API 포함)

<br>

## 🔹 참고하면 좋은 URI 설계 개념

- **문서 (document)**
  - 단일 개념(파일하나, 객체 인스턴스, 데이터베이스 row)
  - 예) /members/100, /files/start.jpg
- **컬렉션 (Collection)**
  - 서버가 관리하는 리소스 디렉터리
  - 서버가 리소스를 생성하고 관리한다
  - 예) /members
- **스토어 (Store)**
  - 클라이언트가 관리하는 자원 저장소
  - 클라이언트가 리소스의 URI를 알고 관리한다
  - 서버에 등록할 때 URI를 지정해서 전달한다
  - 예) /files
- **컨트롤러 (Controller), 컨트롤 URI**
  - 문서, 컬렉션, 스토어로 해결하기 어려운 추가 프로세스를 실행한다
  - 동사를 직접 사용한다
  - 예) members/{id}/delete

[https://restfulapi.net/resource-naming/](https://restfulapi.net/resource-naming/)
