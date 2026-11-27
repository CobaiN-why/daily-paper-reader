---
title: Efficient Code Analysis via Graph Representation Learning-Guided Large Language Models
title_zh: 基于图表示学习引导大模型的高效代码分析
authors: "Hang Gao, Tao Peng, Baoquan Cui, Hong Huang, Fengge Wu, Junsuo Zhao, Jian Zhang"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf/3bec2b6a1cbfdef0710ff1e6187fd2532aa75747.pdf"
tags: ["query:ai-se"]
score: 8.0
evidence: 基于大模型的代码分析与恶意行为检测
tldr: 大模型虽提升了代码分析能力，却难以在大量良性代码中定位跨文件分散的恶意行为，复杂依赖关系容易被淹没。作者提出图中心注意力获取流程，将项目解析为代码图，用大模型编码节点的语义与结构信号，在稀疏监督下训练图神经网络做初步检测，并通过解释其预测定位高风险代码区域以引导大模型聚焦。实验表明该方法提升了恶意行为定位效率。这为基于大模型的缺陷与漏洞检测提供了可复用方法。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 大模型难以在庞杂代码中定位跨文件分散的恶意行为，依赖关系信息容易丢失。
method: 将项目解析为代码图，用大模型编码节点，训练GNN初步检测并引导大模型聚焦关键区域。
result: 方法在稀疏监督下有效提升了恶意行为的定位能力与效率。
conclusion: 图引导的大模型代码分析为缺陷与漏洞检测类软件工程任务提供了新思路。
---

## Abstract
Large Language Models (LLMs) have significantly advanced code analysis tasks, yet they struggle to detect malicious behaviors fragmented across files, whose intricate dependencies easily get lost in the vast amount of benign code. We therefore propose a graph-centric attention acquisition pipeline that enhances LLMs' ability to localize malicious behavior. The approach parses a project into a code graph, uses an LLM to encode nodes with semantic and structural signals, and trains a Graph Neural Network (GNN) under sparse supervision. The GNN performs an initial detection, and by interpreting these predictions, identifies key code sections that are most likely to contain malicious behavior. These influential regions are then used to guide the LLM's attention for in-depth analysis. This strategy significantly reduces interference from irrelevant context while maintaining low annotation costs. Extensive experiments show that the method consistently outperforms existing approaches on multiple public and custom datasets, highlighting its potential for practical deployment in software security scenarios. Codes can be found in https://github.com/Epiphaniespt/GMLLM.git.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
基于大模型的代码分析与恶意行为检测。

### 2. 核心内容
大模型虽提升了代码分析能力，却难以在大量良性代码中定位跨文件分散的恶意行为，复杂依赖关系容易被淹没。作者提出图中心注意力获取流程，将项目解析为代码图，用大模型编码节点的语义与结构信号，在稀疏监督下训练图神经网络做初步检测，并通过解释其预测定位高风险代码区域以引导大模型聚焦。实验表明该方法提升了恶意行为定位效率。这为基于大模型的缺陷与漏洞检测提供了可复用方法。

### 3. 对应检索需求
application of large language models to software engineering tasks such as code generation and defect detection。

### 4. 来源与原文
- Source：ICML-2026-Accepted
- OpenReview：[https://openreview.net/forum?id=GNieZ8Z5V5](https://openreview.net/forum?id=GNieZ8Z5V5)
