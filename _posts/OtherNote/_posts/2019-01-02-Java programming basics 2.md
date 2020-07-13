---
layout: post
title: Java程序设计基础-笔记PART2
date:   2019-01-02
categories: 编程语言
---

# 第二章

## 面向对象方法的特性 

**抽象**   

+ 忽略问题中与当前目标无关的方面   
+ 只关注与当前目标有关的方面  

例：钟表(各种类型的表)   

+ 数据(属性)  

int Hour;  int Minute; int Second;

+ 方法(行为)  
  
SetTmie();Show Time();

**封装**  

+ 封装是一种信息隐蔽技术  
+ 利用抽象数据类型将数据和基于数据的操作封装在一起；  
+ 用户只能看到对象的封装界面信息，对象的内部细节对用户是隐蔽的；  
+ 封装的目的在于将对象的使用者和设计者分开，使用者不必知道行为实现细节；  

**继承**  

+ 基于已有类产生新类的机制
+ 是指新的类可以获得已有类(称为超类、基类或父类)的属性和行为，称新类为已有类的子类(也称为派生类)；  
+ 在继承过程中子类继承了超类的特性，包括方法和实例变量；  
+ 有助于解决软件的可重用性问题，使程序结构清晰，降低编码和维护的工作量；

+ 单继承(一个子类只有单一的直接超类)，**java只支持单继承**    
+ 多继承(一个子类可以有一个以上的直接超类)  

**多态**  
+ 有继承情况下，超类和子类对象们都可以响应同名消息，但这些对象对同名消息响应具体方式可以不一样(子类覆盖从超类继承的方法)  


##  类声明与对象创建

**类与对象的关系**  
+ 类是对一类对象的描述；  
+ 对象是类具体实例。

![_config.yml]({{ site.baseurl }}/images/Java program/image60.jpg)    
![_config.yml]({{ site.baseurl }}/images/Java program/image62.jpg)    
![_config.yml]({{ site.baseurl }}/images/Java program/image63.jpg)    
![_config.yml]({{ site.baseurl }}/images/Java program/image64.jpg)    
  

##  数据成员   

+ 表示对象的状态  
+ 可以是任意的数据类型  
+ 类变量(静态变量，static修饰)，实例变量(没有static修饰)，类变量可以通过实例访问   

![_config.yml]({{ site.baseurl }}/images/Java program/image65.jpg)     
![_config.yml]({{ site.baseurl }}/images/Java program/image66.jpg)     
![_config.yml]({{ site.baseurl }}/images/Java program/image67.jpg)   
![_config.yml]({{ site.baseurl }}/images/Java program/image68.jpg)   
![_config.yml]({{ site.baseurl }}/images/Java program/image69.jpg)  
![_config.yml]({{ site.baseurl }}/images/Java program/image70.jpg)    
![_config.yml]({{ site.baseurl }}/images/Java program/image71.jpg)   
![_config.yml]({{ site.baseurl }}/images/Java program/image72.jpg)   
![_config.yml]({{ site.baseurl }}/images/Java program/image73.jpg)   
![_config.yml]({{ site.baseurl }}/images/Java program/image74.jpg)    

## 方法成员  


![_config.yml]({{ site.baseurl }}/images/Java program/image75.jpg)    

![_config.yml]({{ site.baseurl }}/images/Java program/image76.jpg)   

![_config.yml]({{ site.baseurl }}/images/Java program/image77.jpg) 

![_config.yml]({{ site.baseurl }}/images/Java program/image78.jpg)  

**实例方法**  
+ 表示特定对象的行为；
+ 声明时前面不加static修饰符； 

**实例方法调用**  
+ 给对象发消息，使用对象的某个行为/功能：调用对象的某个方法。   

  
  
![_config.yml]({{ site.baseurl }}/images/Java program/image79.jpg)  
![_config.yml]({{ site.baseurl }}/images/Java program/image80.jpg)  
![_config.yml]({{ site.baseurl }}/images/Java program/image81.jpg)  
![_config.yml]({{ site.baseurl }}/images/Java program/image82.jpg)  



**类方法**  
+ 也称为静态方法，声明时前面需加static修饰。
+ 不能被声明为抽象。
+ 可以类名直接调用，也可用类实例调用。

![_config.yml]({{ site.baseurl }}/images/Java program/image83.jpg)  
 
**可变长参数**  

![_config.yml]({{ site.baseurl }}/images/Java program/image84.jpg)  
![_config.yml]({{ site.baseurl }}/images/Java program/image85.jpg)  

## 包  

+ 包是一组类的集合   
+ 一个包可以包含若干个类文件，还可以包含若干个包  

![_config.yml]({{ site.baseurl }}/images/Java program/image86.jpg)   


**包的作用**  
+ 将相关的源代码文件组织在一起  
+ 类名的空间管理，利用包来划分名字空间可以避免类名冲突   
+ 提供包一级的封装及存取权限   

**编译单元**  
+ 一个java源代码文件称为一个编译单元，由三部分组成：  
所属包的声明(省略，则属于默认包);
Import（引入）包的声明，用于导入外部的类；  
类和接口的声明
+ 一个编译单元中只能有一个public类，该类名与文件名相同，编译单元中的其他类往往是public类的辅助类，经过编译，每个类都会产生一个class文件。  


**包的声明**  

![_config.yml]({{ site.baseurl }}/images/Java program/image87.jpg)    

**包与目录**  
包名就是文件夹名，即目录名；  
目录名不一定是包名；  

**引入包** 

![_config.yml]({{ site.baseurl }}/images/Java program/image88.jpg)   
![_config.yml]({{ site.baseurl }}/images/Java program/image89.jpg)   


