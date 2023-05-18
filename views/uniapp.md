### unicloud事务
```
const transaction = await db.startTransaction()
try {
	//操作1
	await transaction.collection('user').add()
	//操作2
	await transaction.collection('user').update()
	//事务执行成功
	await transaction.commit()
} catch (error) {
	//事务执行失败
	await transaction.rollback()
}
```

### app和h5的区别
1. 样式：app有顶部状态栏
2. api：app没有document和window操作,

### 安卓和苹果的区别
1. 苹果有底部安全距离, 有些样式苹果不支持,比如css滤镜
2. api：苹果没有短震动