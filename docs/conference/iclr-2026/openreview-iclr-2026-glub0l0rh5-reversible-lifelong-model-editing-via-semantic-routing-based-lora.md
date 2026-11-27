---
title: Reversible Lifelong Model Editing via Semantic Routing-Based LoRA
title_zh: 基于语义路由LoRA的可逆终身模型编辑
authors: "Haihua Luo, Xuming Ran, Tommi Kärkkäinen, Zhonghua Chen, Jiangrong Shen, Qi Xu, Fengyu Cong"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=glUb0l0rH5"
tags: ["query:ai-se"]
score: 5.0
evidence: 基于LoRA路由的大模型知识编辑
tldr: 大语言模型在顺序知识编辑中常出现语义漂移与知识遗忘，现有模块隔离或参数高效方法难以兼顾稳定性与可逆性。本文提出SoLA框架，将每次编辑封装为独立且训练后冻结的LoRA模块，并借助语义路由记录实现可逆的终身模型编辑。实验表明该方法在连续编辑场景下能有效缓解语义漂移与遗忘。该工作为大模型知识持续更新提供了一种可逆、稳定的编辑范式。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 真实世界知识不断演化，需要对大模型进行持续知识编辑，而现有方法易产生语义漂移与知识遗忘。
method: 提出SoLA框架，将每次编辑封装为独立冻结的LoRA模块，并通过语义路由记录实现可逆的终身编辑。
result: 在顺序编辑场景下有效缓解语义漂移与知识遗忘，实现稳定且可逆的知识更新。
conclusion: 为大模型知识的持续、可逆编辑提供了模块化路由的新思路。
---

## Abstract
Large Language Models (LLMs) have demonstrated remarkable capabilities in natural language processing. However, the dynamic evolution of real-world knowledge necessitates continual editing of specific knowledge within LLMs. While existing model editing methods explore modular isolation or parameter-efficient strategies, they often suffer from semantic drift or knowledge forgetting during sequential editing due to the continual updating of semantic content. To address these challenges, we propose $\textbf{SoLA}$, a $\textbf{S}$emantic r$\textbf{o}$uting-based $\textbf{L}$oR$\textbf{A}$ framework for reversible lifelong model editing. In SoLA, each edit is encapsulated as an independent LoRA module which is frozen after training and a semantic routing record is established to map it to the input semantic representation, allowing dynamic activation of LoRA modules via semantic matching. This mechanism avoids semantic drift caused by clustering updating and mitigates catastrophic forgetting from parameter sharing. Importantly, SoLA supports both insertion and deletion of edits. By simply removing key from the semantic routing, specific edits can be precisely revoked, restoring the model’s original behavior. To our knowledge, this reversible rollback editing capability is the first to be achieved in existing literature. Furthermore, SoLA integrates the decision-making process into the edited layer itself, eliminating the need for auxiliary routing networks and enabling end-to-end decision-making process. Extensive experiments across three representative tasks (document classification, question answering, and hallucination correction) demonstrate that SoLA effectively learns and retains edited knowledge, achieving accurate, efficient, and reversible lifelong model editing.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
基于LoRA路由的大模型知识编辑。

### 2. 核心内容
大语言模型在顺序知识编辑中常出现语义漂移与知识遗忘，现有模块隔离或参数高效方法难以兼顾稳定性与可逆性。本文提出SoLA框架，将每次编辑封装为独立且训练后冻结的LoRA模块，并借助语义路由记录实现可逆的终身模型编辑。实验表明该方法在连续编辑场景下能有效缓解语义漂移与遗忘。该工作为大模型知识持续更新提供了一种可逆、稳定的编辑范式。

### 3. 对应检索需求
large language models and their applications。

### 4. 来源与原文
- Source：ICLR-2026-Rejected-Public
- OpenReview：[https://openreview.net/forum?id=glUb0l0rH5](https://openreview.net/forum?id=glUb0l0rH5)
