##什么是react?
一个JavaScript库，用于构建用户交互界面
##react的优势是什么？
- 声明式组件
- 支持部分渲染，节约内存资源，并且渲染速度非常快
- 支持服务端和客户端渲染
- 单向数据流
- 集成简单
- 易于测试
##如何使用react?
###预备知识

 html,css,js,es6 <br/>
 es6参考地址:<br/>
 [火狐官网](https://developer.mozilla.org/en-US/docs/Web/JavaScript/A_re-introduction_to_JavaScript)
[es6](http://es6.ruanyifeng.com/)

###环境准备
  node.js npm react-dev-tools
  ```
  npm install -g create-react-app
  create-react-app my-app
  
  cd my-app
  npm start
  ```
hello world
    
  ```
  ReactDOM.render(
    <h1>Hello, world!</h1>,
    document.getElementById('root')
  );
  ```
###React Component
####组件的书写方式
- functional component

 ```
 function Welcome(props) {
   return <h1>Hello, {props.name}</h1>;
 }
```
 
- class component

```
class Welcome extends React.Component {
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}
```
 
区别：class方式书写的组件可以进行生命周期管理和操作State
###Props and State
####区别
state中的数据是可变的，而props则是不可变的
####选取原则
如果是需要组件调用者来指定时使用props,如果是组件自身的状态改变则使用state
###Event
与html中的事件绑定十分类似，主要注意的是react中的事件是驼峰方式进行命名，并且在事件处理函数中收到的事件对象参数是
经过react进行统一处理过后的合成事件对象。

```
class NameInput extends React.Component {
  handleInputChange = (e) => {
    console.log('the input value:', e.target.value);
  }

  render() {
    return (
      <input onClick={this.handleInputChange}/>
    );
  }
}
```
###Lifecycle management

####Mounting
These methods are called when an instance of a component is being created and inserted into the DOM:

- constructor() 在创建组件实例的时候调用
- componentWillMount() 在实例被载入之前调用
- render() 在渲染组件时调用
- componentDidMount() 在实例被载入之后调用
####Updating
An update can be caused by changes to props or state. These methods are called when a component is being re-rendered:

- componentWillReceiveProps()已被载入组件的props发生改变时调用
- shouldComponentUpdate()在render方法之前被调用，如果该方法返回false则不会对组件进行重新渲染
- componentWillUpdate()在更新组件之前调用
- render()在组件的props或state发生改变时重新渲染组件的更新的内容
- componentDidUpdate()在组件更新之后调用
####Unmounting

- componentWillUnmount() 在组件被移除出DOM之前调用


###注意事项：
- 在组件中永远不要去修改props
- 组件的返回值一定要是一个单节点的元素
- 自定义组件的名称要首字母大写