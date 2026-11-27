---
title: "FullStack-Agent: Enhancing Agentic Full-Stack Web Coding via Development-Oriented Testing and Repository Back-Translation"
title_zh: FullStack-Agent：通过开发导向测试与仓库反向翻译增强智能体全栈 Web 编码
authors: "Zimu Lu, Houxing Ren, Yunqiao Yang, Ke Wang, Zhuofan Zong, Mingjie Zhan, Hongsheng Li"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf/7127858647af7d078e50bb9e39db79a7928f1fcb.pdf"
tags: ["query:ai-se"]
score: 9.0
evidence: 面向全栈 Web 开发的统一 LLM 代码智能体系统
tldr: 现有 LLM 代码智能体多只生成前端页面，掩盖了真实全栈数据处理与存储能力的缺失。本文提出 FullStack-Agent，一个统一的全栈智能体编码系统，引入开发导向测试与仓库反向翻译机制，以控制数据流并精准定位代码库中的隐蔽缺陷。实验表明该系统能显著提升全栈应用的可用性与正确性，推动代码智能体从页面生成走向真实工程开发。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 现有代码智能体只做前端页面，缺乏真实全栈数据处理与缺陷定位能力。
method: 提出统一智能体系统，结合开发导向测试与仓库反向翻译来控制数据流并定位缺陷。
result: 系统在复杂全栈 Web 开发任务上显著提升了应用完整性与正确性。
conclusion: 该工作推动 LLM 代码智能体从页面生成迈向真实生产级全栈工程。
---

## Abstract
Assisting non-expert users to develop complex interactive websites has become a popular task for LLM-powered code agents.
However, existing code agents tend to only generate frontend web pages, masking the lack of real full-stack data processing and storage with fancy visual effects.
Notably, constructing production-level full-stack web applications is far more challenging than only generating frontend web pages, demanding careful control of data flow, comprehensive understanding of constantly updating packages and dependencies, and accurate localization of obscure bugs in the codebase.
To address these difficulties, we introduce FullStack-Agent, a unified agent system for full-stack agentic coding that consists of three parts:
(1) FullStack-Dev, a multi-agent framework with strong planning, code editing, codebase navigation, and bug localization abilities.
(2) FullStack-Learn, an innovative data-scaling and self-improving method that back-translates crawled and synthesized website repositories to improve the backbone LLM of FullStack-Dev.
(3) FullStack-Bench, a comprehensive benchmark that systematically tests the frontend, backend and database functionalities of the generated website.
Our FullStack-Dev outperforms the previous state-of-the-art method by 8.7\%, 38.2\%, and 15.9\% on the frontend, backend, and database test cases respectively.
Additionally, FullStack-Learn raises the performance of a 30B model by 9.7\%, 9.5\%, and 2.8\% on the three sets of test cases through self-improvement, demonstrating the effectiveness of our approach.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
面向全栈 Web 开发的统一 LLM 代码智能体系统。

### 2. 核心内容
现有 LLM 代码智能体多只生成前端页面，掩盖了真实全栈数据处理与存储能力的缺失。本文提出 FullStack-Agent，一个统一的全栈智能体编码系统，引入开发导向测试与仓库反向翻译机制，以控制数据流并精准定位代码库中的隐蔽缺陷。实验表明该系统能显著提升全栈应用的可用性与正确性，推动代码智能体从页面生成走向真实工程开发。

### 3. 对应检索需求
autonomous agents for coding tasks。

### 4. 来源与原文
- Source：ICML-2026-Accepted
- OpenReview：[https://openreview.net/forum?id=xblX2nQrj7](https://openreview.net/forum?id=xblX2nQrj7)
