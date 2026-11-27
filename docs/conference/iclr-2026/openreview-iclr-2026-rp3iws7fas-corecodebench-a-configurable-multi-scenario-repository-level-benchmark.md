---
title: "CoreCodeBench: A Configurable Multi-Scenario Repository-Level Benchmark"
title_zh: CoreCodeBench：可配置的多场景仓库级基准
authors: "Lingyue Fu, Hao Guan, Bolun Zhang, Haowei Yuan, Yaoming Zhu, Jun Xu, Lin Qiu, ZongYu Wang, Xuezhi Cao, Xunliang Cai, Weinan Zhang, Weiwen Liu, Yong Yu"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=rp3iWs7fAS"
tags: ["query:ai-se"]
score: 8.0
evidence: 多场景仓库级代码评测基准
tldr: 现有仓库级代码基准多聚焦代码生成或缺陷修复等单一场景，难以覆盖真实工程流程的多样性与复杂度，且生成测试可靠性不足、问题定位可控性差。本文提出全自动流水线CorePipe，将仓库转化为综合测试用例，并构建可配置的多场景仓库级基准CoreCodeBench。该工作为工程级代码大模型评测提供了更全面、可控的评测手段。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 现有仓库级基准场景单一、测试可靠性差且问题定位可控性不足，难以评估工程级代码能力。
method: 提出全自动流水线CorePipe将仓库转化为测试用例，并构建可配置多场景的CoreCodeBench基准。
result: 实现了覆盖多种工程场景、定位可控的仓库级代码大模型评测。
conclusion: 为工程级代码大模型提供了更全面可控的多场景评测基准。
---

## Abstract
As Large Language Models (LLMs) demonstrate increasingly sophisticated code processing capabilities, evaluating their performance on engineering-level code remains challenging. Existing repository-level benchmarks primarily focus on single scenarios, such as code generation or bug fixing, without adequately capturing the diversity and complexity of real-world software or project engineering workflows. Furthermore, these benchmarks suffer from limited controllability in question positioning and reliability issues in their generated test cases. To address these limitations, we present CorePipe, a fully automated pipeline that converts repositories into comprehensive test cases, and introduce CoreCodeBench, a configurable multi-scenario repository-level benchmark. To simulate real engineering scenarios, CorePipe generates three types of atomic questions (Development, BugFix, and Test-Driven Development) specifically targeting core code segments. These atomic questions are further combined into three types of composite questions, with difficulty levels flexibly adjusted through hyperparameter tuning. CoreCodeBench provides a comprehensive and extensive repository-level benchmark to investigate the applicability of LLMs in real-world engineering projects. Experiments with 16 LLMs across diverse scenarios reveal varying capabilities and offer multi-dimensional insights into LLM performance in engineering contexts. Code of CorePipe and data of CoreCodeBench are available.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
多场景仓库级代码评测基准。

### 2. 核心内容
现有仓库级代码基准多聚焦代码生成或缺陷修复等单一场景，难以覆盖真实工程流程的多样性与复杂度，且生成测试可靠性不足、问题定位可控性差。本文提出全自动流水线CorePipe，将仓库转化为综合测试用例，并构建可配置的多场景仓库级基准CoreCodeBench。该工作为工程级代码大模型评测提供了更全面、可控的评测手段。

### 3. 对应检索需求
application of large language models to software engineering tasks such as code generation and defect detection。

### 4. 来源与原文
- Source：ICLR-2026-Public
- OpenReview：[https://openreview.net/forum?id=rp3iWs7fAS](https://openreview.net/forum?id=rp3iWs7fAS)
