---
layout: post
title: ReactNative的生命周期
date: 2017-05-15
tag: HTML+ReactNative
---

React Native组件的生命周期大致上可以划分为<Strong>实例化阶段</Strong>、<Strong>存在阶段</Strong>和<Strong>销毁阶段</Strong>，如图所示:

![](/images/posts/RNLifeTime/1.png)

其中最常用的为<Strong>实例化阶段</Strong>，该阶段就是组件的构建、展示时期，需要我们根据几个函数的调用过程，控制好组件的展示和逻辑的处理。

#### getDefaultProps
该函数用于初始化一些默认的属性，通常会将固定的内容放在这个函数 中进行初始化和赋值；
在组件中，可以利用`this.props`获取在这里初始化它的属性，由于组件初始化后，再次使用该组件不会调用getDefaultProps函数，所以组件自己不可以自己修改props（即：props可认为是只读的），只可由其他组件调用它时在外部修改。
该函数是用于对组件的一些状态进行初始化；

```bash


render是一个组件中必须有的方法，本质上是一个函数，并返回JSX或其他组件来构成DOM，和Android的XML布局类似，注意：`只能返回一个顶级元素`;
此外，在render函数中，只可通过this.state和this.props来访问在之前函数中初始化的数据值 。
下图是利用了fetch API来异步请求Web API来加载数据：

![](/images/posts/RNLifeTime/2.png)




### 三、销毁期阶段函数功能分析
用于清理一些无用的内容，如：点击事件Listener，只有一个过程：`componentWillUnmount`
<strong>注意：</strong>由于 `this.props` 和 `this.state` 都用于描述组件的特性，可能会产生混淆。一个简单的区分方法是，`this.props` 表示那些一旦定义，就不再改变的特性，而 `this.state` 是会随着用户互动而产生变化的特性。

#### 4.2  获取真实的DOM节点
 只有当它插入文档以后，才会变成真实的 DOM 。

下图是利用了fetch API来异步请求Web API来加载数据：


 上面代码中，组件 View 的子节点有一个文本输入框，用于获取用户的输入。这时就必须获取真实的 DOM 节点，虚拟 DOM 是拿不到用户输入的。为了做到这一点，文本输入框必须有一个 ref属性，然后`this.refs.[refName]`就会返回这个真实的 DOM 节点。
      
### 五、总结

### 六、ES5和ES6的差异化

es5，es6 都是对 ecmascript规范的补充，es5已经大规模使用了，es6目前可能在个别平台存在浏览器兼容性问题。
 
#### 区别1：创建组件


![](/images/posts/RNLifeTime/6.png)

ES6的写法：

![](/images/posts/RNLifeTime/7.png)

#### 区别2：组件的属性props

![](/images/posts/RNLifeTime/8.png)

ES6:

![](/images/posts/RNLifeTime/9.png)

#### 区别3：组件的状态state

![](/images/posts/RNLifeTime/10.png)

ES6:

![](/images/posts/RNLifeTime/11.png)













