---
title: Avey-B
title_zh: Avey-B：面向工业NLP的紧凑无注意力双向编码器
authors: "Devang Acharya, Mohammad Hammoud"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=kQ9j5RY8ff"
tags: ["query:ai-se"]
score: 7.0
evidence: 面向工业级NLP的紧凑双向编码器
tldr: 在算力与内存受限的工业场景中，紧凑的双向编码器仍是NLP的核心骨干，但BERT式自注意力结构代价较高。本文将无注意力、自回归的Avey重构为仅编码器范式，提出Avey-B，并引入静态与动态参数解耦、稳定性归一化和神经压缩等创新。实验表明该架构在多项任务上优于四种常用Transformer编码器，为低资源NLP提供了一种高效替代方案。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 算力与内存受限的工业NLP仍依赖紧凑双向编码器，但BERT式自注意力结构计算代价较高。
method: 将无注意力自回归的Avey重构为仅编码器架构，引入静态与动态参数解耦、稳定性归一化和神经压缩。
result: 该重构架构在多项任务上优于四种常用Transformer编码器，展现出更优的性能与效率。
conclusion: 为低资源工业NLP提供了一种高效且具竞争力的无注意力编码器方案。
---

## Abstract
Compact pretrained bidirectional encoders remain the backbone of industrial NLP under tight compute and memory budgets. Their effectiveness stems from self-attention’s ability to deliver high-quality bidirectional contextualization with sequence-level parallelism, as popularized by BERT-style architectures. Recently, **Avey** was introduced as an autoregressive, attention-free alternative that naturally admits an encoder-only adaptation. In this paper, we reformulate Avey for the encoder-only paradigm and propose several innovations to its architecture, including decoupled static and dynamic parameterizations, stability-oriented normalization, and neural compression. Results show that this reformulated architecture compares favorably to four widely used Transformer-based encoders, consistently outperforming them on standard token-classification and information-retrieval benchmarks while scaling more efficiently to long contexts.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
面向工业级NLP的紧凑双向编码器。

### 2. 核心内容
在算力与内存受限的工业场景中，紧凑的双向编码器仍是NLP的核心骨干，但BERT式自注意力结构代价较高。本文将无注意力、自回归的Avey重构为仅编码器范式，提出Avey-B，并引入静态与动态参数解耦、稳定性归一化和神经压缩等创新。实验表明该架构在多项任务上优于四种常用Transformer编码器，为低资源NLP提供了一种高效替代方案。

### 3. 对应检索需求
natural language processing techniques。

### 4. 来源与原文
- Source：ICLR-2026-Accepted
- OpenReview：[https://openreview.net/forum?id=kQ9j5RY8ff](https://openreview.net/forum?id=kQ9j5RY8ff)
