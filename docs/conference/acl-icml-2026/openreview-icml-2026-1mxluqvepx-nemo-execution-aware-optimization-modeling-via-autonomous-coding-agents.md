---
title: "NEMO: Execution-Aware Optimization Modeling via Autonomous Coding Agents"
title_zh: NEMO：通过自主编码智能体实现执行感知的优化建模
authors: "Yang Song, Anoushka Vyas, Zirui Wei, Sina Khoshfetrat Pakazad, Henrik Ohlsson, Graham Neubig"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf/eaafad01c645f13aea55a2acf38421321edc09dd.pdf"
tags: ["query:ai-se"]
score: 9.0
evidence: 自主编码智能体将自然语言转化为可执行代码
tldr: 现有方法依赖专用大模型或定制智能体，常生成语法错误或不可执行的代码。NEMO将自主编码智能体作为一等抽象，借助沙箱执行保证代码可运行，并引入非对称验证循环实现自动校验与修复。系统把自然语言决策问题转化为可执行数学优化实现，显著提升正确性与鲁棒性，为智能体驱动的代码生成提供了新范式。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 现有大模型或定制智能体生成优化代码时常出现语法错误和不可执行问题。
method: 将自主编码智能体作为一等抽象，用沙箱执行保障可运行，并设计非对称验证循环进行自动校验与修复。
result: 系统能把自然语言决策问题稳定转化为可执行优化实现并自动修复错误。
conclusion: 表明以执行约束为核心的编码智能体可显著提升代码生成可靠性。
---

## Abstract
We present **NEMO**, a system that translates **N**atural-language descriptions of decision problems into formal **E**xecutable **M**athematical **O**ptimization implementations using autonomous coding agents (ACAs). Existing approaches rely on specialized large language models (LLMs) or bespoke task-specific agents that are often brittle and frequently generate syntactically invalid or non-executable code. NEMO instead treats ACAs as a first-class abstraction analogous to API-based interaction with LLMs; their sandboxed execution guarantees code is executable by construction and supports automated validation and repair. We introduce novel coordination patterns including asymmetric validation loops between independently generated optimizer and simulator implementations, external memory for experience reuse, and robustness enhancements via minimum Bayes risk (MBR) decoding and self-consistency. Across nine established optimization benchmarks, NEMO achieves state-of-the-art performance on the majority of tasks with substantial margins on several datasets, demonstrating the power of execution-aware agentic architectures for automated optimization modeling.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
自主编码智能体将自然语言转化为可执行代码。

### 2. 核心内容
现有方法依赖专用大模型或定制智能体，常生成语法错误或不可执行的代码。NEMO将自主编码智能体作为一等抽象，借助沙箱执行保证代码可运行，并引入非对称验证循环实现自动校验与修复。系统把自然语言决策问题转化为可执行数学优化实现，显著提升正确性与鲁棒性，为智能体驱动的代码生成提供了新范式。

### 3. 对应检索需求
autonomous agents for coding tasks。

### 4. 来源与原文
- Source：ICML-2026-Accepted
- OpenReview：[https://openreview.net/forum?id=1MxluQVepx](https://openreview.net/forum?id=1MxluQVepx)