## 类的访问权限控制   

![_config.yml]({{ site.baseurl }}/images/Java program/image90.jpg)    
![_config.yml]({{ site.baseurl }}/images/Java program/image91.jpg)    
![_config.yml]({{ site.baseurl }}/images/Java program/image92.jpg)    
![_config.yml]({{ site.baseurl }}/images/Java program/image93.jpg)    
![_config.yml]({{ site.baseurl }}/images/Java program/image94.jpg)    
![_config.yml]({{ site.baseurl }}/images/Java program/image95.jpg)    
![_config.yml]({{ site.baseurl }}/images/Java program/image96.jpg)    
![_config.yml]({{ site.baseurl }}/images/Java program/image97.jpg)   

**当形参与实参同名时，使用this指代实例对象**  

![_config.yml]({{ site.baseurl }}/images/Java program/image98.jpg)   


## 对象初始化与回收  

![_config.yml]({{ site.baseurl }}/images/Java program/image99.jpg)   

![_config.yml]({{ site.baseurl }}/images/Java program/image100.jpg)  

![_config.yml]({{ site.baseurl }}/images/Java program/image101.jpg)  

![_config.yml]({{ site.baseurl }}/images/Java program/image102.jpg)  

![_config.yml]({{ site.baseurl }}/images/Java program/image103.jpg)  

**显式声明构造方法，编译器不再生成默认的构造方法。**   

![_config.yml]({{ site.baseurl }}/images/Java program/image104.jpg)  

![_config.yml]({{ site.baseurl }}/images/Java program/image105.jpg)  

**使用this重载构造对象方法**  

![_config.yml]({{ site.baseurl }}/images/Java program/image106.jpg)  

![_config.yml]({{ site.baseurl }}/images/Java program/image107.jpg) 

**final变量初始化后不能再改变**  

![_config.yml]({{ site.baseurl }}/images/Java program/image108.jpg) 

## 内存回收   

![_config.yml]({{ site.baseurl }}/images/Java program/image109.jpg)  

![_config.yml]({{ site.baseurl }}/images/Java program/image110.jpg) 

![_config.yml]({{ site.baseurl }}/images/Java program/image111.jpg) 

## 枚举类

枚举类的对象的可取值是有一定范围的，所有可取值是可列出来的，枚举类的构造函数是private。

![_config.yml]({{ site.baseurl }}/images/Java program/image112.jpg)   
![_config.yml]({{ site.baseurl }}/images/Java program/image113.jpg)   
![_config.yml]({{ site.baseurl }}/images/Java program/image114.jpg)   
![_config.yml]({{ site.baseurl }}/images/Java program/image115.jpg)   
![_config.yml]({{ site.baseurl }}/images/Java program/image116.jpg)   
![_config.yml]({{ site.baseurl }}/images/Java program/image117.jpg)   
![_config.yml]({{ site.baseurl }}/images/Java program/image118.jpg)    
![_config.yml]({{ site.baseurl }}/images/Java program/image119.jpg)      

[JAVA：初始化及使用enum枚举类型](https://blog.csdn.net/qq_38333529/article/details/79795117)    

[深入分析Java中的枚举类](https://blog.csdn.net/abc123lzf/article/details/82084893)    

[Java 枚举类型使用，枚举集合介绍](https://baijiahao.baidu.com/s?id=1635855960809938591&wfr=spider&for=pc&isFailFlag=1)

## 应用   

![_config.yml]({{ site.baseurl }}/images/Java program/image120.jpg)   
![_config.yml]({{ site.baseurl }}/images/Java program/image121.jpg)   
![_config.yml]({{ site.baseurl }}/images/Java program/image122.jpg)   
![_config.yml]({{ site.baseurl }}/images/Java program/image123.jpg)   
![_config.yml]({{ site.baseurl }}/images/Java program/image124.jpg)   
![_config.yml]({{ site.baseurl }}/images/Java program/image125.jpg)   
![_config.yml]({{ site.baseurl }}/images/Java program/image126.jpg)   
![_config.yml]({{ site.baseurl }}/images/Java program/image127.jpg)   
![_config.yml]({{ site.baseurl }}/images/Java program/image128.jpg)    
![_config.yml]({{ site.baseurl }}/images/Java program/image129.jpg)   
![_config.yml]({{ site.baseurl }}/images/Java program/image130.jpg)   
![_config.yml]({{ site.baseurl }}/images/Java program/image131.jpg)   
![_config.yml]({{ site.baseurl }}/images/Java program/image132.jpg)   
![_config.yml]({{ site.baseurl }}/images/Java program/image133.jpg)   
![_config.yml]({{ site.baseurl }}/images/Java program/image134.jpg)   
![_config.yml]({{ site.baseurl }}/images/Java program/image135.jpg)   
![_config.yml]({{ site.baseurl }}/images/Java program/image136.jpg)   


## 总结  

方法外的变量是全局变量，方法内变量是局部变量，局部变量要先初始化在访问前   
static方法和全局变量是类方法和类变量  
final变量初始化后不能再改变，final修饰的方法不能被重写，final修饰的类不能被继承   
final变量初始化方式：在定义变量时直接赋值，声明变量后在构造方法中赋值，或构造代码块中赋值(构造代码块会在构造方法执行前执行)，如果是静态变量要么直接赋值，要么在静态代码块中赋值      
显式声明构造方法，编译器不再生成默认的构造方法    
枚举类构造函数是private    
  
所属权：static    
访问权:private (空修饰) protected public   
变化权:final   
继承：类，变量、方法   
