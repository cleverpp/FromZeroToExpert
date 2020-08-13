# 基于AST(抽象语法树)实现React项目转ReactNative项目
## 引言
React项目和ReactNative项目虽然都是基于React语法编写的，但是两者的运行环境是不一样的。React项目的运行环境是浏览器或webview，而ReactNative项目的运行环境是Android或ios的原生控件。
那么如何将React项目转换为ReactNative项目呢？答案是：AST(抽象语法树)。本文将介绍以下内容：
1. 底层编译原理之AST(抽象语法树)
2. 基于AST如何将React项目转ReactNative
## 底层编译原理之AST(抽象语法树)
谈及编译原理，很多上过该门课的人第一反应是难。我们先来复习下编译原理。
> 编译原理即是对高级程序语言进行翻译的一门科学技术。编译可以分为五个基本步骤:词法分析、语法分析、语义分析及中间代码的生成、优化、目标代码的生成。这是每个编译器都必须的基本步骤和流程, 从源头输入高级语言源程序输出目标语言代码。

AST抽象语法树即五个步骤中的 语法分析之后中间代码生成之前的一个中间表示。常见编译型语言的编译流程如下所示：

![编译流程](https://github.com/cleverpp/FromZeroToExpert/blob/master/advanced/assets/common-lang-compile.png)

而对于解释型语言（例如 JavaScript）来说，通过词法分析 -> 语法分析 -> 语法树，就可以开始解释执行了。

以上即是对编译原理的复习以及AST概念的介绍，那么AST到底是怎样的？如何生成AST？可以应用哪些场景呢？ 如下图所示，左侧是基于React语法编写的代码片段，右侧是对应的AST形式，右侧的每一层结构被叫做节点(Node)。一个AST可以由单一的节点或是成百上千个节点构成。

![AST形式](https://github.com/cleverpp/FromZeroToExpert/blob/master/advanced/assets/ast.png)

### AST的生成
一般来说，将一种结构化语言的代码编译成另一种类似的结构化语言的代码包括以下几个步骤：

![AST生成与转换](https://github.com/cleverpp/FromZeroToExpert/blob/master/advanced/assets/parse-transform-generate.png)

首先是 Parse，将代码解析（Parse）成抽象语法树（AST，Abstract Syntex Tree），然后对 AST 进行遍历（traverse）和转换（transform），最后是生成（generate），根据新的 AST 生成编译后的代码。**请大家记住这个过程，这就是React项目转换为ReactNative项目的核心原理**

可以进行AST生成的解析器有：
1. acorn
2. @babel/parse， Babel 的 JavaScript 解析器，原名 Babylon。最初是 从 Acorn 项目 fork 出来的
3. Esprima，Eslint可选的解析器之一
4. espree，Eslint默认解析器，从Esprima v1.2.2中fork出来的
5. recast

### 应用场景
前端基于AST实现的一些工具很多，以下是我们经常接触到的一些：
1. babel: 实现 JS 编译，转换过程是 AST 的转换
2. ESlint: 代码错误或风格的检查，发现一些潜在的错误
3. IDE 的错误提示、格式化、高亮、自动补全等
4. UglifyJS 压缩代码
5. 代码打包工具 webpack

## 基于AST如何将React项目转ReactNative
这个问题的回答在AST的生成小节中说明过，首先将React项目中的代码解析成AST，然后对AST进行遍历（traverse），把不符合ReactNative使用规范中的节点（Node）转换（transform）成符合规范的内容，例如，本来在react项目引用的react-dom的 ImportDeclaration节点删掉，添加引用react-native的 ImportDeclaration节点，经过一系列的转换后最后得到一个新的AST，将该新的AST生成目标代码，到此即完成了转换。这么听起来是不是还挺简单的，so young so naive！

在接下来的篇幅中重点介绍将React项目转换为ReactNative项目需要进行那些工作

### 定义规范
如果不定义规范，同样是React项目，写出来的代码五花八门，对这些代码进行转换的工作是无法收敛。所以定义代码规范是转换可以实现的前提。代码规范中包括：生命周期函数的使用、组件的定义及范围、第三方库的引用范围、css的使用规范、编码规范等等。让大家遵循规范的最好办法是提供项目模板 或者脚手架等。

### UI组件库
在普通React项目中，我们的JSX中混杂着原生html标签和自定义的组件，如果是对这样的代码进行转换，难度会比较大，原生标签非常丰富，很多标签没有对应的ReactNative组件，这样的标签在进行转换时不能仅做简单的Identifier转换，需要额外增加许多代码。既然是这样，更好的办法是提供一套抹平差异的UI组件规范，基于React实现一套该组件，基于ReactNative实现一套该组件，在编写React项目中就直接使用该UI组件，在转换时处理起来就比较容易。

### 编译器
在前期的三端合一项目中，我们将ReactNative项目转换为React项目的的react-native-web，其实现原理即使用h5来实现ReactNative的组件，再利用webpack编译时将对react-native的引用替换为react-native-web。同样的，在React转ReactNative时，我们可以将react-native-web作为我们React项目的基础UI库，只是webpack无法将React项目编译成ReactNative环境的代码，而是需要我们基于AST实现一个编译器。

编译器的实现原理即前文中反复提到的解析-转换-生成目标代码的过程，而在具体实现时，我们需要考虑的有：JS代码的编译、CSS的编译、其它类型文件的编译。

### 第三方库的处理
对于项目中不可缺少的第三方库，例如React全家桶中的React-Router，需要进行react-native的适配。例如 基于react-navigation实现react-router的API。

对于仅在web中可使用，而ReactNative项目无法实现的第三方库要禁止使用，或采取其它方案

### Native原生能力的调用
无论是React项目还是ReactNative项目，都有需要调用原生能力的需求。React项目中调用原生能力一般是利用cordova或jsbridge实现，而在 React Native 中则是通过NativeModules直接使用原生模块导出的方法。

在处理这一块比较好的方式和UI组件库是类似的，先定义好一套API，然后基于React和ReactNative各实现一套。

### 其它
1. package.json文件，在转换后要安装转换ReactNative项目中需要的依赖
2. 开发模式的项目运行
3. 生产模式的项目包

## 总结
1. 编译可以分为五个基本步骤:词法分析、语法分析、语义分析及中间代码的生成、优化、目标代码的生成
2. 对于解释型语言（例如 JavaScript）来说，通过词法分析 -> 语法分析 -> 语法树，就可以开始解释执行了
3. 一般来说，将一种结构化语言的代码编译成另一种类似的结构化语言的代码经过解析成AST-遍历并转换AST-将新的AST生成目标代码
4. 将React项目转换为ReactNative项目需要：定义规范、UI组件库、编译器、第三方库的处理、Native原生能力的调用、项目运行等
