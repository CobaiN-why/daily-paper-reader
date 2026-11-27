---
title: "CodeClash: Benchmarking Goal-Oriented Software Engineering"
title_zh: CodeClash：面向目标导向软件工程的基准评测
authors: "John Yang, Kilian Lieret, Joyce Yang, Carlos E. Jimenez, Muhtasham Oblokulov, Aryan Siddiqui, Ofir Press, Ludwig Schmidt, Diyi Yang"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf/adaf4beddd11a064ba21aa59d983c1fbafc2775b.pdf"
tags: ["query:ai-se"]
score: 8.0
evidence: 面向目标导向智能体软件工程的基准
tldr: 现有编码基准多评估修bug、写测试等界定明确的任务，难以反映真实开发中以高层目标驱动的迭代过程。作者提出CodeClash基准，让语言模型智能体在多轮锦标赛中反复编辑代码，并通过代码竞技场按目标进行对抗评比。该设定要求智能体在无明确指引下自主推进开放式目标。工作为评估目标导向的智能体软件工程能力提供了新基准。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 现有编码基准只考察修复缺陷、编写测试等狭窄明确任务，缺乏对开放式目标开发的评估。
method: 构建多轮锦标赛式基准，语言模型智能体迭代编辑代码，再由代码竞技场按目标进行对抗评判。
result: 该基准揭示了语言模型在无显式指引下迭代实现高层目标方面的能力与不足。
conclusion: 为衡量智能体式软件工程的目标导向开发能力提供了新的评测框架。
---

## Abstract
Existing coding benchmarks evaluate language models (LMs) on concrete, well-specified tasks such as fixing bugs or writing tests.
However, human programmers do not spend all day addressing isolated GitHub issues.
Instead, real-world software development is grounded in the pursuit of high-level goals.
Evaluating whether LMs can iteratively develop code to accomplish open-ended objectives without explicit guidance remains an open challenge.
We introduce CodeClash, a benchmark where LMs compete in multi-round tournaments to build the best codebase for achieving a competitive objective.
Each round proceeds in two parts: agents edit their code, then their codebases compete head-to-head in a code arena that determines winners based on objectives like score maximization, resource acquisition, or survival.
Models must decide for themselves how to improve their code both absolutely and against their opponents.
We run 1680 tournaments to evaluate 8 LMs across 6 arenas, revealing how models exhibit diverse development styles and share fundamental limitations in strategic reasoning.
Models also struggle with long-term codebase maintenance; repositories become progressively messy and redundant.
Top models lose every round against expert human programmers.
We open-source CodeClash to advance the study of autonomous, goal-oriented code development.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
面向目标导向智能体软件工程的基准。

### 2. 核心内容
现有编码基准多评估修bug、写测试等界定明确的任务，难以反映真实开发中以高层目标驱动的迭代过程。作者提出CodeClash基准，让语言模型智能体在多轮锦标赛中反复编辑代码，并通过代码竞技场按目标进行对抗评比。该设定要求智能体在无明确指引下自主推进开放式目标。工作为评估目标导向的智能体软件工程能力提供了新基准。

### 3. 对应检索需求
software engineering tasks and automation。

### 4. 来源与原文
- Source：ICML-2026-Accepted
- OpenReview：[https://openreview.net/forum?id=SW2D390ePP](https://openreview.net/forum?id=SW2D390ePP)
