---
title: "Kimi-Dev: Agentless Training as Skill Prior for SWE-agents"
title_zh: Kimi-Dev：以无智能体训练作为SWE智能体的技能先验
authors: "Zonghan Yang, Shengjie Wang, Kelin Fu, Wenyang He, Weimin Xiong, Yibo Liu, Yibo Miao, Bofei Gao, Yejie Wang, YINGWEI MA, Yanhao Li, Yue Liu, Zhenxing Hu, kaitai zhang, Shuyi Wang, Huarong Chen, Flood Sung, Yang Liu, Yang Gao, Zhilin Yang, Tianyu Liu"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=tYppHuGhxJ"
tags: ["query:ai-se"]
score: 9.0
evidence: 为软件工程智能体赋能的训练方案
tldr: "大模型在软件工程中的应用常分为多轮交互的SWE-Agent与单轮工作流的Agentless两类范式，二者被视为互斥。本文认为二者可互补，推理密集的Agentless训练能形成定位、代码编辑与自省等技能先验。作者整理训练配方并推出开源模型Kimi-Dev，在SWE-bench Verified上达到60.4%，并经微调进一步赋能SWE-Agent，为软件工程智能体训练提供了新范式。"
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: SWE-Agent与Agentless两类范式被视为互斥，缺乏对二者互补性的系统利用。
method: 整理Agentless训练配方，训练开源SWE大模型并进一步微调适配SWE-Agent。
result: "Kimi-Dev在SWE-bench Verified上达到60.4%，为工作流方法中最佳。"
conclusion: 表明Agentless训练可作为技能先验有效提升软件工程智能体性能。
---

## Abstract
Large Language Models (LLMs) are increasingly applied to software engineering (SWE), with SWE-bench as a key benchmark. Solutions are split into SWE-Agent frameworks with multi-turn interactions and workflow-based Agentless methods with single-turn verifiable steps. We argue these paradigms are not mutually exclusive: reasoning-intensive Agentless training induces skill priors, including localization, code edit, and self-reflection that enable efficient and effective SWE-Agent adaptation. In this work, we first curate the Agentless training recipe and present Kimi-Dev, an open-source SWE LLM achieving 60.4\% on SWE-bench Verified, the best among workflow approaches. With additional SFT adaptation on 5k publicly-available trajectories, Kimi-Dev powers SWE-Agents to 48.6\% pass@1, on par with that of Claude 3.5 Sonnet (241022 version). These results show that structured skill priors from Agentless training can bridge workflow and agentic frameworks for transferable coding agents.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
为软件工程智能体赋能的训练方案。

### 2. 核心内容
大模型在软件工程中的应用常分为多轮交互的SWE-Agent与单轮工作流的Agentless两类范式，二者被视为互斥。本文认为二者可互补，推理密集的Agentless训练能形成定位、代码编辑与自省等技能先验。作者整理训练配方并推出开源模型Kimi-Dev，在SWE-bench Verified上达到60.4%，并经微调进一步赋能SWE-Agent，为软件工程智能体训练提供了新范式。

### 3. 对应检索需求
autonomous agents for coding tasks。

### 4. 来源与原文
- Source：ICLR-2026-Accepted
- OpenReview：[https://openreview.net/forum?id=tYppHuGhxJ](https://openreview.net/forum?id=tYppHuGhxJ)
