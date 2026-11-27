---
title: Structurally Aligned Subtask-Level Memory for Software Engineering Agents
title_zh: 面向软件工程智能体的结构对齐子任务级记忆
authors: "Kangning Shen, Jingyuan Zhang, Chenxi Sun, Wencong Zeng, Yang Yue"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf/3e2e8de22a1fb642ce3897235fef2bb6eef954c0.pdf"
tags: ["query:ai-se"]
score: 9.0
evidence: 面向大模型软件工程智能体的子任务级记忆
tldr: 大模型作为自主软件工程智能体展现出潜力，近期工作引入记忆机制以支撑长周期推理，但通常以整个问题求解过程为原子单位进行存储与检索。作者实证表明实例级记忆存在粒度失配，当任务表面描述相似而各阶段所需推理不同时会导致错误检索。为此提出结构对齐的子任务级记忆方法，使记忆的存储、检索与更新在子任务粒度上对齐。该方法提升了软件工程智能体长周期推理中的检索准确性，为智能体记忆设计提供了新思路。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 现有软件工程智能体的记忆以整个实例为粒度，存在粒度失配，导致相似任务下的错误检索。
method: 提出结构对齐的子任务级记忆方法，使记忆的存储、检索与更新在子任务粒度上对齐。
result: 实验表明子任务级记忆缓解了实例级记忆的检索偏差，提升了长周期推理表现。
conclusion: 为软件工程智能体的记忆机制设计提供了更细粒度且结构对齐的方案。
---

## Abstract
Large Language Models (LLMs) have demonstrated significant potential as autonomous software engineering (SWE) agents. Recent work has further explored augmenting these agents with memory mechanisms to support long-horizon reasoning. However, these approaches typically operate at a coarse instance granularity, treating the entire problem-solving episode as the atomic unit of storage and retrieval. We empirically demonstrate that instance-level memory suffers from a fundamental granularity mismatch, resulting in misguided retrieval when tasks with similar surface descriptions require distinct reasoning logic at specific stages. To address this, we propose Structurally Aligned Subtask-Level Memory, a method that aligns memory storage, retrieval, and updating with the agent’s functional decomposition. Extensive experiments on SWE-bench Verified demonstrate that our method consistently outperforms both vanilla agents and strong instance-level memory baselines across diverse backbones, improving mean Pass@1 over the vanilla agent by +4.7 pp on average (e.g., +6.8 pp on Gemini 2.5 Pro). Performance gains grow with more interaction steps, showing that leveraging past experience benefits long-horizon reasoning in complex software engineering tasks.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
面向大模型软件工程智能体的子任务级记忆。

### 2. 核心内容
大模型作为自主软件工程智能体展现出潜力，近期工作引入记忆机制以支撑长周期推理，但通常以整个问题求解过程为原子单位进行存储与检索。作者实证表明实例级记忆存在粒度失配，当任务表面描述相似而各阶段所需推理不同时会导致错误检索。为此提出结构对齐的子任务级记忆方法，使记忆的存储、检索与更新在子任务粒度上对齐。该方法提升了软件工程智能体长周期推理中的检索准确性，为智能体记忆设计提供了新思路。

### 3. 对应检索需求
autonomous agents for coding tasks。

### 4. 来源与原文
- Source：ICML-2026-Accepted
- OpenReview：[https://openreview.net/forum?id=2CoRS45Ucj](https://openreview.net/forum?id=2CoRS45Ucj)
