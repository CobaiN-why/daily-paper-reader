---
title: Cross-Lingual Data Scaling for Large Language Models
title_zh: 面向大模型的跨语言数据缩放
authors: "Zhihao Wang, Junjie Huang, Jianheng Huang, Tong Sun, Yaoxiang Wang, dingqi, Hongjian Zou, YiXuan Liao, Xiaoxin Chen, Junfeng Yao, Yidong Chen, Jinsong Su"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=yuRO2wZ8su"
tags: ["query:ai-se"]
score: 5.0
evidence: 通过合成数据与知识迁移实现大模型跨语言数据缩放
tldr: 低资源语言受限于小而停滞的数据集，难以随数据规模提升性能。本文提出跨语言数据缩放，系统比较两种途径：将高资源语言数据经翻译或语码转换转为低资源合成数据，以及通过调整预训练语言顺序与比例迁移知识。英中实验表明单纯数据转换难以持续扩展，而知识迁移更有潜力，为低资源语言的大模型能力提升提供了实证指导。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 低资源语言数据集小而停滞，难以随数据规模提升模型性能。
method: 比较合成数据转换与调整预训练语言顺序比例的知识迁移两种跨语言缩放途径。
result: 英中实验显示单纯数据转换难以持续扩展，知识迁移更有效。
conclusion: 为低资源语言的大模型能力提升提供了实证依据与方向。
---

## Abstract
Large language models (LLMs) achieve consistent performance gains through data scaling, yet low-resource languages remain limited by small and stagnant dataset sizes.
To address this limitation, we introduce cross-lingual data scaling, where performance in low-resource languages scales with the dataset size of high-resource languages.
We systematically investigate two potential approaches: (i) transforming high-resource language data into synthetic data for low-resource languages via translation or code-switching, and (ii) transferring the learned knowledge from high-resource languages to low-resource languages by adjusting language order and proportion during pretraining.
Experiments on English and Chinese show that data transformation fails to sustain cross-lingual data scaling, whereas knowledge transfer enables low-resource language performance to scale with the growth of high-resource language data.
Building on these findings, we propose ScaleX, a two-stage pretraining framework designed for effective cross-lingual data scaling.
In the first stage, LLMs are pretrained on high-resource language data under a constant learning rate schedule;
in the second stage, training continues on a mixture of high- and low-resource languages under a cosine learning rate schedule.
ScaleX outperforms existing approaches with progressively larger margins as high-resource data scales up, and further generalizes to both multilingual and large-scale bilingual pretraining.
Our analysis also reveals that learning rate scheduling and shared tokens across languages are critical to sustaining performance scaling in low-resource languages.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
通过合成数据与知识迁移实现大模型跨语言数据缩放。

### 2. 核心内容
低资源语言受限于小而停滞的数据集，难以随数据规模提升性能。本文提出跨语言数据缩放，系统比较两种途径：将高资源语言数据经翻译或语码转换转为低资源合成数据，以及通过调整预训练语言顺序与比例迁移知识。英中实验表明单纯数据转换难以持续扩展，而知识迁移更有潜力，为低资源语言的大模型能力提升提供了实证指导。

### 3. 对应检索需求
recent advances in NLP。

### 4. 来源与原文
- Source：ICLR-2026-Rejected-Public
- OpenReview：[https://openreview.net/forum?id=yuRO2wZ8su](https://openreview.net/forum?id=yuRO2wZ8su)
