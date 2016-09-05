---
published: true
title: DocChat - An Information Retrieval Approach for Chatbot Engines Using Unstructured Documents
layout: post
---

[PDF](http://aclweb.org/anthology/P16-1049)

Most current chatbot engines are designed to reply to user utterances based on existing utterance-response (or Q-R)1 pairs. In this paper, we present DocChat, **a novel information retrieval approach for chatbot engines that can leverage unstructured documents, instead of Q-R pairs, to respond to utterances. A learning to rank model with features designed at different levels of granularity is proposed to measure the relevance between utterances and responses directly**. We evaluate our proposed approach in both English and Chinese: (i) For English, we evaluate DocChat on WikiQA and QASent, two answer sentence selection tasks, and compare it with state-of-the-art methods. Reasonable improvements and good adaptability are observed. (ii) For Chinese, we compare DocChat with XiaoIce2, a famous chitchat engine in China, and side-by-side evaluation shows that DocChat is a perfect complement for chatbot engines using Q-R pairs as main source of responses.


\begin{displaymath}\phi(x,y)\end{displaymath}

$$
\begin{align*}
  & \phi(x,y) = \phi \left(\sum_{i=1}^n x_ie_i, \sum_{j=1}^n y_je_j \right)
  = \sum_{i=1}^n \sum_{j=1}^n x_i y_j \phi(e_i, e_j) = \\
  & (x_1, \ldots, x_n) \left( \begin{array}{ccc}
      \phi(e_1, e_1) & \cdots & \phi(e_1, e_n) \\
      \vdots & \ddots & \vdots \\
      \phi(e_n, e_1) & \cdots & \phi(e_n, e_n)
    \end{array} \right)
  \left( \begin{array}{c}
      y_1 \\
      \vdots \\
      y_n
    \end{array} \right)
\end{align*}
$$

Three steps:

* response retrieval, which retrieves response candidates C from D based on Q
* response ranking, which ranks all response candidates in C and selects the most possible response candidate as Sˆ
* response triggering, which decides whether it is confident enough to response Q using Sˆ