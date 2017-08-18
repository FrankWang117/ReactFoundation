# React ES5与ES6语法写法比较  
## 安装  
从React官网找到[安装](http://www.css88.com/react/docs/installation.html)地址，下载html文件，查看源码：

```
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <title>Hello World</title>
    <script src="https://unpkg.com/react@latest/dist/react.js"></script>
    <script src="https://unpkg.com/react-dom@latest/dist/react-dom.js"></script>
    <script src="https://unpkg.com/babel-standalone@6.15.0/babel.min.js"></script>
  </head>
  <body>
    <div id="root"></div>
    <script type="text/babel">

      ReactDOM.render(
        <h1>Hello, world!</h1>,
        document.getElementById('root')
      );

    </script>
  </body>
</html>

```
文件首先加载了“react.js" "react-dom.js"两个最基本的库与DOM操作相关的 功能。后又加载了”babel.min.js“	，官方建议：它会执行一个缓慢的运行时代码转换，所以不要在生产环境使用它。
官网上还提供另外两种安装React的方法。
## Hello，World [Hello demo](https://github.com/FrankWang1991/ReactFoundation/tree/master/Demo01-Helloworld)
万丈高楼平地起，万行代码起于此。每个新编码都从hello，world说起，这个也不例外。分析”安装“里提到的文件。
	可以看到在`<body>` 标签中添加了`<script type="text/babel">` ，这是代表使用了[JSX语法](http://www.css88.com/react/docs/introducing-jsx.html)。
	在Html文件中有`<div id="root"></div>` 这样的根节点。要渲染一个React元素到一个根DOM节点，把他们传递给`ReacDOM.render()`方法。如上图所示。  
## 组件Components  
   React 中可以将代码封装成一个个可以复用的组件，并且可以对每个组件进行单独设置，比如进度条这种组件。可以用在音乐播放进度，亦可以用在音量控制。
   组件命名**第一个字母必须大写**，因为组件必须返回一个单独的根元素，所以组件类的**顶级标签只能有一个**，否则会报错。如里面有两个元素，顶层需要用一个`<div>`元素将其包裹起来。
使用**ES6**定义一个组件：
	
	
```
    <script type="text/babel">
      class HelloComponents extends React.Component{
          render(){
            return (
            <div>
              <h1>Hello,Components</h1>
              <p>this is use ES6</p>
            </div>
            )
        }
    }
      ReactDOM.render(
        <HelloComponents />,
        document.getElementById('root')
      );
    </script>
```
使用**ES5**定义一个组件：

```
    <script type="text/babel">
      var HelloComponents = React.createClass({
      render:function(){
      return(<h1>Hello,Components (use ES5)</h1>)
    }
    })

      ReactDOM.render(
        <HelloComponents />,
        document.getElementById('root')
      );
    </script>
```
## 默认属性props  
可以给组件设置相关的特性，其是不可更改的。有别于下文的state
使用**ES6**来设置默认属性：
在组件外，使用`组件.defaultProps` 设置组件的固有属性。
```
    <script type="text/babel">
      class SetProps extends React.Component{
          render(){
            return (
            <div>
              <h1>Hello,{this.props.name}</h1>
              <p>{this.props.name}的性别是：{this.props.sex}</p>
              <p>this is use ES6</p>
            </div>
            )
        }
    }
    SetProps.defaultProps = {
        name:"LiLei",
        sex:"male",
  }
      ReactDOM.render(
        <SetProps />,
        document.getElementById('root')
      );
    </script>
```
使用**ES5**来设置默认属性：
使用`getDefaultProps`方法设置默认属性。
```
    <script type="text/babel">
      var SetProps = React.createClass({
        getDefaultProps:function(){
          return {
            name:"HanMeiMei",
            sex:"Female"
        }
      },
        render:function(){
          return(
          <div>
            <h1>Hello,{this.props.name}</h1>
            <p>{this.props.name}的性别是：{this.props.sex}</p>
            <p>this is use ES5</p>
          </div>)
        }
    })
      ReactDOM.render(
        <SetProps />,
        document.getElementById('root')
      );
    </script>
```
需要注意的是在ES5中每个方法的结尾需要用逗号来分隔开。因为其是对象的方法。
## 初始化状态State  
也是用来设置组件的特性，但是可以随着用户的交互而发生改变，区别于props。
不要直接修改`state`，需要使用`this.setState()`方法
使用**ES6**来设置状态：
在`constructor` 中使用 `this.state` 设置初始状态。其中 `constructor` 方法不设置的时候默认添加。
```
    <script type="text/babel">
      class SetProps extends React.Component{
        constructor(){
          super();
          this.state={
            age:18,
        }}
          render(){
            return (
            <div>
              <h1>Hello,{this.props.name}</h1>
              <p>{this.props.name}的性别是：{this.props.sex},年龄是{this.state.age}</p>
              <p>this is use ES6</p>
            </div>
            )
        }
    }
    SetProps.defaultProps = {
        name:"LiLei",
        sex:"male",
  }
      ReactDOM.render(
        <SetProps />,
        document.getElementById('root')
      );
    </script>
```
使用**ES5**来设置状态：	
使用`getInitialState` 方法设置初始状态。
```
      var SetProps = React.createClass({
        getDefaultProps:function(){
          return {
            name:"HanMeiMei",
            sex:"Female"
        }
      },
        getInitialState :function(){
          return {age:20}
    },
        render:function(){
          return(
          <div>
            <h1>Hello,{this.props.name}</h1>
            <p>{this.props.name}的性别是：{this.props.sex},年龄是:{this.state.age}</p>
            <p>this is use ES5</p>
          </div>)
        }
    })
      ReactDOM.render(
        <SetProps />,
        document.getElementById('root')
      );
    </script>
```
##  Function 函数
使用**ES6**来设置函数：	
方法不会自动绑定 this 到实例中，需要在构造函数中显示的使用`.bind(this)`:
下面这个例子，当用户点击按钮时，会更改状态，也就是本例中的`age`值。
```
    <script type="text/babel">
      class SetFunction extends React.Component{
        constructor(){
          super();
          this.state={
            age:18,
        };
        //这句是必须的。
        this.ChangeAge = this.ChangeAge.bind(this);
      }
        ChangeAge(){
        //this.setState此方法修改状态值。
          this.setState({
          age : this.state.age + 1
        })
      }
         render(){
            return (
            <div>
              <h1>Hello,{this.props.name}</h1>
              <p>{this.props.name}的性别是：{this.props.sex},年龄是:{this.state.age}</p>
              <p>this is use ES6</p>
              <button type="button" onClick={this.ChangeAge}>change age</button>
            </div>
            )
        }
    }
    SetFunction.defaultProps = {
        name:"LiLei",
        sex:"male",
  }
      ReactDOM.render(
        <SetFunction />,
        document.getElementById('root')
      );
    </script>
```
如果不想显式的在类构造函数中绑定`this`，亦可以使用 箭头函数进行书写：
以上面的代码作为实例(-代表删去此行。+代表增加或修改此行)：
```
- this.ChangeAge = this.ChangeAge.bind(this);
+ <button type="button" onClick={(e)=>this.ChangeAge(e)}>change age</button>
```

使用**ES5**来设置函数：
方法可以自行绑定。
```
    <script type="text/babel">
      var SetProps = React.createClass({
        getDefaultProps:function(){
          return {
            name:"HanMeiMei",
            sex:"Female"
        }
      },
        getInitialState :function(){
          return {age:20}
      },
      //设置函数
        ChangeAge:function(){
          this.setState({
          age:this.state.age+ 1
        })
    },
        render:function(){
          return(
          <div>
            <h1>Hello,{this.props.name}</h1>
            <p>{this.props.name}的性别是：{this.props.sex},年龄是:{this.state.age}</p>
            <p>this is use ES5</p>
            //给button绑定函数
            <button type="button" onClick={this.ChangeAge}>ChangeAge</button>
          </div>)
        }
    })
      ReactDOM.render(
        <SetProps />,
        document.getElementById('root')
      );
    </script>
```
