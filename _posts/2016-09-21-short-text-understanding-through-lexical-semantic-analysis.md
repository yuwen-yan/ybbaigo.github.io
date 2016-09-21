---
published: true
title: DocChat - An Information Retrieval Approach for Chatbot Engines Using Unstructured Documents
layout: post
---

[PDF](https://www.microsoft.com/en-us/research/publication/short-text-understanding-through-lexical-semantic-analysis/)



##Abstract

Understanding short texts is crucial to many applications, but challenges abound. First, short texts do not always observe the syntax of a written language. As a result, traditional natural language processing methods cannot be easily applied. Second, short texts usually do not contain sufficient statistical signals to support many state-of-the-art approaches for text processing such as topic modeling. Third, short texts are usually more ambiguous. We argue that knowledge is needed in order to better understand short texts. **In this work, we use lexicalsemantic knowledge provided by a well-known semantic network for short text understanding. Our knowledge-intensive approach disrupts traditional methods for tasks such as text segmentation, part-of-speech tagging, and concept labeling, in the sense that we focus on semantics in all these tasks**. We conduct a comprehensive performance evaluation on real-life data. The results show that knowledge is indispensable for short text understanding, and our knowledge-intensive approaches are effective in harvesting semantics of short texts.

Preliminary Concepts

* Definition 1 (vocabulary): A vocabulary is a collection ofwords and phrases (of a certain language).
* Definition 2 (term): A term t is an entry in the vocabulary.
* Definition 3 (segmentation): A segmentation p of a short text is a sequence of terms p = {t1, t2, ..., tn} such that: 1) terms cannot overlap with each other,  2) every non-stopword in the short text should be covered by a term.
* Definition 4 (type and typed-term): A term can be mapped to multiple types including verb, adjective, attribute, concept, and instance.
* Definition 5 (concept vector and concept cluster vector):During concept labeling, we map a typed-term to a concept vector, or map a typed-term to a concept cluster vector.

##Notes

整个系统依赖的数据信息主要分为：

* 词典（动词、形容词、属性、概念、实例）
* 每个实例都有哪些概念，比如*disneyland*既有可能是**theme park**也有可能**company**。
* 共现网络，用于说在某种*context*下面某一个实例最有可能所属的概念

整个系统处理流程主要分三部分

* 分词，基于图的思路。Affinity Model
* 实体类别识别，传统动态规划的思路，图的思路，还有*Pairwise Model*的思路
* 实体消歧处理，概念簇


整个系统强依赖于**Probase**或者类似的外部资源。不过全文给出了基于类似topic model的短文本理解整体解决方案。