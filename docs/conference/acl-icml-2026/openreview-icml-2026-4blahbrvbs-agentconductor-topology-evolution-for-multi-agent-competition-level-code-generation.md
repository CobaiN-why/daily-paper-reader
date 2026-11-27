---
title: "AgentConductor: Topology Evolution for Multi-Agent Competition-Level Code Generation"
title_zh: AgentConductor：面向多智能体竞赛级代码生成的拓扑演化
authors: "Siyu Wang, Ruotian Lu, Zhihao Yang, Yuchao Wang, Yanzhou Zhang, Lei Xu, Qimin Xu, Guojun Yin, Cailian Chen, Xinping Guan"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf/6ffc4b8b771eaf3318c96846c00a057cf5739573.pdf"
tags: ["query:ai-se"]
score: 9.0
evidence: 面向竞赛级代码生成的多智能体拓扑演化
tldr: 大模型驱动的多智能体系统通过预定义拓扑协调专门化智能体，在竞赛级代码生成等复杂任务上展现潜力，但现有方法既不根据任务难度调整拓扑密度，也无法利用执行反馈在实例内精化拓扑，导致通信冗余与性能瓶颈。作者提出AgentConductor，以基于大模型编排者为核心，并用强化学习优化多智能体系统，使拓扑随任务动态演化。该方法减少了冗余通信并提升了复杂代码生成的表现。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 现有多智能体代码生成依赖固定拓扑，无法随任务难度调整密度或用执行反馈精化，导致通信冗余与瓶颈。
method: 提出AgentConductor，以基于大模型的编排者为核心，用强化学习优化多智能体系统，使拓扑按任务动态演化。
result: 该方法减少冗余通信并提升了竞赛级代码生成任务的性能表现。
conclusion: 为多智能体代码生成中的自适应协作拓扑设计提供了强化学习方案。
---

## Abstract
Large language model(LLM)-driven multi-agent systems(MAS) coordinate specialized agents through predefined topologies and show promise for complex tasks such as competition-level code generation. Recent studies demonstrate that carefully designed multi-agent workflows and communication graphs can significantly improve code generation performance by leveraging collaborative reasoning. However, existing methods neither adapt topology density to task difficulty nor refine the topology within an instance using execution feedback, which leads to redundant communication and performance bottlenecks. To address these issues, we propose AgentConductor: a reinforcement learning-optimized MAS with an LLM-based orchestrator agent as its core, which enables end-to-end feedback-driven dynamic generation of interaction topologies. For each query, AgentConductor infers agent roles and task difficulty, then constructs a task-adapted, density-aware layered directed acyclic graph(DAG) topology, underpinned by two key innovations. First, we design a novel topology density function to quantify communication-aware multi-agent interactions. Second, we adopt difficulty interval partitioning to avoid excessive pruning for precise topological density upper bound measurement per difficulty level and finer-grained control. Across five code datasets, AgentConductor outperforms the strongest baseline by up to 14.6\% in pass@1, with 13\% lower topology density and 68\% lower token cost.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
面向竞赛级代码生成的多智能体拓扑演化。

### 2. 核心内容
大模型驱动的多智能体系统通过预定义拓扑协调专门化智能体，在竞赛级代码生成等复杂任务上展现潜力，但现有方法既不根据任务难度调整拓扑密度，也无法利用执行反馈在实例内精化拓扑，导致通信冗余与性能瓶颈。作者提出AgentConductor，以基于大模型编排者为核心，并用强化学习优化多智能体系统，使拓扑随任务动态演化。该方法减少了冗余通信并提升了复杂代码生成的表现。

### 3. 对应检索需求
autonomous agents for coding tasks。

### 4. 来源与原文
- Source：ICML-2026-Accepted
- OpenReview：[https://openreview.net/forum?id=4bLahBrVBs](https://openreview.net/forum?id=4bLahBrVBs)
