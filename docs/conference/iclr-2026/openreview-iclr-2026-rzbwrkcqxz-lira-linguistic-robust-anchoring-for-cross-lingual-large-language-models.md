---
title: "LiRA: Linguistic Robust Anchoring for Cross-lingual Large Language Models"
title_zh: LiRA：面向跨语言大模型的稳健语言锚定
authors: "Haolin Li, Haipeng Zhang, Mang Li, Yaohua Wang, Lijie Wen, zhang yu, Biqing Huang"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=rZBWRkcqXZ"
tags: ["query:ai-se"]
score: 5.0
evidence: 跨语言大模型表征训练框架
tldr: 大模型在高资源语言上趋于饱和，但受限于训练数据不足与对齐不稳，低资源语言表现明显偏弱。本文提出LiRA训练框架，通过锚定表征组合结构与多智能体协同编码，将低资源语言锚定到英语语义空间，并联合增强检索与推理能力。实验表明该框架在低资源条件下稳健提升跨语言表征与下游任务表现，为多语言NLP提供了可迁移的对齐方法。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 低资源语言因数据稀缺与对齐不稳导致大模型表现偏弱，亟需稳健的跨语言表征方法。
method: 提出LiRA训练框架，通过锚定表征组合与多智能体协同编码将低资源语言对齐到英语语义空间。
result: 在低资源条件下稳健提升跨语言表征质量，并联合增强检索与推理能力。
conclusion: 为多语言大模型的对齐与低资源语言能力提升提供了可迁移的训练框架。
---

## Abstract
As large language models (LLMs) rapidly advance, performance on high-resource languages (e.g., English, Chinese) is nearing saturation, yet remains substantially lower for low-resource languages (e.g., Urdu, Thai) due to limited training data, machine-translation noise, and unstable cross-lingual alignment. We introduce LiRA (Linguistic Robust Anchoring for Large Language Models), a training framework that robustly improves cross-lingual representations under low-resource conditions while jointly strengthening retrieval and reasoning. LiRA comprises two modules: (i) Arca (Anchored Representation Composition Architecture), which anchors low-resource languages to an English semantic space via anchor-based alignment and multi-agent collaborative encoding, preserving geometric stability in a shared embedding space; and (ii) LaCR (Language-coupled Semantic Reasoner), which adds a language-aware lightweight reasoning head with consistency regularization on top of Arca’s multilingual representations, unifying the training objective to enhance cross-lingual understanding, retrieval, and reasoning robustness. We further construct and release a multilingual product retrieval dataset covering five Southeast Asian and two South Asian languages. Experiments across low-resource benchmarks (cross-lingual retrieval, semantic similarity, and reasoning) show consistent gains and robustness under few-shot and noise-amplified settings; ablations validate the contribution of both Arca and LaCR. Code will be released on GitHub and the dataset on Hugging Face.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
跨语言大模型表征训练框架。

### 2. 核心内容
大模型在高资源语言上趋于饱和，但受限于训练数据不足与对齐不稳，低资源语言表现明显偏弱。本文提出LiRA训练框架，通过锚定表征组合结构与多智能体协同编码，将低资源语言锚定到英语语义空间，并联合增强检索与推理能力。实验表明该框架在低资源条件下稳健提升跨语言表征与下游任务表现，为多语言NLP提供了可迁移的对齐方法。

### 3. 对应检索需求
natural language processing techniques。

### 4. 来源与原文
- Source：ICLR-2026-Rejected-Public
- OpenReview：[https://openreview.net/forum?id=rZBWRkcqXZ](https://openreview.net/forum?id=rZBWRkcqXZ)
