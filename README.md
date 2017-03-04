# Paulpang

### 使用说明

本博客是参考[leopard](http://baixin.io)的模板而搭建的个人博客.具体使用说明请参考[leopard](http://baixin.io)


#### 安装步骤

##### 1. 创建Github 域名和空间
> * 注册[Github](https://www.github.com)账号;
> 
> * 点击首页任意位置出现的 New repository按钮创建仓库, Respository name 中的username.github.io 的username 一定与前面的Owner 一致，记住你的username下面会用到。     

##### 2. 获取博客模板

```bash
git clone https://github.com/leopardpan/leopardpan.github.io.git
```
进入到你这个文件夹里面,然后这个模板使用git push到你的username.github.io仓库里面

##### 3. 安装Jekyll

```bash
gem install jekyll
注意:如果您的Homebrew安装在/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)",这时候需要下面的安装方式

sudo gem install -n /usr/local/bin jekyll
```

##### 4. 安装bundler

```bash
gem install bundler
或者
sudo gem install -n /usr/local/bin bundler
```
##### 5. 运行bundler
```bash
bundle install
```
##### 6. 启动本地服务

```bash
jekyll server
```
 
在浏览器输入 [127.0.0.1:4000](127.0.0.1:4000) ， 就可以看到博客效果了。


##### 7. 修改模板样式

>* 如果你想使用这个模板，请把 _posts/ 目录下的文章都去掉。
>* 修改 _config.yml 文件里面的内容为你自己的个人信息。



<br>

本博客在[Vno Jekyll](https://github.com/onevcat/vno-jekyll)基础上修改的。  