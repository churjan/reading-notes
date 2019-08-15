# CSS揭秘

|基本信息||
|:-|:-|
|图书名称|CSS揭秘 |
|外文书名|CSS Secret Better Solutions to Everyday Web Design Problems|
|作者|[希]Lea Verou 著 CSS魔法 译|
|出版社|人民邮电出版社|
|出版日期|2016年04月01日|

## 第二章 背景与边框

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

### 第7章 结构与布局

36 自适应内部元素

![](/images/intrinsic-sizing.png)

```css
figure {
width: min-content;
margin: auto; }
```

