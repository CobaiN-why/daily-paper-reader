---
title: "Holistic Agent Leaderboard: The Missing Infrastructure for AI Agent Evaluation"
title_zh: 整体智能体排行榜：AI智能体评测缺失的基础设施
authors: "Sayash Kapoor, Benedikt Stroebl, Peter Kirgis, Nitya Nadgir, Zachary S Siegel, Boyi Wei, Tianci Xue, Ziru Chen, Felix Chen, Saiteja Utpala, Franck Ndzomga, Dheeraj Oruganty, Sophie Luskin, Kangheng Liu, Botao Yu, Amit Arora, Dongyoon Hahm, Harsh Trivedi, Huan Sun, Juyong Lee, Tengjun Jin, Yifan Mai, Yifei Zhou, Yuxuan Zhu, Rishi Bommasani, Daniel Kang, Dawn Song, Peter Henderson, Yu Su, Percy Liang, Arvind Narayanan"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=vUaY1t64ZZ"
tags: ["query:ai-se"]
score: 7.0
evidence: 面向含编码任务在内的AI智能体的标准化评测框架
tldr: AI智能体评测存在实现错误多、耗时长、结论不一致等问题，影响对智能体真实能力的判断。本文提出Holistic Agent Leaderboard标准化评测框架，可在数百台虚拟机上并行编排评测，并进行模型、脚手架与基准的三维分析。作者在9个模型与9个基准上完成两万余次智能体运行验证其有效性，为编码等任务中的智能体评测提供了可靠基础设施。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 现有AI智能体评测存在耗时长、实现错误多、结论不可靠等问题。
method: 提出标准化评测框架，跨虚拟机并行编排并在模型、脚手架与基准三维度分析。
result: 在9个模型和9个基准上完成两万余次智能体运行，验证了框架的有效性。
conclusion: 该工作为编码等任务中的智能体评测提供了可靠、可扩展的基础设施。
---

## Abstract
AI agents have been developed for complex real-world tasks from coding to customer service. But AI agent evaluations suffer from many challenges that undermine our understanding of how well agents really work (Figure 1). We introduce the Holistic Agent Leaderboard (HAL) to address these challenges. We make three main contributions. First, we provide a standardized evaluation harness that orchestrates parallel evaluations across hundreds of VMs, reducing evaluation time from weeks to hours while eliminating common implementation bugs. Second, we conduct three-dimensional analysis spanning models, scaffolds, and benchmarks. We validate the harness by conducting 21,730 agent rollouts across 9 models and 9 benchmarks in coding, web navigation, science, and customer service with a total cost of about $40,000. Our analysis reveals surprising insights, such as higher reasoning effort reducing accuracy in the majority of runs. Third, we use LLM-aided log inspection to uncover previously unreported behaviors, such as searching for the benchmark on HuggingFace instead of solving a task, or misusing credit cards in flight booking tasks. We share all agent logs, comprising 2.5B tokens of language model calls, to incentivize further research into agent behavior. By standardizing how the field evaluates agents and addressing common pitfalls in agent evaluation, we hope to shift the focus from agents that ace benchmarks to agents that work reliably in the real world.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
面向含编码任务在内的AI智能体的标准化评测框架。

### 2. 核心内容
AI智能体评测存在实现错误多、耗时长、结论不一致等问题，影响对智能体真实能力的判断。本文提出Holistic Agent Leaderboard标准化评测框架，可在数百台虚拟机上并行编排评测，并进行模型、脚手架与基准的三维分析。作者在9个模型与9个基准上完成两万余次智能体运行验证其有效性，为编码等任务中的智能体评测提供了可靠基础设施。

### 3. 对应检索需求
autonomous agents for coding tasks。

### 4. 来源与原文
- Source：ICLR-2026-Accepted
- OpenReview：[https://openreview.net/forum?id=vUaY1t64ZZ](https://openreview.net/forum?id=vUaY1t64ZZ)
