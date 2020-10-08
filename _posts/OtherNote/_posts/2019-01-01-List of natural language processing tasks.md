---
layout: post
title: List of natural language processing tasks
date:   2019-01-01
categories: NLP
---  

# Syntax(语法)  

**Grammar induction(语法归纳)**  

生成正式的语法规则(grammar)描述语言的句法(syntax)。句法是研究句子的个个组成部分和它们的排列顺序   

**Lemmatization(词形还原)**  

词形还原就是去掉单词的词缀，提取单词的主干部分，通常提取后的单词会是字典中的单词，不同于词干提取（stemming），词干提取后的单词不一定会出现在单词中。比如，单词“cars”词形还原后的单词为“car”，单词“ate”词形还原后的单词为“eat”。

**Morphological segmentation(语素切分)**  

将单词分成单独的词素(individual morphemes)，并识别词素的类别。英语的形态(morphology)非常简单，尤其是屈折形态(inflectional morphology)语言，因此通常可以完全忽略此任务，而可以将单词的所有可能形式（例如“ open，opens，opened，opening”）建模为单独的单词。在语言如土耳其或Meitei，高度凝集的印度语言是不可能的，因为每个字典条目都有成千上万种可能的单词形式。    
语素，语言学术语，是指语言中最小的音义结合体。也就是说一个语言单位必须同时满足三个条件——“最小、有音、有义”才能被称作语素，尤其是“最小”和“有义”。   
(A morpheme is the smallest meaningful unit in a language. A morpheme is not identical to a word. The main difference between them is that a morpheme sometimes does not stand alone, but a word, by definition, always stands alone.)   

[英语中的词素](https://wenku.baidu.com/view/8cb7f95477a20029bd64783e0912a21614797fec.html) 

**Part-of-speech tagging(词性标记)**  

别名POS-tagging, tagging  

给定一个句子，为每个单词确定词性（POS）。许多单词，尤其是普通单词，可以有多种词性。例如，“ book” 可以是名词("the book on the table") 或动词("to book a flight")； "set" 可以是名词，动词或形容词; "out" 至少有五个不同的词性；一些语言比其他语言具有更多的歧义。词形态( inflectional morphology)变化很少的语言，例如英语，尤其容易产生歧义。汉语之所以容易产生这种歧义，是因为它是一种声调语言。这种变化不容易通过正字法传达预期的意义。同一个字需要加上音才能辨别，单有字存在歧义(正字法，乃关于文字使用的规范性法则，是确定正规使用的、书写和语法符合相关规范的文字。)

**Parsing(解析)**    

确定给定句子的语法分析树(parse tree)(语法分析)。该语法对自然语言是模糊(ambiguous)的和典型的句子有多种可能的分析。也许令人惊讶的是，对于一个典型的句子来说，可能有成千上万个潜在的语法分析（其中大多数对于人类来说似乎完全是毫无意义的）。解析有两种主要类型，即依存句法分析(Dependency Parsing)和成分句法分析(Constituency Parsing)。依存句法分析着重于句子中单词之间的关系（标记诸如主要对象和谓词之类的事物），而成分句法分析着重于使用概率上下文无关语法（Probabilistic Context-Free Grammar PCFG）来构建解析树(Parse Tree)。另请参阅：随机语法。

**Sentence breaking(断句)(also known as sentence boundary disambiguation)(又称句子边界消歧)**    

给定一段文本，找到句子边界。句子边界通常用句点或其他标点符号标记，但是这些相同的字符(characters)可以用于其他目的（例如标记缩写）。

**Stemming(词干提取)**   

将屈折的(inflected)(或有时派生的(derived)))单词还原为其词根形式的过程。(e.g. "close" will be the root for "closed", "closing", "close", "closer" etc.).    

**Word segmentation(分词)**   

把一段连续的文本分成几个词。对于像英语这样的语言来说，这是相当微不足道的，因为单词通常由空格隔开。然而，一些书面语言如汉语、日语和泰语并没有以这种方式标记单词边界，在这些语言中，文本分割是一项重要的任务，需要了解语言中单词的词汇和词形(morphology)。有时这个过程也用于数据挖掘中的单词袋（BOW）创建等情况。  

形态学(morphology)是词素的研究。语素被定义为“语言中最小的意思单位”。由于所有单词都具有含义，因此它们至少具有1个词素，但是一个单词可以具有多个词素。 例如，单词“ cat”只有一个词素，而单词“ cats”有2个词素，-s表示多个。

**Terminology extraction(术语抽取)**   

术语抽取的目的是从给定的语料库(corpus)中自动抽取相关术语。

# Semantics(语义学)   

**Lexical semantics(词汇语义学)**  

What is the computational meaning of individual words in context?


**Distributional semantics(分布语义学)**  

如何从数据中学习语义表示(semantic representations)？

**Machine translation(机器翻译)p**  

自动将文本从一种人类语言翻译成另一种人类语言。这是最困难的问题之一，并且通常属于“AI-complete” 这类问题之一，这需要人类拥有的所有不同类型的知识(语法，语义，关于现实世界的事实等)来解决。   

**Named entity recognition(命名实体识别) (NER)**    

