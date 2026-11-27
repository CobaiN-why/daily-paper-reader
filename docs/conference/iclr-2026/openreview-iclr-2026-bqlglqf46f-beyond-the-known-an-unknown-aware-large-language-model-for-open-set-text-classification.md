---
title: "Beyond the Known: An Unknown-Aware Large Language Model for Open-Set Text Classification"
title_zh: 超越已知：面向开放集文本分类的未知感知大模型
authors: "Xi Chen, Chuan Qin, Ziqi Wang, Shasha Hu, Chao Wang, Hengshu Zhu, Hui Xiong"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=BqLGlQF46f"
tags: ["query:ai-se"]
score: 6.0
evidence: 未知感知大模型将开放集文本分类重构为子集条件生成
tldr: 开放集文本分类要求模型在正确分类已知类别的同时拒绝分布外输入，而现有方法缺乏对未知的感知导致过度自信。本文提出UnLLM，将分类重构为子集条件的文本生成任务，通过采样标签子集提示大模型以增强未知感知。实验表明该方法提升了分布外检测与整体分类可靠性，为真实NLP系统提供更稳健的方案。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 现有开放集分类方法缺乏未知感知，对分布外输入产生过度自信预测。
method: 提出UnLLM，将分类重构为子集条件文本生成，用采样标签子集提示大模型。
result: 实验显示该方法提升了分布外检测能力和开放集分类的可靠性。
conclusion: 为真实NLP系统的未知感知分类提供了生成式新范式。
---

## Abstract
Open-set text classification (OSTC) requires models to correctly classify in-distribution (ID) samples while reliably rejecting out-of-distribution (OOD) inputs—an essential capability for real-world NLP systems. Most OSTC methods train on ID data under the closed assumption that all outputs belong to the known label space and then perform OOD detection with the biased representations, which inherently lack awareness of unknowns and thus yield overconfident predictions on OOD inputs. In this work, we present UnLLM, an Unknown-aware Large Language Model for OSTC. Instead of fixing classification to the entire known label space, we reformulate it into a subset-conditioned text generation task: the LLM is prompted with sampled subsets of known labels, and any instance outside the candidate set is explicitly assigned as “unknown”. This reformulation transforms OOD detection from a post-hoc procedure into an intrinsic modeling capability. More importantly, our approach is the first to explicitly incorporate the unknown into classification, enabling systematic modeling of unknowns through a unified representation–logits–inference optimization, which progressively strengthens the model’s capacity to capture open-set risk. Extensive experiments across six benchmarks show that UnLLM consistently outperforms state-of-the-art (SOTA) baselines. Code and datasets are available at https://github.com/cx9941/UnLLM.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
未知感知大模型将开放集文本分类重构为子集条件生成。

### 2. 核心内容
开放集文本分类要求模型在正确分类已知类别的同时拒绝分布外输入，而现有方法缺乏对未知的感知导致过度自信。本文提出UnLLM，将分类重构为子集条件的文本生成任务，通过采样标签子集提示大模型以增强未知感知。实验表明该方法提升了分布外检测与整体分类可靠性，为真实NLP系统提供更稳健的方案。

### 3. 对应检索需求
natural language processing techniques。

### 4. 来源与原文
- Source：ICLR-2026-Accepted
- OpenReview：[https://openreview.net/forum?id=BqLGlQF46f](https://openreview.net/forum?id=BqLGlQF46f)
