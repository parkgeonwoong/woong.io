---
title: Interactive-addition
date: 2022-01-15 13:37:58
tags:
categories:
  - Interactive
---

## ✅ 인터랙티브 교차 페이징

- 사진 여러개를 position fixed로 겹쳐서 JS에 의해 사진이 달라지는 교차페이지

```javascript
//선택된 컨텐츠랩 활성
contentWrap[pageNum].classList.add("active");
for (var i = 0; i < 4; i++) {
  //활성된 컨텐츠랩 내부 이미지들 활성
  contentWrap[pageNum].getElementsByTagName("img")[i].classList.add("active");
}
```

<br>

## ✅ translateZ 활용한 입체적인 페이지

- translateZ : 앞 뒤로 움직여서 입체감을 높여준다
- perspective : 깊이감을 준다. 적으면 변화가 빠르고, 높으면 변화가 천천히

<br>

```javascript
let scrollTop = 0;
let imageAll;
let totalNum = 0;

window.onload = function () {
  progressBar = document.getElementsByClassName("progressBar")[0];
  imageAll = document.querySelectorAll(".parallax_image");

  totalNum = imageAll.length;

  window.addEventListener("scroll", scrollFunc);
};

function scrollFunc(e) {
  scrollTop = this.scrollY;

  for (var i = 0; i < totalNum; i++) {
    imageAll[i].style.transform =
      "perspective(400px) translateZ(" +
      scrollTop / (5 * (totalNum - i)) +
      "px)";
    // imageAll[i].style.transform = "perspective(400px) translateZ("+ scrollTop/5 +"px)"; 동시에 움직여 입체감이 없다
  }
}
```
