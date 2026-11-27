---
title: "FormulaCode: Evaluating Agentic Optimization on Large Codebases"
title_zh: FormulaCode：评估大代码库上的智能体优化
authors: "Atharva Sehgal, James Hou, Akanksha Sarkar, Ishaan Mantripragada, Swarat Chaudhuri, Jennifer J. Sun, Yisong Yue"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf/f8b7bf5adfff48909d3dc49fd7e1fd6ffdbf20ef.pdf"
tags: ["query:ai-se"]
score: 8.0
evidence: 评估LLM编码智能体在大代码库优化的基准
tldr: 现有代码基准多依赖合成任务、二值正确性或单目标评估，难以衡量编码智能体在真实大代码库上的整体优化能力。FormulaCode从GitHub科学计算仓库挖掘957个性能瓶颈，配以专家补丁与社区性能负载，构建多目标细粒度评测基准。实验揭示智能体在仓库级优化上的表现与不足，为更真实的智能体评估提供工具。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 现有代码基准依赖合成任务与单目标信号，难评估真实代码库的整体优化。
method: 从GitHub仓库挖掘性能瓶颈，配以专家补丁和社区负载构建多目标评测基准。
result: 基准包含957个瓶颈及大量性能负载，揭示智能体优化的能力与局限。
conclusion: 该基准为仓库级编码智能体优化能力提供更真实的评估手段。
---

## Abstract
Large language model (LLM) coding agents increasingly operate at the repository level, motivating benchmarks that evaluate their ability to optimize entire codebases under realistic constraints. Existing code benchmarks largely rely on synthetic tasks, binary correctness signals, or single-objective evaluation, limiting their ability to assess holistic optimization behavior. We introduce FormulaCode, a benchmark for evaluating agentic optimization on large, real-world codebases with fine-grained, multi-objective performance metrics. FormulaCode comprises 957 performance bottlenecks mined from scientific Python repositories on GitHub, each paired with expert-authored patches and 264.6 community-maintained performance workloads per task, enabling evaluation of the full optimization lifecycle—triage, diagnosis, and resolution—under realistic correctness and performance constraints. Our evaluations reveal that repository-scale, multi-objective optimization remains a major challenge for frontier LLM agents.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
评估LLM编码智能体在大代码库优化的基准。

### 2. 核心内容
现有代码基准多依赖合成任务、二值正确性或单目标评估，难以衡量编码智能体在真实大代码库上的整体优化能力。FormulaCode从GitHub科学计算仓库挖掘957个性能瓶颈，配以专家补丁与社区性能负载，构建多目标细粒度评测基准。实验揭示智能体在仓库级优化上的表现与不足，为更真实的智能体评估提供工具。

### 3. 对应检索需求
autonomous agents for coding tasks。

### 4. 来源与原文
- Source：ICML-2026-Accepted
- OpenReview：[https://openreview.net/forum?id=WArbqRUsAe](https://openreview.net/forum?id=WArbqRUsAe)
