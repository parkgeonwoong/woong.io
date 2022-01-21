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
```

<br>

```markdown
# 백업

\_config.yml
source,
\_config.icarus.yml
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
