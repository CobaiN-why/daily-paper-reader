---
title: Active Model Selection for Large Language Models
title_zh: 面向大模型的主动模型选择
authors: "Yavuz Durmazkeser, Patrik Okanovic, Andreas Kirsch, Torsten Hoefler, Nezihe Merve Gürel"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=i308eYimsa"
tags: ["query:ai-se"]
score: 4.0
evidence: 在有限标注下主动选择最优大模型的框架
tldr: "现有大模型评测依赖全标注数据，成本高昂。本文提出LLM SELECTOR，首个面向大模型的主动模型选择框架，能针对给定任务自适应挑选最具信息量的查询进行标注，并借助基于评判者的预言机进一步降低标注成本。在6个基准、151个大模型上的实验表明其可将标注成本最多降低59.62%，为高效模型选型提供了实用工具。"
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 现有大模型评测与选型依赖全标注数据，标注成本高昂。
method: 提出主动模型选择框架，自适应选取信息量大的查询并借助评判者预言机标注。
result: "在6个基准151个模型上将标注成本最多降低59.62%。"
conclusion: 为低标注成本下的大模型选型与评测提供了高效方法。
---

## Abstract
We introduce LLM SELECTOR, the first framework for active model selection of Large Language Models (LLMs). Unlike prior evaluation and benchmarking approaches that rely on fully annotated datasets, LLM SELECTOR efficiently identifies the best LLM with limited annotations. In particular, for any given task, LLM SELECTOR adaptively selects a small set of queries to annotate that are most informative about the best model for the task. To further reduce annotation cost, we leverage a judge-based oracle annotation model. Through extensive experiments on 6 benchmarks with 151 LLMs, we show that LLM SELECTOR reduces annotation costs by up to 59.62% when selecting the best and near-best LLM for the task.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
在有限标注下主动选择最优大模型的框架。

### 2. 核心内容
现有大模型评测依赖全标注数据，成本高昂。本文提出LLM SELECTOR，首个面向大模型的主动模型选择框架，能针对给定任务自适应挑选最具信息量的查询进行标注，并借助基于评判者的预言机进一步降低标注成本。在6个基准、151个大模型上的实验表明其可将标注成本最多降低59.62%，为高效模型选型提供了实用工具。

### 3. 对应检索需求
large language models and their applications。

### 4. 来源与原文
- Source：ICLR-2026-Rejected-Public
- OpenReview：[https://openreview.net/forum?id=i308eYimsa](https://openreview.net/forum?id=i308eYimsa)
