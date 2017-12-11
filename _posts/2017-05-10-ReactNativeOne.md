---
layout: post
title: React Native版本管理
date: 2017-05-10
tag: HTML+ReactNative
---
## 一、管理React Native库的版本


在开发中，会经常的去控制React Native的版本库，得以适配各种条件下的开发，那该如何查看、控制ReactNative的版本呢？

### 1 查看本地的React Native的版本

```bash
react-native --version
```
	

### 2 更新本地的React Native的版本

```bash
 npm update -g react-native-cli
```
### 3 查询react-native的npm包最新版本

 NPM的全称是Node Package Manager ，是一个NodeJS包管理和分发工具，已经成为了非官方的发布Node模块（包）的标准。
   
#### npm包地址 ：
   `https://www.npmjs.com/package/react-native
   `
    
#### 命令行查询

```bash
npm info react-native
```

### 4 升级或者降级npm包的版本

 新的npm包会包含更新在运行react-native init命令生成的一些动态文件，例如init创建项目的时候会生成iOS和Android的子项目，我们可以通过以下的命令进行获取最新的代码
 
#### 命令行查询
      
```bash
react-native upgrade
```


## 二、WebStom设置React Native代码提示

### 1  从gitHub上下载xml插件
    
```bash
git clone https://github.com/virtoolswebplayer/ReactNative-LiveTemplate  
```

### 2  安装
     
```bash
将ReactNative.xml复制到 ~/Library/Preferences/WebStorm10/templates ，然后重启 WebStrom。
```

## 三、创建RN项目

init命令默认会创建最新的版本，而目前最新的0.45及以上版本需要下载boost等几个第三方库编译。这些库在国内即便翻墙也很难下载成功，导致很多人无法运行iOS项目！！！中文网在论坛中提供了这些库的国内下载链接。如果你嫌麻烦，又没有对新版本的需求，那么可以暂时创建0.44.3的版本

> 提示：你可以使用--version参数（注意是两个杠）创建指定版本的项目。例如react-native init MyApp --version 0.44.3。注意版本号必须精确到两个小数点。

#### 代码命令

```bash
react-native init 项目名称
cd 改项目名称
react-native run-ios
```

> 提示：如果run-ios无法正常运行，请使用Xcode运行来查看具体错误（run-ios的报错没有任何具体信息）。
