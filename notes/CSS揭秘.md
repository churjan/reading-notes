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

## 第4章 视觉效果

### 15 单侧投影

![](/images/shadow-one-side.png)

```css
box-shadow: 0 5px 4px -4px black;
```

### 16 不规则投影


![](/images/drop-shadow.png)

```css
filter: drop-shadow(2px 2px 10px rgba(0,0,0,.5));
```

## 第6章  用户体验

### 30 扩大可点击区域

![](/images/hit-area.png)

box-shadow方案

```css
button {
	padding: .3em .5em;
	border: 10px solid transparent;
	border-radius: 50%;
	background: #58a;
	background-clip: padding-box;
	box-shadow: 0 0 0 1px rgba(0,0,0,.3) inset;
	color: white;
	font: bold 150%/1 sans-serif;
	cursor: pointer;
}
```

伪元素方案

```css
button {
	position: relative;
	padding: .3em .5em;
	background: #58a;
	border-radius: 50%;
	border: 1px solid rgba(0,0,0,.3);
	box-shadow:  0 .1em .2em -.05em rgba(0,0,0,.5);
	color: white;
	font: bold 150%/1 sans-serif;
	cursor: pointer;
}

button:before {
	content: '';
	position: absolute;
	top: -10px; right: -10px;
	bottom: -10px; left: -10px;
}
```

### 31 自定义复选框

```html
<input type="checkbox" id="awesome" />
<label for="awesome">Awesome!</label>
```

![](/images/custom-checkboxes.png)

```css
input[type="checkbox"] + label::before {
  content: '\a0'; /* 不换行空格 */
  display: inline-block;
  vertical-align: .2em;
  width: .8em;
  height: .8em;
  margin-right: .2em;
  border-radius: .2em;
  background: silver;
  text-indent: .15em;
  line-height: .65;
}
input[type="checkbox"]:checked + label::before {
  content: '\2713';
  background: yellowgreen;
}
input[type="checkbox"] {
  position: absolute;
  clip: rect(0,0,0,0);
}
```

### 32 通过阴影来弱化背景

![](/images/modal.png)

伪元素方案

```css
body.dimmed::before {
position: fixed;
top: 0;
right: 0;
 bottom: 0;
left: 0;
z-index: 1;
background: rgba(0,0,0,.8);
}
```

box-shadow 方案

缺点：不能阻止点击穿透

```css
box-shadow: 0 0 0 50vmax rgba(0,0,0,.8);
```

### 33 通过模糊来弱化背景

![](/images/emphasizing.png)

```css
filter: blur(10px);
```

### 34 滚动提示

```html
<ul>	
	<li>Ada Catlace</li>	
	<li>Alan Purring</li>
	<li>Schrödingcat</li>
	<li>Tim Purrners-Lee</li>
	<li>Webkitty</li>	
	<li>Json</li>
	<li>Void</li>
	<li>Neko</li>	
	<li>NaN</li>
	<li>Cat5</li>
	<li>Vector</li>
</ul>
```

![](/images/scrolling-hints.png)

```css
ul {
	display: inline-block;
	overflow: auto;
	width: 7.2em;
	height: 7em;
	border: 1px solid silver;
	padding: .3em .5em;
	list-style: none;
	margin-top: 2em;
	font: 100 200%/1.6 'Frutiger LT Std', sans-serif;
	background: linear-gradient(white 15px, hsla(0,0%,100%,0)) 0 0 / 100% 50px,
	            radial-gradient(at top, rgba(0,0,0,.2), transparent 70%) 0 0 / 100% 15px,
	            linear-gradient(to top, white 15px, hsla(0,0%,100%,0)) bottom / 100% 50px,
	            radial-gradient(at bottom, rgba(0,0,0,.2), transparent 70%) bottom / 100% 15px;
	background-repeat: no-repeat;
	background-attachment: local, scroll, local, scroll;
	margin-top: 30px;
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

## 第8章 过渡与动画

### 43 逐帧动画

```html
<div class="loader">Loading...</div>
```

![](/images/loader.png)

```css
.loader {
  width: 100px; height: 100px;
  background: url(img/loader.png) 0 0;
  /* 把文本隐藏起来 */
  text-indent: 200%;
  white-space: nowrap;
  overflow: hidden; 
}
@keyframes loader {
  to {
    background-position: -800px 0;  
  } 
}
.loader {
  width: 100px; height: 100px;
  background: url(img/loader.png) 0 0;
  animation: loader 1s infinite linear;
  /* 把文本隐藏起来 */
  text-indent: 200%;
  white-space: nowrap;
  overflow: hidden;
}
```

### 45 打字动画

```html
<h1>CSS is awesome!</h1>
```

![](/images/typing.png)

```css
@keyframes typing {
	from { width: 0 }
}

@keyframes caret {
	50% { border-right-color: transparent; }
}

h1 {
	font: bold 200% Consolas, Monaco, monospace;
	/*width: 8.25em;*/
	width: 15ch;
	white-space: nowrap;
	overflow: hidden;
	border-right: .05em solid;
	animation: typing 8s steps(15),
	           caret 1s steps(1) infinite;
}
```


