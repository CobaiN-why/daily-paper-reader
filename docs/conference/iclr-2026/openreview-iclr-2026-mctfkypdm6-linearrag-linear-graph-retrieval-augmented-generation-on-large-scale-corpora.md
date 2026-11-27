---
title: "LinearRAG: Linear Graph Retrieval Augmented Generation on Large-scale Corpora"
title_zh: LinearRAG：面向大规模语料的线性图检索增强生成
authors: "Luyao Zhuang, Shengyuan Chen, Yilin Xiao, Huachi Zhou, Yujing Zhang, Hao Chen, Qinggang Zhang, Xiao Huang"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=mCtfkypdm6"
tags: ["query:ai-se"]
score: 5.0
evidence: 缓解大模型幻觉的图检索增强生成方法
tldr: 检索增强生成常用于缓解大模型幻觉，但面对大规模碎片化语料时效果有限，而图式RAG又依赖不稳定且昂贵的关系抽取，易产生噪声图。本文重新审视GraphRAG流程并提出LinearRAG，以线性化方式构建图结构以提升检索质量。方法旨在支持复杂多跳推理并降低图构建成本，为大模型在知识密集型任务中的应用提供更稳健的检索支撑。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 传统检索增强生成难以处理大规模碎片化语料，图式方法又受困于不稳定且昂贵的关系抽取噪声。
method: 重新设计GraphRAG流程，提出LinearRAG以线性化方式构建图并改进检索。
result: 方法降低图构建开销与噪声关系影响，提升复杂多跳查询下的检索质量。
conclusion: 为大规模语料下缓解大模型幻觉提供了更稳健高效的检索增强生成方案。
---

## Abstract
Retrieval-Augmented Generation (RAG) is widely used to mitigate hallucinations of Large Language Models (LLMs) by leveraging external knowledge. While effective for simple queries, traditional RAG systems struggle with large-scale, unstructured corpora where information is fragmented. Recent advances incorporate knowledge graphs to capture relational structures, enabling more comprehensive retrieval for complex, multi-hop reasoning tasks. However, existing graph-based RAG (GraphRAG) methods rely on unstable and costly relation extraction for graph construction, often producing noisy graphs with incorrect or inconsistent relations that degrade retrieval quality. In this paper, we revisit the pipeline of existing GraphRAG systems and propose Linear Graph-based Retrieval-Augmented Generation (LinearRAG), an efficient framework that enables reliable graph construction and precise passage retrieval. Specifically, LinearRAG constructs a relation-free hierarchical graph, termed Tri-Graph, using only lightweight entity extraction and semantic linking, avoiding unstable relation modeling. This new paradigm of graph construction scales linearly with corpus size and incurs no extra token consumption, providing an economical and reliable indexing of the original passages. For retrieval, LinearRAG adopts a two-stage strategy: (i) relevant entity activation via local semantic bridging, followed by (ii) passage retrieval through global importance aggregation. Extensive experiments on four benchmark datasets demonstrate that LinearRAG significantly outperforms baseline models. Our code and datasets are available at https://github.com/DEEP-PolyU/LinearRAG.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
缓解大模型幻觉的图检索增强生成方法。

### 2. 核心内容
检索增强生成常用于缓解大模型幻觉，但面对大规模碎片化语料时效果有限，而图式RAG又依赖不稳定且昂贵的关系抽取，易产生噪声图。本文重新审视GraphRAG流程并提出LinearRAG，以线性化方式构建图结构以提升检索质量。方法旨在支持复杂多跳推理并降低图构建成本，为大模型在知识密集型任务中的应用提供更稳健的检索支撑。

### 3. 对应检索需求
large language models and their applications。

### 4. 来源与原文
- Source：ICLR-2026-Accepted
- OpenReview：[https://openreview.net/forum?id=mCtfkypdm6](https://openreview.net/forum?id=mCtfkypdm6)
