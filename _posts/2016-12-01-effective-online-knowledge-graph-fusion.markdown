---
published: true
title: Effective Online Knowledge Graph Fusion
layout: post
---

[PDF](http://iswc2015.semanticweb.org/sites/iswc2015.semanticweb.org/files/93660257.pdf)



## Abstract

Recently, Web search engines have empowered their search with knowledge graphs to satisfy increasing demands of complex information needs about entities. Each engine offers an online knowledge graph service to display highly relevant information about the query entity in form of a structured summary called knowledge card. The cards from different engines might be complementary. Therefore, it is necessary to fuse knowledge cards from these engines to get a comprehensive view. Such a problem can be considered as a new branch of ontology alignment, which is actually an on-the-fly online data fusion based on the users’ needs. **In this paper, we present the first effort to work on knowledge cards fusion. We propose a novel probabilistic scoring algorithm for card disambiguation to select the most likely entity a card should refer to. We then design a learning-based method to align properties from cards representing the same entity. Finally, we perform value deduplication to group equivalent values of the aligned properties as value clusters.** The experimental results show that our approach outperforms the state of the art ontology alignment algorithms in terms of precision and recall.


## Notes

全文主要分三部分：

* 实体消歧，将卡片上的实体映射到Wikipedia上的实体。主要通过考虑`commonness` and `relatedness`等因素来判断是否进行融合。
* 属性名消歧，将同一属性的不同表达方式融合在一起。首先对属性名/属性值进行normalize（属性名转小写、属性值分隔符处理、属性值数字值单位不同），然后分别计算属性名相似度（Property Similarity）、属性值重合度（Value Over Ratio）、属性值匹配度（Value Match Ratio）。最后通过通过一些验证机制对非法属性进行过滤。
* 属性值消歧，将同一属性的不同属性值进行归一化处理。参考属性名的预处理过程。


本文整体上都是传统的消歧方法，但是偏实用，工程使用上应该会有不错的效果。