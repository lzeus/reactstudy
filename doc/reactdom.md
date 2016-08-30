# React DOM

## ReactElement

React 中最主要的类型就是 ReactElement。

### 与dom元素的区别

它有四个属性：type，props，key 和 ref。它没有方法，并且原型上什么都没有。
一个 ReactElement 实例是一个轻量的，无状态的，不可变的，是一个虚拟 DOM。

### ReactElement的创建

#### 使用 React.createElement 创建该类型的一个实例。
```javascript
var root = React.createElement('div',null);
```
#### 使用 React JSX 语法，创建该类型的一个实例。
所以，如下代码是等价的：
```javascript
var root = <div></div>;
```

#### 子元素的创建
```javascript
var child = React.createElement('li', null, 'Text Content');//这里的'Text Content'是作为子元素存在的
var root = React.createElement('ul', { className: 'my-list' }, child);
ReactDOM.render(root, document.body);
```
下面为jsx形式
```javascript
var root = <ul className="my-list">
             <li>Text Content</li>
           </ul>;
ReactDOM.render(root, document.body);
```
### ReactElement的渲染
ReactDOM.render 是 React 的最基本方法，用于将模板转为 HTML 语言，并插入指定的 DOM 节点。
API形式如下
`ReactDOM.render(root, document.body);`

## react Node

一个 ReactNode 可以是：
- ReactElement
- string （又名 ReactText）
- number （又名 ReactText）
- ReactNode 实例数组 （又名 ReactFragment）。


这些被用作其它 ReactElement 实例的属性，用于表示子级。
实际上它们创建了一个 ReactElement 实例树。
（These are used as properties of other ReactElements to represent children. Effectively they create a tree of ReactElements.）

## 可扩展的 React 组件

在使用 React 开发中，可以仅使用 ReactElement 实例，但是，要充分利用 React，就要使用 ReactComponent 来封装状态化的组件。

意义在于，自定义组件的render逻辑，制定主键的渲染

一个 ReactComponent 类就是一个简单的 JavaScript 类（或者说是“构造函数”）。
```javascript
var MyComponent = React.createClass({
  render: function() {
    ...
  }
});
```
当该构造函数调用的时候，应该会返回一个对象，该对象至少带有一个 render 方法。该对象指向一个 ReactComponent 实例。
```javascript
var component = new MyComponent(props); // never do this
```
除非为了测试，正常情况下不要自己调用该构造函数。

React 会帮你调用这个函数。

- 把 ReactComponent 类传给 createElement，就会得到一个 ReactElement 实例。
```javascript
var element = React.createElement(MyComponent);
```
- 使用 JSX：
```javascript
var element = <MyComponent />;
```

当该实例传给 ReactDOM.render 的时候，React 将会调用构造函数，然后创建并返回一个 ReactComponent。

```javascript
var component = ReactDOM.render(element, document.body);
```
如果一直用相同的 ReactElement 类型和相同的 DOM 元素容器调用 ReactDOM.render，将会总是返回相同的实例。该实例是状态化的。
```javascript
var componentA = ReactDOM.render(<MyComponent />, document.body);
var componentB = ReactDOM.render(<MyComponent />, document.body);
componentA === componentB; // true
```
这就是为什么不应该创建你自己的实例。相反，在创建之前，ReactElement 是一个虚拟的 ReactComponent。

ReactComponent 的 render 方法应该返回另一个 ReactElement，这就允许组件被组装。

（The render method of a ReactComponent is expected to return another ReactElement. This allows these components to be composed. Ultimately the render resolves into ReactElement with a string tag which instantiates a DOM Element instance and inserts it into the document.）
