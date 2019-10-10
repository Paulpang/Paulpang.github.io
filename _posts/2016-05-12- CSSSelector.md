---
layout: post
title: CSS选择器
date: 2016-05-12
tag: CSS
---

## 什么是CSS选择器
按照一定的规则选出符合条件的元素，为之添加CSS样式

## 选择器的种类繁多，大概可以这么归类

### 通用选择器（universal selector）(比如 *{})

* 一般用来给所有元素作一些通用性的设置
* 比如内边距、外边距

**注意** : 效率比较低，尽量不要使用

### 元素选择器（type selectors）(比如div{})

* 又叫标签选择器

### 类选择器（class selectors）(比如 .name{})

* 一个元素可以有多个class值，每个class之间用空格隔开
* class值如果由多个单词组成，单词之间可以用中划线-、下划线_连接，也可以使用驼峰标识
* 最好不要用标签名作为class值


### id选择器（id selectors）(比如 #name {})

* 一个HTML文档里面的id值是唯一的，不能重复
* id值如果由多个单词组成，单词之间可以用中划线-、下划线_连接，也可以使用驼峰标识
* 最好不要用标签名作为id值
* 中划线又叫连字符（hyphen）


### 属性选择器（attribute selectors）(比如 [href="top"])

* 拥有title属性的元素

### 后代选择器 (比如 div span)

* div元素里面的span元素（**包括直接、间接子元素**）

```
div span {
	color : red;
}
```

### 子选择器 (比如 div>span)

* div元素里面的**直接**span子元素（**不包括间接子元素**）

```
div>span {
	color: red;
}
div > span {
	color: red;
}

```


### 相邻兄弟选择器 (比如 div+span)

* div元素后面**紧挨着的p元素**（**且div、p元素必须是兄弟关系**）

```
div+p {
	color: red;
}

```
### 全体兄弟选择器 (比如 div~p)
* div元素**后面的p元素**（且div、p元素必须是兄弟关系）

```
div~p {
	color: red;
}

```

### 交集选择器 (比如 div.one#title)

* **同时**符合2个条件的元素：div元素、class值有one

```
div.one {
	color: red;
}

```


### 并集选择器 (比如 div,.one,#title)
* 所有的div元素 + 所有class值有one的元素 + 所有title属性值等于test的元素

```
div,.one,[title="test"] {
	color: red;
}

```
### 伪类

* 动态伪类
	* a:link 未访问的链接
	* a:visited 已访问的链接
	* a: hover 当鼠标移动到链接上
	* a: active  当鼠标左键点击链接不松开
	* a : focus 当链接呗tab健选择激活时
	* :hover,:active,:focus还可以应用到其他元素上

	**使用注意**
	
	* :hover必须放在:link和:visited后面才能完全生效
	* :active必须放在:hover后面才能完全生效
	* 所以建议的编写顺序是 :link、:visited、:hover、:active
	* 记忆：女朋友看到LV包包后，ha ha大笑

**去除a元素默认的:focus效果**


```
a:focus {
	outline:none;
}
```

> 或者将tabindex属性设置为-1


**tabindex属性**

* 使用tabindex可以控制tab键选中元素的顺序，从1开始

* tabindex设置为-1，代表禁止使用tab键选中


	
* 结构伪类

	* :nth-child(an+b)
		* 是**父元素**中的第几个子元素
		* nth-child(2n)和nth-child(even) 表示是父元素中的第偶数个子元素（第2、4、6、8......个）
		* nth-child(2n + 1)跟:nth-child(odd)同义 表示是父元素中的第奇数个子元素（第1、3、5、7......个）
	* :nth-last-child(an+b)
		* 从父元素的最后一个子元素开始往前计数
		* nth-last-child(1)，代表从父元素的倒数第一个子元素
		* nth-last-child(-n + 2)，代表从父元素的最后2个子元素
	* :nth-of-type(an+b)
		* 是**父元素**中**同种类型**的子元素开始往后计数
	* :nth-last-of-type(an+b)
		* 是**父元素**中**同种类型**的子元素开始往前计数
	
* 否定伪类
	* not()的格式是:not(x)
	* x是一个简单选择器
	* 元素选择器、通用选择器、属性选择器、类选择器、id选择器、伪类（除否定伪类）
	* :not(x)表示除x以外的元素
	* not()支持简单选择器，不支持组合


### 伪元素

为了区分伪元素和伪类，建议伪元素使用2个冒号

* ::first-line
	* ::first-line可以针对首行文本设置属性
	* 只有下列属性可以应用在::first-line伪元素
	* 字体属性、颜色属性、背景属性
	* word-spacing、letter-spacing、text-decoration、text-transform、line-height
* ::first-letter
	* ::first-letter可以针对首字母设置属性
	* 只有下列属性可以应用在::first-letter伪元素
	* 字体属性、margin属性、padding属性、border属性、颜色属性、背景属性
	* text-decoration、text-transform、letter-spacing、word-spacing（适当的时候）、line-height、float、vertical-align（只有当float是none时）
* ::before
	* ::before和::after用来在一个元素的内容之前或之后插入其他内容（可以是文字、图片）

* ::after

