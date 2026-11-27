---
title: Fine-tuning large language models for text ranking with listwise constraints
title_zh: 基于列表级约束微调大语言模型用于文本排序
authors: "Jiawen Song, Bingfei Zhang, Sai Gao, Xueyao Zhang, Wenqing Xu, Guanyu Chen, Junwei Xing, Hui Li, Yunpeng Peng, Zhi Zang"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=05uq3XUJaT"
tags: ["query:ai-se"]
score: 6.0
evidence: 基于大模型的文本排序检索框架
tldr: 本文针对大模型检索增强中排序质量有待提升的问题，提出一个面向文本排序的大模型微调框架。方法上融合注意力机制的隐层表示、引入多层感知机增强特征变换，并设计列表级ListRank损失以刻画细粒度相关性顺序。实验结果表明该模型取得当前最优的排序性能，并公开了模型。该工作为基于大模型的相关性排序与检索增强提供了可复用方案。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 大模型检索增强下游任务时，排序质量仍需提升，现有方法对细粒度相关性顺序建模不足。
method: 提出融合隐层注意力、MLP特征变换与列表级ListRank损失的大模型检索排序框架。
result: 实验显示该框架在文本排序任务上达到当前最优性能，并公开模型。
conclusion: 该工作为大模型驱动的检索增强与相关性排序提供了有效的微调方法。
---

## Abstract
With the rapid adoption of large language models (LLMs) across diverse applications, retrieval augmentation has become a key factor for improving downstream performance. Recent advances show that LLM-based retrieval can substantially enhance ranking quality. In this work, we present a novel LLM-based retrieval framework optimized along three complementary dimensions: (1) a customized attention-based fusion of hidden-layer representations, (2) a dedicated multi-layer perceptron (MLP) module for enriched feature transformation, and (3) a new list-wise learning objective, ListRank loss, to capture fine-grained relevance order. Experimental results demonstrate that our model achieves state-of-the-art performance. The model is publicly available for download on HuggingFace.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
基于大模型的文本排序检索框架。

### 2. 核心内容
本文针对大模型检索增强中排序质量有待提升的问题，提出一个面向文本排序的大模型微调框架。方法上融合注意力机制的隐层表示、引入多层感知机增强特征变换，并设计列表级ListRank损失以刻画细粒度相关性顺序。实验结果表明该模型取得当前最优的排序性能，并公开了模型。该工作为基于大模型的相关性排序与检索增强提供了可复用方案。

### 3. 对应检索需求
large language models and their applications。

### 4. 来源与原文
- Source：ICLR-2026-Public
- OpenReview：[https://openreview.net/forum?id=05uq3XUJaT](https://openreview.net/forum?id=05uq3XUJaT)
