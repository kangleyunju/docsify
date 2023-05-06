### css高度塌陷
父元素没有设置高度，子元素浮动float，导致塌陷，子元素跑到父元素外面
1. 给父级设置高度
2. 父级开启元素BFC属性， overflow: hidden
3. 设置父级伪元素，清除浮动clear: both
4. 父级下加一个空白的div，清除浮动clear: both

### 元素的BFC属性
BFC就是Block Formatting Context的缩写，当元素开启BFC属性之后，这个元素就会变成一个独立的区域，它就不会影响到其他的元素，这样布局就不会混乱，开启BFC有：
1. 设置元素浮动float（不推荐）
2. display:inline-block（不推荐）
3. overflow:hidden（推荐）
4. 设置元素绝对定位（不推荐）

### px，rem，em
* px绝对单位，像素
* em相对单位，相对于上下文元素大小，默认1em=16px
* rem根目录单位，相对于根元素大小，html的大小，默认1rem=16px

### css3新属性
* boder-radius，box-shadow，text-shadow
* transform，2D3D转换，animation动画
* 新增伪类，比如常用的nth-child()

### css隐藏元素的方法
* overflow:hidden
* opcity:0
* z-index:-1
* width:0,height:0
* display:none
* transform:scale(0)
* position:absolute;left:-9999
* color:rgba(0,0,0,0)
* clip-path

### 伪类
* :hover
* :active
* :focus

### 伪元素
* ::before
* ::after
* ::first-letter
* ::first-line

### 响应式布局
是为了多设备显示适应问题
* rem
* %
* flex
* 媒体查询
* vh,vw


### li与li之间有看不见的间隔
* 原因：当li{display:inline-block}，li换行会产生间隔
* 解决：直接并排去掉间隙
```
//有间隙
<ul>
	<li>1</li>
	<li>2</li>
</ul>
//无间隙
<ul>
<li>1</li><li>2</li>
</ul>
```