---
title: "RExBench: Can coding agents autonomously implement AI research extensions?"
title_zh: RExBench：编码智能体能否自主实现AI研究扩展
authors: "Nicholas Edwards, Yukyung Lee, Yujun Audrey Mao, Yulu Qin, Sebastian Schuster, Najoung Kim"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=0xpakqqTbe"
tags: ["query:ai-se"]
score: 8.0
evidence: 评估自主编码智能体实现AI研究扩展的基准
tldr: 基于大模型的智能体已能自主完成复杂软件工程任务，但缺乏评估其实现研究扩展能力的基准。本文提出RExBench，构建12篇研究论文的真实扩展任务，每个任务以现有论文与代码库为基础并配以领域专家撰写的指令，用于考察智能体能否自主实现新的研究假设。该基准具备抗数据污染特性，为衡量自主编码智能体在科研软件工程场景中的能力提供了标准化平台。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: LLM智能体已能自主完成复杂软件工程任务，但缺少评估其实现研究扩展能力的基准。
method: 提出RExBench，基于12篇论文构造真实扩展任务，每项任务包含现有代码库与专家撰写指令，考察智能体自主实现新假设。
result: 该基准具备抗数据污染特性，系统刻画了自主编码智能体实现研究扩展的能力。
conclusion: 为评估自主编码智能体在科研软件工程场景中的能力提供了标准化基准。
---

## Abstract
Agents based on Large Language Models (LLMs) have shown promise for performing sophisticated software engineering tasks autonomously. In addition, there has been progress towards developing agents that can perform parts of the research pipeline in machine learning and the natural sciences. We argue that research extension and its implementation is a critical capability for such systems, and introduce RExBench to support the evaluation of this capability. RExBench is a benchmark consisting of realistic extensions of 12 research papers that aim to investigate novel research hypotheses. Each task is set up as an extension to an existing research paper and codebase, accompanied by domain expert-written instructions. RExBench is robust to data contamination, and supports an automatic evaluation infrastructure that executes agent outputs to determine whether the success criteria are met. We use this benchmark to evaluate 13 LLM agents implemented using three different frameworks: aider, Claude Code, and OpenHands. We find that all agents fail to autonomously implement the majority of the extensions, with the best agent at around 31% success rate. Although the success rate improves with additional human-written hints, the best performance under this setting remains below 48%. This indicates that current agents are still short of being able to handle realistic research extension tasks without substantial human guidance. Based on analyses of prominent failure modes, we put forward actionable short- and long-horizon recommendations for future research coding agent development.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
评估自主编码智能体实现AI研究扩展的基准。

### 2. 核心内容
基于大模型的智能体已能自主完成复杂软件工程任务，但缺乏评估其实现研究扩展能力的基准。本文提出RExBench，构建12篇研究论文的真实扩展任务，每个任务以现有论文与代码库为基础并配以领域专家撰写的指令，用于考察智能体能否自主实现新的研究假设。该基准具备抗数据污染特性，为衡量自主编码智能体在科研软件工程场景中的能力提供了标准化平台。

### 3. 对应检索需求
autonomous agents for coding tasks。

### 4. 来源与原文
- Source：ICLR-2026-Public
- OpenReview：[https://openreview.net/forum?id=0xpakqqTbe](https://openreview.net/forum?id=0xpakqqTbe)
