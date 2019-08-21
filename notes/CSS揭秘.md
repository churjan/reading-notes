# CSS揭秘

|基本信息||
|:-|:-|
|图书名称|CSS揭秘 |
|外文书名|CSS Secret Better Solutions to Everyday Web Design Problems|
|作者|[希]Lea Verou 著 CSS魔法 译|
|出版社|人民邮电出版社|
|出版日期|2016年04月01日|

## 第2章 背景与边框

### 1 半透明边框

![](/images/semi-transparent-borders.png)

```css
border: 10px solid hsla(0,0%,100%,.5);
background: white;
background-clip: padding-box;  /*默认值是border-box,背景会延伸到边框所在的区域下层。/
```

### 2 多重边框

![](/images/mutiple-borders.png)

box-shadow方案

```css
background: yellowgreen;
/*box-shadow 是层层叠加的，第一层投影位于最顶
层，依次类推*/
box-shadow: 0 0 0 10px #655,
            0 0 0 15px deeppink,
            0 2px 5px 15px rgba(0,0,0,.6);
```

outline方案（它只适用于双层“边框”的场景）

```css
background: yellowgreen;
border: 10px solid #655;
outline: 5px solid deeppink;
```

### 3 灵活的背景定位

![](/images/extended-bg-position.png)

background-position 的扩展语法方案

```css
padding: 10px;
background: url(code-pirate.svg) no-repeat #58a;
background-position: right 10px bottom 10px;
```

background-origin 方案

```css
padding: 10px;
background: url(code-pirate.svg) no-repeat #58a;
background-position: right 10px bottom 10px;
```

calc() 方案

```css
background: url("code-pirate.svg") no-repeat;
background-position: calc(100% - 20px) calc(100% - 10px);
```

### 4 边框内圆角

![](/images/inner-border.png)

描边并不会跟着元素的圆角走,但 box-shadow 却是会的

```css
background: tan;
border-radius: .8em;
padding: 1em;
box-shadow: 0 0 0 .6em #655;
outline: .6em solid #655;
```

### 5 条纹背景

水平条纹

![](/images/horizontal-stripes.png)

```css
background: linear-gradient(#fb3 50%, #58a 0);/*默认to bottom 角度顺时针增加*/
background-size: 100% 30px;
```

垂直条纹

![](/images/vertical-stripes.png)

```css
background: linear-gradient(to right, #fb3 50%, #58a 0);/*或90deg*/
background-size: 30px 100%;
```

斜向条纹

![](/images/diagonal-stripes.png)

每条条纹长度为15px

```css
background: linear-gradient(45deg,
  #fb3 25%, #58a 0, #58a 50%,
  #fb3 0, #fb3 75%, #58a 0);
background-size: 42.426406871px 42.426406871px;
```

更好的斜向条纹


```css
background: repeating-linear-gradient(45deg,
  #fb3, #fb3 15px, #58a 0, #58a 30px);
```

灵活的同色系条纹

![](/images/subtle-stripes.png)

```css
background: #58a;
background-image: repeating-linear-gradient(30deg, 
              hsla(0,0%,100%,.1), hsla(0,0%,100%,.1) 15px,
              transparent 0, transparent 30px);
height: 100vh;
```

### 6 复杂的背景图案

网格

![](/images/blueprint.png)

```css
background: #58a;
background-image: linear-gradient(white 2px, transparent 0),
                  linear-gradient(90deg, white 2px, transparent 0),
                  linear-gradient(hsla(0,0%,100%,.3) 1px, transparent 0),
                  linear-gradient(90deg, hsla(0,0%,100%,.3) 1px, transparent 0);
background-size: 50px 50px, 50px 50px,
                 10px 10px, 10px 10px;
```

波点

![](/images/polka.png)

```css
background: #655;
background-image: radial-gradient(tan 20%, transparent 0),
                  radial-gradient(tan 20%, transparent 0);
background-size: 30px 30px;
background-position: 0 0, 15px 15px;
```

棋盘

![](/images/checkerboard.png)

```css
background: #eee;
background-image: 
	linear-gradient(45deg, rgba(0,0,0,.25) 25%, transparent 0, transparent 75%, rgba(0,0,0,.25) 0),
	linear-gradient(45deg, rgba(0,0,0,.25) 25%, transparent 0, transparent 75%, rgba(0,0,0,.25) 0);
background-position: 0 0, 15px 15px;
background-size: 30px 30px;
min-height: 100%;
```

## 第3章 形状

### 9 自适应的椭圆

![](/images/ellipse.png)

```css
border-radius:50%;
```

半圆

![](/images/half-ellipse.png)

