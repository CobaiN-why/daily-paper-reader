---
title: "Huxley-G\\\"odel Machine: Human-Level Coding Agent Development by an Approximation of the Optimal Self-Improving Machine"
title_zh: 赫胥黎-哥德尔机：通过逼近最优自我改进机器实现人类水平编码智能体
authors: "Wenyi Wang, Piotr Piękos, Li Nanbo, Firas Laakom, Yimeng Chen, Mateusz Ostaszewski, Mingchen Zhuge, Jürgen Schmidhuber"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=T0EiEuhOOL"
tags: ["query:ai-se"]
score: 8.0
evidence: 通过编辑自身代码库实现自我改进的编码智能体
tldr: 近期研究让编码智能体通过编辑自身代码库实现自我改进，但作者发现智能体的自我改进潜力与其编码基准表现之间存在错配。受赫胥黎进化支概念启发，论文提出指标CMP，通过聚合智能体后代的基准表现来刻画其自我改进潜力。基于该指标的扩展策略更有利于发展出高水平编码智能体，为自主编码智能体的自我进化提供了新的评价与搜索依据。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 现有编码智能体以基准表现衡量自我改进潜力，但二者存在错配，可能误导后续自我修改。
method: 借鉴进化支概念提出聚合后代基准表现的指标CMP，用于衡量智能体自我改进潜力并指导扩展。
result: 实验表明以CMP为指标可更有效地发展出高水平编码智能体。
conclusion: 该工作为自主编码智能体的自我改进评价与搜索提供了新的度量与方向。
---

## Abstract
Recent studies operationalize self-improvement through coding agents that edit their own codebases. They grow a tree of self-modifications through expansion strategies that favor higher software engineering benchmark performance, assuming that this implies more promising subsequent self-modifications. However, we identify a mismatch between the agent’s self-improvement potential (metaproductivity) and its coding benchmark performance, namely the Metaproductivity-Performance~Mismatch. Inspired by Huxley’s concept of clade, we propose a metric ($\mathrm{CMP}$) that aggregates the benchmark performances of the descendants of an agent as an indicator of its potential for self-improvement. We show that, in our self-improving coding agent development setting, access to the true CMP is sufficient to simulate how the Gödel Machine would behave under certain assumptions. We introduce the Huxley-G\"odel Machine (HGM), which, by estimating $\mathrm{CMP}$ and using it as guidance, searches the tree of self-modifications. On SWE-bench Verified and Polyglot, HGM outperforms prior self-improving coding agent development methods while using fewer allocated CPU hours. Last but not least, HGM demonstrates strong transfer to other coding datasets and LLMs. %large language models. 
The agent optimized by HGM on SWE-bench Verified with GPT-5 mini and evaluated on SWE-bench Lite with GPT-5 achieves human-level performance, matching the best officially checked results of human-engineered coding agents. Our code is publicly available at https://github.com/metauto-ai/HGM.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
通过编辑自身代码库实现自我改进的编码智能体。

### 2. 核心内容
近期研究让编码智能体通过编辑自身代码库实现自我改进，但作者发现智能体的自我改进潜力与其编码基准表现之间存在错配。受赫胥黎进化支概念启发，论文提出指标CMP，通过聚合智能体后代的基准表现来刻画其自我改进潜力。基于该指标的扩展策略更有利于发展出高水平编码智能体，为自主编码智能体的自我进化提供了新的评价与搜索依据。

### 3. 对应检索需求
autonomous agents for coding tasks。

### 4. 来源与原文
- Source：ICLR-2026-Accepted
- OpenReview：[https://openreview.net/forum?id=T0EiEuhOOL](https://openreview.net/forum?id=T0EiEuhOOL)
