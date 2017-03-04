---
layout: post
title: CocoaPods系列之一: CocoaPods的安装
date: 2016-04-14
tag: 工具

---
cocoapods能够帮助我们快速的搜索到第三方框架,然后自动集成到工程里面,并编译成一个libPod.a的静态库给我们项目使用.

在安装cocoapods的时候,首先安装gem,然后通过gem来安装cocoapods.

### 一. gem的安装

Gem是一个管理Ruby库和程序的标准包，它通过Ruby Gem（如 [http://rubygems.org/](http://rubygems.org/) 或者修改镜像[http://ruby.taobao.org/](http://ruby.taobao.org/)）源来查找、安装、升级和卸载软件包，非常的便捷。

##### 安装gem的常用命令如下:

<strong>1. 查看gem版本</strong>
	
```bash
gem --version	
```
<strong>2. 更新gem</strong>
 
```bash 
gem update --system
```
注解: sudo 是以超级管理员的身份操作
 
<strong>3. 查看数据源 </strong>
 
```bash
 gem sources

```
<strong> 4. 删除数据源</strong>
 
```bash
 gem sources --remove https://rubygems.org/
```
 
<strong>5. 添加数据源</strong>
 
```bash
 gem sources -a https://ruby.taobao.org/
```
<strong>6. 搜索软件包</strong>

```bash
 gem search 软件包关键字
```
 
<strong>7. 安装软件包</strong>
 
```bash
gem install 软件包名称
```
  
<strong>8. 安装上一个版本软件包</strong>

 ```bash
 gem install cocoapods --pre
 ```
<strong>9. 卸载安装包</strong>

```bash
gem uninstall 软件包名称
```
 
注意: 以上命令最好使用之前,都添加上sudo,作用是以管理员身份运行该命令.

有时候我们在安装的时候会安装失败,可能由于ruby的版本过低导致的升级失败,如果遇到这种情况,可以安装RVM版本管理器来升级ruby,具体操作如下:

<strong>A. 安装RVM</strong>

```bash
curl -L get.rvm.io | bash -s stable
```
<strong>B. 验证是否安装成功</strong>

```bash
rvm -v
```
<strong>C. 查看ruby版本</strong>

```bash
ruby -v
```
<strong>D. 列出当前所有可用版本</strong>

```bash
rvm list known
```
<strong>E. 安装指定版本ruby</strong>

```bash
rvm install ruby --head
```
如果安装失败, 可能是没有安装homebrew, 先安装即可,具体如何安装homebrew,请查看安装方法: [Homebrew](http://brew.sh/index_zh-cn.html)

### 二. 使用gem安装cocoapods

```bash
sudo gem install cocoapods
```
如果安装失败,可能是由于gem版本过低,需要更新gem再次安装.

```bash
sudo gem update --system
sudo gem uninstall cocoapods
sudo gem install cocoapods
```
当macOS系统升级到10.11后,Cocoapods报错: ```bashERROR: While executing gen ...(Errno
:EPERM) Operation not permitted - /usr/bin/pod```这时候需要以下操作:

```bash
sudo gem update --system
sudo gem uninstall cocoapods
sudo gem install -n /usr/local/bin cocoapods
```
### 三. 验证是否安装成功

```bash
pod --version
```

通过以上的操作,恭喜你,你已经成功的安装了cocoapod了,接下来你就可以快乐的玩耍了.

 
 
 
 
 
 
 
 
 
 
