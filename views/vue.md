### Vue2和vue3的区别
* vue2使用到object.definepropoty, 通过遍历每一层的属性实现监听,直接改动原始对象,通过get和set函数,来设置和读取属性
* vue3使用proxy, new proxy(),监听的是整个整个对象,产生的是一个新的对象