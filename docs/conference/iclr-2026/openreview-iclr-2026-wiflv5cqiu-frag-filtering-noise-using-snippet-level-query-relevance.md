---
title: "FRAG: Filtering Noise Using Snippet-Level Query Relevance"
title_zh: FRAG：基于片段级查询相关性的噪声过滤
authors: "Yeming Jian, Yonggang Zhang, Shanzhi Gu, Long Lan, Tongliang Liu, Yiu-ming Cheung, Bo Han"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=wIflv5cQiU"
tags: ["query:ai-se"]
score: 4.0
evidence: 以片段级相关性过滤降低RAG噪声
tldr: 检索增强生成扩大检索窗口可提升效果，但会引入更多噪声干扰模型注意力并降低准确率。本文提出细粒度RAG方法FRAG，从查询中识别关键片段并依据片段级相关性过滤检索噪声。针对复杂查询中的隐式多跳逻辑关系，方法进一步保留推理所需知识。该工作为提升检索增强生成的鲁棒性提供了新思路。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 扩大检索窗口会引入更多噪声干扰注意力并降低准确率，复杂查询还需处理隐式多跳关系。
method: 提出细粒度RAG方法，从查询识别关键片段并依据片段级相关性过滤检索噪声。
result: 在过滤噪声的同时保留推理所需知识，缓解复杂查询下的性能下降。
conclusion: 该工作为提升检索增强生成的准确性与鲁棒性提供了新思路。
---

## Abstract
Retrieval-Augmented Generation (RAG) augments large language models (LLMs) with external retrievals. Typically, expanding the retrieval window can improve RAG performance by retrieving more relevant content. However, it risks increased noise, which distracts the model’s attention and degrades accuracy. To mitigate this, we propose Fine-Grained RAG (FRAG), which identifies key snippets from query and extracts relevant information while filtering noise from retrievals using snippet-level query relevance. Yet, a new challenge arises in addressing complex RAG queries, which require knowledge pieces with implicit multi-hop logical relationships. Failure to identify these relationships may lead to loss of inference-based knowledge during filtering, degrading performance. To address this, we propose Self-Recognition, which extracts inference-based knowledge by leveraging historically extracted knowledge as contextual references. While FRAG notably improves performance, it incurs high computational cost. To alleviate this, we present FRAG-ip, a fine-tuned framework which markedly accelerates FRAG by an order of magnitude. Extensive experiments show that FRAG significantly boosts RAG, yielding average accuracy gains of 4.94%/13.44% on simple/complex tasks.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
以片段级相关性过滤降低RAG噪声。

### 2. 核心内容
检索增强生成扩大检索窗口可提升效果，但会引入更多噪声干扰模型注意力并降低准确率。本文提出细粒度RAG方法FRAG，从查询中识别关键片段并依据片段级相关性过滤检索噪声。针对复杂查询中的隐式多跳逻辑关系，方法进一步保留推理所需知识。该工作为提升检索增强生成的鲁棒性提供了新思路。

### 3. 对应检索需求
recent advances in NLP。

### 4. 来源与原文
- Source：ICLR-2026-Rejected-Public
- OpenReview：[https://openreview.net/forum?id=wIflv5cQiU](https://openreview.net/forum?id=wIflv5cQiU)
