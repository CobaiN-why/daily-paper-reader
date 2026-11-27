---
title: "Rule2DRC: Benchmarking LLM Agents for DRC Script Synthesis with Execution-Guided Test Generation"
title_zh: Rule2DRC：以执行引导测试生成评测大模型智能体的DRC脚本合成
authors: "Jinuk Kim, Junsoo Byun, Donghwi Hwang, Seong-Jin Park, Hyun Oh Song"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf/93c417ae126d847f2619a4597461ac29f172cf0a.pdf"
tags: ["query:ai-se"]
score: 8.0
evidence: 以执行引导测试生成评测大模型编码智能体
tldr: 芯片设计规则需通过可执行DRC脚本校验，但把自然语言规则转成脚本耗时且需专业知识，现有基准规模小且多以代码相似度而非执行正确性评估。Rule2DRC构建含1000条规则到脚本任务的大规模基准，支持智能体合成与调试脚本，并采用执行引导的测试生成。该基准更贴近真实执行正确性，为智能体编码与测试生成研究提供可靠评测。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 自然语言规则转DRC脚本费时且需专业知识，现有基准规模小、评估不贴执行正确性。
method: 构建含1000条规则到脚本任务的大规模基准，采用执行引导测试生成评估智能体。
result: 以执行正确性而非代码相似度评测智能体脚本合成与调试能力。
conclusion: 为智能体编码与测试生成提供了贴近真实执行的评测平台。
---

## Abstract
Manufacturable chip layouts must satisfy thousands of geometry-based design rules, and design rule checking (DRC) enforces them by running executable DRC scripts on layouts. Translating natural language rules into correct DRC scripts is labor-intensive and requires specialized expertise, motivating LLM agents for DRC script synthesis and debugging. However, existing benchmarks have small evaluation sets and often evaluate scripts by code similarity rather than execution correctness, and prior machine learning-based methods either ignore execution feedback or require labeled test layouts as agent's input. To this end, we introduce Rule2DRC, a large-scale benchmark for DRC script coding agents with 1,000 rule-to-script tasks and 13,921 evaluation chip layouts for execution-based scoring. Rule2DRC provides an evaluation pipeline that measures functional correctness via DRC execution outcomes without requiring evaluation layouts as input to the agent. We also propose SplitTester, a tester agent for program selection that uses execution feedback to generate discriminative test cases and separate previously indistinguishable candidate scripts, substantially improving Best-of-N selection performance in this domain.
We release the code at https://github.com/snu-mllab/Rule2DRC.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
以执行引导测试生成评测大模型编码智能体。

### 2. 核心内容
芯片设计规则需通过可执行DRC脚本校验，但把自然语言规则转成脚本耗时且需专业知识，现有基准规模小且多以代码相似度而非执行正确性评估。Rule2DRC构建含1000条规则到脚本任务的大规模基准，支持智能体合成与调试脚本，并采用执行引导的测试生成。该基准更贴近真实执行正确性，为智能体编码与测试生成研究提供可靠评测。

### 3. 对应检索需求
coding agents for automated test generation and documentation。

### 4. 来源与原文
- Source：ICML-2026-Accepted
- OpenReview：[https://openreview.net/forum?id=alXhEw7Ogt](https://openreview.net/forum?id=alXhEw7Ogt)
