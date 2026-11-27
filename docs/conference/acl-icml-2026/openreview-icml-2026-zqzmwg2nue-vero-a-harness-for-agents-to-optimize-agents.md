---
title: "VeRO: A Harness for Agents to Optimize Agents"
title_zh: VeRO：让智能体优化智能体的评测框架
authors: "Varun Ursekar, Apaar Shanker, Veronica Chatrath, Yuan Xue, Samuel Marc Denton"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf/38a8d3fd104d5e22b373e495b857fc055245fcdf.pdf"
tags: ["query:ai-se"]
score: 8.0
evidence: 支持编码智能体优化目标智能体的框架
tldr: 智能体脚手架优化是编码智能体的新兴应用，即通过修改和评估目标智能体的代码来迭代改进它，但社区对其表现缺乏系统认识。该任务不同于传统软件工程，因为脚手架交织着确定性代码与随机的大模型输出，需要同时记录执行轨迹和下游结果。作者提出VeRO外层框架，提供版本化快照、预算受控的评估与结构化执行轨迹，并构建VeRO-Bench基准套件，为研究编码智能体优化智能体提供了系统化工具与评测基础。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 编码智能体用于优化目标智能体的脚手架优化任务缺乏系统认识，且确定性代码与随机模型输出交织带来评测困难。
method: 提出VeRO外层框架，提供版本化快照、预算受控评估与结构化执行轨迹，并构建VeRO-Bench基准套件。
result: 该框架与基准为刻画编码智能体在脚手架优化任务上的表现提供了可复现的评测手段。
conclusion: 为智能体优化智能体这一新兴方向建立了系统化评测基础。
---

## Abstract
An important emerging application of coding agents is *agent harness optimization*: the iterative improvement of a *target agent* by editing and evaluating its code. Despite its relevance, the community lacks a systematic understanding of coding agent performance on this task. Harness optimization differs from conventional software engineering: agent harnesses interleave deterministic code with stochastic LLM completions, requiring structured capture of both intermediate execution traces and downstream outcomes. To address these challenges, we introduce (1) VeRO (Versioning, Rewards, and Observations), an *outer harness* that provides versioned snapshots, budget-controlled evaluation, and structured execution traces of *target harnesses*, and (2) VeRO-Bench, a benchmark suite of target agents and tasks with reference evaluation procedures. Using VeRO, we conduct an empirical study comparing optimizers across tasks and analyzing which modifications reliably improve target agent harnesses. We release VeRO to support research on agent optimization as a core capability for coding agents. Code is available at https://github.com/scaleapi/vero.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
支持编码智能体优化目标智能体的框架。

### 2. 核心内容
智能体脚手架优化是编码智能体的新兴应用，即通过修改和评估目标智能体的代码来迭代改进它，但社区对其表现缺乏系统认识。该任务不同于传统软件工程，因为脚手架交织着确定性代码与随机的大模型输出，需要同时记录执行轨迹和下游结果。作者提出VeRO外层框架，提供版本化快照、预算受控的评估与结构化执行轨迹，并构建VeRO-Bench基准套件，为研究编码智能体优化智能体提供了系统化工具与评测基础。

### 3. 对应检索需求
autonomous agents for coding tasks。

### 4. 来源与原文
- Source：ICML-2026-Accepted
- OpenReview：[https://openreview.net/forum?id=zQzmwG2Nue](https://openreview.net/forum?id=zQzmwG2Nue)
