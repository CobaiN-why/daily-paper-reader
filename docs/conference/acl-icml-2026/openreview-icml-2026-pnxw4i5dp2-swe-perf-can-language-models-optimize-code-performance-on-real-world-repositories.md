---
title: "SWE-Perf: Can Language Models Optimize Code Performance on Real-World Repositories?"
title_zh: SWE-Perf：语言模型能否优化真实仓库中的代码性能
authors: "Xinyi He, Qian Liu, Mingzhe Du, Lin Yan, ZhiJie Fan, Yiming Huang, Yin Zheng, Zejian Yuan, Zejun MA"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf/fff904133978987916773f3d0946c8d70734659e.pdf"
tags: ["query:ai-se"]
score: 8.0
evidence: 评测大模型在仓库级代码性能优化上的基准
tldr: 代码性能优化对生产系统至关重要，但大模型在仓库级代码性能提升上的能力尚缺乏系统评测。SWE-Perf从流行GitHub仓库的性能改进PR中构建140个实例，每个包含代码库、目标函数与性能需求。该基准首次系统评估大模型在真实仓库中的性能优化表现，为软件工程自动化研究提供了新评测维度。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 大模型在仓库级代码性能优化上的能力缺乏系统评测基准。
method: 从真实GitHub性能改进PR构建140个含代码库与目标函数的评测实例。
result: 首次系统评估大模型在真实仓库场景下的性能优化表现。
conclusion: 为软件工程中的性能优化自动化研究提供了专门评测基准。
---

## Abstract
Code performance optimization is paramount in real-world software engineering and critical for production-level systems. While Large Language Models (LLMs) have demonstrated impressive capabilities in code generation and bug fixing, their proficiency in enhancing code performance at the repository level remains largely unexplored. To address this gap, we introduce SWE-Perf, the first benchmark specifically designed to systematically evaluate LLMs on code performance optimization tasks within authentic repository contexts. SWE-Perf comprises 140 carefully curated instances, each derived from performance-improving pull requests from popular GitHub repositories. Each benchmark instance includes the relevant codebase, target functions, performance-related tests, expert-authored patches, and executable environments. Through a comprehensive evaluation of representative methods that span file-level and repo-level approaches (e.g., Agentless and OpenHands), we reveal a substantial capability gap between existing LLMs and expert-level optimization performance, highlighting critical research opportunities in this emerging field.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
评测大模型在仓库级代码性能优化上的基准。

### 2. 核心内容
代码性能优化对生产系统至关重要，但大模型在仓库级代码性能提升上的能力尚缺乏系统评测。SWE-Perf从流行GitHub仓库的性能改进PR中构建140个实例，每个包含代码库、目标函数与性能需求。该基准首次系统评估大模型在真实仓库中的性能优化表现，为软件工程自动化研究提供了新评测维度。

### 3. 对应检索需求
software engineering tasks and automation。

### 4. 来源与原文
- Source：ICML-2026-Accepted
- OpenReview：[https://openreview.net/forum?id=pNxw4i5Dp2](https://openreview.net/forum?id=pNxw4i5Dp2)
