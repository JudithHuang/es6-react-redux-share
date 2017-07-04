title: React
speaker: Judith Huang
url: https://github.com/judithhuang/es6-react-redux-share
transition: slide
theme: dark
date: 2017年7月03号

[slide]
# React & Redux
<small>演讲者：Judith Huang</small>

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
# JSX 语法
------
- 标签的使用: React 可以渲染 HTML 标签 (strings) 或 React 组件;
- 使用 JavaScript 表达式: 我们可以在 JSX 中使用  JavaScript 表达式。表达式写在花括号 `{}` 中;
- 数组: JSX 允许在模板中插入数组，数组会自动展开所有成员;
- 注释: 需要写在花括号中, 如: `{/* 这是一个 jsx 注释 */}`;

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
- [React 中文](https://chenyitian.gitbooks.io/react-docs/content/docs/02.1-jsx-in-depth.html)
- [Redux 中文](http://cn.redux.js.org/)
- [Why did we build React?](https://facebook.github.io/react/blog/2013/06/05/why-react.html)
- [create react app](https://github.com/facebookincubator/create-react-app)    
- [webpack](https://webpack.github.io/docs/)
- [axios](https://github.com/mzabriskie/axios.git)
- [react-router](https://github.com/ReactTraining/react-router)
