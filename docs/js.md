## 函数柯里化
### 定义
函数里面返回函数，从而做到参数复用的目的

### 例子
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