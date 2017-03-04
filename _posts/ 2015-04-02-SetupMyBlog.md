---
layout: post
title: 如何搭建个人的免费博客
date: 2015-04-02 
tag: 技术 
---
本文主要针对mac OS进行搭建自己的博客,具体步骤如下:
#### 1. 创建Github 域名和空间
##### 1.1注册

首先你需要注册一个[Github](https://www.github.com)!账号，已有的可以下翻去1.2 创建仓库，注意username，这会影响到你的域名，你的域名将会是 username.github.io ，所以认真的取个名字吧。


##### 1.2 创建仓库

然后需要创建一个仓库(repository) 来存储我们的网站，点击首页任意位置出现的 New repository按钮创建仓库, Respository name 中的username.github.io 的username 一定与前面的Owner 一致，记住你的username下面会用到。

第一步就已经完成了，下面是安装。

#### 2. 安装

[Hexo](https://hexo.io/zh-cn/docs/index.html) 可以说是目前最流行的博客框架了，基于Nodejs，更多信息可以google，下面需要安装的工具包括 Git，Nodejs，Hexo。（Windows 用户自行搜索这些工具，直接安装即可，试过基本没啥问题）

+ 安装Git
我就想问问，还有谁没装Git么？

```bash
// 如果已安装HomeBrew 无需执行此行
 $ /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

 $ brew install git   // 安装Git
```

你也可以通过下载[安装程序](https://sourceforge.net/projects/git-osx-installer/)来安装

+ 安装Nodejs

先安装nvm，这是Nodejs版本管理器，可以轻松切换Nodejs版本。 这里有两种方式安装。如果使用curl的方式安装，安装完成之后一定要重启终端。

```bash
 1. Homebrew 安装方式，此安装方式无需重启
 $ brew install nvm  
 $ mkdir ~/.nvm
 $ export NVM_DIR=~/.nvm
 $ . $(brew --prefix nvm)/nvm.sh

 2. curl安装方式
 $ curl https://raw.github.com/creationix/nvm/master/install.sh | sh
```
安装完成后，<strong>重启终端</strong> 并执行下列命令即可安装 Node.js。

```bash
 $ nvm install 4
```

+ 安装Hexo

以上所有都安装完成之后再安装Hexo

```bash
$ sudo npm install hexo-cli -g
```

所有必须工具已经安装完成，下面我们就可以生成博客，上传至我们的Github 仓库了。

#### 3. 编写，发布
接下来我们需要用Hexo初始化一个博客，然后更改一些自定义的配置，或者加上自己喜欢的主题，写上第一篇文章，然后发布到自己的个人Github网站(username.github.io)。

##### 1. 创建博客
将下面的 username 替换成你自己的username(其实也无所谓，作者强迫症)，执行成功后，会创建出一个名为 username.github.io 的文件夹。

```bash
$ hexo init username.github.io

```
##### 2.更改配置
<strong>主题安装</strong>

为了使博客不太难看，我们需要安装一个主题，切换至刚刚生成的Hexo 目录，安装主题

```bash
$ cd username.github.io
$ git clone https://github.com/iissnan/hexo-theme-next themes/next
```

这里选了一个极简的主题，也是Hexo众多主题中最受欢迎的一个。上面出现的喵神的主题 在[这里](https://github.com/monniya/hexo-theme-new-vno)。Hexo也有[更多主题](https://hexo.io/themes/)供你选择。

<strong>基础配置：</strong>打开文件位置username.github.io/_config.yml修改几个键值对，下面把几个必须设置的列出来按需求修改，记得保存， 还有注意配置的键值之间一定要有空格。[更多设置](https://hexo.io/zh-cn/docs/configuration.html)...

```bash
title: dimsky 的 9 维空间    //你博客的名字
author: dimsky  //你的名字
language: zh-Hans    //语言 中文
theme: next   //刚刚安装的主题名称
deploy:
   type: git    //使用Git 发布
   repo: https://github.com/username/username.github.io.git    // 刚创建的Github仓库
```

<strong>主题配置：</strong>

主题配置文件在username.github.io/themes/next/_config.yml中修改，这里略过。[设置详情](http://theme-next.iissnan.com/getting-started.html#theme-settings)

##### 3.写文章
所有基础框架都已经创建完成，接下来可以开始写你的第一篇博客了
在username.github.io/source/_posts下创建你的第一个博客吧，例如，创建一个名为FirstNight.md的文件，用Markdown大肆发挥吧，注意保存。
如：

```bash
---
 title: First Night
 ---
 > 你好,Paulpang!
```
##### 4. 测试
```bash
 $ hexo s
```
测试服务启动，你可以在浏览器中输入https://localhost:4000 访问了。
##### 5. 安装hexo-deployer-git自动部署发布工具

```bash
 $ npm install hexo-deployer-git --save
```

##### 6. 发布
测试没问题后，我们就生成静态网页文件发布至我们的Github pages 中。

```bash
 $ hexo clean && hexo g && hexo d
```
如果这是你的第一次，终端会让你输入Github 的邮箱和密码，正确输入后，稍等片刻，就会把你的博客上传至Github 了。以后在每次把博客写完后，执行一下这个命令就可以直接发布了.

到此您已经拥有了属于自己的博客了,开始尽情的玩耍吧!
[https://Paulpang.github.io](https://Paulpang.github.io)



