---
layout: post
title: Java程序设计基础-笔记PART1
date:   2019-01-01
categories: 编程语言
---

# 第一章  
**计算机程序设计**    
+ 对问题进行抽象
+ 用计算机语言表述，利用机器求解  

**程序设计语言发展的历程**  
+ 机器语言
+ 汇编语言
+ 高级语言
+ 面向对象语言  

**面向对象的思想**  
+ 将客观事物看做具有状态和行为的对象，通过抽象找出同类对象的共同状态和行为，构成类

**面向对象技术给软件发展带来的意处**  
+ 可重用性
+ 可靠性

**面向对象语言的基本特征**  
+ 抽象和封装
+ 继承
+ 多态

**Java发展历程**  
![_config.yml]({{ site.baseurl }}/images/Java program/image1.jpg)  
![_config.yml]({{ site.baseurl }}/images/Java program/image2.jpg)  

**Java程序编译执行的过程**  
![_config.yml]({{ site.baseurl }}/images/Java program/image3.jpg)  

**一次编写，各处运行**  
![_config.yml]({{ site.baseurl }}/images/Java program/image4.jpg)  

## 基本数据类型和表达式

**文字量**  
+ 文字量直接出现在程序中并被编译器直接使用，比如30、2.141592654.文字量也称为文字常量，所谓常量，就是在其生存期内值不可改变的量   

**标识符**
+ 标识符是一个名词，与内存中的某个位置（地址）相对应
+ 标识符的第一个字符必须是下来字符之一： 
   + 大写字母（A-Z）
   + 小写字母（a-z）
   + 下划线（_）
   + 美元符号（$） 
+ 标识符的第二个字符以及后继字符必须是：上述列表中任意字符，数字字符（0-9）

**变量**
+ 一个由标识符命名的项
+ 每个变量都有类型；
+ 变量的值可以改变

**常量**  
+ 常量一旦被初始化以后就不可改变

**数值型**  
![_config.yml]({{ site.baseurl }}/images/Java program/image5.jpg)  

**数值型文字量**   
![_config.yml]({{ site.baseurl }}/images/Java program/image6.jpg)    

**字符类型的文字量**  
+ 字符类型的文字量是单引号括起来的字符或者转义序列，如‘Z’，‘k’,‘\t’。  
+ 用16位的Unicode字符作为编码方式，如下面代码所示：
   + char var_char = 'a'
   + char char_tab='\t'
+ 某些特殊的字符型常量需要使用转义的形式来表示**  

![_config.yml]({{ site.baseurl }}/images/Java program/image7.jpg)  

**布尔类型表示一个逻辑量，有两个取值true和false,例如：**  
+ boolean is_salaried;
+ boolean is_hourly;
+ is_salaried =true;
+ is_hourly = false;  

**String是一个类**  
+ String类JDK标准类结合中的一部分    
+ String animal="walrus";  

**字符串文字量**  
+ 由零个或多个字符组成，以双引号括起
+ 每个字符都可以用转义序列来表示
+ 例如：  
"" //空字符串
"\"" //只包含"的字符串
"This is a string" //只有16个字符的字符串
"This is a "+ "string"  //字符串常量表达式，由两个字符创常量组成


**算术运算符**  
+ 运算符++和--  例i++，--j;
+ 一元运算符+和-
+ 加法运算符+和-
+ 乘法运算符 *，/，和 %

**赋值运算符**  
+ 简单赋值运算符 =
+ 复合赋值运算符

![_config.yml]({{ site.baseurl }}/images/Java program/image8.jpg)   

**关系运算符**  
![_config.yml]({{ site.baseurl }}/images/Java program/image9.jpg)  

**逻辑运算符**  
![_config.yml]({{ site.baseurl }}/images/Java program/image10.jpg)  

**条件运算符(表达式1?表达式2:表达式3)**  
+ 首先计算表达式1
+ 如果表达式1的值为true，则选择表达式2的值
+ 如果表达式1的值为false，则选择表达式3的值

**类型转换**  
+ 每个表达式都有类型
+ 如果表达式的类型对于上下文不合适
   + 有时可能会导致编译错误
   + 有时语言会进行隐含类型转换
   
**扩展转换**  
![_config.yml]({{ site.baseurl }}/images/Java program/image11.jpg)   

**窄化转换**  
![_config.yml]({{ site.baseurl }}/images/Java program/image12.jpg)   

**隐含转换**
 + 赋值转换：将表达式类型转换为制定变量的类型
 + 方法调用转换：适用于方法和构造方法调用中的每一个参数
 + 字符串转换
    + 任何类型（包括null）都可以转换为字符串类型
    + 只当一个操作数是String 时适用于+运算符的操作数
    
**显示转换（强制转换）**
+ 将一个表达式转换为指定的类型 例如：(float)5.0

## 数组 

**数组的概念**   

注意：数组元素是同一类型

![_config.yml]({{ site.baseurl }}/images/Java program/image13.jpg) 

**数组是对象**  

动态初始化程序运行时才动态分配内存空间(数组先声明，再分配空间，没有赋值)，静态是程序编译时进行初始化(数组可以静态初始化)

![_config.yml]({{ site.baseurl }}/images/Java program/image14.jpg) 

**数组的元素** 

![_config.yml]({{ site.baseurl }}/images/Java program/image15.jpg) 

**数组的创建和使用**  

+ 数组的声明  
+ 数组的创建
+ 数组元素的初始化
+ 使用数组  

