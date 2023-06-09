### 输入网址到页面渲染经历了哪些
* 发送到dns服务器，通过输入的域名获取ip地址
* 通过ip地址与服务器建立tcp连接(因特网的一个通信协议)
* 服务器响应请求，返回请求的数据
* 浏览器下载数据，并且解析html代码，生成dom树，解析css和js，渲染页面直到显示完成

### 同源策略
同源策略是一种Web浏览器安全机制，用于限制来自不同源（域名、协议或端口）的脚本之间的交互

### 跨域
当协议，域名，端口这三个有任意一个不一样就算跨域
1. jsonp，json with padding，由于scrippt标签是不存在跨域的，所以jsonp就是通过script标签来实现请求
2. cors：在服务端设置Access-Control-Allow-Origin等CORS相关响应头，允许跨域请求。
3. 后端代理，本地代理
4. WebSocket


### websocket是什么
是一种在客户端和服务器之间建立持久化连接的网络协议，它允许双方实时地进行数据传输，长连接

### 网站优化
* 减少http请求
* 减小图片的体积，使用图片缩略图等， 图片懒加载等
* Css提前，先让页面出来，HTML 内容从上至下依次解析
* 减少 DOM 操作

### 移动端怎么自适应
* 使用第三方库，如flexible.js轻松搞定各种不同的移动端设备兼容自适应问题
* rem，我们只需要在根元素确定一个px字号，则可以来算出元素的宽高。1rem=16px，直接在html标签定义一个font-size
* 媒体查询，@media在不同的分辨率下引入不同的css样式，也就是要写多套css

### http状态码有哪些
1. 1xx信息状态码，表示已经接收到请求，正在继续处理中
2. 2xx成功
3. 3xx重定向
4. 4xx客户端错误
5. 5xx服务端错误

### 0.1+0.2为什么不等于0.3
* 原因：二进制浮点数， 相加后精度丢失
* 解决方法：先乘后除，toFixed

### 客户端和服务端的三次握手
1. 第一次握手是由客户端发出的，目的是请求建立连接
2. 第二次握手是由服务端发出的，目的是确认客户端的请求并告诉客户端自己的初始序列号
3. 第三次握手是客户端发出的，目的是告诉服务端已经准备好，可以正式传输数据了

### 自适应布局和响应式布局
* 自适应布局需要写多套css，媒体查询
* 响应式布局只需一套代码，流式布局(使用%和em单位来确定元素大小和位置)+媒体查询

### 浏览器的回流和重绘
1. 回流是元素的几何属性发生改变,比如高度宽度,浏览器重新计算,重新排版
2. 重绘是元素的外观发生改变,比如颜色,背景,变宽,浏览器重新绘制外观
3. 二者都会消耗资源,可以使用css动画代替js,减少dom操作
