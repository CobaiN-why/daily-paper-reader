---
title: Refactoring Codebases Through Library Design
title_zh: 通过库设计重构代码库
authors: "Žiga Kovačič, Justin T Chiu, Celine Lee, Wenting Zhao, Kevin Ellis"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=INXrtaUeGR"
tags: ["query:ai-se"]
score: 8.0
evidence: 代码智能体将代码库重构为可复用库设计
tldr: 随着代码智能体被用于解决孤立的一次性编程问题，如何让其重构代码以支持复用与可维护性成为关键挑战。本文先通过渐近分析和人类研究，发现最小描述长度最符合开发者对重构质量的偏好，随后提出MiniCode基准（要求将多文件重构为共享库）和Librarian方法。该工作为评估和提升代码智能体的库级重构能力提供了基准与方法。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 代码智能体常用于解决孤立的一次性编程问题，如何重构代码以支持复用与可维护性成为关键挑战。
method: 通过渐近分析和人类研究确定最小描述长度契合重构质量偏好，并提出MiniCode基准与Librarian重构方法。
result: 研究揭示了开发者对重构质量的偏好，并提供了可评估多文件重构为共享库能力的基准与方法。
conclusion: 为评估和提升代码智能体的库级重构能力提供了理论依据、基准和方法。
---

## Abstract
Maintainable and general software allows developers to build robust applications efficiently, yet achieving these qualities often requires refactoring specialized solutions into reusable components. This challenge becomes particularly relevant as code agents become used to solve isolated one-off programming problems. We investigate code agents' capacity to refactor code in ways that support growth and reusability. We first investigate what makes a good refactoring, finding via asymptotics analysis and a human study that Minimum Description Length best aligns with developer preferences for code refactoring quality. We then present both a benchmark and a method for refactoring: MiniCode, a benchmark where multiple files must be refactored into a shared library, and Librarian, a sample-and-rerank method for generating reusable libraries. We compare Librarian to state-of-the-art library generation methods, and study it on real-world code bases.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
代码智能体将代码库重构为可复用库设计。

### 2. 核心内容
随着代码智能体被用于解决孤立的一次性编程问题，如何让其重构代码以支持复用与可维护性成为关键挑战。本文先通过渐近分析和人类研究，发现最小描述长度最符合开发者对重构质量的偏好，随后提出MiniCode基准（要求将多文件重构为共享库）和Librarian方法。该工作为评估和提升代码智能体的库级重构能力提供了基准与方法。

### 3. 对应检索需求
autonomous agents for coding tasks。

### 4. 来源与原文
- Source：ICLR-2026-Rejected-Public
- OpenReview：[https://openreview.net/forum?id=INXrtaUeGR](https://openreview.net/forum?id=INXrtaUeGR)
