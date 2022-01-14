---
title: Interactive mouse
date: 2022-01-14 21:42:16
tags:
categories:
  - Interactive
---

# 📌 Mouse를 활용한 인터렉티브

## ✅ mouse move 활용

```javascript
window.addEventListener("mousemove", function(e) {
    console.log(e.clientX, e.clientY);
}
```

- 위에 처럼 마우스 X, Y 좌표가 직접 console에 찍힌다.

<br>

```javascript
document.getElementsByClassName("className")[0];
```

- 배열로 넘어오기 때문에 첫번째 요소인 [0]을 선택해준다.

<br>

## ✅ requestAnimationFrame == loop

- loop라는 자연스럽게 움직이게 활용
- 화려한 애니메이션 & 3D 컨텐츠에 활용

```javascript
function loop() {
  console.log("계속 실행됩니다.");

  window.requestAnimationFrame(loop);
}
```

<br>

## ✅ 자연스러운 마우스 움직임

- CSS 속성을 JS에서 사용하는 방법

```javascript
item.style.transform = "translate("+ x값 + "px, " + Y값 +"px)";


CSS : item { transform : translate(100px, 100px); }
JS:  item.style.transform = "translate(100px, 100px)";
```

<br>

➡️ **마우스 자연스러운 움직이는 공식**

```javascript
mx += (x - mx) * speed;
```

- 움직일 값 += (현재 마우스 위치 - 바로 전 위치 값) \* 0.001;

> 현재 위치가 100, 마우스 현재 위치가 150이라고 치면! 100부터 50만큼 이동을 하면 되는데.  
> 한 번에 50을 더해주면 바로 착! 이동을 하니까 조금씩 작은 수를 더해주는 겁니다.
> 100 += (150 - 100) \* 0.001; 이렇게 계산 된 수를 계속 더해주는 방식.

<br>

## ✅ transition, easing (가속도)

[easing test](https://matthewlein.com/tools/ceaser)

- transition은 시간에 대한 변화량이다.
- easing은 가속도로써 변화를 줄 수 있다.

<br>

### 🔸 정리

> - 마우스의 x, y 좌표를 JS로 직접 찍어보면서 기본 개념 다루기
>
> - requestAnimationFrame을 이용하여 콜백함수로 60프레임을 > 다루어 자연스러운 animation 효과를 나타낸다.
>
> - 마우스의 자연스러운 움직임을 위해서 시간차에 따른 변화량을 > 사용 (loop = requestAnimationFrame)
>
> - CSS속성을 JS로 나타내어 필요한 부분, 세심한 부분에 CSS > 속성을 대입한다.
