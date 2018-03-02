# JavaScript高级程序设计（第3版）笔记

## 第一章 JavaScript简介

JavaScript创始人兰登·艾奇(Brendan Eich)

## 第二章 在 HTML 中使用 JavaScript

### 延迟脚本defer

HTML 4.01 为`<script>`标签定义了defer属性。这个属性的用途是表明脚本在执行时不会影响页面的构造。也就是说,脚本会被延迟到整个页面都解析完毕后再运行。因此,在`<script>`元素中设置defer属性,相当于告诉浏览器立即下载,但延迟执行。

### 异步脚本

指定 async 属性的目的是不让页面等待两个脚本下载和执行,从而异步加载页面其他内容。 为此,建议异步脚本不要在加载期间修改 DOM。

## 第三章 基本概念

5种简单数据类型(也称为基本数据类型):Undefined、Null、Boolean、Number 和 String。还有 1 种复杂数据类型——Object

## 第四章 变量、作用域和内存问题

5 种基本数据类型:Undefined、Null、Boolean、Number 和 String。

### 传递参数

ECMAScript中所有函数的参数都是按值传递的。

```js
function setName(obj) { obj.name = "Nicholas"; obj = new Object(); obj.name = "Greg"; }

var person = new Object(); setName(person); alert(person.name); //"Nicholas"
```

### 执行环境及作用域

每个执行环境都有一个与之关联的变量对象(variable object),环境中定义的所有变量和函数都保存在这个对象中。每个函数都有自己的执行环境。  
每个函数都有自己的执行环境。当执行流进入一个函数时,函数的环境就会被推入一个环境栈中。 而在函数执行之后,栈将其环境弹出,把控制权返回给之前的执行环境。ECMAScript 程序中的执行流 正是由这个方便的机制控制着。  
当代码在一个环境中执行时,会创建变量对象的一个作用域链(scope chain)。作用域链的用途,是 保证对执行环境有权访问的所有变量和函数的有序访问。作用域链的前端,始终都是当前执行的代码所 在环境的变量对象。如果这个环境是函数,则将其活动对象(activation object)作为变量对象。活动对 象在最开始时只包含一个变量,即 arguments 对象(这个对象在全局环境中是不存在的)。作用域链中 的下一个变量对象来自包含(外部)环境,而再下一个变量对象则来自下一个包含环境。这样,一直延 续到全局执行环境;全局执行环境的变量对象始终都是作用域链中的最后一个对象。

## 第五章 引用类型

对象是某个特定引用类型的实例。新对象是使用 new 操作符后跟一个构造函数来创建的。 构造函数本身就是一个函数,只不过该函数是出于创建新对象的目的而定义的。

### 操作方法

如果 slice()方法的参数中有一个负数,则用数组长度加上该数来确定相应的位 置。例如,在一个包含 5 项的数组上调用 slice(-2,-1)与调用 slice(3,4)得到的结果相同。如果结束位置小于起始位置,则返回空数组。

splice()方法始终都会返回一个数组,该数组中包含从原始数组中删除的项(如果没有删除任何项,则返回一个空数组)。

### 迭代方法

every():对数组中的每一项运行给定函数,如果该函数对每一项都返回 true,则返回 true。   
filter():对数组中的每一项运行给定函数,返回该函数会返回 true 的项组成的数组。  
forEach():对数组中的每一项运行给定函数。这个方法没有返回值。  
map():对数组中的每一项运行给定函数,返回每次函数调用的结果组成的数组。  
some():对数组中的每一项运行给定函数,如果该函数对任一项返回 true,则返回 true。

以上方法都不会修改数组中的包含的值。

### Function类型

函数实际上是对象。每个函数都是Function类型的实例,而且都与其他引用类型一样具有属性和方法。由于函 数是对象,因此函数名实际上也是一个指向函数对象的指针,不会与某个函数绑定。

### 没有重载

### 函数内部属性

arguments.callee,指向拥有这个arguments对象的函数
caller,这个属性中保存着调用当前函数的函数的引用

### 基本包装类型

