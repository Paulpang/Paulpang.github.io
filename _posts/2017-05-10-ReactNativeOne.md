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