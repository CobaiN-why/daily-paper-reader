---
title: "CDTP: A Large-Scale Chinese Data-Text Pair Dataset for Comprehensive Evaluation of Chinese LLMs"
title_zh: CDTP：用于全面评估中文大模型的大规模中文数据文本对数据集
authors: "Chengwei Wu, Jiapu Wang, Mingyang Gao, Xingrui Zhuo, Jipeng Guo, Runlin Lei, Haoran Luo, Tianyu Chen, Haoyi Zhou, Shirui Pan, Zechao Li"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=2GhjkigNTx"
tags: ["query:ai-se"]
score: 6.0
evidence: 面向大模型评估的大规模中文数据文本对基准
tldr: 现有大模型评测基准以英文为中心，且缺乏结构化数据，难以充分评估中文大模型。本文构建了大规模中文数据-文本对数据集CDTP，并据此提出综合性中文大模型评测基准CB-ECLLM。该基准针对中文语料以非结构化自由文本为主、缺少结构化表示的问题进行设计。工作为中文大模型能力评估提供了结构化数据与更贴合语言特性的评测手段。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 现有大模型基准偏重英文且缺乏结构化数据，难以贴合中文语言特性评估中文大模型。
method: 构建大规模中文数据-文本对数据集CDTP，并据此建立综合中文大模型评测基准CB-ECLLM。
result: 该基准弥补了英文中心与缺少结构化表示的不足，为中文大模型提供更全面评估。
conclusion: CDTP与CB-ECLLM为中文大模型能力评测提供了结构化数据与基准支撑。
---

## Abstract
Large Language Models (LLMs) have achieved remarkable success across a wide range of natural language processing tasks. However, Chinese LLMs face unique challenges, primarily due to the dominance of unstructured free text and the lack of structured representations in Chinese corpora. While existing benchmarks for LLMs partially assess Chinese LLMs, they are still predominantly English-centric and fail to address the unique linguistic characteristics of Chinese, lacking structured datasets essential for robust evaluation. To address these challenges, we present a **C**omprehensive **B**enchmark for **E**valuating **C**hinese **L**arge **L**anguage **M**odels (CB-ECLLM) based on the newly constructed Chinese Data-Text Pair (CDTP) dataset. Specifically, CDTP comprises over 7 million aligned text pairs, each consisting of unstructured text coupled with one or more corresponding triples, alongside a total of 15 million triples spanning four critical domains. The core contributions of CDTP are threefold: (i) enriching Chinese corpora with high-quality structured information; (ii) enabling fine-grained evaluation tailored to knowledge-driven tasks; and (iii) supporting multi-task fine-tuning to assess generalization and robustness across scenarios, including Knowledge Graph Completion, Triple-to-Text generation, and Question Answering. Furthermore, we conduct rigorous evaluations through extensive experiments and ablation studies to assess the effectiveness, Supervised Fine-Tuning (SFT), and robustness of the benchmark. To support reproducible research, we offer an open-source codebase and outline potential directions for future investigations based on our insights.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
面向大模型评估的大规模中文数据文本对基准。

### 2. 核心内容
现有大模型评测基准以英文为中心，且缺乏结构化数据，难以充分评估中文大模型。本文构建了大规模中文数据-文本对数据集CDTP，并据此提出综合性中文大模型评测基准CB-ECLLM。该基准针对中文语料以非结构化自由文本为主、缺少结构化表示的问题进行设计。工作为中文大模型能力评估提供了结构化数据与更贴合语言特性的评测手段。

### 3. 对应检索需求
large language models and their applications。

### 4. 来源与原文
- Source：ICLR-2026-Public
- OpenReview：[https://openreview.net/forum?id=2GhjkigNTx](https://openreview.net/forum?id=2GhjkigNTx)
