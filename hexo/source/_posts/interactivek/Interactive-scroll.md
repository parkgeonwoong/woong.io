---
title: Interactive-scroll
date: 2022-01-15 13:32:27
tags:
toc: true
categories:
  - Interactive
---

# ๐ ์คํฌ๋กค ๊ฐ์ ํ์ฉํ ์ธํฐ๋ํฐ๋ธ

- ํจ๋ด๋์ค๋ ๋ ์ด์ด๊ฐ ์กด์ฌํด์ผ ํ๋ค. (๋ฉ์ถฐ ์๋ ๋ ์ด์ด, ์ฒ์ฒํ ์์ง์ด๋ ๋ ์ด์ด, ๋นจ๋ฆฌ ์์ง์ด๋ ๋ ์ด์ด, ์์ )

- ์คํฌ๋กค ๊ฐ์ ๋ฐ์์ค๋ ๊ฒ ๋ถํฐ ์์

`Parallax Scrolling` : ์ฌ์ฉ์๊ฐ ์คํฌ๋กคํ  ๋ ๋ฐฐ๊ฒฝ ์ด๋ฏธ์ง๊ฐ ๋๋ฆฌ๊ฒ ์์ง์ด๋ฉฐ, ๊ทผ๊ฑฐ๋ฆฌ๋ฅผ ๋นจ๋ฆฌ ์์ง์ด๋ ์ฆ ์์ฒด๊ฐ์ ๋๋ ์ ์๋ ๋์์ธ ๊ธฐ๋ฒ

- ์คํฌ๋กค์ ์์ง์ผ ๋๋ง๋ค transform์ translate, scale, opacity ๋ฑ ๋ณํ๋ฅผ ์ง์  ์ค๋ค.

<!-- more -->

<br>

- CSS ๊ทธ๋ผ๋์ธํธ ์ ์ฉ

```css
background: linear-gradient(150deg, tomato, orange, white);
```

<br>

### โ ์คํฌ๋กค ๊ฐ ๋ฐ์์ค๊ธฐ

```javascript
window.addEventListener("scroll", function (e) {
  scrollTop = document.documentElement.scrollTop;
});
```

<br>

### โ ํ๋ฉด width ๊ธธ์ด์ ์คํฌ๋กค ๋ฐ ๊ตฌํ. ๋ฐฑ๋ถ์จ ๊ตฌํ๋ ๊ณต์.

> **๊ฐ๋ก ํผ์ผํธ๊ฐ = ํ์ฌ ์คํฌ๋กค ํ ์์น / (๋ฌธ์ ์ ์ฒด ๊ธธ์ด - ์๋์ฐ ์ฐฝ ๋์ด ) \* 100;**

```javascript
per =
  Math.round(
    scrollTop / (document.documentElement.scrollHeight - window.innerHeight)
  ) * 100;
```

<br>

### โ scrollTop ํจ๋ด๋ ์ค ๊ตฌํ

```javascript
window.addEventListener("scroll", function (e) {
  scrollTop = document.documentElement.scrollTop;
  let per = Math.ceil(
    (scrollTop / (document.body.scrollHeight - window.outerHeight)) * 100
  );

  bar.style.height = per + "%";

  cloudWrap.style.transform = "translate(0," + scrollTop / 1.2 + "px)";
});
```

- (์๋์ฐ ๊ธฐ์ค) ์คํฌ๋กค ํ ๋ฒ์ 100ํฝ์์ฉ ์ด๋

- ๋ชจ๋๊ฐ 100์ฉ ์ด๋ํ ๋ ์ง์ ํ ์ค๋ธ์ ํธ๋ง 100 / 1.2 = 83.3 ์ฉ ์ด๋์ ํ๊ฒ ๋์ด ๋๋ฆฌ๊ฒ ์์ง์ด๋ ๋๋

- ๋ฐ๋๋ก 100 \* .8 ๋ก ํด๋ ๋น์ทํ ๊ฒฐ๊ณผ
