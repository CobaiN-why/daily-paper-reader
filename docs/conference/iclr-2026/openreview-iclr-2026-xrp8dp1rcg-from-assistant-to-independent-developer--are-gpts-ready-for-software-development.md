---
title: From Assistant to Independent Developer — Are GPTs Ready for Software Development?
title_zh: 从助手到独立开发者——GPT能否胜任软件开发？
authors: "Dezhi Ran, Yuan Cao, Mengzhou Wu, Simin Chen, Yuzhe Guo, Jun Ren, Zihe Song, Hao Yu, Jialei Wei, Linyi Li, Wei Yang, Baishakhi Ray, Tao Xie"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=XrP8dp1rCg"
tags: ["query:ai-se"]
score: 9.0
evidence: 评估大模型从规格构建完整软件系统的基准
tldr: 大模型在函数级代码生成上表现优异，但真实应用需要跨组件编排与全生命周期一致性，现有基准难以评估这种能力。本文提出包含101个真实安卓应用开发问题的基准，给定自然语言功能规格要求模型从零构建完整软件系统。该工作揭示了从函数级助手到独立开发者之间的差距，为大模型软件工程能力评估提供了更贴近实际的测试平台。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 现有基准只评估函数级代码生成，无法衡量模型构建完整软件系统的能力。
method: 构建包含101个真实安卓应用开发问题的基准，从自然语言规格生成完整系统。
result: 该基准暴露了模型在系统级组件编排与状态一致性上的明显不足。
conclusion: 为大模型从函数级走向系统级软件开发的能力评估提供了贴近实际的平台。
---

## Abstract
Large language models (LLMs) have demonstrated remarkable capability in function-level code generation tasks. 
Unlike isolated functions, real-world applications demand reasoning over the entire software system: developers must orchestrate how different components interact, maintain consistency across states over time, and ensure the application behaves correctly within the lifecycle and framework constraints. Yet, no existing benchmark adequately evaluates whether LLMs can bridge this gap and construct entire software systems from scratch.

To address this gap, we propose \tool, a benchmark consisting of 101 software development problems drawn from real-world Android apps. Given a natural language specification detailing the app functionality, a language model is tasked with \textbf{implementing the functionality into an Android app from scratch}. Developing an Android app from scratch requires understanding and coordinating app states, lifecycle management, and asynchronous operations, calling for LLMs to generate context-aware, robust, and maintainable code. To construct \tool, we design a multi-agent system to automatically summarize the main functionalities from app documents and navigate the app to synthesize test cases validating the functional correctness of app implementation. Following rigorous manual verification by Android development experts, \tool incorporates the test cases within an automated evaluation framework that enables reproducible assessment without human intervention, making it easily adoptable for future research. Our evaluation on 12 flagship LLMs show that all evaluated models achieve low effectiveness, with the best-performing model (GPT-5) developing only 18.8\% functionally correct applications, highlighting fundamental limitations in current models' ability to handle complex, multi-component software engineering challenges.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
评估大模型从规格构建完整软件系统的基准。

### 2. 核心内容
大模型在函数级代码生成上表现优异，但真实应用需要跨组件编排与全生命周期一致性，现有基准难以评估这种能力。本文提出包含101个真实安卓应用开发问题的基准，给定自然语言功能规格要求模型从零构建完整软件系统。该工作揭示了从函数级助手到独立开发者之间的差距，为大模型软件工程能力评估提供了更贴近实际的测试平台。

### 3. 对应检索需求
application of large language models to software engineering tasks such as code generation and defect detection。

### 4. 来源与原文
- Source：ICLR-2026-Accepted
- OpenReview：[https://openreview.net/forum?id=XrP8dp1rCg](https://openreview.net/forum?id=XrP8dp1rCg)
