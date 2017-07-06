title: ES6 & React & Redux in En
speaker: Judith Huang
url: https://github.com/judithhuang/es6-react-redux-share
transition: slide
theme: dark
date: 2017年6月30号

[slide]
# ES6 & React & Redux
<small>Speaker Huang</small>

[slide]
# ES6

[slide]
# Introduction
------
ECMAScript 6, also known as ECMAScript 2015, is the latest version of the ECMAScript standard. ES6 is a significant update to the language, and the first update to the language since ES5 was standardized in 2009. Implementation of these features in major JavaScript engines is underway now.

[slide]
# Let + Const
------
- Block-scoped binding constructs. `let` is the new `var`. `const` is single-assignment. Static restrictions prevent use before assignment.

```js
{
  let x = 1;
  console.log(x); // 1
}

console.log(x); // Uncaught ReferenceError: x is not defined

const y = 3;
y = 4; // Uncaught TypeError: Assignment to constant variable
```

[slide]
# Destructuring
------
- Destructuring allows binding using pattern matching, with support for matching arrays and objects. Destructuring is fail-soft, similar to standard object lookup foo["bar"], producing undefined values when not found.

```js
// list matching
const [a, b] = [1, 2, 3];

// object matching
const { name, age } = { name: 'Tom' };

// Can be used in parameter position
function f({ name }) {
  console.log(name);
}

f({ name: 'Tom' });
```

[slide]
# Template Strings
------
- Template strings provide syntactic sugar for constructing strings. This is similar to string interpolation features in Perl, Python and more. Optionally, a tag can be added to allow the string construction to be customized, avoiding injection attacks or constructing higher level data structures from string contents.

```js
const name = 'Tom';
const time = 'today';

`Hello ${name}, How are you ${time}?`;
```

[slide]
# Arrows
------
- Arrows are a function shorthand using the `=>` syntax. They are syntactically similar to the related feature in C#, Java 8 and CoffeeScript. They support both statement block bodies as well as expression bodies which return the value of the expression. Unlike functions, arrows share the same lexical this as their surrounding code.

```js
const evens = [1, 3, 5];
const odds = evens.map(number => number + 1);

// similar with
const odds = evens.map(function(number) => { return number + 1; });
```

[slide]
# Classes
------
- ES6 classes are a simple sugar over the prototype-based OO pattern. Having a single convenient declarative form makes class patterns easier to use, and encourages interoperability. Classes support prototype-based inheritance, super calls, instance and static methods and constructors.

[slide]
# Classes
------
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

  // 静态方法
  static sayHello() {
    return 'hello';
  }

  // 私有方法
  static _private() {
    console.log('This is a private method');
  }
}

const point = new Point(0, 0);
point.toString();
Point.sayHello();
```

[slide]
# Default + Rest + Spread
------
- Callee-evaluated default parameter values. Turn an array into consecutive arguments in a function call. Bind trailing parameters to an array. Rest replaces the need for arguments and addresses common cases more directly.

```js
function f(x, y=12) {
  // y is 12 if not passed (or passed as undefined)
  return x + y;
}
f(3) == 15
function f(x, ...y) {
  // y is an Array
  return x * y.length;
}
f(3, "hello", true) == 6
function f(x, y, z) {
  return x + y + z;
}
// Pass each elem of array as argument
f(...[1,2,3]) == 6
```

[slide]
# Modules
------
- Language-level support for modules for component definition. Codifies patterns from popular JavaScript module loaders (AMD, CommonJS). Runtime behaviour defined by a host-defined default loader. Implicitly async model – no code executes until requested modules are available and processed.

```js
// lib/math.js
export function sum(x, y) {
  return x + y;
}
export var pi = 3.141593;

// app.js
import * as math from "lib/math";
alert("2π = " + math.sum(math.pi, math.pi));
```

[slide]
# Symbols
------
- Symbols enable access control for object state. Symbols allow properties to be keyed by either string (as in ES5) or symbol. Symbols are a new primitive type. Optional description parameter used in debugging - but is not part of identity. Symbols are unique (like gensym), but not private since they are exposed via reflection features like Object.getOwnPropertySymbols.

```js
const _private_key = Symbol('_private_key');

class Point {
  [_private_key]() {
    console.log('This is private method');
  }
}
```

[slide]
### Math + Number + String + Array + Object APIs
------
- Many new library additions, including core Math libraries, Array conversion helpers, String helpers, and Object.assign for copying.

```js
Number.EPSILON
Number.isInteger(Infinity) // false
Number.isNaN("NaN") // false

Math.acosh(3) // 1.762747174039086
Math.hypot(3, 4) // 5
Math.imul(Math.pow(2, 32) - 1, Math.pow(2, 32) - 2) // 2

"abcde".includes("cd") // true
"abc".repeat(3) // "abcabcabc"

Array.from(document.querySelectorAll('*')) // Returns a real Array
Array.of(1, 2, 3) // Similar to new Array(...), but without special one-arg behavior
[0, 0, 0].fill(7, 1) // [0,7,7]
[1, 2, 3].find(x => x == 3) // 3
[1, 2, 3].findIndex(x => x == 2) // 1
[1, 2, 3, 4, 5].copyWithin(3, 0) // [1, 2, 3, 1, 2]
["a", "b", "c"].entries() // iterator [0, "a"], [1,"b"], [2,"c"]
["a", "b", "c"].keys() // iterator 0, 1, 2
["a", "b", "c"].values() // iterator "a", "b", "c"

Object.assign(Point, { origin: new Point(0,0) })
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

[slide]
# React

[slide]
# Introducing JSX
------
- This funny tag syntax is neither a string nor HTML.
- It is called JSX, and it is a syntax extension to JavaScript. We recommend using it with React to describe what the UI should look like. JSX may remind you of a template language, but it comes with the full power of JavaScript.

```js
const element = <h1>Hello, world!</h1>;
```

[slide]
# Introducing JSX
------
- Embedding Expressions in JSX
- JSX is an Expression Too
- Specifying Attributes with JSX
- Specifying Children with JSX
- JSX Prevents Injection Attacks
- JSX Represents Objects