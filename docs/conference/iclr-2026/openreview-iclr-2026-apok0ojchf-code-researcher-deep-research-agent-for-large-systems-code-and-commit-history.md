---
title: "Code Researcher: Deep Research Agent for Large Systems Code and Commit History"
title_zh: Code Researcher：面向大型系统代码与提交历史的深度研究智能体
authors: "Ramneet Singh, Sathvik Joel, Nalin Wadhwa, Abhav Mehrotra, Ramakrishna B Bairi, Aditya Kanade, Nagarajan Natarajan"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=aPOk0OjChf"
tags: ["query:ai-se"]
score: 9.0
evidence: 面向系统代码的深度研究型编码智能体
tldr: 现有大模型编码智能体在小型基准上表现良好，但在庞大复杂的系统代码上效果有限，修改前需从海量代码库与提交历史中检索上下文。本文提出首个面向代码的深度研究智能体Code Researcher，围绕语义、模式与提交历史进行多步推理，检索相关上下文以生成修复崩溃的补丁。该方法将深度研究范式引入系统代码维护，拓展了自主编码智能体的应用边界。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 大模型编码智能体在系统代码上效果欠佳，修改前需大量检索代码库与提交历史上下文。
method: 设计面向代码的深度研究智能体，对语义、模式与提交历史进行多步推理并检索相关上下文生成补丁。
result: 将该智能体用于系统代码崩溃修复补丁生成，展示了在复杂系统代码上的有效性。
conclusion: 把深度研究范式引入代码维护，拓展了自主编码智能体的应用范围。
---

## Abstract
Large Language Model (LLM)-based coding agents have shown promising results on coding benchmarks, but their effectiveness on systems code remains underexplored. Due to the size and complexities of systems code, making changes to a systems codebase requires *researching* about many pieces of context, derived from the large codebase and its massive commit history, *before* making changes. Inspired by the recent progress on deep research agents, we design the first deep research agent for code, called Code Researcher, and apply it to the problem of generating patches to mitigate crashes reported in systems code. Code Researcher performs multi-step reasoning about semantics, patterns, and commit history of code to retrieve all relevant context from the codebase and its commit history. We evaluate Code Researcher on kBenchSyz, a benchmark of Linux kernel crashes, and show that it significantly outperforms strong baselines, achieving a crash-resolution rate (CRR) of 48%, compared to 31.5% by SWE-agent and 31% by Agentless, using OpenAI's GPT-4o model. Scaling up sampling budget to 10 trajectories increases Code Researcher's CRR to 54%. Code Researcher is also robust to model choices, reaching 67% with the newer Gemini 2.5-Flash model. Through another experiment on an open-source multimedia software, we show the generalizability of Code Researcher and also conduct ablations. Our experiments highlight the importance of global context gathering and multi-faceted reasoning for large codebases.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
面向系统代码的深度研究型编码智能体。

### 2. 核心内容
现有大模型编码智能体在小型基准上表现良好，但在庞大复杂的系统代码上效果有限，修改前需从海量代码库与提交历史中检索上下文。本文提出首个面向代码的深度研究智能体Code Researcher，围绕语义、模式与提交历史进行多步推理，检索相关上下文以生成修复崩溃的补丁。该方法将深度研究范式引入系统代码维护，拓展了自主编码智能体的应用边界。

### 3. 对应检索需求
autonomous agents for coding tasks。

### 4. 来源与原文
- Source：ICLR-2026-Rejected-Public
- OpenReview：[https://openreview.net/forum?id=aPOk0OjChf](https://openreview.net/forum?id=aPOk0OjChf)
