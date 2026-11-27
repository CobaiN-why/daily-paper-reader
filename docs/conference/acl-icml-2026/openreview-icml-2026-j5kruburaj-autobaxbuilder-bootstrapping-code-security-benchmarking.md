---
title: "AutoBaxBuilder: Bootstrapping Code Security Benchmarking"
title_zh: AutoBaxBuilder：面向代码安全基准的自举式构建
authors: "Tobias von Arx, Niels Mündler, Mark Vero, Maximilian Baader, Martin Vechev"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf/abdc41f70c4a24446baaad18991dcc2dc684f5c8.pdf"
tags: ["query:ai-se"]
score: 8.0
evidence: 评估大模型生成代码的安全性
tldr: 大模型在软件工程中被广泛采用，但其生成代码常含安全漏洞，而人工构建的安全基准易受数据污染且难以持续升级。作者提出AutoBaxBuilder自动化流水线，从现有资源自动生成代码安全评测任务，并不断提升难度以挑战更强模型。该工作使LLM生成代码的正确性与安全性评估更加可靠，为大模型代码安全研究提供可扩展的基准支撑。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 大模型生成代码常含安全漏洞，而人工构建的安全基准易被训练数据污染且难以扩展与升级。
method: 提出AutoBaxBuilder自动化流水线，从现有资源自动生成并扩充代码安全评测任务，提升难度。
result: 该流水线可自动生成多样且具挑战性的代码安全基准任务，避免人工构建的污染与饱和问题。
conclusion: AutoBaxBuilder为大模型生成代码的安全与正确性评估提供了可扩展、可持续的基准方案。
---

## Abstract
As large language models (LLMs) see wide adoption in software engineering, the reliable assessment of the correctness and security of LLM-generated code is crucial. Notably, prior work showed that LLMs are prone to generating code with security vulnerabilities, highlighting that security is often overlooked. These insights were enabled by specialized benchmarks crafted by security experts through significant manual effort. However, benchmarks (i) inevitably end up contaminating training data, (ii) must extend to new tasks to provide a more complete picture, and (iii) must increase in difficulty to challenge more capable LLMs. In this work, we address these challenges and present AutoBaxBuilder, an automated pipeline that generates code security benchmarking tasks from scratch. It leverages the code-understanding capabilities of LLMs combined with robust reliability checks to construct functional tests and end-to-end security-probing exploits. The quality of the pipeline is quantitatively confirmed by aligning its predictions with an expert-written baseline and qualitatively validated through manual soundness verification. We use AutoBaxBuilder to construct a new benchmark and release it to the public as AutoBaxBench, together with a thorough evaluation on contemporary LLMs. AutoBaxBuilder generates new tasks in under 2 hours, for less than USD 4. Including a manual verification, this reduces the required human effort for benchmark construction by a factor of 12.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
评估大模型生成代码的安全性。

### 2. 核心内容
大模型在软件工程中被广泛采用，但其生成代码常含安全漏洞，而人工构建的安全基准易受数据污染且难以持续升级。作者提出AutoBaxBuilder自动化流水线，从现有资源自动生成代码安全评测任务，并不断提升难度以挑战更强模型。该工作使LLM生成代码的正确性与安全性评估更加可靠，为大模型代码安全研究提供可扩展的基准支撑。

### 3. 对应检索需求
大模型安全。

### 4. 来源与原文
- Source：ICML-2026-Accepted
- OpenReview：[https://openreview.net/forum?id=J5KrubuRAJ](https://openreview.net/forum?id=J5KrubuRAJ)
