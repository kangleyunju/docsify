### 函数柯里化
函数里面返回函数，从而做到参数复用的目的
```
function add(){
	let args = Array.prototype.slice.call(arguments);
	let inner = function(){
		args.push(...arguments)
		return inner
	}
	inner.toString = function(){
		return args.reduce((prev,cur) => {
				return prev + cur
		})
	}
	return inner
}
parseInt(add(1,2)(3)(4))//10
parseInt(add(1,2)(3)(4))//10
```

### js数据类型
* 基本数据类型 string，number，boolen，undefined，null
* 复杂数据类型 object
* 新增类型 Symbol，bigint

```
//Symbol 本质上是一种唯一标识符，可用作对象的唯一属性名
//bigint 大数字
console.log(typeof(9007199254740992n))//bigint
```

### 判断js数据类型
1. typeof

```
typeof([])//object
typeof(null)//object
typeof(1)//number
typeof([1,2,3])//object
typeof(undefined)//undefined
typeof(null)//object
```
2. instanceof 

```
[] instanceof Array; // true
'123' instanceof String //false 简单数据类型不能直接判断
new String('123') instanceof String//true
```
3. constructor 

```
console.log([1,2,3].constructor==Array)
```
4. Object.prototype.toString.call()

```
Object.prototype.toString.call(1)
```

### 数组循环

* for，for of，forEach只能循环数组
* for in 可以循环对象object
* find 返回符合条件的项
* findIndex 返回符合条件的下标
* map用于改造数组，可以return返回值
* some返回一个boolean，判断是否有元素是否符合条件，数组里面所有的元素有一个符合条件就返回true
* every返回一个boolean，判断每个元素是否符合条件，数组里面所有的元素都符合才返回true
* filter过滤数组
* reduce复杂操作，去重，求和，计算等

```
let array = [0, 1, 2, 3, 4, 5]
for (i = 0; i < array.length; i++) {
} 
for (var i in array) {
} 
for (var i of array) {
} 
array.map(v=>{
	return v===2 (map可以return返回值)
})
```
```
//reduce求出现的次数
let names = ['aa', 'bb', 'cc', 'dd', 'aa'];
let nameNum = names.reduce((pre, cur) => {
	if (cur in pre) {
		pre[cur]++
	} else {
		pre[cur] = 1
	}
	return pre
}, {})
console.log(nameNum); //{aa: 2, bb: 1, cc: 1, dd: 1}
```
```
//reduce去重
let arr = [1,2,3,4,4,1]
let newArr = arr.reduce((pre,cur)=>{
    if(!pre.includes(cur)){
      return pre.concat(cur)
    }else{
      return pre
    }
},[])
console.log(newArr);// [1, 2, 3, 4]
```
```
//reduce求和
var result = [
    {
        subject: 'math',
        score: 10
    },
    {
        subject: 'chinese',
        score: 20
    },
    {
        subject: 'english',
        score: 30
    }
];
var sum = result.reduce(function(prev, cur) {
    return cur.score + prev;
}, 0);
console.log(sum) //60
```


### 浅拷贝
只复制最外一层，拷贝的是一个对象的指针，而不是复制对象本身，拷贝出来的对象共用一个指针，其中一个改变了值，其他的也会同时改变
1. Object.assign(obj)
```
//后者属性覆盖前者
let obj1={a:1,b:2}
let obj2={a:1,b:2}
let obj3=Object.assign(obj1,obj2)
```
2. 扩展运算符{ ...obj }
3. 数组浅拷贝slice，concat

### 深拷贝
1. Json.parse(Json.stringfy())
2. 递归
3. 第三方库，lodash.cloneDeep




### 数组去重
1. [...new Set(arr)], 只能一维数组
2. 通过reduce

### call，apply，bind
* 相同点：都是用来改变this的指向
* 不同点：call，apply是立即调用，第一个参数都是this，call第二个是字符串，apply第二个是数组，Bind是在需要的时候调用


### 使用splice替换数组某个值
```
let aa=[1,2,3]
aa.splice(0,1,5)
console.log(aa)//[5,2,3]
```

### 正则
1. 以什么开头
```
/^a/.test('a12b')//true
```
1. 以什么结尾
```
/a$/.test('a12b')//false
```

### ES6新语法
1. 用let定义变量，用const定义常量，有作用域块，无法被重新赋值
2. 新增了箭头函数，箭头函数内部的this和外部的this一致，绑定到最近的一层对象上，是一个匿名函数
3. 新增了promise对象，实际上是一个构造函数，一个promise对象就是一个异步操作，立即执行，解决了回调地狱的问题，es7新增了async await
4. 新增了模块化，import导入，export导出

