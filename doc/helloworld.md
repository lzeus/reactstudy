```javascript
var HelloWorld = React.createClass({
        //定义HelloWorld元素
        render: function() {
          return (
            <p>Hello, <input type="text" placeholder="Your name here" />!It is {this.props.date.toTimeString()}</p>
          );
        }
      });

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
