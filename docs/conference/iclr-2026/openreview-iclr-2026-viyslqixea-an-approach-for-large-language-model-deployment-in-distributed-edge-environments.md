---
title: An Approach for Large Language Model Deployment in Distributed Edge Environments
title_zh: 一种面向分布式边缘环境的大语言模型部署方法
authors: "Partha BP, Kowsik Nandagopan D, Anand M"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=viySlQiXEA"
tags: ["query:ai-se"]
score: 4.0
evidence: 面向边缘部署的多大模型协作
tldr: 大模型在资源受限设备上部署时面临一致性与效率问题。本文探索用多智能体方式让多个大模型协同工作，先由两个模型生成多个答案，再由另一个大模型融合，并比较全精度与INT8量化对性能的影响。在Natural Questions数据集上的实验表明，组合较小模型可获得更准确稳定的答案，为受限环境下的模型部署提供参考。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 大模型在资源受限设备上部署时存在一致性与效率不足的问题。
method: 采用多模型协作，由两个模型生成答案再由第三个模型融合，并比较量化前后性能。
result: 实验显示组合较小模型能得到更准确稳定的答案，量化对性能有可比较的影响。
conclusion: 为边缘受限环境下提升大模型答案质量与稳定性提供了多模型协作思路。
---

## Abstract
Large Language Models (LLMs) have made a huge impact on tasks like question answering and text generation. However, they still struggle with consistency and efficiency, especially when deployed on resource-limited devices. In this paper, we explore using multiple LLMs to work together in a multi-agent system to improve performance. We use two large language models to generate multiple answers, and then combine the answers using another large language model. We also look at how reducing the precision of these models using quantization affects performance, comparing full-precision and INT8 versions. Our experiments, using questions from the Natural Questions dataset, show that combining smaller models results in more accurate and stable answers than relying on just one model. Quantization helps make the models more efficient, without sacrificing too much performance, making them easier to deploy on devices with limited computational power.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
面向边缘部署的多大模型协作。

### 2. 核心内容
大模型在资源受限设备上部署时面临一致性与效率问题。本文探索用多智能体方式让多个大模型协同工作，先由两个模型生成多个答案，再由另一个大模型融合，并比较全精度与INT8量化对性能的影响。在Natural Questions数据集上的实验表明，组合较小模型可获得更准确稳定的答案，为受限环境下的模型部署提供参考。

### 3. 对应检索需求
large language models and their applications。

### 4. 来源与原文
- Source：ICLR-2026-Rejected-Public
- OpenReview：[https://openreview.net/forum?id=viySlQiXEA](https://openreview.net/forum?id=viySlQiXEA)
