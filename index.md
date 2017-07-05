title: ES6 & React & Redux
speaker: Judith Huang
url: https://github.com/judithhuang/es6-react-redux-share
transition: slide
theme: dark
date: 2017年6月30号

[slide]
# ES6 & React & Redux
<small>演讲者：Judith Huang</small>

[slide]
# ES6

[slide]
# let 命令
------
- 基本用法: ES6 新增了 `let` 命令，用来声明变量。它的用法类似于 `var` , 但是所声明的变量，只在 `let` 命令的代码块内有效。
- 不存在变量提升: `var` 命令会发生”变量提升“现象，即变量可以在声明之前使用，值为 `undefined`。
`let` 命令改变了语法行为，它所声明的变量一定要在声明后使用，否则报错。
- 暂时性死区: 只要块级作用域内存在let命令，它所声明的变量就“绑定”（binding）这个区域，不再受外部的影响。 
- 不允许重复声明: let 不允许在相同作用域内，重复声明同一个变量。

[slide]
# const 命令
------
- const: const 声明一个只读的常量。一旦声明， 就必须立即初始化, 常量的值就不能改变。

```js
const PI = 3.1415;
PI // 3.1415

PI = 3;
// TypeError: Assignment to constant variable.
```

[slide]
# 变量的解构赋值
------
- 数据的解构赋值: ES6 允许按照一定模式，从数组和对象中提取值，对变量进行赋值，这被称为解构（Destructuring）。

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
# 字符串的扩展
------
- 字符串的遍历器接口: ES6为字符串添加了遍历器接口（详见《Iterator》一章），使得字符串可以被for...of循环遍历。
- ES6提供的三种新方法:
    - includes()：返回布尔值，表示是否找到了参数字符串。
    - startsWith()：返回布尔值，表示参数字符串是否在源字符串的头部。
    - endsWith()：返回布尔值，表示参数字符串是否在源字符串的尾部。
- 模板字符串: 模板字符串（template string）是增强版的字符串，用反引号（`）标识。它可以当作普通字符串使用，也可以用来定义多行字符串，或者在字符串中嵌入变量。

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
- 扩展运算符: 扩展运算符（spread）是三个点（...）。它好比 rest 参数的逆运算，将一个数组转为用逗号分隔的参数序列。
- ES6 提供的新方法:
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
- 属性的简洁表示法: ES6 允许直接写入变量和函数，作为对象的属性和方法。这样的书写更加简洁。
- 属性名表达式: 下面代码的方法一是直接用标识符作为属性名，方法二是用表达式作为属性名，这时要将表达式放在方括号之内。

```js
// 属性的简洁表示法
const name = 'Tim';
const person = { name };

// 属性名表达式
obj['a' + 'bc'] = 123;
```

[slide]
# 对象的扩展
------
- Object.assign: Object.assign 方法用于对象的合并，将源对象（source）的所有可枚举属性，复制到目标对象（target）。    
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
- ES6 引入了一种新的原始数据类型Symbol，表示独一无二的值。它是 JavaScript 语言的第七种数据类型，前六种是：undefined、null、布尔值（Boolean）、字符串（String）、数值（Number）、对象（Object）。    
- Symbol 值通过Symbol函数生成。这就是说，对象的属性名现在可以有两种类型，一种是原来就有的字符串，另一种就是新增的 Symbol 类型。凡是属性名属于 Symbol 类型，就都是独一无二的，可以保证不会与其他属性名产生冲突。

```js
let s = Symbol();