引用类型与基本包装类型的主要区别就是对象的生存期。使用 new 操作符创建的引用类型的实例, 在执行流离开当前作用域之前都一直保存在内存中。而自动创建的基本包装类型的对象,则只存在于一 行代码的执行瞬间,然后立即被销毁。这意味着我们不能在运行时为基本类型值添加属性和方法。

### 字符串操作方法

下面三个方法第二个参数都为口，,则将字符串的长度作为结束位置  

slice(startIdx,endIdx) 
startIdx:负数时与总长度相加 endIdx:负数时与总长度相加  

substring(startIdx,endIdx) 
startIdx:负数时为0 endIdx:负数时为0 且数字小在的在前

substr(startIdx,count)  
startIdx:负数时与总长度相加 count:负数为0

```js
var stringValue = "hello world"; 
alert(stringValue.slice(-3)); //"rld"
alert(stringValue.substring(-3)); //"hello world"
alert(stringValue.substr(-3)); //"rld"
alert(stringValue.slice(3, -4)); //"lo w"
alert(stringValue.substring(3, -4)); //"hel"
alert(stringValue.substr(3, -4));//""(空字符串)
```

## 第六章 面向对象的程序设计

ECMAScript 中有两种属性:数据属性和访问器属性。

### 属性类型

[[Configurable]]:表示能否通过 delete 删除属性从而重新定义属性,能否修改属性的特 性,或者能否把属性修改为访问器属性。像前面例子中那样直接在对象上定义的属性,它们的 这个特性默认值为 true。  
[[Enumerable]]:表示能否通过 for-in 循环返回属性。像前面例子中那样直接在对象上定义的属性,它们的这个特性默认值为 true。  
[[Writable]]:表示能否修改属性的值。像前面例子中那样直接在对象上定义的属性,它们的这个特性默认值为 true。  
[[Value]]:包含这个属性的数据值。读取属性值的时候,从这个位置读;写入属性值的时候, 把新值保存在这个位置。这个特性的默认值为 undefined。

要修改属性默认的特性,必须使用 ECMAScript 5 的 Object.defineProperty()方法。这个方法 接收三个参数:属性所在的对象、属性的名字和一个描述符对象。

Object.definePro- perties()方法，为对象定义多个属性。

使用 ECMAScript 5 的 Object.getOwnPropertyDescriptor()方法,可以取得给定属性的描述 符。

### 创建对象

#### 工厂模式

```js
function createPerson(name, age, job){
  var o = new Object();
  o.name = name;
  o.age = age;
  o.job = job;
  o.sayName = function(){
    alert(this.name);
  };
  return o;
}

var person1 = createPerson("Nicholas", 29, "Software Engineer");
var person2 = createPerson("Greg", 27, "Doctor");
```

#### 构造函数模式

```js
function Person(name, age, job){
  this.name = name;
  this.age = age;
  this.job = job;
  this.sayName = function(){
    alert(this.name);
  };
}
var person1 = new Person("Nicholas", 29, "Software Engineer");
var person2 = new Person("Greg", 27, "Doctor");
```

#### 原型模式

```js
function Person(){ }

Person.prototype.name = "Nicholas";
Person.prototype.age = 29;
Person.prototype.job = "Software Engineer";
Person.prototype.sayName = function(){
  alert(this.name);
};

var person1 = new Person();
person1.sayName(); //"Nicholas"

var person2 = new Person();
person2.sayName(); //"Nicholas"

alert(person1.sayName == person2.sayName);//true
```

#### 组合使用构造函数模式和原型模式

```js
function Person(name, age, job){
   this.name = name;
   this.age = age;
   this.job = job;
   this.friends = ["Shelby", "Court"];
}

Person.prototype = {
  constructor : Person,
  sayName : function(){
    alert(this.name);
 }
}

var person1 = new Person("Nicholas", 29, "Software Engineer");
var person2 = new Person("Greg", 27, "Doctor");

person1.friends.push("Van");
alert(person1.friends); //"Shelby,Count,Van"
alert(person2.friends); //"Shelby,Count"
alert(person1.friends === person2.friends);
alert(person1.sayName === person2.sayName);

//false //true
```

#### 动态原型模式

