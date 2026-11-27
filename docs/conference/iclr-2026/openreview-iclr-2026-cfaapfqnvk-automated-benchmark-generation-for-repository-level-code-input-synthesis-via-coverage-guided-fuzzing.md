---
title: Automated Benchmark Generation for Repository-Level Code Input Synthesis via Coverage-Guided Fuzzing
title_zh: 通过覆盖率引导模糊测试自动生成仓库级代码输入合成基准
authors: "Siwei Wei, Yuqi Guo, Yan Cai"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=CFaapfQnVk"
tags: ["query:ai-se"]
score: 8.0
evidence: 面向仓库级测试输入生成的大模型评测基准
tldr: 现有软件工程基准多依赖人工编写的issue、补丁和单元测试，规模受限且存在训练语料泄漏风险。本文提出TTG-GEN，利用覆盖率引导的模糊测试从真实代码库自动生成定向测试输入生成问题，要求大模型合成能执行指定代码位置的输入字节序列。该框架可规模化构建贴近调试场景的评测任务，更真实地考察大模型的仓库级测试与缺陷定位能力。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 现有仓库级测试基准依赖人工数据，规模有限且存在解法泄漏风险，难以可靠评估大模型的软件工程能力。
method: 提出TTG-GEN框架，用覆盖率引导模糊测试从真实代码库自动生成定向测试输入生成问题。
result: 生成的评测任务要求模型合成能命中指定代码位置的输入，贴近工程师调试实践并规避数据泄漏。
conclusion: 该自动化基准生成方法可规模化评估大模型在仓库级测试与调试任务上的真实能力。
---

## Abstract
Evaluating the capabilities of large language models (LLMs) on practical, repository-level testing tasks is crucial for their effective application in software engineering. Many existing benchmarks rely on human-authored data such as issues, patches, and unit tests, which can limit scalability and introduce risks of solution leakage from training corpora. We introduce TTG-GEN, an automated
framework for generating targeted test-input generation (TTG) problems from real-world codebases, in which LLMs are tasked with synthesizing input byte sequences to execute specific, designated code locations. These problems are representative of tasks performed by software engineers during debugging and are designed to probe an LLM’s understanding of complex control and data flow
in real-world scenarios. TTG-GEN leverages coverage-guided fuzzing (CGF) to identify reachable yet non-trivial target locations that require structure-aware inputs to cover. By automatically generating TTG problems, TTG-GEN offers a practical, scalable, and continuously updatable framework with a low risk of direct solution leakage, suited for evaluating repository-level code comprehension.
Using TTG-GEN, we construct TTG-BENCH-LITE, a benchmark of 500 such problems derived from 16 foundational C/C++ software projects. Our evaluation across retrieval-based and agent-based settings shows that even the most capable LLMs solve only 15% of these problems on their first attempt. This indicates that comprehending and manipulating program behavior at the repository level
remains a significant hurdle for current models, highlighting a substantial gap between their current abilities and the proficiency required for complex software engineering tasks.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
面向仓库级测试输入生成的大模型评测基准。

### 2. 核心内容
现有软件工程基准多依赖人工编写的issue、补丁和单元测试，规模受限且存在训练语料泄漏风险。本文提出TTG-GEN，利用覆盖率引导的模糊测试从真实代码库自动生成定向测试输入生成问题，要求大模型合成能执行指定代码位置的输入字节序列。该框架可规模化构建贴近调试场景的评测任务，更真实地考察大模型的仓库级测试与缺陷定位能力。

### 3. 对应检索需求
application of large language models to software engineering tasks such as code generation and defect detection。

### 4. 来源与原文
- Source：ICLR-2026-Rejected-Public
- OpenReview：[https://openreview.net/forum?id=CFaapfQnVk](https://openreview.net/forum?id=CFaapfQnVk)
