---
title: "SWE-Ext: Extending and Scaling Augmented Data for Repository-Level Coding Tasks"
title_zh: SWE-Ext：扩展与规模化面向仓库级编码任务的增强数据
authors: "Wei Li, Xin Zhang, Shaohang Wei, Yanjie Gao, Zhongxin Guo, Wen Luo, Feifan Song, Yangyu Huang, Houfeng Wang"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=HYQXJYzmFU"
tags: ["query:ai-se"]
score: 8.0
evidence: 扩展大模型仓库级编码任务训练数据
tldr: 仓库级基准显示大模型处理复杂软件工程任务仍具挑战，但现有训练数据局限于单语issue解决与功能实现。本文提出SWE-Ext，沿多语言覆盖与辅助代码补全两个维度扩展增强数据，覆盖10种语言。研究发现跨语言数据能提供可迁移信号，普遍增强单语环境下的定位与编辑能力，为提升仓库级编码能力提供数据基础。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 现有仓库级编码训练数据局限于单语issue解决与功能实现，制约大模型在复杂软件工程任务上的能力。
method: 提出SWE-Ext，沿多语言覆盖与辅助代码补全两个维度大规模扩展增强训练数据。
result: 实验揭示跨语言数据可提供可迁移信号，普遍增强单语设置下的定位与编辑能力。
conclusion: 为提升大模型仓库级编码能力提供了可扩展的多语言增强数据与方法洞见。
---

## Abstract
Repository-level benchmarks such as SWE-Bench have highlighted the challenges of scaling language models to complex software engineering tasks. However, current training data remains narrow in scope, primarily focusing on monolingual issue resolving and feature implementation. In this work, we introduce SWE-Ext, a large-scale effort to extend and scale augmented data for repository-level coding tasks. SWE-Ext broadens existing data along two key dimensions: multilingual coverage (spanning 10 languages) and an auxiliary code completion task. We uncover distinct transfer mechanisms: data from other programming languages provides transferable signals that generally enhance localization and editing capabilities in single-language (Python) settings, while code completion data strengthens code editing capabilities, particularly for feature implementation tasks requiring substantial new code generation. These extensions yield consistent improvements on Python repository-level benchmarks like SWE-Bench and FEA-Bench. Our method offers a simple yet effective way to leverage more open-source data for advancing repository-level code models.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
扩展大模型仓库级编码任务训练数据。

### 2. 核心内容
仓库级基准显示大模型处理复杂软件工程任务仍具挑战，但现有训练数据局限于单语issue解决与功能实现。本文提出SWE-Ext，沿多语言覆盖与辅助代码补全两个维度扩展增强数据，覆盖10种语言。研究发现跨语言数据能提供可迁移信号，普遍增强单语环境下的定位与编辑能力，为提升仓库级编码能力提供数据基础。

### 3. 对应检索需求
application of large language models to software engineering tasks such as code generation and defect detection。

### 4. 来源与原文
- Source：ICLR-2026-Public
- OpenReview：[https://openreview.net/forum?id=HYQXJYzmFU](https://openreview.net/forum?id=HYQXJYzmFU)
