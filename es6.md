title: ES6
speaker: Judith Huang
url: https://github.com/judithhuang/es6-react-redux-share
transition: slide
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
# 变量的解构赋值
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
# 变量的解构赋值
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
# 变量的解构赋值
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
# 变量的解构赋值
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
模板字符串（template string）是增强版的字符串，用反引号（`）标识。它可以当作普通字符串使用，也可以用来定义多行字符串，或者在字符串中嵌入变量。

[slide]
# 字符串的扩展
------
- 模板字符串  
模板字符串（template string）是增强版的字符串，用反引号（`）标识。它可以当作普通字符串使用，也可以用来定义多行字符串，或者在字符串中嵌入变量。

```js
const name = "Bob", time = "today";

// es5
'Hello ' + name + ', how are you ' + time + '?' 

// es6
`Hello ${name}, how are you ${time}?`
```

[slide]
# 数组的扩展
------
- 扩展运算符    
扩展运算符（spread）是三个点（...）。它好比 rest 参数的逆运算，将一个数组转为用逗号分隔的参数序列。

```js
console.log(...[1, 2, 3])
// 1 2 3

console.log(1, ...[2, 3, 4], 5)
// 1 2 3 4 5

[...document.querySelectorAll('div')]
// [<div>, <div>, <div>]
```

[slide]
# 数组的扩展
------
- Array.from()
- Array.of()
- 数组实例的 copyWithin()
- 数组实例的 find() 和 findIndex()
- 数组实例的fill()
- 数组实例的 entries()，keys() 和 values()
- 数组实例的 includes()

[slide]
# 对象的扩展
------
- 属性的简洁表示法    
ES6 允许直接写入变量和函数，作为对象的属性和方法。这样的书写更加简洁。

```js
var foo = 'bar';
var baz = {foo};
baz // {foo: "bar"}

// 等同于
var baz = {foo: foo};
```

- 属性名表达式     
下面代码的方法一是直接用标识符作为属性名，方法二是用表达式作为属性名，这时要将表达式放在方括号之内。

```js
// 方法一
obj.foo = true;

// 方法二
obj['a' + 'bc'] = 123;
```

[slide]
# 对象的扩展
------
- Object.assign    
Object.assign方法用于对象的合并，将源对象（source）的所有可枚举属性，复制到目标对象（target）。    
注意，如果目标对象与源对象有同名属性，或多个源对象有同名属性，则后面的属性会覆盖前面的属性。

```js
var target = { a: 1 };

var source1 = { b: 2 };
var source2 = { c: 3 };

Object.assign(target, source1, source2);
target // {a:1, b:2, c:3}
```

[slide]
# 对象的扩展
------
- 对象的扩展运算符    
  - 解构赋值: 对象的解构赋值用于从一个对象取值，相当于将所有可遍历的、但尚未被读取的属性，分配到指定的对象上面。所有的键和它们的值，都会拷贝到新对象上面。
  - 扩展运算符: 扩展运算符（...）用于取出参数对象的所有可遍历属性，拷贝到当前对象之中。

```js
// 1. 解构赋值
let { x, y, ...z } = { x: 1, y: 2, a: 3, b: 4 };
x // 1
y // 2
z // { a: 3, b: 4 }

// 2. 扩展运算符
let z = { a: 3, b: 4 };
let n = { ...z };
n // { a: 3, b: 4 }
```

[slide]
# Symbol
------
- 概述    
ES6 引入了一种新的原始数据类型Symbol，表示独一无二的值。它是 JavaScript 语言的第七种数据类型，前六种是：undefined、null、布尔值（Boolean）、字符串（String）、数值（Number）、对象（Object）。    
Symbol 值通过Symbol函数生成。这就是说，对象的属性名现在可以有两种类型，一种是原来就有的字符串，另一种就是新增的 Symbol 类型。凡是属性名属于 Symbol 类型，就都是独一无二的，可以保证不会与其他属性名产生冲突。

```js
let s = Symbol();

typeof s; // "symbol"
```

[slide]
# Promise 对象
------
- 基本用法    
Promise构造函数接受一个函数作为参数，该函数的两个参数分别是resolve和reject。它们是两个函数，由 JavaScript 引擎提供，不用自己部署。    
resolve函数的作用是，将Promise对象的状态从“未完成”变为“成功”（即从 Pending 变为 Resolved），在异步操作成功时调用，并将异步操作的结果，作为参数传递出去；reject函数的作用是，将Promise对象的状态从“未完成”变为“失败”（即从 Pending 变为 Rejected），在异步操作失败时调用，并将异步操作报出的错误，作为参数传递出去。    
Promise实例生成以后，可以用then方法分别指定Resolved状态和Reject状态的回调函数。

[slide]
# Promise 对象
------   

```js
var promise = new Promise(function(resolve, reject) {
  // ... some code

  if (/* 异步操作成功 */){
    resolve(value);
  } else {
    reject(error);
  }
});

promise.then(function(value) {
  // success
}, function(error) {
  // failure
});
```

[slide]
# Class 的基本语法
------
- 简介    
ES6 提供了更接近传统语言的写法，引入了 Class（类）这个概念，作为对象的模板。通过class关键字，可以定义类。    

基本上，ES6 的class可以看作只是一个语法糖，它的绝大部分功能，ES5 都可以做到，新的class写法只是让对象原型的写法更加清晰、更像面向对象编程的语法而已。上面的代码用 ES6 的class改写，就是下面这样。

[slide]
# Class 的基本语法
------
- 简介    
  - constructor: 类的默认方法，通过new命令生成对象实例时，自动调用该方法
  - 静态方法: 该方法不会被实例继承，而是直接通过类来调用
  - 私有方法: ES6 不提供, 可以命名上加以区别

```js
class Point {
  constructor(x, y) {
    this.x = x;
    this.y = y;
  }

  // 公有方法
  toString() {
    return '(' + this.x + ', ' + this.y + ')';
  }

  static sayHello() {
    return 'hello';
  }

  _private() {
    console.log('This is a private method');
  }
}

const point = new Point(0, 0);
point.toString();
```

[slide]
# Module 的语法
------
模块功能主要由两个命令构成：export和import。export命令用于规定模块的对外接口，import命令用于输入其他模块提供的功能。

```js
// profile.js
var firstName = 'Michael';
var lastName = 'Jackson';
var year = 1958;

export {firstName, lastName, year};

// main.js
import {firstName, lastName, year} from './profile';
function setName(element) {
  element.textContent = firstName + ' ' + lastName;
}
```

[slide]
# 转码器 
------
- [Babel](http://babeljs.io/)
- [Traceur](https://github.com/google/traceur-compiler)

[slide]
# References

- [ECMAScript 6 入门](http://es6.ruanyifeng.com/)
- [ES6 Features](https://github.com/lukehoban/es6features)