```js
function Person(name, age, job){
  //属性
  this.name = name;
  this.age = age;
  this.job = job;
  //方法
  if (typeof this.sayName != "function"){
    Person.prototype.sayName = function(){
      alert(this.name);
    };
  }

}

var friend = new Person("Nicholas", 29, "Software Engineer"); friend.sayName();
```

#### 寄生构造函数模式

```js
function Person(name, age, job){
  var o = new Object();
  o.name = name;
  o.age = age;
  o.job = job;
  o.sayName = function(){
    alert(this.name);
  };
  return o;
}

var friend = new Person("Nicholas", 29, "Software Engineer"); friend.sayName(); //"Nicholas"
```

#### 稳妥构造函数模式

```js
function Person(name, age, job){
//创建要返回的对象
var o = new Object();
//可以在这里定义私有变量和函数
//添加方法
o.sayName = function(){
  alert(name);
};
//返回对象 return o;
}
```

### 继承

继承是OO语言中的一个最为人津津乐道的概念。许多OO语言都支持两种继承方式:接口继承和实现继承。接口继承只继承方法签名,而实现继承则继承实际的方法。如前所述,由于函数没有签名,在ECMAScript中无法实现接口继承。ECMAScript只支持实现继承,而且其实现继承主要是依靠原型链来实现的。

#### 原型链

```js
function SuperType(){
  this.property = true;
}
SuperType.prototype.getSuperValue = function(){
  return this.property;
};
function SubType(){
  this.subproperty = false;
}

//继承了 SuperType
SubType.prototype = new SuperType();
SubType.prototype.getSubValue = function (){
  return this.subproperty;
};
var instance = new SubType();
alert(instance.getSuperValue());
//true
```

#### 借用构造函数

```js
function SuperType(){
  this.colors = ["red", "blue", "green"];
}
function SubType(){
//继承了
SuperType SuperType.call(this);
}
var instance1 = new SubType();
instance1.colors.push("black");
alert(instance1.colors); //"red,blue,green,black"

var instance2 = new SubType();
alert(instance2.colors); //"red,blue,green"
```

#### 组合继承

```js
function SuperType(name){
  this.name = name;
  this.colors = ["red", "blue", "green"];
}
SuperType.prototype.sayName = function(){
  alert(this.name);
};
function SubType(name, age){
  //继承属性
  SuperType.call(this, name);
  this.age = age;
}
//继承方法
SubType.prototype = new SuperType(); SubType.prototype.constructor = SubType; SubType.prototype.sayAge = function(){
  alert(this.age);
};
var instance1 = new SubType("Nicholas", 29); instance1.colors.push("black");
alert(instance1.colors); //"red,blue,green,black"
instance1.sayName(); //"Nicholas";
instance1.sayAge(); //29

var instance2 = new SubType("Greg", 27);
alert(instance2.colors); //"red,blue,green"
instance2.sayName(); //"Greg";
instance2.sayAge(); //27
```

#### 原型式继承

```js
function object(o){
  function F(){}
  F.prototype = o;
  return new F();
}
```

#### 寄生式继承

```js
function createAnother(original){
  var clone = object(original); //通过调用函数创建一个新对象
  clone.sayHi = function(){ //以某种方式来增强这个对象
  alert("hi");
};
return clone; //返回这个对象
}
```

#### 寄生组合式继承

```js
function inheritPrototype(subType, superType){
  var prototype = object(superType.prototype); prototype.constructor = subType;
  subType.prototype = prototype;
}
```

```js
function SuperType(name){
  this.name = name; this.colors = ["red", "blue", "green"];
}
SuperType.prototype.sayName = function(){
  alert(this.name);
};
function SubType(name, age){
  SuperType.call(this, name);
  this.age = age;
}
inheritPrototype(SubType, SuperType);
SubType.prototype.sayAge = function(){
  alert(this.age);
};
```

## 第七章 函数表达式

### 闭包

闭包是指有权访问另一个 函数作用域中的变量的函数。

### 私有变量

