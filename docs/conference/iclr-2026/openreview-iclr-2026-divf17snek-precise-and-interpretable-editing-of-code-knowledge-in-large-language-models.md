---
title: Precise and Interpretable Editing of Code Knowledge in Large Language Models
title_zh: 大语言模型中代码知识的精确与可解释编辑
authors: "Min Xue, Nikolai Bolik, Lennart Stöpler, Erik Imgrund, Janik Schmid, Artur Andrzejak"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=diVf17SNek"
tags: ["query:ai-se"]
score: 7.0
evidence: 代码大模型中的代码知识编辑
tldr: 代码大模型虽在代码补全、翻译与摘要等任务表现优异，但预训练模型静态固化，难以低成本地注入新知识以纠正错误行为。本文提出一种精确且可解释的代码知识编辑方法，针对Transformer多层感知机中的多义神经元问题，以极少数据实现模型更新。该工作为代码大模型的持续维护与行为纠正提供了高效、可解释的编辑途径。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 预训练代码大模型静态固化，重训练成本高而提示工程无法永久改变模型，需要高效知识编辑。
method: 提出针对MLP多义神经元的精确可解释代码知识编辑方法，以极少数据实现模型更新。
result: 在少量数据下实现代码知识的有效纠正，并提升编辑的可解释性。
conclusion: 为代码大模型的持续维护与错误纠正提供了高效可解释的编辑手段。
---

## Abstract
Large Language Models (LLMs) have demonstrated outstanding capabilities in various code-related tasks, including code completion, translation, or summarization. However, these pretrained models are static, posing a challenge to incorporate new knowledge into an LLM to correct erroneous behavior. Approaches such as retraining or fine-tuning demand extensive labeled datasets and might be computationally expensive, while prompt engineering fails to change models permanently. Knowledge Editing (KE) techniques offer a more efficient alternative, enabling model updates with minimal data, even just a single example. Nevertheless, existing KE methods often manipulate parameters within the Transformer's multi-layer perceptrons (MLPs), where neuronal polysemanticity hinders both the precision and interpretability of the edits. To address these limitations, we exploit TransCoder, an MLP-like model component with a wide and sparsely activated hidden feature vector. Specifically, we introduce **TransCoder-based Precise Editing** (**TCPE**), a novel method that leverages the sparsity and monosemanticity of the TransCoder’s neurons for highly localized knowledge editing. TCPE exhibits neuron-level mechanistic interpretability characteristics, revealing the correspondence between the edited neurons and the specific code-related knowledge. Furthermore, we present KECode, a new evaluation benchmark for code-to-code translation based on functional equivalence. Using KECode, we conduct a systematic evaluation of representative KE methods in the context of code-to-code translation. Our experimental results demonstrate that TCPE outperforms existing KE methods, achieving a substantial improvement of translation accuracy of CodeLlama-7b-Instruct from 57.5% to 64.0% in a low-resource scenario of Java-to-D translation.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
代码大模型中的代码知识编辑。

### 2. 核心内容
代码大模型虽在代码补全、翻译与摘要等任务表现优异，但预训练模型静态固化，难以低成本地注入新知识以纠正错误行为。本文提出一种精确且可解释的代码知识编辑方法，针对Transformer多层感知机中的多义神经元问题，以极少数据实现模型更新。该工作为代码大模型的持续维护与行为纠正提供了高效、可解释的编辑途径。

### 3. 对应检索需求
application of large language models to software engineering tasks such as code generation and defect detection。

### 4. 来源与原文
- Source：ICLR-2026-Accepted
- OpenReview：[https://openreview.net/forum?id=diVf17SNek](https://openreview.net/forum?id=diVf17SNek)
