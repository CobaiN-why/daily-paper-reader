---
title: "Ambig-SWE: Interactive Agents to Overcome Underspecificity in Software Engineering"
title_zh: Ambig-SWE：用交互式代理克服软件工程中的欠明确性
authors: "Sanidhya Vijayvargiya, Xuhui Zhou, Akhila Yerukola, Maarten Sap, Graham Neubig"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=X2yzXtH4wp"
tags: ["query:ai-se"]
score: 8.0
evidence: 大模型代理在交互式代码生成中处理欠明确指令
tldr: AI代理常基于欠明确的用户指令自动化任务，但擅自假设或缺乏澄清会带来风险。本文提出Ambig-SWE，系统评测开源与专有大模型代理在交互式代码生成中检测欠明确性、提出针对性澄清问题并利用交互改进表现的能力。结果显示模型在这些环节仍显吃力，凸显了面向软件工程任务的自主编码代理在澄清与交互方面的改进需求。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 代理处理欠明确指令时擅自假设或缺乏澄清会带来风险与资源浪费。
method: 构建交互式代码生成评测，考察检测欠明确性、提问澄清与利用交互三步能力。
result: 实验显示模型在检测欠明确性和有效澄清方面仍存在明显不足。
conclusion: 为面向软件工程的自主编码代理交互能力改进指明了方向。
---

## Abstract
AI agents are increasingly being deployed to automate tasks, often based on underspecified user instructions. Making unwarranted assumptions to compensate for the missing information and failing to ask clarifying questions can lead to suboptimal outcomes, safety risks due to tool misuse, and wasted computational resources. In this work, we study the ability of LLM agents to handle underspecified instructions in interactive code generation settings by evaluating proprietary and open-weight models on their performance across three key steps: (a) detecting underspecificity, (b) asking targeted clarification questions, and (c) leveraging the interaction to improve performance in underspecified scenarios. Our findings reveal that models struggle to distinguish between well-specified and underspecified instructions. However, when models interact for underspecified inputs, they effectively obtain vital information from the user leading to significant improvements in performance, up to 74\% over the non-interactive settings, underscoring the value of effective interaction. Our study highlights critical gaps in how current state-of-the-art models handle missing information in complex software engineering tasks and structures the evaluation into distinct steps to enable targeted improvements.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
大模型代理在交互式代码生成中处理欠明确指令。

### 2. 核心内容
AI代理常基于欠明确的用户指令自动化任务，但擅自假设或缺乏澄清会带来风险。本文提出Ambig-SWE，系统评测开源与专有大模型代理在交互式代码生成中检测欠明确性、提出针对性澄清问题并利用交互改进表现的能力。结果显示模型在这些环节仍显吃力，凸显了面向软件工程任务的自主编码代理在澄清与交互方面的改进需求。

### 3. 对应检索需求
autonomous agents for coding tasks。

### 4. 来源与原文
- Source：ICLR-2026-Accepted
- OpenReview：[https://openreview.net/forum?id=X2yzXtH4wp](https://openreview.net/forum?id=X2yzXtH4wp)
