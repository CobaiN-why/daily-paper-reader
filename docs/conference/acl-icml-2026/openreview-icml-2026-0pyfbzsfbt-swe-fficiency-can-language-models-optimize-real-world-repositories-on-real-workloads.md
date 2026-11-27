---
title: "SWE-fficiency: Can Language Models Optimize Real-World Repositories on Real Workloads?"
title_zh: SWE-fficiency：语言模型能否在真实工作负载上优化真实仓库？
authors: "Jeffrey Jian Ma, Milad Hashemi, Amir Yazdanbakhsh, Kevin Swersky, Ofir Press, Enhui Li, Vijay Janapa Reddi, Parthasarathy Ranganathan"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf/bf882cf5b4599415debce13b7f06ede8550eea57.pdf"
tags: ["query:ai-se"]
score: 8.0
evidence: 评估语言模型优化真实代码仓库的基准
tldr: 现有代码基准多关注修什么，而较少考察如何修，难以衡量真实的仓库级优化能力。本文提出 SWE-fficiency，一个面向真实工作负载的仓库级性能优化基准，包含跨九个常用数据科学与 HPC 仓库的 498 个任务，要求智能体理解代码语义、定位性能瓶颈并生成补丁。该基准要求补丁通过原有单元测试并达到专家级加速效果，为评估语言模型的软件工程能力提供了更严格的场景。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 现有基准侧重指出要修什么，缺少对仓库级性能优化过程与正确性的评估。
method: 构建 498 个跨九个真实仓库的优化任务，要求智能体定位瓶颈并生成通过测试的补丁。
result: 基准揭示语言模型在保持正确性的同时达到专家级加速仍具挑战。
conclusion: 该基准为评测语言模型的真实软件工程优化能力提供了严格场景。
---

## Abstract
Optimizing the performance of large-scale software repositories demands expertise in code reasoning and software engineering (SWE) to reduce runtime while preserving program correctness. However, most benchmarks emphasize what to fix rather than how to fix code. We introduce SWE-fficiency, a benchmark for evaluating repository-level performance optimization on real workloads. Our suite contains 498 tasks across nine widely used data-science, machine-learning, and HPC repositories (e.g., numpy, pandas, scipy): given a complete codebase and a slow workload, an agent must investigate code semantics, localize bottlenecks and relevant tests, and produce a patch that matches or exceeds expert speedup while passing the same unit tests. To enable this how-to-fix evaluation, our automated pipeline scrapes GitHub pull requests for performance-improving edits, combining keyword filtering, static analysis, coverage tooling, and execution validation to both confirm expert speedup baselines and identify relevant repository unit tests. Empirical evaluation of state-of-the-art agents reveals significant underperformance. On average, top agents achieve less than 0.23x the expert speedup: agents struggle in localizing optimization opportunities, reasoning about execution across functions, and maintaining correctness in proposed edits. We release the benchmark and accompanying data pipeline to facilitate research on automated performance engineering and long-horizon software reasoning.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
评估语言模型优化真实代码仓库的基准。

### 2. 核心内容
现有代码基准多关注修什么，而较少考察如何修，难以衡量真实的仓库级优化能力。本文提出 SWE-fficiency，一个面向真实工作负载的仓库级性能优化基准，包含跨九个常用数据科学与 HPC 仓库的 498 个任务，要求智能体理解代码语义、定位性能瓶颈并生成补丁。该基准要求补丁通过原有单元测试并达到专家级加速效果，为评估语言模型的软件工程能力提供了更严格的场景。

### 3. 对应检索需求
application of large language models to software engineering tasks such as code generation and defect detection。

### 4. 来源与原文
- Source：ICML-2026-Accepted
- OpenReview：[https://openreview.net/forum?id=0pyFbZSfbT](https://openreview.net/forum?id=0pyFbZSfbT)
