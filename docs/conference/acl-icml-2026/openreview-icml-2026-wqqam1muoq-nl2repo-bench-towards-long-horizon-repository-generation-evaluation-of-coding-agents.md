---
title: "NL2Repo-Bench: Towards Long-Horizon Repository Generation Evaluation of Coding Agents"
title_zh: NL2Repo-Bench：面向编码智能体长周期仓库生成的评估
authors: "Jingzhe Ding, Shengda Long, Changxin PU, Ge Zhang, zhou huan, Hongwan Gao, Xiang Gao, Chao He, Yue Hou, FEI HU, Zhaojian Li, Weiran Shi, Zaiyuan Wang, Daoguang Zan, Chenchen Zhang, Xiaoxu Zhang, Chen Qizhi, Xianfu Cheng, Bo Deng, Qingshui Gu, Kai Hua, Juntao Lin, Pai Liu, Mingchen Li, Minghao Li, Xuanguang Pan, Zifan Peng, Yujia Qin, Yong Shan, Zhewen Tan, Haoran Wang, Zihan Wang, Weihao Xie, Yishuo Yuan, Jiayu Zhang, Yunfei Zhao, He Zhu, LIYA ZHU, Chenyang Zou, Ming Ding, Jianpeng Jiao, Jiaheng Liu, Minghao Liu, Qian Liu, Chongyang Tao, Jian Yang, Tong Yang, Zhaoxiang Zhang, Xinjie Chen, Wenhao Huang"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf/b48d109d4d831392d64d071013bf1beb11f3d2e9.pdf"
tags: ["query:ai-se"]
score: 9.0
evidence: 面向编码智能体长周期仓库生成的基准
tldr: 现有基准多只评估编码智能体的短周期行为，如局部代码生成或仓库修复，难以反映真实软件开发所需的长期规划能力。作者提出NL2Repo-Bench，仅给定一份自然语言需求文档和空工作区，要求智能体自主设计架构、管理依赖并生成可安装的Python仓库。该基准系统刻画了智能体在长周期推理、规划与执行上的表现，为评估自主软件开发能力提供了新标准。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 现有基准仅评估编码智能体的短周期行为，无法判断其能否支撑真实仓库构建所需的长期推理与规划。
method: 提出NL2Repo-Bench，仅给定自然语言需求文档与空工作区，要求智能体自主设计架构、管理依赖并生成完整可安装仓库。
result: 该基准系统考察了智能体在长周期规划、执行与仓库生成上的能力，填补了长期自主软件开发评估的空白。
conclusion: 为评估编码智能体能否胜任端到端仓库构建提供了新的长周期评测范式。
---

## Abstract
Recent advances in coding agents suggest rapid progress toward autonomous software development, yet existing benchmarks primarily evaluate short-horizon behaviors such as localized code generation, scaffolded completion, or repository repair, leaving it unclear whether agents can sustain coherent reasoning, planning, and execution over the extended horizons demanded by real-world repository construction. To address this gap, we introduce NL2Repo-Bench, a benchmark explicitly designed to evaluate the long-horizon repository generation from scratch: given only a single natural-language requirements document and an empty workspace, agents must autonomously design the architecture, manage dependencies, and produce a fully installable Python library. Experiments across state-of-the-art open- and closed-source models reveal that long-horizon repository generation remains largely unsolved, with even the strongest agents achieving merely 40\% average test pass rates and rarely completing an entire repository correctly. Further analysis identifies systematic long-horizon failure modes, including premature termination, loss of global coherence, fragile cross-file dependencies, and inadequate planning over hundreds of interaction steps.
These results position NL2Repo-Bench as a rigorous, execution-based testbed for evaluating sustained agentic competence and highlight long-horizon reasoning as a key bottleneck for autonomous coding agents. Our data and code are available at https://github.com/multimodal-art-projection/NL2RepoBench.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
面向编码智能体长周期仓库生成的基准。

### 2. 核心内容
现有基准多只评估编码智能体的短周期行为，如局部代码生成或仓库修复，难以反映真实软件开发所需的长期规划能力。作者提出NL2Repo-Bench，仅给定一份自然语言需求文档和空工作区，要求智能体自主设计架构、管理依赖并生成可安装的Python仓库。该基准系统刻画了智能体在长周期推理、规划与执行上的表现，为评估自主软件开发能力提供了新标准。

### 3. 对应检索需求
autonomous agents for coding tasks。

### 4. 来源与原文
- Source：ICML-2026-Accepted
- OpenReview：[https://openreview.net/forum?id=wqQam1muOQ](https://openreview.net/forum?id=wqQam1muOQ)