![_config.yml]({{ site.baseurl }}/images/Java program/image16.jpg)   
![_config.yml]({{ site.baseurl }}/images/Java program/image17.jpg)   
![_config.yml]({{ site.baseurl }}/images/Java program/image18.jpg)   
![_config.yml]({{ site.baseurl }}/images/Java program/image19.jpg)   
![_config.yml]({{ site.baseurl }}/images/Java program/image20.jpg)  
![_config.yml]({{ site.baseurl }}/images/Java program/image21.jpg)  

**数组名是一个引用**   

![_config.yml]({{ site.baseurl }}/images/Java program/image22.jpg)    
![_config.yml]({{ site.baseurl }}/images/Java program/image23.jpg) 

**数据复制**   

![_config.yml]({{ site.baseurl }}/images/Java program/image24.jpg)    
![_config.yml]({{ site.baseurl }}/images/Java program/image25.jpg)   

**多维数组**

![_config.yml]({{ site.baseurl }}/images/Java program/image26.jpg) 

![_config.yml]({{ site.baseurl }}/images/Java program/image27.jpg) 

![_config.yml]({{ site.baseurl }}/images/Java program/image28.jpg) 

## 算法流程控制

![_config.yml]({{ site.baseurl }}/images/Java program/image29.jpg)   
![_config.yml]({{ site.baseurl }}/images/Java program/image30.jpg)   
![_config.yml]({{ site.baseurl }}/images/Java program/image31.jpg)   
![_config.yml]({{ site.baseurl }}/images/Java program/image32.jpg)    
![_config.yml]({{ site.baseurl }}/images/Java program/image33.jpg)    
![_config.yml]({{ site.baseurl }}/images/Java program/image34.jpg)    
![_config.yml]({{ site.baseurl }}/images/Java program/image35.jpg)    
![_config.yml]({{ site.baseurl }}/images/Java program/image36.jpg)   

带标号和不带标号的continue   

![_config.yml]({{ site.baseurl }}/images/Java program/image37.jpg)  


# 第一章补充   

**Java数据类型** 

文字量整数默认为int,浮点数默认为double 

图中例子，byte类型变量不能取值128和-129，因为超出了byte的取值范围，long类型例子，int不能取2147483648，因为超出范围，当将2147483648赋值给long类型时需要在末尾标注2147483648L

![_config.yml]({{ site.baseurl }}/images/Java program/image38.jpg)  

如果使用八进制表示整数时需要以0开头，数码取值为0～7。如果以十六进制表示整数时需要以0x开头，其数码取值为0~9，A~F或a~f。   

最后一行代码“-”只是为了方便阅读，没有实际意义

![_config.yml]({{ site.baseurl }}/images/Java program/image39.jpg)

图中展示科学计数表示方式：1.36E+5f=1.36*10^5f ,末尾f是代表float
注意浮点数十六进制写法

![_config.yml]({{ site.baseurl }}/images/Java program/image40.jpg)  

转义符：  

![_config.yml]({{ site.baseurl }}/images/Java program/image41.jpg)  
 
布尔型(默认值是false)：  
 
![_config.yml]({{ site.baseurl }}/images/Java program/image42.jpg)  

如果数值超出了数据类型的取值范围，计算结果将发生错误   

图中展示值超出int范围的结果，以及修改为long后结果

![_config.yml]({{ site.baseurl }}/images/Java program/image43.jpg)  
![_config.yml]({{ site.baseurl }}/images/Java program/image44.jpg)  
![_config.yml]({{ site.baseurl }}/images/Java program/image45.jpg) 

**基础数据类型的转换**  

![_config.yml]({{ site.baseurl }}/images/Java program/image46.jpg)  

自动转换：  

![_config.yml]({{ site.baseurl }}/images/Java program/image47.jpg)  

强制转换：  

如果值超出转换后数据类型取值范围，将取其对界限值的余数    

![_config.yml]({{ site.baseurl }}/images/Java program/image48.jpg)  
![_config.yml]({{ site.baseurl }}/images/Java program/image49.jpg)  
![_config.yml]({{ site.baseurl }}/images/Java program/image50.jpg) 

**数组**   

![_config.yml]({{ site.baseurl }}/images/Java program/image51.jpg)  
![_config.yml]({{ site.baseurl }}/images/Java program/image52.jpg)  
![_config.yml]({{ site.baseurl }}/images/Java program/image53.jpg)  

**基本数据类型变量**   

变量声明方式：  
![_config.yml]({{ site.baseurl }}/images/Java program/image54.jpg)     

变量存储方式：  

![_config.yml]({{ site.baseurl }}/images/Java program/image55.jpg)   

**局部变量使用前需要进行初始化**(即不能只声明，而不赋值或不使用new初始化)，变量作用域在代码块内，内层代码块可以访问外层的变量，但外层不能访问内层的变量(没有特殊声明下)

![_config.yml]({{ site.baseurl }}/images/Java program/image56.jpg)  

final修饰的变量初始化后不能再改变其值    

![_config.yml]({{ site.baseurl }}/images/Java program/image57.jpg)  

**命令行参数**  

main函数在运行没有写入参数时,args为:   

![_config.yml]({{ site.baseurl }}/images/Java program/image58.jpg)   

main函数在运行写入参数时,args为(在doc命令后输入参数或按eplipse方式输入):   

![_config.yml]({{ site.baseurl }}/images/Java program/image59.jpg)   
