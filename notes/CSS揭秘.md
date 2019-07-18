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

```css
border: 10px solid hsla(0,0%,100%,.5);
background: white;
background-clip: padding-box;  /*默认值是border-box,背景会延伸到边框所在的区域下层。/
```

![](/images/semi-transparent-borders.png)

### 2 多重边框

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

![](/images/mutiple-borders.png)

### 3 灵活的背景定位

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

![](/images/extended-bg-position.png)





