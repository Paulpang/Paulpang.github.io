---
layout: post
title: iOS开发中页面之间的传值总结
date: 2015-05-30
tag: iOS
---
在iOS开发中,我们经常会遇到界面之间的传值问题,其中主要分为 **顺向传值** 和 **逆向传值** 两种方式.

#### 顺向传值
顺传: 就是在界面从A控制器跳转到B控制器的时候,顺便将A界面的值传递给B控制器. 这种方式一般用**属性传值**的方式进行传递,具体操作办法为:

 * 首先SecondViewController视图中需要有一个属性用来 存储传递过来的值：

	```bash
 @property(nonatomic,retain) NSString *firstValue ;//属性传值
	```

 * 然后OneViewController视图需要引用SecondViewController视图的头文件，在视图中的按钮点击事件中，通过SecondViewController的对象将需要传递的值存在firstValue中:

	```bash
(void)buttonAction:(UIButton *)button {

	SecondViewController *second = [[SecondViewController alloc]init];//用下一个视图的属性接受想要传过去的值,属性传值
	second.firstValue = _txtFiled.text;

    [self.navigationControllerpushViewController:second animated:YES];

	}
	```

页面跳转之后，就能在SecondViewController视图中，通过存值的属性，取用刚才传递过来的值：

> 显示传过来的值[_txtFiledsetText:_firstValue];//firstValue保存传过来的值


#### 逆向传值

逆传 是指 将界面是从A 跳转到B控制器,但是在从重B控制器返回A控制器的时候,需要将B界面的值传递给A界面. 这时候一般用**通知** 或者 **代理** 或者**block** 方式进行传递.

##### 通知传值

1. 首先在B界面发出通知

	```bash
	[[NSNotificationCenterdefaultCenter] postNotificationName:@”myNotificationName” object:broadcasterObject];
	```
2. 在A界面接收通知

	```bash
	[[NSNotificationCenterdefaultCenter] addObserver:listenerObject selector:@selector(receivingMethodOnListener:)     name:@”myNotificationName” object:nil]; 
	```
同时在A界面需要注销通知

对于**通知传值**的分析:

	```bash
优点: 通知的发送者和接受者都不需要知道对方。可以指定接收通知的具体方法。通知名可以是任何字符串。
缺点: 较键值观察需要多点代码。在删掉前必须移除监听者。不能传大量数值，只能让谁去做什么事。
	```

##### 代理协议传值

1. 在B界面注册协议

	```bash
  @protocol ClassBDelegate<NSObject> 
  - (void)methodOne; 
  @optional 
  - (void)methodTwo:(NSString *)value; 
  @end

	```
2. 在B界面的.h中定义一个代理属性

	```bash
	  @interface ClassB 
	  @property (nonatomic, weak) id<ClassBDelegate> delegate; 
	  @end 

	```	
3. 当我们在ClassB的实现文件（ClassB.m）中遇到想让别的类（如 ClassA）处理的问题时，就可以这样

	```bash
	  [self.delegate methodOne]; 
	  [self.delegate methodTwo:@"需要传递的值"];
	```
4. 在A界面遵守代理协议

	```bash
	  @interface ClassA<ClassBDelegate> 

	  @end
	```
	
5. 在A界面中实现代理方法

	```bash
	  - (void)methodOne{
	      // 具体实现内容 
	  } 
	 - (void)methodTwo:(NSString *)value{  
	    // 具体实现内容   
	 }
	```