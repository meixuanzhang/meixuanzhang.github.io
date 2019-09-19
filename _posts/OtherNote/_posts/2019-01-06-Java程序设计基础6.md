---
layout: post
title: Java程序设计基础-笔记PART6
date:   2019-01-07
categories: 编程语言
---

# 第六章  

## java集合框架介绍    

![_config.yml]({{ site.baseurl }}/images/Java program/image317.jpg)   
![_config.yml]({{ site.baseurl }}/images/Java program/image318.jpg)   
![_config.yml]({{ site.baseurl }}/images/Java program/image319.jpg) 

## 主要接口及常用的实现类   

**Collection接口**  

+ 声明一组操作成批对象的抽象方法    
+ 实现它的类：AbstractCollection    

![_config.yml]({{ site.baseurl }}/images/Java program/image320.jpg)   


**Set接口**  

+ 对equals和hashCode操作有了更强的约定，如果两个set对象包含同样的元素，二者便是相等的   

![_config.yml]({{ site.baseurl }}/images/Java program/image321.jpg)   
 

**SortedSet接口**

+ 一种特殊的Set    
+ 其中的元素是升序排列的，还增加了与次序相关的操作     
+ 通常用于存放词汇表这样的内容    
+ 实现它的类：ConcurrentSkipListSet,TreeSet

**List接口**  

+ 可包含重复元素   
+ 元素是有顺序的，每个元素都有一个index值(从0开始)标明元素在列表中的位置  

![_config.yml]({{ site.baseurl }}/images/Java program/image322.jpg)   
 

**QueQue接口**  

+ 除了Collection的基本操作，队接口另外还有插入、移除和查看操作 
+ FIFO(先进先出，first in first out)    

![_config.yml]({{ site.baseurl }}/images/Java program/image323.jpg)   


**Map接口**  

+ 用于维护键/值对(key/value paris)  
+ 不能有重复的关键字，每个关键字最多能够映射到一个值    
+ 声明时可以带有两个参数，即Map<K,V>,K表示关键字的类型,V表示值的类型   

![_config.yml]({{ site.baseurl }}/images/Java program/image324.jpg)   
![_config.yml]({{ site.baseurl }}/images/Java program/image325.jpg) 

**SortedMap接口**   
+ Map 子接口
+ 一种特殊的Map,其中关键字是升序排列的
+ 通常用于词典和电话目录  
+ 在声明时可以带有两个类型参数，即SortedMap<K,V>,K表示关键字的类型,V表示值的类型  
+ 实现它的类：TreeMap，ConcurrentSkipListMap(支持并发)  




## 常用算法  

**对集合的运算**  

+ 大多数算法都是用于操作List对象  
+ 有两个(min和max)可用于任意集合对象

![_config.yml]({{ site.baseurl }}/images/Java program/image326.jpg)   
![_config.yml]({{ site.baseurl }}/images/Java program/image327.jpg)   
![_config.yml]({{ site.baseurl }}/images/Java program/image328.jpg)   
![_config.yml]({{ site.baseurl }}/images/Java program/image329.jpg)   
![_config.yml]({{ site.baseurl }}/images/Java program/image330.jpg) 



## 数组实用方法  

![_config.yml]({{ site.baseurl }}/images/Java program/image331.jpg)   
![_config.yml]({{ site.baseurl }}/images/Java program/image332.jpg)   
![_config.yml]({{ site.baseurl }}/images/Java program/image333.jpg)   

## 基于动态数组的类型(Vector,ArrayList)   

![_config.yml]({{ site.baseurl }}/images/Java program/image334.jpg)   
![_config.yml]({{ site.baseurl }}/images/Java program/image335.jpg)   
![_config.yml]({{ site.baseurl }}/images/Java program/image336.jpg)   
![_config.yml]({{ site.baseurl }}/images/Java program/image337.jpg) 

## 遍历Collection  

![_config.yml]({{ site.baseurl }}/images/Java program/image338.jpg)   
![_config.yml]({{ site.baseurl }}/images/Java program/image339.jpg)   
![_config.yml]({{ site.baseurl }}/images/Java program/image340.jpg)   
![_config.yml]({{ site.baseurl }}/images/Java program/image341.jpg)   
![_config.yml]({{ site.baseurl }}/images/Java program/image342.jpg)   
![_config.yml]({{ site.baseurl }}/images/Java program/image343.jpg)   
![_config.yml]({{ site.baseurl }}/images/Java program/image344.jpg)  

**通过聚类操作遍历**   

+ 聚类操作与lambda表达式一起使用

![_config.yml]({{ site.baseurl }}/images/Java program/image345.jpg)   


## Map接口及其实现  

![_config.yml]({{ site.baseurl }}/images/Java program/image346.jpg)  
![_config.yml]({{ site.baseurl }}/images/Java program/image347.jpg)   
![_config.yml]({{ site.baseurl }}/images/Java program/image348.jpg)   
![_config.yml]({{ site.baseurl }}/images/Java program/image349.jpg)  
+ 容量(capacity):哈希表的容量不是固定的，随对象的加入，其容量可以自动扩充。   
+ 关键字/键：每个存储的对象都需要一个关键字key,key可以是对象本身，也可以是对象的一部分(如对象的某一个属性)。  
+ 哈希码(hash code):要将对象存储到HashTable,就需要将其关键字key映射到一个整型数据，称为key的哈希码(hash code)。   
+ 哈希函数(hash function):返回对象的哈希码。    
+ 项(item):哈希表中的每一项都有两个域，关键字域key及值域value(即存储的对象)。key及value都可以是任意的Object类型的对象，但不能为空(null),HashTable中的所有关键字都是唯一的。    
+ 装填因子(load factor):(表中填入的项数)/(表的容量)   
 
![_config.yml]({{ site.baseurl }}/images/Java program/image350.jpg)   
![_config.yml]({{ site.baseurl }}/images/Java program/image351.jpg)  
![_config.yml]({{ site.baseurl }}/images/Java program/image352.jpg)  

  


## 总结






