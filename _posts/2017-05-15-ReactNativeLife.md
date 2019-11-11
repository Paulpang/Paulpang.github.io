---
layout: post
title: ReactNative的生命周期
date: 2017-05-15
tag: ReactNative
---

React Native组件的生命周期大致上可以划分为<Strong>实例化阶段</Strong>、<Strong>存在阶段</Strong>和<Strong>销毁阶段</Strong>，如图所示:

![](/images/posts/RNLifeTime/1.png)

其中最常用的为<Strong>实例化阶段</Strong>，该阶段就是组件的构建、展示时期，需要我们根据几个函数的调用过程，控制好组件的展示和逻辑的处理。### 一、实例化阶段函数功能分析

#### getDefaultProps       
该函数用于初始化一些默认的属性，通常会将固定的内容放在这个函数 中进行初始化和赋值；        
在组件中，可以利用`this.props`获取在这里初始化它的属性，由于组件初始化后，再次使用该组件不会调用getDefaultProps函数，所以组件自己不可以自己修改props（即：props可认为是只读的），只可由其他组件调用它时在外部修改。#### getInitialState  
该函数是用于对组件的一些状态进行初始化；由于该函数不同于getDefaultProps，在以后的过程中，会再次调用，所以可以将控制控件的状态的一些变量放在这里初始化，如控件上显示的文字，可以通过`this.state`来获取值，通过`this.setState`来修改state值， 比如：

```bashthis.setState({    activePage: activePage,     currentX: contentOffSetX  });```<strong>注意:</strong> 一旦调用了`this.setState`方法，组件一定会调用`render`方法，对组件进行再次的渲染，不过，如果React框架会自动根据DOM的状态来判断是否需要真正的渲染。
#### componentWillMount相当于OC中的ViewWillAppear方法，在组件将要被加载在视图上之前调用，功能相对较少。
#### render
render是一个组件中必须有的方法，本质上是一个函数，并返回JSX或其他组件来构成DOM，和Android的XML布局类似，注意：`只能返回一个顶级元素`;       
此外，在render函数中，只可通过this.state和this.props来访问在之前函数中初始化的数据值 。#### componentDidMount在调用了render方法后，组件加载成功并被成功渲染出来以后，所要执行的后续操作，一般会在这个函数中处理网络请求等加载数据的操作；因为UI已经成功被渲染出来， 所以放在这个函数里进行请求操作，不会出现UI上的错误。
下图是利用了fetch API来异步请求Web API来加载数据：

![](/images/posts/RNLifeTime/2.png)### 二、存在期阶段函数功能分析
* componentWillReceiveProps    指父元素对组件的props或state进行了修改
* shouldComponentUpdate    一般用于优化，可以返回false或true来控制是否进行渲染* componentWillUpdate组件刷新前调用，类似componentWillMount
* componentDidUpdate更新后的hook

### 三、销毁期阶段函数功能分析    
用于清理一些无用的内容，如：点击事件Listener，只有一个过程：`componentWillUnmount`### 四、常用知识点分析#### 4.1  this.state      开发中组件免不了要与用户互动，React 的一大创新，就是将组件看成是一个状态机，一开始有一个初始状态，然后用户互动，导致状态变化，从而触发重新渲染 UI。举个例子：![](/images/posts/RNLifeTime/3.png)当用户点击组件，导致状态变化，`this.setState` 方法就修改状态值，每次修改以后，自动调用 `this.render` 方法，再次渲染组件。可以把组件看成一个“状态机”. 根据不同的status有不同的UI展示。只要使用setState改变状态值，根据diff算法算出来有差以后，就会执行ReactDom的render方法，重新渲染页面。 
<strong>注意：</strong>由于 `this.props` 和 `this.state` 都用于描述组件的特性，可能会产生混淆。一个简单的区分方法是，`this.props` 表示那些一旦定义，就不再改变的特性，而 `this.state` 是会随着用户互动而产生变化的特性。

#### 4.2  获取真实的DOM节点在React Native中，组件并不是真实的 DOM 节点，而是存在于内存之中的一种数据结构，叫做虚拟 DOM （virtual DOM）。 
 只有当它插入文档以后，才会变成真实的 DOM 。 根据 React 的设计，所有的 DOM 变动，都先在虚拟 DOM 上发生，然后再将实际发生变动的部分，反映在真实 DOM上，这种算法叫做 DOM diff，它可以极大提高网页的性能表现。但是，有时需要从组件获取真实 DOM 的节点，这时就要用到 `ref` 属性;下图通过一个案例来演示：![](/images/posts/RNLifeTime/4.png)

下图是利用了fetch API来异步请求Web API来加载数据：![](/images/posts/RNLifeTime/5.png)


 上面代码中，组件 View 的子节点有一个文本输入框，用于获取用户的输入。这时就必须获取真实的 DOM 节点，虚拟 DOM 是拿不到用户输入的。为了做到这一点，文本输入框必须有一个 ref属性，然后`this.refs.[refName]`就会返回这个真实的 DOM 节点。      需要注意的是，由于 <strong>this.refs.[refName]</strong> 属性获取的是真实 DOM ，所以必须等到虚拟 DOM 插入文档以后，才能使用这个属性，否则会报错。上面代码中，通过为组件指定 Click 事件的回调函数，确保了只有等到真实 DOM 发生 Click 事件之后，才会读取 `this.refs.[refName]` 属性。
      
### 五、总结React Native组件的生命周期，经历了`Mount->Update->Unmount`这三个大的过程，即从创建到销毁的过程，结合OC中的开发经验，我们在以上的基础上应该可以快速的上手React Native的开发。

### 六、ES5和ES6的差异化

es5，es6 都是对 ecmascript规范的补充，es5已经大规模使用了，es6目前可能在个别平台存在浏览器兼容性问题。
 
#### 区别1：创建组件组件是一个自定义的js对象，在es5中使用React.createClass()；在es6中必须继承React.component，然后进行创建。
ES5的写法：

![](/images/posts/RNLifeTime/6.png)

ES6的写法：

![](/images/posts/RNLifeTime/7.png)

#### 区别2：组件的属性props在ES6中，其为属性：defaultProps(可以标识static定义在class内，也可以定义在class外)，而在ES5中，其为方法：getDefaultProps: function(){return {name:value}};ES5:

![](/images/posts/RNLifeTime/8.png)

ES6:

![](/images/posts/RNLifeTime/9.png)

#### 区别3：组件的状态stateES5:

![](/images/posts/RNLifeTime/10.png)

ES6:

![](/images/posts/RNLifeTime/11.png)














