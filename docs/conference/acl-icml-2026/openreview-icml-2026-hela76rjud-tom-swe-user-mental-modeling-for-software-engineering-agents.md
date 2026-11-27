---
title: "TOM-SWE: User Mental Modeling For Software Engineering Agents"
title_zh: TOM-SWE：面向软件工程智能体的用户心智建模
authors: "Xuhui Zhou, Valerie Chen, Zora Zhiruo Wang, Graham Neubig, Maarten Sap, Xingyao Wang"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf/7109bbeb5c63adcf4bbcac412f871fc3b7f44e60.pdf"
tags: ["query:ai-se"]
score: 9.0
evidence: 面向软件工程编码智能体的双智能体架构
tldr: 现有编码智能体在指令欠明确或依赖上下文时难以推断并跟踪用户意图，导致任务执行偏差。作者提出ToM-SWE双智能体架构，将主软件工程智能体与轻量心智理论伙伴智能体配对，由后者从指令和历史交互中推断用户目标、约束与偏好并维护持久记忆。该伙伴智能体在保护隐私、控制上下文的同时向主智能体提供用户相关建议。工作为意图感知的自主编码智能体提供了新范式。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 编码智能体虽能规划、编辑与测试代码，但在指令含糊时难以推断和跟踪用户真实意图。
method: 提出双智能体架构，为主软件工程智能体配备轻量心智理论伙伴智能体，建模用户目标、约束与偏好并维护持久记忆。
result: 伙伴智能体在保护隐私和压缩上下文的前提下向主智能体提供用户相关建议，提升意图理解能力。
conclusion: 该架构为构建能理解用户意图的自主软件工程智能体提供了可复用的设计思路。
---

## Abstract
Recent advances in coding agents have made them capable of planning, editing, running, and testing complex code bases. Despite their growing ability in coding tasks, these systems still struggle to infer and track user intent, especially when instructions are underspecified or context-dependent. To bridge this gap, we introduce ToM-SWE, a dual-agent architecture that pairs a primary software-engineering (SWE) agent with a lightweight theory-of-mind (ToM) partner agent dedicated to modeling the user's mental state. The ToM agent infers user goals, constraints, and preferences from instructions and interaction history, maintains a persistent memory of the user, and provides user-related suggestions to the SWE agent, while preserving privacy and minimizing context window load. In two software engineering benchmarks (ambiguous SWE-bench and stateful SWE-bench), ToM-SWE improves task success rates and user satisfaction. Notably, on the stateful SWE benchmark, a newly introduced evaluation that provides agents with a user simulator along with previous interaction histories, ToM-SWE achieves a substantially higher task success rate of 59.7% compared to 18.1% for OpenHands, a state-of-the-art SWE agent. Furthermore, in a three-week study with professional developers using ToM-SWE in their daily work, participants found it better aligned with their intent and useful 86% of the time, underscoring the value of stateful user modeling for practical coding agents.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
面向软件工程编码智能体的双智能体架构。

### 2. 核心内容
现有编码智能体在指令欠明确或依赖上下文时难以推断并跟踪用户意图，导致任务执行偏差。作者提出ToM-SWE双智能体架构，将主软件工程智能体与轻量心智理论伙伴智能体配对，由后者从指令和历史交互中推断用户目标、约束与偏好并维护持久记忆。该伙伴智能体在保护隐私、控制上下文的同时向主智能体提供用户相关建议。工作为意图感知的自主编码智能体提供了新范式。

### 3. 对应检索需求
autonomous agents for coding tasks。

### 4. 来源与原文
- Source：ICML-2026-Accepted
- OpenReview：[https://openreview.net/forum?id=HeLa76rJuD](https://openreview.net/forum?id=HeLa76rJuD)
