---
title: "RANGER: Repository-Level Agent for Graph Enhanced Retrieval"
title_zh: RANGER：图增强检索的仓库级智能体
authors: "Pratik Shah, Rajat Ghosh, Aryan Singhal, Debojyoti Dutta"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=EPTVoeaz7Y"
tags: ["query:ai-se"]
score: 8.0
evidence: 面向软件工程代码检索的仓库级智能体
tldr: 通用自动化软件工程中的代码补全、修复、问答等任务都需要可靠的代码检索系统，但现有工作多聚焦代码实体查询而忽视自然语言查询。本文提出RANGER仓库级代码检索智能体，先构建整个仓库的知识图谱，再结合图增强检索处理两类查询。该工作填补了自然语言查询检索的空白，为软件工程自动化任务提供了更强的基础能力。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 软件工程任务需要同时支持代码实体查询与自然语言查询的代码检索系统。
method: 构建仓库知识图谱，并以图增强检索的智能体统一处理两类查询。
result: 该方法在代码检索任务上兼顾代码实体查询与自然语言查询的需求。
conclusion: 为自动化软件工程中的代码检索提供了更通用的仓库级智能体方案。
---

## Abstract
General-purpose automated software engineering (ASE) includes tasks such as code completion, retrieval, repair, QA, and summarization. These tasks require a code retrieval system that can handle specific queries about code entities, or code entity queries (for example, locating a specific class or retrieving the dependencies of a function), as well as general queries without explicit code entities, or natural language queries (for example, describing a task and retrieving the corresponding code). We present RANGER, a repository-level code retrieval agent designed to address both query types, filling a gap in recent works that have focused primarily on code-entity queries. We first present a tool that constructs a comprehensive knowledge graph of the entire repository, capturing hierarchical and cross-file dependencies down to the variable level, and augments graph nodes with textual descriptions and embeddings to bridge the gap between code and natural language. RANGER then operates on this graph through a dual-stage retrieval pipeline. Entity-based queries are answered through fast Cypher lookups, while natural language queries are handled by MCTS-guided graph exploration. We evaluate RANGER across four diverse benchmarks that represent core ASE tasks, including code search, question answering, cross-file dependency retrieval, and repository-level code completion. On CodeSearchNet and RepoQA, it outperforms retrieval baselines that use embeddings from strong models such as Qwen3-8B. On RepoBench, it achieves superior cross-file dependency retrieval over baselines, and on CrossCodeEval, pairing RANGER with BM25 delivers the highest exact match rate in code completion compared to other RAG methods.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
面向软件工程代码检索的仓库级智能体。

### 2. 核心内容
通用自动化软件工程中的代码补全、修复、问答等任务都需要可靠的代码检索系统，但现有工作多聚焦代码实体查询而忽视自然语言查询。本文提出RANGER仓库级代码检索智能体，先构建整个仓库的知识图谱，再结合图增强检索处理两类查询。该工作填补了自然语言查询检索的空白，为软件工程自动化任务提供了更强的基础能力。

### 3. 对应检索需求
autonomous agents for coding tasks。

### 4. 来源与原文
- Source：ICLR-2026-Public
- OpenReview：[https://openreview.net/forum?id=EPTVoeaz7Y](https://openreview.net/forum?id=EPTVoeaz7Y)
