# 使用属性
## 示例
### 示例-编译前
```javascript
var Comment = React.createClass({
  render: function() {
    return (
      <div className="comment">
        <h2 className="commentAuthor">
          {this.props.author}
        </h2>
        {this.props.children}
      </div>
    );
  }
});
var CommentList = React.createClass({
  render: function() {
    return (
      <div className="commentList">
        <Comment author="Pete Hunt">This is one comment</Comment>
        <Comment author="Jordan Walke">This is *another* comment</Comment>
      </div>
    );
  }
});
```

需要注意的是，当组件xml中使用到js变量时，需要将变量用{}引用起来
### 示例-编译后
```javascript
var Comment = React.createClass({displayName: "Comment",
  render: function() {
    return (
      React.createElement("div", {className: "comment"}, 
        React.createElement("h2", {className: "commentAuthor"}, 
          this.props.author
        ), 
        this.props.children
      )
    );
  }
});
var CommentList = React.createClass({displayName: "CommentList",
  render: function() {
    return (
      React.createElement("div", {className: "commentList"}, 
        React.createElement(Comment, {author: "Pete Hunt"}, "This is one comment"), 
        React.createElement(Comment, {author: "Jordan Walke"}, "This is *another* comment")
      )
    );
  }
});
```
## 传递动态数据示例
### 传递动态数据示例-编译前
```javascript
var data = [
  {author: "Pete Hunt", text: "This is Pete Hunt's comment"},
  {author: "Jordan Walke", text: "This is Jordan Walke's comment"},
  {author: "Larry", text: "This is Larry's comment"}
];


var Comment = React.createClass({
  render: function() {
    return (
      <div className="comment">
        <h2 className="commentAuthor">{this.props.author}</h2>
        <h4>{this.props.children.toString()}</h4>
      </div>
    );
  }
});


var CommentList = React.createClass({
  render: function() {
    var commentNodes = this.props.data.map(function (comment) {
      return (
        <Comment author={comment.author}>
          {comment.text}
        </Comment>
      );
    });
    return (
      <div className="commentList">
        {commentNodes}
      </div>
    );
  }
});

var CommentBox = React.createClass({
  render: function() {
    return (
      <div className="commentBox">
        <h1>Comments</h1>
        <CommentList data={this.props.data} />
      </div>
    );
  }
});

ReactDOM.render(
  <CommentBox data={data} />,
  document.getElementById('example')
);
```

### 传递动态数据示例-编译后面
```javascript
var data = [
  {author: "Pete Hunt", text: "This is Pete Hunt's comment"},
  {author: "Jordan Walke", text: "This is Jordan Walke's comment"},
  {author: "Larry", text: "This is Larry's comment"}
];


var Comment = React.createClass({displayName: "Comment",
  render: function() {
    return (
      React.createElement("div", {className: "comment"}, 
        React.createElement("h2", {className: "commentAuthor"}, this.props.author), 
        React.createElement("h4", null, this.props.children.toString())
      )
    );
  }
});


var CommentList = React.createClass({displayName: "CommentList",
  render: function() {
    var commentNodes = this.props.data.map(function (comment) {
      return (
        React.createElement(Comment, {author: comment.author}, 
          comment.text
        )
      );
    });
    return (
      React.createElement("div", {className: "commentList"}, 
        commentNodes
      )
    );
  }
});

var CommentBox = React.createClass({displayName: "CommentBox",
  render: function() {
    return (
      React.createElement("div", {className: "commentBox"}, 
        React.createElement("h1", null, "Comments"), 
        React.createElement(CommentList, {data: this.props.data})
      )
    );
  }
});

ReactDOM.render(
  React.createElement(CommentBox, {data: data}),
  document.getElementById('example')
);
```

