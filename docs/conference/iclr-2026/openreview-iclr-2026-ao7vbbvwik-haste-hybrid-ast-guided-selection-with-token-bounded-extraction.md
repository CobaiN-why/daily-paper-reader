---
title: "HASTE: Hybrid AST-guided Selection with Token-bounded Extraction"
title_zh: HASTE：结合AST引导选择与令牌受限抽取的混合方法
authors: "Mitali Raj, Saish Bhorpe, Mushtaq saeed, Adam Labaran Mohammed"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=ao7VBbvWIK"
tags: ["query:ai-se"]
score: 8.0
evidence: 面向大模型软件工程自动化的AST引导上下文检索
tldr: 大模型虽有望自动化缺陷修复与大规模重构等软件工程任务，但受限的上下文窗口使代码检索面临结构完整性与语义相关性之间的取舍。作者提出HASTE，将基于抽象语法树的结构感知选择与令牌受限的抽取相结合，在保留关键结构依赖的同时定位最相关代码。该方法缓解了上下文截断导致的幻觉与不连贯问题，为LLM驱动的软件工程任务提供了通用上下文构建方案。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 大模型上下文窗口有限，代码检索在结构完整性与语义相关性之间难以兼顾。
method: 提出HASTE，将AST引导的结构感知选择与令牌受限抽取结合以构建连贯上下文。
result: 该方法在保留结构依赖的同时定位相关代码，缓解了幻觉与代码不连贯问题。
conclusion: 为LLM驱动的缺陷修复与重构等软件工程任务提供了通用的上下文构建方案。
---

## Abstract
The rise of Large Language Models (LLMs) has opened new frontiers in software engineering, promising to automate complex tasks from bug fixing to large-scale refactoring. However, this promise is critically hampered by a fundamental constraint: the limited context window of these models. This limitation forces a difficult trade-off in context retrieval. On one hand, structure-aware approaches preserve syntactic integrity but often fail to pinpoint the most semantically relevant code for a given task. On the other, relevance-focused techniques excel at finding pertinent snippets but risk severing critical structural dependencies, leading to incoherent code that causes LLMs to hallucinate.

To resolve this trade-off, we introduce HASTE (Hybrid AST-guided Selection with Token-bounded Extraction), a novel framework that synergistically integrates robust information retrieval with deep structural analysis. HASTE leverages the Abstract Syntax Tree (AST), combining lexical and semantic search to ensure the extracted code is not only topically relevant but also structurally coherent and executable. Our evaluation, conducted using a robust LLM-as-a-judge framework, demonstrates that HASTE achieves upto 85% code compression while significantly improving the success rate of automated code edits and maintaining high structural fidelity, thereby reducing model-generated hallucinations. HASTE represents a key step towards enabling reliable and scalable AI-assisted software development.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
面向大模型软件工程自动化的AST引导上下文检索。

### 2. 核心内容
大模型虽有望自动化缺陷修复与大规模重构等软件工程任务，但受限的上下文窗口使代码检索面临结构完整性与语义相关性之间的取舍。作者提出HASTE，将基于抽象语法树的结构感知选择与令牌受限的抽取相结合，在保留关键结构依赖的同时定位最相关代码。该方法缓解了上下文截断导致的幻觉与不连贯问题，为LLM驱动的软件工程任务提供了通用上下文构建方案。

### 3. 对应检索需求
software engineering tasks and automation。

### 4. 来源与原文
- Source：ICLR-2026-Public
- OpenReview：[https://openreview.net/forum?id=ao7VBbvWIK](https://openreview.net/forum?id=ao7VBbvWIK)