任何在函数中定义的变量,都可以认为是私有变量,因为不能在函数的外部访问这些变量。 私有变量包括函数的参数、局部变量和在函数内部定义的其他函数。
有权访问私有变量和私有函数的公有方法称为特权方法(privileged method)。

```js
function MyObject(){
  //私有变量和私有函数 var privateVariable = 10;
  function privateFunction(){
    return false;
  }
  //特权方法
  this.publicMethod = function (){
    privateVariable++;
    return privateFunction();
  };
}
```

## 第八章 BOM

### location 对象

```js
location.href = "http://www.churjan.com";
location.reload();//重新加载(有可能从缓存中加载)
location.reload(true);//重新加载(从服务器重新加载)
location.replace("http://www.churjan.com/")//不会在历史记录中生成新记录
```

## 第十章 DOM

文档节点是每个文档的根节点。在这个例子中,文档节点只有一个子节点,即`<html>`素,我们称之为文档元素。文档元素是文档的最外层元素,文档中的其他所有元素都包含在文档元素中。每个文 档只能有一个文档元素。在 HTML 页面中,文档元素始终都是`<html>`元素。在 XML 中,没有预定义 的元素,因此任何元素都可能成为文档元素。

每个节点都有一个 childNodes 属性,其中保存着一个 NodeList 对象。NodeList 是一种类数组 对象,用于保存一组有序的节点,可以通过位置来访问这些节点。请注意,虽然可以通过方括号语法来 访问 NodeList 的值,而且这个对象也有 length 属性,但它并不是 Array 的实例。NodeList 对象的 独特之处在于,它实际上是基于 DOM 结构动态执行查询的结果,因此 DOM 结构的变化能够自动反映 在 NodeList 对象中。

### 操作节点

appendChild(),用于向 childNodes 列表的末尾添加一个节点

insertBefore(),如果需要把节点放在 childNodes 列表中某个特定的位置上, 而不是放在末尾,那么可以使用 insertBefore()方法。这个方法接受两个参数:要插入的节点和作为参照的节点。

replaceChild()方法接受的两个参数是:要插入的节点和要替换的节点

### Element类型

要访问元素的标签名,可以使用 nodeName 属性,也可以使用 tagName 属性;这两个属性会返回 相同的值(使用后者主要是为了清晰起见)。以下面的元素为例:

```js
<div id="myDiv"></div>
var div = document.getElementById("myDiv");
alert(div.tagName); //"DIV"
alert(div.tagName == div.nodeName); //true
```
 
### 动态脚本

动态加载的外部 JavaScript 文件能够立即运行,比如下面的`<script>`元素:


`<script type="text/javascript" src="client.js"></script>`

这个`<script>`元素包含了第 9 章的客户端检测脚本。而创建这个节点的 DOM 代码如下所示:

```js
var script = document.createElement("script");
script.type = "text/javascript";
script.src = "client.js";
document.body.appendChild(script);
```

### 总结
Document 类型表示整个文档,是一组分层节点的根节点。在 JavaScript 中,document 对象是

Document 的一个实例。使用 document 对象,有很多种方式可以查询和取得节点。

## DOM扩展

### classList 属性

add(value):将给定的字符串值添加到列表中。如果值已经存在,就不添加了。   
contains(value):表示列表中是否存在给定的值,如果存在则返回 true,否则返回 false。  
remove(value):从列表中删除给定的字符串。  
toggle(value):如果列表中已经存在给定的值,删除它;如果列表中没有给定的值,添加它。

## DOM2 和 DOM3

DOM1 级主要定义的是 HTML 和 XML 文档的底层结构。DOM2 和 DOM3 级则在这个结构 的基础上引入了更多的交互能力, 也支持了更高级的 XML 特性。 为此, DOM2 和 DOM3 级分为许多模块(模块之间具有某种关联), 分别描述了 DOM 的某个非常具体的子集。

## 第十三章 事件

### 事件冒泡

事件冒泡(event bubbling),即事件开始时由最具体的元素(文档中嵌套层次最深 的那个节点)接收,然后逐级向上传播到较为不具体的节点(文档)。

### 事件捕获

事件捕获(event capturing),事件捕获的思想 是不太具体的节点应该更早接收到事件,而最具体的节点应该最后接收到事件。事件捕获的用意在于在 事件到达预定目标之前捕获它。

