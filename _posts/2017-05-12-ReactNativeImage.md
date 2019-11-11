---
layout: post
title: ReactNative常用组件之Image
date: 2017-05-12
tag: ReactNative
---

在开发中还有一个非常重要的组件Image，通过这个组件可以展示各种各样的图片，而且在React Native中该组件可以通过多种方式加载图片资源。

###  一、Image组件的基本用法
#### 1.1 从当前项目中加载图片

```bash
export default class App extends Component<{}> {
  render() {
    return (
      <View style={styles.container}>
        <Text style={styles._textStyle}>
         加载本地视图
        </Text>

        <Image source={require('./images/download.jpg')} style={{width:200,height:300}}>

        </Image>


      </View>
    );
  }
}
```
该图片资源文件的查找和JS模块相似，该会根据填写的图片路径相对于当前的js文件路径进行搜索。

此外，React Naive的Packager会根据平台选择相应的文件，例如:my_icon.ios.png和my_icon.android.png两个文件(命名方式android或者ios)，会分别根据android或者ios平台选择相应的文件。



#### 1.2 加载使用APP中的图片

```bash
<View style={styles.container}>
       <Text style={styles.textMarginTop}>加载Xcode中的图片</Text>
       <Image source={require('image!icon_homepage_map')} style={{width: 50,height:50}}/>
 </View> 
```
 使用已经打包在APP中的图片资源(例如:xcode asset文件夹以及Android drawable文件夹)


#### 1.3 加载来自网络的图片：

客户端的很多图片资源基本上都是实时通过网络进行获取的，写法和上面的加载本地资源图片的方式不太一样，<strong>这边一定需要指定图片的尺寸大小</strong>，实现如下：

```bash
<View style={styles.container}>
        <Image source={{uri:'https://www.baidu.com/img/bd_logo1.png'}} style={{flex:1,width:200, height:100, resizeMode: Image.resizeMode.cover}}/>
        <Image source={{uri:'https://www.baidu.com/img/bd_logo1.png'}} style={{flex:1,width:200, height:100, resizeMode: Image.resizeMode.contain}}/>
        <Image source={{uri:'https://www.baidu.com/img/bd_logo1.png'}} style={{flex:1,width:200, height:100, resizeMode: Image.resizeMode.stretch}}>
</View>

```
 细心的同学可能已经注意到，我在上面用到了resizeMode这样一个属性，那么这个属性的作用相当于OC中设置图片的内容模式
 
> Image.resizeMode.cover：图片居中显示，没有被拉伸，超出部分被截断；
 
> Image.resizeMode.contain：容器完全容纳图片，图片等比例进拉伸；

> Image.resizeMode.stretch： 图片被拉伸适应容器大小，有可能会发生变形。

#### 1.4 设置图片为背景
 
```bash
  <Image source={{uri:'https://www.baidu.com/img/bd_logo1.png'}} style={{flex:1,width:200, height:100, resizeMode: Image.resizeMode.stretch}}>
           <Text style={{marginTop: 60, backgroundColor: 'red'}}>下面是背景图片</Text>
  </Image>
```

### 二、Image组件的常见属性

#### 2.1 属性方法

  <strong>onLayout(function)</strong>
   当Image布局发生改变的，会进行调用该方法，调用的代码为:{nativeEvent: {layout: {x, y, width, height}}}.
   
   <strong>onLoad (function)</strong>
   当图片加载成功之后，回调该方法
   
   <strong>onLoadEnd (function)</strong>
   当图片加载失败回调该方法，该不会管图片加载成功还是失败
   
   <strong>onLoadStart (fcuntion)</strong>
   当图片开始加载的时候调用该方法
   
   <strong>resizeMode</strong>
   缩放比例,可选参数('cover', 'contain', 'stretch') 该当图片的尺寸超过布局的尺寸的时候，会根据设置Mode进行缩放或者裁剪图片
   
   <strong>source{uri:string}</strong>
   进行标记图片的引用，该参数可以为一个网络url地址或者一个本地的路径

#### 2.2 样式风格属性
  <strong>FlexBox</strong>  支持弹性盒子风格
  
  <strong>Transforms</strong>  支持属性动画
  
  <strong>backgroundColor</strong> 背景颜色
  
  <strong>borderColor</strong>     边框颜色
  
  <strong>borderWidth</strong> 边框宽度
  
  <strong>borderRadius</strong>  边框圆角
  
  <strong>overflow</strong> 设置图片尺寸超过容器可以设置显示或者隐藏('visible','hidden')
  
  <strong>tintColor</strong>  颜色设置
  
  <strong>opacity</strong> 设置不透明度0.0(透明)~1.0(完全不透明)
