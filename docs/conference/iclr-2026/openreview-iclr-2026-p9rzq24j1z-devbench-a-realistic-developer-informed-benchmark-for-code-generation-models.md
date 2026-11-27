---
title: "DevBench: A Realistic, Developer-Informed Benchmark for Code Generation Models"
title_zh: DevBench：面向代码生成模型的真实开发者驱动基准
authors: "Pareesa Ameneh Golnari, Adarsh Kumarappan, Wen Wen, Xiaoyu Liu, Gabriel Ryan, Yuting Sun, Shengyu Fu, Elsie Nallipogu"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=P9RZQ24j1z"
tags: ["query:ai-se"]
score: 8.0
evidence: 基于遥测数据评估大模型真实代码补全的基准
tldr: 现有代码生成基准常缺乏生态效度且易受训练数据污染。本文提出DevBench，一个由开发者遥测驱动的真实代码补全基准，覆盖六种语言、六类任务共1800个评测实例，结合功能正确性、相似度与LLM评判指标。对9个先进模型的评估揭示了其在语法精度、语义推理与实用价值上的差异，为代码生成模型提供了更贴近真实的诊断工具。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 现有代码生成基准缺乏生态效度且易受训练数据污染。
method: 构建基于开发者遥测的1800实例基准，结合正确性、相似度与LLM评判评估。
result: 评估9个先进模型，揭示其在语法、语义与实用性上的差异。
conclusion: 为代码生成模型提供了更贴近真实场景的诊断性评测基准。
---

## Abstract
DevBench is a telemetry-driven benchmark designed to evaluate Large Language Models (LLMs) on realistic code completion tasks. It includes 1,800 evaluation instances across six programming languages and six task categories derived from real developer telemetry, such as API usage and code purpose understanding. Unlike prior benchmarks, it emphasizes ecological validity, avoids training data contamination, and enables detailed diagnostics. The evaluation combines functional correctness, similarity-based metrics, and LLM-judge assessments focused on usefulness and contextual relevance. 9 state-of-the-art models were assessed, revealing differences in syntactic precision, semantic reasoning, and practical utility. Our benchmark provides actionable insights to guide model selection and improvement—detail that is often missing from other benchmarks but is essential for both practical deployment and targeted model development.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
基于遥测数据评估大模型真实代码补全的基准。

### 2. 核心内容
现有代码生成基准常缺乏生态效度且易受训练数据污染。本文提出DevBench，一个由开发者遥测驱动的真实代码补全基准，覆盖六种语言、六类任务共1800个评测实例，结合功能正确性、相似度与LLM评判指标。对9个先进模型的评估揭示了其在语法精度、语义推理与实用价值上的差异，为代码生成模型提供了更贴近真实的诊断工具。

### 3. 对应检索需求
application of large language models to software engineering tasks such as code generation and defect detection。

### 4. 来源与原文
- Source：ICLR-2026-Rejected-Public
- OpenReview：[https://openreview.net/forum?id=P9RZQ24j1z](https://openreview.net/forum?id=P9RZQ24j1z)
