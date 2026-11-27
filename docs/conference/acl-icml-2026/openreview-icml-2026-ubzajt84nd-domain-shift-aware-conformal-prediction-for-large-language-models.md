---
title: Domain-Shift-Aware Conformal Prediction for Large Language Models
title_zh: 面向大语言模型的域偏移感知共形预测
authors: "Zhexiao Lin, Yuanyuan Li, Neeraj Sarna, Yuanyuan Gao, Michael Berger"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf/46425d4552de2386327d8b62a8250a05163a6585.pdf"
tags: ["query:ai-se"]
score: 6.0
evidence: 通过校准预测集降低大模型幻觉风险
tldr: 大模型常产生过度自信且事实错误的输出，带来实际应用风险，而标准共形预测在域偏移下会失效。作者提出域偏移感知的共形预测框架DS-CP，依据校准样本与测试提示的接近程度进行重加权，从而在保持有效性同时增强自适应性。该框架为提升大模型输出的可靠性提供了分布无关的覆盖保证，有助于缓解幻觉带来的安全隐患。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 大模型易产生过度自信的错误输出，标准共形预测在域偏移下失效，导致覆盖不足与预测不可靠。
method: 提出DS-CP框架，按校准样本与测试提示的接近程度重加权，使共形预测在域偏移下保持有效并增强适应性。
result: 该方法在保持有限样本覆盖保证的同时提升了预测集的自适应性，缓解了域偏移下的覆盖不足问题。
conclusion: DS-CP为大模型在分布变化场景下的可靠输出提供了更具鲁棒性的不确定性量化手段。
---

## Abstract
Large language models have achieved impressive performance across diverse tasks. However, their tendency to produce overconfident and factually incorrect outputs, known as hallucinations, poses risks in real world applications. Conformal prediction provides finite-sample, distribution-free coverage guarantees, but standard conformal prediction breaks down under domain shift, often leading to under-coverage and unreliable prediction sets. We propose a new framework called Domain-Shift-Aware Conformal Prediction (DS-CP). Our framework adapts conformal prediction to large language models under domain shift, by systematically reweighting calibration samples based on their proximity to the test prompt, thereby preserving validity while enhancing adaptivity. Our theoretical analysis and experiments on the MMLU benchmark demonstrate that the proposed method delivers more reliable coverage than standard conformal prediction, especially under substantial distribution shifts, while maintaining efficiency. This provides a practical step toward trustworthy uncertainty quantification for large language models in real-world deployment.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
通过校准预测集降低大模型幻觉风险。

### 2. 核心内容
大模型常产生过度自信且事实错误的输出，带来实际应用风险，而标准共形预测在域偏移下会失效。作者提出域偏移感知的共形预测框架DS-CP，依据校准样本与测试提示的接近程度进行重加权，从而在保持有效性同时增强自适应性。该框架为提升大模型输出的可靠性提供了分布无关的覆盖保证，有助于缓解幻觉带来的安全隐患。

### 3. 对应检索需求
大模型安全。

### 4. 来源与原文
- Source：ICML-2026-Accepted
- OpenReview：[https://openreview.net/forum?id=UbzajT84Nd](https://openreview.net/forum?id=UbzajT84Nd)
