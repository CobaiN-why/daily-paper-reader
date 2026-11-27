---
title: "ARCS: Agentic Retrieval-Augmented Code Synthesis with Iterative Refinement"
title_zh: ARCS：带迭代细化的代理式检索增强代码合成
authors: "Manish Bhattarai, Miguel cordova, Minh N. Vu, Javier E. Santos, Ismael Boureima, Daniel O'Malley"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=qrfgXhZcG7"
tags: ["query:ai-se"]
score: 9.0
evidence: 代理式检索增强代码合成与执行修复循环提升大模型代码生成
tldr: "大模型代码生成常受幻觉与收敛慢困扰，且难以微调。本文提出ARCS，一种无需微调的代理式检索增强代码合成系统，通过先检索上下文再生成、执行测试并迭代修复的预算化合成-执行-修复循环工作。在HumanEval上以Llama-3.1-405B达到87.2%的pass@1，超越CodeAgent，并给出终止性与有界成本的保证。"
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 大模型代码生成存在幻觉且收敛慢，需要无需微调的高效改进方法。
method: 提出预算化的合成-执行-修复循环，先检索代码上下文再生成并基于测试反馈修复。
result: "在HumanEval上达到87.2%的pass@1，超过CodeAgent基线。"
conclusion: 验证了检索先行的代理式迭代细化能显著提升代码生成可靠性。
---

## Abstract
We present Agentic Retrieval-Augmented Code Synthesis (ARCS), a system that improves LLM-based code generation without fine-tuning. ARCS operates through a budgeted synthesize–execute–repair loop over a frozen model: it retrieves relevant code context before generation, proposes candidates, executes them against tests, and repairs based on execution feedback. This retrieval-before-generation design reduces hallucination and accelerates convergence. We formalize ARCS as a state-action process with provable guarantees on termination, monotonic improvement, and bounded cost. A tiered controller (Small/Medium/Large) trades latency for accuracy predictably. On HumanEval, ARCS achieves up to 87.2\% pass@1 with Llama-3.1-405B, surpassing CodeAgent (82.3\%) while using simpler control than tree-search methods. On TransCoder, it achieves $\geq 90\%$ accuracy on most translation pairs. On a LANL scientific corpus, it improves CodeBLEU by +0.115 over baseline RAG. ARCS provides a practical, reproducible approach to reliable code synthesis using existing LLM checkpoints.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
代理式检索增强代码合成与执行修复循环提升大模型代码生成。

### 2. 核心内容
大模型代码生成常受幻觉与收敛慢困扰，且难以微调。本文提出ARCS，一种无需微调的代理式检索增强代码合成系统，通过先检索上下文再生成、执行测试并迭代修复的预算化合成-执行-修复循环工作。在HumanEval上以Llama-3.1-405B达到87.2%的pass@1，超越CodeAgent，并给出终止性与有界成本的保证。

### 3. 对应检索需求
application of large language models to software engineering tasks such as code generation and defect detection。

### 4. 来源与原文
- Source：ICLR-2026-Public
- OpenReview：[https://openreview.net/forum?id=qrfgXhZcG7](https://openreview.net/forum?id=qrfgXhZcG7)
