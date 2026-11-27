---
title: "CATArena: Evaluating Evolutionary Capabilities of Code Agents via Iterative Tournaments"
title_zh: CATArena：通过迭代锦标赛评测代码代理的进化能力
authors: "Lingyue Fu, Xin Ding, Linyue Pan, Yaoming Zhu, Shao Zhang, Lin Qiu, Xuezhi Cao, Xunliang Cai, Jiaxin Ding, Weiwen Liu, Weinan Zhang, Yong Yu"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf/b0ecee835bb12ab78de71038956558f31bb6af07.pdf"
tags: ["query:ai-se"]
score: 8.0
evidence: 评测代码代理多轮进化能力的框架
tldr: 现有大模型代码代理评测多聚焦单轮生成可用代码，无法反映持续优化与多轮迭代开发的能力。作者提出CATArena框架，让代理在多轮锦标赛中基于执行反馈通过自我反思与同伴学习不断改进代码，并设计双指标体系统计静态生成能力与进化潜力。实验表明代理的进化潜力与单轮生成水平并不一致，揭示了两者的差异。该工作为自主编码代理的持续优化能力评估提供了新方法。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 现有代码代理评测局限于单轮功能生成，无法衡量持续优化与多轮迭代开发能力。
method: 构建多轮锦标赛框架，代理通过自我反思与同伴学习改进代码，并用双指标解耦生成能力与进化潜力。
result: 实验显示代理的进化潜力与单轮生成水平存在明显差异。
conclusion: 该框架为自主编码代理持续优化能力的评测提供了可复用方案。
---

## Abstract
Current evaluation for Large Language Model (LLM) code agents predominantly focus on generating functional code in single-turn scenarios, which fails to evaluate the agent's capability for continuous code optimization and multi-turn iterative development. To bridge this gap, we introduce CATArena, a framework designed to evaluate the evolutionary capabilities of code agents via iterative tournaments. Agents engage in multi-turn tournaments and continuously refine their code through self-reflection and peer-learning based on comprehensive execution feedback. For evaluation, we propose a dual-metric system to decouple static generation proficiency from evolutionary potential. Extensive experiments reveal that an agent's evolutionary potential is not strictly correlated with its initial proficiency. Our analysis further reveals that current agents struggle to concurrently leverage both peer-learning and self-reflection for effective performance gains. Furthermore, the results validate CATArena's high extensibility and resistance to variance tasks, establishing it as a continuous and reliable standard for assessing the evolutionary capability of LLM code agents.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
评测代码代理多轮进化能力的框架。

### 2. 核心内容
现有大模型代码代理评测多聚焦单轮生成可用代码，无法反映持续优化与多轮迭代开发的能力。作者提出CATArena框架，让代理在多轮锦标赛中基于执行反馈通过自我反思与同伴学习不断改进代码，并设计双指标体系统计静态生成能力与进化潜力。实验表明代理的进化潜力与单轮生成水平并不一致，揭示了两者的差异。该工作为自主编码代理的持续优化能力评估提供了新方法。

### 3. 对应检索需求
autonomous agents for coding tasks。

### 4. 来源与原文
- Source：ICML-2026-Accepted
- OpenReview：[https://openreview.net/forum?id=913g1X1YAW](https://openreview.net/forum?id=913g1X1YAW)