typeof s; // "symbol"
```

[slide]
# Promise 对象
------
- Promise 构造函数接受一个函数作为参数，该函数的两个参数分别是 resolve 和 reject 。它们是两个函数，由 JavaScript 引擎提供，不用自己部署。    
- resolve 函数的作用是，将 Promise 对象的状态从“未完成”变为“成功”（即从 Pending 变为 Resolved），在异步操作成功时调用，并将异步操作的结果，作为参数传递出去；reject 函数的作用是，将 Promise 对象的状态从“未完成”变为“失败”（即从 Pending 变为 Rejected），在异步操作失败时调用，并将异步操作报出的错误，作为参数传递出去。    
- Promise 实例生成以后，可以用 then 方法分别指定 Resolved 状态和 Reject 状态的回调函数。

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
- ES6 提供了更接近传统语言的写法，引入了 Class（类）这个概念，作为对象的模板。通过 class 关键字，可以定义类。    
- 基本上，ES6 的 class 可以看作只是一个语法糖，它的绝大部分功能，ES5 都可以做到，新的 class 写法只是让对象原型的写法更加清晰、更像面向对象编程的语法而已。
- constructor: 类的默认方法，通过 new 命令生成对象实例时，自动调用该方法
- 静态方法: 该方法不会被实例继承，而是直接通过类来调用
- 私有方法: ES6 不提供, 可以命名上加以区别

[slide]
# Class 的基本语法

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
# Module 的语法
------
- 模块功能主要由两个命令构成：export 和 import。export 命令用于规定模块的对外接口，import 命令用于输入其他模块提供的功能。

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

[slide]
# React & Redux

[slide]
# 什么是 React.js
------
- 在整个 Web 应用的 MVC 架构中，你可以将React看作为视图层，并且是一个高效 的视图。React 提供了和以往不一样的方式来看待视图，它以组件开发为基础。 对 React 应用而言，你需要分割你的页面，使其成为一个个的组件。也就是说，你的 应用是由这些组件组合而成的。    
- 你可以通过分割组件的方式去开发复杂的页面或某个功能区块，并且组件是可以被复用的。这个过程大概类似于用乐高积木去瓶装不同的物体。我们称这种编程方式称为组件驱动开发。
- React 的一大特点是其所拥有的虚拟 DOM，它让页面渲染变得非常的高效，并且比直接 操纵 DOM 变得更为可控。这两大特点的组合使得 React 具有强大的自上而下的页面渲染能力。

[slide]
# 组件
------    
- React 应用都是构建在组件之上的。
- 组件两个核心概念:
  - props: 是组件的配置属性, 在组件内部是不变的, 只是在调用这个组件的时候传入不同的属性来定制显示这个组件;
  - state: 是组件的当前状态, 可以把组件简单看成一个“状态机”，根据状态 state 呈现不同的 UI 展示。一旦状态（数据）更改，组件就会自动调用 render 重新渲染 UI，这个更改的动作会通过 this.setState 方法来触发;

[slide]
# JSX
------
- JSX 是 React 的核心组成部分，它使用 XML 标记的方式去直接声明界面，界面组件之间可以互相嵌套。可以理解为在 JS 中编写与 XML 类似的语言,一种定义带属性树结构（DOM结构）的语法，它的目的不是要在浏览器或者引擎中实现，它的目的是通过各种编译器将这些标记编译成标准的JS语言。

[slide]
# Virtual DOM
------ 
- 当组件状态 state 有更改的时候，React 会自动调用组件的 render 方法重新渲染整个组件的 UI。
当然如果真的这样大面积的操作 DOM，性能会是一个很大的问题，所以 React 实现了一个Virtual DOM，组件 DOM 结构就是映射到这个 Virtual DOM 上，React 在这个 Virtual DOM 上实现了一个 diff 算法，当要重新渲染组件的时候，会通过 diff 寻找到要变更的 DOM 节点，再把这个修改更新到浏览器实际的 DOM 节点上，所以实际上不是真的渲染整个 DOM 树。这个 Virtual DOM 是一个纯粹的 JS 数据结构，所以性能会比原生 DOM 快很多。

[slide]
# Data Flow
------
- “单向数据绑定”是 React 推崇的一种应用架构的方式。简单来说单向数据流就是确保数据是单向绑定的，例如下图，数据的更新永远是顺着一个方向而不能反过来。     
<div class="columns2">
    <img src="/images/data_flow.png">
</div>

[slide]
# 组件的生命周期
------
- getInitialState: 初始化 this.state 的值，只在组件装载之前调用一次。
如果是使用 ES6 的语法，你也可以在构造函数中初始化状态

```js
class Counter extends Component {
  constructor(props) {
    super(props);
    this.state = { count: props.initialCount };
  }

  render() {
    // ...
  }
}
```

[slide]
# 组件的生命周期
------
- getDefaultProps: 只在组件创建时调用一次并缓存返回的对象（即在 React.createClass 之后就会调用）。
因为这个方法在实例初始化之前调用，所以在这个方法里面不能依赖 this 获取到这个组件的实例。
在组件装载之后，这个方法缓存的结果会用来保证访问 this.props 的属性时，当这个属性没有在父组件中传入（在这个组件的 JSX 属性里设置），也总是有值的。

```js
class Counter extends Component {
  defaultProps = {
    name: 'Tom'
  }

