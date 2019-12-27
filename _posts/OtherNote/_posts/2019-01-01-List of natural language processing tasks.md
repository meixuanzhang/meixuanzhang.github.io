---
layout: post
title: List of natural language processing tasks
date:   2019-01-01
categories: 
---  


# Syntax(语法)  

**Grammar induction(语法归纳)**  

生成正式的语法规则(grammar)描述语言的句法(syntax)。句法是研究句子的个个组成部分和它们的排列顺序   

**Lemmatization(词形还原)**
The task of removing inflectional endings only and to return the base dictionary form of a word which is also known as a lemma.
Morphological segmentation
Separate words into individual morphemes and identify the class of the morphemes. The difficulty of this task depends greatly on the complexity of the morphology (i.e. the structure of words) of the language being considered. English has fairly simple morphology, especially inflectional morphology, and thus it is often possible to ignore this task entirely and simply model all possible forms of a word (e.g. "open, opens, opened, opening") as separate words. In languages such as Turkish or Meitei,[14] a highly agglutinated Indian language, however, such an approach is not possible, as each dictionary entry has thousands of possible word forms.

词形还原就是去掉单词的词缀，提取单词的主干部分，通常提取后的单词会是字典中的单词，不同于词干提取（stemming），提取后的单词不一定会出现在单词中。比如，单词“cars”词形还原后的单词为“car”，单词“ate”词形还原后的单词为“eat”。

**Part-of-speech tagging(词性标记)**  

别名POS-tagging, tagging  

给定一个句子，为每个单词确定词性（POS）。许多单词，尤其是普通单词，可以有多种词性。例如，“ book” 可以是名词("the book on the table") 或动词("to book a flight")； "set" 可以是名词，动词或形容词; "out" 至少有五个不同的词性；一些语言比其他语言具有更多的歧义。词形态( inflectional morphology)变化很少的语言，例如英语，尤其容易产生歧义。汉语之所以容易产生这种歧义，是因为它是一种声调语言。这种变化不容易通过正字法传达预期的意义。同一个字需要加上音才能辨别，单有字存在歧义(正字法，乃关于文字使用的规范性法则，是确定正规使用的、书写和语法符合相关规范的文字。)

Parsing
Determine the parse tree (grammatical analysis) of a given sentence. The grammar for natural languages is ambiguous and typical sentences have multiple possible analyses. Perhaps surprisingly, for a typical sentence, there may be thousands of potential parses (most of which will seem completely nonsensical to a human). There are two primary types of parsing, Dependency Parsing, and Constituency Parsing. Dependency Parsing focuses on the relationships between words in a sentence (marking things like Primary Objects and predicates), whereas Constituency Parsing focuses on building out the Parse Tree using a Probabilistic Context-Free Grammar (PCFG). See also: Stochastic grammar.
Sentence breaking (also known as sentence boundary disambiguation)
Given a chunk of text, find the sentence boundaries. Sentence boundaries are often marked by periods or other punctuation marks, but these same characters can serve other purposes (e.g. marking abbreviations).
Stemming
The process of reducing inflected (or sometimes derived) words to their root form. (e.g. "close" will be the root for "closed", "closing", "close", "closer" etc.).
Word segmentation
Separate a chunk of continuous text into separate words. For a language like English, this is fairly trivial, since words are usually separated by spaces. However, some written languages like Chinese, Japanese and Thai do not mark word boundaries in such a fashion, and in those languages text segmentation is a significant task requiring knowledge of the vocabulary and morphology of words in the language. Sometimes this process is also used in cases like Bag of Words (BOW) creation in data mining.
Terminology extraction
The goal of terminology extraction is to automatically extract relevant terms from a given corpus.

