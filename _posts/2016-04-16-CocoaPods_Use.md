---
layout: post
title: CocoaPods的使用
date: 2016-04-16 
tag: iOS 
---
上一篇我们已经介绍了[cocoapods的安装](https://paulpang.github.io/2017/02/28/cocoapods系列之----cocoapods的安装/),接下来我们来说一下cocoapods是如何使用的.对于cocoapods的使用分为两种:<strong>使用框架的人</strong>和<strong>开发框架的人</strong>分别需要怎么操作. 

接下来我们首先介绍一下使用框架的人改如何操作:
### 一. 使用框架的人如何做

#### 1.检索第三方框架

```bash
pod search 框架关键字
```
注意:pod search内部是从本地缓存的"第三方框架描述信息" 生成的检索文件中检索到 相关框架的信息.如果遇到```bash[!]Unalbe to find a pod with name,author,summary,or descriptionmatching "AFNetworing"```这种错误时,需要删除cocoapods索引文件:```rm ~/Library/Caches/CocoaPods/search_index.json```

#### 2. 安装第三方框架

##### 2.1 创建Podfile文件

```bash
pod init
```
Podfile文件的作用是使用ruby语法编写的 "框架依赖描述文件"; 就是告诉cocoapods需要下载集成哪些框架,常见配置语法请参见简书[Podfile语法](http://www.jianshu.com/p/8af475c4f717)

##### 2.2 安装框架

```bash
pod install
```
pod install内部主要做了一下事情:如果cocoapods是1.0.1版本及以后版本,直接就是根据 Podfile 文件找到框架信息, 然后下载集成; 如果是之前版本,首先先更新本地框架信息源信息(由于比较耗时,做好后面添加--no-repo-update),然后在根据 Podfile 文件找到框架信息, 然后下载集成.

在安装的时候若出现```bash The dependency 'ANNetworking' is not used in any concrete target```错误,原因是<font color=gray size=2>由于Podfile文件的描述中没有描述Xcode工程中的targets,如果在老版本没有指明, CocoaPods会创建一个名称为default的隐式target，会和我们工程中的第一个target相对应;在1.0.1版本之后, 要求必须指明才可以.</font>

解决方案: 需要指定一栏的目标target,在Podfile文件中添加
<font color=red face=“黑体” size=2> target "项目名称"</font>; 如果让多个target使用同一个Pod依赖库,可用使用<font color=red face="黑体", size=2>link_with "FirstTarget","SecondTarget"</font>,具体使用技巧可用查看<strong>[cocoaPods官网](https://guides.cocoapods.org)</strong>

在输入pod install后,会生成一个叫Podfile.lock的文件,这个文件的作用是记录着上一次下载的框架的最新版本

#### 3. pod install 和 pod update的区别


```bash
pod install:
	如果Podfile.lock文件存在, 直接从此文件中读取框架信息下载安装;
	如果不存在, 依然会读取Podfile文件内的框架信息,下载好之后, 再根据下载好的框架信息, 生成Podfile.lock文件
	
pod update
	不管Podfile.lock是否存在, 都会读取Podfile文件的的框架信息去下载,下载好之后, 再根据下载好的框架信息, 生成Podfile.lock文件
	
主要区别在于, Podfile文件内的框架信息, 版本描述没有指定具体版本	
```
<strong>实际项目开发过程中, 该如何选择install 和 update 命令??</strong>

```bash
如果是多人开发,根据自己以往的经验:

一般情况下, 每个人从共享库把项目下载下来之后, 都会执行pod install 命令安装!! 而不是选择 pod update ,目的: 是为了保证大家使用的第三方框架版本一致!!

如果以后大家需要统一升级第三方框架, 那么每个人在执行 pod update
```

### 二. 开发框架的人如何做

##### 1. 创建库工程, 添加源文件到Classes文件夹

#### 2. 上传项目到github, 并且打好标签

```bash
git push origin master
git tag '1.0.0' 
git push --tags 
```
#### 3. 配置并上传框架的  PodSpec 文件, 并使用trunk的方式上传

##### 3.1 创建Podspec文件

```bash
pod spec create 文件名称
```
PodSpec文件主要是描述自己的框架信息,如:作者,版本,下载地址等等.pod install 就是根据这个文件里面的源文件路径进行安装的.<strong>注意: 一般这个文件的名称和工程名称保持一致</strong>

##### 3.2 验证文件内容格式

```bash
pod spec lint podspec文件
```
##### 3.3. 注册trunk

```bash
pod trunk register xxx@qq.com 'Paulpang'  --verbose

--verbose参数是为了便于输出注册过程中的调试信息
```
如果出现<font color= red size= 2>ACE,YOU'RE SET UP.</font>说明已经注册成功,然后在终端输入 pod trunk push 项目名 进行提交

##### 3.4 通过trunk推送podsspec文件进行提交

```bash
pod trunk push 项目名
```
注意: 这种方式其实就是上传这个描述文件到cocoapods在github上的仓库中[https://github.com/CocoaPods/Specs](https://github.com/CocoaPods/Specs);你也可以按照正常的操作, 先fork , 然后提交 pull request

##### 3.5 等待审核

#### 4. 更新本地pod 第三方框架信息数据源

```bash
pod setup
```
注意: 可以省略这一步骤, 因为上述提交, 直接更新了本地索引库

#### 5. 测试

```bash
使用pod search 命令搜索自己的框架, 如果可以搜索到, 那么代表审核通过了
```

### 三. cocoapods相关操作

#### 1. 查看第三方框架仓库源

```bash
pod repo
```
#### 2. 移除仓库源

```bash
pod repo remove master
```
#### 3. 添加仓库源

```bash
pod repo add master http://git.oschina.net/akuandev/Specs.git
```
#### 4. 初始化(下载服务器中所有第三方框架信息, 缓存到电脑本地)

```bash
pod setup
```

### 四. cocoapods几个重要的路径介绍

#### 1. 索引缓存路径

```bash
 ~/Library/Caches/CocoaPods/
```
如果发现框架信息本地已经缓存, 但是就是无法搜索框架, 可以删除这个索引文件, 重新生成

#### 2. pod命令安装路径

```bash
/usr/local/bin
```
#### 3. pod 框架索引信息缓存路径

```bash
/Users/apple/.cocoapods/repos/master
```

以上就是cocoapods的简单使用和原理介绍.如有疑问,请给我留言.









































