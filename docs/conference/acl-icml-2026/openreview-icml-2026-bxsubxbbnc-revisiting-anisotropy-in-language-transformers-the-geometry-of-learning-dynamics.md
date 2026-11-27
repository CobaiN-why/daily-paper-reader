---
title: "Revisiting Anisotropy in Language Transformers: The Geometry of Learning Dynamics"
title_zh: 重访语言Transformer中的各向异性：学习动力学的几何
authors: "Raphael Bernas, Fanny Jourdan, Antonin Poché, CELINE HUDELOT"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf/8b4389f30d4e69a74c3e5aae2d97d05492d3ba49.pdf"
tags: ["query:ai-se"]
score: 4.0
evidence: 语言Transformer中各向异性几何的理论分析
tldr: Transformer架构主导了自然语言处理，但模型表征存在固有的各向异性现象，给几何解释带来挑战。已有理论研究很少从表征几何本身出发进行论证。作者补充了基于表征几何的理论分析，说明该现象的问题本质，并在训练检查点阶段而非事后应用机制可解释性技术来观察模型内部几何动态。通过分析多个模型，该工作加深了对语言模型学习动力学与表征结构的理解，属于NLP基础理论研究。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 语言Transformer存在固有的各向异性现象，已有理论研究缺乏基于表征几何的论证。
method: 从表征几何角度给出理论分析，并在训练检查点阶段应用机制可解释性技术观察模型内部几何动态。
result: 通过多模型分析揭示了各向异性现象的本质及其与学习动力学的关系。
conclusion: 为理解语言模型表征几何与训练动态提供了理论基础，属NLP基础研究。
---

## Abstract
Since their introduction, Transformer architectures have dominated Natural Language Processing (NLP). However, recent research has highlighted an inherent anisotropy phenomenon in these models, presenting a significant challenge to their geometric interpretation. Previous theoretical studies on this phenomenon are rarely based on the underlying representation geometry. In this paper, we extend them by providing such theoretical arguments assessing the problematic nature of this phenomenon. Furthermore, to observe geometric internal model dynamics, we apply mechanistic interpretability (MI) techniques during the model's training checkpoints rather than post-hoc, as it is commonly done in the literature. By analyzing multiple models and their checkpoints -including EuroBERT, the Pythia suite, and SmolLM2- we investigate the structure of embedding representations and their correlation with the on manifold entropy of their underlying distribution.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
语言Transformer中各向异性几何的理论分析。

### 2. 核心内容
Transformer架构主导了自然语言处理，但模型表征存在固有的各向异性现象，给几何解释带来挑战。已有理论研究很少从表征几何本身出发进行论证。作者补充了基于表征几何的理论分析，说明该现象的问题本质，并在训练检查点阶段而非事后应用机制可解释性技术来观察模型内部几何动态。通过分析多个模型，该工作加深了对语言模型学习动力学与表征结构的理解，属于NLP基础理论研究。

### 3. 对应检索需求
recent advances in NLP。

### 4. 来源与原文
- Source：ICML-2026-Accepted
- OpenReview：[https://openreview.net/forum?id=BxSubxbbNc](https://openreview.net/forum?id=BxSubxbbNc)
