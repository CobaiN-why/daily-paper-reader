---
title: What Language is This? Ask Your Tokenizer.
title_zh: 这是什么语言？问问你的分词器
authors: "Clara Meister, Ahmetcan Yavuz, Pietro Lesci, Tiago Pimentel"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf/ee2e36b28f26b9da6744c9a3262d6ce2459ffa70.pdf"
tags: ["query:ai-se"]
score: 6.0
evidence: 面向多语言 NLP 流水线的高效语种识别方法
tldr: 语种识别是多语言自然语言处理流水线的关键环节，但现有系统在低资源与近缘语言上仍较脆弱。本文提出 UniLID，基于 UnigramLM 分词算法的概率框架与参数估计，通过判断字符串在哪种语言分布下似然最高来识别语种。该方法数据与计算高效，并支持增量扩展，为多语言语料筛选与跨语言评测提供了轻量可靠的工具。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 现有语种识别系统在低资源语言和近缘语言上表现脆弱。
method: 利用 UnigramLM 分词算法的概率框架，以似然最大原则推断字符串所属语言。
result: 该方法在数据与计算高效的前提下支持增量扩展并保持良好识别效果。
conclusion: 复用分词器概率结构可为多语言 NLP 提供轻量可靠的语种识别方案。
---

## Abstract
Language Identification (LID) is an important
component of many multilingual natural language processing pipelines, where it facilitates corpus curation, training data analysis, and cross-lingual
evaluation of large language models. Despite near-
perfect performance on high-resource languages,
existing systems remain brittle in low-resource and closely related language settings. We introduce UniLID, a simple and efficient LID method
based on the UnigramLM tokenization algorithm,
leveraging its probabilistic framing, parameter
estimation technique and inference strategy. In
short, to predict a string’s language label, we simply ask: under which language’s unigram distribution is this string most likely? Our formulation is
data- and compute-efficient, supports incremental
addition of new languages without retraining
existing models, and can naturally be integrated
into existing language model tokenization
pipelines. Empirical evaluations against widely
used baselines, including fastText, GlotLID-M, and
CLD3, show that UniLID achieves competitive
performance on standard benchmarks, substantially improves sample efficiency in low-resource
settings—surpassing 70% accuracy with as few as
five labeled samples per language—and delivers
large gains on fine-grained dialect identification.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
面向多语言 NLP 流水线的高效语种识别方法。

### 2. 核心内容
语种识别是多语言自然语言处理流水线的关键环节，但现有系统在低资源与近缘语言上仍较脆弱。本文提出 UniLID，基于 UnigramLM 分词算法的概率框架与参数估计，通过判断字符串在哪种语言分布下似然最高来识别语种。该方法数据与计算高效，并支持增量扩展，为多语言语料筛选与跨语言评测提供了轻量可靠的工具。

### 3. 对应检索需求
natural language processing techniques。

### 4. 来源与原文
- Source：ICML-2026-Accepted
- OpenReview：[https://openreview.net/forum?id=HhWaVjXmLN](https://openreview.net/forum?id=HhWaVjXmLN)
