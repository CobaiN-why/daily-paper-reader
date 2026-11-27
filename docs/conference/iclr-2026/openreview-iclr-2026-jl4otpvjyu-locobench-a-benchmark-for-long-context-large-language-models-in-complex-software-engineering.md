---
title: "LoCoBench: A Benchmark for Long-Context Large Language Models in Complex Software Engineering"
title_zh: LoCoBench：面向复杂软件工程的长上下文大模型基准
authors: "Jielin Qiu, Zuxin Liu, Zhiwei Liu, Rithesh R N, Jianguo Zhang, Haolin Chen, Shiyu Wang, Ming Zhu, Liangwei Yang, Juntao Tan, Zhepeng Cen, Cheng Qian, Shelby Heinecke, Weiran Yao, Silvio Savarese, Caiming Xiong, Huan Wang"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=jl4OtPVjYU"
tags: ["query:ai-se"]
score: 8.0
evidence: 面向复杂软件工程任务的长上下文大模型基准
tldr: 百万级上下文窗口为大模型理解代码与软件开发评估带来新可能，但现有基准多局限于单函数或短上下文任务。作者提出LoCoBench，覆盖整库理解、跨文件推理与架构一致性等能力，包含1万到100万令牌、10种语言的8000个场景。该基准可精确测量长上下文性能随规模增长的退化，为复杂软件工程场景下的大模型评估提供了系统工具。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 现有代码基准多聚焦单函数或短上下文，难以评估真实复杂开发任务。
method: 构建覆盖整库理解、跨文件推理与架构一致性的长上下文基准，含多语言多规模场景。
result: 该基准可精确测量长上下文模型随规模增长的性能退化。
conclusion: 为复杂软件工程场景下大模型的长上下文能力评估提供了系统工具。
---

## Abstract
The rise of long-context language models with million-token windows opens new possibilities for advanced code understanding and software development evaluation. We propose LoCoBench, a benchmark designed to assess long-context LLMs on realistic, complex development tasks. Unlike existing benchmarks centered on single-function or short-context tasks, LoCoBench targets capabilities like whole-codebase understanding, cross-file reasoning, and architectural consistency in large systems. It offers 8,000 scenarios across 10 languages, with context lengths from 10K to 1M tokens, enabling precise measurement of long-context performance degradation. LoCoBench spans 8 task categories, architectural understanding, cross-file refactoring, multi-session development, bug investigation, feature implementation, code comprehension, integration testing, and security analysis. Built through a 5-phase pipeline, it produces diverse, high-quality scenarios requiring reasoning over large codebases. We introduce a comprehensive evaluation framework with 17 metrics across 4 dimensions including 6 new evaluation metrics: Architectural Coherence Score, Dependency Traversal Accuracy, Cross-File Reasoning Depth, Incremental Development Capability, Information Coverage Utilization, Multi-Session Memory Retention, combined into a unified LoCoBench Score (LCBS). Evaluations of state-of-the-art models reveal substantial performance gaps, underscoring long-context software development as a critical challenge.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
面向复杂软件工程任务的长上下文大模型基准。

### 2. 核心内容
百万级上下文窗口为大模型理解代码与软件开发评估带来新可能，但现有基准多局限于单函数或短上下文任务。作者提出LoCoBench，覆盖整库理解、跨文件推理与架构一致性等能力，包含1万到100万令牌、10种语言的8000个场景。该基准可精确测量长上下文性能随规模增长的退化，为复杂软件工程场景下的大模型评估提供了系统工具。

### 3. 对应检索需求
software engineering tasks and automation。

### 4. 来源与原文
- Source：ICLR-2026-Public
- OpenReview：[https://openreview.net/forum?id=jl4OtPVjYU](https://openreview.net/forum?id=jl4OtPVjYU)
