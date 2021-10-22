---
layout: post
title: HTML属性(三)
date: 2016-05-06
tag: HTML
---

## 列表

#### 有序列表：ol、li

* ol （ordered list）有序列表，直接子元素只能是li
* li （list item）列表中的每一项

格式:

```
	<ol>
		<li></li>
		<li></li>
		<li></li>
	</ol>

```
#### 无序列表 ul、li

* ul （unordered list）无序列表，直接子元素只能是li
* li （list item）列表中的每一项

格式:

```
	<ul>
		<li></li>
		<li></li>
		<li></li>
	</ul>

```

#### 定义列表 dl、dt、dd

* dl（definition list） 定义列表，直接子元素只能是dt、dd
* dt（definition term） 列表中每一项的项目名
* dd（definition description）列表中每一项的具体描述，是对 dt 的描述、解释、补充
* 一个dt后面一般紧跟着1个或者多个dd
* dt、dd常见的组合
	* 事物的名称、事物的描述
	* 问题、答案
	* 类别名、归属于这类的各种事物

### 列表相关的CSS属性

*	列表相关的常见CSS属性有4个：list-style-type、list-style-image、list-style-position、list-style
* 适用于display设置为list-item的元素，比如li元素
* 它们都可以继承，所以设置给ol、ul元素，默认也会应用到li元素
* list-style-type：设置li元素前面标记的样式
* disc（实心圆）、circle（空心圆）、square（实心方块）
* decimal（阿拉伯数字）、lower-roman（小写罗马数字）、upper-roman（大写罗马数字）
lower-alpha（小写英文字母）、upper-alpha（大写英文字母）
none（什么也没有）


* **list-style-image：**设置某张图片为li元素前面的标记，会覆盖list-style-type的设置
* **list-style-position：**设置li元素前面标记的位置，可以取outside、inside2个值
* **list-style：**是list-style-type、list-style-image、
* **list-style-position**的缩写属性
* **list-style:** outside url("images/dot.png");
* 一般最常用的还是设置为**none**，去掉li元素前面的默认标记 list-style: none;

### 表格

#### table (表格)

**常用属性**

* border 边框的宽度
* cellpadding 单元格内部的间距
* cellspacing 单元格之间的间距
* width 表格的宽度
* align 表格的水平对齐方式 left、center、right

#### tr (表格中的行)
**常用属性**

* valign 单元格的垂直对齐方式
* top、middle、bottom、baseline
* align 单元格的水平对齐方式 left、center、right


#### td (行中的单元格)

* valign 单元格的垂直对齐方式
* top、middle、bottom、baseline
* align 单元格的水平对齐方式 left、center、right
* width 单元格的宽度
* height 单元格的高度
* rowspan 单元格可横跨的行数
* colspan 单元格可横跨的列数

#### 表格的CSS属性

* table的border-spacing用于设置单元格之间的水平、垂直间距

#### 表格细线

```
table {
	border-collapse: collapse;
}

td {
	border: 1px solod #000;
}

```


## 表单

### form 表单
一般情况下，其他表单相关元素都是它的后代元素

form常用属性
* action 用于提交表单数据的请求URL

* method 请求方法（get和post），默认是get

* target 在什么地方打开URL（参考a元素的target）
* enctype 规定了在向服务器发送表单数据之前如何对数据进行编码
* 取值有3种
	* application/x-www-form-urlencoded：默认的编码方式
	* multipart/form-data：文件上传时必须为这个值，并且method必须是post
	* text/plain：普通文本传输
* accept-charset：规定表单提交时使用的字符编码



### input
单行文本输入框、单选框、复选框、按钮等元素

#### input常用属性
* type：input的类型
* text：文本输入框（明文输入）
* password：文本输入框（密文输入）
* radio：单选框
* checkbox：复选框
* button：按钮
* reset：重置
* submit：提交表单数据给服务器
* file：文件上传
* hidden：隐藏域
* maxlength：允许输入的最大字数
* placeholder：占位文字

* readonly：只读
* disabled：禁用
* checked：默认被选中 只有当type为radio或checkbox时可用
* autofocus：当页面加载时，自动聚焦
* name：名字 在提交数据给服务器时，可用于区分数据类型
* value：取值
* form：设置所属的form元素（填写form元素的id） 一旦使用了此属性，input元素即使不写在form元素内部，它的数据也能够提交给服务器

**布尔属性**

* 常见的布尔属性有disabled、checked、readonly、multiple、autofocus、selected
* 如果要给布尔属性设值，值就是属性名本身
* 布尔属性可以没有属性值，写上属性名就代表使用这个属性

**input按钮**

* 普通按钮（type=button）：使用value属性设置按钮文字
* 重置按钮（type=reset）：重置它所属form的所有表单元素（包括input、textarea、select）
* 提交按钮（type=submit）：提交它所属form的表单数据给服务器（包括input、textarea、select）
* 默认情况下，敲回车键（Enter）会自动提交表单数据给服务器


### textarea
多行文本框

缩放的CSS设置

* 禁止缩放：resize: none;
* 水平缩放：resize: horizontal;
* 垂直缩放：resize: vertical;
* 水平垂直缩放：resize: both;


### select、option
下拉选择框 
option是select的子元素，一个option代表一个选项

```
<select name="edu">
	<option></option>
	<option></option>
	<option></option>
</select>
```

* select常用属性
	* multiple：可以多选
	* size：显示多少项
* option常用属性
* selected：默认被选中


### button
使用button元素也能实现按钮，功能效果跟input一样

* 普通按钮（type=button）：使用value属性设置按钮文字
* 重置按钮（type=reset）：重置它所属form的所有表单元素（包括input、textarea、select）
* 提交按钮（type=submit）：提交它所属form的表单数据给服务器（包括input、textarea、select）
* 默认情况下，敲回车键（Enter）会自动提交表单数据给服务器


### label

* label元素一般跟input配合使用，用来表示input的标题
* labe可以跟某个input绑定，点击label就可以激活对应的input,必须用id绑定

```
<label for="username">用户名</label>
<input id="username" type="text" name="username"></input>

```


### fieldset
表单元素组

### legend
fieldset的标题


