---
title: Toward Robust Multilingual Adaptation of LLMs for Low-Resource Languages
title_zh: 面向低资源语言的大模型鲁棒多语言适配
authors: "Haolin Li, Haipeng Zhang, Mang Li, Yaohua Wang, Lijie Wen, zhang yu, Biqing Huang"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf/7e024af39686e2ccaa9be7482ef125794be96e41.pdf"
tags: ["query:ai-se"]
score: 6.0
evidence: 面向大模型的多语言适配框架
tldr: 大模型在低资源语言上受限于训练数据稀缺、翻译噪声和跨语言对齐不稳定。作者提出LiRA即插即用框架，在已有预训练骨干上微调，其中Arca通过锚点对齐与协同编码将低资源输入映射到共享英语语义空间，LaSR则用语言感知头提升检索、排序与推理的跨语言一致性。理论分析表明在对齐误差与翻译偏差有界时表示偏移可控，实验验证多语言性能提升。该工作为大模型的多语言应用提供了通用增强方案。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 大模型在低资源语言上因数据不足、翻译噪声和跨语言对齐不稳而表现欠佳。
method: 提出即插即用的LiRA框架，用锚点对齐的Arca模块和语言感知头LaSR提升跨语言一致性。
result: 理论证明表示偏差有界，实验显示多语言适配效果得到改善。
conclusion: 该框架可作为通用组件增强大模型在低资源语言上的应用能力。
---

## Abstract
Large language models (LLMs) continue to struggle with low-resource languages due to limited training data, translation noise, and unstable cross-lingual alignment. We propose LiRA (Linguistic Robust Anchoring for LLMs), a plug-and-play framework that improves multilingual adaptation through fine-tuning on existing pretrained backbones. LiRA combines two components: Arca, which aligns low-resource inputs to a shared English semantic space through anchor-based alignment and collaborative encoding, and LaSR, a language-aware head that promotes cross-lingual consistency for retrieval, ranking, and reasoning. We provide a theoretical analysis showing that, under bounded anchoring error and translation-induced bias, LiRA yields bounded representation deviation and stable downstream behavior under local Lipschitz continuity. We further introduce a multilingual product retrieval dataset covering five Southeast Asian and two South Asian languages. Experiments on retrieval, ranking, question answering, and reasoning benchmarks show that LiRA consistently improves strong multilingual and LLM-based baselines. Code and data will be released publicly.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
面向大模型的多语言适配框架。

### 2. 核心内容
大模型在低资源语言上受限于训练数据稀缺、翻译噪声和跨语言对齐不稳定。作者提出LiRA即插即用框架，在已有预训练骨干上微调，其中Arca通过锚点对齐与协同编码将低资源输入映射到共享英语语义空间，LaSR则用语言感知头提升检索、排序与推理的跨语言一致性。理论分析表明在对齐误差与翻译偏差有界时表示偏移可控，实验验证多语言性能提升。该工作为大模型的多语言应用提供了通用增强方案。

### 3. 对应检索需求
large language models and their applications。

### 4. 来源与原文
- Source：ICML-2026-Accepted
- OpenReview：[https://openreview.net/forum?id=YPq13MlFgO](https://openreview.net/forum?id=YPq13MlFgO)
