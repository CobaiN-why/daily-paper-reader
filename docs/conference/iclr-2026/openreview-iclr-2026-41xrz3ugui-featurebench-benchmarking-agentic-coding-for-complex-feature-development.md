---
title: "FeatureBench: Benchmarking Agentic Coding for Complex Feature Development"
title_zh: FeatureBench：面向复杂功能开发的智能体编码基准
authors: "Qixing Zhou, JiaCheng Zhang, Haiyang Wang, Rui Hao, Jiahe Wang, Minghao Han, Yuxue Yang, Shuzhe Wu, Feiyang Pan, Lue Fan, Dandan Tu, Zhaoxiang Zhang"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=41xrZ3uGuI"
tags: ["query:ai-se"]
score: 9.0
evidence: 面向大模型编码智能体复杂功能开发的基准
tldr: 现有编码智能体基准任务范围狭窄，多局限于单个PR内的缺陷修复，且评测不可执行或难以自动更新覆盖。本文提出FeatureBench，面向端到端、以功能为导向的软件开发，采用基于执行的评测协议与可扩展的覆盖更新机制。该基准能更全面刻画大模型编码智能体在真实开发场景中的能力边界，为改进智能体提供严格评测基础。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 现有编码智能体基准任务范围窄、评测不可执行且缺乏自动化覆盖更新，难以反映真实开发能力。
method: 构建FeatureBench基准，采用基于执行的评测协议与可扩展的自动化覆盖更新机制。
result: 该基准将评测扩展到端到端功能开发，更全面刻画智能体编码能力的边界。
conclusion: 为评估和改进大模型编码智能体在真实软件开发中的表现提供了严格而可扩展的基准。
---

## Abstract
Agents powered by large language models (LLMs) are increasingly adopted in the software industry, contributing code as collaborators or even autonomous developers. As their presence grows, it becomes important to assess the current boundaries of their coding abilities. Existing agentic coding benchmarks, however, cover a limited task scope, e.g., bug fixing within a single pull request (PR), and often rely on non-executable evaluations or lack an automated approach for continually updating the evaluation coverage.  To address such issues, we propose FeatureBench, a benchmark designed to evaluate agentic coding performance in end-to-end, feature-oriented software development. FeatureBench incorporates an execution-based evaluation protocol and a scalable test-driven method that automatically derives tasks from code repositories with minimal human effort. By tracing from unit tests along a dependency graph, our approach can identify feature-level coding tasks spanning multiple commits and PRs scattered across the development timeline, while ensuring the proper functioning of other features after the separation.  Using this framework, we curated 200 challenging evaluation tasks and 3825 executable environments from 24 open-source repositories in the first version of our benchmark. Empirical evaluation reveals that the state-of-the-art agentic model, such as Claude 4.5 Opus, which achieves a 74.4% resolved rate on SWE-bench, succeeds on only 11.0% of tasks, opening new opportunities for advancing agentic coding. Moreover, benefiting from our automated task collection toolkit, FeatureBench can be easily scaled and updated over time to mitigate data leakage. The inherent verifiability of constructed environments also makes our method potentially valuable for agent training.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
面向大模型编码智能体复杂功能开发的基准。

### 2. 核心内容
现有编码智能体基准任务范围狭窄，多局限于单个PR内的缺陷修复，且评测不可执行或难以自动更新覆盖。本文提出FeatureBench，面向端到端、以功能为导向的软件开发，采用基于执行的评测协议与可扩展的覆盖更新机制。该基准能更全面刻画大模型编码智能体在真实开发场景中的能力边界，为改进智能体提供严格评测基础。

### 3. 对应检索需求
autonomous agents for coding tasks。

### 4. 来源与原文
- Source：ICLR-2026-Accepted
- OpenReview：[https://openreview.net/forum?id=41xrZ3uGuI](https://openreview.net/forum?id=41xrZ3uGuI)
