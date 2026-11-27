---
title: "CoDA-Bench: Can Code Agents Handle Data-Intensive Tasks?"
title_zh: CoDA-Bench：代码智能体能处理数据密集型任务吗？
authors: "Yuxin Zhang, Ju Fan, Meihao Fan, Shaolei Zhang, Xiaoyong Du"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf/1848ca3977492cbd7416933e3a72164906a481bb.pdf"
tags: ["query:ai-se"]
score: 8.0
evidence: 面向数据密集型任务的代码智能体评测基准
tldr: 现有代码智能体评测基准通常将代码能力与数据处理能力割裂评估，难以反映真实开发场景。本文提出 CoDA-Bench，基于 Kaggle 生态构建包含数百个数据集的数据密集型 Linux 沙箱，要求智能体主动探索复杂文件层级并完成任务。该基准首次联合评估代码与数据智能，为自主工程智能体提供了更贴近真实开发的衡量标准。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 现有基准把代码能力与数据能力分开评估，与真实开发场景存在明显差距。
method: 作者基于 Kaggle 生态构建数据密集型 Linux 沙箱，要求智能体主动探索文件系统完成任务。
result: 该基准首次在同一环境中联合评估代码智能与数据智能，揭示了现有智能体的能力缺口。
conclusion: CoDA-Bench 为自主工程智能体提供了更贴近真实开发的评测标准。
---

## Abstract
Advanced agents are increasingly demonstrating the potential to operate as autonomous engineers, creating a growing demand for evaluation benchmarks that capture the complexity of real-world development. Such environments typically involve both complex code and large-scale data (i.e., file system). However, existing benchmarks usually evaluate code-centric or data-centric capabilities in isolation, leaving a clear gap with real development scenarios. In this paper, we bridge this gap by introducing CoDA-Bench, the first benchmark to jointly evaluate code and data intelligence in a data-intensive environment. We construct a data-intensive Linux sandbox based on the Kaggle ecosystem (containing hundreds of datasets), where agents must actively explore complex file hierarchies to identify relevant resources and generate code for data-driven analytical tasks. CoDA-Bench comprises 1,009 tasks spanning 31 communities, with each task environment containing an average of 980 files, simulating realistic data scale and noise. Evaluations of advanced agents reveal that even top-performing systems struggle to effectively integrate data discovery with code execution, achieving a success rate of only 61.1\%. These results highlight a substantial gap in current agentic capabilities for data-intensive tasks and point to promising directions for future research.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
面向数据密集型任务的代码智能体评测基准。

### 2. 核心内容
现有代码智能体评测基准通常将代码能力与数据处理能力割裂评估，难以反映真实开发场景。本文提出 CoDA-Bench，基于 Kaggle 生态构建包含数百个数据集的数据密集型 Linux 沙箱，要求智能体主动探索复杂文件层级并完成任务。该基准首次联合评估代码与数据智能，为自主工程智能体提供了更贴近真实开发的衡量标准。

### 3. 对应检索需求
autonomous agents for coding tasks。

### 4. 来源与原文
- Source：ICML-2026-Accepted
- OpenReview：[https://openreview.net/forum?id=TUcgDjfdVk](https://openreview.net/forum?id=TUcgDjfdVk)
