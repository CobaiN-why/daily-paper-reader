---
title: Generalizable End-to-End Tool-Use RL with Synthetic CodeGym
title_zh: 基于合成CodeGym的可泛化端到端工具使用强化学习
authors: "Weihua Du, Hailei Gong, Zhan Ling, Kang Liu, Lingfeng Shen, Xuesong Yao, Yufei Xu, Dingyuan Shi, Yiming Yang, Jiecao Chen"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=QRSeFZfu8E"
tags: ["query:ai-se"]
score: 7.0
evidence: 以编程问题为基础构建工具使用智能体的训练环境
tldr: 工具增强的大模型智能体往往依赖静态轨迹微调或在狭窄任务上强化学习，导致面对新工具和新流程时泛化差、易失效。作者提出CodeGym框架，以代码执行为结构化载体，合成多样、可验证、可控的多轮工具使用训练环境，并据此进行端到端强化学习。该工作提升了智能体在未见工具与工作流上的泛化能力，为可扩展的编码类工具智能体训练提供了通用方案。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 现有工具使用智能体训练依赖静态轨迹或狭窄任务，泛化性差且对新工具脆弱。
method: 以编程问题为结构化载体，构建CodeGym合成多样可验证的多轮工具使用环境并进行端到端强化学习。
result: 该方法提升了智能体在新工具和未见工作流上的泛化表现。
conclusion: 以代码为载体的环境合成与强化学习为训练可泛化的工具使用智能体提供了有效路径。
---

## Abstract
Tool-augmented large language models (LLMs), hereafter LLM agents, leverage external tools to solve diverse tasks and interface with the real world. However, current training practices largely rely on supervised fine-tuning (SFT) over static trajectories or reinforcement learning (RL) on narrow tasks, which generalize poorly beyond development settings and lead to brittleness with new tools and unseen workflows. Because code execution reflects many structural patterns of real-world workflows, we use coding problems as a structured substrate to build tool-use agent training environments with diverse task configurations. To this end, we introduce **CodeGym**, a scalable framework that synthesizes diverse, verifiable, and controllable multi-turn tool-use environments for agent RL, enabling LLM agents to explore and master various workflows actively. CodeGym converts static coding problems into interactive environments by extracting atomic functions or logic into callable tools, yielding verifiable tasks that span various tool-execution workflows. Models of varying sizes and chain-of-thought configurations trained in CodeGym exhibit consistent out-of-distribution generalizability; for example, Qwen2.5-32B-Instruct achieves an absolute accuracy gain of 8.7 points on the OOD benchmark $\tau$-Bench. These results highlight CodeGym as a step toward scalable general-purpose RL environments for training tool-use behaviors that align with real-world agent workflows. Our code is publicly available at https://github.com/StigLidu/CodeGym.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
以编程问题为基础构建工具使用智能体的训练环境。

### 2. 核心内容
工具增强的大模型智能体往往依赖静态轨迹微调或在狭窄任务上强化学习，导致面对新工具和新流程时泛化差、易失效。作者提出CodeGym框架，以代码执行为结构化载体，合成多样、可验证、可控的多轮工具使用训练环境，并据此进行端到端强化学习。该工作提升了智能体在未见工具与工作流上的泛化能力，为可扩展的编码类工具智能体训练提供了通用方案。

### 3. 对应检索需求
autonomous agents for coding tasks。

### 4. 来源与原文
- Source：ICLR-2026-Accepted
- OpenReview：[https://openreview.net/forum?id=QRSeFZfu8E](https://openreview.net/forum?id=QRSeFZfu8E)
