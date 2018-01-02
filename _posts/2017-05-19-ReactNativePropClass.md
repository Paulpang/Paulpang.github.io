---
layout: post
title: ReactNative自定义类
date: 2017-05-19
tag: HTML+ReactNative
---
在实际开发中,我们经常需要自定义类,那么如何自定义类?如何给类的对象添加属性/方法? 如何给类添加类属性/类方法呢?

### 1、如何自定义类

```bash
// 自定义类
export default class Person {

	实现代码
}

```
### 2、如何给自定义类添加对象属性/方法

```bash
// 自定义类
export default class Person {

	// 在自定义类中,如果需要给这个类的对象定义属性,需要用=
	name = 'Paul'
	age=10;
	
	// 对象方法
    eat(){
        console.log('对象吃饭了吗?');
    }
}

```
<strong>注意 : 在外界调用这个类的是方法的时候,外界需要创建对象.然后拿能拿到属性,例如:</strong>

```bash
var person = new Person();
person.name = "Paulpang"
```
### 3、如何给自定义类添加类属性/方法

```bash
// 自定义类
export default class Person {

	// 类属性
    static money = 10;
    // 类方法
    static eat(){
        console.log('类方法-吃');
    }
}

```
<strong>注意 : 在外界调用这个类的是方法的时候,直接用类名调用就可以拿到该属性,例如:</strong>

```bash
Person.name = "Paulpang";
```

