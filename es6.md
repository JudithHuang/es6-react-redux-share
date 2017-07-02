title: ES6
speaker: Judith Huang
url: https://github.com/judithhuang/es6-react-redux-share
transition: slide3
theme: dark
date: 2017年6月30号

[slide]
# ES6
<small>演讲者：Judith Huang</small>

[slide]
# let 命令
------
- 基本用法:    
ES6 新增了 `let` 命令，用来声明变量。它的用法类似于 `var` , 但是所声明的变量，只在 `let` 命令的代码块内有效。

```js
{
  let a = 10;
  var b = 1;
}

a // ReferenceError: a is not defined.
b // 1
```

- 不存在变量提升    
`var` 命令会发生”变量提升“现象，即变量可以在声明之前使用，值为 `undefined`。
`let` 命令改变了语法行为，它所声明的变量一定要在声明后使用，否则报错。

```js
// var 的情况
console.log(number); // 输出undefined
var number = 2;

// let 的情况
console.log(bar); // 报错ReferenceError
let bar = 2;
```

[slide]
# let 命令
------
- 暂时性死区:   
只要块级作用域内存在let命令，它所声明的变量就“绑定”（binding）这个区域，不再受外部的影响。    
下面代码中，存在全局变量tmp，但是块级作用域内let又声明了一个局部变量tmp，导致后者绑定这个块级作用域，所以在let声明变量前，对tmp赋值会报错。

```js
var tmp = 123;

if (true) {
  tmp = 'abc'; // ReferenceError
  let tmp;
}
```

[slide]
# let 命令
------
- 不允许重复声明:    
let不允许在相同作用域内，重复声明同一个变量。

```js
// 报错
function () {
  let a = 10;
  var a = 1;
}

// 报错
function () {
  let a = 10;
  let a = 1;
}
```

[slide]
# const 命令
------
`const` 声明一个只读的常量。一旦声明，常量的值就不能改变。
`const` 一旦声明变量，就必须立即初始化，不能留到以后赋值。

```js
const PI = 3.1415;
PI // 3.1415

PI = 3;
// TypeError: Assignment to constant variable.
```

[slide]
# 变量的结构赋值
------
- 数据的解构赋值:    
ES6 允许按照一定模式，从数组和对象中提取值，对变量进行赋值，这被称为解构（Destructuring）。

```js
// 以前写法
let a = 1;
let b = 2;
let c = 3;

// ES6写法
let [a, b, c] = [1, 2, 3];

// 解构设置默认值, 如果一个数组成员不严格等于undefined，默认值是不会生效的
let [x = 1] = [undefined];
x // 1

let [x = 1] = [null];
x // null
```

[slide]
# 变量的结构赋值
------
- 对象的解构赋值    
对象的解构与数组有一个重要的不同。数组的元素是按次序排列的，变量的取值由它的位置决定；而对象的属性没有次序，变量必须与属性同名，才能取到正确的值。

```js
let { name } = { name: "Tom" };
name // "Tom"

// 如果变量名与属性名不一致
let { name: myName } = { name: "Tom" };
myName // Tom

// 解构设置默认值
let { name: myName = "Tim" } = { };
```

[slide]
# 变量的结构赋值
------
- 字符串的解构赋值    
字符串也可以解构赋值。这是因为此时，字符串被转换成了一个类似数组的对象。

```js
const [a, b, c, d, e] = 'hello';
a // "h"
b // "e"
c // "l"
d // "l"
e // "o"
```

[slide]
# 变量的结构赋值
------
- 函数参数的解构赋值    
函数 `add` 的参数表面上是一个数组，但在传入参数的那一刻，数组参数就被解构成变量 `x` 和 `y` 。对于函数内部的代码来说，它们能感受到的参数就是 `x` 和 `y` 。

```js
function add([x, y]){
  return x + y;
}

add([1, 2]); // 3
```    


[slide]
# 字符串的扩展
------
- 字符串的遍历器接口    
ES6为字符串添加了遍历器接口（详见《Iterator》一章），使得字符串可以被for...of循环遍历。

```js
for (let codePoint of 'foo') {
  console.log(codePoint)
}
// "f"
// "o"
// "o"
```

- includes(), startsWith(), endsWith()     
传统上，JavaScript只有indexOf方法，可以用来确定一个字符串是否包含在另一个字符串中。ES6又提供了三种新方法。这三个方法都支持第二个参数，表示开始搜索的位置

    - includes()：返回布尔值，表示是否找到了参数字符串。
    - startsWith()：返回布尔值，表示参数字符串是否在源字符串的头部。
    - endsWith()：返回布尔值，表示参数字符串是否在源字符串的尾部。

[slide]
# 字符串的扩展
------
- 模板字符串    
传统的JavaScript语言，输出模板通常是这样写的

```js
$('#result').append(
  'There are <b>' + basket.count + '</b> ' +
  'items in your basket, ' +
  '<em>' + basket.onSale +
  '</em> are on sale!'
);
```

上面这种写法相当繁琐不方便，ES6引入了模板字符串解决这个问题。

```js
$('#result').append(`
  There are <b>${basket.count}</b> items
   in your basket, <em>${basket.onSale}</em>
  are on sale!
`);
```

[slide]
# 字符串的扩展
------
- 模板字符串  
模板字符串（template string）是增强版的字符串，用反引号（`）标识。它可以当作普通字符串使用，也可以用来定义多行字符串，或者在字符串中嵌入变量。

```js
// 普通字符串
`In JavaScript '\n' is a line-feed.`

// 多行字符串
`In JavaScript this is
 not legal.`

console.log(`string text line 1
string text line 2`);

// 字符串中嵌入变量
var name = "Bob", time = "today";
`Hello ${name}, how are you ${time}?`

// 大括号内部可以放入任意的JavaScript表达式，可以进行运算，以及引用对象属性。
var x = 1;
var y = 2;

`${x} + ${y} = ${x + y}`
// "1 + 2 = 3"

// 模板字符串之中还能调用函数。
function fn() {
  return "Hello World";
}

`foo ${fn()} bar`
// foo Hello World bar
```

[slide]
# 正则的扩展

[slide]
# 数值的扩展

[slide]
# 函数的扩展

[slide]
# 对象的扩展

[slide]
# Symbol

[slide]
# Set & Map

[slide]
# Proxy

[slide]
# Reflect

[slide]
 # Promise 对象

[slide]
# Iterator 和 for ... of 循环

[slide]
# Generator 函数

[slide]
# async 函数

[slide]
# Class 的基本语法

[slide]
# Decorator

[slide]
# Module 的语法

[slide]
# babel

[slide]
# reference

- [ECMAScript 6 入门](http://es6.ruanyifeng.com/)
- [ES6 Features](https://github.com/lukehoban/es6features)