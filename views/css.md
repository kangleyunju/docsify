### css高度塌陷
父元素没有设置高度,子元素浮动float,导致塌陷,子元素跑到父元素外面
* 给父级设置高度
* 父级开启元素BFC属性, overflow: hidden
* 设置父级伪元素,清除浮动clear: both
* 父级下加一个空白的div,清除浮动clear: both

### px,rem,em
* px绝对单位,像素
* em相对单位,相对于上下文元素大小,默认1em=16px
* rem根目录单位,相对于根元素大小,html的大小,默认1rem=16px

### css3新属性
* boder-radius,box-shadow,text-shadow
* transform,2D3D转换，animation动画
* 新增伪类，比如常用的nth-child()