---
title: Continuous Control of LLM Text Generation via Probabilistic Prompting
title_zh: 通过概率提示实现对大模型文本生成的连续控制
authors: "Jimin Kim, Hyungu Kahng"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=QlueaQClYw"
tags: ["query:ai-se"]
score: 6.0
evidence: 用概率提示实现对大模型文本生成的细粒度连续控制
tldr: 高质量标注数据稀缺，而现有基于大模型的合成数据生成依赖僵硬的类别条件，导致文本极化且不真实。本文提出概率提示框架，并实现零样本方法SoftGen，通过从分布采样概率向量、以概率提示条件生成并自验证的三阶段流程，实现细粒度连续控制。方法提升了合成文本的保真度与多样性，为NLP数据增强提供了更灵活的手段。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 高质量标注数据稀缺，现有合成数据生成依赖僵硬类别条件导致文本不真实。
method: 提出概率提示框架与SoftGen三阶段零样本流程，用连续概率向量条件控制生成。
result: 提升了合成文本的保真度与多样性，实现细粒度控制。
conclusion: 为NLP数据增强与可控文本生成提供了更灵活的方案。
---

## Abstract
The scarcity of high-quality labeled data remains a critical bottleneck in natural language processing, while existing synthetic data generation approaches using Large Language Models (LLMs) rely on rigid categorical conditioning that produces polarized and unrealistic text. We introduce Probabilistic Prompting, a framework that achieves fine-grained control over LLM text generation by conditioning on continuous probability vectors rather than discrete categorical instructions. To realize this framework, we propose SoftGen, a zero-shot method implementing a three-stage pipeline: (1) sampling probability vectors from tailored distributions, (2) generating text conditioned on probabilistic prompts, and (3) self-verification to ensure high fidelity. Through comprehensive evaluation on five text classification benchmarks, we demonstrate three key contributions. First, we provide rigorous analysis of generation fidelity, revealing that LLMs can faithfully follow probabilistic instructions and uncovering systematic relationships between label entropy and generation quality that vary by task dimensionality. Second, we show substantial downstream utility: models trained on our synthetic data achieve improved accuracy and calibration compared to traditional categorical approaches.
Third, we establish theoretical foundations grounded in the Maximum Entropy Principle, including formal definitions of Generator Calibration and mathematical proofs connecting prompt entropy to output diversity. Our work demonstrates that preserving continuous probability structure in synthetic data generation provides richer supervisory signals and enables more realistic, diverse datasets better reflecting the continuous nature of semantic properties in natural language.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
用概率提示实现对大模型文本生成的细粒度连续控制。

### 2. 核心内容
高质量标注数据稀缺，而现有基于大模型的合成数据生成依赖僵硬的类别条件，导致文本极化且不真实。本文提出概率提示框架，并实现零样本方法SoftGen，通过从分布采样概率向量、以概率提示条件生成并自验证的三阶段流程，实现细粒度连续控制。方法提升了合成文本的保真度与多样性，为NLP数据增强提供了更灵活的手段。

### 3. 对应检索需求
natural language processing techniques。

### 4. 来源与原文
- Source：ICLR-2026-Public
- OpenReview：[https://openreview.net/forum?id=QlueaQClYw](https://openreview.net/forum?id=QlueaQClYw)
