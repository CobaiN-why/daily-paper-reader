---
title: "LLM-based Embeddings: Attention Values Encode Sentence Semantics Better Than Hidden States"
title_zh: 基于LLM的句向量：注意力值比隐藏状态更能编码句子语义
authors: "Yeqin Zhang, Yunfei Wang, Chen Jiaxuan, Ke Qin, Yizheng Zhao, Cam-Tu Nguyen"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf/ad8533a32926aa1e9ec4956507993a73d9de36a8.pdf"
tags: ["query:ai-se"]
score: 7.0
evidence: 面向自然语言处理应用的LLM句向量表示
tldr: 句子表示是众多自然语言处理应用的基础，但现有基于大模型的方法多取最后一层隐藏状态，其面向下一token预测而难以捕捉全局句级语义。作者提出新视角，指出注意力值向量比隐藏状态更能编码句子语义，并给出免训练的值聚合方法VA，跨多层与多token位置池化。实验表明VA在免训练设置下优于其他LLM句向量，甚至比肩集成方法MetaEOL。该工作为高效句表示提供了简洁有效的新方案。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 现有LLM句向量多依赖最后一层隐藏状态，其面向下一token预测，难以捕捉全局句级语义。
method: 提出免训练的值聚合方法VA，跨多层与多token位置对注意力值向量进行池化以生成句表示。
result: 在免训练设置下VA优于其他LLM句向量方法，并可媲美集成方法MetaEOL。
conclusion: 表明注意力值向量是更有效的句语义载体，为自然语言处理表示学习提供新思路。
---

## Abstract
Sentence representations are foundational to many Natural Language Processing (NLP) applications. While recent methods leverage Large Language Models (LLMs) to derive sentence representations, most rely on final-layer hidden states, which are optimized for next-token prediction and thus often fail to capture global, sentence-level semantics.
This paper introduces a novel perspective, demonstrating that attention value vectors capture sentence semantics more effectively than hidden states. We propose *Value Aggregation (VA)*, a simple method that pools token values across multiple layers and token indices. In a training-free setting, VA outperforms other LLM-based embeddings, even matches or surpasses the ensemble-based MetaEOL. Furthermore, we demonstrate that when paired with suitable prompts, the layer attention outputs can be interpreted as aligned weighted value vectors. Specifically, the attention scores of the last token function as the weights, while the output projection matrix ($W_O$) aligns these weighted value vectors with the common space of the LLM residual stream. This refined method, termed *Aligned Weighted VA (AlignedWVA)*, achieves state-of-the-art performance among training-free LLM-based embeddings, outperforming the high-cost MetaEOL by a substantial margin. Finally, we highlight the potential of obtaining strong LLM embedding models through fine-tuning Value Aggregation.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
面向自然语言处理应用的LLM句向量表示。

### 2. 核心内容
句子表示是众多自然语言处理应用的基础，但现有基于大模型的方法多取最后一层隐藏状态，其面向下一token预测而难以捕捉全局句级语义。作者提出新视角，指出注意力值向量比隐藏状态更能编码句子语义，并给出免训练的值聚合方法VA，跨多层与多token位置池化。实验表明VA在免训练设置下优于其他LLM句向量，甚至比肩集成方法MetaEOL。该工作为高效句表示提供了简洁有效的新方案。

### 3. 对应检索需求
natural language processing techniques。

### 4. 来源与原文
- Source：ICML-2026-Accepted
- OpenReview：[https://openreview.net/forum?id=nAfV9H2Z1u](https://openreview.net/forum?id=nAfV9H2Z1u)
