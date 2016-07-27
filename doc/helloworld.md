# react 初体验
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
```
## jsx语法中的xml段，都会被编译为React.createElement
```javascript
setInterval(function() {
  React.render(
    <HelloWorld date={new Date()} />, //设置HelloWorld元素相关的属性 this.props.date = new Date();
    document.getElementById('example')
  );
}, 500);
```

会被jsx编译为
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