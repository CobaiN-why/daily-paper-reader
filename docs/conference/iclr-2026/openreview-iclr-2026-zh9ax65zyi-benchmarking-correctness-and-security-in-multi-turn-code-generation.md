---
title: Benchmarking Correctness and Security in Multi-Turn Code Generation
title_zh: 多轮代码生成中正确性与安全性的基准评测
authors: "Ruchit Rawal, Jeffrey Yang Fan Chiang, Chihao Shen, Jeffery Siyuan Tian, Aastha Mahajan, Tom Goldstein, Yizheng Chen"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=zH9aX65Zyi"
tags: ["query:ai-se"]
score: 8.0
evidence: 评估大模型多轮代码生成正确性与安全性的基准
tldr: AI编码助手显著提升开发效率，但现有基准多限于单轮任务，难以反映真实开发的迭代特性。本文提出MT-Sec，首个在多轮编码场景下系统评估代码正确性与安全性的基准，通过合成数据流水线将单轮任务转化为语义对齐的多轮交互序列并复用原测试套件。作者评测了32个开源与闭源模型，揭示了多轮条件下正确性与安全性的新挑战。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 现有代码生成基准多为单轮任务，无法反映真实开发的迭代特性。
method: 用合成数据流水线将单轮任务转为多轮交互序列，构建MT-Sec基准。
result: 在32个开源与闭源模型上评测，揭示多轮场景下正确性与安全性的挑战。
conclusion: 为大模型代码生成的正确性与安全性评估提供了首个多轮基准。
---

## Abstract
AI coding assistants powered by large language models (LLMs) have transformed software development, significantly boosting productivity. While existing benchmarks evaluate the correctness and security of LLM-generated code, they are typically limited to single-turn tasks that do not reflect the iterative nature of real-world development. We introduce MT-Sec, the first benchmark to systematically evaluate both correctness and security in multi-turn coding scenarios.  We construct this using a synthetic data pipeline that transforms existing single-turn tasks into semantically aligned multi-turn interaction sequences, allowing reuse of original test suites while modeling the complexity of real-world coding processes. We evaluate 32 open- and closed-source models, and 3 agent-scaffolding on MT-Sec and observe a consistent 20-27% drop in “correct & secure" outputs from single-turn to multi-turn settings--even among state-of-the-art models. Beyond full-program generation, we also evaluate models on multi-turn code-diff generation--an unexplored yet practically relevant setting--and find that models perform worse here, with increased rates of functionally incorrect and insecure outputs. Finally, we find that while agent scaffoldings boost single-turn code generation performance, they are not quite as effective in multi-turn evaluations. Together, these findings highlight the need for benchmarks that jointly evaluate correctness and security in multi-turn, real-world coding workflows.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
评估大模型多轮代码生成正确性与安全性的基准。

### 2. 核心内容
AI编码助手显著提升开发效率，但现有基准多限于单轮任务，难以反映真实开发的迭代特性。本文提出MT-Sec，首个在多轮编码场景下系统评估代码正确性与安全性的基准，通过合成数据流水线将单轮任务转化为语义对齐的多轮交互序列并复用原测试套件。作者评测了32个开源与闭源模型，揭示了多轮条件下正确性与安全性的新挑战。

### 3. 对应检索需求
application of large language models to software engineering tasks such as code generation and defect detection。

### 4. 来源与原文
- Source：ICLR-2026-Rejected-Public
- OpenReview：[https://openreview.net/forum?id=zH9aX65Zyi](https://openreview.net/forum?id=zH9aX65Zyi)
