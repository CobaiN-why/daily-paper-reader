---
title: "Smoothed-ModernBERT: Co-Attentional Synergy of Probabilistic Topic Models and ModernBERT through Dynamic Fusion"
title_zh: Smoothed-ModernBERT：概率主题模型与ModernBERT的协同动态融合
authors: "Akinlolu Oluwabusayo Ojo, Nizar Bouguila"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=MMUTEyFt4D"
tags: ["query:ai-se"]
score: 6.0
evidence: 结合ModernBERT与主题模型的自然语言处理混合方法
tldr: 文档分类中，Transformer擅长上下文语义却忽略潜在主题结构，而概率主题模型能捕捉主题却缺乏细粒度语境依赖。本文提出Smoothed-ModernBERT混合模型，通过动态融合将ModernBERT的上下文表征与平滑狄利克雷主题模型的可解释主题表示相结合。该工作提升了文档级分类的表征能力，为自然语言处理中的文本分类任务提供了新思路。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: Transformer忽略文档潜在主题结构，而主题模型缺乏细粒度语境依赖。
method: 提出动态融合框架，将ModernBERT上下文表征与平滑狄利克雷主题模型结合。
result: 该混合方法在文档分类任务上提升了表征能力与分类效果。
conclusion: 为自然语言处理中文档级文本分类提供了可解释且有效的融合方案。
---

## Abstract
Document classification remains a critical challenge in natural language processing (NLP) as text volumes and thematic complexity escalate. Although transformer-based architectures like BERT excel at capturing contextual semantics, they often overlook the latent thematic structures inherent in document-level discourse. Conversely, probabilistic topic models effectively distill coarse-grained thematic patterns but struggle with nuanced contextual dependencies. To address these limitations, this study introduces a novel hybrid approach that synergizes the contextual depth of ModernBERT with the interpretable thematic representations of smoothed-Dirichlet-based topic models. Our model aligns token-level representations with document-level thematic distributions by optimizing contextual and topic objectives through a co-attention mechanism layer. By utilizing a dynamic fusion layer, where co-attention scores dynamically gate and blend BERT’s embeddings with topic mixtures at each instance, the approach captures both fine-grained context and global theme interplay in a unified representation. Our method bridges a critical gap in the NLP methodology, paving the way for enhanced model generalizability in domains that require both thematic abstraction and contextual granularity. Empirical evaluations on benchmark corpora demonstrate consistent classification robustness over standalone approaches. To ensure the reproducibility of our experiments and encourage further research, we open-source our implementation code.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
结合ModernBERT与主题模型的自然语言处理混合方法。

### 2. 核心内容
文档分类中，Transformer擅长上下文语义却忽略潜在主题结构，而概率主题模型能捕捉主题却缺乏细粒度语境依赖。本文提出Smoothed-ModernBERT混合模型，通过动态融合将ModernBERT的上下文表征与平滑狄利克雷主题模型的可解释主题表示相结合。该工作提升了文档级分类的表征能力，为自然语言处理中的文本分类任务提供了新思路。

### 3. 对应检索需求
natural language processing techniques。

### 4. 来源与原文
- Source：ICLR-2026-Public
- OpenReview：[https://openreview.net/forum?id=MMUTEyFt4D](https://openreview.net/forum?id=MMUTEyFt4D)
