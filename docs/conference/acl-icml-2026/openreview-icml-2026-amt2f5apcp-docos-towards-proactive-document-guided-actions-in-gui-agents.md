---
title: "DocOS: Towards Proactive Document-Guided Actions in GUI Agents"
title_zh: DocOS：迈向GUI智能体中主动的文档引导动作
authors: "Jingjing Liu, Ziye Huang, Zihao Cheng, Zeming Liu, Jiahong Wu, Yuhang Guo, Kehai Chen, Yunhong Wang, Haifeng Wang"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf/e25e37a6177e0dacb5b6469f6171994b6ea0534f.pdf"
tags: ["query:ai-se"]
score: 4.0
evidence: GUI智能体主动检索文档以处理长尾任务
tldr: GUI智能体虽能自动操作设备，但主要依赖预训练或指令微调得到的静态参数知识，面对需要明确流程知识的长尾任务时往往只能低效试错。作者提出主动文档引导动作这一新范式，让智能体在开放网络环境中自主检索相关文档并据此解决问题，并构建评测基准来检验该能力。该工作将文档检索与智能体行动结合，为提升GUI智能体在长尾任务上的泛化性提供了新思路，但与代码生成类软件工程任务关联较弱。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: GUI智能体依赖静态参数知识，难以应对需要流程知识的长尾任务，只能低效试错。
method: 提出主动文档引导动作范式，使智能体在开放网络环境中自主检索相关文档并据此执行操作，并构建评测基准。
result: 该范式让智能体借助外部文档解决长尾任务，提升了任务处理的适应性与效率。
conclusion: 为结合文档检索的智能体行动提供了新方向，但与代码软件工程任务关联有限。
---

## Abstract
While Graphical User Interface (GUI) agents have shown promising performance in automated device interaction, they primarily depend on static parametric knowledge from pre-training or instruction tuning. This reliance fundamentally limits their ability to handle long-tailed tasks that require explicit procedural knowledge absent from model parameters, often forcing agents to resort to inefficient and brittle trial-and-error exploration. To mitigate this limitation, we introduce Proactive Document-Guided Action for GUI agents in dynamic, open-web environments, a novel paradigm that mirrors human problem-solving by enabling agents to autonomously search for relevant documentation to resolve long-tailed tasks. To evaluate agents' capability in this paradigm, we propose DocOS, a benchmark designed to assess document-guided problem solving in fully interactive environments. DocOS requires agents to autonomously navigate a web browser, locate relevant online documentation, comprehend procedural instructions, and faithfully ground them into executable GUI actions. Extensive experiments reveal that progress is strictly constrained by dual bottlenecks: agents struggle to reliably locate relevant information during proactive search and frequently fail to faithfully ground retrieved instructions into precise actions, pointing toward document-guided interaction as a crucial pathway for enabling self-evolving GUI agents in dynamic environments.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
GUI智能体主动检索文档以处理长尾任务。

### 2. 核心内容
GUI智能体虽能自动操作设备，但主要依赖预训练或指令微调得到的静态参数知识，面对需要明确流程知识的长尾任务时往往只能低效试错。作者提出主动文档引导动作这一新范式，让智能体在开放网络环境中自主检索相关文档并据此解决问题，并构建评测基准来检验该能力。该工作将文档检索与智能体行动结合，为提升GUI智能体在长尾任务上的泛化性提供了新思路，但与代码生成类软件工程任务关联较弱。

### 3. 对应检索需求
autonomous agents for coding tasks。

### 4. 来源与原文
- Source：ICML-2026-Accepted
- OpenReview：[https://openreview.net/forum?id=AmT2F5APcp](https://openreview.net/forum?id=AmT2F5APcp)
