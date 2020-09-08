---
title: Github-pages-404
date: 2020-01-07 14:59:05
tags:
- GitHub
categories:
- GitHub
---

#### GitHub-pages

有时候会出现404，无法访问

##### 情况一：

```
Jekyll theme，没有选择主题
```

##### 解决办法：

```
在页面存储库根目录中创建一个.nojekyll文件并将其推送到GitHub，
这样可以完全绕过GitHub Pages上的Jekyll处理
```

##### 情况二：

```
username.github.io
# 你的username弄错了
```

##### 解决办法：

```
去settings里面修改Repository name
```

