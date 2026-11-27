---
title: Knowledge-Centric Data Selection for Effective Domain Adaptation of Language Models
title_zh: 面向语言模型高效领域适配的知识中心数据选择
authors: "tianfeng zhao, ZICHENG ZHAO, XinyangGuo, Xingwu Liu, Xiang Cheng, Shaofang Nie, Shuai Cheng Li, Ming Li"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=7ZRF2ZkJpt"
tags: ["query:ai-se"]
score: 5.0
evidence: 面向大语言模型训练的熵基数据过滤
tldr: 大规模语料常含噪声与冗余，现有过滤依赖人工或启发式方法，缺乏量化准则。本文提出基于熵的数据过滤框架，定量评估单个样本的信息量与覆盖度。实验表明该方法能系统筛选高价值数据，提升监督微调效率并改善检索增强质量。该工作为语言模型领域自适应提供了可复用的数据选择方案。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 大规模语料含噪声与冗余，现有数据过滤依赖人工或启发式方法，缺乏量化准则。
method: 提出基于熵的数据过滤框架，定量评估单个样本的信息量与覆盖度以筛选高价值数据。
result: 方法提升监督微调效率，并改善检索增强场景下的检索质量。
conclusion: 该工作为语言模型领域自适应提供了系统化且可复用的数据选择方案。
---

## Abstract
Data filtering remains a fundamental challenge in training large language models (LLMs). Large-scale corpora often contain noisy or redundant samples that undermine training efficiency and limit model performance. Existing approaches typically rely on manual curation or heuristic model-based filtering, yet lack a principled and widely accepted quantitative criterion for deciding which data should be retained. To address this gap, we propose an entropy-based data filtering framework that quantitatively evaluates the informativeness and coverage of individual samples. Our method enables the systematic selection of high-value data, improving the efficiency of supervised fine-tuning (SFT) while also enhancing retrieval quality in retrieval-augmented generation (RAG). These results highlight the effectiveness of entropy-driven filtering as a general strategy for improving both adaptation and retrieval in large-scale LLM pipelines.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
面向大语言模型训练的熵基数据过滤。

### 2. 核心内容
大规模语料常含噪声与冗余，现有过滤依赖人工或启发式方法，缺乏量化准则。本文提出基于熵的数据过滤框架，定量评估单个样本的信息量与覆盖度。实验表明该方法能系统筛选高价值数据，提升监督微调效率并改善检索增强质量。该工作为语言模型领域自适应提供了可复用的数据选择方案。

### 3. 对应检索需求
large language models and their applications。

### 4. 来源与原文
- Source：ICLR-2026-Rejected-Public
- OpenReview：[https://openreview.net/forum?id=7ZRF2ZkJpt](https://openreview.net/forum?id=7ZRF2ZkJpt)
