---
title: "From Reproduction to Replication: Evaluating Research Agents with Progressive Code Masking"
title_zh: 从复现到复刻：用渐进式代码掩码评估科研智能体
authors: "Gyeongwon James Kim, Alex Wilf, Louis-Philippe Morency, Daniel Fried"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=qBcHWGBnIb"
tags: ["query:ai-se"]
score: 8.0
evidence: 用渐进式代码掩码评估自主编码智能体的基准
tldr: 自主代码生成智能体有望加速科学发现，但缺乏评估其在给定不同代码起点时实现科研想法的基准。本文提出AutoExperiment，通过渐进式代码掩码构造从复现到从零复刻的连续任务谱，评估智能体依据论文自然语言描述实现并运行机器学习实验的能力。该基准为衡量自主编码智能体在真实科研软件工程任务中的能力提供了系统化工具。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 自主代码生成智能体被寄望加速科研，但缺少评估其在给定不同代码起点时实现科研想法的基准。
method: 提出AutoExperiment基准，用渐进式代码掩码构造从复现到从零复刻的任务谱，要求智能体按论文描述实现并运行实验。
result: 该基准系统刻画了智能体在不同代码起点下的实验实现能力，揭示了自主编码智能体的能力边界。
conclusion: 为评估自主编码智能体在真实科研软件工程任务中的能力提供了标准化基准。
---

## Abstract
Recent progress in autonomous code generation has fueled excitement around AI agents capable of accelerating scientific discovery by running experiments. However, there is currently no benchmark that evaluates whether such agents can implement scientific ideas when given varied amounts of code as a starting point, interpolating between reproduction (running code) and from-scratch replication (fully re-implementing and running code). We introduce AutoExperiment, a benchmark that evaluates AI agents’ ability to implement and run machine learning experiments based on natural language descriptions in research papers. In each task, agents are given a research paper, a codebase with key functions masked out, and a command to run the experiment. The goal is to generate the missing code, execute the experiment in a sandboxed environment, and reproduce the results. AutoExperiment scales in difficulty by varying the number of missing functions $n$, ranging from partial reproduction to full replication. We evaluate state-of-the-art agents and find that performance degrades rapidly as $n$ increases. Agents that can dynamically interact with the environment (e.g. to debug their code) can outperform agents in fixed ``agentless'' harnesses, and there exists a significant gap between single-shot and multi-trial success rates (Pass@1 vs. Pass@5), motivating verifier approaches to our benchmark. Our findings highlight critical challenges in long-horizon code generation, context retrieval, and autonomous experiment execution, establishing AutoExperiment as a new benchmark for evaluating progress in AI-driven scientific experimentation. Our data and code are open-sourced at https://github.com/j1mk1m/AutoExperiment.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
用渐进式代码掩码评估自主编码智能体的基准。

### 2. 核心内容
自主代码生成智能体有望加速科学发现，但缺乏评估其在给定不同代码起点时实现科研想法的基准。本文提出AutoExperiment，通过渐进式代码掩码构造从复现到从零复刻的连续任务谱，评估智能体依据论文自然语言描述实现并运行机器学习实验的能力。该基准为衡量自主编码智能体在真实科研软件工程任务中的能力提供了系统化工具。

### 3. 对应检索需求
autonomous agents for coding tasks。

### 4. 来源与原文
- Source：ICLR-2026-Accepted
- OpenReview：[https://openreview.net/forum?id=qBcHWGBnIb](https://openreview.net/forum?id=qBcHWGBnIb)
