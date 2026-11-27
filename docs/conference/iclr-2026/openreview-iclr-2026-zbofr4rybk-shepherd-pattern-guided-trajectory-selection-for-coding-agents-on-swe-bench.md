---
title: "Shepherd: Pattern-Guided Trajectory Selection for Coding Agents on SWE-Bench"
title_zh: Shepherd：面向SWE-Bench编码智能体的模式引导轨迹选择
authors: "Alejandro Cuadron, Aditya Desai, Luis Gaspar Schroeder, Xingyao Wang, Wenjie Ma, Dacheng Li, Yichuan Wang, Ion Stoica, Graham Neubig, Joseph E. Gonzalez"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=ZBOFr4ryBk"
tags: ["query:ai-se"]
score: 9.0
evidence: 分析并改进在SWE-Bench上的大模型编码智能体
tldr: 尽管大模型编码智能体进步显著，但在SWE-bench等复杂软件工程任务上仍只能解决约一半问题。本文系统分析18个先进模型的3908条执行轨迹，归纳出无法与环境交互、并行发出相互依赖动作、过早假定完成三类失败模式。基于此提出模式引导的轨迹选择方法Shepherd，用于提升编码智能体在软件工程任务上的表现，为理解与修复智能体失败提供了依据。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 编码智能体在复杂软件工程任务上表现有限，需要系统理解其失败原因。
method: 分析大量执行轨迹归纳失败模式，并提出模式引导的轨迹选择方法。
result: 在多个先进模型上识别出三类典型失败模式并据此改进智能体表现。
conclusion: 该工作为诊断和提升编码智能体在软件工程任务上的能力提供了系统方法。
---

## Abstract
Despite major improvements in LLM coding agents, their performance on complex software engineering tasks is still limited—leading models to solve only about half of the software engineering tasks in benchmarks like SWE-bench. This gap highlights the need to systematically understand why coding agents fail.
We comprehensively analyze coding agent failure patterns in 18 state-of-the-art open- and closed-weight models. Through meticulous examination of 3,908 execution trajectories, we identify three distinct failure patterns: (1) \fa{}, where agents fail to interact with the environment; (2) \oo{}, where agents issue interdependent actions simultaneously rather than sequentially; and (3) \ft{}, where agents prematurely assume task completion.
Using these failure patterns, we introduce \judge{}, a test-time steering mechanism that leverages an LLM-as-a-judge framework to evaluate trajectories. \judge{} shows a strong monotonic correlation with expert annotations and can effectively identify problematic patterns in agent behavior. When applied to select optimal trajectories from multiple runs, \judge{} significantly improves performance, increasing o1-low from 21\% to 31\% on SWE-bench Verified, outperforming the more expensive o1-high model (29\%) at 57\% of the cost.
We open-source our comprehensive dataset of trajectories to facilitate further research on improving coding agent capabilities.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
分析并改进在SWE-Bench上的大模型编码智能体。

### 2. 核心内容
尽管大模型编码智能体进步显著，但在SWE-bench等复杂软件工程任务上仍只能解决约一半问题。本文系统分析18个先进模型的3908条执行轨迹，归纳出无法与环境交互、并行发出相互依赖动作、过早假定完成三类失败模式。基于此提出模式引导的轨迹选择方法Shepherd，用于提升编码智能体在软件工程任务上的表现，为理解与修复智能体失败提供了依据。

### 3. 对应检索需求
autonomous agents for coding tasks。

### 4. 来源与原文
- Source：ICLR-2026-Rejected-Public
- OpenReview：[https://openreview.net/forum?id=ZBOFr4ryBk](https://openreview.net/forum?id=ZBOFr4ryBk)
