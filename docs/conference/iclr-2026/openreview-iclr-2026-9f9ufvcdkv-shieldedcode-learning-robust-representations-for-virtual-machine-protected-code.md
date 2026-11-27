---
title: "ShieldedCode: Learning Robust Representations for Virtual Machine Protected Code"
title_zh: ShieldedCode：面向虚拟机保护代码的鲁棒表示学习
authors: "Mingqiao Mo, Yunlong Tan, Hao Zhang, Heng Zhang, Yangfan He"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=9F9UFVcDkV"
tags: ["query:ai-se"]
score: 6.0
evidence: 基于大模型的软件保护与鲁棒代码表示
tldr: 大模型在代码生成上进展显著，但其软件保护潜力尚未挖掘，传统虚拟机保护依赖刚性规则且易被自动化分析破解。本文提出首个保护感知框架，学习虚拟机保护代码的鲁棒表示。方法构建源码与规范化VM实现的配对数据集，并引入指令内、前序与指令间的层级依赖建模。工作将大模型能力拓展到软件安全与代码保护领域。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 传统虚拟机保护依赖刚性规则、成本高且易被自动化分析破解，大模型的软件保护潜力未被挖掘。
method: 构建源码与规范化VM实现配对数据集，并引入指令内、前序与指令间的层级依赖建模学习鲁棒表示。
result: 联合语言建模与功能目标优化，提升了对虚拟机保护代码的表示与保护能力。
conclusion: 该工作将大模型能力拓展到软件安全与代码保护方向。
---

## Abstract
Large language models (LLMs) have achieved remarkable progress in code generation, yet their potential for software protection remains largely untapped.    Reverse engineering continues to threaten software security, while traditional virtual machine protection (VMP) relies on rigid, rule-based transformations that are costly to design and vulnerable to automated analysis.    In this work, we present the first protection-aware framework that learns robust representations of VMP-protected code.    Our approach builds large-scale paired datasets of source code and normalized VM implementations, and introduces hierarchical dependency modeling at intra-, preceding-, and inter-instruction levels.    We jointly optimize language modeling with functionality-aware and protection-aware contrastive objectives to capture both semantic equivalence and protection strength.    To further assess resilience, we propose a protection effectiveness optimization task that quantifies and ranks different VM variants derived from the same source. Coupled with a two-stage continual pre-training and fine-tuning pipeline, our method enables models to generate, compare, and reason over protected code. Extensive experiments show that our framework significantly improves robustness across diverse protection levels, opening a new research direction for learning-based software defense. In this work, we present ShieldedCode, the first protection-aware framework that learns robust representations of VMP-protected code. Our method achieves 26.95\% Pass@1 on L0 VM code generation compared to 22.58\% for GPT-4o, and improves binary similarity detection Recall@1 by 10\% over state of art methods like jTrans.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
基于大模型的软件保护与鲁棒代码表示。

### 2. 核心内容
大模型在代码生成上进展显著，但其软件保护潜力尚未挖掘，传统虚拟机保护依赖刚性规则且易被自动化分析破解。本文提出首个保护感知框架，学习虚拟机保护代码的鲁棒表示。方法构建源码与规范化VM实现的配对数据集，并引入指令内、前序与指令间的层级依赖建模。工作将大模型能力拓展到软件安全与代码保护领域。

### 3. 对应检索需求
大模型安全。

### 4. 来源与原文
- Source：ICLR-2026-Accepted
- OpenReview：[https://openreview.net/forum?id=9F9UFVcDkV](https://openreview.net/forum?id=9F9UFVcDkV)
