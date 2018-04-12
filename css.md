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


## 参考(即本人的学习的路径)
1. [W3C技术资料: 理解CSS规范](http://www.chinaw3c.org/archives/369/)
2. [css的历史与原理](http://www.nowamagic.net/librarys/veda/detail/192)
3. [前端布局概述](https://mp.weixin.qq.com/s/8eAfz_I5xIhh7oFRifxaFw)
4. [层叠样式表的层叠是什么意思？](https://www.zhihu.com/question/20077745)
5. [css2.2](https://www.w3.org/TR/CSS22/)
6. [深入理解CSS优先级](https://www.cnblogs.com/starof/p/4387525.html)

[css mdn](https://developer.mozilla.org/zh-CN/docs/Web/CSS)
