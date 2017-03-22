---
layout: post
title: runtime运行时的介绍和用法
date: 2016-09-20
tag: iOS
---
## runtime的理解:

```
1. runtime是一套比较底层的C语言的API,属于1个C语言库,包含了很多底层的C语言的API
2. 在开发中编写的OC代码,在程序运行过程中,最终都是转换成runtime的C语言进行编译和运行.

```
例如: 
```
Persion *p = [[Persion alloc] init];
```

在运行过程中转换成:

```
objc_msgSend(objc_msgSend("Persion","alloc"),"init")
```


## runtime的主要用途:

* 利用NSCodeing进行归档和反归档(利用runtime变量模型的对象的所有属性)
* 字典转模型(利用runtime变量模型的对象的所有属性,根据属性名从字典中取出对应的值,设置到模型的属性上面)
* KVO(利用runtime动态产生一个类)


---
* 导入头文件

```
#import <objc/runtime.h>
#import <objc/message.h>

```
 * 动态的创建一个类
 * 动态的为某个类添加(修改)属性\方法
 * 遍历一个雷的所有成员变量\属性\方法
 
---


### 1. 获取Person中所有的方法名称
```
    unsigned int couont = 0;
    /*
     第一个参数, 需要获取的类
     第二个参数, 获取到的个数
    */
    
    Method *methods = class_copyMethodList([Person class], &couont);
    for (int i = 0; i < couont; i++) {
        // 1.获取遍历到得方法名称
        SEL m = method_getName(methods[i]);
        // 2.将方法名称转换为字符串
        NSString *methodName = NSStringFromSelector(m);
        // 3.输出
        NSLog(@"%@", methodName);
    }

```

### 2. 获取对象的私有成员变量

 
```
 Ivar *var = class_copyIvarList([Person class], &couont);
   for (int i = 0; i < couont; i++) {
         // 1.获取遍历到得成员变量名称
         const char *varName = ivar_getName(var[i]);
         // 2.将变量名称转换为字符串
         NSString *name = [NSString stringWithUTF8String:varName];
         // 3.输出
         NSLog(@"%@", name);
     }
```

### 3. 获取对象的私有属性

```
    objc_property_t *propertes = class_copyPropertyList([Person class], &couont);
    for (int i = 0; i < couont; i++) {
        // 1.获取遍历到得属性名称
        const char * propertyName =  property_getName(propertes[i]);
        // 2.将属性名称转换为字符串
        NSString *name = [NSString stringWithUTF8String:propertyName];
        // 3.输出
         NSLog(@"%@", name);
    }

```

```
   	 // 将数据保存到本地
    Person *p = [[Person alloc] init];
    p.score = 99.8;
    p.className = @"xxxx";
    p.picUrls = @[@"123", @"456"];
    [NSKeyedArchiver archiveRootObject:p toFile:@"/Users/zhaoxiaohu/Desktop/person.data"];
    
    // 从本地读取数据
   Person *p =  [NSKeyedUnarchiver unarchiveObjectWithFile:@"/Users/zhaoxiaohu/Desktop/person.data"];
    NSLog(@"%@", p);

```

#### 在Persion.h中

```

@interface Person : NSObject<NSCoding>

@property (nonatomic, strong) NSArray *picUrls;
@property (nonatomic, copy) NSString *className;
@property (nonatomic, assign) float score;

@property (nonatomic, strong) NSNumber *number;

- (void)demo;
@end

```

#### 在Persion.m中

```
#import "Person.h"
#import <objc/runtime.h>

@implementation Person
{
    int _age;
    double _height;
    NSString *_name;
}

- (void)test
{
    NSLog(@"%s", __func__);
}

- (void)demo
{
    NSLog(@"%s", __func__);

}

/*
- (void)encodeWithCoder:(NSCoder *)encoder
{
    [encoder encodeObject:self.picUrls forKey:@"picUrls"];
    [encoder encodeObject:@(self.score) forKey:@"score"];
    [encoder encodeObject:self.className forKey:@"className"];
}

- (id)initWithCoder:(NSCoder *)decoder
{
    if (self = [super init]) {
        self.picUrls = [decoder decodeObjectForKey:@"picUrls"];
        self.score = [[decoder decodeObjectForKey:@"score"] doubleValue];
        self.className = [decoder decodeObjectForKey:@"className"];
    }
    return self;
}
 */

- (void)encodeWithCoder:(NSCoder *)encoder
{
    unsigned int count = 0;
    // 1.取出所有的属性
    objc_property_t *propertes = class_copyPropertyList([self class], &count);
    // 2.遍历所有的属性
    for (int i = 0; i < count; i++) {
        // 获取当前遍历到的属性名称
       const char *propertyName = property_getName(propertes[i]);
        NSString *name = [NSString stringWithUTF8String:propertyName];
        // 利用KVC取出对应属性的值
        id value = [self valueForKey:name];
        // 归档到文件中
        [encoder encodeObject:value forKey:name];
    }
}

- (id)initWithCoder:(NSCoder *)decoder
{
    if (self = [super init]) {
        
        unsigned int count = 0;
        // 1.取出所有的属性
        objc_property_t *propertes = class_copyPropertyList([self class], &count);
        // 2.遍历所有的属性
        for (int i = 0; i < count; i++) {
            // 获取当前遍历到的属性名称
            const char *propertyName = property_getName(propertes[i]);
            NSString *name = [NSString stringWithUTF8String:propertyName];
            // 解归档当前遍历到得属性的值
            id value = [decoder decodeObjectForKey:name];
//            self.className = [decoder decodeObjectForKey:@"className"];
            // 利用KVC给属性设值
            [self setValue:value forKey:name];
        }
    }
    return self;
}



```

#### 实例代码下载地址:
[https://github.com/Paulpang/runtime](https://github.com/Paulpang/runtime)

 
 
 
 



