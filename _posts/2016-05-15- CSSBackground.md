---
layout: post
title:  CSS之background-image/image/精灵图
date: 2016-05-15
tag: CSS
---

## CSS属性 - background-image

* background-image用于设置元素的背景图片
	* 会盖在background-color的上面
	* 在图片的透明区域，可以看到背景色
* 如果设置了多张图片
	* 设置的第一张图片将显示在最上面，其他图片按顺序层叠在下面
* 注意：如果设置了背景图片后，元素没有具体的宽高，背景图片是不会显示出来的

## CSS属性 - background-repeat

* background-repeat用于设置背景图片是否要平铺
* 常见的设值有
	* repeat：平铺
	* no-repeat：不平铺
	* repeat-x：只在水平方向平铺
	* repeat-y：只在垂直平方向平铺

## CSS属性 - background-size
* background-size用于设置背景图片的大小
## CSS属性 - background-position
* background-position用于设置背景图片在水平、垂直方向上的具体位置
	* 水平方向还可以设值：left、center、right
	* 垂直方向还可以设值：top、center、bottom
	* 如果只设置了1个方向，另一个方向默认是center
	* 比如background-position: 80px; 等价于 background-position: 80px  center;

## CSS Sprite(精灵图)

### 什么是CSS Sprite
* 是一种CSS图像合成技术，将各种小图片合并到一张图片上，然后利用CSS的背景定位来显示对应的图片部分
* 有人翻译为：CSS雪碧、CSS精灵

### 使用CSS Sprite的好处
* 减少网页的http请求数量，加快网页响应速度，减轻服务器压力
* 减小图片总大小
* 解决了图片命名的困扰，只需要针对一张集合的图片命名
* 更换风格方便，只需要在少数张图片上修改图片的颜色或样式，整个网页的风格就可以改变

### Sprite图片制作（雪碧图、精灵图）
* 方法1：Photoshop
* 方法2：[生成精灵图网站](https://www.toptal.com/developers/css/sprite-generator)

### 精灵图设置方法
* background-position: 水平方向,垂直方向

## background-image和img的选择



* 利用background-image和img都能够实现显示图片的需求，在开发中该如何选择？

|  | img | background-image |
| :---         |     :---:      |    ---: |
| 性质   | HTML元素     | CSS样式    |
| 图片是否占用空间     | √    | ×      |
| 浏览器右键直接查看地址     | √    | ×      |
| 支持CSS Sprite     | ×    | √     |
| 更有可能被搜索引擎收录     | √ （结合alt属性）   | ×      |
| 加载顺序 | 优先加载 | 等加载完HTML元素后再加载    |

* 总结
	* img，作为网页内容的重要组成部分，比如广告图片、LOGO图片、文章配图、产品图片
	* background-image，可有可无。有，能让网页更加美观。无，也不影响用户获取完整的网页内容信息
* 宗旨
	* 在没有任何CSS样式的情况下，用户也能浏览到网页中完整的内容信息（PS：网络出现问题或服务器出现问题时，有可能会导致CSS文件加载失败）


## CSS属性 - cursor

* cursor可以设置鼠标指针（光标）在元素上面时的显示样式
* cursor常见的设值有
* auto：浏览器根据上下文决定指针的显示样式，比如根据文本和非文本切换指针样式
* default：由操作系统决定，一般就是一个小箭头
* pointer：一只小手，鼠标指针挪动到链接上面默认就是这个样式
* text：一条竖线，鼠标指针挪动到文本输入框上面默认就是这个样式
* none：没有任何指针显示在元素上面

	





