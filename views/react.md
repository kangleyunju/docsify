### React介绍
是前端的框架，facebook出的前端js库，遵循组件的方法，有助于构建可重用的ui组件，主要特点：使用虚拟dom，服务器端渲染，单向数据流(或数据绑定)
提高了应用的性能，可以方便地在客户端和服务器端使用，由于react里面有jsx(js xml)，代码的可读性更好，是一种文件，可以使html文件容易理解，提高程序性功能，js的语法扩展
* 优点：它提高了应用的性能，可以方便地在客户端和服务器端使用，由于JSX，代码的可读性很好，使用React，编写UI测试用例变得非常容易
* 缺点：React 只是一个库，而不是一个完整的框架，它的库非常庞大，需要时间来理解，编码变得复杂，因为它使用内联模板和JSX

### jsx
react的语法糖，它允许在html中写JS，它不能被浏览器直接识别，需要通过webpack、babel之类的编译工具转换为JS执行

### 状态提升
是指将组件间共享的状态提升到它们的最近公共父组件中进行管理

### hooks
* 16.8加入的,为了解决代码复用难的问题,使function组件可以管理state和生命周期
* useState,useRouter等

### 纯函数
一个函数的返回结果只依赖于它的参数，并且在执行的过程中没有副作用，我们就把该函数称作纯函数 
```
//非纯函数
function  add ( a,  b ){
	console.log( a + b*Math.random() )
}
//纯函数
function  add ( a,  b ){
	return  a + b*0.5
}
```

### 高阶函数
接收一个组件作为参数并返回一个新组件的函数,作用是
1. 代码复用
2. 状态管理,将共享状态注入到组件中
3. 渲染劫持,通过props和state来控制渲染过程

### 函数组件和类组件
* 函数组件:只是单纯的数据展示
```
import React from 'react';
function Hello(props) {
  return <div>Hello, {props.name}!</div>;
}
export default Hello;
```
* 类组件:处理事件,需要保存状态等复杂逻辑,有自己的状态和生命周期,需要声明constuctor,需要手动绑定this,需要继承class
```
class Hello extends React.Component {}
```

### react生命周期
1. 挂载
constructor()
render()
componentDidMount()

2. 更新
shouldComponentUpdate()
componentDidUpdate()//组件完成更新后

3. 卸载
componentWillUnmount  ()

4. 错误捕获
componentDidCatch ()


### 组件传值
1. 父向子:props传递
2. 子传父:向子组件传一个回调函数,ref调用子组件方法,利用事件冒泡传递出去
3. 兄弟组件:需要一个父组件作为中介,a->父->b
4. 父组件向后代组件通信,可以在父组件中创建一个context对象，并通过Provider组件向子孙组件提供该context
```
const MyContext = React.createContext();
//父
<MyContext.Provider value={{ message: 'Hello, World!' }}>
	<Child />
</MyContext.Provider>
//子
const { message } = React.useContext(MyContext);
```

### react优化
1. webpack配置第三方插件去掉打印
2. 第三方包使用cdn优化, 配置生产环境
3. 路由懒加载,lazy函数,supense组件

### react怎么实现路由跳转
1. <link to>
2. history.push