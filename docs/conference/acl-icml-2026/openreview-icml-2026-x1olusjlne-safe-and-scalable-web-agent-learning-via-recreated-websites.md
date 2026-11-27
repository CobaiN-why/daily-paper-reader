---
title: Safe and Scalable Web Agent Learning via Recreated Websites
title_zh: 通过重建网站实现安全且可扩展的 Web 智能体学习
authors: "Hyungjoo Chae, Jungsoo Park, Alan Ritter"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf/c2afd1ace56b4878c7b02ffb5a7e124fa1ae83a3.pdf"
tags: ["query:ai-se"]
score: 5.0
evidence: 通过重建网站构建可验证沙箱以保障智能体安全学习
tldr: 在真实网站上训练自主 Web 智能体存在探索不安全、难以重置且反馈不可验证的问题。本文提出 VeriEnv 框架，将语言模型用作环境创建者，把真实网站自动克隆为可执行、可验证的合成环境，并通过 Python SDK 提供确定性奖励。该设计使智能体学习脱离不安全的真实交互，同时支持环境的可扩展自演化，为智能体安全训练提供了新思路。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 真实网站环境不安全、难重置且缺少可验证反馈，限制了智能体训练。
method: 用语言模型把真实网站克隆为可执行的合成沙箱，并提供确定性的可验证奖励。
result: 该方法在 Web 智能体基准上实现了可扩展且安全的自我演化训练。
conclusion: 将环境合成与智能体学习解耦，为智能体安全训练提供了可行路径。
---

## Abstract
Training autonomous web agents is fundamentally limited by the environments they learn from: real-world websites are unsafe to explore, hard to reset, and rarely provide verifiable feedback.
We propose VeriEnv, a framework that treats language models as environment creators, automatically cloning real-world websites into fully executable, verifiable synthetic environments.
By exposing controlled internal access via a Python SDK, VeriEnv enables agents to self-generate tasks with deterministic, programmatically verifiable rewards, eliminating reliance on heuristic or LLM-based judges.
This design decouples agent learning from unsafe real-world interaction while enabling scalable self-evolution through environment expansion.
Through experiments on web agent benchmarks, we show that agents trained with VeriEnv generalize to unseen websites, achieve site-specific mastery through self-evolving training, and benefit from scaling the number of training environments.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
通过重建网站构建可验证沙箱以保障智能体安全学习。

### 2. 核心内容
在真实网站上训练自主 Web 智能体存在探索不安全、难以重置且反馈不可验证的问题。本文提出 VeriEnv 框架，将语言模型用作环境创建者，把真实网站自动克隆为可执行、可验证的合成环境，并通过 Python SDK 提供确定性奖励。该设计使智能体学习脱离不安全的真实交互，同时支持环境的可扩展自演化，为智能体安全训练提供了新思路。

### 3. 对应检索需求
大模型安全。

### 4. 来源与原文
- Source：ICML-2026-Accepted
- OpenReview：[https://openreview.net/forum?id=x1OLusJLNe](https://openreview.net/forum?id=x1OLusJLNe)
