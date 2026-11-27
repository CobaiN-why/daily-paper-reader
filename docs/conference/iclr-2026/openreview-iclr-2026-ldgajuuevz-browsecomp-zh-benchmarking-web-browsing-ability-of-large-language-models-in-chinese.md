---
title: "BrowseComp-ZH: Benchmarking Web Browsing Ability of Large Language Models in Chinese"
title_zh: BrowseComp-ZH：评估大语言模型中文网页浏览能力的基准
authors: "Peilin Zhou, Junling Liu, Xiang Ying, Can Zhang, Yifan Shao, Qichen Ye, Dading Chong, Zhiling Jin, Chenxuan Xie, Meng Cao, Yuxin Gu, Sixin Hong, Jing Ren, Jian Chen, Chao Liu, Yining Hua, Sunghun Kim"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=LDGAjUuEVZ"
tags: ["query:ai-se"]
score: 4.0
evidence: 评估大模型智能体中文网页浏览能力的基准
tldr: 现有面向大模型智能体的网页浏览基准几乎只覆盖英文，忽视了中文网络在语言、基础设施与检索上的独特挑战。作者构建了BrowseComp-ZH，一个由母语者从零撰写、非翻译而来的高难度中文基准，真实反映中文信息检索行为与文化语境。该基准为大模型智能体在中文网络环境下的浏览与推理能力提供了更有针对性的评估工具，但主要涉及通用智能体而非软件工程任务。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 现有网页浏览基准仅覆盖英文，忽视中文网络生态的语言与检索挑战。
method: 由母语者从零构建高难度中文网页浏览基准，覆盖真实信息检索行为与文化语境。
result: 该基准能更有针对性地评估大模型智能体在中文网络中的浏览与推理能力。
conclusion: 工作填补了中文网页浏览评估空白，但主要面向通用智能体而非软件工程任务。
---

## Abstract
As large language models (LLMs) evolve into web-interacting agents, their ability to retrieve and reason over real-time information has become a crucial benchmark for general intelligence. However, existing benchmarks such as BrowseComp focus solely on English, neglecting the linguistic, infrastructural, and retrieval-specific challenges posed by other information ecosystems—particularly the Chinese web. We present BrowseComp-ZH, a high-difficulty, natively-constructed benchmark designed to assess LLM agents’ web browsing abilities in Chinese. Rather than translating from English, all questions in BrowseComp-ZH are written from scratch by native speakers to reflect authentic information-seeking behaviors and cultural contexts. The dataset comprises 289 multi-hop questions across 11 diverse domains, each reverse-engineered from a short, verifiable answer and filtered through a twostage quality control pipeline to ensure retrieval hardness and answer uniqueness. We evaluate over 20 leading LLMs and agentic search systems. Despite strong language and retrieval abilities, most models perform poorly: many score below 10% accuracy, and only a few exceed 20%. Even the best system achieves just 42.9% accuracy. These results highlight the considerable difficulty of BrowseComp-ZH, where success requires not only robust retrieval strategies but also advanced multihop reasoning and information reconciliation—abilities that remain challenging for current models. BrowseComp-ZH thus serves as a stress test for web-interactive LLMs beyond English, offering a rigorous and linguistically diverse evaluation framework to guide future research on multilingual agent capabilities.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
评估大模型智能体中文网页浏览能力的基准。

### 2. 核心内容
现有面向大模型智能体的网页浏览基准几乎只覆盖英文，忽视了中文网络在语言、基础设施与检索上的独特挑战。作者构建了BrowseComp-ZH，一个由母语者从零撰写、非翻译而来的高难度中文基准，真实反映中文信息检索行为与文化语境。该基准为大模型智能体在中文网络环境下的浏览与推理能力提供了更有针对性的评估工具，但主要涉及通用智能体而非软件工程任务。

### 3. 对应检索需求
large language models and their applications。

### 4. 来源与原文
- Source：ICLR-2026-Rejected-Public
- OpenReview：[https://openreview.net/forum?id=LDGAjUuEVZ](https://openreview.net/forum?id=LDGAjUuEVZ)
