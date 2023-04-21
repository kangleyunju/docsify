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
* typeof

```
typeof([])//object
typeof(null)//object
typeof(1)//number
typeof([1,2,3])//object
typeof(undefined)//undefined
typeof(null)//object
```
* instanceof 

```
[] instanceof Array; // true
'123' instanceof String //false 简单数据类型不能直接判断
new String('123') instanceof String//true
```
* constructor 

```
console.log([1,2,3].constructor==Array)
```
* Object.prototype.toString.call

```
Object.prototype.toString.call(1)
```

### js循环

* for，for of，forEach只能循环数组
* for in 可以循环对象object
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