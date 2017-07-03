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
# React 简介

[slide]
# JSX
------
- 简介
JSX语法，像是在Javascript代码里直接写XML的语法，实质上这只是一个语法糖，每一个XML标签都会被JSX转换工具转换成纯Javascript代码，React 官方推荐使用JSX， 当然你想直接使用纯Javascript代码写也是可以的，只是使用JSX，组件的结构和组件之间的关系看上去更加清晰。

```js
const arr = [
  <h1>我是一级标题</h1>,
  <h2>我是二级标题</h2>,
];

React.render(
  <div>
    <div>
      <div>content</div>
      <div>表达式: { 1 + 2 }</div>
      {/* 模板中插入数组，数组会自动展开所有成员 */}
      { arr }
    </div>
  </div>,
  document.getElementById('example')
);
```

[slide]
# JSX 陷阱
------
- style属性: 不能采用引号的书写方式
- HTML转义: 内容是用户输入的富文本，从后台取到数据后展示在页面上，希望展示相应的样式

```js
var content='<strong>content</strong>';
 
React.render(
    <div 
        style={{color:'red'}}
        dangerouslySetInnerHTML={{__html: content}}
    >   
        {/* content */}
        {/* 直接输出内容: <strong>content</strong> */}
    </div>,
    document.body
);
```

[slide]
# 渲染元素

[slide]
# Refs 和 DOM

[slide]
# 组件

[slide]
# 状态(State)

[slide]
# 生命周期

[slide]
# 处理事件

[slide]
# 表单

[slide]
# 受控组件(Controlled Components)

[slide]
# 不受控的组件

[slide]
# 状态提升(Lifting State Up)

[slide]
# 组合和继承对比（Composition vs Inheritance）

[slide]
# Redux 简介
随着 JavaScript 单页应用开发日趋复杂，JavaScript 需要管理比任何时候都要多的 state （状态）。 这些 state 可能包括服务器响应、缓存数据、本地生成尚未持久化到服务器的数据，也包括 UI 状态，如激活的路由，被选中的标签，是否显示加载动效或者分页器等等。    
管理不断变化的 state 非常困难。如果一个 model 的变化会引起另一个 model 变化，那么当 view 变化时，就可能引起对应 model 以及另一个 model 的变化，依次地，可能会引起另一个 view 的变化。直至你搞不清楚到底发生了什么。state 在什么时候，由于什么原因，如何变化已然不受控制。 当系统变得错综复杂的时候，想重现问题或者添加新功能就会变得举步维艰。

[slide]
# Action

[slide]
# reducer

[slide]
# 数据流

[slide]
# 搭配 React

[slide]
# References
------
- [React tutorial](https://facebook.github.io/react/tutorial/tutorial.html)
- [Redux](http://redux.js.org/docs/introduction/)
