---
title: Computer-Use Agents as Judges for Automatic GUI Design
title_zh: 计算机使用代理作为自动GUI设计的评判者
authors: "Kevin Qinghong Lin, Siyuan Hu, Linjie Li, Zhengyuan Yang, Lijuan Wang, Philip Torr, Mike Zheng Shou"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=ZMOLw9eBPm"
tags: ["query:ai-se"]
score: 5.0
evidence: 面向编码的大模型与计算机使用代理用于自动GUI设计
tldr: 现有GUI主要面向人类设计，导致计算机使用代理需模仿不必要的人类行为。本文提出一个涵盖52个应用、1560个合成任务的自动GUI开发基准，探索能否让计算机使用代理充当评判者来辅助编码大模型进行界面设计。实验评估了代理评判对生成质量的影响，为代理与代码模型协同的自动化软件开发提供了新视角。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 现有GUI多为人类设计，代理需模仿低效的人类操作行为。
method: 构建覆盖52个应用、1560个合成任务的自动GUI开发基准，让代理充当评判者辅助编码模型。
result: 实验探究代理评判对编码模型GUI设计质量的作用与差异。
conclusion: 为代理与代码模型协同的自动化界面开发提供了评测基础与新思路。
---

## Abstract
Computer-Use Agents (CUA) are becoming increasingly capable of autonomously operating digital environments through Graphical User Interfaces (GUI). Yet, most GUI remain designed primarily for humans—prioritizing aesthetics and usability—forcing agents to adopt human-oriented behaviors that are unnecessary for efficient task execution.
At the same time, rapid advances in coding-oriented language models (Coder) have transformed automatic GUI design. This raises a fundamental question: \textit{Can CUA as judges to assist Coder for automatic GUI design}?
To investigate, we introduce \textbf{\bench}, a benchmark for \underline{A}utomatic G\underline{UI} development spanning 52 applications across diverse domains. Using  language models, we synthesis 1560 tasks that simulate real-world scenarios. To ensure task reliability, we further develop a verifier that programmatically checks whether each task is executable within its environment.
Building on this, we propose a \textbf{Coder–CUA in Collaboration} framework: the Coder acts as Designer, generating and revising websites, while the CUA serves as Judge, evaluating functionality and refining designs. Success is measured not by visual appearance, but by task solvability and CUA navigation success rate. 
To turn CUA feedback into usable guidance, we design an \textbf{CUA Dashboard} that compresses multi-step navigation histories into concise visual summaries, offering interpretable guidance for iterative redesign.
By positioning agents as both designers and judges, our framework shifts interface design toward agent-native efficiency and reliability. 
Our work takes a step toward shifting agents from passive use toward active participation in digital environments.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
面向编码的大模型与计算机使用代理用于自动GUI设计。

### 2. 核心内容
现有GUI主要面向人类设计，导致计算机使用代理需模仿不必要的人类行为。本文提出一个涵盖52个应用、1560个合成任务的自动GUI开发基准，探索能否让计算机使用代理充当评判者来辅助编码大模型进行界面设计。实验评估了代理评判对生成质量的影响，为代理与代码模型协同的自动化软件开发提供了新视角。

### 3. 对应检索需求
large language models and their applications。

### 4. 来源与原文
- Source：ICLR-2026-Public
- OpenReview：[https://openreview.net/forum?id=ZMOLw9eBPm](https://openreview.net/forum?id=ZMOLw9eBPm)
