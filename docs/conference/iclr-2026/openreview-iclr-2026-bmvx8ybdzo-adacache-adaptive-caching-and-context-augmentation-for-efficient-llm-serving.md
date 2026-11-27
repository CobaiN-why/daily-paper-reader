---
title: "AdaCache: Adaptive Caching and Context Augmentation for Efficient LLM Serving"
title_zh: AdaCache：面向高效大模型服务的自适应缓存与上下文增广
authors: "Zeng Zihao, Siyi Li, Xinyu Yan, Lei Xiao, Wei Yang Bryan Lim"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=Bmvx8ybDzo"
tags: ["query:ai-se"]
score: 4.0
evidence: 面向高效大模型服务的自适应缓存
tldr: 检索增强生成通过引入外部知识增强大模型，但扩展输入序列带来显著计算开销。现有RAG系统存在频繁检索块重复处理与过度深度检索两大低效问题。本文提出AdaCache自适应缓存框架，通过缓存感知的部分重计算与上下文增广两种策略优化服务效率。该工作为高效大模型推理部署提供了可复用的系统级方案。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: RAG扩展输入序列带来显著计算开销，且存在检索块重复处理与过度深度检索问题。
method: 提出自适应缓存框架，结合缓存感知的部分重计算与上下文增广两种优化策略。
result: 减少频繁检索块的重复处理并避免过度供给上下文，提升大模型服务效率。
conclusion: 该工作为大模型推理部署提供了系统级的缓存优化方案。
---

## Abstract
Retrieval-Augmented Generation (RAG) significantly enhances Large Language Models by integrating external knowledge sources, but at the cost of substantial computational overhead from extended input sequences. 
Current RAG systems exhibit two fundamental inefficiencies: redundant processing of frequently retrieved text chunks across multiple queries, and uniform deep retrieval that over-provisions context regardless of query complexity.
We present AdaCache, an adaptive caching framework that addresses these limitations through dual optimization strategies. 
First, we introduce a cache-aware partial recomputation mechanism that profiles attention patterns to construct selective cache variants, enabling flexible reuse while preserving cross-chunk dependencies. 
Second, we develop adaptive context augmentation that dynamically determines optimal retrieval depth via lightweight confidence estimation, avoiding unnecessary overhead on simple queries.
Comprehensive experiments across diverse datasets and LLMs demonstrate that AdaCache delivers substantial improvements in Time-To-First-Token compared to state-of-the-art RAG caching systems, while preserving generation quality.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
面向高效大模型服务的自适应缓存。

### 2. 核心内容
检索增强生成通过引入外部知识增强大模型，但扩展输入序列带来显著计算开销。现有RAG系统存在频繁检索块重复处理与过度深度检索两大低效问题。本文提出AdaCache自适应缓存框架，通过缓存感知的部分重计算与上下文增广两种策略优化服务效率。该工作为高效大模型推理部署提供了可复用的系统级方案。

### 3. 对应检索需求
large language models and their applications。

### 4. 来源与原文
- Source：ICLR-2026-Accepted
- OpenReview：[https://openreview.net/forum?id=Bmvx8ybDzo](https://openreview.net/forum?id=Bmvx8ybDzo)
