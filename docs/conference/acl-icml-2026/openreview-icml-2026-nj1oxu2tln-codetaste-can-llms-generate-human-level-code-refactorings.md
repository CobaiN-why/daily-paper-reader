---
title: "CodeTaste: Can LLMs Generate Human-Level Code Refactorings?"
title_zh: CodeTaste：大模型能否生成人类水平的代码重构？
authors: "Alex Thillen, Niels Mündler, Veselin Raychev, Martin Vechev"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf/c622859abc38f62a0691615ec0af6bbcf5506b13.pdf"
tags: ["query:ai-se"]
score: 9.0
evidence: 面向大模型编码代理的代码重构基准
tldr: 大模型编码代理虽能生成可用代码，却常引入复杂度、重复与架构债务，而重构是人工应对这些问题的关键手段。作者构建了CodeTaste基准，从大型多文件开源重构中挖掘任务，并用仓库测试套件衡量功能正确性、用基于数据流推理的静态检查验证代码模式变化。实验评估代理能否可靠执行重构并识别开发者真实选择的重构，揭示其与人类水平的差距。该工作为代码生成与软件维护类任务提供了更贴近真实工程的评测基础。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 大模型生成的代码常积累复杂度和重复，需要重构来改善结构，但代理能否可靠执行重构尚不清楚。
method: 构建从多文件开源重构中挖掘的基准，结合仓库测试套件与基于数据流推理的定制静态检查进行评分。
result: 实验显示代理在重构执行与识别人类实际选择的重构上仍有明显差距。
conclusion: 该基准为评估编码代理的代码质量改进能力提供了贴近真实工程的测试手段。
---

## Abstract
LLM coding agents can generate working code, but their solutions often accumulate complexity, duplication, and architectural debt. Human developers address such issues through refactoring: behavior-preserving program transformations that improve structure and maintainability. We investigate whether agents (i) can execute refactorings reliably and (ii) identify the refactorings that human developers actually chose in real codebases.
To this end, we construct CodeTaste, a benchmark mined from large multi-file open-source refactorings. To score solutions, we combine repository test suites that measure functional correctness with tailored static checks that verify removal of undesired and introduction of desired code patterns using dataflow reasoning.
Our results show a clear gap: agents perform well at implementing refactorings that are specified in detail, but often fail to discover the human refactoring choices when given a focus area for changes. A propose-then-implement decomposition improves alignment, and selecting the best-aligned proposal before implementation can yield further gains. CodeTaste provides an evaluation target and a potential preference signal for aligning coding agents with human refactoring decisions in realistic codebases. We release the benchmark, leaderboard, and code.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
面向大模型编码代理的代码重构基准。

### 2. 核心内容
大模型编码代理虽能生成可用代码，却常引入复杂度、重复与架构债务，而重构是人工应对这些问题的关键手段。作者构建了CodeTaste基准，从大型多文件开源重构中挖掘任务，并用仓库测试套件衡量功能正确性、用基于数据流推理的静态检查验证代码模式变化。实验评估代理能否可靠执行重构并识别开发者真实选择的重构，揭示其与人类水平的差距。该工作为代码生成与软件维护类任务提供了更贴近真实工程的评测基础。

### 3. 对应检索需求
application of large language models to software engineering tasks such as code generation and defect detection。

### 4. 来源与原文
- Source：ICML-2026-Accepted
- OpenReview：[https://openreview.net/forum?id=nj1oXU2tln](https://openreview.net/forum?id=nj1oXU2tln)