### const
const定义的变量是不可重新赋值的，但对于复合类型，可以更改其属性或元素的值。
```
const arr = [1, 2, 3];
arr[0] = 4; // 可以更改元素值
console.log(arr); // 输出：[4, 2, 3]
```

### 闭包
* 闭包就是能够读取其他函数内部变量的函数称为闭包
* 闭包的内存占用是不会释放的，如果滥用闭包，会造成内存泄漏

```
for (var i = 0; i < 5; i++) {
  setTimeout(function() { console.log(i); }, i * 1000 );
}
//5,5,5,5,5,5
```
```
//es5闭包
for (var i = 0; i < 5; i++) {
  (function(j) {
    setTimeout(function() { console.log(j); }, j * 1000 );
  })(i);
}
//1,2,3,4,5
```
```
//es6
for (let i = 0; i < 5; i++) {
  setTimeout(function() { console.log(i); }, i * 1000 );
}
//1,2,3,4,5
```

### 闭包的好处
1. 使成员私有化，使数据访问更安全
2. 防止全局污染，因为是外部访问函数内部的变量
3. 将变量保存在内存中

### 哪些操作会造成内存泄漏
内存泄漏就是，程序已经动态分配的内存无法释放或未释放，导致程序运行缓慢甚至崩溃
1. 未释放内存
2. 某个对象循环引用
3. 事件监听没有移除
4. 过渡缓存，缓存没有清理一直保留在内存中

### 防抖和节流5

1. 防抖，用户停止操作后执行事件，input实时搜索
```
function debounce(func, delay) {
  let timeoutId;
  return function(...args) {
    clearTimeout(timeoutId);
    timeoutId = setTimeout(() => func.apply(this, args), delay);
  };
}
```
2. 节流,用户每隔一段时间进行操作,如提交
```
function throttle(fn, delay) {
  let lastTime = 0;
  return function(...args) {
    const currentTime = Date.now();
    if (currentTime - lastTime >= delay) {
      fn.apply(this, args);
      lastTime = currentTime;
    }
  }
}
```


### 数组转对象
1. {...arr}
2. Object.fromEntries([['name', '张三'], ['age', 18], ['gender', '男']])

### 对象转数组
1. Array.from(obj)
2. Object.values(obj)
3. 循环
4. Object.entries({name: '张三', age: 20, gender: '男'})


### call，apply，bind
* 三者的相同点：都是用来改变this的指向
* call，apply是立即调用，第一个参数都是this，call第二个是字符串，apply第二个是数组
* bind不会立即执行，需要手动调用

```
function sayHello(name) {
  console.log('Hello, ' + name + '!');
}
sayHello.call(null, '张三'); // Hello, 张三!
sayHello.apply(null, ['张三']); // Hello, 张三!
```

```
function sayHello(name) {
  console.log('Hello, ' + name + '!');
}
const newFn = sayHello.bind(null, '张三');
newFn(); // Hello, 张三!
```

### js继承
* 不使用object.create:构造函数继承,原型链继承,组合继承
* 使用object.create:原型式继承,寄生式继承,寄生组合继承

### 原型原型链
* 每个对象都有一个对象,称为原型,通过原型,一个对象可以继承另一个对象的属性和方法,进而代码重用,节省内存
* 可以通过object.create(obj)来创建一个对象的原型
* 当我们访问一个对象的属性或方法时，如果该对象本身没有该属性或方法，就会沿着原型链一直向上查找，直到找到该属性或方法为止。如果找不到则返回 undefined
* 通过obj._proto_可以获取对象的原型
* 通过instanceof来检查一个对象是否是另一个对象的实例

```
var parentObj = { name:'张三'};
var myObj = Object.create(parentObj);
if (myObj instanceof parentObj) {
  console.log('myObj 是 parentObj 的实例');
} else {
  console.log('myObj 不是 parentObj 的实例');
}
```

### 怎么实现图片懒加载
1. new IntersectionObserver(),判断元素是否滚动到可视区域
2. 通过计算页面滚动距离

### push，pop，shift，usnhift
* push末尾添加一个或多个
* pop末尾删除一个元素
* shift删除第一个元素
* usnhift开头添加一个或多个，array.unshift(1,2)

### 计算结果
1. 1/0 Infinity 无限
2. 1+undefined//NaN
3. 1.25.toFixed(1)//1.3，四舍五入
4. Math.round(3.49)//3.5，四舍五入

