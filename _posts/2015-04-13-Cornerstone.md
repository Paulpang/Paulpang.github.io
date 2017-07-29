---
layout: post
title: Cornerstone
date: 2015-04-13 
tags: iOS    
---


#### 一. 将服务器文件下载到本地

* 打开Cornerstone,点击 "+" 添加服务器的地址/昵称名称/用户名/密码
   
　　
#### 二. 将远程代码库checkout到本地
* 点击Checkout按钮----->点击Additional Options --->Format 选择最新版本 ----> 然后点击确认Checkout

注意: 选择最新版本的目的是为了忽略部分带"?"的文件

#### 三. 在本地目录下创建项目


#### 四. 打开Cornerstone进行提交项目

* 选择要提交的项目,点击Commit----> 弹出一个提示框 -----> 选择Ignore进行提交.

注意:

1. 在提交的时候,不能选择 Commit Anyway ,而是选择Ignore,目的是为了忽略没用的文件
2. 在提交代码的时候,如果发现xcuserdata/xcshareddata 没有被忽略掉, 我们需要手动删除这两个文件, 然后在提交, 提交完以后在点击这两个文件右击 选择忽略就ok了




#### 五. 合并分支到主干

```bash
* Trunk		主干,一般项目开发都在主干进行开发
* Tags 		存放已经上线的重大版本号
* Branches 	当发生重大Bug或者有新的需求的时候,创建一个分支,在分支上开发,开发完成后,在合并到主干
```
1. 当在主干Trunk上完成1.0版本,上架后,需要打一个Tag 进行1.0版本的备份 :  选择REPOSITORIES ---->点击主干上的项目-----> 右击---->Tag...---->Where右边按钮现在tags文件夹的位置 --->Tag As: 注释
2. 当Appstore上1.0版本有重大Bug时, 需要将Tag中1.0版本创建一个分支进行bug修复. 选择REPOSITORIES----> 选择Tags中的1.0版本----->右击选择Branch...----->Where右边按钮现在Banches文件夹的位置 --->Banch As: 注释 ------> Create Branch
3. 选择REPOSITORIES----> 选择Branches中的1.0版本-----> 点击Checkout 将分支中的1.0版本下载到本地解决bug

4. 在本地,当分支上的Bug修复完成以后,,将代码commit提交到分支服务器上面,
5. 在REPOSITORIES中,将分支上面的修复Bug的版本也打tag 版本1.1放到Tags目录下,修复bug版本为1.1

6. 将服务器上1.1版本合并到本地的主干上面 : 选择WORKING COPIES下面的本地主干代码区域模块中的项目(不是文件夹)----> 点击Merge合并按钮 -----> 点击Merge from 右侧的按钮选择合并到REPOSITORIES下面----->分支下面的1.1bug修复版本----->点击 Merge Changes按钮就行合并

注意: 如果合并的时候出现冲突 , 点击选择WORKING COPIES---->打开本地主干Trunk的代码 ----> 解决冲突,一般只需要删除>>>>>/=====/<<<<< 就可以了 -----> 解决完冲突后---->点击Resolve------>点击Commit按钮将解决后的代码提交到主干服务器

这样,就完整的将分支的代码合并到主干上面了




#### 六. Xcode中配置SVN

1. 打开Xcode --->偏好设置--->Accounts ---> 选择"+" ---> Add Repository ----> 添加 svn地址 type类型为Subversion  UserName 和Password ------> 点击Add.
2. 这样就可以直接用Xcode来提交代码了,就不用Cornerstone了



































