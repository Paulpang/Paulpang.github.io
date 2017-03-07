---
layout: post
title: UITabBarController 和 UINavigationController 的分析
date: 2014-10-23 
tags: iOS    
---
最近工作不是太忙,在开发中,一直对UITabBarController和UINavigationController里面的内部结构不是太清楚,心里面一直模棱两可.经过今天一天的研究和在网上查找资料,现在明白了其中的内部结构,记录下来以便日后查找.

### UINavigationController

UINavigationController上面的导航条是UINavgationBar,在UINavgationBar上面的是 UINavgationItem, 在UINavgationItem上面有title, titleView, leftBarButtonItem 和 rightBarButtonItem, 其中leftBarButtonItem和rightBarButtonItem 都属于 UIBarButtonItem的属性.
具体结构如下:

```bash
UINavigationController-----> UINavgationBar----> UINavgationItem

UINavgationItem 包含:
	1. title
	2. titleView
	3. UIBarButtonItem
		* leftBarButtonItem
		* rightBarButtonItem


```
###  UITabBarController

UITabBarController底部是UITabBar,在UITabBar上面是UITabBarItem, 在UITabBarItem内部分别有image, selectedImage,title属性. 
具体结构如下:

```bash
UITabBarController----> UITabBar----> UITabBarItem

UITabBarItem 包含:
	1. image
	2. selectedImage
	3. title

```
