---
title: Process-Level Trajectory Evaluation for Environment Configuration in Software Engineering Agents
title_zh: 软件工程智能体环境配置的过程级轨迹评估
authors: "Jiayi Kuang, Yinghui Li, Xin Zhang, Yangning Li, di yin, Xing Sun, Ying Shen, Philip S. Yu"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=Q8qgloDKUO"
tags: ["query:ai-se"]
score: 8.0
evidence: 面向软件工程智能体环境配置的过程级评测
tldr: 环境配置是软件工程智能体落地的瓶颈，依赖大量人工且缺乏高质量数据，现有基准只评估端到端构建或测试成功与否。本文提出EnConda-bench，通过注入真实README错误自动构建任务，对智能体在环境规划、感知驱动错误诊断、反馈驱动修复与执行等环节进行过程级轨迹评估。该基准揭示了智能体在何处以及为何成功或失败，为改进软件工程智能体提供了细粒度诊断依据。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 环境配置是软件工程智能体的瓶颈，现有基准只评估端到端结果，无法定位智能体成功或失败的原因。
method: 构建EnConda-bench，通过注入真实README错误自动生成任务，对规划、诊断、修复与执行进行过程级评估。
result: 实现了对智能体环境配置各环节细粒度能力的轨迹化诊断。
conclusion: 为软件工程智能体的环境配置能力提供了细粒度、可解释的评测方法。
---

## Abstract
Large language model-based agents show promise for software engineering, but environment configuration remains a bottleneck due to heavy manual effort and scarce large-scale, high-quality datasets.
Existing benchmarks assess only end-to-end build/test success, obscuring where and why agents succeed or fail.
We introduce the Environment Configuration Diagnosis Benchmark, EnConda-bench, which provides process-level trajectory assessment of fine-grained agent capabilities during environment setup-planning, perception-driven error diagnosis, feedback-driven repair, and action to execute the final environment configuration. 
Our task instances are automatically constructed by injecting realistic README errors and are validated in Docker for scalable, high-quality evaluation.
EnConda-bench combines process-level analysis with end-to-end executability to enable capability assessments beyond aggregate success rates.
Evaluations across state-of-the-art LLMs and agent frameworks show that while agents can localize errors, they struggle to translate feedback into effective corrections, limiting end-to-end performance.
To our knowledge, EnConda-bench is the first framework to provide process-level internal capability assessment for environment configuration, offering actionable insights for improving software engineering agents.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
面向软件工程智能体环境配置的过程级评测。

### 2. 核心内容
环境配置是软件工程智能体落地的瓶颈，依赖大量人工且缺乏高质量数据，现有基准只评估端到端构建或测试成功与否。本文提出EnConda-bench，通过注入真实README错误自动构建任务，对智能体在环境规划、感知驱动错误诊断、反馈驱动修复与执行等环节进行过程级轨迹评估。该基准揭示了智能体在何处以及为何成功或失败，为改进软件工程智能体提供了细粒度诊断依据。

### 3. 对应检索需求
autonomous agents for coding tasks。

### 4. 来源与原文
- Source：ICLR-2026-Accepted
- OpenReview：[https://openreview.net/forum?id=Q8qgloDKUO](https://openreview.net/forum?id=Q8qgloDKUO)
