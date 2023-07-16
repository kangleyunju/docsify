### Vue2和vue3的区别
1. vue2使用到object.definepropoty， 通过遍历每一层的属性实现监听，直接改动原始对象，通过get和set函数，来设置和读取属性，但是不能监听对象新增和删除属性，vue3使用es6的proxy， new proxy()，监听的是整个整个对象，当数据发生变化时进行视图更新
2. vue2中v-for层级更高,vue3中v-if层级更高
3. 插槽写法不一样,vue3是#slot
4. 定义全局变量不一样,vue2是Vue.prototype,vue3是app.config.globalProperties
5. 生命周期不一样
6. vue3可以没有根元素,可以没有template

### vue生命周期
|					| Vue2					| vue3						|
| ---			| ---						| ---							|
| 创建前	| beforeCreate	| setup						|
| 创建后	| created				| setup						|
| 挂载前	| beforeMount		| onBeforeMount		|
| 挂载后	| mounted				| onMounted				|
| 更新前	| beforeUpdate	|onBeforeUpdate		|
| 更新后	| updated				| onUpdated				|
| 卸载前	| beforeDestroy	| onBeforeUnmount	|
| 卸载后	| destroyed			| onUnmounted			|
| 组件显示| activated			| onActiveted			|
| 组件隐藏| deactivated		| onDeactivated		|
| 捕获错误| errorCaptured	| onErrorCaptured	|

### vue父子组件生命周期顺序
父beforeCreate-> 父create -> 子beforeCreate-> 子created -> 子mounted -> 父mounted

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

### vuex
状态管理工具，用途是集中管理所有的组件，实现组件之间的数据共享，是专门管理数据的工具，保存在运行内存里面
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
1. 组合式api，更好的逻辑复用
2. ref和reactive都是将非响应式的值转化成响应式对象，reactive可以包含多个属性，给每个对象都包一层 Proxy，通过 Proxy 监听属性的变化
```
import {toRefs,reactive} from "vue"
const data=reactive({
	name:'张飞',
	age:28
})
const dataToRefs=toRefs(data)
return {...dataToRefs}
```

### 微前端的优点
1. 便于独立开发独立部署
2. 可维护性更好，便于局部更新增量更新
3. 技术兼容好，适用于不同框架

### 微前端的缺点
1. 子应用之间资源共享能力较差，代码总体积变大

### qiankuan的原理
1. 应用加载：单页面single-spa解决了路由和应用入口的问题，但是没有解决应用加载的问题，qianKun利用import-html-entry这个库解决了应用加载，那么这个库的作用就是获取子应用里面的css，js放到html里面，将html作为入口文件，很好解决了js隔离，css隔离和应用通信的问题
2. js隔离：import-html-entry，为每个子应用生成一个window的代理对象，防止子应用js全局污染
3. css隔离：给每个根节点添加一个特殊属性，类似于scoped属性
4. 应用通信：全局的globalState对象用来保存全局变量，通过setGlobalState修改变量，onGlobalStateChange监听变量

### vite，webpack，rollup的区别
1. webpack：所有模块都进行编译，拥有庞大的插件生态系统
2. vite：启动的时候不需要打包，因为浏览器本身支持ES Modules，碰到一个import就会发送一个http请求去加载文件,并在后端进行简单的分解和整合返回给浏览器,vite在整个过程中没有对文件进行编译打包,真正做到按需加载，底层上是基于es build进行预构建，es build是通过go语言编写的，比js快,正式环境线上用到了rollup,打包体积更小,支持相对路径,使用到新的esmodel
3. rollup：在打包过程中使用静态分析，确定模块的依赖关系，这样可以更好地进行Tree Shaking，将所有的模块转换成ES6模块，然后将它们合并成一个文件，按需打包，消除未使用的代码，体积更小

### vue优化
1. v-for时,key尽量使用特定的id,diff算法可以减少判断
2. 第三方插件按需引入
3. 图片懒加载,压缩图片,使用精灵图,避免使用大图片
4. 长列表展示可以采取虚拟滚动,只展示可视区域的数据,vue-virtual-scroller / vue-virtual-scroll-list
5. vue2中,v-for比v-if的层级更高,需要注意下
6. webpack开启压缩,gzip
7. 减少http请求,优化请求
8. 合理使用缓存

### vue-loader
解析vue文件的template、script 和 style,转成js,css,html

### vue项目seo优化
1. nuxt.js
2. 设置mete标签,设置一些合理的title、description                                                                     
3. keywords关键字
4. 创建一个站点地图,包行所有内容的XML文件,可以帮助搜索引擎了解你的网站,比如第三方库vue-sitemap
5. img填写alt,增加图片的相关性

### webpack
* loader本质上是一个函数，它的作用是将某个源码字符串转换成另一个源码字符串返回,如clean-log-loader去除打印
* plugin是通过扩展webpack功能，加入自定义的构建行为,html-webpack-plugin: 自动生成页面

### watch和watchEffect的区别
* watchEffect会立即监听,watch需要immediately
* watchEffect会根据其中的属性，自动监听其变化
```
watch(
  () => number.count,
  (newValue, oldValue) => {
    console.log("新的值:", newValue);
    console.log("旧的值:", oldValue);
  },
  { deep: true }
)
watchEffect(()=>{
  console.log("新的值:", number.count);
})
```

### vue中的data为什么是函数
防止多个组件之间共用一个data,产生数据污染,采用函数形式,每次以函数形式返回一份新的data,这样就拥有自己的作用域

### history和hash的区别
1. hash在路由里面有#
2. history刷新后会404,需要后端配置