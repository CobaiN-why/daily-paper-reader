---
title: "SWE-Refactor: A Repository-Aware Benchmark for Evaluating LLMs on Real-World Code Refactoring"
title_zh: SWE-Refactor：面向真实世界代码重构的大模型评测仓库感知基准
authors: "Yisen Xu, Jinqiu Yang, Tse-Hsun Chen"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=caPQXR9eeJ"
tags: ["query:ai-se"]
score: 9.0
evidence: 评估大模型真实代码重构能力的基准
tldr: 现有代码重构基准多聚焦原子重构类型，且包含纠缠的无关改动、缺少仓库结构信息，难以准确评估大模型的真实重构能力。本文提出SWE-Refactor，一个仓库感知的真实世界代码重构评测基准，强调保留程序行为的同时改进结构。该基准覆盖更复杂的重构类型并提供仓库与结构上下文，使评测更贴近实际开发场景，为LLM在软件工程重构任务上的能力衡量提供了更可靠的工具。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 已有代码重构基准多聚焦原子类型、数据噪声大且缺少仓库结构信息，难以准确衡量大模型的真实重构能力。
method: 构建仓库感知的重构评测基准，纳入更复杂的重构类型，并提供代码仓库与结构信息以支撑贴近真实的评测。
result: 该基准能更干净地隔离重构相关改动并覆盖复杂重构，从而更准确地刻画大模型的重构表现。
conclusion: 为LLM在软件工程代码重构任务上的评估提供了更贴近真实开发、更可靠的基准工具。
---

## Abstract
Recent advances in Large Language Models (LLMs) have garnered significant attention for their applications in software engineering tasks. Among these tasks, code refactoring has its own unique challenges. Unlike code generation, refactoring requires precise changes that preserve program behavior while improving structure, making automated evaluation difficult. Existing refactoring benchmarks suffer from three key limitations: (1) they often focus on atomic refactoring types while missing more complex ones; (2) they contain noisy data with entangled, unrelated code changes, making it difficult to study LLM’s true refactoring capability accurately; and (3) they lack code repository and structural information to support realistic evaluations. To address these issues, we propose SWE-Refactor, a new benchmark for LLM-based code refactoring. SWE-Refactor contains 1,099 real-world, pure refactorings collected from 18 real-world Java projects. Each refactoring instance is verified through compilation, test execution, and automated refactoring detection tools to ensure correctness. Unlike prior benchmarks, SWERefactor covers both atomic and compound refactoring types (single and multiple code changes). It includes rich repository-level data (e.g., method callers and callees, class hierarchies), as well as configuration details like test coverage and build settings. We evaluate nine widely used LLMs on SWE-Refactor, including GPT-4o-mini, DeepSeek-V3, and CodeLLaMa. DeepSeek-V3 achieves the best performance with 457 successful refactorings (41.58%), followed by GPT-4o-mini with 438 (39.85%). DeepSeek-V3 performs particularly well on Extract Method, completing 301 cases, while GPT-4o-mini demonstrates stronger performance on more complex refactoring types, such as Move Method and Extract and Move Method. Furthermore, we find that adding retrieval context via few-shot examples and using a multi-agent workflow significantly improve performance, with the multi-agent approach achieving the highest success rate. We release SWE-Refactor and all evaluation results to support future research on LLM-based code refactoring.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
评估大模型真实代码重构能力的基准。

### 2. 核心内容
现有代码重构基准多聚焦原子重构类型，且包含纠缠的无关改动、缺少仓库结构信息，难以准确评估大模型的真实重构能力。本文提出SWE-Refactor，一个仓库感知的真实世界代码重构评测基准，强调保留程序行为的同时改进结构。该基准覆盖更复杂的重构类型并提供仓库与结构上下文，使评测更贴近实际开发场景，为LLM在软件工程重构任务上的能力衡量提供了更可靠的工具。

### 3. 对应检索需求
application of large language models to software engineering tasks such as code generation and defect detection。

### 4. 来源与原文
- Source：ICLR-2026-Rejected-Public
- OpenReview：[https://openreview.net/forum?id=caPQXR9eeJ](https://openreview.net/forum?id=caPQXR9eeJ)