### DOM事件流

“DOM2级事件”规定的事件流包括三个阶段:事件捕获阶段、处于目标阶段和事件冒泡阶段。

### 事件对象

在触发 DOM 上的某个事件时,会产生一个事件对象 event,这个对象中包含着所有与事件有关的 信息。包括导致事件的元素、事件的类型以及其他与特定事件相关的信息。例如,鼠标操作导致的事件 对象中,会包含鼠标位置的信息,而键盘操作导致的事件对象中,会包含与按下的键有关的信息。所有 浏览器都支持 event 对象,但支持方式不同。

## 第十五章 使用Canvas绘图

```js
strokeStyle //填充
fillStyle //描边

//这三个方法都能接收 4 个参数:矩形的 x 坐标、矩形的 y 坐标、矩形 宽度和矩形高度
fillRect()
strokeRect()
clearRect()
```

### 绘制路径

```js
beginPath()
arc(x,y,radius,startAngle,endAngle,counterclockwise)
lineTo(x,y)
moveTo(x,y)
stroke()
fill()
```

## 第十六章 HTML5 脚本编程

### 跨平台推送
跨文档消息传送(cross-document messaging),有时候简称为 XDM,指的是在来自不同域的页面间 传递消息。
postMessage()方法接收两个参数:一条消息和一个表示消息接收方来自哪个域的字符串。

接收到 XDM 消息时,会触发 window 对象的 message 事件。这个事件是以异步形式触发的,因此 从发送消息到接收消息(触发接收窗口的 message 事件)可能要经过一段时间的延迟。触发 message 事件后,传递给 onmessage 处理程序的事件对象包含以下三方面的重要信息。

data:作为 postMessage()第一个参数传入的字符串数据。  
origin:发送消息的文档所在的域,例如"http://www.wrox.com"。  
source:发送消息的文档的 window 对象的代理。这个代理对象主要用于在发送上一条消息的 窗口中调用 postMessage() 方法。 如果发送消息的窗口来自同一个域, 那这个对象就是 window。

### 原生拖放

#### 被拖拽的元素

(1) dragstart   
(2) drag   
(3) dragend

#### 放置目标的元素

(1) dragenter   
(2) dragover   
(3) dragleave 或 drop

## 第二十章 JSON

JSON 对象有两个方法:stringify()和 parse()。

## 第二十一章 Ajax 与 Comet

```js
var xhr = new XMLHttpRequest();
xhr.onreadystatechange = function(){ 
  if (xhr.readyState == 4){ 
    if ((xhr.status >= 200 && xhr.status < 300) || xhr.status == 304){
        alert(xhr.responseText); 
      } else {
        alert("Request was unsuccessful: " + xhr.status); 
      }
}

}; 
xhr.open("get", "example.txt", true); 
xhr.setRequestHeader("MyHeader", "MyValue");
xhr.send(null);
```

`xhr.abort();`停止触发事件

### http头部信息

默认情况下,在发送 XHR 请求的同时,还会发送下列头部信息。 
Accept:浏览器能够处理的内容类型。

Accept-Charset:浏览器能够显示的字符集。

Accept-Encoding:浏览器能够处理的压缩编码。

Accept-Language:浏览器当前设置的语言。 

Connection:浏览器与服务器之间连接的类型。

Cookie:当前页面设置的任何 Cookie。 

Host:发出请求的页面所在的域 。 

Referer:发出请求的页面的 URI。注意,HTTP 规范将这个头部字段拼写错了,而为保证与规范一致,也只能将错就错了。(这个英文单词的正确拼法应该是 referrer。)

 User-Agent:浏览器的用户代理字符串。

### POST请求

 ```js
 ...
xhr.setRequestHeader("Content-Type", "application/x-www-form-urlencoded"); 
var form = document.getElementById("user-info");
 xhr.send(serialize(form));
 ```

### 函数节流

```js
function throttle(method, context) { 
  clearTimeout(method.tId);
   method.tId= setTimeout(function(){
      method.call(context); 
  }, 100); 
}
```