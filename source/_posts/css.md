---
title: css
date: 2023-04-17 13:54
tags: [技术分享]
---
### 复合选择器
* 多元素选择器：选择器1,选择器2{属性:值;}
* 后代元素选择器：E F{属性:值;}
* 子元素选择器：E > F{属性:值;}
* 相邻元素选择器：E + F{属性:值;}

### ！Important 属性

内容介绍

一、什么是 important

二、!important 在 CSS 中的作用

三、语法格式

一、什么是 important

important 在英文中含义是“重要的”意思

二、!important 在 CSS 中的作用

它主要是用来提升属性的女重。其属性的权重值无穷大

三、语法格式

使用！Important属性的语法格式

属性：值！Important

P{

加了！Important的属性它的权重值会变得无穷

```
Color:#foo！Important

P1{Color:#foo ;

#P2{Color:#foo；
```
一定要注意！import 的语法规则：

Ø  正确的写法

n  属性：值 ！important;

Ø  错误的写法

n  属性：值；！important; （不能将！important 写在分号的外面 一定要写在分号的里面）

n  属性：值 important; （！不能省略）

使用！important 一定要注意以下几点：

1，！important 它是提升的属性的权重，而不是提升选择器的权重！

上图的效果：

文本的颜色是听加了！important 的属性， 文本的大小是听 ID 选择器的 因为！important 它只是提升了属性的权重并没有提升选择器的优先级。

2，！important 它不能提升继承过来的权重! 
