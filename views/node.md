### express，koa，egg，nest
* koa是express原班人马出的node框架
* 回调的处理逻辑不同，express是通过callback，不支持异步，koa是通过async await，箭头函数，等更具有语义化的API
* express 内置了很多中间件，koa是比express更加轻量，自己下载
* egg是阿里出品的基于koa企业级应用开发框架，内置多进程管理，内置XXS，SSRF，SCRF等攻击的防御，提供IP白名单机制，钓鱼攻击的防御方案
* express适合小型项目，koa适合中型项目，Egg适合大型项目
* nest是一个基于Node.js的渐进式框架，它使用TypeScript编写，并借鉴了Angular的设计思想

### 洋葱模型
无论哪个框架都是基于中间件来实现的,中间件的作用就是拦截和修改请求和响应结果,一层一层向内传递,再向外传递

### node是怎么实现监听的
可以使用 Node.js 的内置 process 对象来监听Node项目的内存使用情况，具体可以使用 process.memoryUsage()，返回结果有4个