---
title: "SWE-Effi: Re-Evaluating Software AI Agent System Effectiveness Under Resource Constraints"
title_zh: SWE-Effi：资源约束下重新评估软件AI智能体系统的有效性
authors: "Zhiyu Fan, Kirill Vasilevski, Dayi Lin, Boyuan Chen, Yihao Chen, Zhiqing Zhong, Jie M. Zhang, Pinjia He, Ahmed Hassan"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=x7C9A4Y9cF"
tags: ["query:ai-se"]
score: 8.0
evidence: 在资源约束下重新评估代码智能体的有效性
tldr: 现有面向软件工程的AI智能体榜单只关注解决正确率，忽视资源约束下的有效性。本文提出SWE-Effi，一组新指标，从准确率与资源成本的平衡角度对代码智能体进行整体有效性评估，覆盖自主问题解决与功能新增等任务。该工作弥补了只看正确率的评价盲区，为软件工程智能体的实用化评估提供了更全面的衡量标准。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 现有软件工程智能体榜单只看解决正确率，忽视资源成本与整体有效性。
method: 提出SWE-Effi指标集，以准确率与资源成本的平衡衡量代码智能体的整体有效性。
result: 该指标揭示了仅看正确率所忽略的效率差异，提供更全面的评估。
conclusion: SWE-Effi为软件工程智能体在资源受限场景下的实用评估提供了新标准。
---

## Abstract
The advancement of large language models (LLMs) and code agents has demonstrated significant potential to assist software engineering (SWE) tasks, such as autonomous issue resolution and feature addition. Existing AI for software engineering leaderboards (e.g., SWE-bench) focus solely on solution accuracy, ignoring the crucial factor of effectiveness in a resource-constrained world. This is a universal problem that also exists beyond software engineering tasks: any AI system should be more than correct—it must also be cost-effective. To address this gap, we introduce SWE-Effi, a set of new metrics to re-evaluate AI systems in terms of holistic effectiveness scores. We define effectiveness as the balance between the accuracy of outcome (e.g., issue resolve rate) and the resources consumed (e.g., token and time). In this paper, we specifically focus on the software engineering scenario by re-ranking popular AI systems for issue resolution on a subset of the SWE-bench benchmark using our new multi-dimensional metrics.   
    We found that AI system’s effectiveness depends not just on the scaffold itself, but on how well it integrates with the base model, which is key to achieving strong performance in a resource-efficient manner. We also identified systematic challenges such as the “token snowball” effect and, more significantly, a pattern of “expensive failures”. In these cases, agents consume excessive resources while stuck on unsolvable tasks—an issue that not only limits practical deployment but also drives up the cost of failed rollouts during RL training. Lastly, we observed a clear trade-off between effectiveness under the token budget and effectiveness under the time budget, which plays a crucial role in managing project budgets and enabling scalable reinforcement learning, where fast responses are essential.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
在资源约束下重新评估代码智能体的有效性。

### 2. 核心内容
现有面向软件工程的AI智能体榜单只关注解决正确率，忽视资源约束下的有效性。本文提出SWE-Effi，一组新指标，从准确率与资源成本的平衡角度对代码智能体进行整体有效性评估，覆盖自主问题解决与功能新增等任务。该工作弥补了只看正确率的评价盲区，为软件工程智能体的实用化评估提供了更全面的衡量标准。

### 3. 对应检索需求
autonomous agents for coding tasks。

### 4. 来源与原文
- Source：ICLR-2026-Rejected-Public
- OpenReview：[https://openreview.net/forum?id=x7C9A4Y9cF](https://openreview.net/forum?id=x7C9A4Y9cF)
