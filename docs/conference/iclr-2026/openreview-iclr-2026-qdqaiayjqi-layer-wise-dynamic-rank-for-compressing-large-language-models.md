---
title: Layer-wise dynamic rank for compressing large language models
title_zh: 面向大模型压缩的逐层动态秩方法
authors: "Zhendong Mi, Bian Sun, Grace Li Zhang, Shaoyi Huang"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=qDQAiayjQI"
tags: ["query:ai-se"]
score: 4.0
evidence: 面向大模型的逐层动态秩压缩
tldr: 大模型规模迅速增长带来严重的内存与计算开销，SVD后训练压缩虽受关注，但现有方法对各层采用统一压缩率，忽视了层内信息异质性。本文重新审视SVD压缩，提出D-Rank框架，按层动态分配平衡的秩以保留信息。该工作在不显著损失性能的前提下提升了压缩效率，为大模型部署与落地提供了更实用的压缩方案。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 现有SVD压缩对各层采用统一压缩率，忽视了层内信息的异质性。
method: 提出D-Rank框架，按层动态分配平衡的秩进行SVD后训练压缩。
result: 该方法在保持模型性能的同时提升了压缩效率。
conclusion: 为大模型的高效部署提供了更贴合层间差异的压缩方案。
---

## Abstract
Large language models (LLMs) have rapidly scaled in size, bringing severe memory and computational challenges that hinder their deployment. Singular Value Decomposition (SVD)-based compression has emerged as an appealing post-training compression technique for LLMs, yet most existing methods apply a uniform compression ratio across all layers, implicitly assuming homogeneous information included in various layers. This overlooks the substantial intra-layer heterogeneity observed in LLMs, where middle layers tend to encode richer information while early and late layers are more redundant. In this work, we revisit the existing SVD-based compression method and propose D-Rank, a framework with layer-wise balanced Dynamic Rank allocation for LLMs compression. We first introduce effective rank as a principled metric to measure the information density of weight matrices, and then allocate ranks via a Lagrange multiplier-based optimization scheme to adaptively assign more capacity to groups with higher information density under a fixed compression ratio. Moreover, we rebalance the allocated ranks across attention layers to account for their varying importance and extend D-Rank to latest LLMs with grouped-query attention. Extensive experiments on various LLMs with different scales across multiple compression ratios demonstrate that D-Rank consistently outperforms SVD-LLM, ASVD, and Basis Sharing, achieving more than 15 lower perplexity with LLaMA-3-8B model on C4 datasets at 20% compression ratio and up to 5% higher zero-shot reasoning accuracy with LLaMA-7B model at 40% compression ratio while achieving even higher throughput.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
面向大模型的逐层动态秩压缩。

### 2. 核心内容
大模型规模迅速增长带来严重的内存与计算开销，SVD后训练压缩虽受关注，但现有方法对各层采用统一压缩率，忽视了层内信息异质性。本文重新审视SVD压缩，提出D-Rank框架，按层动态分配平衡的秩以保留信息。该工作在不显著损失性能的前提下提升了压缩效率，为大模型部署与落地提供了更实用的压缩方案。

### 3. 对应检索需求
large language models and their applications。

### 4. 来源与原文
- Source：ICLR-2026-Rejected-Public
- OpenReview：[https://openreview.net/forum?id=qDQAiayjQI](https://openreview.net/forum?id=qDQAiayjQI)