### 什么是同步，什么是异步
* 同步指的是一次只能完成一件任务，如果有多个任务，就必须排队，前面一个任务完成，再执行后面一个任务
* 异步指的是每一个任务有一个或多个回调函数（callback），前一个任务结束后，不是执行后一个任务，而是执行回调函数

### 手写一个promise
```
new Promise((resolve,reject) => {
	
}).then(res=>{
	resolve(res)
}).catch(err=>{

})
```

### promise 的三个状态
* 初始态 pending
* 成功 resolved/fulfilled
* 失败 rejected

### callback
* callback回调通常用来描述一种函数调用方式，这种方式是将函数作为另一个函数的参数，以便在另一个函数完成后被调用执行
* Promise 可以更轻松地处理异步代码中的错误和异常，catch捕捉错误，还提供了promise.all来处理多个异步操作
```
function request(callback){
	let url='https://api.vvhan.com/api/weather'
	const xhr = new XMLHttpRequest();
	 xhr.onreadystatechange = function () {
		 if(xhr.readyState === 4)
		 callback(JSON.parse(xhr.response))
	 };
	 xhr.open("GET", url, true);
	 xhr.send();
}
function log(data){
	console.log('结果',data);
}
request(log)
```

### session、cookie 和 localStorage
1. 时效,cookie可以设置过期时间,session当浏览器关闭数据消失,localStorage一直保留在内存中,除非手动清除
2. 大小,cookie只能存储4kb,session和localStorage可以存更多
3. 安全,cookie更加安全,session和localStorage数据保留在浏览器中容易被劫持
4. cookie适用于服务器会话token,session和localStorage用于存储临时数据

### 宏任务微任务
js是单线程的,任务按顺序一个一个的执行，但是一个任务耗时太长,那么后面的任务就需要等待，为了解决这种情况，将任务分为了同步任务和异步任务,而异步任务又可以分为微任务和宏任务,先执行微任务再执行宏任务
* 宏任务
1. setTimeout 
2. setInterval 
3. setImmediate node环境
4. requestAnimationFrame 

* 微任务
1. Promise.then catch finally
2. MutationObserver 
3. process.nextTick  node环境

### js事件循环
js事件循环是JavaScript运行时环境中的一种执行机制，用于处理用户交互、网络请求、计时器和其他异步操作。js单线程的，当JavaScript遇到异步代码时，例如发起一个网络请求或通过setTimeout()函数设置一个计时器，它将被添加到事件队列中等待执行。一旦主线程完成当前任务并且事件队列中有待处理的任务，事件循环将取出下一个任务并将其推入主线程中执行。这个过程不断重复，直到所有任务都被处理完毕。

### js事件委托
利用事件冒泡的原理，将子元素的事件添加到父元素，好处是代码简洁，减少内存占用，动态绑定事件

```
console.log(await(fn1()))
console.log(2)
setTimeout(()=>{
	console.log(3,'setTimeout')
})
this.$nextTick(()=>{
	console.log(4,'nextTick')
})
new Promise(function(resolve){
	console.log(5,'promise')
	resolve()
}).then(function(){
	console.log(6,'promise')
})
console.log(7)
async function fn1(){
	return 1
}
1
2
5 promise
7
4 nextTick
6 promise
3 setTimeout
```

### 箭头函数和普通函数区别
1. 箭头函数是匿名函数,更加简洁
2. 箭头函数的this继承的最近一层this
3. 箭头函数不能使用bind,apply,call改变this指向
4. 箭头函数不能作为构造函数,也就是不能new function

### set，weakSet，map
* set，es6新增的数据结构，类似数组，其中的值没有重复，通过构造函数生成set数据结构
* 方法有add()，delete()，has()，clear()，keys()，values()
```
const set=new Set();
[8, 2, 3, 4, 3, 2, 1].forEach(x => set.add(x));
console.log(...set)//8 2 3 4 1
```


* map 键值对的结构，特点是键可以是任意值
* 方法有set()，get()，has()，delete()，clear()，keys()，values()
```
const map=new Map();
map.set('a',1);
map.set('b',{name:'mayun'});
console.log(map);
```

* WeakMap 弱引用对象,只能使用对象作为键值对的键
* 方法有set()，get()，has()，delete()
```
const objKey = {};// 创建一个对象作为键
const weakMap=new WeakMap();
weakMap.set(objKey,{name:'mayun'});
console.log(weakMap.get(objKey));
```