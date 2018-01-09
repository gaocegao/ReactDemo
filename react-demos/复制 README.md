## React简介
React 是一个用于构建用户界面的 JAVASCRIPT 库。
React主要用于构建UI，很多人认为 React 是 MVC 中的 V（视图）。
React 起源于 Facebook 的内部项目，用来架设 Instagram 的网站，并于 2013 年 5 月开源。
React 拥有较高的性能，代码逻辑非常简单，越来越多的人已开始关注和使用它。

## React特点
1. 声明式设计 −React采用声明范式，可以轻松描述应用。
2. 高效 −React通过对DOM的模拟，最大限度地减少与DOM的交互。
3. 灵活 −React可以与已知的库或框架很好地配合。
4. JSX − JSX 是 JavaScript 语法的扩展。React 开发不一定使用 JSX ，但我们建议使用它。
5. 组件 − 通过 React 构建组件，使得代码更加容易得到复用，能够很好的应用在大项目的开发中。
6. 单向响应的数据流 − React 实现了单向响应的数据流，从而减少了重复代码，这也是它为什么比传统数据绑定更简单。

## HTML 模板

```html
<!DOCTYPE html>
<html>
  <head>
    <script src="../build/react.js"></script>  
    <script src="../build/react-dom.js"></script>
    <script src="../build/browser.min.js"></script>
  </head>
  <body>
    <div id="example"></div>
    <script type="text/babel">

      // ** 代码写在这**

    </script>
  </body>
</html>
```
react.min.js - React 的核心库
react-dom.js - 提供与DOM的相关功能
browser.min.js - 提供对JSX的支持，将JSX语法转为JavaScript语法


## Demo01: ReactDOM.render()
ReactDOM.reader是React的基本方法，用于将模块转化为HTML语言，并插入到指定的DOM节点
```js
ReactDOM.render(
  <h1>Hello, world!</h1>,
  document.getElementById('example')
);
```
上述代码将h1标题插入到id='example'节点中

## Demo02: JSX语法

```js
var names = ['Alice', 'Emily', 'Kate'];

ReactDOM.render(
  <div>
  {
    names.map(function (name) {
      return <div>Hello, {name}!</div>
    })
  }
  </div>,
  document.getElementById('example')
);
```
上面代码体现了 JSX 的基本语法规则：遇到 HTML 标签（以 < 开头），就用 HTML 规则解析；遇到代码块（以 { 开头），就用 JavaScript 规则解析。上面代码的运行结果如下。


```js
var arr = [
  <h1>Hello world!</h1>,
  <h2>React is awesome</h2>,
];
ReactDOM.render(
  <div>{arr}</div>,
  document.getElementById('example')
);
```
上面代码的arr变量是一个数组，结果 JSX 会把它的所有成员，添加到模板
## Demo03: 组件
React可以将代码封装成组件，像插入普遍HTML标签一样在网页中插入这个组件。
Reac.createClass方法就是创建一个组件类。

```javascript
var HelloMessage = React.createClass({
  render: function() {
    return <h1>Hello {this.props.name}</h1>;
  }
});

ReactDOM.render(
  <HelloMessage name="zhangsan" />,
  document.getElementById('example')
);
```
上述代码组件类名首字母必须大写，不然会报错。组件的用法和原生的HTML标签一致，可以加入任意属性。
比如HelloMessage组件中加入了name属性，值为zhangsan。组件类中通过this.props.name获取。



## Demo04: this.props.children

```javascript
var NotesList = React.createClass({
  render: function() {
    return (
      <ol>
      {
        React.Children.map(this.props.children, function (child) {
          return <li>{child}</li>;
        })
      }
      </ol>
    );
  }
});

ReactDOM.render(
  <NotesList>
    <span>hello</span>
    <span>world</span>
  </NotesList>,
  document.getElementById('example')
);
```
this.props 对象的属性与组件的属性一一对应，但是有一个例外，就是 this.props.children 属性。它表示组件的所有子节点。
React.Children.map用来遍历子节点。

## Demo05 getDefaultProps默认属性
getDefaultProps 方法可以用来设置组件属性的默认值。下面代码会输出Hello World。
```js
var MyTitle = React.createClass({
  getDefaultProps : function () {
    return {
      title : 'Hello World'
    };
  },

  render: function() {
     return <h1> {this.props.title} </h1>;
   }
});

ReactDOM.render(
  <MyTitle />,
  document.body
);
```
## Demo06 React State(状态)
```js
  var Component = React.createClass({
  	getInitialState: function(){
  		return {liked:false};
  	},
  	handleClick: function(){
  		this.setState({liked: !this.state.liked});
  	},
  	render: function(){
  		var text = this.state.liked ? '喜欢':'不喜欢';
  		return (
  			<p onClick={this.handleClick}>
  			  你<strong>{text}</strong>我?点击我切换状态.
  			</p>
  		);
  	}
  });

ReactDOM.render(
	<Component/>,
	document.getElementById('example')
);
```
React 把组件看成是一个状态机（State Machines）。通过与用户的交互，实现不同状态，然后渲染 UI，让用户界面和数据保持一致。

React 里，只需更新组件的 state，然后根据新的 state 重新渲染用户界面（不要操作 DOM）。

以下实例中创建了 LikeButton 组件，getInitialState 方法用于定义初始状态，也就是一个对象，这个对象可以通过 this.state 属性读取。当用户点击组件，导致状态变化，this.setState 方法就修改状态值，每次修改以后，自动调用 this.render 方法，再次渲染组件。