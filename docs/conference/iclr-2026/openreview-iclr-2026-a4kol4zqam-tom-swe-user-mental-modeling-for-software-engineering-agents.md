---
title: "TOM-SWE: User Mental Modeling For Software Engineering Agents"
title_zh: ToM-SWE：面向软件工程智能体的用户心智建模
authors: "Xuhui Zhou, Valerie Chen, Zora Zhiruo Wang, Graham Neubig, Maarten Sap, Xingyao Wang"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=A4koL4Zqam"
tags: ["query:ai-se"]
score: 9.0
evidence: 为软件工程智能体建模用户意图的双智能体架构
tldr: 编码智能体已能规划、编辑、运行与测试复杂代码库，但在指令欠明确或依赖上下文时仍难以推断并跟踪用户意图。本文提出ToM-SWE双智能体架构，为主软件工程智能体配备轻量的心智理论伙伴智能体。该伙伴从指令与交互历史推断用户目标、约束与偏好并维护持久记忆，在保护隐私前提下向主智能体提供建议。工作提升了编码智能体对用户意图的理解能力。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 编码智能体在指令欠明确或依赖上下文时难以推断并跟踪用户意图。
method: 提出双智能体架构，为主软件工程智能体配备轻量的心智理论伙伴智能体来建模用户目标与偏好。
result: 伙伴智能体维护用户持久记忆并提供建议，提升了对欠明确指令的处理能力。
conclusion: 该工作改善了软件工程智能体对用户意图的理解与跟踪。
---

## Abstract
Recent advances in coding agents have made them capable of planning, editing, running, and testing complex code bases. Despite their growing ability in coding tasks, these systems still struggle to infer and track user intent, especially when instructions are underspecified or context-dependent. To bridge this gap, we introduce ToM-SWE, a dual-agent architecture that pairs a primary software-engineering (SWE) agent with a lightweight theory-of-mind (ToM) partner agent dedicated to modeling the user's mental state. The ToM agent infers user goals, constraints, and preferences from instructions and interaction history, maintains a persistent memory of the user, and provides user-related suggestions to the SWE agent, while preserving privacy and minimizing context window load. In two software engineering benchmarks (ambiguous SWE-bench and stateful SWE-bench), ToM-SWE improves task success rates and user satisfaction. Notably, on the stateful SWE benchmark, a newly introduced evaluation that provides agents with a user simulator along with previous interaction histories, ToM-SWE achieves a substantially higher task success rate of 59.7% compared to 18.1% for OpenHands, a state-of-the-art SWE agent. Furthermore, in a three-week study with professional developers using ToM-SWE in their daily work, participants found it better aligned with their intent and useful 86% of the time, underscoring the value of stateful user modeling for practical coding agents.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
为软件工程智能体建模用户意图的双智能体架构。

### 2. 核心内容
编码智能体已能规划、编辑、运行与测试复杂代码库，但在指令欠明确或依赖上下文时仍难以推断并跟踪用户意图。本文提出ToM-SWE双智能体架构，为主软件工程智能体配备轻量的心智理论伙伴智能体。该伙伴从指令与交互历史推断用户目标、约束与偏好并维护持久记忆，在保护隐私前提下向主智能体提供建议。工作提升了编码智能体对用户意图的理解能力。

### 3. 对应检索需求
autonomous agents for coding tasks。

### 4. 来源与原文
- Source：ICLR-2026-Rejected-Public
- OpenReview：[https://openreview.net/forum?id=A4koL4Zqam](https://openreview.net/forum?id=A4koL4Zqam)
