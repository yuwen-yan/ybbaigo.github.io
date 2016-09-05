---
published: true
title: DocChat - An Information Retrieval Approach for Chatbot Engines Using Unstructured Documents
layout: post
---

[PDF](http://aclweb.org/anthology/P16-1049)

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