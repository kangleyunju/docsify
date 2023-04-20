## css高度塌陷
### 定义
父元素没有设置高度,子元素浮动float,导致塌陷,子元素跑到父元素外面
### 解决方法
* 给父级设置高度
* 父级开启元素BFC属性, overflow: hidden
* 设置父级伪元素,清除浮动clear: both
* 父级下加一个空白的div,清除浮动clear: both