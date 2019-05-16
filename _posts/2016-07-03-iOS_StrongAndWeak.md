---
layout: post
title: iOS开发中 Strong 和 weak 的深入理解
date: 2016-07-03
tag: iOS
---

**最近项目不是太忙，闲下来总结一下容易让程序员困扰的一些问题，如有不准确的地方，还请多多指正。**
ARC是苹果为了简化程序员对内存的管理，推出的一套内存管理机制，对象的申请和释放工作会在运行时，由编译器自动添加retain和release。

在开发中什么时候使用strong，什么时候使用weak，什么时候使用copy呢？

**强指针Strong：**<br>
	强指针：strong修饰的属性一般不会自动释放；
		   在OC中，对象默认是强指针，在实际开放中一般属性对象一般用strong来修饰（NSArray，NSDictionary），在使用懒加载定义控件的时候，一般也用strong

eg：
`@property (nonatomic, strong) NSArray *dataList;`
`@property (nonatomic, strong) UILabel *label;
`

	
	懒加载控件
	- (UILabel *)label {
    if (_label == nil) {
        _label = [[UILabel alloc] init];
    }
    return _label;
	}

**弱指针Weak:**<br>

在使用 sb 或者 xib 给控件拖线的时候,为什么拖出来的先属性都是用 weak 修饰呢?
eg

	@property (weak, nonatomic) IBOutlet UILabel *label;


原因是由于在向 xib 或者 sb 里面添加控件的时候,添加的子视图是添加到了跟视图 View 上面, 而 控制器 Controller 对其根视图 View 默认是强引用的,当我们的子控件添加到 view 上面的时候, self.view addSubView: 这个方法会对添加的控件进行强引用,如果在用 strong 对添加的子控件进行修饰的话,相当于有两条强指针对子控件进行强引用, 为了避免这种情况,所以用 weak 修饰.
	
	注意: 
	1. addSubView 默认对其 subView 进行了强引用
	2.在纯手码实现界面布局时，如果通过懒加载处理界面控件，需要使用strong强指针


除此之外,我们在开发的时候用的代理 也是用 weak 进行修饰的,其目的是为了防止控件的循环引用.

	@property (nonatomic, weak) id<PersonDelegate> delegate;



**Copy的使用**<br>
对于 copy 的使用,网上已经有很多关于 copy 介绍, 其包括深 copy 和浅 copy, 在这里我就不再多说了,如果不太明白的话可以网上查一下资料

	copy 一般用来修饰 NSString 和 block
	
eg:

`@property (nonatomic, copy) NSString *str;
`

以上内容是对 strong 和 weak的个人理解,后续会持续完善,今天就写到这里,现在要继续写代码了.