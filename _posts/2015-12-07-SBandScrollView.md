---
layout: post
title: StoryBoard下ScrollView如何添加约束
date: 2015-12-07
tag: iOS
---
在做项目的事后有一个注册页面，为了适配屏幕采用了StoryBoard，添加约束以后运行后发现一个问题。  在4.0 甚至更大的屏幕下是没有问题的，如下图（4.0屏幕）

![](/images/posts/SBAndScrollView/1.png)

但是放到更小的3.5英寸就会出现问题，发现下面的按钮不见了，主要原因是输入框太多，导致更个屏幕放不下更多。如图（3.5）英寸
 
 ![](/images/posts/SBAndScrollView/2.png)


想了下就决定用ScrolleView， ContentSize可以设置为560. 这样在其他屏幕上没有太多的影响，在3.5的屏幕下也可以滑动了。
但是在StoryBord拖过ScrollView，添加约束的时候发现他并不会按照你猜想的去执行。经过查阅资料，大致知道了原因。
这是由于scrollview本身contentSize、contentInsets等复杂的特性导致，苹果文档在讲autolayout的时候甚至专门拿出一节讲
如何对scrollview进行自动布局。

解决方案可以给ScrollView添加一个唯一的子视图，大小和ScrollView一样，然后所有原计划添加到ScrollView上面的控件，
都添加在子视图上面。


###步骤如下：
1.首先在我们的Controller自带的View里面添加一个ScrollView，点开下面设置约束的4个按钮的第2个，约束设置距离父试图的距离为（0，0，0，0）如下图所示。
 
![](/images/posts/SBAndScrollView/3.jpg)

2.在ScrollView上面添加一个View成为ScrollView的子视图，点开下面设置约束的4个按钮的第2个，设置约束距离ScrollView的距离为（0.0.0.0）如下图所示。

![](/images/posts/SBAndScrollView/4.jpg)
 

3.这个时候会发现报错了，不用紧张~，  先不用管它，咱们继续往下走。

![](/images/posts/SBAndScrollView/5.jpg)
 

4.点开下面设置约束的4个按钮的第一个，选择 Horizontal Center in Container, 并打上对勾， （如果想要左右滑动就选择 Vertical Center in Container， 同时实现左右上下则全不选）

![](/images/posts/SBAndScrollView/6.jpg)
 

5.再次打开下面设置约束的4个按钮的第2个 选择Height 设置你想要的560.  （如果想要左右滑动就选择 Width， 同时实现左右上下就全部设置）
（这个高度是以后运行后Scroller的ContentSize）

 ![](/images/posts/SBAndScrollView/7.jpg)

6.设置完成以后发现错误不见了，只有一个黄色的警告，这是由于Frame没有更新导致的，我们来更新下Frame。
 
 ![](/images/posts/SBAndScrollView/8.jpg)


7.接下来我们就可以在这个ScrollView的子视图View上面来添加控件了。 设置约束的时候是相对于父试图View的哦~。布局。
 
 ![](/images/posts/SBAndScrollView/9.jpg)


附：
上面的View是设置的固定的一个值。 如果想要动态的设置，就需要把我们刚才加的高度的约束设置成属性
 
 ![](/images/posts/SBAndScrollView/10.jpg)

起一个名字， height； 然后重写 -(void)updateViewConstraints 方法，在调用super 后 动态的设置height这个约束的constant属性。

 ![](/images/posts/SBAndScrollView/11.jpg)

这样你会发现ScrollView可滑动的幅度会在每次运行后都不一样哦~；

本文转自:蓝鸥科技







