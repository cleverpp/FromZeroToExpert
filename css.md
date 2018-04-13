在想要开始这个系列之前，我是很轻视css的：css还不简单，大概看一下就能上手了，没有遇到哪个页面实现不了呀。遇到问题就去google咯。
所以css方面的知识一直停留在0基础+1的阶段。可如果你想成为专家，那么则需要了解它的历史，原理。

## CSS规范的简单了解
从W3C组织的[CSS Snapshot](https://www.w3.org/TR/CSS/)可以比较全面的了解CSS规范当前的状况。

从CSS Level 2 开始，推荐内容和表现相分离的方式。CSS Level 3是CSS的最后一个Level，后续都采用Module的形式。CSS3核心基于CSS2.1。我们需要详细了解的有：CSS2.1 和 CSS3

## 选择器
这个部分熟记就好，具体请参考http://www.w3school.com.cn/cssref/css_selectors.asp

## 层叠优先级
!important > 内联样式 > 外部样式 > 浏览器默认样式

浏览器根据优先级来决定给元素应用哪个样式，而优先级仅由选择器的匹配规则来决定。
内联 > ID选择器 > 伪类=属性选择器=类选择器 > 元素选择器 > 通用选择器(*) > 继承的样式

## 盒模型(box-model)
- 盒模型：content、padding、border、margin
- 外边距合并
  + 只有垂直方向的外边距会发生合并，水平方向不会
  + 哪几种情况会发生外边距合并
  + 如何避免外边距合并
- box-sizing (CSS3)
  + 默认值为content-box
  + 标准盒模型content-box
  + IE盒模型border-box
  
## 视觉格式模型(Visual formatting model)
> In the visual formatting model, each element in the document tree generates zero or more boxes according to the box model. The layout of these boxes is governed by:
> - box dimensions and type.
> - positioning scheme (normal flow, float, and absolute positioning).
> - relationships between elements in the document tree.
> - external information (e.g., viewport size, intrinsic dimensions of images, etc.).

- 视口(viewport)
- 包含块(containing block)
- BFC(block formatting context)
  + 浮动定位和清除浮动时只会应用于同一个BFC内的元素。浮动不会影响其它BFC中元素的布局，而清除浮动只能清除同一BFC中在它前面的元素的浮动。外边距折叠（Margin collapsing）也只会发生在属于同一BFC的块级元素之间。
  + 对应一个独立、封闭的渲染区域，子元素的CSS样式不会影响BFC元素外部
  + 浮动子元素参与BFC父元素的高度计算，也就是BFC元素能够识别浮动元素（将元素声明为BFC元素，也是clearfix解决父元素塌陷问题的一种常用方法）
  + 占据文档流的BFC元素（可使用overflow: auto创建），能够识别浮动的兄弟元素,不会被浮动的兄弟元素覆盖，与之同行显示；
  + 占据文档流的BFC元素（可使用overflow: auto创建），width为auto时，会占满当前行的剩余宽度；
  
> Floats, absolutely positioned elements, block containers (such as inline-blocks, table-cells, and table-captions) that are not block boxes, and block boxes with 'overflow' other than 'visible' (except when that value has been propagated to the viewport) establish new block formatting contexts for their contents.
- IFC(inline formatting context)
  + 虚拟的矩形框，框内不包含块级盒子
  + IFC内部的元素，按从左到右、从上到下的顺序排布；
  + 可设置水平方向的magin、border、padding
  + 垂直方向可使用vertical-align来设置对齐方式
  + The width of a line box is determined by a containing block and the presence of floats. 
  + The height of a line box is determined by the rules given in the section on line height calculations.
- 定位(positioning)
  + 与定位有关的概念有文档流(Nomal flow)、浮动(float)、和绝对定位(absolute positioning)。涉及到的css属性有'position'和'float'。
  + position的值默认为static，可选值有static | relative | absolute | fixed | inherit
  + static定位，其top、left、right、bottom属性无效。
  + 相对定位relative，其top、left、right、bottom属性指的相对其在文档流的位置。
  + 绝对定位absolute，其top、left、right、bottom属性指的相对其所在的**包含快**
  + 固定定位fixed，相对于viewport进行定位，不会随滚动而移动。


## 参考(即本人的学习的路径)
1. [W3C技术资料: 理解CSS规范](http://www.chinaw3c.org/archives/369/)
2. [css的历史与原理](http://www.nowamagic.net/librarys/veda/detail/192)
3. [前端布局概述](https://mp.weixin.qq.com/s/8eAfz_I5xIhh7oFRifxaFw)
4. [层叠样式表的层叠是什么意思？](https://www.zhihu.com/question/20077745)
5. [css2.2](https://www.w3.org/TR/CSS22/)
6. [深入理解CSS优先级](https://www.cnblogs.com/starof/p/4387525.html)
7. [CSS basic box model](https://www.w3.org/TR/css3-box/)

[css mdn](https://developer.mozilla.org/zh-CN/docs/Web/CSS)
