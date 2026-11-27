---
title: Scaling Agentic Verifier for Competitive Coding
title_zh: 扩展面向竞赛编程的智能体验证器
authors: "Zeyao Ma, Jing Zhang, Xiaokang Zhang, Jiaxi Yang, Zongmeng Zhang, Jiajun Zhang, Yuheng Jing, Lei Zhang, Hao Zheng, Wenting Zhao, Junyang Lin, Binyuan Hui"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf/b95383b9dfc6ae8603f4ee889052dfd595e08740.pdf"
tags: ["query:ai-se"]
score: 8.0
evidence: 智能体验证器生成测试输入以重排代码解
tldr: 大模型在竞赛编程中难以一次答对，现有基于执行的重排受限于测试用例生成困难或随机采样低效。Agentic Verifier作为执行型智能体，主动推理程序行为并搜索高区分度测试输入，通过与执行环境多轮交互迭代精炼输入生成器以产生反例。该方式有效提升候选解重排的准确性，为智能体辅助代码验证提供了新思路。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 大模型单次难以答对竞赛题，现有执行式重排受测试生成与采样效率限制。
method: 构建执行型智能体验证器，主动搜索高区分度测试输入并迭代精炼生成器。
result: 通过暴露候选解行为差异的针对性反例提升重排准确性。
conclusion: 表明执行式智能体可有效提升代码解验证与选择质量。
---

## Abstract
Large language models (LLMs) have demonstrated strong coding capabilities but still struggle to solve competitive programming problems correctly in a single attempt. 
Execution-based re-ranking offers a promising test-time scaling strategy, yet existing methods are constrained by either difficult test case generation or inefficient random input sampling.
To address this limitation, we propose **Agentic Verifier**, an execution-based agent that actively reasons about program behaviors and searches for highly discriminative test inputs that expose behavioral discrepancies among candidate solutions. 
Through multi-turn interaction with code execution environments, the verifier iteratively refines the candidate input generator and produces targeted counterexamples rather than blindly sampling inputs. 
We train the verifier to acquire this discriminative input generation capability via a scalable pipeline combining large-scale data synthesis, rejection fine-tuning, and agentic reinforcement learning.
Extensive experiments across five competitive programming benchmarks demonstrate consistent improvements over strong execution-based baselines, achieving up to **+10-15\%** absolute gains in Best@$k$ accuracy.
Further analysis reveals clear test-time scaling behavior and highlights the verifier’s broader potential beyond reranking.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
智能体验证器生成测试输入以重排代码解。

### 2. 核心内容
大模型在竞赛编程中难以一次答对，现有基于执行的重排受限于测试用例生成困难或随机采样低效。Agentic Verifier作为执行型智能体，主动推理程序行为并搜索高区分度测试输入，通过与执行环境多轮交互迭代精炼输入生成器以产生反例。该方式有效提升候选解重排的准确性，为智能体辅助代码验证提供了新思路。

### 3. 对应检索需求
autonomous agents for coding tasks。

### 4. 来源与原文
- Source：ICML-2026-Accepted
- OpenReview：[https://openreview.net/forum?id=8bHa5wc7X5](https://openreview.net/forum?id=8bHa5wc7X5)
