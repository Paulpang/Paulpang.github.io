---
layout: post
title: ReactNative常用组件之Text
date: 2017-05-11
tag: HTML+ReactNative
---


###  一、什么是Text组件？
一个用于显示文本的React组件，和Android中的TextView组件或者OC中的Label组件相类似，专门用来显示基本的文本信息；除了基本的显示布局之外，可以进行嵌套显示，设置样式，以及可以做事件(例如:点击)处理
	

### 二、Text组件常用的属性方法

```bash
Attributes.style = {
    color string
    containerBackgroundColor string
    fontFamily string
    fontSize number
    fontStyle enum('normal', 'italic')
    fontWeight enum("normal", 'bold', '100', '200', '300', '400', '500', '600', '700', '800', '900')
    lineHeight number
    textAlign enum("auto", 'left', 'right', 'center')
    writingDirection enum("auto", 'ltr', 'rtl')
    numberOfLines number
    textAlign ("auto", 'left', 'right', 'center', 'justify')
    fontWeight ("normal", 'bold', '100', '200', '300', '400', '500', '600', '700', '800', '900')
    onPress  fcuntion
 }
 
```

##### 注释如下：

> `color` 字体颜色

> `numberOfLines` (number) 进行设置Text显示文本的行数，如果显示的内容超过了行数，默认其他多余的信息就不会显示了

> `onPress` (fcuntion)  该方法当文本发生点击的时候调用该方法

> `fontFamily`  字体名称

> `fontSize`  字体大小

> `fontStyle`   字体风格(normal,italic)

> `fontWeight ` 字体粗细权重("normal", 'bold', '100', '200', '300', '400', '500', '600', '700', '800', '900')

> `textShadowOffset`  设置阴影效果{width: number, height: number}

> `textShadowRadius`  阴影效果圆角

> `textShadowColor`  阴影效果的颜色

> `letterSpacing`  字符间距

> `lineHeight`  行高

> `textAlign`   文本对其方式("auto", 'left', 'right', 'center', 'justify')

> `textDecorationLine`  横线位置 ("none", 'underline', 'line-through', 'underline line-through')

> `textDecorationStyle` 线的风格("solid", 'double', 'dotted', 'dashed')

> `textDecorationColor` 线的颜色

>`writingDirection` 文本方向("auto", 'ltr', 'rtl')


## 三、Text组件中样式的继承
 在React-native中是没有样式继承这种说法的， 但是对于Text元素里边的Text元素，其实是能够继承的，文字控制类的属性也是多重继承的，和css中是一样的.