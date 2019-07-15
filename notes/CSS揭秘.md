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
border: 10px solid rgba(255,255,255,.1);
background-clip: padding-box;  /*背景会延伸到边框所在的区域下层。/
```

<div style="width:200px;height:200px;background: #fff;border: 10px solid rgba(255,255,255,.1);color:#000;padding:10px;box-sizing:border-box;background-clip: padding-box;">
我有一个透明的边框
</div>










