---
title: "Auto-SWE-Bench: A Framework for the Scalable Generation of Software Engineering Benchmark from Open-Source Repositories"
title_zh: Auto-SWE-Bench：从开源仓库可扩展生成软件工程基准的框架
authors: "Lilin Wang, Lucas Ramalho, Alan Celestino, Phuc Anthony Pham, yu liu, Umang Kumar Sinha, Andres Portillo, Onassis Osunwa, Gabriel Maduekwe"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=Gxw1EDSm9S"
tags: ["query:ai-se"]
score: 8.0
evidence: 为大模型软件工程任务自动生成仓库级编码基准的框架
tldr: 现有SWE-bench类基准依赖人工整理、数据集静态且集中于Python缺陷修复，难以覆盖真实软件工程需求。本文提出全自动框架SWE-Bench Atlas，通过端到端流水线持续采集开源GitHub项目的实时拉取请求，自动生成大规模、多语言、多样化的仓库级编码任务，涵盖缺陷修复与功能请求。该框架为评估大模型在复杂软件工程任务上的能力提供了可扩展的高保真基准来源。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 现有软件工程基准依赖人工整理、数据静态且偏重Python缺陷修复，覆盖不足。
method: 提出全自动框架SWE-Bench Atlas，持续采集开源仓库拉取请求生成多样化仓库级编码任务。
result: 该框架可生成大规模、多语言、涵盖缺陷修复与功能请求的真实软件工程基准。
conclusion: 该工作为大模型软件工程能力评估提供了可扩展的高保真基准生成方案。
---

## Abstract
Benchmarks like SWE-bench have shaped the evaluation of Large Language Models (LLMs) on complex software engineering tasks. However, these efforts remain limited by manual curation, static datasets, and a focus on Python-based bug fixes. We introduce SWE-Bench Atlas, a fully automated framework for generating high-fidelity, large-scale, multilingual, and diverse real-world repository-level coding tasks from open-source GitHub projects.Unlike synthetic frameworks or manually curated sets, SWE-Bench Atlas introduces an end-to-end pipeline that continuously harvests live pull requests to capture a broad spectrum of real-world software engineering demands, including both bug fixes and feature requests. The framework operates via a five-stage automated pipeline: (1) a Sourcing Module that identifies high-quality pull requests across diverse languages; (2) a Neuro-Symbolic Dockerization System that utilizes tool-augmented and template-guided synthesis to enforce strict reproducibility; (3) a State-Differential Test Oracle Extraction that integrates Adaptive Log Parsing to verify both regressions and feature requests across heterogeneous build system; (4) an Automated Quality Assurance to ensure environmental determinism; and (5) a Hint-Guided Trajectory Synthesis module that converts model-breaking instances into high-value training data. Our initial benchmark consists of 11,133 instances from 3,971 repositories across 11 languages. On a subset of 1,782 instances of this benchmark, today’s strongest models perform as follows: claude-sonnet-4.5 (36.20% pass@10), gpt-5-2025-08-07 (34.57%), gemini/gemini-2.5-pro (16.89%), and gpt-4o (18.24%). Supplementing our findings, a public release of 500-task dataset, together with evaluation scripts is included in the supplementary material. We further demonstrate the utility of our dataset by showing that fine-tuning on SWE-Bench Atlas instances yields measurable improvements on the SWE-bench Multilingual benchmark. By automatically producing dynamic, polyglot, and verifiable tasks, SWE-Bench Atlas enables scalable evaluation and advancement of AI coding and reasoning abilities of next-generation AI systems.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
为大模型软件工程任务自动生成仓库级编码基准的框架。

### 2. 核心内容
现有SWE-bench类基准依赖人工整理、数据集静态且集中于Python缺陷修复，难以覆盖真实软件工程需求。本文提出全自动框架SWE-Bench Atlas，通过端到端流水线持续采集开源GitHub项目的实时拉取请求，自动生成大规模、多语言、多样化的仓库级编码任务，涵盖缺陷修复与功能请求。该框架为评估大模型在复杂软件工程任务上的能力提供了可扩展的高保真基准来源。

### 3. 对应检索需求
application of large language models to software engineering tasks such as code generation and defect detection。

### 4. 来源与原文
- Source：ICLR-2026-Rejected-Public
- OpenReview：[https://openreview.net/forum?id=Gxw1EDSm9S](https://openreview.net/forum?id=Gxw1EDSm9S)
