---
layout: post
title: Java程序设计基础-笔记PART4
date:   2019-01-04
categories: 编程语言
---

# 第四章

## 接口  

+ 接口中可以规定方法的原型：方法名、参数列表以及返回类型，但不能规定方法主体  
+ 也可以包含**基本数据类型的数据成员，但它们都默认为static和final**  


**接口的作用**   
+ 继承多个设计
+ 建立类和类之间的“协议” (将类根据其实现的功能分组用接口代表，而不必顾虑它所在的类继承层次，这样可以最大限制地利用动态绑定，隐藏实现细节) 
 
![_config.yml]({{ site.baseurl }}/images/Java program/image184.jpg)    
![_config.yml]({{ site.baseurl }}/images/Java program/image185.jpg)    
![_config.yml]({{ site.baseurl }}/images/Java program/image186.jpg)    
![_config.yml]({{ site.baseurl }}/images/Java program/image187.jpg)    
![_config.yml]({{ site.baseurl }}/images/Java program/image188.jpg)    
![_config.yml]({{ site.baseurl }}/images/Java program/image189.jpg)    
![_config.yml]({{ site.baseurl }}/images/Java program/image190.jpg)  

**实现多个接口**    
![_config.yml]({{ site.baseurl }}/images/Java program/image191.jpg)    

![_config.yml]({{ site.baseurl }}/images/Java program/image192.jpg)    
![_config.yml]({{ site.baseurl }}/images/Java program/image193.jpg)    
![_config.yml]({{ site.baseurl }}/images/Java program/image194.jpg)   


**接口扩展**
 
![_config.yml]({{ site.baseurl }}/images/Java program/image195.jpg)    
![_config.yml]({{ site.baseurl }}/images/Java program/image196.jpg)    
![_config.yml]({{ site.baseurl }}/images/Java program/image197.jpg)    
![_config.yml]({{ site.baseurl }}/images/Java program/image198.jpg)    
 

 
## 类型转换(引用)   

![_config.yml]({{ site.baseurl }}/images/Java program/image199.jpg)    
![_config.yml]({{ site.baseurl }}/images/Java program/image200.jpg)   
![_config.yml]({{ site.baseurl }}/images/Java program/image201.jpg)   
![_config.yml]({{ site.baseurl }}/images/Java program/image202.jpg)   
![_config.yml]({{ site.baseurl }}/images/Java program/image203.jpg)   
![_config.yml]({{ site.baseurl }}/images/Java program/image204.jpg)   

## 方法的查找(强制转换后查找问题)   

+ 实例方法的查找
+ 类方法的查找 


![_config.yml]({{ site.baseurl }}/images/Java program/image205.jpg)   
![_config.yml]({{ site.baseurl }}/images/Java program/image206.jpg)   


## 多态的概念  

![_config.yml]({{ site.baseurl }}/images/Java program/image207.jpg)    

**多态的目的**  
+ 使代码变得简单且容易理解；
+ 使程序具有很好的可扩展性

![_config.yml]({{ site.baseurl }}/images/Java program/image208.jpg)   
![_config.yml]({{ site.baseurl }}/images/Java program/image209.jpg) 


## 多态的应用

**动态绑定**  
  
![_config.yml]({{ site.baseurl }}/images/Java program/image210.jpg)   
![_config.yml]({{ site.baseurl }}/images/Java program/image211.jpg)   
![_config.yml]({{ site.baseurl }}/images/Java program/image212.jpg)   
![_config.yml]({{ site.baseurl }}/images/Java program/image213.jpg)   

**二次分发**

![_config.yml]({{ site.baseurl }}/images/Java program/image214.jpg)   
![_config.yml]({{ site.baseurl }}/images/Java program/image215.jpg)   
![_config.yml]({{ site.baseurl }}/images/Java program/image216.jpg)   
![_config.yml]({{ site.baseurl }}/images/Java program/image217.jpg)   
![_config.yml]({{ site.baseurl }}/images/Java program/image218.jpg)   


## 构造方法与多态性   

![_config.yml]({{ site.baseurl }}/images/Java program/image219.jpg)   
![_config.yml]({{ site.baseurl }}/images/Java program/image220.jpg)   
![_config.yml]({{ site.baseurl }}/images/Java program/image221.jpg)   
![_config.yml]({{ site.baseurl }}/images/Java program/image222.jpg)  
![_config.yml]({{ site.baseurl }}/images/Java program/image223.jpg)  
![_config.yml]({{ site.baseurl }}/images/Java program/image224.jpg)  
![_config.yml]({{ site.baseurl }}/images/Java program/image225.jpg)  
![_config.yml]({{ site.baseurl }}/images/Java program/image226.jpg)  
![_config.yml]({{ site.baseurl }}/images/Java program/image227.jpg)  
![_config.yml]({{ site.baseurl }}/images/Java program/image228.jpg)  

## 总结
接口数据成员默认是static和final
接口一定是public
接口内方法一定是public abstract   
父类构造器默认为super(),调用父类构造函数不代表创建了父类，this对象本身，super父类    
涉及继承，最好不要在构造方法中调用函数

[java 类中各部分的执行顺序](https://blog.csdn.net/u011877584/article/details/82145301)


