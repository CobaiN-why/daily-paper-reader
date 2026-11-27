---
title: "PLSEMANTICSBENCH: LARGE LANGUAGE MODELS AS PROGRAMMING LANGUAGE INTERPRETERS"
title_zh: PLSEMANTICSBENCH：作为编程语言解释器的大语言模型
authors: "Aditya Thimmaiah, Jiyang Zhang, Jayanth Srinivasa, Junyi Jessy Li, Milos Gligoric"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=D4k9TdOAun"
tags: ["query:ai-se"]
score: 6.0
evidence: 评估大模型能否依据形式语义充当编程语言解释器
tldr: 随着大模型在代码推理上表现出色，一个自然的问题是：能否仅依据编程语言的形式语义让模型执行程序。作者以C子集IMP为对象，用小型步进操作语义与K语义形式化，构建了人工编写、模型翻译与模糊生成三类难度可控的评测集。研究系统考察了大模型作为编程语言解释器的能力与局限，为代码理解与新语言快速原型提供了评估基础。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 探究大模型能否仅依据形式语义执行程序，以支持新语言快速原型。
method: 以IMP语言和SOS、K语义形式化为对象，构建难度可控的三类评测集考察模型解释能力。
result: 研究系统评估了大模型作为编程语言解释器的能力与局限。
conclusion: 该基准为代码理解和新语言特性原型提供了有价值的评估基础。
---

## Abstract
As large language models (LLMs) excel at code reasoning, a natural question
arises: can an LLM execute programs (i.e., act as an interpreter) purely based on a
programming language’s formal semantics? If so, it will enable rapid prototyping
of new programming languages and language features. We study this question using
the imperative language IMP (a subset of C), formalized via small-step operational
semantics (SOS) and rewriting-based operational semantics (K-semantics). We
introduce three evaluation sets—Human-Written, LLM-Translated, and Fuzzer-
Generated-whose difficulty is controlled by code-complexity metrics spanning
the size, control-flow, and data-flow axes. Given a program and its semantics
formalized with SOS/K-semantics, models are evaluated on three tasks ranging
from coarse to fine: (1) final-state prediction, (2) semantic rule prediction, and (3)
execution trace prediction. To distinguish pretraining memorization from semantic
competence, we define two nonstandard semantics obtained through systematic
mutations of the standard rules. Across strong code/reasoning LLMs, performance
drops under nonstandard semantics despite high performance under the standard
one. We further find that (i) there are patterns to different model failures, (ii) most
reasoning models perform exceptionally well on coarse grained tasks involving
reasoning about highly complex programs often containing nested loop depths
beyond five, and surprisingly, (iii) providing formal semantics helps on simple
programs but often hurts on more complex ones. Overall, the results show a
promise that LLMs could serve as programming language interpreters, but points
to the lack of their robust semantics understanding.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
评估大模型能否依据形式语义充当编程语言解释器。

### 2. 核心内容
随着大模型在代码推理上表现出色，一个自然的问题是：能否仅依据编程语言的形式语义让模型执行程序。作者以C子集IMP为对象，用小型步进操作语义与K语义形式化，构建了人工编写、模型翻译与模糊生成三类难度可控的评测集。研究系统考察了大模型作为编程语言解释器的能力与局限，为代码理解与新语言快速原型提供了评估基础。

### 3. 对应检索需求
application of large language models to software engineering tasks such as code generation and defect detection。

### 4. 来源与原文
- Source：ICLR-2026-Rejected-Public
- OpenReview：[https://openreview.net/forum?id=D4k9TdOAun](https://openreview.net/forum?id=D4k9TdOAun)
