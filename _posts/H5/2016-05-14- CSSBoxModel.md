---
layout: post
title:  CSS之盒子模型（Box Model）
date: 2016-05-14
tag: CSS
---
HTML中的每一个元素都可以看做是一个盒子，可以具备这4个属性

### 内容（content）
* 盒子里面装的东西

### 内边距（padding）
* 怕盒子里装的东西损坏而添加的泡沫或者其它抗震的辅料

### 边框（border）
* 就是盒子的边框，比如木盒子四周的木板

### 外边距（margin）
* 为了方便取出，盒子之间保留一定的空隙

#### 注意 :
* 一个元素的实际占用宽度 = border-left + padding-left + width + padding-right + border-right

* 一个元素的实际占用高度 = border-top + padding-top + height + padding-bottom + border-bottom

* 一个元素的空间宽度 = margin-left + border-left + padding-left + width + padding-right + border-right + margin-right

* 一个元素的空间高度 = margin-top + border-top + padding-top + height + padding-bottom + border-bottom + margin-bottom  
 
### 宽度、高度相关属性

#### width：宽度
* min-width：最小宽度，无论内容多少，宽度都大于或等于min-width
* max-width：最大宽度，无论内容多少，宽度都小于或等于max-width

#### height：高度
* min-height：最小高度，无论内容多少，高度都大于或等于min-height
* max-height：最大高度，无论内容多少，高度都小于或等于max-height

#### padding的取值规律

* 按照顺时针方向设值：top、right、bottom、left

* 如果缺少left, 那么left就使用right的值

* 如果缺少bottom, 那么bottom就使用top的

### 上下margin传递

#### margin-top传递
* 如果块级元素的顶部线和块级父元素的顶部线重叠，那么这个块级元素的margin-top值会传递给父元素

#### margin-bottom传递
* 如果块级元素的底部线和块级父元素的底部线重叠，并且父元素的高度是auto，那么这个块级元素的margin-bottom值会传递给父元素
* 水平方向上的margin是永远不会发生传递现象

#### 如何防止出现传递问题？
* 给父元素设置padding-top\padding-bottom
* 给父元素设置border
* 给父元素或者子元素设置display: inline-block
* 以后理解得更深入，还会学到其他解决方法

### 建议
* margin一般是用来设置兄弟元素之间的间距
* padding一般是用来设置父子元素之间的间距


### 上下margin折叠

#### 垂直方向上相邻的2个margin（margin-top、margin-bottom）有可能会合并为1个margin，这种现象叫做collapse（折叠）
#### 水平方向上的margin（margin-left、margin-right）永远不会collapse

#### 折叠后最终值的计算规则
* 如果都是正数，最终值是：绝对值最大的那个正数值
* 如果都是负数，最终值是：绝对值最大的那个负数值
* 如果正数、负数都有，最终值是：最大正数和最小负数相加

#### 如何防止margin collapse？
* 只设置其中一个元素的margin
* 条件允许的话，使用padding取代margin
* 以后理解得更深入，还会学到其他解决方法


## border（边框相关的属性)

### 边框宽度
* border-top-width、border-right-width、border-bottom-width、border-left-width
* border-width是上面4个属性的简写属性

### 边框颜色
* border-top-color、border-right-color、border-bottom-color、border-left-color
* border-color是上面4个属性的简写属性

### 边框样式
* border-top-style、border-right-style、border-bottom-style、border-left-style
* border-style是上面4个属性的简写属性
	* none：没有边框，边框颜色、边框宽度会被忽略
	* hidden：与“none”类似，多用在表格上，用于解决边框冲突
	* dotted：边框是一系列的点 
	* dashed：边框是一条虚线
	* solid：边框是一条实线 
	* double：边框有两条实线。两条线宽和其中的空白的宽度之和等于border-width的值
	* groove：边框看上去好象是雕刻在画布之内 
	* ridge：和grove相反，边框看上去好象是从画布中凸出来
	* inset：该边框使整个框看上去好象是嵌在画布中
	* outset：和inset相反，该边框使整个框看上去好象是从画布中凸出来

#### 行内级非替换元素的注意点

* 以下属性对行内级非替换元素不起作用
* width、height、margin-top、margin-bottom

