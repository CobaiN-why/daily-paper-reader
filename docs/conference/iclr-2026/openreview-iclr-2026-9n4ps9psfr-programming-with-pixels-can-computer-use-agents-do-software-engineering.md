---
title: "Programming with Pixels: Can Computer-Use Agents do Software Engineering?"
title_zh: 以像素编程：计算机使用智能体能否胜任软件工程？
authors: "Pranjal Aggarwal, Sean Welleck"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=9N4Ps9Psfr"
tags: ["query:ai-se"]
score: 9.0
evidence: 计算机使用智能体通过操作IDE自动化多种软件工程任务
tldr: 现有智能体评测多集中于简单场景，难以判断通用计算机使用智能体能否胜任专业化的软件工程工作。为此作者提出PwP，这是首个面向软件工程的综合计算机使用环境，智能体通过视觉方式操控IDE完成多种任务；同时构建PwP-Bench基准，涵盖15项跨模态、跨语言、跨技能的软件工程任务。研究对现有智能体进行了广泛评测，揭示其在真实软件工程自动化中的能力与局限，为通用智能体落地软件开发提供了首个系统化评测基础。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 现有计算机使用智能体评测多停留在简单任务，尚不清楚其能否自动化专业化的软件工程工作。
method: 提出PwP环境，让智能体以视觉方式操控IDE完成软件工程任务，并构建含15项任务的PwP-Bench基准。
result: 通过对多种通用智能体在跨模态、跨语言、跨技能任务上的广泛评测，揭示了其在真实软件工程场景中的表现与不足。
conclusion: 该工作为通用计算机使用智能体能否胜任软件工程自动化提供了首个系统化评测环境与基准。
---

## Abstract
Computer-use agents (CUAs) hold the promise of performing a wide variety of general tasks, but current evaluations have primarily focused on simple scenarios. 
It therefore remains unclear whether such generalist agents can automate more sophisticated and specialized work such as software engineering (SWE). 
To investigate this, we introduce Programming with Pixels (PwP), the first comprehensive computer-use environment for software engineering, where agents visually control an IDE to perform diverse software engineering tasks. 
To enable holistic evaluation, we also introduce PwP-Bench, a benchmark of 15 existing and new software-engineering tasks spanning multiple modalities, programming languages, and skillsets. 
We perform an extensive evaluation of state-of-the-art open-weight and closed-weight CUAs and find that when interacting purely visually, they perform significantly worse than specialized coding agents. 
However, when the same CUAs are given direct access to just two APIs—file editing and bash operations—performance jumps, often reaching the levels of specialized agents despite having a task-agnostic design. 
Furthermore, when given access to additional IDE tools via text APIs, all models show further gains. 
Our analysis shows that current CUAs fall short mainly due to limited visual grounding and the inability to take full advantage of the rich environment, leaving clear room for future improvements.
PwP establishes software engineering as a natural domain for benchmarking whether generalist computer-use agents can reach specialist-level performance on sophisticated tasks.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
计算机使用智能体通过操作IDE自动化多种软件工程任务。

### 2. 核心内容
现有智能体评测多集中于简单场景，难以判断通用计算机使用智能体能否胜任专业化的软件工程工作。为此作者提出PwP，这是首个面向软件工程的综合计算机使用环境，智能体通过视觉方式操控IDE完成多种任务；同时构建PwP-Bench基准，涵盖15项跨模态、跨语言、跨技能的软件工程任务。研究对现有智能体进行了广泛评测，揭示其在真实软件工程自动化中的能力与局限，为通用智能体落地软件开发提供了首个系统化评测基础。

### 3. 对应检索需求
software engineering tasks and automation。

### 4. 来源与原文
- Source：ICLR-2026-Accepted
- OpenReview：[https://openreview.net/forum?id=9N4Ps9Psfr](https://openreview.net/forum?id=9N4Ps9Psfr)
