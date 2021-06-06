---
layout: post
title: tableView设置tableHeaderView使用xib导致高度不准确
date: 2020-04-22
tag: iOS
---

###### 问题 : tableView的header高度不对，一般都是header是从xib加载出来的

#### 解决方法

##### 第一步

新建xib的时候选择的是View，当选择 Size 为 Freeform 时，view的约束就变成这样了，如下图

![](/images/posts/xib/111.png)

改成这样就好了，如下图

![](/images/posts/xib/222.png)

##### 第二步

如果上述还不能的话，就在 viewDidAppear 里，调用一下tableView.reloadData

```
override func viewDidAppear(_ animated: Bool) {
     super.viewDidAppear(animated)
      tableView.reloadData()
 }

```