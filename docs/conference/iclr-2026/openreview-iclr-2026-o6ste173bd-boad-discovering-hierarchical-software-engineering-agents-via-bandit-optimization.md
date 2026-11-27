---
title: "BOAD: Discovering Hierarchical Software Engineering Agents via Bandit Optimization"
title_zh: BOAD：通过赌博机优化发现分层软件工程智能体
authors: "Iris Xu, Guangtao Zeng, Zexue He, Charles Jin, Aldo Pareja, Dan Gutfreund, Chuang Gan, Zhang-Wei Hong"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=O6stE173BD"
tags: ["query:ai-se"]
score: 9.0
evidence: 将软件工程智能体组织为协调子智能体的编排器
tldr: 现有单一大模型智能体在长程、分布外的真实软件工程问题上泛化能力差，且被迫在一条推理链中保留大量无关上下文。作者借鉴人类工程师的分工方式，将软件工程智能体建模为编排器，协调定位、编辑、验证等专用子智能体，并用基于赌博机的优化方法自动发现层级结构。实验表明该分层设计能提升在真实问题上的泛化与修复表现，为构建更稳健的自主编码智能体提供了新思路。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 单一智能体处理长程软件工程任务时上下文冗余、泛化差，亟需更合理的结构设计。
method: 将软件工程智能体建模为编排器，协调定位、编辑、验证等专用子智能体，并用赌博机优化发现分层结构。
result: 分层智能体设计在真实软件工程问题上改善了泛化能力与修复表现。
conclusion: 分层编排结构为构建更稳健、可泛化的自主编码智能体提供了有效范式。
---

## Abstract
Large language models (LLMs) have shown strong reasoning and coding capabilities, yet they struggle to generalize to real-world software engineering (SWE) problems that are long-horizon and out-of-distribution. Existing systems often rely on a single agent to handle the entire workflow—interpreting issues, navigating large codebases, and implementing fixes—within one reasoning chain. Such monolithic designs force the model to retain irrelevant context, leading to spurious correlations and poor generalization. Motivated by how human engineers decompose complex problems, we propose structuring SWE agents as orchestrators coordinating specialized sub-agents for sub-tasks such as localization, editing, and validation. The challenge lies in discovering effective hierarchies automatically: as the number of sub-agents grows, the search space becomes combinatorial, and it is difficult to attribute credit to individual sub-agents within a team. We address these challenges by formulating hierarchy discovery as a multi-armed bandit (MAB) problem, where each arm represents a candidate sub-agent and the reward measures its helpfulness when collaborating with others. This framework, termed Bandit Optimization for Agent Design (BOAD), enables efficient exploration of sub-agent designs under limited evaluation budgets. On SWE-bench-Verified, BOAD outperforms single-agent and manually designed multi-agent systems. On SWE-bench-Live, featuring more recent and out-of-distribution issues, our 36B system ranks second on the leaderboard at the time of evaluation, surpassing larger models such as GPT-4 and Claude. These results demonstrate that automatically discovered hierarchical multi-agent systems significantly improve generalization on challenging long-horizon SWE tasks. Code is available at https://github.com/iamxjy/BOAD-SWE-Agent.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
将软件工程智能体组织为协调子智能体的编排器。

### 2. 核心内容
现有单一大模型智能体在长程、分布外的真实软件工程问题上泛化能力差，且被迫在一条推理链中保留大量无关上下文。作者借鉴人类工程师的分工方式，将软件工程智能体建模为编排器，协调定位、编辑、验证等专用子智能体，并用基于赌博机的优化方法自动发现层级结构。实验表明该分层设计能提升在真实问题上的泛化与修复表现，为构建更稳健的自主编码智能体提供了新思路。

### 3. 对应检索需求
autonomous agents for coding tasks。

### 4. 来源与原文
- Source：ICLR-2026-Accepted
- OpenReview：[https://openreview.net/forum?id=O6stE173BD](https://openreview.net/forum?id=O6stE173BD)
