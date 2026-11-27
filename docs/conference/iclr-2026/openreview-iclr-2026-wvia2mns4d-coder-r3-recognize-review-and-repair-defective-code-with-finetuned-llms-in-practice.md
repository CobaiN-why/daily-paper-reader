---
title: "Coder-R3: Recognize, Review and Repair Defective Code with Finetuned LLMs in Practice"
title_zh: Coder-R3：实践中用微调大模型识别、审查与修复缺陷代码
authors: "Liankai Jin, Yong Zhang, Zimu Tang, Xi Wei, Meng Meng, Annan Li, Xiao Wen, Xu Zhou, Si Liu"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=WvIa2MnS4D"
tags: ["query:ai-se"]
score: 9.0
evidence: 微调大模型实现统一代码审查与缺陷修复
tldr: 现有代码审查大模型通常将流程拆分为离散子任务并为每个组件单独微调模型，忽视了任务间协同且难以落地。本文提出统一的代码审查问题建模方法，用微调大模型联合完成缺陷识别、审查与修复。该方案减少了多模型多阶段的复杂调用，提升了真实部署中的实用性。工作推进了大模型在缺陷检测与代码修复中的应用。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 现有代码审查大模型将流程拆成离散子任务分别微调，忽视协同且难以实际部署。
method: 提出统一的代码审查问题建模方法，用微调大模型联合完成缺陷识别、审查与修复。
result: 减少多模型多阶段的复杂调用，提升真实场景下的实用性与审查效果。
conclusion: 该工作推进了大模型在代码缺陷检测与自动修复任务中的落地应用。
---

## Abstract
Large language models (LLMs) have emerged as powerful tools for software engineering tasks, demonstrating particular promise in code review activities. However, existing research on code review LLMs typically decomposes the review process into discrete subtasks, collecting data and fine-tuning separate models for each individual component. This fragmented approach overlooks the synergistic relationships between different tasks, necessitates multiple models with complex multi-stage invocations, and consequently exhibits limited practical applicability in real-world deployment scenarios. In this work, we advance beyond previous code review research by proposing a unified and comprehensive code review problem modeling approach. We focus on the complete code review process, including Recognize, Review, and Repair defective code fragments consecutively, and propose $Coder\text{-}R^3$, an approach that enables a single LLM to handle all code review-related subtasks uniformly. Additionally, we establish a practically feasible closed-loop iterative process for industrial scenarios, encompassing data construction, model evaluation, and operational feedback integration. We rigorously evaluate the effectiveness of various strategies, including input context selection, output format, and training methodologies. $Coder\text{-}R^3$ achieves state-of-the-art performance on the CodeReviewer benchmark, and demonstrates superior effectiveness in real enterprise scenarios. Our work provides valuable insights for enterprises seeking to leverage large language models to enhance code review efficiency.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
微调大模型实现统一代码审查与缺陷修复。

### 2. 核心内容
现有代码审查大模型通常将流程拆分为离散子任务并为每个组件单独微调模型，忽视了任务间协同且难以落地。本文提出统一的代码审查问题建模方法，用微调大模型联合完成缺陷识别、审查与修复。该方案减少了多模型多阶段的复杂调用，提升了真实部署中的实用性。工作推进了大模型在缺陷检测与代码修复中的应用。

### 3. 对应检索需求
application of large language models to software engineering tasks such as code generation and defect detection。

### 4. 来源与原文
- Source：ICLR-2026-Rejected-Public
- OpenReview：[https://openreview.net/forum?id=WvIa2MnS4D](https://openreview.net/forum?id=WvIa2MnS4D)
