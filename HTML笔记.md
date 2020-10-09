# HTML笔记

### 一、基础概念：

- HTML：理解HTML是超文本标记语言，是使用标签(HTML tag)来描述网页
- 标签：标签是由*尖括号*包围的关键词，通常是*成对出现*，对大小写*不敏感*
- html文档等价于网页，由html标签和纯文本组成
- 元素：指的是从开始标签到结束标签的所有代码
- 属性：在开始标签中以key=value的形式存在

### 二、常用标签

- 需要熟悉常用标签，及标签的常用属性

```html
标题<h1>-<h6>
段落<p>
链接<a>
图像<img/>
换行<br/>
水平线<hr/> 
块<div>和<span>
框架<frameset>和<frame>
内联框架<iframe>
头<head>
样式<style>
脚本<script>
链接资源<link>
元数据<meta>
表单<form>
```

<!--这是一段注释。注释不会在浏览器中显示。-->

### 三、常用属性

- 属性和属性值对大小写*不敏感*
- 属性值需要加引号

- 多使用手册查属性

### 四、常用样式

- 用于改变 HTML 元素的样式
- style="background-color:red"

```html
# 使用样式的三种方法
# 方法1:外部样式表
<head>
  <link rel="stylesheet" type="text/css" href="mystyle.css">
</head>
# 方法2:内部样式表
<head>
  <style type="text/css">
    body {background-color: red}
    p {margin-left: 20px}
  </style>
</head>
# 方法3：内联样式
<p style="color: red; margin-left: 20px">
```

标签、属性、颜色、实体

### 五、RWD

- RWD 指的是响应式 Web 设计（Responsive Web Design）
- RWD 能够以可变尺寸传递网页

### 六、字符实体

```html
空格 &nbsp; 或者 &#160;
```

### 七、URL

```
scheme://host.domain:port/path/filename
```

### 八、声明

```
<!DOCTYPE html>
```

### 九、其他

- 支持在网页上绘制图形
- 网页支持SVG矢量图
- 网页支持音效、音乐、视频和动画
- 支持地理定位
- 支持拖放
- 支持本地存储
- 支持应用缓存，离线浏览

