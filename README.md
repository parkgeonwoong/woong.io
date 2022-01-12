## hexo

https://parkgeonwoong.github.io/

```shell
hexo s
hexo deploy

hexo clean
hexo d -g

git add .
git commit -m '메세지'
git push origin master
```

<br>

```markdown
# 백업

\_config.yml
source,
\_config.icarus.yml
```

1. hexo 설치

   https://hexo.io/ko/index.html

   ```markdown
   npm install hexo-cli -g

   npm install hexo-cli -g
   hexo init blog
   cd blog
   npm install
   hexo server
   ```

2. 테마 안에 icarus를 설치

   https://ppoffice.github.io/hexo-theme-icarus/uncategorized/getting-started-with-icarus/

   ```markdown
   git clone https://github.com/ppoffice/hexo-theme-icarus.git themes/icarus

   \_config.yml
   theme: icarus
   ```
