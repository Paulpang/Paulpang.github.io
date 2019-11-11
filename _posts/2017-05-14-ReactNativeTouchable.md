---
layout: post
title: ReactNative常用组件之Touchable
date: 2017-05-14
tag: ReactNative
---


### 一、高亮触摸  TouchableHighlight
当手指点击按下的时候，该视图的不透明度会进行降低同时会看到相应的颜色，其实现原理则是在底层新添加了一个View。此外，TouchableHighlight只能进行一层嵌套，不能多层嵌套。
#### 常用属性：
 * <strong>activeOpacity</strong>  number 设置组件在进行触摸的时候，显示的不透明度(取值在0-1之间)* <strong>onHideUnderlay</strong>  function  方法 当底层被隐藏的时候调用* <strong>onShowUnderlay</strong>  function 方法 当底层显示的时候调用* <strong>style</strong>  可以设置控件的风格演示，该风格演示可以参考View组件的style* <strong>underlayColor</strong>  当触摸或者点击控件的时候显示出的颜色
 
### 二、不透明触摸  TouchableOpacity该组件封装了响应触摸事件；当点击按下的时候，该组件的透明度会降低。#### 常用属性：* <strong>activeOpacity</strong>  number        设置当用户触摸的时候，组件的透明度
