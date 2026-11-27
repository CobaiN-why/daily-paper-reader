---
title: "SWE-Compass: Towards Unified Evaluation of Agentic Coding Abilities for Large Language Models"
title_zh: SWE-Compass：面向大语言模型智能体编码能力的统一评测
authors: "Jingxuan Xu, Ken Deng, Weihao Li, Songwei Yu, Haoyang Huang, Xinping Lei, Yifan Yao, Huaixi Tang, Zhiyi Lai, Kepeng Lei, Zizheng Zhan, Yanan Wu, Chenchen Zhang, Wenqiang Zhu, Wen Xiang, Zongxian Feng, Han Li, Junqi Xiong, Dailin Li, Zuchen Gao, Kun Wu, Yuanxing Zhang, Wuxuan Gong, Ziyuan Gao, Guanxiang Wang, Yirong Xue, Mengfei Xie, Xiaojiang Zhang, Jinghui Wang, Wenhao Zhuang, Zheng Lin, Huiming Wang, Zhaoxiang Zhang, Yuqun Zhang, Haotian Zhang, Ming Sun, Chen Bin, Jiaheng Liu"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf/28d65e09d693997a88bfa1c5732b002e0a6f9487.pdf"
tags: ["query:ai-se"]
score: 9.0
evidence: 面向大模型智能体编码能力的统一评测基准
tldr: 现有软件工程评测任务覆盖窄、语言偏倚强，且与真实开发流程脱节，难以全面衡量大模型编码能力。作者提出SWE-Compass基准，将异构代码评测统一为结构化框架，涵盖8类任务、8种场景和10种语言，并从真实GitHub拉取请求中筛选出2000个高质量实例。该基准更贴近真实开发者工作流，为智能体编码能力的统一评估提供了标准化工具。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 现有软件工程评测任务覆盖窄、存在语言偏倚，且与真实开发者工作流对齐不足。
method: 构建SWE-Compass统一基准，涵盖8类任务、8种场景和10种语言，从GitHub拉取请求中筛选2000个实例。
result: 该基准将异构代码评测整合为结构化且贴近生产环境的框架，覆盖多个此前未被充分探索的维度。
conclusion: SWE-Compass为评估大模型智能体编码能力提供了更全面、贴近真实开发的标准化方案。
---

## Abstract
Evaluating large language models (LLMs) for software engineering has been limited by narrow task coverage, language bias, and insufficient alignment with real-world developer workflows. Existing benchmarks often focus on algorithmic problems or Python-centric bug fixing, leaving critical dimensions of software engineering underexplored. To address these gaps, we introduce SWE-Compass, a comprehensive benchmark that unifies heterogeneous code-related evaluations into a structured and production-aligned framework. SWE-Compass spans 8 task types, 8 programming scenarios, and 10 programming languages, with 2000 high-quality instances curated from authentic GitHub pull requests and refined through systematic filtering and validation. We benchmark ten state-of-the-art LLMs under two agentic frameworks, SWE-Agent and Claude Code, revealing a clear hierarchy of difficulty across task types, languages, and scenarios. Moreover, by aligning evaluation with real-world developer practices, we hope SWE-Compass can provide a rigorous and reproducible foundation for diagnosing and advancing agentic coding capabilities in large language models.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
面向大模型智能体编码能力的统一评测基准。

### 2. 核心内容
现有软件工程评测任务覆盖窄、语言偏倚强，且与真实开发流程脱节，难以全面衡量大模型编码能力。作者提出SWE-Compass基准，将异构代码评测统一为结构化框架，涵盖8类任务、8种场景和10种语言，并从真实GitHub拉取请求中筛选出2000个高质量实例。该基准更贴近真实开发者工作流，为智能体编码能力的统一评估提供了标准化工具。

### 3. 对应检索需求
autonomous agents for coding tasks。

### 4. 来源与原文
- Source：ICML-2026-Accepted
- OpenReview：[https://openreview.net/forum?id=MHXIvy3bsb](https://openreview.net/forum?id=MHXIvy3bsb)
