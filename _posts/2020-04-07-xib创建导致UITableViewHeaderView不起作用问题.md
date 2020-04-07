---
layout: post
title: xib创建View导致UITableViewHeaderView不起作用问题
date: 2020-04-07
tag: iOS
---

###### 背景 : 在开发中,给tableViewHeaderView设置高度,在向下滑动的时候,背景图片会粘着顶部拉伸,在以前用xib实现的时候直接在xib上面放一个背景图片,并经xib设置为tableview的headerView.然后在scrollowDidScroll这个方法中监听scrollView的偏移量来实现. 
###### 但是最近在实现相同的功能的时候,这个写没有效果,导致背景图片跟着tableView的滑动一起滑动,没有粘合到顶部不动.

#### 解决方法

原来在Xcode 11之后,在用Xib或者StoreBorad拖控件的时候,默认的约束为Automatic,如图所示

![](/images/posts/xib/image1.png)

如果外界要动态的改变约束,这时候自动布局就不起作用,为了解决这个问题,在拖控件的时候,我们需要将控件的自动布局不选择Automatic,如图所示

![](/images/posts/xib/image2.png)

为此,我们有时候在遇到利用Xib设置tableView的headerView的时候,导致高度headerView的高度不对,之前是通过设置

> headerView.autoresizingMask = []

来解决高度不对的问题,感觉导致这个的原因还是因为automic导致自动布局没有生效的结果.


**依据**

```base
在Xcode 11 之后
 UITableView 中的单元格现在可以使用画布中的自动布局约束视图自行调整大小。要选择现有表视图的行为，请为表视图估计的项目大小启用 Automatic设置，为 Size inspector 中的“单元格高度”启用 Automatic。

• NSView 和 UIView 在 Size inspector 中具有布局模式选项，以明确选择“translates autoresizing mask into constraints”。默认设置为 Automatic，这是现有行为。Automatic 意味着当视图受故事板或 .xib文件中的约束影响时，“translates autoresizing mask into constraints”是 off 状态，但如果不受约束则是 on 状态。

• 使用 Add Missing Constraints 提高了自动布局约束生成的可靠性。

• UIScrollView 的内容可以在画布中滚动，一旦其子视图完全受到自动布局约束的约束。

• 现在，UICollectionView 中的单元格可以使用画布中的“自动布局”约束视图进行自我调整。要选择现有集合视图的行为，请为集合视图的估计大小启用 Automatic 设置，并从 Size inspector 启用单元格大小的 Automatic 设置。如果在 iOS 13 之前部署，则可以通过在 viewDidLoad 期间调用 performBatchUpdates:completion:来激活自调整大小的集合视图单元格。

• 在检查器字体弹出框中，Family 弹出窗口现在将菜单项呈现为适用字体的预览。

• 现在可以在文档范围内对错放的帧执行 Update Frames 操作，而无需选择视图。

• UIScrollView 支持内容和框架布局指南，可以在 Size inspector 中启用，以便更好地控制可滚动内容。

```

