---
title: Interactive mouse
date: 2022-01-14 21:42:16
tags:
toc: true
categories:
  - Interactive
---

# ๐ Mouse๋ฅผ ํ์ฉํ ์ธํฐ๋ ํฐ๋ธ

## โ mouse move ํ์ฉ

```javascript
window.addEventListener("mousemove", function(e) {
    console.log(e.clientX, e.clientY);
}
```

- ์์ ์ฒ๋ผ ๋ง์ฐ์ค X, Y ์ขํ๊ฐ ์ง์  console์ ์ฐํ๋ค.

<!-- more -->

<br>

```javascript
document.getElementsByClassName("className")[0];
```

- ๋ฐฐ์ด๋ก ๋์ด์ค๊ธฐ ๋๋ฌธ์ ์ฒซ๋ฒ์งธ ์์์ธ [0]์ ์ ํํด์ค๋ค.

<br>

## โ requestAnimationFrame == loop

- loop๋ผ๋ ์์ฐ์ค๋ฝ๊ฒ ์์ง์ด๊ฒ ํ์ฉ
- ํ๋ คํ ์ ๋๋ฉ์ด์ & 3D ์ปจํ์ธ ์ ํ์ฉ

```javascript
function loop() {
  console.log("๊ณ์ ์คํ๋ฉ๋๋ค.");

  window.requestAnimationFrame(loop);
}
```

<br>

## โ ์์ฐ์ค๋ฌ์ด ๋ง์ฐ์ค ์์ง์

- CSS ์์ฑ์ JS์์ ์ฌ์ฉํ๋ ๋ฐฉ๋ฒ

```javascript
item.style.transform = "translate("+ x๊ฐ + "px, " + Y๊ฐ +"px)";


CSS : item { transform : translate(100px, 100px); }
JS:  item.style.transform = "translate(100px, 100px)";
```

<br>

โก๏ธ **๋ง์ฐ์ค ์์ฐ์ค๋ฌ์ด ์์ง์ด๋ ๊ณต์**

```javascript
mx += (x - mx) * speed;
```

- ์์ง์ผ ๊ฐ += (ํ์ฌ ๋ง์ฐ์ค ์์น - ๋ฐ๋ก ์  ์์น ๊ฐ) \* 0.001;

> ํ์ฌ ์์น๊ฐ 100, ๋ง์ฐ์ค ํ์ฌ ์์น๊ฐ 150์ด๋ผ๊ณ  ์น๋ฉด! 100๋ถํฐ 50๋งํผ ์ด๋์ ํ๋ฉด ๋๋๋ฐ.  
> ํ ๋ฒ์ 50์ ๋ํด์ฃผ๋ฉด ๋ฐ๋ก ์ฐฉ! ์ด๋์ ํ๋๊น ์กฐ๊ธ์ฉ ์์ ์๋ฅผ ๋ํด์ฃผ๋ ๊ฒ๋๋ค.
> 100 += (150 - 100) \* 0.001; ์ด๋ ๊ฒ ๊ณ์ฐ ๋ ์๋ฅผ ๊ณ์ ๋ํด์ฃผ๋ ๋ฐฉ์.

<br>

## โ transition, easing (๊ฐ์๋)

[easing test](https://matthewlein.com/tools/ceaser)

- transition์ ์๊ฐ์ ๋ํ ๋ณํ๋์ด๋ค.
- easing์ ๊ฐ์๋๋ก์จ ๋ณํ๋ฅผ ์ค ์ ์๋ค.

<br>

### ๐ธ ์ ๋ฆฌ

> - ๋ง์ฐ์ค์ x, y ์ขํ๋ฅผ JS๋ก ์ง์  ์ฐ์ด๋ณด๋ฉด์ ๊ธฐ๋ณธ ๊ฐ๋ ๋ค๋ฃจ๊ธฐ
>
> - requestAnimationFrame์ ์ด์ฉํ์ฌ ์ฝ๋ฐฑํจ์๋ก 60ํ๋ ์์ > ๋ค๋ฃจ์ด ์์ฐ์ค๋ฌ์ด animation ํจ๊ณผ๋ฅผ ๋ํ๋ธ๋ค.
>
> - ๋ง์ฐ์ค์ ์์ฐ์ค๋ฌ์ด ์์ง์์ ์ํด์ ์๊ฐ์ฐจ์ ๋ฐ๋ฅธ ๋ณํ๋์ > ์ฌ์ฉ (loop = requestAnimationFrame)
>
> - CSS์์ฑ์ JS๋ก ๋ํ๋ด์ด ํ์ํ ๋ถ๋ถ, ์ธ์ฌํ ๋ถ๋ถ์ CSS > ์์ฑ์ ๋์ํ๋ค.
