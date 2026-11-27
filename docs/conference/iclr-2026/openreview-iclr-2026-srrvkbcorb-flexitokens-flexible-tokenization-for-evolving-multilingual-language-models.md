---
title: "FLEXITOKENS: Flexible Tokenization for Evolving  Multilingual Language Models"
title_zh: FLEXITOKENS：面向演进多语言模型的可变分词
authors: "Abraham Toluwase Owodunni, Orevaoghene Ahia, Sachin Kumar"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=srrvKbcoRB"
tags: ["query:ai-se"]
score: 6.0
evidence: 面向多语言模型的可学习自适应分词
tldr: 多语言语言模型在适应新数据分布时受限于固定的子词分词器，常导致对未见语言或领域文本的过度切分。本文提出FlexiTokens，构建字节级语言模型并加入可学习的分词模块，预测字节序列中的边界以形成变长片段，从而实现自适应分词。实验表明该方法能更高效地处理分布外语言与文本，为多语言模型的灵活适配提供了新的分词方案。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 多语言模型在适应新数据分布时受限于固定的子词分词器，易对未见语言或领域文本过度切分。
method: 构建字节级语言模型并加入可学习边界预测模块，将字节序列编码为变长片段以实现自适应分词。
result: 该方法缓解了固定压缩率带来的问题，能更高效地处理分布外语言与文本。
conclusion: 为多语言模型在演进数据分布下的灵活分词与适配提供了可行方案。
---

## Abstract
Multilingual language models are challenging to adapt to new data distributions by simple finetuning due to the rigidity of their subword tokenizers, which typically remain unchanged during adaptation. This inflexibility often leads to inefficient tokenization, causing overfragmentation of out-of-distribution domains, unseen languages, or scripts. In this work, we develop byte-level LMs with learnable tokenizers to make tokenization adaptive. Our models include a submodule that learns to predict boundaries between the input byte sequence, encoding it into variable-length segments. Existing tokenizer-free methods train this boundary predictor using an auxiliary loss that enforces a fixed compression rate across the training corpus, introducing a new kind of rigidity. We propose FLEXITOKENS, a simplified training objective that enables significantly greater flexibility during adaptation. Evaluating across multiple multilingual benchmarks, morphologically diverse tasks, and domains, we demonstrate that FLEXITOKENS consistently reduces token over-fragmentation and achieves up to 10% improvements on downstream task performance compared to subword and other gradient-based tokenizers.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
面向多语言模型的可学习自适应分词。

### 2. 核心内容
多语言语言模型在适应新数据分布时受限于固定的子词分词器，常导致对未见语言或领域文本的过度切分。本文提出FlexiTokens，构建字节级语言模型并加入可学习的分词模块，预测字节序列中的边界以形成变长片段，从而实现自适应分词。实验表明该方法能更高效地处理分布外语言与文本，为多语言模型的灵活适配提供了新的分词方案。

### 3. 对应检索需求
natural language processing techniques。

### 4. 来源与原文
- Source：ICLR-2026-Public
- OpenReview：[https://openreview.net/forum?id=srrvKbcoRB](https://openreview.net/forum?id=srrvKbcoRB)
