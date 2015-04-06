---
layout: post
title: "C++程序猿的iOS学习笔记1：objective-c语法"
description: ""
category: objective-c
tags: [objective-c]
---
{% include JB/setup %}

简单罗列下感觉不同的语法。

- 基础
    - #import
    包含文件
    - @autorelasepool
    自动释放池
    - @"HelloWorld"
    常量NSString对象
    - NSLog
    库函数

- 面向对象
    - [ClassOrInstance method]
    向对象发消息
    [receiver message]
    <pre>
    yourCar = [Car new];
    [yourCar prep]; // 实例方法
    </pre>

    - 类
    <pre>
    @interface NewClassName: ParentClassName
    propertyAndMethodDeclaration;
    @end
    </pre>

    <pre>
    -(void) print; // -实例方法，+类方法；void为无返回值
    -(int) currentAgs; // int为返回值，括号中
    -(void) setNumerator:(int) n; // 一个参数，类型在括号中
    </pre>

    <pre>
    @implementation Fraction
    {
        int numerator;  // 实例变量
        int denominator;
    }

    -(void) setNumerator:(int) n
    {
        numerator = n; // 实例方法
    }
    </pre>

    - 代码创建新实例并初始化
    <pre>
    Fraction * myFraction; // 声明
    myFraction = [Fraction alloc]; // 进入初始状态
    myFraction = [myFraction init]; // 初始化

    // or in one line

    Fraction * myFraction = [[Fraction alloc] init];
    </pre>

    - 调用
    <pre>
    [myFraction setNumerator: 1];
    </pre>

    - property
    属性前面不要以new,alloc,copy,init这些词开头
    <pre>
    // .h , after @interface
    @property int numerator,denominator;

    // .m , after @implementation
    @synthesize numerator,denominator;
    </pre>

    <pre>
    // 点运算符访问属性
    myFraction.numerator; // 而不是，[myFraction numerator]
    myFraction.numerator = 2; 
    </pre>

    - 多参数
    <pre>
    -(void) setTo:(int)n over:(int)d;
    [myFraction setTo:3 over:7]

    // 省略参数名
    -(int)set:(int)n:(int)d;
    [myFraction set:1:3]
    </pre>

    - self
    <pre>
    // 将消息发送到当前对象自己。
    [self reduce]
    </pre>

- 类型
    - id类型
    可存储任何类型的对象
    - BOOL
    <pre>
    BOOL isPrime;
    if(isPrime){
        //...
    }
    </pre>

    - 初始化
    <pre>
    - (id)init
    {
        self = [super init];

        if(self){
            // code
        }
        return self;
    }
    </pre>

    

- 头文件
    <pre>
    #import <Foundation/Foundation.h>
    #import <ctype.h> // islower isupper ...
    </pre>

- 继承
    - NSObject

    - @class 
    提前声明


- 异常
    <pre>
    @try{
        [f noSuchMethod];
    }
    @catch(NSException *exception){
        NSLog(@”Caught %@%@”,[exception name],[exception reason]);
    }
    NSLog(@”Execution continues!”);
    </pre>

    <pre>
    @throw myException;
    @throw;
    @finally
    </pre>
- 作用域
    <pre>
    @protected
    @private
    @public
    @package
    </pre>
    
- 编码规范
    <pre>
    实例变量以下划线“_”开头
    @synthesize window=_window;
    </pre>

- 分类
    <pre>
    #import “Fraction.h”
    @interface Fraction(MathOps)
        //...
    @end

    @implementation Fraction(MathOps)
        //...
    @end
    </pre>

    <pre>
    类的扩展:未命名分类
    @interface XXObject()
        // new member
    @end

    @implementation XXObject
        // new method
    @end

    </pre>

- 协议
    <pre>
    @protocol NSCopying
    - (id)copyWithZone : (NSZone * )zone;
    @end


    // 采用协议
    @interface AddressBook: NSObject <NSCopying>
    @end 

    // 采用多个协议
    @interface AddressBook: NSObject <NSCopying,NSCoding>
    @end
    </pre>


    <pre>
    //继承当前类的用户需要实现的方法和可选方法
    @protocol Drawing
    -(void) paint;
    @optional
    -(void) outline;
    </pre>

- 块(Blocks)
    <pre>
    ^(void){}

    void (^printMessage)(void)= {};
    printMessage();
    

    </pre>

- 复合字面量
- selector












