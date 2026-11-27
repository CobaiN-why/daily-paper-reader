---
title: "MEnvAgent: Scalable Polyglot Environment Construction for Verifiable Software Engineering"
title_zh: MEnvAgent：面向可验证软件工程的可扩展多语言环境构建
authors: "Chuanzhe Guo, Jingjing Wu, Sijun He, Yang Chen, Zhaoqi Kuang, Shilong Fan, Bingjin Chen, Siqi Bao, Jing Liu, Hua Wu, Qingfu Zhu, Wanxiang Che, Haifeng Wang"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf/e55372dd31f2b3bdc16496adf54d8c5aeb1ddada.pdf"
tags: ["query:ai-se"]
score: 8.0
evidence: 面向可验证软件工程的多智能体环境构建框架
tldr: 大模型软件工程智能体受限于可验证数据稀缺，根源在于多语言可执行环境构建复杂。MEnvAgent提出多语言自动环境构建框架，采用规划-执行-验证多智能体架构自主解决构建失败，并用环境复用机制降低开销。基于新基准MEnvBench的评估表明其能规模化生成可验证任务实例，为SWE智能体训练与评测提供支撑。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 可验证数据稀缺制约SWE智能体发展，根源是多语言可执行环境构建困难。
method: 采用规划-执行-验证多智能体架构自动构建环境，并用环境复用机制降低开销。
result: 在新基准MEnvBench上可规模化生成可验证的软件工程任务实例。
conclusion: 自动化环境构建为SWE智能体训练与评测提供可扩展数据基础。
---

## Abstract
The evolution of Large Language Model (LLM) agents for software engineering (SWE) is constrained by the scarcity of verifiable datasets, a bottleneck stemming from the complexity of constructing executable environments across diverse languages. To address this, we introduce **MEnvAgent**, a **M**ulti-language framework for automated **Env**ironment construction that facilitates scalable generation of verifiable task instances. MEnvAgent employs a multi-agent Planning-Execution-Verification architecture to autonomously resolve construction failures and integrates a novel Environment Reuse Mechanism that reduces computational overhead by incrementally patching historical environments. Evaluations on MEnvBench, a new benchmark comprising 1,000 tasks across 10 languages, demonstrate that MEnvAgent outperforms baselines, improving Fail-to-Pass (F2P) rates by **8.6%** while reducing time costs by **43%**. Additionally, we demonstrate the utility of MEnvAgent by constructing MEnvData-SWE, the largest open-source polyglot dataset of realistic verifiable Docker environments to date, alongside solution trajectories that enable consistent performance gains on SWE tasks across a wide range of models.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
面向可验证软件工程的多智能体环境构建框架。

### 2. 核心内容
大模型软件工程智能体受限于可验证数据稀缺，根源在于多语言可执行环境构建复杂。MEnvAgent提出多语言自动环境构建框架，采用规划-执行-验证多智能体架构自主解决构建失败，并用环境复用机制降低开销。基于新基准MEnvBench的评估表明其能规模化生成可验证任务实例，为SWE智能体训练与评测提供支撑。

### 3. 对应检索需求
software engineering tasks and automation。

### 4. 来源与原文
- Source：ICML-2026-Accepted
- OpenReview：[https://openreview.net/forum?id=Mkal0hTCnh](https://openreview.net/forum?id=Mkal0hTCnh)
