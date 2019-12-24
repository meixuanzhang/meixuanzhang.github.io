---
layout: post
title: week 1 
date:   2019-05-01
categories: From Languages to Information
---  

# Regular expressions(正则化)

$$\bullet$$ 如何对下面单词进行查找? 

woodchuck、woodchucks、Woodchuck、Woodchucks  

## Disjunctions(分离)


$$\bullet$$ 下列括号表示匹配，括号内字母或数字表示可以选择的匹配范围      

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image1.png)  

$$\bullet$$ 下列是匹配范围另一种表示  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image2.png) 

## Negation in Disjunctions  

$$\bullet$$ 下列表示匹配的否定，使用$$^$$符号  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image3.png) 


$$\bullet$$ Errors 

正则化两类错误：False positives: 匹配了不想匹配的，False negative： 没有匹配到想匹配的

通过以下两个方面减少错误率：  

提升accracy和precision(减少False positives)   
提升coverage和recall(减少False negative)    


# Sentence Segmentation  

$$"!,?"$$符号相对来说没有什么歧义

$$"."$$符号是有歧义的：它可以是句子的结束，可以是数字小数点如4.5 

需要建立模型(hand-writter rules,regular expressions,or machine-learning)进行区分如：  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image4.png) 

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image5.png) 


# Word Tokenization  

## Text Normalization   


$$\bullet$$ NL任务中需要对文本进行标准化：  
1、在运行文本中segmenting(分割）/tokenizing(标记)words   
2、标准化 words的格式  
3、在运行文本中分割句子     
 
## 下列句子有多少words?   
 
![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image6.png)  
 
"main-mainly"是片段(fragments) 
"uh"表示停顿，需要计算 
 
![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image7.png)  
 
将"San Francisco"作为一个words，则句子有14个words，将"San Francisco"作为两个words，则句子有15个words.   
Type 重复words算一个，如句子中"the"  


![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image8.png)   

N表示文本的单词数，V则是表示文本单词集合数(单词不重复计算) 


## Tokenization: language issues   

中文词之间是没有间隔的   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image9.png)  
![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image10.png)  
![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image11.png)   

# Word Normalization and Stemming  

根据不同需求对文本进行预处理  

## Normalization   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image12.png)   

## Case Folding(大小写转换)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image13.png)   

## Lemmatization(词形还原)  

找出词的原型 

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image14.png)   

## Morphology(词态学)

研究各种语句的变化规律，各种词型（例如：动词，名词等）和语干的规则变化与不规则变化,(如名词复数，动词过去式变化)   
![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image15.png)  

## Stemming(词干)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image16.png)  
![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image17.png)  

土耳其一个单词有很多的词干  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image18.png)  


----------------------------------------------------------------------------------------------------------------

# 2.1 Defining Minimum Edit Distance  

## 如何评价两个字符串(strings)相似？  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image19.png)  

两个字符串相似评价对机器翻译,信息提取,语言识别等非常有用  

## Edit Distance  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image20.png)  

将一个单词转换成另一个单词所需的操作数(insertion 插入，deletion 删除，substitution替换)

## Mininun Edit Distance  

为了对齐插入了星号

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image21.png)  

将I删除，N替换成E，T替换成X，插入C，N替换成U

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image22.png)  

## Other uses of Edit Distance in NLP  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image23.png)  

## 计算 Mininun Edit Distance  过程  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image24.png)  

## 数学符号表示Min Edit Distance   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image25.png) 

# 2.2 Computing Mininun Edit Distance   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image26.png) 

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image27.png) 

三条计算公式对应删除，插入，替换

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image28.png)  

Y轴表示待变换的单词，X轴表示目标单词   

图中"#"号表示位置0，根据算法初始化表格$$D(i,0)=i,D(0,j)=j$$，即表格两个轴填写的(1-9)   

如何计算剩下空格举例：  

Y轴"#"变换为X轴"#",相等没有操作填0  

Y轴"#I"变换为X轴"#E",有三条路径,即图中三个绿色圈：

上方路径：前面路径Y轴"#"等于X轴"#"(操作0),将"I"删除(操作1)，则此时Y轴"#I"变换成"#"，后面路径**插入**为"E"(操作1)，整个变换操作为2，即红色格子数=前方格子里数字+1   
中间路径：前面路径Y轴"#"等于X轴"#"(操作0),则此时Y轴"#"变换成"#"，后面路径将"I" **替换** 为"E"(操作2)，整个变换操作为2 ，即红色格子数=对角格子里数字+2   
下方路径：前面路径Y轴"#"等于X轴"#"(操作0),插入"E"(操作1)，则此时Y轴"#"变换成"#E"，后面路径将"I" **删除**(操作1)，整个变换操作为2 ， 即红色格子数=下方格子里数字+1

取最小值填入表中,每个空格都会有三条路径对应三个操作，但是值不一定相等  

最后绘制出整张图：  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image29.png)  

8就是将"INTENTION"变换为X轴"EXECUTION"所需最小操作数

# 2.3 Backtrace for Computiing Alignments计算路线  

通过Backtrace确定变换过程，从最右边顶点格子往前选择小于等于其的格子，最终路径有可能不止一条，图中黄色路径操作也是8，如何根据路径转换如图：  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image30.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image31.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image32.png)   

## Performance  

Time: O(nm) 计算表格   
Space: O(nm) 存储表格   
Backtrace： O(n+m)   

# 2.4 Weighted Minimum Edit Distance  

为什么需要添加权重？ 

拼写纠正(spell correction) 中一些字母输入错误可能性高于其他字母  
生物学中某些类型发生删除和插入的可能性高于其他类型  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image33.png)  

# 2.5  Minimum Edit Distance in Computation Biology  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image37.png)  

序列比对是一种排列DNA，RNA或蛋白质序列以识别可能是序列之间功能，结构或进化关系的结果的相似区域的方法。

## 为什么需要序列比对(sequence alignment)   

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image34.png)  

其可以找到区域在基因组位置？  
其可以发现基因的功能  
其可能会通过比较不同的物种来寻找进化的事物。   
这对于组装DNA测序片段也很重要，通过序列比对我们将尝试组装碎片，我们想寻找重叠的碎片。我们将讨论重叠的部分并找到它们之间的一些匹配；找到这两个部分匹配。   
通过比较个体(个体序列比对)并寻找突变，找到有相似和不同的地方


## NLP和Biology在alignment方面差异 

NLP使用distance描述 Edit Distance，希望减少distance和weights  
Biology使用similarity描述 Edit Distance，希望增大similarity和scores  

## 算法  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image35.png) 

d表示插入/删除操作成本(negative)，s是匹配的价值(positive)  

## 算法变种  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image38.png)  

匹配只惩罚重叠部分，不重叠部分不惩罚，所以下图初始化时删除惩罚是0,可以从任何点开始匹配

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image39.png) 

局部匹配问题：

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image40.png) 

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image41.png) 

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image42.png)  

X匹配Y:  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image43.png)  

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image44.png) 

![_config.yml]({{ site.baseurl }}/images/9From Languages to Information/image45.png) 