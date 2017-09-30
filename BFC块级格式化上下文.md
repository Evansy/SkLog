## BFC 块级格式化上下文 (Block Formatting Context)

### BFC的触发
* `flaot`       不为`none`
* `overflow`    为`hidden`、`auto`
* `display`     为`table-cell`、`table-caption`、`inline-block`
* `position`    为`fixed`、`absolute`
 > display：table也认为可以生成BFC，其实这里的主要原因在于Table会默认生成一个匿名的table-cell，正是这个匿名的table-ccell生成了BFC

 ### BFC的约束

* 生成BFC元素的子元素会一个接一个的放置。垂直方向上他们的起点是一个包含块的顶部，两个相邻子元素之间的垂直距离取决于元素的margin特性。在BFC中相邻的块级元素外边距会折叠。
* 生成BFC元素的子元素中，每一个子元素做外边距与包含块的左边界相接触，（对于从右到左的格式化，右外边距接触右边界），即使浮动元素也是如此（尽管子元素的内容区域会由于浮动而压缩），除非这个子元素也创建了一个新的BFC（如它自身也是一个浮动元素）。
    * 内部的Box会在垂直方向上一个接一个的放置
    * 垂直方向上的距离由margin决定。（完整的说法是：属于同一个BFC的两个相邻Box的margin会发生重叠，与方向无关。）
    * 每个元素的左外边距与包含块的左边界相接触（从左向右），即使浮动元素也是如此。（这说明BFC中子元素不会超出他的包含块，而position为absolute的元素可以超出他的包含块边界）
    * BFC的区域不会与float的元素区域重叠
    * 计算BFC的高度时，浮动子元素也参与计算
    * BFC就是页面上的一个隔离的独立容器，容器里面的子元素不会影响到外面元素，反之亦然

看到以上的几条约束，让我想起学习css时的几条规则
* Block元素会扩展到与父元素同宽，所以block元素会垂直排
* 垂直方向上的两个相邻DIV的margin会重叠，而水平方向不会(此规则并不完全正确)
* 浮动元素会尽量接近往左上方（或右上方）
* 为父元素设置overflow：hidden或浮动父元素，则会包含浮动元素

### BFC的应用领域
* 防止margin重叠
* 清除浮动
* 多兰布局

### 参考文章
http://www.cnblogs.com/dojo-lzz/p/3999013.html