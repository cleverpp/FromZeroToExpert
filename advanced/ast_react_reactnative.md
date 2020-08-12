# 基于AST(抽象语法树)实现React项目转ReactNative项目
## 引言
React项目和ReactNative项目虽然都是基于React语法编写的，但是两者的运行环境是不一样的。React项目的运行环境是浏览器或webview，而ReactNative项目的运行环境是Android或ios的原生控件。
那么如何将React项目转换为ReactNative项目呢？答案是：AST(抽象语法树)。本文将介绍以下内容：
1. 底层编译原理之AST(抽象语法树)概念
2. 基于AST如何将React项目转ReactNative
## 底层编译原理之AST(抽象语法树)概念
谈及编译原理，很多上过该门课的人第一反应是难。我们先来复习下编译原理。
