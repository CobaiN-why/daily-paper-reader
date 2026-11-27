---
title: Partial-Correlation Learning for Large Language Models with Skip-Tuning
title_zh: 基于Skip-Tuning的大模型部分相关学习
authors: "Yuheng Lu, Zuhe Song, Caixia Yuan, Xiaojie Wang"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=21j00qo8P4"
tags: ["query:ai-se"]
score: 5.0
evidence: 基于跳跃语言建模的大模型微调策略
tldr: 大模型在监督微调中若使用完整连续文本，易因大量常见风格文本导致分布偏移，引发过拟合与灾难性遗忘。本文提出Skip-Tuning，一种利用非连续文本片段的微调策略，通过跳跃语言建模实现部分相关学习，使模型仅从稀疏但富含知识的片段中学习。该方法有助于保留预训练知识并提升领域适应效果，为大模型后训练提供了一种更稳健的微调思路。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 传统监督微调使用完整连续文本，易造成与预训练语料的分布偏移，导致过拟合和灾难性遗忘。
method: 提出Skip-Tuning微调策略，使用非连续文本片段进行跳跃语言建模，实现部分相关学习，仅利用知识密集片段。
result: 该方法可减少常见风格文本带来的分布偏移，在注入领域知识的同时缓解过拟合与遗忘。
conclusion: 为大模型后训练提供了一种更稳健、更保知识的微调范式。
---

## Abstract
Large Language Models (LLMs) require post-training to adapt to specific applications, with Supervised Fine-Tuning (SFT) crucial for injecting emerging or domain-specific knowledge. Conventional SFT using complete sequential text risks causing a distribution shift from pretraining corpora due to large volumes of common-style text, potentially leading to overfitting and catastrophic forgetting. We introduce Skip-Tuning, a novel fine-tuning strategy that utilizes noncontinuous text segments instead. Skip-Tuning performs skipped language modeling on text segments and enables a paradigm of partial-correlation learning, where the model learns from sparse but meaningful text fragments. By excluding common-style texts and using only knowledge-intensive text for fine-tuning, Skip-Tuning demonstrates improvements in fine-tuning effectiveness and generalization in the knowledge editing setting. Furthermore, we demonstrate the effectiveness of partial-correlation learning in a system-prompt following task, which illustrates the broad application of Skip-Tuning across various NLP scenarios.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
基于跳跃语言建模的大模型微调策略。

### 2. 核心内容
大模型在监督微调中若使用完整连续文本，易因大量常见风格文本导致分布偏移，引发过拟合与灾难性遗忘。本文提出Skip-Tuning，一种利用非连续文本片段的微调策略，通过跳跃语言建模实现部分相关学习，使模型仅从稀疏但富含知识的片段中学习。该方法有助于保留预训练知识并提升领域适应效果，为大模型后训练提供了一种更稳健的微调思路。

### 3. 对应检索需求
large language models and their applications。

### 4. 来源与原文
- Source：ICLR-2026-Public
- OpenReview：[https://openreview.net/forum?id=21j00qo8P4](https://openreview.net/forum?id=21j00qo8P4)
