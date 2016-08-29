# react 初体验
## react html模版
一个典型的react html页面代码大致如下
```html
<!DOCTYPE html>
<html>
  <head>
  	<!-- React 的核心库 -->
    <script src="../build/react.js"></script>
    <!-- 提供与 DOM 相关的功能 -->
    <script src="../build/react-dom.js"></script>
    <!-- 将 JSX 语法转为 JavaScript 语法
    包括将ES6转换为ES5
    这一步很消耗时间，
    实际上线的时候，应该将它放到服务器完成 
    -->
    <script src="../build/browser.min.js"></script>
  </head>
  <body>
    <div id="example"></div>
    <!--
    React 独有的 JSX 语法，跟 JavaScript 不兼容.
    凡是使用 JSX 的地方，都要加上 type="text/babel".
    -->
    <script type="text/babel">
    	
    	var names = ['Alice', 'Emily', 'Kate'];

		ReactDOM.render(
  			<div>
  				{
    			names.map(function (name) {
      			return <div>Hello, {name}!</div>
    			})
  				}
  			</div>,document.getElementById('example')
		);
    </script>
  </body>
</html>
```

## JSX基本语法规则

-  遇到 HTML 标签（以 < 开头），就用 HTML 规则解析
-  遇到代码块（以 { 开头），就用 JavaScript 规则解析

## 定义react组件
```javascript
var HelloWorld = React.createClass({
        render: function() {
          return (
            <p>Hello, <input type="text" placeholder="Your name here" />!It is {this.props.date.toTimeString()}</p>
          );
          //这里的<p><input>标签不是真正的 DOM 节点；他们是 React p div组件的实例。
          //你可以认为这些标签就是一些标记或者数据， React知道如何处理它们
        }
      });
      
setInterval(function() {
  //ReactDOM.render() 实例化根组件，启动框架，把标记注入到第二个参数指定的原生的 DOM 元素中。
  React.render(
    <HelloWorld date={new Date()} />, //设置HelloWorld元素相关的属性 this.props.date = new Date();
    document.getElementById('example')
  );
}, 500);
```
## jsx语法中的xml段，都会被编译为React.createElement
```javascript
var HelloWorld = React.createClass({displayName: "HelloWorld",
        render: function() {
          return (
            React.createElement("p", null, "Hello, ", React.createElement("input", {type: "text", placeholder: "Your name here"}), "!It is ", this.props.date.toTimeString())
          );
        }
      });

setInterval(function() {
  React.render(
    React.createElement(HelloWorld, {date: new Date()}),
    document.getElementById('example')
  );
}, 500);
```
