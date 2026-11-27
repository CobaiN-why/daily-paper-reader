---
title: "HAI-Eval: Measuring Human-AI Synergy in Collaborative Coding"
title_zh: HAI-Eval：衡量协同编码中人机协同效应的基准
authors: "Hanjun Luo, Chiming Ni, Jiaheng Wen, Zhimu Huang, Yiran Wang, Bingduo Liao, Sylvia Chung, Yingbin Jin, Xinfeng Li, Wenyuan Xu, XiaoFeng Wang, Hanan Salam"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=pKqt8psClA"
tags: ["query:ai-se"]
score: 8.0
evidence: 评估人机协同编码智能体的基准
tldr: 大模型驱动的编码智能体正重塑开发范式，但现有评测要么针对人类要么针对模型，难以刻画人机协同。本文提出HAI-Eval统一基准，核心是协作必要性题目模板，这些任务对单独模型或独立人类都难以完成。基准从协同视角衡量人机合作的编码能力。该工作为编码智能体的协同能力评估提供了新工具。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 现有评测要么针对人类要么针对模型，无法刻画依赖人机协同的编码任务成功。
method: 提出HAI-Eval统一基准，设计对独立模型和独立人类都难以完成的协作必要性题目模板。
result: 从协同视角系统衡量人机合作在编码任务中的表现与互补性。
conclusion: 该工作为编码智能体的协同能力评估提供了新的基准工具。
---

## Abstract
LLM-powered coding agents are reshaping the development paradigm. However, existing evaluation systems, neither traditional tests for humans nor benchmarks for LLMs, fail to capture this shift. They remain focused on well-defined algorithmic problems, which excludes problems where success depends on human-AI collaboration. Such collaborative problems not only require human reasoning to interpret complex contexts and guide solution strategies, but also demand AI efficiency for implementation. To bridge this gap, we introduce HAI-Eval, a unified benchmark designed to measure the synergy of human-AI partnership in coding. HAI-Eval's core innovation is its "Collaboration-Necessary" problem templates, which are intractable for both standalone LLMs and unaided humans, but solvable through effective collaboration. Specifically, HAI-Eval uses 45 templates to dynamically create tasks. It also provides a standardized IDE for human participants and a reproducible toolkit with 450 task instances for LLMs, ensuring an ecologically valid evaluation. We conduct a within-subject study with 45 participants and benchmark their performance against 5 state-of-the-art LLMs under 4 different levels of human intervention. Results show that while standalone LLMs and unaided participants achieve poor pass rates (0.67% and 18.89%), human–AI collaboration significantly improves performance to 31.11%. Our analysis reveals an emerging co-reasoning partnership. This finding challenges the traditional human-tool hierarchy by showing that strategic breakthroughs can originate from either humans or AI. HAI-Eval establishes not only a challenging benchmark for next-generation coding agents but also a grounded, scalable framework for assessing core developer competencies in the AI era. Our benchmark and interactive demo are openly accessible.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
评估人机协同编码智能体的基准。

### 2. 核心内容
大模型驱动的编码智能体正重塑开发范式，但现有评测要么针对人类要么针对模型，难以刻画人机协同。本文提出HAI-Eval统一基准，核心是协作必要性题目模板，这些任务对单独模型或独立人类都难以完成。基准从协同视角衡量人机合作的编码能力。该工作为编码智能体的协同能力评估提供了新工具。

### 3. 对应检索需求
coding agents for automated test generation and documentation。

### 4. 来源与原文
- Source：ICLR-2026-Public
- OpenReview：[https://openreview.net/forum?id=pKqt8psClA](https://openreview.net/forum?id=pKqt8psClA)
