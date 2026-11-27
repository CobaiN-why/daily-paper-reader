---
title: "FreeRet: MLLMs as Training-Free Retrievers"
title_zh: FreeRet：多模态大模型作为免训练检索器
authors: "Yuhan Zhu, Xiangyu Zeng, Chenting Wang, Xinhao Li, Yicheng Xu, Ziang Yan, Yi Wang, Limin Wang"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=OxDdAscau3"
tags: ["query:ai-se"]
score: 5.0
evidence: 将现成多模态大模型转为免训练检索器
tldr: 多模态大模型作为混合模态检索基础时通常需要大量额外训练才能转为对比编码器。本文提出即插即用框架FreeRet，无需额外训练即可将任意多模态大模型变为两阶段检索器：先直接从模型提取语义嵌入进行快速候选搜索，再利用其推理能力精细重排。框架还通过绕过词法对齐层、引入显式先验等方式提升表示质量，为大模型在检索任务中的免训练应用提供了新思路。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 多模态大模型用于检索常需大量后训练转为对比编码器，成本高且不够灵活。
method: 提出免训练框架FreeRet，利用模型直接生成的语义嵌入做候选搜索并结合推理能力重排。
result: 该框架在无需额外训练的情况下实现有效的两阶段多模态检索。
conclusion: FreeRet为大模型在混合模态检索中的即插即用应用提供了可行路径。
---

## Abstract
Multimodal large language models (MLLMs) are emerging as versatile foundations for mixed-modality retrieval.
Yet, they often require heavy post-hoc training to convert them into contrastive encoders for retrieval.
This work asks: \textit{Can off-the-shelf MLLMs serve as powerful retrievers without additional training?}
We present \textbf{FreeRet}, a plug‑and‑play framework that turns any MLLM into a two‑stage retriever.
FreeRet first derives semantically grounded embeddings directly from the model for fast candidate search, and then exploits its reasoning ability for precise reranking.
The framework contributes three advances: bypassing lexical alignment layers to obtain semantically faithful embeddings, conditioning representation generation with explicit priors, and mitigating framing effect in reranking via neutral choice framing.
On the MMEB and MMEB-V2 benchmarks spanning 46 datasets, FreeRet substantially outperforms models trained on millions of pairs.
Beyond benchmarks, FreeRet is model-agnostic and scales seamlessly across MLLM families and sizes, preserves their generative abilities, supports arbitrary modality combinations, and unifies retrieval, reranking, and generation into end-to-end RAG within a single model.
Our findings demonstrate that pretrained MLLMs, when carefully harnessed, can serve as strong retrieval engines without training, closing a critical gap in their role as generalists.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
将现成多模态大模型转为免训练检索器。

### 2. 核心内容
多模态大模型作为混合模态检索基础时通常需要大量额外训练才能转为对比编码器。本文提出即插即用框架FreeRet，无需额外训练即可将任意多模态大模型变为两阶段检索器：先直接从模型提取语义嵌入进行快速候选搜索，再利用其推理能力精细重排。框架还通过绕过词法对齐层、引入显式先验等方式提升表示质量，为大模型在检索任务中的免训练应用提供了新思路。

### 3. 对应检索需求
large language models and their applications。

### 4. 来源与原文
- Source：ICLR-2026-Rejected-Public
- OpenReview：[https://openreview.net/forum?id=OxDdAscau3](https://openreview.net/forum?id=OxDdAscau3)