给定一个文本流，确定文本中的哪些项映射到专有名称，例如人员或地点，以及每个此类名称的类型（例如人员、位置、组织）。尽管大写可以帮助识别英语等语言中的命名实体，但这些信息无法帮助确定命名实体的类型，而且在任何情况下，这些信息往往不准确或不充分。例如，句子的第一个字母也是大写的，命名实体通常跨越几个单词，只有一些单词是大写的。此外，非西方文字中的许多其他语言（如中文或阿拉伯语）根本没有大写，即使是有大写的语言也可能无法一致地使用它来区分名称。例如，德语将所有名词大写，而不管它们是否是名称，法语和西班牙语不将用作形容词的名称大写。    

**Natural language generation(自然语言生成)**  

将来自计算机数据库的信息或语义意图(semantic intents)转换为可读的人类语言   

**Natural language understanding(自然语言理解)**  

将文本块转换为更为形式化的表示形式，如更易于计算机程序操作的一阶逻辑结构。自然语言理解涉及到从多种可能的语义中识别出预期的语义，这些语义可以从自然语言表达式中派生出来，自然语言表达式通常采用自然语言概念的有组织符号的形式( the form of organized notations of natural language concepts)。 Introduction and creation of language metamodel and ontology are efficient however empirical solutions。自然语言语义的显式形式化不会与与隐含假设的混淆，如closed-world assumption（CWA）与open world assumption 或 subjective Yes/No vs. objective True/False是语义形式化基础的构建的基础

**Optical character recognition (光学字符识别)(OCR)** 

给定含有打印文本的图像，请确定相应的文本。

**Question answering(回答问题)**   

给定一个人类语言问题，确定其答案。典型的问题有特定的正确答案（例如“加拿大的首都是什么？”），但有时也会考虑开放性问题（例如“生活的意义是什么？”）。最近研究了甚至更复杂的问题。[16]

**Recognizing Textual entailment(识别文字蕴含RTE)**    

给定两个文本片段，一个文本的所描述内容能推论出另一个文本所描述的内容则表示蕴含返回True。如下列蕴含成立的例子:    

T: Parviz Davudi was representing Iran at a meeting of the Shanghai Co-operation Organisation (SCO), the fledgling association that binds Russia, China and four former Soviet republics of central Asia together to fight terrorism.
H: China is a member of SCO.

**Relationship extraction(关系提取)**

给定大量文本，请确定命名实体之间的关系 (e.g. who is married to whom).属于information extraction其中一个任务。  

**Sentiment analysis(情感分析) (see also multimodal sentiment analysis)**  

通常从一组文档中提取主观信息，通常使用在线评论来确定特定对象的“极性(polarity)”。它对于识别社交媒体中的舆论趋势和市场营销尤其有用。

**Topic segmentation and recognition(主题划分与识别)**   

给定一段文本，将其分成若干段，每一段都对应一个主题，确定每一段的主题。

**Word sense disambiguation(词义消歧)**   

许多单词具有不止一种含义 ; 我们必须选择在上下文中最有意义的含义。对于这个问题，通常会给我们一个单词列表和相关的词义，例如从词典或在线资源中

# Discourse(话语)   

**Automatic summarization(自动汇总)**  

产生一段可读的文本摘要。通常用于提供已知类型文本的摘要，例如研究论文，报纸财务版块中的文章。

**Coreference resolution(共指消解)p**       

给定一个句子或更大的文本块，确定哪些单词（“提及”）引用相同的对象（“实体”）。指代消解(Anaphora resolution)是这项任务的一个具体例子，它特别关注代词与它们所指的名词或名称的匹配。更一般的共指消解任务还包括识别所谓“桥接关系(bridging relationships)”其涉及引用表达式。例如，在“He entered John’s house through the front door”这样的句子中，“front door”是指代表达，要确定的桥接关系是指被指代的门是约翰家的前门（而不是其他可能被指代的结构）。    

**Discourse analysis(话语分析)**  

该主题包括几个相关任务。一项任务是识别关联文本的话语结构，即句子之间话语关系的性质（例如阐述，解释，对比）。另一个可能的任务是在一段文本中识别和分类文本块中的言语行为（如是非问题、内容问题、陈述、断言等）。

# Speech(语音)   

**Speech recognition(语音识别)**  

给定一个人讲话的声音片段，确定语音的文本表示形式。这是文本与语音的对立面，并且是通称为“AI-complete”（见上文）的极其困难的问题之一。在自然语音中，连续单词之间几乎没有任何停顿，因此语音分段是语音识别的必要子任务（请参见下文）。在大多数的语言，连续的字母在一个过程相互融合表示的声音称为协同发音，所以将模拟信号转换成离散字符可能是一个非常困难的过程。同样，假定具有不同口音的人说相同语言的单词，则语音识别软件必须能够从文本等价性的角度将各种各样的输入识别为彼此相同。  

**Speech segmentation(语音分割)**  

给定一个人讲话的声音片段，请将其分成单词。语音识别的子任务，通常与语音识别组合。

**Text-to-speech(文字转语音)**  

给定文本，将文本转换成声音表达。文字转语音可以帮助视障人士。

**Dialogue(对话)**  

The first published work by an artificial intelligence was published in 2018, 1 the Road, marketed as a novel, contains sixty million words.


-------------------------------------------------


