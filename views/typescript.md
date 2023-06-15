### typescript
由微软开发的在JavaScript的基础上添加静态类型定义编程语言

### any和unknown的区别
* any彻底放弃了类型检查
* unknown相较于any更加严格，在执行大多数操作之前，会进行某种形式的检查

```
let aa: any = 123
console.log(aa.msg)//符合TS的语法
let bb: unknown = 123
console.log(bb.msg)//Error，unknown不确定有底下有该属性
```

### ts定义类型
* 定义变量
```
let a: string | number = 1
```
* 定义数组
```
let arr:[string, number, boolean]
arr=['a',1,true]
```
* 定义函数
```
function getInfo(a: string, b: number): string|number {
	if(b>5){
		return b
	}else{
		return a
	}
}
console.log(getInfo('zs', 20));
```
* 函数参数未知个数
```
function fn(...args:number[]){
	console.log(args)
	let res=args.reduce((pre,cur)=>{
		return pre+cur
	},0)
	console.log(res)
}
fn(1,2,3,4)
```