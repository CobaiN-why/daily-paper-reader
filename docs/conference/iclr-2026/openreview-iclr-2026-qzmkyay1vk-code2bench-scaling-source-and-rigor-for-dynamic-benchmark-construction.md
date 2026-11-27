---
title: "Code2Bench: Scaling Source and Rigor for Dynamic Benchmark Construction"
title_zh: Code2Bench：面向动态基准构建的来源与严格度扩展
authors: "Zhe Zhang, Runlin Liu, Aishan Liu, Xingyu Liu, Xiang Gao, Hailong Sun"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=QZmKyAy1VK"
tags: ["query:ai-se"]
score: 8.0
evidence: 用于严格评估代码生成大模型的动态基准
tldr: "评估代码生成大模型受制于静态易污染的题目来源与低严格度的测试。本文提出Dual Scaling基准构建理念，从动态真实代码库持续扩展题目来源，并用自动化高覆盖的属性测试提升测试严格度。CODE2BENCH以作用域图分析进行依赖分类，并设100%分支覆盖质量门槛，为代码生成模型提供更严谨、可持续更新的评测。"
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 代码生成大模型评测依赖静态易污染题目与低严格度测试，难以反映真实能力。
method: 提出Dual Scaling理念并用CODE2BENCH实现，结合作用域图分析与属性测试及分支覆盖门槛。
result: 通过动态真实仓库扩展题目来源并以高覆盖属性测试提升严格度，构建可持续更新基准。
conclusion: 为代码生成大模型提供更严谨、抗污染且可扩展的评测框架。
---

## Abstract
The evaluation of code-generating Large Language Models (LLMs) is fundamentally constrained by two intertwined challenges: a reliance on static, easily contaminated problem sources and the use of superficial, low-rigor testing. This paper introduces a new benchmark construction philosophy, Dual Scaling, designed to systematically address both limitations. Our approach involves continuously
scaling the source of problems from dynamic, real-world code repositories and systematically scaling the rigor of tests via automated, high-coverage Property-Based Testing (PBT). We instantiate this philosophy in CODE2BENCH, an end-to-end framework that leverages Scope Graph analysis for principled dependency classification and a 100% branch coverage quality gate to ensure test suite integrity.
Using this framework, we construct CODE2BENCH-2509, a new benchmark suite with native instances in both Python and Java. Our extensive evaluation of 10 state-of-the-art LLMs on CODE2BENCH-2509, powered by a novel "diagnostic
fingerprint" visualization, yields three key insights: (1) models exhibit a fundamental performance gap, excelling at API application (Weakly Self-Contained tasks) but struggling with algorithmic synthesis (Self-Contained tasks); (2) a model’s
performance is profoundly shaped by the target language’s ecosystem, a nuance we are the first to systematically quantify; and (3) our rigorous, scaled testing is critical in uncovering an "illusion of correctness" prevalent in simpler benchmarks. Our work presents a robust, scalable, and diagnostic paradigm for the next generation of LLM evaluation in software engineering. The code, data, and results are available at https://code2bench.github.io/.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
用于严格评估代码生成大模型的动态基准。

### 2. 核心内容
评估代码生成大模型受制于静态易污染的题目来源与低严格度的测试。本文提出Dual Scaling基准构建理念，从动态真实代码库持续扩展题目来源，并用自动化高覆盖的属性测试提升测试严格度。CODE2BENCH以作用域图分析进行依赖分类，并设100%分支覆盖质量门槛，为代码生成模型提供更严谨、可持续更新的评测。

### 3. 对应检索需求
application of large language models to software engineering tasks such as code generation and defect detection。

### 4. 来源与原文
- Source：ICLR-2026-Accepted
- OpenReview：[https://openreview.net/forum?id=QZmKyAy1VK](https://openreview.net/forum?id=QZmKyAy1VK)
