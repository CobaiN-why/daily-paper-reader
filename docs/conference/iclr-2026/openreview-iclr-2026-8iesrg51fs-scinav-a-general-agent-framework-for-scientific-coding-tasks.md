---
title: "SciNav: A General Agent Framework for Scientific Coding Tasks"
title_zh: SciNav：面向科学编码任务的通用智能体框架
authors: "TIANSHU ZHANG, Huan Sun"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=8iEsrg51Fs"
tags: ["query:ai-se"]
score: 7.0
evidence: 面向科学编码任务的通用大模型智能体框架
tldr: 现有科学智能体多针对主观难评估的开放问题，而科学编码基准任务虽可客观评测，其智能体方法仍是工程化流程，缺乏原则性框架设计。本文提出SciNav，一个面向科学编码任务的端到端通用智能体框架。方法围绕可执行输出构建原则化流程，弥补了框架设计空白。该工作为自主编码智能体提供了可推广的体系结构。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 科学编码基准任务可客观评测，但现有智能体方法仍是工程化流程，缺乏原则性框架设计。
method: 提出SciNav端到端通用智能体框架，围绕可执行输出构建原则化的科学编码流程。
result: 在具有明确可执行输出的科学编码任务上实现了端到端、可客观评估的智能体方案。
conclusion: 该工作为自主编码智能体提供了可推广的原则性框架设计。
---

## Abstract
Autonomous science agents, built on large language models (LLMs), are increasingly being investigated to generate hypotheses, design experiments, and produce reports. Prior science agents primarily focus on open-ended scientific problems, where such outputs—hypotheses, experiments, or analyses are inherently subjective and thus difficult to evaluate rigorously. In contrast, existing scientific coding benchmarks provide tasks with clearly defined, executable outputs that enable objective assessment. However, current agent-based approaches to these benchmarks remain engineering-driven pipelines, lacking principled framework design. This mismatch exposes a gap: the absence of end-to-end, principled science agent frameworks for scientific coding tasks. We address this gap by focusing on scientific coding tasks, where evaluation can be made rigorously, and introducing an agent framework SciNav (Scientific Navigator) that enables more effective solution exploration. Our framework is designed to operate efficiently under constrained search budgets, moving beyond reliance on pre-defined success metrics and prolonged search cycles. Inspired by findings that comparative judgments often reveal finer-grained quality differences and therefore provide greater discriminative power than absolute scoring, our framework leverages pairwise relative judgments within a tree search process to select top-K promising solution branches, prune low-potential ones, and progressively narrow down the solution candidates on the selected branches guided by relative comparisons. We demonstrate our agent's effectiveness across different types of tasks on two benchmarks. Experiments show that SciNav significantly outperforms direct prompting and prior agents like OpenHands and Self-Debug across different base models, task types, and difficulty levels, and exceeds different frontier comparators such as random selection and LLM absolute scoring. These results confirm the strength of our agent design and highlight the effectiveness of relative judgment–guided top-K search for high-quality scientific coding, marking a step toward more practical science agents.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
面向科学编码任务的通用大模型智能体框架。

### 2. 核心内容
现有科学智能体多针对主观难评估的开放问题，而科学编码基准任务虽可客观评测，其智能体方法仍是工程化流程，缺乏原则性框架设计。本文提出SciNav，一个面向科学编码任务的端到端通用智能体框架。方法围绕可执行输出构建原则化流程，弥补了框架设计空白。该工作为自主编码智能体提供了可推广的体系结构。

### 3. 对应检索需求
autonomous agents for coding tasks。

### 4. 来源与原文
- Source：ICLR-2026-Accepted
- OpenReview：[https://openreview.net/forum?id=8iEsrg51Fs](https://openreview.net/forum?id=8iEsrg51Fs)