  render() {
    // ...
  }
}
```

[slide]
# 组件的生命周期
------
- render: 组装生成这个组件的 HTML 结构（使用原生 HTML 标签或者子组件），也可以返回 null 或者 false。

```js
class Counter extends Component {
  render() {
    if (/* 条件一 */) {
      return null;
    }

    if (/* 未登录 */) {
      return (<div> Please login first </div>);
    }

    return (<div> Hello, Your name is Tom </div>);
  }
}
```

[slide]
# 组件的生命周期函数
------
- componentWillMount: 只会在装载之前调用一次，在 render 之前调用，你可以在这个方法里面调用 setState 改变状态，并且不会导致额外调用一次 render, 通常情况下，推荐用`constructor()`方法代替;
- componentDidMount: 只会在装载完成之后调用一次，在 render 之后调用，这里可以加载服务器数据, 也可以使用`setState()`方法触发重新渲染;
- componentWillReceiveProps: 在已经挂载的组件接收到新props时触发, 在除了第一次生命周期之后的生命周期中触发;

[slide]
# 组件的生命周期函数
------
- shouldComponentUpdate: 在接收到新 props 或 state 时，或者说在 componentWillReceiveProps 后触发, 首次渲染时或者  forceUpdate() 时不会触发;
- componentWillUpdate: 在 props 或 state 发生改变或者 shouldComponentUpdate 触发后, 在 render 之前, 这个方法在组件初始化时不会被调用;
- componentDidUpdate: 在发生更新或 componentWillUpdate 后, 使用这个方法可以对组件中的DOM进行操作;
- componentWillUnmount: 在组件卸载或销毁之前, 可以处理一些必要的清理操作，比如无效的timers、interval，或者取消网络请求，或者清理任何在 componentDidMount 中创建的DOM元素;

[slide]
# 事件处理
------
- React 里面绑定事件的方式和在 HTML 中绑定事件类似，使用驼峰式命名指定要绑定的 onClick 属性为组件定义的一个方法(参考: [React 支持的事件列表](https://facebook.github.io/react/docs/events.html))     
- “合成事件”和“原生事件”    
React 实现了一个“合成事件”层（synthetic event system），这个事件模型保证了和 W3C 标准保持一致，所以不用担心有什么诡异的用法，并且这个事件层消除了 IE 与 W3C 标准实现之间的兼容问题。   

[slide]
# 事件处理
------
- “合成事件”还提供了额外的好处：    
  - 事件委托    
  “合成事件”会以事件委托（event delegation）的方式绑定到组件最上层，并且在组件卸载（unmount）的时候自动销毁绑定的事件。    
  - 什么是“原生事件”？    
  比如你在 componentDidMount 方法里面通过 addEventListener 绑定的事件就是浏览器原生事件。
  使用原生事件的时候注意在 componentWillUnmount 解除绑定 removeEventListener。
  所有通过 JSX 这种方式绑定的事件都是绑定到“合成事件”，除非你有特别的理由，建议总是用 React 的方式处理事件。    

[slide]
# DOM 操作
------
- 大部分情况下你不需要通过查询 DOM 元素去更新组件的 UI，你只要关注设置组件的状态（setState）。但是可能在某些情况下你确实需要直接操作 DOM。

```js
class App extends Component {
  refDom = (ref) => {
    if (ref) {
      this.ref = ref;
      // 这里可以对获取到的 DOM 元素进行更新操作
    } else {
      delete this.ref;
    }
  }

