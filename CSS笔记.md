# CSS笔记

#### 格式

```css
h1
{
    color:orange;
    text-align:center;
}
```

#### 注释

```css
/*这是个注释*/
```

#### id选择器

```
#para1
{
    text-align:center;
    color:red;
}
```

#### class选择权

```
.center {text-align:center;}
# 指定p元素使用class="center"
p.center {text-align:center;}
```

#### 样式表-3种导入方式

**外部样式表**

```html
<head>
<link rel="stylesheet" type="text/css" href="mystyle.css">
</head>
```

**内部样式表**

```html
<head>
<style>
hr {color:sienna;}
p {margin-left:20px;}
body {background-image:url("images/back40.gif");}
</style>
</head>
```

**内联样式**

```
<p style="color:sienna;margin-left:20px">这是一个段落。</p>
```

## 常用样式

- 背景 -- 可以定义颜色，图片
- 文本 -- 颜色、对齐、修饰等
- 字体 -- 字体、大小、粗细等
- 链接 -- 点击等
- 边框样式 -- 上下左右可以分别设置
- 轮廓 -- 不占位置

## 盒子模型

 <img src="/Users/zhou/Library/Application Support/typora-user-images/image-20201006132106262.png" alt="image-20201006132106262" style="zoom:50%;" />

**例子：**

```
div {
    width: 300px;
    border: 25px solid green;
    padding: 25px;
    margin: 25px;
}
```

### 分组和嵌套

- 分组：每个选择器用逗号分隔
- 嵌套：空格隔开

### 元素显示和隐藏

```css
visibility:hidden;  /* 隐藏，占位 */
display:none;  /* 隐藏，不占位 */
display:inline;  /* 内联元素 */
display:block;  /* 块元素 */
```

### 定位

```css
/* top, bottom, left, right */
position: static; /* 静态定位的元素不会受到 top, bottom, left, right影响。 */
position:fixed;  /* 元素的位置相对于浏览器窗口是固定位置。 */
position:relative;  /* 相对定位元素的定位是相对其正常位置。*/
position:absolute;  /* absolute 定位使元素的位置与文档流无关，因此不占据空间。*/
position: sticky;  /* 粘性定位 */
z-index:-1; /* z-index属性指定了一个元素的堆叠顺序（哪个元素应该放在前面，或后面）*/
```

# 常用属性

- overflow 属性用于控制内容溢出元素框时显示的方式
- 浮动 float
- 对齐 margin: auto;
- 图片透明 opacity:1.0;

### 伪类

```
a:link {color:#000000;}      /* 未访问链接*/
a:visited {color:#00FF00;}  /* 已访问链接 */
a:hover {color:#FF00FF;}  /* 鼠标移动到链接上 */
a:active {color:#0000FF;}  /* 鼠标点击时 */
```

# CSS3规范

- 边框

  ```
  border-radius:10px; 圆角
  box-shadow: 10px 10px 5px #888888;  阴影
  border-image:url(border.png) 30 30 round;  边界图片
  ```

- 背景、渐变、文本效果、字体
- 2D和3D
- 过渡、动画等