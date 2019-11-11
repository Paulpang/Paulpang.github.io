---
layout: post
title: ReactNative自定义组件之PropTypes
date: 2017-05-18
tag: ReactNative
---

在实际开发中,我们经常需要自定义组件,而且需要在自定义组件是设置属性和方法.那么如何自定义组件? 如何将属性和方法暴露出去,供外界调用呢? 下面我们研究一下这些问题.

### 一、如何自定义组件？

* 首先创建一个.js文件 例如
```bash
BannerView.js
```
* 导入常用组件

```bash

// 1.导入组件(面向组件),React(JSX)
// React:默认组件,不需要添加{}
// Compoent:非默认组件,需要添加{}
import React, {Component,PropTypes} from 'react'

// 2.导入常用组件,注册组件,样式组件,View组件,Text组件
import
{
    AppRegistry,
    StyleSheet,
    Text,
    View,
    TouchableOpacity,
    Button,
    TextInput,
    Image,
    Dimensions
}
    from 'react-native'
```
* 自定义组件

```bash
// 自定义组件
export default class 自定义组件的名称 extends Component{

这里写code, 所有的自己属性/方法.以及子控件都在这里处理
	render() {

		return (
			<View></View>
		);
	}
}

```
### 二、如何将属性和方法暴露出去?
利用`PropTypes`来解决这个问题,在`PropTypes`类里面定义属性和方法 ,可以是外界在使用这个自定义组件的时候,能够`自动有属性功能`的提示.

#### PropTypes的作用
* 暴露属性,让外界有提示功能
* 检查属性类型
* PropTypes里面定义的属性,只能声明属性,不会实现属性,因此在使用属性的时候,必须需要外界给赋值才能使用.
* 如果在自定义控件的render方法中需要用到propTypes里面的属性,这时候需要在render方法中使用

	```bash
	<Text>{this.props.属性名称}</Text>
	不能使用
	<Text>{this.属性名称}</Text>
	```

##### 注意
* <strong>PropTypes必须要用static声明，否则无效果。</strong>
* <strong>propTypes:定义(声明)属性, 但不会真正生成属性</strong>
* <strong>static：用来定义类方法或者类属性，定义类的方法和属性，生成的对象就自动有这样的属性了。</strong>
* <strong>PropTypes 只能用于React框架的自定义组件，默认JS是没有的，因为它是React框架中的。</strong>

### 三、PropTypes的属性类型

```bash
# 数组类型
PropTypes.array

# 布尔类型
PropTypes.bool

# 函数类型
PropTypes.func

# 数值类型
PropTypes.number

# 对象类型
PropTypes.object

# 字符串类型
PropTypes.string

# 规定prop为必传字段
PropTypes.func.isRequired

# prop可为任意类型
PropTypes.any.isRequired

```

<strong>注意 :</strong> 如果PropTypes里面的属性或者方法是外界必须实现的,这时候需要这个属性或方法后面加上 isRequired来修饰 例如: 

```bash
 // 定义属性
    static propTypes = {
        name:PropTypes.string.isRequired, // 必须实现的属性
        age:PropTypes.number // 定义方法(外界可实现和不实现)
    }
```

### 四、PropTypes的使用步骤 

1. PropTypes:属性检测，使用的时候需要先导入，在React框架中

```bash
import React, { Component,PropTypes } from 'react';
```
2. 在类方法中定义属性/方法

```bash
// 自定义组件
export default class XMGCompoent extends Component{

    static propTypes = {
       name:PropTypes.string.isRequired, // 定义属性
       click:PropTypes.func    // 定义方法
    }
}

```
3.如果需要自定义属性并设置初始化值需要用 `defaultProps`来设置

```bash
// 自定义属性，设置初始值
// 生成属性,初始化值,给props初始化值
static defaultProps = {
    name:'xmg',
    age:20
}

```
<strong>注意 : `defaultProps` : 底层就会把类属性defaultProps里面的值赋值给props.</strong>

### 五、案例代码

```bash
/**
 * Created by Paul on 2017/5/18.
 */

import React, { Component,PropTypes } from 'react';
import {
    AppRegistry,
    StyleSheet,
    Text,
    View,

} from 'react-native';

export default class BannerView extends Component {

    // 定义属性
    static propTypes = {
        name: PropTypes.string.isRequired,
        age:PropTypes.number
    }

    // 初始值
    static defaultProps = {
        name:'Paul',
        age:28
    }

    render() {
        // 打印出来, 
        console.log(this.props.name)
        return (
            <View>

            </View>
        )
    }

}


```