  render() {
    return (
      <div ref={(ref) => this.refDom(ref)} ref="name">
        hello
      </div>
    );
  }
}
```

[slide]
# 组件间通信
------
- 父子组件间通信    
这种情况下很简单，就是通过 props 属性传递，在父组件给子组件设置 props，然后子组件就可以通过 props 访问到父组件的数据／方法，这样就搭建起了父子组件间通信的桥梁。
- 非父子组件间的通信    
使用全局事件 Pub/Sub 模式，在 componentDidMount 里面订阅事件，在 componentWillUnmount 里面取消订阅，当收到事件触发的时候调用 setState 更新 UI。
这种模式在复杂的系统里面可能会变得难以维护，所以看个人权衡是否将组件封装到大的组件，甚至整个页面或者应用就封装到一个组件。

[slide]
# Redux 简介
- 随着 JavaScript 单页应用开发日趋复杂，JavaScript 需要管理比任何时候都要多的 state （状态）。 这些 state 可能包括服务器响应、缓存数据、本地生成尚未持久化到服务器的数据，也包括 UI 状态，如激活的路由，被选中的标签，是否显示加载动效或者分页器等等。    
管理不断变化的 state 非常困难。如果一个 model 的变化会引起另一个 model 变化，那么当 view 变化时，就可能引起对应 model 以及另一个 model 的变化，依次地，可能会引起另一个 view 的变化。直至你搞不清楚到底发生了什么。state 在什么时候，由于什么原因，如何变化已然不受控制。 当系统变得错综复杂的时候，想重现问题或者添加新功能就会变得举步维艰。

[slide]
# Action
------
- Action 是把数据从应用传到 store 的有效载荷。它是 store 数据的唯一来源。一般来说你会通过 store.dispatch() 将 action 传到 store;
- Action 本质上是 JavaScript 普通对象。我们约定，action 内必须使用一个字符串类型的 type 字段来表示将要执行的动作。多数情况下，type 会被定义成字符串常量。当应用规模越来越大时，建议使用单独的模块或文件来存放 action;
- Action 创建函数: 生成 action 的方法。“action” 和 “action 创建函数” 这两个概念很容易混在一起，使用时最好注意区分;

```js
function addTodo(text) {
  return {
    type: ADD_TODO,
    text
  };
}
```

[slide]
# reducer
------
- Action 只是描述了有事情发生了这一事实，并没有指明应用如何更新 state。而这正是 reducer 要做的事情;
- 在 Redux 应用中，所有的 state 都被保存在一个单一对象中;
- 确定了 state 对象的结构，就可以开始开发 reducer。reducer 就是一个纯函数，接收旧的 state 和 action，返回新的 state。

```js
function todoApp(state = ['first todo'], action) {
  switch(action.type) {
    case ADD_TODO:
      return [...state, action.text];
    default:
      return state;
  }
}
```

[slide]
# Store
------
- 在前面的章节中, 我们学会了使用 action 来描述“发生了什么”，和使用 reducers 来根据 action 更新 state 的用法, Store 就是把它们联系到一起的对象;
- Store 有以下职责：
  - 维持应用的 state;
  - 提供 getState() 方法获取 state;
  - 提供 dispatch(action) 方法更新 state;
  - 通过 subscribe(listener) 注册监听器;
  - 通过 subscribe(listener) 返回的函数注销监听器;

[slide]
# Store
------
- Redux 应用只有一个单一的 store。当需要拆分数据处理逻辑时，应该使用 reducer 组合 而不是创建多个 store。

```js
import { createStore } from 'redux';
import { addTodo } from './actions';
import todoApp from './reducers';
const store = createStore(todoApp);

// 打印初始状态
console.log(store.getState())

// 每次 state 更新时，打印日志
// 注意 subscribe() 返回一个函数用来注销监听器
let unsubscribe = store.subscribe(() =>
  console.log(store.getState())
)

store.dispatch(addTodo('Learn about actions'));

// 停止监听 state 更新
unsubscribe();
```

[slide]
# 创建自己的 React 应用
------
- create-react-app: 使用第三方库 create-react-app 创建自己的 React 应用

  - npm install -g create-react-app
  - create-react-app app-name
  - cd app-name
  - npm start

[slide]
# References
------
- [React tutorial](https://facebook.github.io/react/tutorial/tutorial.html)
- [Redux](http://redux.js.org/docs/introduction/)
- [create-react-app](https://github.com/facebookincubator/create-react-app)    
- [aphrodite](https://github.com/Khan/aphrodite)
- [axios](https://github.com/mzabriskie/axios.git)
- [react-redux](https://github.com/reactjs/react-redux)
- [react-router-redux](https://github.com/reactjs/react-router-redux)
- [react-router](https://github.com/ReactTraining/react-router)
- [webpack](https://webpack.github.io/docs/)
- [快速打造简易高效的 webpack 配置](https://juejin.im/post/595a0ed86fb9a06ba6463cd3?utm_source=gold_browser_extension)
- [Why did we build React?](https://facebook.github.io/react/blog/2013/06/05/why-react.html)