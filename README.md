## hexo

https://parkgeonwoong.github.io/

```shell
# hexo 로컬 서버
hexo s

# 배포
hexo clean
hexo d -g

# 다른 레포지토리 - 백업
git add .
git commit -m '메세지'
git push origin master

# 새 페이지, 포스트
hexo new [layout] <title>
layout: post, page, draft

# 카테고리
---
title: Test
date: 2022-01-12 17:08:41
tags:
categories:
   - Test
   - test (이게 하위로 들어간다)
---

# post 안에 목차
---
...
toc: true
---

# post 내용 일정 부분 숨기기
post 안에
<!-- more -- >

# 이미지 경로
1. 이미지 파일은 source/images에 업로드 후
2. ![](/images/http.PNG) 같이 사용
```

<br>

```markdown
# 백업

\_config.yml
source,
\_config.icarus.yml

# git clone 이후

1. git clone 레포지토리
2. npm i 으로 dependencies 가져오기
3. icarus 테마가 없기에 테마 설치
4. hexo d -g 으로 보여줄 public 생성
5. icarus 테마 수정
```

### 1. hexo 설치

https://hexo.io/ko/index.html

```markdown
npm install hexo-cli -g

npm install hexo-cli -g
hexo init blog
cd blog
npm install
hexo server
```

### 2. 테마 안에 icarus를 설치

https://ppoffice.github.io/hexo-theme-icarus/uncategorized/getting-started-with-icarus/

```markdown
git clone https://github.com/ppoffice/hexo-theme-icarus.git themes/icarus

\_config.yml
theme: icarus
```

### 3. icarus 테마 수정

- 레이아웃 변경하기

- `node_modules/hexo-theme-icarus/layout/common/widgets.jsx`

```jsx
function getColumnSizeClass(columnCount) {
  switch (columnCount) {
    case 2:
      return "is-3-tablet is-3-desktop is-3-widescreen";
    case 3:
      return "is-2.5-tablet is-2.5-desktop is-2.5-widescreen";
  }
  return "";
}
```

- `node_modules/hexo-theme-icarus/layout/layout.jsx`

```jsx
"order-2": true,
                    "column-main": true,
                    "is-12": columnCount === 1,
                    "is-8-tablet is-8-desktop is-8-widescreen":
                      columnCount === 2,
                    "is-9-tablet is-9-desktop is-7-widescreen":
                      columnCount === 3,
```

- `node_modules\hexo-theme-icarus\include\style\base.styl`

```jsx
$gap ?= 16px
$tablet ?= 769px
$desktop ?= 1288px
$widescreen ?= 1480px
$fullhd ?= 1672px
```
