---
title: "SWE-PolyBench: A multi-language benchmark for repository level evaluation of coding agents"
title_zh: SWE-PolyBench：面向编码智能体仓库级评测的多语言基准
authors: "Muhammad Shihab Rashid, Christian Bock, Yuan Zhuang, Alexander Buchholz, Timothy B Esler, Simon Valentin, Luca Franceschi, Martin Wistuba, Prabhu Teja S, Woojung Kim, Anoop Deoras, Giovanni Zappella, Laurent Callot"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=n577FC6CKk"
tags: ["query:ai-se"]
score: 9.0
evidence: 面向大模型编码智能体的多语言仓库级评测基准
tldr: 大模型编码智能体能力出众，但跨语言、真实场景下的评测仍具挑战。本文提出SWE-PolyBench，涵盖21个仓库共2110个实例，覆盖Java、JavaScript、TypeScript与Python，任务包含缺陷修复、功能新增与代码重构，并提供基于执行的评测框架及验证子集。该基准支持多语言仓库级自动化评估，便于系统比较编码智能体在真实软件工程任务上的表现。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 编码智能体虽表现优异，但缺乏跨多种编程语言与真实场景的仓库级评测手段。
method: 构建SWE-PolyBench多语言基准，含2110个实例、验证子集及基于执行的评测框架。
result: 覆盖四种语言与缺陷修复、功能新增、重构等任务，实现多语言仓库级自动化评测。
conclusion: 为编码智能体在多样化真实软件工程任务上的比较评估提供了统一的多语言基准。
---

## Abstract
Coding agents powered by large language models have shown impressive capabilities in software engineering tasks, but evaluating their performance across diverse programming languages and real-world scenarios remains challenging. We introduce SWE-PolyBench, a new multi-language benchmark for repository-level, execution-based evaluation of coding agents. SWE-PolyBench contains 2110 instances from 21 repositories and includes tasks in Java, JavaScript, TypeScript and Python, covering bug fixes, feature additions, and code refactoring. We provide a verified subset of 384 instances(SWE-PolyBench_Verified), a task and repository-stratified subsample of 500 instances (SWE-PolyBench500) and release an evaluation harness allowing for fully automated evaluation. We further introduce novel instance stratifications and retrieval metrics rooted in syntax tree analysis to deepen the understanding of coding agent performances. Our experiments with leading open-source coding agents on SWE-PolyBench show that current agents exhibit uneven performances across languages and struggle with complex problems, while showing higher performance on simpler tasks. SWE-PolyBench aims to drive progress in developing more versatile and robust AI coding assistants for real-world software engineering

---

## 论文详细总结（自动生成）

### 1. 检索相关性
面向大模型编码智能体的多语言仓库级评测基准。

### 2. 核心内容
大模型编码智能体能力出众，但跨语言、真实场景下的评测仍具挑战。本文提出SWE-PolyBench，涵盖21个仓库共2110个实例，覆盖Java、JavaScript、TypeScript与Python，任务包含缺陷修复、功能新增与代码重构，并提供基于执行的评测框架及验证子集。该基准支持多语言仓库级自动化评估，便于系统比较编码智能体在真实软件工程任务上的表现。

### 3. 对应检索需求
autonomous agents for coding tasks。

### 4. 来源与原文
- Source：ICLR-2026-Rejected-Public
- OpenReview：[https://openreview.net/forum?id=n577FC6CKk](https://openreview.net/forum?id=n577FC6CKk)
