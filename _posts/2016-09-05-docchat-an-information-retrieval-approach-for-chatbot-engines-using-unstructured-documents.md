---
published: true
title: DocChat - An Information Retrieval Approach for Chatbot Engines Using Unstructured Documents
layout: post
---

[PDF](http://aclweb.org/anthology/P16-1049)


## Abstract

Most current chatbot engines are designed to reply to user utterances based on existing utterance-response (or Q-R)1 pairs. In this paper, we present DocChat, **a novel information retrieval approach for chatbot engines that can leverage unstructured documents, instead of Q-R pairs, to respond to utterances. A learning to rank model with features designed at different levels of granularity is proposed to measure the relevance between utterances and responses directly**. We evaluate our proposed approach in both English and Chinese: (i) For English, we evaluate DocChat on WikiQA and QASent, two answer sentence selection tasks, and compare it with state-of-the-art methods. Reasonable improvements and good adaptability are observed. (ii) For Chinese, we compare DocChat with XiaoIce2, a famous chitchat engine in China, and side-by-side evaluation shows that DocChat is a perfect complement for chatbot engines using Q-R pairs as main source of responses.

Three steps:

* **Response Retrieval**, which retrieves response candidates _C_ from _D_ based on _Q_

$$
C = Retrieve(Q, D)
$$

* **Response Ranking**, which ranks all response candidates in C and selects the most possible response candidate as $$\widehat{S}$$

$$
\widehat{S} = argmaxRank_{S \epsilon C} (S, Q)
$$

* **Response Triggering**, which decides whether it is confident enough to response Q using $$\widehat{S}$$

$$
I = Trigger( \widehat{S}, Q)
$$

## Notes

模型

* 整体框架与传统QA系统有一些变化，传统模型先进行问题分类，再检索，再进行实体识别给出答案；本文是先检索选候选，再排序选Top1，再通过分类器判断是否返回结果。
* 检索模块没有什么新东西，从上产品线的角度看来，`Elastic Search`或许是一个好的选择。
* 排序模型深刻反映了一个有搜索背景的团队能力。排序模型用的是普通`regression`模型，但`feature engineering`非常全面，包括`Paraphrase`、`Topic model`、`Deep learning`等。其中`Deep learning`也是用来抽`feature`，不过不是传统`RNN dual encoder`，而是`CNN dual encoder`。
* 分类模型对三个识别（问题好不好，答案好不好，问题答案匹配的好不好）分别进行的判断，应该是考虑到`Chatbot`本身需要的高精度特性。

数据

* 训练数据相对容易获取，百度知道或许是很好的训练预料


评价

* 评价方面，`WikiQA`场景用了已有的测试集，`Chatbot`场景并没有提出好的评价标准，还是一如既往的人工、人工再人工


结果

* 从论文上提供的实验结果上看来大概在70%左右，后续或许可以调整最后的分类模型来提高准确率，适当降低召回率，提高系统可用度。


总结

* 本文还是在用检索搜索的思路在解决`Chatbot`对话问题，优点在于可以消耗非结构化文档数据，并且相关技术都是已比较成熟；缺点在于整个模型只是在检索，没有对问题的理解，在实际产品中，无法解决用户基于`context`的多轮对话问题。