* 以下属性对行内级非替换元素的效果比较特殊
* padding-top、padding-bottom、border-top、border-bottom

## CSS属性 - border-xx-radius

#### border-xx-radius定义的是四分之一椭圆的半径
* 第1个值是水平半径
* 第2个值是垂直半径（如果不设置，就跟随水平半径的值）

## CSS属性 - outline
* outline表示元素的外轮廓
	* 不占用空间
	* 默认显示在border的外面
	* 每个部位都是完整连接的，不会像border那样有可能会断开（比如行内级非替换元素的换行）

* outline相关属性有
	* outline-width
	* outline-style：取值跟border的样式一样，比如solid、dotted等
	* outline-color
	* outline：outline-width、outline-style、outline-color的简写属性，跟border用法类似
	* outline-offset：设置outline和border之间的间距

* 应用实例
 * 去除a元素、input元素的focus轮廓效果

## CSS属性 - box-shadow

* box-shadow属性可以设置一个或者多个阴影
每个阴影用<shadow>表示
* 多个阴影之间用逗号,隔开，从前到后叠加
* <shadow>的常见格式如下
	* 第1个<length>：水平方向的偏移，正数往右偏移

	* 第2个<length>：垂直方向的偏移，正数往下偏移

	* 第3个<length>：模糊半径（blur radius）

	* 第4个<length>：延伸距离

	* <color>：阴影的颜色，如果没有设置，就跟随color属性的颜色

	* inset：外框阴影变成内框阴影


## CSS属性 - box-sizing

* box-sizing用来设置盒子模型中宽高的行为
content-box
	* padding、border都布置在width、height外边

* border-box
	* padding、border都布置在width、height里边

### 元素的水平居中显示

在一些需求中，需要元素在父元素中水平居中显示（父元素一般都是块级元素、inline-block）

#### 行内级元素、inline-block元素
* 水平居中：在父元素中设置text-align: center

#### 块级元素
* 水平居中：给自己设置margin-left: auto、margin-right: auto

#### 定位盒子想要水平居中的方式

```
{
	left: 50%;
	margin-left: 自身盒子宽度的一半；
}
```

### offset

包含四个属性,作用是获取对象的自身的尺寸

> offsetWith = width + border + padding
>

```
<style>
    #demo {
     	 width: 200px;
        height: 200px;
        background-color: #00f;
        border: 10px sandybrown solid;
    }
</style>
    
    
<script>
    var demo = document.getElementById("demo");
    console.log(demo.offsetWidth)
</script>        
```

> offsetHeight = height + border + padding
> 

offsetLeft、offsetTop 指的是：返回距离上级带有**定位**盒子的距离
> offsetLeft
> 

> offsetTop
> 

**注意：** <br>
1、如果上级元素都没有定位，则以body为准<br>
2、offsetLeft是从上级元素的padding开始计算，不包含上级元素的border宽度,即：就是子box到定位的上级box边框到边框的距离<br>
>
> offsetParent 
> 返回该对象的带有定位的上级元素注意与parentNode的区别
> 

**注意：** <br>
1、如果当前元素的父级元素没有进行css定位（position：absolute/relative）,offsetParent为Body<br>
2、如果当前元素的父级元素有css定位（position：absolute/relative）,offsetParent为取最近的那个上级元素<br>

### top/right/bottom/left

> top/right/bottom/left 适用于定位元素，也就是说，只有定位元素才有这几个属性，不是定位元素没有这几个属性
> 

#### offsetTop 和 style.top的区别

- 最大区别在于  offsetLeft  可以返回没有定位盒子的距离左侧的位置。 而 style.top 不可以  只有定位的盒子 才有 left  top right
- ffsetTop 返回的是数字，而 style.top 返回的是字符串，除了数字外还带有单位：px

```
style.left = 300px      

parseInt（300px）    结果  300

parseInt（style.left） + parseInt（style.left）

```
- offsetTop 只读，而 style.top 可读写。
- 如果没有给 HTML 元素指定过 top 样式，则 style.top 返回的是空字符串。
- 最重要的区别  style.left 只能得到 行内样式     offsetLeft 随便

```
// 行内样式
<div id="demo" style="width: 100px">
    <div id="div1"></div>
</div>
```



