# Semantics
Lexical semantics
What is the computational meaning of individual words in context?
Distributional semantics
How can we learn semantic representations from data?
Machine translation
Automatically translate text from one human language to another. This is one of the most difficult problems, and is a member of a class of problems colloquially termed "AI-complete", i.e. requiring all of the different types of knowledge that humans possess (grammar, semantics, facts about the real world, etc.) to solve properly.
Named entity recognition (NER)
Given a stream of text, determine which items in the text map to proper names, such as people or places, and what the type of each such name is (e.g. person, location, organization). Although capitalization can aid in recognizing named entities in languages such as English, this information cannot aid in determining the type of named entity, and in any case, is often inaccurate or insufficient. For example, the first letter of a sentence is also capitalized, and named entities often span several words, only some of which are capitalized. Furthermore, many other languages in non-Western scripts (e.g. Chinese or Arabic) do not have any capitalization at all, and even languages with capitalization may not consistently use it to distinguish names. For example, German capitalizes all nouns, regardless of whether they are names, and French and Spanish do not capitalize names that serve as adjectives.
Natural language generation
Convert information from computer databases or semantic intents into readable human language.
Natural language understanding
Convert chunks of text into more formal representations such as first-order logic structures that are easier for computer programs to manipulate. Natural language understanding involves the identification of the intended semantic from the multiple possible semantics which can be derived from a natural language expression which usually takes the form of organized notations of natural language concepts. Introduction and creation of language metamodel and ontology are efficient however empirical solutions. An explicit formalization of natural language semantics without confusions with implicit assumptions such as closed-world assumption (CWA) vs. open-world assumption, or subjective Yes/No vs. objective True/False is expected for the construction of a basis of semantics formalization.[15]
Optical character recognition (OCR)
Given an image representing printed text, determine the corresponding text.
Question answering
Given a human-language question, determine its answer. Typical questions have a specific right answer (such as "What is the capital of Canada?"), but sometimes open-ended questions are also considered (such as "What is the meaning of life?"). Recent works have looked at even more complex questions.[16]
Recognizing Textual entailment
Given two text fragments, determine if one being true entails the other, entails the other's negation, or allows the other to be either true or false.[17]
Relationship extraction
Given a chunk of text, identify the relationships among named entities (e.g. who is married to whom).
Sentiment analysis (see also multimodal sentiment analysis)
Extract subjective information usually from a set of documents, often using online reviews to determine "polarity" about specific objects. It is especially useful for identifying trends of public opinion in social media, for marketing.
Topic segmentation and recognition
Given a chunk of text, separate it into segments each of which is devoted to a topic, and identify the topic of the segment.
Word sense disambiguation
Many words have more than one meaning; we have to select the meaning which makes the most sense in context. For this problem, we are typically given a list of words and associated word senses, e.g. from a dictionary or an online resource such as WordNet.
# Discourse
Automatic summarization
Produce a readable summary of a chunk of text. Often used to provide summaries of the text of a known type, such as research papers, articles in the financial section of a newspaper.
Coreference resolution
Given a sentence or larger chunk of text, determine which words ("mentions") refer to the same objects ("entities"). Anaphora resolution is a specific example of this task, and is specifically concerned with matching up pronouns with the nouns or names to which they refer. The more general task of coreference resolution also includes identifying so-called "bridging relationships" involving referring expressions. For example, in a sentence such as "He entered John's house through the front door", "the front door" is a referring expression and the bridging relationship to be identified is the fact that the door being referred to is the front door of John's house (rather than of some other structure that might also be referred to).
Discourse analysis
This rubric includes several related tasks. One task is identifying the discourse structure of a connected text, i.e. the nature of the discourse relationships between sentences (e.g. elaboration, explanation, contrast). Another possible task is recognizing and classifying the speech acts in a chunk of text (e.g. yes-no question, content question, statement, assertion, etc.).
# Speech
Speech recognition
Given a sound clip of a person or people speaking, determine the textual representation of the speech. This is the opposite of text to speech and is one of the extremely difficult problems colloquially termed "AI-complete" (see above). In natural speech there are hardly any pauses between successive words, and thus speech segmentation is a necessary subtask of speech recognition (see below). In most spoken languages, the sounds representing successive letters blend into each other in a process termed coarticulation, so the conversion of the analog signal to discrete characters can be a very difficult process. Also, given that words in the same language are spoken by people with different accents, the speech recognition software must be able to recognize the wide variety of input as being identical to each other in terms of its textual equivalent.
Speech segmentation
Given a sound clip of a person or people speaking, separate it into words. A subtask of speech recognition and typically grouped with it.
Text-to-speech
Given a text, transform those units and produce a spoken representation. Text-to-speech can be used to aid the visually impaired.[18]
Dialogue
The first published work by an artificial intelligence was published in 2018, 1 the Road, marketed as a novel, contains sixty million words.


![_config.yml]({{ site.baseurl }}/images/Java program/image59.jpg)   
