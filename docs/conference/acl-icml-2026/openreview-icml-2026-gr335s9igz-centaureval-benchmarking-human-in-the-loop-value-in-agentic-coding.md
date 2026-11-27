---
title: "CentaurEval: Benchmarking Human-in-the-Loop Value in Agentic Coding"
title_zh: CentaurEval：评测代理式编码中人机协同的价值
authors: "Hanjun Luo, Chiming Ni, Jiaheng Wen, Zhimu Huang, Bingduo Liao, Sylvia Chung, Yiran Wang, Yingbin Jin, Jialin Li, Xinfeng Li, Wenyuan Xu, XiaoFeng Wang, Hanan Salam"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf/13aec4ba474a032a82684cae1c4385467f906f35.pdf"
tags: ["query:ai-se"]
score: 9.0
evidence: 面向人机协同编码代理的评测基准
tldr: 大模型编码代理正在重塑开发范式，但传统面向人类的测试与面向模型的基准都无法衡量人机协同的价值，因为它们排除了需要人类推理引导与AI高效实现相结合的问题。作者提出CentaurEval，其核心是只有通过有效协作才能解决的协同必要型问题模板，可动态实例化45类任务，并为人类提供标准IDE、为模型提供450项可复现任务工具包。实验对多种代理进行评测，揭示协同带来的增益。该基准为智能软件工程中的人机协作提供了生态有效的评测手段。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 现有测试与基准无法刻画人机协同编码的价值，缺少只有协作才能解决的问题设定。
method: 设计协同必要型问题模板并动态实例化任务，为人类提供IDE、为大模型提供可复现任务工具包。
result: 在45类模板与450项任务上评测多种代理，量化了人机协同带来的性能增益。
conclusion: 该基准为智能软件工程中编码代理的人机协作研究提供了生态有效的评测框架。
---

## Abstract
LLM-powered coding agents are reshaping the development paradigm. However, existing evaluation systems, neither traditional tests for humans nor benchmarks for LLMs, fail to capture this shift, excluding problems that require both human reasoning to guide solutions and AI efficiency for implementation. We introduce CentaurEval, a unified, ecologically valid benchmark for measuring human-in-the-loop value in coding. CentaurEval's core innovation is its "Collaboration-Necessary" problem templates, which are intractable for standalone LLMs or humans, but solvable through effective collaboration. CentaurEval dynamically instantiates tasks from 45 templates, providing a standardized IDE for humans and a reproducible 450-task toolkit for LLMs. We benchmark 45 participants against 5 LLMs under 4 levels of human intervention. Results show that while LLMs or humans alone achieve poor pass rates (0.67% and 18.89%), human–AI collaboration significantly improves to 31.11%. Our analysis reveals an emerging co-reasoning partnership, challenging the traditional human-tool hierarchy by showing that strategic breakthroughs can originate from either humans or AI.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
面向人机协同编码代理的评测基准。

### 2. 核心内容
大模型编码代理正在重塑开发范式，但传统面向人类的测试与面向模型的基准都无法衡量人机协同的价值，因为它们排除了需要人类推理引导与AI高效实现相结合的问题。作者提出CentaurEval，其核心是只有通过有效协作才能解决的协同必要型问题模板，可动态实例化45类任务，并为人类提供标准IDE、为模型提供450项可复现任务工具包。实验对多种代理进行评测，揭示协同带来的增益。该基准为智能软件工程中的人机协作提供了生态有效的评测手段。

### 3. 对应检索需求
autonomous agents for coding tasks。

### 4. 来源与原文
- Source：ICML-2026-Accepted
- OpenReview：[https://openreview.net/forum?id=GR335S9IgZ](https://openreview.net/forum?id=GR335S9IgZ)
