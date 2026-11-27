---
title: "RegexPSPACE: A Benchmark for Evaluating LLM Reasoning on PSPACE-Complete Regex Problems"
title_zh: RegexPSPACE：评估大模型在PSPACE完全正则问题上推理能力的基准
authors: "Hyundong Jin, Joonghyuk Hahn, Yo-Sub Han"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=gu9yu4FTkI"
tags: ["query:ai-se"]
score: 5.0
evidence: 评估大模型在正则问题上推理极限的基准
tldr: 现有研究多聚焦NP类问题，难以刻画大模型在更高复杂度上的推理边界。本文提出RegexPSPACE基准，基于正则表达式等价判定与最小化两个PSPACE完全问题来系统评测大模型与大型推理模型。实验揭示了模型在有限上下文下的空间复杂度瓶颈，为理解大模型计算能力上限提供了更严格的标准。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 现有基准多局限于NP复杂度问题，难以严格刻画大模型推理的计算上限。
method: 构建基于正则等价判定与最小化两个PSPACE完全问题的基准来评测大模型推理。
result: 实验显示大模型在PSPACE完全问题上受上下文窗口带来的空间复杂度限制明显。
conclusion: 该基准为评估大模型计算能力提供了更严格的标准与新的分析视角。
---

## Abstract
Large language models (LLMs) show strong performance across natural language processing (NLP), mathematical reasoning, and programming, and recent large reasoning models (LRMs) further emphasize explicit reasoning. Yet their computational limits$\textemdash$particularly spatial complexity constrained by finite context windows$\textemdash$remain poorly understood. While recent works often focus on problems within the NP complexity class, we push the boundary by introducing a novel benchmark grounded in two PSPACE-complete regular expression (regex) problems: equivalence decision (RegexEQ) and minimization (RegexMin). PSPACE-complete problems serve as a more rigorous standard for assessing computational capacity, as their solutions require massive search space exploration. We perform a double-exponential space exploration to construct a labeled dataset of over a million regex instances with a sound filtering process to build the benchmark. We conduct extensive evaluations on 6 LLMs and 5 LRMs of varying scales, revealing common failure patterns such as verbosity and repetition. With its well-defined structure and quantitative evaluation metrics, this work presents the first empirical investigation into the spatial computational limitations of LLMs and LRMs, offering a new framework for evaluating their advanced reasoning capabilities.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
评估大模型在正则问题上推理极限的基准。

### 2. 核心内容
现有研究多聚焦NP类问题，难以刻画大模型在更高复杂度上的推理边界。本文提出RegexPSPACE基准，基于正则表达式等价判定与最小化两个PSPACE完全问题来系统评测大模型与大型推理模型。实验揭示了模型在有限上下文下的空间复杂度瓶颈，为理解大模型计算能力上限提供了更严格的标准。

### 3. 对应检索需求
large language models and their applications。

### 4. 来源与原文
- Source：ICLR-2026-Public
- OpenReview：[https://openreview.net/forum?id=gu9yu4FTkI](https://openreview.net/forum?id=gu9yu4FTkI)
