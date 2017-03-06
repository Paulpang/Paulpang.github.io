---
layout: post
title: 开发框架的人如何用CocoaPods ?
date: 2016-04-17 
tag: iOS 
---
上一篇我们已经介绍了[cocoapods的安装](https://paulpang.github.io/2016/04/Cocoapods_Install/)以及[使用框架的人如何使用CocoaPods](https://paulpang.github.io/2016/04/CocoaPods_Use/),接下来我们来说一下对于<strong>开发框架的人</strong>改如何将开发的框架上传到cocoapods供别人使用.


### 开发框架的人如何将框架发布到CocoaPods上

##### 0. 在本地创建一个文件夹,用来你开发框架的文件

##### 1. 首先在Github上面创建一个库

注意: 如果这个库里面创建的有readme,gitignore等文件,这时候需要现将远程文件pull到本地库所在的文件夹里面

```bash
git pull origin master
```
如果不这样做,你直接将本地的框架上传到github上面会报错,报错内容如下

```bash
To git@github.com:**/Demo.git 
! [rejected] master -> master (non-fast-forward) 
error: failed to push some refs to ‘git@github.com:**/Demo.git’ 
hint: Updates were rejected because the tip of your current branch is behind 
hint: its remote counterpart. Merge the remote changes (e.g. ‘git pull’) 
hint: before pushing again. 
hint: See the ‘Note about fast-forwards’ in ‘git push –help’ for details.
```

##### 2.  将你开发的框架代码Classes文件夹放到本地创建的文件夹中

#### 3. 上传项目到github, 并且打好标签

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

打印的信息如下:
opening connection to trunk.cocoapods.org:443...
opened
starting SSL for trunk.cocoapods.org:443...
SSL established
<- "POST /api/v1/sessions HTTP/1.1\r\nContent-Type: application/json; charset=utf-8\r\nAccept: application/json; charset=utf-8\r\nUser-Agent: CocoaPods/1.2.0\r\nAccept-Encoding: gzip;q=1.0,deflate;q=0.6,identity;q=0.3\r\nHost: trunk.cocoapods.org\r\nContent-Length: 68\r\n\r\n"
<- "{\"email\":\"pxj1314@hotmail.com\",\"name\":\"Paulpang\",\"description\":null}"
-> "HTTP/1.1 201 Created\r\n"
-> "Date: Mon, 06 Mar 2017 03:32:59 GMT\r\n"
-> "Connection: keep-alive\r\n"
-> "Strict-Transport-Security: max-age=31536000\r\n"
-> "Content-Type: application/json\r\n"
-> "Content-Length: 193\r\n"
-> "X-Content-Type-Options: nosniff\r\n"
-> "Server: thin 1.6.2 codename Doc Brown\r\n"
-> "Via: 1.1 vegur\r\n"
-> "\r\n"
reading 193 bytes...
-> "{\"created_at\":\"2017-03-06 03:32:59 UTC\",\"valid_until\":\"2017-07-12 03:32:59 UTC\",\"verified\":false,\"created_from_ip\":\"1.180.235.247\",\"description\":null,\"token\":\"40594b9963f55053ad8f25e9bd771a1e\"}"
read 193 bytes
Conn keep-alive
[!] Please verify the session by clicking the link in the verification email that has been sent to pxj1314@hotmail.com

```


##### 3.4 验证您的邮箱,一般cocoapods发的邮件在垃圾箱里面,打开邮箱里面的链接进行验证
如果出现<font color= red size= 2>ACE,YOU'RE SET UP.</font>说明已经注册成功,然后在终端输入 pod trunk push 项目名 进行提交

##### 3.5 通过trunk推送podspec文件进行提交

```bash
pod trunk push 项目名.podspec
```
注意: 这种方式其实就是上传这个描述文件到cocoapods在github上的仓库中[https://github.com/CocoaPods/Specs](https://github.com/CocoaPods/Specs);你也可以按照正常的操作, 先fork , 然后提交 pull request

##### 3.6 等待审核

#### 4. 更新本地pod 第三方框架信息数据源

```bash
pod setup
```
注意: 可以省略这一步骤, 因为上述提交, 直接更新了本地索引库

#### 5. 测试

```bash
使用pod search 命令搜索自己的框架, 如果可以搜索到, 那么代表审核通过了
```

#### 6. 创建一个pods库的模板库

cd 到框架的上一级目录,是Example和框架处于同一级

```bash
pod lib create 库的名称
```
提示信息:

> 1. What is your name?
> 
>  输入对应的信息: Paulpang
> 
> 2. What is your email?
> 
>	pxj1314@hotmail.com
>
> 3. What language do you want to use? [Swift/Objc]
> 
>  Objc
		
> 4. Would you like to include a demo application with your librara ? [Yes/No] // 是否需要一个测试的Demo
> 
>  Yes
> 
> 5. Which testing frameworks will you use? [Specta/Kiwi/None]
> 
>	None
>
> 6. Would you like to do view based texting? [Yes/No]
> 
>  No
>
> 7. What is your class prefix?
>
>	XJ




