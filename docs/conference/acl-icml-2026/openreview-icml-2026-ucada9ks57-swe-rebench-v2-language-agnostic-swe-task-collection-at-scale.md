---
title: "SWE-rebench V2: Language-Agnostic SWE Task Collection at Scale"
title_zh: SWE-rebench V2：大规模语言无关的软件工程任务收集
authors: "Ibragim Badertdinov, Maksim Nekrashevich, Anton Shevtsov, Alexander Golubev"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf/1d755b769d4eb555477e4bf99ea31bdc1c6580ee.pdf"
tags: ["query:ai-se"]
score: 8.0
evidence: 面向软件工程智能体的语言无关任务收集流水线
tldr: 软件工程智能体进步迅速，但强化学习训练受限于缺乏可复现执行环境和可靠测试套件的大规模任务集。作者提出SWE-rebench V2，一条语言无关的自动化流水线，通过交互式设置智能体合成仓库级安装与测试流程，并过滤不健全实例，从而大规模采集真实可执行的软件工程任务。该工作为训练代码智能体提供了可扩展的数据与环境基础。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 强化学习训练软件工程智能体缺乏大规模、可复现执行且语言多样的任务集。
method: 提出语言无关自动化流水线，用交互式设置智能体合成安装与测试流程并过滤不健全实例。
result: 实现大规模采集真实可执行的软件工程任务并构建RL训练环境。
conclusion: 为训练代码智能体提供了可扩展的数据与环境基础。
---

## Abstract
Software engineering agents (SWE) are improving rapidly, with recent gains largely driven by reinforcement learning (RL). However, RL training is constrained by the scarcity of large-scale task collections with reproducible execution environments and reliable test suites. Although a growing number of benchmarks have emerged, datasets suitable for training remain limited in scale and diversity or often target a limited set of high-resource language ecosystems. We introduce SWE-rebench V2, a language-agnostic automated pipeline for harvesting executable real-world SWE tasks and constructing RL training environments at scale. The pipeline synthesizes repository-specific installation and test procedures via an interactive setup agent, and filters unsound instances using an ensemble of LLM judges, validated against human-verified SWE-bench annotations. Using this pipeline, we construct a dataset of 32,079 tasks spanning 20 languages and 3,617 repositories, with pre-built images for reproducible execution. To further scale training data, we additionally release 120,000+ tasks with installation instructions, fail-to-pass tests and rich metadata, where the problem statement is generated based on the original pull request description. We validate the collected instances through a diagnostic study that covers a subset of tasks in five programming languages across seven popular models, and provide instance-level metadata that flags common confounders such as overly restrictive tests and underspecified descriptions. We release the datasets, the collection and execution code, and associated artifacts to enable large-scale training of SWE agents across diverse languages and repositories.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
面向软件工程智能体的语言无关任务收集流水线。

### 2. 核心内容
软件工程智能体进步迅速，但强化学习训练受限于缺乏可复现执行环境和可靠测试套件的大规模任务集。作者提出SWE-rebench V2，一条语言无关的自动化流水线，通过交互式设置智能体合成仓库级安装与测试流程，并过滤不健全实例，从而大规模采集真实可执行的软件工程任务。该工作为训练代码智能体提供了可扩展的数据与环境基础。

### 3. 对应检索需求
autonomous agents for coding tasks。

### 4. 来源与原文
- Source：ICML-2026-Accepted
- OpenReview：[https://openreview.net/forum?id=UCAda9kS57](https://openreview.net/forum?id=UCAda9kS57)
