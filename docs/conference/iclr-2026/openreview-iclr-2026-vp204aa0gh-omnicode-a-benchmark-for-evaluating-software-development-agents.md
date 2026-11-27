---
title: "OmniCode: A Benchmark for Evaluating Software Development Agents"
title_zh: OmniCode：面向软件开发智能体评测的基准
authors: "Atharv Sonwane, Eng-Shen Tu, Claas Beger, Wei-Chung Lu, Carter Larsen, Debjit Dhar, Simon Alford, Rachel Chen, Ronit Pattanayak, Tuan Anh Dang, Guohao Chen, Gloria Geng, Kevin Ellis, Saikat Dutta"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=VP204Aa0gH"
tags: ["query:ai-se"]
score: 9.0
evidence: 覆盖测试生成等多样任务的软件开发智能体基准
tldr: 现有编码基准如HumanEval和SWE-Bench多局限于竞赛编程与补丁生成，难以反映真实开发的多样任务。本文提出OmniCode，涵盖代码评审响应、测试生成、风格违规修复与程序修复等多类软件工程任务。该基准能更严格地评估大模型驱动的开发智能体在广泛真实任务上的能力，推动更全面的编码智能体研究。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 现有编码基准任务过于狭窄，无法反映工程师在真实开发中承担的多样软件工程任务。
method: 提出OmniCode基准，包含代码评审响应、测试生成、风格修复与程序修复等多类任务。
result: 基准覆盖更广泛的软件工程任务类别，可更严格评估开发智能体的综合能力。
conclusion: 为推进更贴近真实开发的编码智能体研究提供了多样化任务评测基础。
---

## Abstract
LLM-powered coding agents are redefining how real-world software is developed.
To drive the research towards better coding agents, we require challenging bench-
marks that can rigorously evaluate the ability of such agents to perform various
software engineering tasks. However, popular coding benchmarks such as Hu-
manEval and SWE-Bench focus on narrowly scoped tasks such as competition
programming and patch generation. In reality, software engineers have to handle
a broader set of tasks for real-world software development. To address this gap,
we propose OmniCode, a novel software engineering benchmark that contains a
diverse set of task categories, including responding to code reviews, test generation,
fixing style violations, and program repair. Overall, OmniCode contains 2912 tasks
in Python, 728 tasks per category.
In contrast to prior software engineering benchmarks, the tasks in OmniCode are
(1) manually validated to eliminate ill-defined problems, and (2) synthetically
crafted or recently curated to avoid data leakage issues, presenting a new frame-
work for synthetically generating diverse software tasks from limited real world
data. We evaluate OmniCode with popular agent frameworks such as SWE-Agent,
demonstrating shortcomings on tasks that differ from bug-fixing. For instance,
SWE-Agent with Gemini 2.5 Flash obtains 14.0 % on test generation and 8.1 %
on fixing style issues. With OmniCode, our aim is to spur the development of
agents that can perform well across a broader spectrum of software development
processes.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
覆盖测试生成等多样任务的软件开发智能体基准。

### 2. 核心内容
现有编码基准如HumanEval和SWE-Bench多局限于竞赛编程与补丁生成，难以反映真实开发的多样任务。本文提出OmniCode，涵盖代码评审响应、测试生成、风格违规修复与程序修复等多类软件工程任务。该基准能更严格地评估大模型驱动的开发智能体在广泛真实任务上的能力，推动更全面的编码智能体研究。

### 3. 对应检索需求
coding agents for automated test generation and documentation。

### 4. 来源与原文
- Source：ICLR-2026-Public
- OpenReview：[https://openreview.net/forum?id=VP204Aa0gH](https://openreview.net/forum?id=VP204Aa0gH)
