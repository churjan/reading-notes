# 你不知道的JavaScript（中卷）

## 第一部分 类型和语法

### 第一章 类型

类型是值的内部特征,它定义了值的行为,以使其区别于其他值。

JavaScript

有七种内置类型:

```js
空值(null)
未定义(undefined)
布尔值(boolean)
数字(number)
字符串(string)
对象(object)
符号(symbol,ES6中新增)
```

我们可以用`typeof`运算符来查看值的类型,它返回的是类型的字符串值。

```js
typeof 42 //number
typeof '42' //string
typeof true //bollean
typeof null //object
typeof undefined //undefined
typeof Symbol() //symbol
typeof {n:42} //object
typeof function a(){} //function
```

#### 值和类型

JavaScript中的变量是没有类型的,只有值才有。变量可以随时持有任何类型的值。

#### `undefined`和`undeclared`

```js
undeclared(not defined) //没声明
undefined //生命了但没赋值
```

通过`typeof`的安全防范机制(阻止报错)来检查`undeclared`变量  

```js
if(typeof atob === "undefined")
```

或者`window`

```js
if(window.atob)
```

### 第二章 值

#### 数组

对数组声明后即可向其中加入值,不需要预先设定大小

数组通过数字进行索引, 但有趣的是它们也是对象, 所以也可以包含字符串键值和属性(但这些并不计算在数组长度内):

```js
var a = [ ];
a[0] = 1;
a["foobar"] = 2;
a.length;  //1
a["foobar"];  //2
a.foobar;  //2
```

类数组,有时需要将类数组(一组通过数字索引的值)转换为真正的数组

```js
function foo() {
  var arr = Array.prototype.slice.call( arguments );
  arr.push( "bam" );
  console.log( arr );
}
foo( "bar", "baz" );  // ["bar","baz","bam"]
```

用ES6中的内置工具函数`Array.from(..)`也能实现同样的功能:

```js
var arr = Array.from( arguments );
```

#### 数字

JavaScript中的“整数”就是没有小数的十进制数。所以42.0即等同于“整数”42。

#### 特殊数值

`undefined`类型只有一个值,即`undefined`。`null`类型也只有一个值,即`null`。它们的名称既是类型也是值。

`undefined`,指没有指(missing value),指从未赋值
`null`,指空值(empty value),指曾赋过值,但是目前没有值

void 运算符,`undefined`是一个内置标识符(除非被重新定义,见前面的介绍), 它的值为`undefined`,通过`void`运算符即可得到该值。

```js
var a = 42;
console.log( void a, a ); // undefined 42
```

### 第三章 原生函数

#### 内部属性`[[Class]]`

所有`typeof`返回值为"object"的对象(如数组)都包含一个内部属性`[[Class]]`(我们可以把它看作一个内部的分类,而非传统的面向对象意义上的类)。这个属性无法直接访问,

一般通过`Object.prototype.toString(..)`来查看。

#### 封装对象包装

封装对象(objectwrapper)扮演着十分重要的角色。由于基本类型值没有`.length`和`.toString()`这样的属性和方法,需要通过封装对象才能访问,此时JavaScript会自动为基本类型值包装(box或者 wrap)一个封装对象:

```js
var a = "abc";
a.length; // 3
a.toUpperCase(); // "ABC"
```

#### 拆封

如果想要得到封装对象中的基本类型值,可以使用`valueOf()`函数
