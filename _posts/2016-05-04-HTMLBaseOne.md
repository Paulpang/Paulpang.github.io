---
layout: post
title: HTML基础(一)
date: 2016-05-04
tag: HTML + ReactNative
---
## 一、HTML标签介绍:


### 1. 单标签:

* 文本注释标签
	
	```
	command + /
	```
	
* 文本换行标签

	```
	<br>
	```
* 横线标签

	```
	<hr>
	```

### 2. 双标签:


 * 段落标签  `<p></p>`
 
 * 标题标签  `<hn> </hn>  其中 (n = 1,2,3,4,5,6)`

 * 文本标签  `<font></font>`
 
 * 文字加粗显示 `<strong></strong>或者<b></b>`
 		
 * 文字斜体显示 `<em></em>或者<i></i>`
 			
 * 文字删除线`<del></del>或者<s></s>`
 			
 * 文字下横线标签`<ins></ins>或者<u></u>`
 	
 
### 3. 图片标签<img>

* 格式

	```
	<img src="1.jpg" title= "哈哈">
	```
* 属性

	* Src: 设置显示图片（图片名称或者图片路径）
	* Title：用来设置鼠标方到图片上显示的文字
	* Alt：当图盘无法正常显示的时候，对图片的描述
	* Width: 用来设置图片宽度
	* Width: 用来设置图片宽度
	
### 4. 超链接 (a)

 * 格式

	```
	<a href="http://www.baidu.com">百度</a>
	```
* 属性

	* Title: 当鼠标放到超链接上显示的文字
	* target="_self"    默认值  网页在当前页面中打开
	* target="_blank"   网页在新窗口中打开

### 4. 锚链接 (a)

 * 任何一个标签设置id属性，并取值

	```
	<p id="db">百度</p>
	```
* 给a标签设置href属性  “#id名称”

	```
	<a href="#db">返回顶部</a>
	```
<strong> 注意: 文字和图片都可以设置超链接</strong>




# 二、列表


### 1. 无序列表(ul)

* 格式

	```
	<ul>
		<li></li>  // 列表项
		<li></li>
		<li></li>
		<li></li>
		<li></li>
		 ......
	</ul>
	```	
* 属性:

	* type="square"     小方块显示
	* type="square"     小方块显示


### 2. 有序列表（ol）

* 格式

	```
	<ol>
		<li></li>  // 列表项
		<li></li>
		<li></li>
		<li></li>
		<li></li>
		 ......
	</ol>
	```	
* Type属性:

	* A, a ，  i (小写的罗马数字)  I(大写的罗马数字)
	* start="3", li前面的显示从第几个开始
	
### 3. 自定义列表（dl）

* 格式

	```
	 <dl>
		<dt>售后服务</dt>  小标题
		<dd>收货地址</dd> 列表项
		<dd>在线支付</dd>
		<dd>客服电话</dd>
	 </dl>
	```

### 4.特殊字符

常用的几个特殊字符

```
空格符  &nbsp
<      &It
>      &gt

```

# 二、Meta标签介绍

## 1 Meta介绍
### 1.1 编码格式

```
<meta  charset="utf-8">
```
 * Charset：字符集
 * utf-8 : 编码格式
 
#### 1.2 对网站进行优化的作用  SEO
```
<meta  name="keywords"  content="p2p理财,互联网金融,投资">
```


```
<meta  name="description" content="互联网金融,投资出借,p2p借贷">
```

#### 1.3  网页重定向
```
<meta http-equiv="refresh"  content="5;url=http://www.baidu.com">
```

### 2. Link标签介绍

#### 2.1 给网页titile中放置小图标(内部样式)

```
<link  rel="icon"  href="favicon.ico">
```

#### 2.2 给网页titile中放置小图标(外部样式)
```
<link rel="stylesheet"   href="1.css">
```
# 三、表格(table)

#### 0. 作用：显示数据
### 1. 格式

```
<table>                        // 定义表格
	<tr>                        // 行
		<td>姓名</td>
		<td>年龄</td>            // 列(单元格)
		<td>职业</td>
		<td>籍贯</td>
	<tr>
</table>
```
### 1.2 属性介绍

*  border:   设置表格边框
*  width:  设置表格宽度
*  Height:   设置高度
*  cellspacing：设置单元格之间的距离
*  cellpadding：文字距离单元格边框的距离
*  bgcolor="red"   设置背景颜色
*  align=center,left,right  给td或者tr设置让文字居中
*  table设置表格居中
*   设置表格标题，用法和td一样<th></th>

### 1.3 设置表格表头

```
<caption> <h4>通讯录</h4> </caption>
```
# 四、表单(form)

### 1.1 作用

* 表单的作用用来收集信息

#### 1.2 组成

* 提示信息
* 表单控件

#### 1.3 表单格式

```
	<form action = "" method = "post">
	
	</form>
```
#### 1.4 属性
* action：  处理用户数据信息
* Method：get 或者 post

### 2. 表单控件

#### 2.1 文本输入框

```
<input type= "text" maxlength="6">
```
* maxlength：  设置文本输入框最多能输多少字符
* readonly="readonly"   设置文本输入框为只读（只能读不能编辑）
* disabled="disabled”	  控件属于非激活的状态
* name="username"				  给输入框设置名称
* Value=””				   设置或者显示输入的值


#### 2.2 密码输入框

```
<input type= "password">
```
* maxlength：  设置文本输入框最多能输多少字符
* readonly="readonly"   设置文本输入框为只读（只能读不能编辑）
* disabled="disabled”	  控件属于非激活的状态
* name="username"				  给输入框设置名称
* Value=””				   设置或者显示输入的值


#### 2.3 单选按钮

```
<input type= "radio" name= "sex" checked= "checked">男
<input type= "radio" name= "sex">女
```
<strong>
	注意：实现单选效果一定要给控件设置相同的名称
</strong>

* checked="checked"    设置默认选中项

#### 2.4 下拉列表

```
<select  multiple="multiple"> // 实现多选效果
	<option selected= "selected">北京</option>  // 设置默认选中项
	<option>上海</option>
	<option>深圳</option>
	<option>广州</option>
</select>
```
#### 2.5 多选控件

```
<input type= "checkbox"  checked= "checked">抽烟
<input type= "checkbox"  checked= "checked">喝酒
<input type= "checkbox"  checked= "checked">写代码
```
<strong>设置默认选中项： checked=checked</strong>


#### 2.6 多行文本输入框

```
<textarea>
	
</textarea>
```
#### 2.7 上传图片控件

```
<input type="file">
```
#### 2.8 表单提交按钮

```
<input type="submit">   // 表单提交按钮
```

#### 2.9 普通按钮

```
<input type="button" value="普通按钮">   // 表单提交按钮
```
<strong>注意：该按钮不能进行表单提交。通常和js代码配合使用</strong>

#### 2.10 重置按钮

```
<input type="reset">  
```
<strong>
	将控件中的值恢复到默认值状态
</strong>

#### 2.11 图片按钮

```
<input type="image" src="button.jpg">  
```
<strong>
	该控件也可以进行表单的提交
</strong>

#### 2.12 表单分支控件

```
<fieldset>  
	<legend>用户注册</legend>
</fieldset>
```

