---
layout: post
title: Java程序设计基础-笔记PART3
date:   2019-01-03
categories: 编程语言
---

# 第三章

## 类继承的概念和语法    

+ 根据已有类来定义新类，新类拥有已有类的所有功能    
+ java只支持类的单继承，每个子类只能有一个直接超类   
+ 超类是所有子类的公共属性及方法的集合,子类则是超类的特殊化  
+ 继承机制可以提高程序的抽象程度,提高代码的可重用性


**超类和子类**  
+ 子类对象与超类对象存在“是一个...”（或“是一种...”)的关系  

**子类对象**  
+ 从外部来看，它应该包括：与超类相同的接口，可以具有更多的方法和数据成员  
+ 其包含着超类的所有变量和方法  


![_config.yml]({{ site.baseurl }}/images/Java program/image137.jpg)   
![_config.yml]({{ site.baseurl }}/images/Java program/image138.jpg)   
![_config.yml]({{ site.baseurl }}/images/Java program/image139.jpg)   
![_config.yml]({{ site.baseurl }}/images/Java program/image140.jpg)   
![_config.yml]({{ site.baseurl }}/images/Java program/image141.jpg)     

## 隐藏与覆盖  

隐藏，超类和子类变量名相同，但类型不同(非覆盖)

**当子类执行继承自超类的操作时，处理的是继承自超类的变量，而当子类执行它自己声明的方法时，所操作的是它自己声明的变量**  

![_config.yml]({{ site.baseurl }}/images/Java program/image142.jpg)   
![_config.yml]({{ site.baseurl }}/images/Java program/image143.jpg)   
![_config.yml]({{ site.baseurl }}/images/Java program/image144.jpg)   

覆盖：  

![_config.yml]({{ site.baseurl }}/images/Java program/image145.jpg)    
![_config.yml]({{ site.baseurl }}/images/Java program/image146.jpg)   
![_config.yml]({{ site.baseurl }}/images/Java program/image147.jpg) 

## Object类  

+ 所有类的直接类或间接超类，处在类层次最高点   
+ 包含了所有java类的公共属性  

![_config.yml]({{ site.baseurl }}/images/Java program/image148.jpg)   
![_config.yml]({{ site.baseurl }}/images/Java program/image161.jpg)  
![_config.yml]({{ site.baseurl }}/images/Java program/image149.jpg)   
![_config.yml]({{ site.baseurl }}/images/Java program/image150.jpg)   
![_config.yml]({{ site.baseurl }}/images/Java program/image151.jpg)   
![_config.yml]({{ site.baseurl }}/images/Java program/image152.jpg)   
![_config.yml]({{ site.baseurl }}/images/Java program/image153.jpg)   
![_config.yml]({{ site.baseurl }}/images/Java program/image154.jpg)   
![_config.yml]({{ site.baseurl }}/images/Java program/image155.jpg)   
![_config.yml]({{ site.baseurl }}/images/Java program/image156.jpg)  
![_config.yml]({{ site.baseurl }}/images/Java program/image157.jpg)  
![_config.yml]({{ site.baseurl }}/images/Java program/image158.jpg)  
![_config.yml]({{ site.baseurl }}/images/Java program/image159.jpg)   
![_config.yml]({{ site.baseurl }}/images/Java program/image160.jpg)   


## 终结类与终结方法   

  
![_config.yml]({{ site.baseurl }}/images/Java program/image162.jpg)   
![_config.yml]({{ site.baseurl }}/images/Java program/image163.jpg)   
![_config.yml]({{ site.baseurl }}/images/Java program/image164.jpg)   


## 抽象类   
  
![_config.yml]({{ site.baseurl }}/images/Java program/image165.jpg)   
![_config.yml]({{ site.baseurl }}/images/Java program/image166.jpg)   
![_config.yml]({{ site.baseurl }}/images/Java program/image167.jpg)   
![_config.yml]({{ site.baseurl }}/images/Java program/image168.jpg)   
![_config.yml]({{ site.baseurl }}/images/Java program/image169.jpg)   
![_config.yml]({{ site.baseurl }}/images/Java program/image170.jpg) 

## 泛型  

![_config.yml]({{ site.baseurl }}/images/Java program/image177.jpg)    
![_config.yml]({{ site.baseurl }}/images/Java program/image178.jpg)    
![_config.yml]({{ site.baseurl }}/images/Java program/image179.jpg)  
![_config.yml]({{ site.baseurl }}/images/Java program/image180.jpg)    
![_config.yml]({{ site.baseurl }}/images/Java program/image181.jpg)    
![_config.yml]({{ site.baseurl }}/images/Java program/image182.jpg)  
![_config.yml]({{ site.baseurl }}/images/Java program/image183.jpg)    
 

## 类的组合  

![_config.yml]({{ site.baseurl }}/images/Java program/image171.jpg)    
![_config.yml]({{ site.baseurl }}/images/Java program/image172.jpg)    
![_config.yml]({{ site.baseurl }}/images/Java program/image173.jpg)    
![_config.yml]({{ site.baseurl }}/images/Java program/image174.jpg)    
![_config.yml]({{ site.baseurl }}/images/Java program/image175.jpg)    
![_config.yml]({{ site.baseurl }}/images/Java program/image176.jpg)    


## 总结

重写、隐藏、覆盖、访问

隐藏指的是子类把父类的属性或者方法隐藏了，即将子类强制转换成父类后，调用的还是父类的属性和方法，而覆盖则指的是父类引用指向了子类对象，调用的时候会调用子类的具体方法。   
变量只能被隐藏(包括静态和非静态)，不能被覆盖
可以用子类的静态变量隐藏父类的静态变量，也可以用子类的非静态变量隐藏父类的静态变量，也可以用非最终变量(final)隐藏父类中的最终变量；
静态方法(static)只能被隐藏，不能被覆盖；
非静态方法可以被覆盖；
不能用子类的静态方法隐藏父类中的非静态方法(重写)，否则编译会报错；
不能用子类的非静态方法覆盖父类的静态方法(重写)，否则编译会报错；
不能重写父类中的最终方法(final)；
抽象方法必须在具体类中被覆盖；
父类内中的私有属性和方法，子类内是无法访问(super)到的，只是拥有   

子类重写父类的方法时候，不能抛出与父类方法不同的异常。意味着：如果父类的方法抛出了异常，子类重写该方法时没有抛出异常是合法的；但是如果父类中的方法没有抛出异常，而子类重写该方法时抛出了异常，那么就会编译错误；另外，如果子类在重写父类的方法的时候抛出的异常与父类方法中抛出的异常不一样，那么也是会编译错误的，如父类方法中抛出的是InterruptedException，而子类重写该方法时抛出的是Exception，那么也会编译错误。   

(抽象类和抽象方法)  
抽象类不能实例化  
抽象方法只有方法原型没有方法体  
泛型类(变量是泛型或方法返回是泛型)  
泛型方法(参数是泛型)   
泛型类与通配符    
构造函数只是初始化，不是实例化   
private 只能类内使用，实例对象都调用不了



