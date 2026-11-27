---
title: "TestExplora: Benchmarking LLMs for Proactive Bug Discovery via Repository-Level Test Generation"
title_zh: TestExplora：通过仓库级测试生成对LLM主动缺陷发现能力进行基准测试
authors: "Steven Liu, Jane Luo, Xin Zhang, Aofan Liu, Hao Liu, Jie Wu, Ziyang Huang, Yangyu Huang, Yu Kang, Scarlett Li"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf/295beb61dd3e489b3eba675b27f0bbc331d02591.pdf"
tags: ["query:ai-se"]
score: 9.0
evidence: 通过仓库级测试生成进行主动缺陷发现的LLM基准
tldr: 现有软件测试评测多聚焦回归预防与缺陷复现，却系统性地忽视主动缺陷发现这一目标。作者提出TestExplora基准，在完整真实仓库环境中评估大模型作为主动测试者的能力，要求其在缺陷显现为失败之前加以暴露。该工作填补了主动测试评测的空白，为代码智能体的测试生成与缺陷检测研究提供了新的评测框架。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 现有评测忽视主动缺陷发现，只关注回归预防与缺陷复现两个目标。
method: 构建TestExplora基准，在完整真实仓库环境中评估大模型作为主动测试者的能力。
result: 该基准能够在缺陷显现为失败之前检验模型的主动发现能力。
conclusion: 为代码智能体的测试生成与缺陷检测提供了面向主动测试的评测框架。
---

## Abstract
Given that Large Language Models (LLMs) are increasingly applied to automate software development, comprehensive software assurance spans three distinct goals: regression prevention, reactive reproduction, and proactive discovery. Current evaluations systematically overlook the third goal. Specifically, they either constrain models to a compliance trap by treating existing code as the ground truth for regression prevention, or rely on post-failure artifacts (e.g., issue reports) for reactive bug reproduction, failing to expose defects before they manifest as failures. To bridge this gap, we present TestExplora, a benchmark designed to evaluate LLMs as proactive testers within full-scale, realistic repository environments. Comprising 2,389 tasks across 482 repositories, TestExplora conceals all defect-related information, forcing models to uncover bugs by identifying discrepancies between implementation and documentation-derived intent—utilizing documentation as the reference oracle. Furthermore, to ensure sustainable evaluation and mitigate risks of data leakage in static datasets, we propose a continuous, time-aware data collection framework. Our evaluation reveals a significant capability gap: state-of-the-art models achieve a maximum Fail-to-Pass ($F2P$) rate of only 16.06%. Further analysis indicates that navigating complex cross-module interactions and leveraging agentic exploration are critical to advancing LLMs toward autonomous software quality assurance. Consistent with this, SWEAgent instantiated with GPT-5-mini achieves an $F2P$ of 17.27% and an $F2P@5$ of 29.7%, highlighting the effectiveness and promise of agentic exploration in proactive bug discovery tasks.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
通过仓库级测试生成进行主动缺陷发现的LLM基准。

### 2. 核心内容
现有软件测试评测多聚焦回归预防与缺陷复现，却系统性地忽视主动缺陷发现这一目标。作者提出TestExplora基准，在完整真实仓库环境中评估大模型作为主动测试者的能力，要求其在缺陷显现为失败之前加以暴露。该工作填补了主动测试评测的空白，为代码智能体的测试生成与缺陷检测研究提供了新的评测框架。

### 3. 对应检索需求
coding agents for automated test generation and documentation。

### 4. 来源与原文
- Source：ICML-2026-Accepted
- OpenReview：[https://openreview.net/forum?id=pxw9YfTYtC](https://openreview.net/forum?id=pxw9YfTYtC)
