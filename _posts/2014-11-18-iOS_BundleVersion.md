---
layout: post
title: iOS开发中BundleVersion的规范使用
date: 2014-11-18 
tags: iOS    
---
最近在查看AppStore上面的App的时候,发现很多公司的版本号使用的不是太规范,下面来介绍一下BundleVersion的规范使用.

#### 版本号的格式：
```bash
v<主版本号>.<副版本号>.<发布号>
```
版本号的初始值：v1.0.0
#### 管理规则:

##### 主版本号（Major version）

```bash
1.  产品的主体构件进行重大修改，主版本号加1；
2. 产品的主体构件之间的接口协议重大修改，主版本号加1。
```

##### 副版本号（Minor version）

```bash
1. 主版本号变更时，副版本号置0；
2. 数据结构变更(新增或修改注释含义的情况除外)，副版本号加1；
3. 若副版本号累加至超过20时，采用主版本号进位制，主版本号加1，副版本号重新置0。
```

##### 发布号（Release）

```bash
1. 主版本号或副版本号变更时，Release号置0；
2. 若发布的版本无数据结构变更，则Release号加1。
```
注意: CFBundleVersion:内部版本号, 团队开发中内部只用的，只有我们自己可以看到.

以上是关于版本号的介绍,希望对大家有所帮助.