```css
div {
	display: inline-block;
	width: 16em;
	height: 10em;
	margin: 1em;
	background: #fb3;
	border-radius: 50% / 100% 100% 0 0;
}

div:nth-of-type(2) { border-radius: 50% / 0 0 100% 100%; }
div:nth-of-type(3) { border-radius: 100% 0 0 100% / 50%; }
div:nth-of-type(4) { border-radius: 0 100% 100% 0 / 50%; }
```

四分之一圆

![](/images/quarter-ellipse.png)

```css
border-radius: 100% 0 0 0;
```

### 10 平行四边形

![](/images/parallelograms.png)

嵌套元素方案

```html
<a href="#yolo" class="button">
<div>Click me</div>
</a>
```

```css
.button { transform: skewX(-45deg); }
.button > div { transform: skewX(45deg); }
```

伪元素方案

```css
.button {
  position: relative;
  /* 其他的文字颜色、内边距等样式…… */
}
.button::before {
  content: ''; /* 用伪元素来生成一个矩形 */
  position: absolute;
  top: 0; right: 0; bottom: 0; left: 0;
  z-index: -1;
  background: #58a;
  transform: skew(45deg);
}
```

### 11 菱形图片

![](/images/diamond-images.png)

基于变形的方案

```css
.picture {
  width: 400px;
  transform: rotate(45deg);
  overflow: hidden; }
.picture > img {
  max-width: 100%;
  transform: rotate(-45deg) scale(1.42);
}
```

裁切路径方案

```css
img {
  clip-path: polygon(50% 0, 100% 50%,50% 100%, 0 50%);
  transition: 1s clip-path; }
img:hover {
  clip-path: polygon(0 0, 100% 0, 100% 100%, 0 100%);
}
```

### 12 切角效果

![](/images/bevel-corners-gradients.png)

```css
div {
	background: #58a;
	background: linear-gradient(135deg, transparent 15px, #58a 0) top left,
	            linear-gradient(-135deg, transparent 15px, #58a 0) top right,
	            linear-gradient(-45deg, transparent 15px, #58a 0) bottom right,
	            linear-gradient(45deg, transparent 15px, #58a 0) bottom left;
	background-size: 50% 50%;
	background-repeat: no-repeat;
	
	padding: 1em 1.2em;
	max-width: 12em;
	color: white;
	font: 150%/1.6 Baskerville, Palatino, serif;
}
```
### 13 梯形标签页

![](/images/trapezoid.png)

```css
.tab {
position: relative;
 display: inline-block;
 padding: .5em 1em .35em;
 color: white; }
.tab::before {
 content: ''; /* 用伪元素来生成一个矩形 */
 position: absolute;
 top: 0; right: 0; bottom: 0; left: 0;
 z-index: -1;
 background: #58a;
 transform: perspective(.5em) rotateX(5deg);
}
```

### 14 简单的饼图

![](/images/pie.png)


```css
.pie {
	width: 100px; height: 100px;
	border-radius: 50%;
	background: yellowgreen;
	background-image: linear-gradient(to right, transparent 50%, currentColor 0);
	color: #655;
}

.pie::before {
	content: '';
	display: block;
	margin-left: 50%;
	height: 100%;
	border-radius: 0 100% 100% 0 / 50%;
	background-color: inherit;
	transform-origin: left;
	animation: spin 3s linear infinite, bg 6s step-end infinite;
}

@keyframes spin {
	to { transform: rotate(.5turn); }
}
@keyframes bg {
	50% { background: currentColor; }
}
```
















## 第7章 结构与布局

### 36 自适应内部元素

![](/images/intrinsic-sizing.png)

```css
figure {
  width: min-content;
  margin: auto;
}
```

### 39 满幅的背景，定宽的内容

![](/images/fluid-fixed.png)

```css
/* 假设最小宽度是900px */
.sec{
  padding: 0 calc(50% - 450px);
  background: #333; 
}
```

### 40 垂直居中

![](/images/vertical-centering-abs.png)

需要知道宽高

```css
main {
  position: absolute;
  top: calc(50% - 3em);
  left: calc(50% - 9em);
  width: 18em;
  height: 6em;
}
```

不需要知道宽高

```css
main {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}
```

基于 Flexbox 的解决方案

```css
body {
  display: flex;
  min-height: 100vh;
}
main {
  margin: auto;
}
```

### 41 紧贴底部的页脚

![](/images/sticky-footer-fixed.png)


固定高度的解决方案

```css
#wrapper {
  min-height: calc(100vh - 7em); 
}
```

更灵活的解决方案

```css
body {
  display: flex;
  flex-flow: column;
  min-height:100vh;
}
main{
  flex:1;
}
```

