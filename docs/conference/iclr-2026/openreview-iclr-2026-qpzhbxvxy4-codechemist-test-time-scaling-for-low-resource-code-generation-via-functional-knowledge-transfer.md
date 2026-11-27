---
title: "CodeChemist: Test-Time Scaling for Low-Resource Code Generation via Functional Knowledge Transfer"
title_zh: CodeChemist：通过功能知识迁移实现低资源代码生成的测试时扩展
authors: "KaiXin Wang, Tianlin Li, Xiaoyu Zhang, Aishan Liu, Xianglong Liu, Ziqi Liu, Zhiqiang Zhang, JUN ZHOU, Bin Shi"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=qpZhbxVXY4"
tags: ["query:ai-se"]
score: 9.0
evidence: 通过功能知识迁移的代码生成测试时扩展
tldr: 代码大模型在不同编程语言上的表现差异明显，低资源语言因数据稀缺而生成质量不佳。本文提出CodeChemist，一个简单有效的测试时扩展框架：先在高资源语言上生成并执行代码以获得捕获功能知识的测试用例，再通过多温度对冲采样为低资源语言生成候选并筛选。实验表明该方法能显著提升低资源语言的代码生成表现，增强了代码大模型的整体可用性。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 代码大模型在低资源编程语言上因数据稀缺而性能不佳，限制了其整体可用性。
method: 提出CodeChemist测试时扩展框架，在高资源语言上生成执行代码获得测试用例，再经多温度对冲采样为低资源语言筛选候选。
result: 该方法有效提升了低资源编程语言的代码生成质量，缩小了跨语言性能差距。
conclusion: 为提升代码大模型在低资源语言上的生成能力提供了一种无需训练的高效方案。
---

## Abstract
Code Large Language Models (CodeLLMs) have been widely adopted for code generation, powering applications with large user bases.
Their performance, however, varies sharply across programming languages (PLs) and is particularly suboptimal for low-resource PLs due to data scarcity, limiting their overall usability. In this work, we introduce CodeChemist, a simple yet effective test-time scaling framework that transfers the model's functional knowledge from high-resource to low-resource PLs via synthesized test cases.
Specifically, CodeChemist first performs code generation and execution in high-resource PLs to derive test cases that capture functional knowledge, then applies multi-temperature hedged sampling to produce candidate code snippets in the low-resource PL, and finally selects the best candidate by executing the synthesized test cases. Extensive experiments demonstrate that CodeChemist significantly outperforms existing test-time scaling methods, improving code generation for low-resource PLs without retraining.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
通过功能知识迁移的代码生成测试时扩展。

### 2. 核心内容
代码大模型在不同编程语言上的表现差异明显，低资源语言因数据稀缺而生成质量不佳。本文提出CodeChemist，一个简单有效的测试时扩展框架：先在高资源语言上生成并执行代码以获得捕获功能知识的测试用例，再通过多温度对冲采样为低资源语言生成候选并筛选。实验表明该方法能显著提升低资源语言的代码生成表现，增强了代码大模型的整体可用性。

### 3. 对应检索需求
application of large language models to software engineering tasks such as code generation and defect detection。

### 4. 来源与原文
- Source：ICLR-2026-Rejected-Public
- OpenReview：[https://openreview.net/forum?id=qpZhbxVXY4](https://openreview.net/forum?id=qpZhbxVXY4)
