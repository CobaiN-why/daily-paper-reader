---
title: "Prior-based Noisy Text Data Filtering: Fast and Strong Alternative For Perplexity"
title_zh: 基于先验的噪声文本数据过滤：困惑度的快速强替代方案
authors: "Yeongbin Seo, Gayoung Kim, Jaehyung Kim, Jinyoung Yeo"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=VDjbFzbD2f"
tags: ["query:ai-se"]
score: 4.0
evidence: 面向大模型预训练的基于先验的文本过滤
tldr: 大模型预训练需从海量网页语料中筛选高质量数据，基于困惑度的过滤虽有效但耗时且对噪声或分布外样本不可靠。本文提出基于先验的数据过滤方法，利用语料级词频统计估计词元先验，并依据其均值与标准差筛选文档，作为困惑度的快速替代。该方法在保持过滤效果的同时显著降低计算成本，为高效数据清洗提供了新思路。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 基于困惑度的预训练数据过滤耗时且对噪声样本不可靠，需要更高效可靠的替代方案。
method: 利用语料级词频统计估计词元先验，并依据先验均值与标准差筛选文档作为困惑度代理。
result: 在保持过滤效果的同时显著降低计算开销，成为困惑度的快速替代。
conclusion: 为大规模预训练语料的高效数据筛选提供了轻量可行的新方法。
---

## Abstract
As large language models (LLMs) are pretrained on massive web corpora, careful selection of data becomes essential to ensure effective and efficient learning. While perplexity (PPL)-based filtering has demonstrated strong performance, it suffers from drawbacks: substantial time costs and inherent unreliability of the model when handling noisy or out-of-distribution samples. In this work, we propose a simple yet powerful alternative: a prior-based data filtering method that estimates token priors using corpus-level term frequency statistics, inspired by linguistic insights on word roles and lexical density. Our approach filters documents based on the mean and standard deviation of token priors, serving as a fast proxy to PPL while requiring no model inference. Despite its simplicity, the prior-based filter achieves the highest average performance across 20 downstream benchmarks, while reducing time cost by over 1000× compared to PPL-based filtering. We further demonstrate its applicability to symbolic languages such as code and math, and its dynamic adaptability to multilingual corpora without supervision.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
面向大模型预训练的基于先验的文本过滤。

### 2. 核心内容
大模型预训练需从海量网页语料中筛选高质量数据，基于困惑度的过滤虽有效但耗时且对噪声或分布外样本不可靠。本文提出基于先验的数据过滤方法，利用语料级词频统计估计词元先验，并依据其均值与标准差筛选文档，作为困惑度的快速替代。该方法在保持过滤效果的同时显著降低计算成本，为高效数据清洗提供了新思路。

### 3. 对应检索需求
natural language processing techniques。

### 4. 来源与原文
- Source：ICLR-2026-Accepted
- OpenReview：[https://openreview.net/forum?id=VDjbFzbD2f](https://openreview.net/forum?id=VDjbFzbD2f)
