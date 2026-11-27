---
title: "MulFCoder: Framework-conditioned Multi-agent for MLLM-based Multi-framework Front-end Code Generation"
title_zh: MulFCoder：面向多框架前端代码生成的框架条件化多智能体方法
authors: "Jie Wu, Haoran Ma, Shisong Tang, Yulin Xu, Xiaoyu Kang, Jiechao Gao"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf/f4a13100d2374401899019eb2c56b7596c583504.pdf"
tags: ["query:ai-se"]
score: 9.0
evidence: 多智能体多模态大模型多框架前端代码生成
tldr: 从UI截图生成可运行前端代码长期是自动化软件工程难题，现有方法多局限于HTML/CSS，React/Vue/Angular等多框架生成不足。MulFCoder提出框架条件化多智能体方法，将框架约束编码为可判定规则空间，由定位、规划、编码等智能体协同生成代码。实验表明其能显著缩小多框架生成差距，提升前端代码生成质量。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 多框架前端代码生成研究不足，简单改提示难以应对框架特异性错误。
method: 提出框架条件化多智能体方法，将框架约束编码为规则空间，由多个智能体分工生成代码。
result: 实验显示该方法在多框架前端代码生成上明显优于现有基线。
conclusion: 显式编码框架约束的多智能体设计有效提升前端代码生成可用性。
---

## Abstract
Generating runnable front-end code from UI screenshots is a long-standing goal in automated software engineering.
Existing MLLM-based methods predominantly focused on HTML/CSS, leaving multi-framework generation for React/Vue/Angular underexplored.
Naively modifying prompts leads to substantial performance gaps across multi-framework and highly framework-specific error modes.
To address this, we propose MulFCoder, a framework-conditioned multi-agent method that explicitly encodes framework constraints to bring multi-framework differences into a decidable rule space.
MulFCoder orchestrates four agents: 
Grounder constructs an ElementTable, ContentTable, and macro-layout regions from detected UI elements; 
Planner builds a DOM-like hierarchical layout tree, produces a task schedule, and derives a framework-specific file Contract; 
Writer generates structured file writes or patches within a restricted edit window; 
Judger enforces lightweight, framework-conditioned constraints to accept or reject updates and trigger bounded repairs, preventing drift and deadlocks without expensive builds.
Experiments demonstrate that MulFCoder substantially improves compilation success rate and reduces framework-specific errors, with particularly pronounced gains on Angular.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
多智能体多模态大模型多框架前端代码生成。

### 2. 核心内容
从UI截图生成可运行前端代码长期是自动化软件工程难题，现有方法多局限于HTML/CSS，React/Vue/Angular等多框架生成不足。MulFCoder提出框架条件化多智能体方法，将框架约束编码为可判定规则空间，由定位、规划、编码等智能体协同生成代码。实验表明其能显著缩小多框架生成差距，提升前端代码生成质量。

### 3. 对应检索需求
application of large language models to software engineering tasks such as code generation and defect detection。

### 4. 来源与原文
- Source：ICML-2026-Accepted
- OpenReview：[https://openreview.net/forum?id=xUW3aH4ie3](https://openreview.net/forum?id=xUW3aH4ie3)
