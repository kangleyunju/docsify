### Vue2和vue3的区别
* vue2使用到object.definepropoty， 通过遍历每一层的属性实现监听，直接改动原始对象，通过get和set函数，来设置和读取属性，但是不能监听对象新增和删除属性
* vue3使用proxy， new proxy()，监听的是整个整个对象，产生的是一个新的对象

### vue双向绑定的原理|vue相应式原理
* 数据劫持，通过object.definepropoty这个方法，遍历data每个数据，进行数据劫持， 里面有setter和getter函数，当数据发生变化时，会通过，setter函数会通知依赖收集器，而这个依赖收集器通知订阅该属性的watch
* 发布者-订阅者模式， 结合虚拟dom技术， 这个观察者watch会通过diff算法，差异化算法，仅更新发生变化的部分，避免了全量更新产生的性能问题

### v-model 的原理是什么
1. 绑定值
2. 事件监听,监听值的变化
3. 设置值,更新视图

### MVVM开发模式的理解
* Model 代表数据模型，存储数据和业务逻辑
* View  代表UI视图，负责数据的展示；
* ViewModel 负责监听模型中数据的改变，并且控制视图的更新
* model和view并无直接关联，而是通过viewmode来进行联系的，因此当 Model 中的数据改变时会触发 View层的刷新，view中由于用户交互操作而改变的数据也会在 Model 中同步

### mvc和mvvm的区别
* mvc 是单向数据改变，默认只是 model 的改变，进而控制 view
* 而 mvvm 是双向改变， model 和 view自动更新
* mvvm对控制器进行了瘦身

### vue跳转的方式
* 标签跳转<router-link to="url"/>  
* this.$router.push('/')
* this.$router.push(path:path，qury)
* this.$router.push(name:name，params)

### comuted和watch的区别
* computed ：多个属性来确定一个值推荐computed ，通过return返回，会缓存，只要数据不发生变化，就使用缓存的数据，不支持异步
* watch：一个值的变化引起一系列操作用watch，两个参数，分别是newval和oldval，另外可以深度监听，deep和立即监听immediately，可以异步，不会缓存 

### vue生命周期
* 创建前后，created
* 挂载前后，mounted
* 更新前后，updated，
* 销毁前后，destroyed

### vuex
状态管理工具，用途是集中管理所有的组件，实现组件之间的数据共享，是专门管理数据的工具
1. state 保存数据
2. mutation 改变数据的方法，同步  this.$store.commit(方法名，提交的数据)，触发mutation就意味新的状态的更新，如果mutatiuon是异步的就不知道状态何时变更
3. action 改变数据，异步，然后分发mutation进行操作，this.$store.dispatch(方法名，提交的数据)，api调用，setTimeout等，
4. getter 计算属性的方法
5. modules 模块化，拆分store

### keep-alive
把切换出去的组件保留在内存中，可以保留它的状态或避免重新渲染，从a页面到b页面再回来，不用重新渲染， 对应了两个生命周期，激活时actived，未激活deactived
* include，要缓存的组件
* exclude，不要缓存的组件
* max，最多缓存几个组件

### slot插槽
可以向插槽的地方添加任何内容，甚至是一个组件,name命名插槽的名字
* 默认插槽<slot></slot>
* 具名插槽<slot name="left"></slot>


### vue3 setup
1. 组合式api,更好的逻辑复用
2. ref和reactive都是将非响应式的值转化成响应式对象,reactive可以包含多个属性

### 微前端的优点
1. 便于独立开发独立部署
2. 可维护性更好,便于局部更新增量更新
3. 技术兼容好,适用于不同框架

### 微前端的缺点
1. 子应用之间资源共享能力较差,代码总体积变大

### qiankuan的原理
1. 应用加载：单页面single-spa解决了路由和应用入口的问题,但是没有解决应用加载的问题,qianKun利用import-html-entry这个库解决了应用加载,那么这个库的作用就是获取子应用里面的css,js放到html里面,将html作为入口文件,很好解决了js隔离,css隔离和应用通信的问题
2. js隔离：import-html-entry,为每个子应用生成一个window的代理对象,防止子应用js全局污染
3. css隔离：给每个根节点添加一个特殊属性,类似于scoped属性
4. 应用通信：全局的globalState对象用来保存全局变量,通过setGlobalState修改变量,onGlobalStateChange监听变量

### vite和webpack的区别
1. webpack：所有模块都进行编译
2. vite：启动的时候不需要打包，因为浏览器本身支持ES Modules，碰到一个impiort就会发送一个http请求去加载文件,并在后端进行简单的分解和整合返回给浏览器,vite在整个过程中没有对文件进行编译打包,真正做到按需加载，底层上是基于es build进行预构建的，es build是通过go语言编写的，比js快

