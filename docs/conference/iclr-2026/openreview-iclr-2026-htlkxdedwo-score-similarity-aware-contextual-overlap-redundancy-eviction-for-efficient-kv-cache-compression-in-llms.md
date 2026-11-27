---
title: "SCORE: Similarity-Aware Contextual Overlap-Redundancy Eviction for Efficient KV Cache Compression in LLMs"
title_zh: SCORE：面向大模型高效KV缓存压缩的相似度感知上下文重叠冗余淘汰
authors: "Gilha lee, Seungil Lee, Hyun Kim"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=HTlkxdEDWo"
tags: ["query:ai-se"]
score: 4.0
evidence: 面向长上下文大模型推理的KV缓存压缩
tldr: 大模型长上下文能力带来突破，但键值缓存在推理时仍是关键内存瓶颈。现有缓存淘汰策略多依赖启发式或单轴重要性度量，忽视层与注意力头之间的动态交互。本文提出SCORE框架，引入基于距离的多层级相似度度量以量化并消除冗余。该工作为长上下文大模型的高效推理提供了缓存压缩方案。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 长上下文推理中键值缓存是内存瓶颈，现有淘汰策略依赖启发式或单轴度量，忽视层级交互。
method: 提出SCORE框架，引入基于距离的多层级相似度度量来量化并淘汰冗余缓存。
result: 在长上下文场景下实现更有效的KV缓存压缩，缓解推理内存瓶颈。
conclusion: 该工作为长上下文大模型的高效推理提供了新的缓存压缩思路。
---

## Abstract
Recent advances in large language models (LLMs) have unlocked remarkable long-context capabilities, enabling breakthroughs across diverse NLP tasks. However, despite architectural progress and compression techniques such as quantization, the key-value (KV) cache remains a critical memory bottleneck during inference. Prior work has explored cache optimization via eviction strategies, yet most rely on heuristic or single-axis importance metrics, neglecting the nuanced and dynamic interplay between layers and attention heads. In this paper, we propose SCORE (Similarity-aware Contextual Overlap-Redundancy Eviction), a novel framework that introduces a distance-based multi-level similarity metric to quantify and eliminate structural redundancy within the KV cache. By dynamically reallocating cache budgets across layers and heads and employing a redundancy-aware greedy token selection mechanism, SCORE preserves semantic diversity while minimizing memory overhead. Extensive experiments on long-context benchmarks such as LongBench and NeedleBench show that SCORE retains 95\% of full KV cache performance using only 1.5\% of the cache, consistently outperforming state-of-the-art baselines under strict memory constraints. These results underscore the value of fine-grained, context-aware cache management for scalable and efficient long-context inference in LLMs.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
面向长上下文大模型推理的KV缓存压缩。

### 2. 核心内容
大模型长上下文能力带来突破，但键值缓存在推理时仍是关键内存瓶颈。现有缓存淘汰策略多依赖启发式或单轴重要性度量，忽视层与注意力头之间的动态交互。本文提出SCORE框架，引入基于距离的多层级相似度度量以量化并消除冗余。该工作为长上下文大模型的高效推理提供了缓存压缩方案。

### 3. 对应检索需求
large language models and their applications。

### 4. 来源与原文
- Source：ICLR-2026-Public
- OpenReview：[https://openreview.net/forum?id=HTlkxdEDWo](https://openreview.net/forum?id=HTlkxdEDWo)
