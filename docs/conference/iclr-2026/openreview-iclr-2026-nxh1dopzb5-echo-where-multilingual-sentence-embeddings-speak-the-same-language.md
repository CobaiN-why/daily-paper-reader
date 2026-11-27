---
title: "ECHO: Where Multilingual Sentence Embeddings Speak the Same Language"
title_zh: ECHO：让多语言句子嵌入说同一种语言
authors: "João Maria Janeiro, Pere-Lluís Huguet Cabot, Ioannis Tsiamas, Artyom Kozhevnikov, David Dale, Belen Alastruey, Alexandre Mourachko, Holger Schwenk, Loic Barrault, Kevin Heffernan, Paul-Ambroise Duquenne"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=nXH1DopZb5"
tags: ["query:ai-se"]
score: 5.0
evidence: 结合大模型初始化与难负样本的跨语言句子编码器
tldr: 跨语言句子编码器需同时兼顾下游性能与跨语言对齐，早期对比学习方法未能充分利用难负样本。本文提出跨语言句子编码器ECHO，融合对比学习目标、大模型初始化与难负样本使用，以弥合对比与非对比方法之间的差距。该设计在保持强下游表现的同时提升跨语言对齐效果，为多语言自然语言处理中的句子表示学习提供了新方案。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 跨语言句子编码器难以兼顾下游性能与跨语言对齐，现有方法未充分利用难负样本。
method: 提出融合对比目标、大模型初始化与难负样本的跨语言句子编码器ECHO。
result: 该方法在强下游表现与跨语言对齐之间取得更好平衡。
conclusion: ECHO为多语言句子表示与跨语言对齐提供了有效的编码器设计。
---

## Abstract
Cross-lingual sentence encoders create unified embedding representations of sentences across languages. However, achieving both strong downstream performance and cross-lingual alignment remains a fundamental challenge. Early models relied on contrastive learning, yet were unable to leverage hard negatives to unlock the full benefits of the contrastive paradigm. These contrastive approaches were surpassed by non-contrastive approaches leveraging token-level decoders. This is in contrast with recent generic embedding models that achieve strong results by combining contrastive objectives, large language models (LLMs) initialization, and hard negatives usage.
We introduce ECHO, a novel cross-lingual sentence encoder that bridges this gap by integrating pretrained LLMs in an Encoder-Decoder architecture with contrastive training and hard negatives. Our bottleneck Encoder-Decoder design forces the model to capture essential semantic information in a shared vector space while preserving fine-grained nuances. ECHO achieves half of the error rate of the previous state-of-the-art encoders in cross-lingual similarity search across 200 languages, while showcasing unprecedented cross-lingual transfer on downstream tasks.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
结合大模型初始化与难负样本的跨语言句子编码器。

### 2. 核心内容
跨语言句子编码器需同时兼顾下游性能与跨语言对齐，早期对比学习方法未能充分利用难负样本。本文提出跨语言句子编码器ECHO，融合对比学习目标、大模型初始化与难负样本使用，以弥合对比与非对比方法之间的差距。该设计在保持强下游表现的同时提升跨语言对齐效果，为多语言自然语言处理中的句子表示学习提供了新方案。

### 3. 对应检索需求
natural language processing techniques。

### 4. 来源与原文
- Source：ICLR-2026-Rejected-Public
- OpenReview：[https://openreview.net/forum?id=nXH1DopZb5](https://openreview.net/forum?id=nXH1DopZb5)
