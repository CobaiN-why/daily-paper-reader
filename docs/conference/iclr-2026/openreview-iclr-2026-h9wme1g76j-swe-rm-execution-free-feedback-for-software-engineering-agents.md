---
title: "SWE-RM: Execution-free Feedback for Software Engineering Agents"
title_zh: SWE-RM：面向软件工程智能体的免执行反馈
authors: "KaShun SHUM, Binyuan Hui, Jiawei Chen, Lei Zhang, X. W., Jiaxi Yang, Yuzhen Huang, Junyang Lin, Junxian He"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=H9wMe1G76j"
tags: ["query:ai-se"]
score: 9.0
evidence: 面向软件工程智能体的免执行奖励反馈
tldr: 现有编码智能体依赖单元测试等执行反馈，但测试用例收集代价高且反馈稀疏，难以区分同为成功或失败的轨迹。本文研究面向真实软件工程智能体的免执行反馈奖励模型SWE-RM，在不依赖测试用例的情况下提供更细粒度信号，并兼顾测试时扩展与强化学习。该工作为提升自主软件工程智能体的训练与推理反馈质量提供了新途径。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 基于单元测试的执行反馈稀疏且收集成本高，难以有效区分智能体轨迹优劣。
method: 提出免执行的奖励模型SWE-RM，在不依赖测试用例的情况下提供细粒度反馈，兼容测试时扩展与强化学习。
result: 为软件工程智能体提供更细粒度、可扩展的反馈信号以提升训练与推理效果。
conclusion: 展示了免执行奖励模型在软件工程智能体反馈中的潜力与应用价值。
---

## Abstract
Execution-based feedback like unit testing is widely used in the development of coding agents through test-time scaling (TTS) and reinforcement learning (RL). This paradigm requires scalable and reliable collection of unit test cases to provide accurate feedback, and the resulting feedback is often sparse and cannot effectively distinguish between trajectories that are both successful or both unsuccessful. In contrast, execution-free feedback from reward models can provide more fine-grained signals without depending on unit test cases. Despite this potential, execution-free feedback for realistic software engineering (SWE) agents remains underexplored. Aiming to develop versatile reward models that are effective across TTS and RL, however, we observe that two verifiers with nearly identical TTS performance can nevertheless yield very different results in RL. Intuitively, TTS primarily reflects the model’s ability to select the best trajectory, but this ability does not necessarily generalize to RL. To address this limitation, we identify two additional aspects that are crucial for RL training: classification accuracy and calibration. We then conduct comprehensive controlled experiments to investigate how to train a robust reward model that performs well across these metrics. In particular, we analyze the impact of various factors such as training data scale, policy mixtures, and data source composition.
Guided by these investigations, we introduce SWE-RM, an accurate and robust reward model adopting a mixture-of-experts architecture with 30B total parameters and 3B activated during inference. SWE-RM substantially improves SWE agents on both TTS and RL performance. For example, it increases the accuracy of Qwen3-Coder-Flash from 51.6% to 62.0%, and Qwen3-Coder-Max from 67.0% to 74.6% on SWE-Bench Verified using TTS, achieving new state-of-the-art performance among open-source models. On RL training, SWE-RM lifts the resolve rate of execution-based counterparts by 3 absolute points on SWE-Bench Verified.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
面向软件工程智能体的免执行奖励反馈。

### 2. 核心内容
现有编码智能体依赖单元测试等执行反馈，但测试用例收集代价高且反馈稀疏，难以区分同为成功或失败的轨迹。本文研究面向真实软件工程智能体的免执行反馈奖励模型SWE-RM，在不依赖测试用例的情况下提供更细粒度信号，并兼顾测试时扩展与强化学习。该工作为提升自主软件工程智能体的训练与推理反馈质量提供了新途径。

### 3. 对应检索需求
autonomous agents for coding tasks。

### 4. 来源与原文
- Source：ICLR-2026-Accepted
- OpenReview：[https://openreview.net/forum?id=H9wMe1G76j](https://openreview.net/forum?id=H9wMe1G76j)
