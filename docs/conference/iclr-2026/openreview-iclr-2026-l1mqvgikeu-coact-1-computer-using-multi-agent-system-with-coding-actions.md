---
title: "CoAct-1: Computer-using Multi-agent System with Coding Actions"
title_zh: CoAct-1：具备编码动作的计算机使用多智能体系统
authors: "Linxin Song, Yutong Dai, Viraj Prabhu, Jieyu Zhang, Taiwei Shi, Li Li, Junnan Li, silvio savarese, Zeyuan Chen, Jieyu Zhao, Ran Xu, Caiming Xiong"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=l1MQVgIKEU"
tags: ["query:ai-se"]
score: 7.0
evidence: 使智能体以编码为动作的多智能体系统
tldr: 通过图形界面操作电脑的自主智能体在长程复杂任务上效率低、鲁棒性差，仅靠GUI操作存在固有限制。本文提出CoAct-1多智能体系统，将编码作为增强动作，由编排器动态把子任务分配给GUI操作者或专门的程序员智能体。该方法结合界面控制与直接程序化执行，提升了复杂任务的效率与可靠性，为编码能力融入通用智能体提供了新范式。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 纯GUI操作的计算机使用智能体在长程复杂任务上效率低、脆弱，仅靠规划难以克服操作局限。
method: 提出CoAct-1多智能体系统，由编排器在GUI操作者与程序员智能体间动态分配子任务。
result: 结合界面控制与程序化执行，提升了复杂长程任务的效率与可靠性。
conclusion: 表明将编码作为增强动作可提升通用计算机智能体的能力，为智能体设计提供新思路。
---

## Abstract
Autonomous agents that operate computers via Graphical User Interfaces (GUIs) often struggle with efficiency and reliability on complex, long-horizon tasks. While augmenting these agents with planners can improve task decomposition, they remain constrained by the inherent limitations of performing all actions through GUI manipulation, leading to brittleness and inefficiency. In this work, we introduce a more robust and flexible paradigm: enabling agents to use coding as an enhanced action. We present CoAct-1, a novel multi-agent system that synergistically combines GUI-based control with direct programmatic execution. CoAct-1 features an Orchestrator that dynamically delegates subtasks to either a conventional GUI Operator or a specialized Programmer agent, which can write and execute Python or Bash scripts. This hybrid approach allows the agent to bypass inefficient GUI action sequences for tasks like file management and data processing, while still utilizing visual interaction when necessary. We evaluate our system on the challenging OSWorld and WindowsAgentArena benchmark, where CoAct-1 achieves a new state-of-the-art success rate of 60.8% on OSWorld and 52.5% on WindowsAgentArena, significantly outperforming prior methods. Furthermore, our approach dramatically improves efficiency, reducing the average number of steps required to complete a task to just 10.15 on OSWorld, compared to 15 for leading GUI agents. Our results demonstrate that integrating coding as a core action provides a more powerful, efficient, and scalable path toward generalized computer automation.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
使智能体以编码为动作的多智能体系统。

### 2. 核心内容
通过图形界面操作电脑的自主智能体在长程复杂任务上效率低、鲁棒性差，仅靠GUI操作存在固有限制。本文提出CoAct-1多智能体系统，将编码作为增强动作，由编排器动态把子任务分配给GUI操作者或专门的程序员智能体。该方法结合界面控制与直接程序化执行，提升了复杂任务的效率与可靠性，为编码能力融入通用智能体提供了新范式。

### 3. 对应检索需求
autonomous agents for coding tasks。

### 4. 来源与原文
- Source：ICLR-2026-Accepted
- OpenReview：[https://openreview.net/forum?id=l1MQVgIKEU](https://openreview.net/forum?id=l1MQVgIKEU)
