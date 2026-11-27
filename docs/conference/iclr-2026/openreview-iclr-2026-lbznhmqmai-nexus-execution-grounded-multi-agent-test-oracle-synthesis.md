---
title: "Nexus: Execution-Grounded Multi-Agent Test Oracle Synthesis"
title_zh: Nexus：基于执行接地的多智能体测试预言合成
authors: "Dong HUANG, Mingzhe Du, Jie M. Zhang, Zheng Lin, Meng Luo, Qianru Zhang, See-Kiong Ng"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=lbZNHMqMAI"
tags: ["query:ai-se"]
score: 9.0
evidence: 面向测试预言自动生成的多智能体框架
tldr: 非回归测试中的测试预言生成长期困难，需要准确判定被测函数在给定输入下是否符合预期。作者提出Nexus多智能体框架，让四位持有不同测试理念的专家智能体先审议批评初始预言，再通过执行验证与迭代自我修正逐步精化。该框架以执行结果为接地，提升了测试预言的准确性与可靠性，为自动化测试生成提供了可复用的多智能体方案。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 非回归测试中的测试预言生成长期困难，难以准确判定被测函数行为是否符合预期。
method: 提出多智能体框架，由多位专家智能体审议、验证并通过执行接地迭代自我修正测试预言。
result: 该方法以执行结果为接地提升了测试预言的准确性与可靠性。
conclusion: 多智能体协同与执行验证为自动化测试生成提供了有效可复用的方案。
---

## Abstract
Test oracle generation in non-regression testing is a longstanding challenge in
software engineering, where the goal is to produce oracles that can accurately
determine whether a function under test (FUT) behaves as intended for a given
input. In this paper, we introduce Nexus, a novel multi-agent framework to address this challenge. Nexus generates test oracles by leveraging a diverse set of
specialized agents that synthesize test oracles through a structured process of deliberation, validation, and iterative self-refinement. During the deliberation phase,
a panel of four specialist agents, each embodying a distinct testing philosophy,
collaboratively critiques and refines an initial set of test oracles. Then, in the
validation phase, Nexus generates a plausible candidate implementation of the
FUT and executes the proposed oracles against it in a secure sandbox. For any
oracle that fails this execution-based check, Nexus activates an automated selfrefinement loop, using the specific runtime error to debug and correct the oracle before re-validation. Our extensive evaluation on seven diverse benchmarks
demonstrates that Nexus consistently and substantially outperforms state-of-theart baselines. For instance, Nexus improves the test-level oracle accuracy on the
LiveCodeBench from 46.30% to 57.73% for GPT-4.1-Mini. The improved accuracy also significantly enhances downstream tasks: the bug detection rate of GPT4.1-Mini generated test oracles on HumanEval increases from 90.91% to 95.45%
for Nexus compared to baselines, and the success rate of automated program repair improves from 35.23% to 69.32%.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
面向测试预言自动生成的多智能体框架。

### 2. 核心内容
非回归测试中的测试预言生成长期困难，需要准确判定被测函数在给定输入下是否符合预期。作者提出Nexus多智能体框架，让四位持有不同测试理念的专家智能体先审议批评初始预言，再通过执行验证与迭代自我修正逐步精化。该框架以执行结果为接地，提升了测试预言的准确性与可靠性，为自动化测试生成提供了可复用的多智能体方案。

### 3. 对应检索需求
coding agents for automated test generation and documentation。

### 4. 来源与原文
- Source：ICLR-2026-Rejected-Public
- OpenReview：[https://openreview.net/forum?id=lbZNHMqMAI](https://openreview.net/forum?id=lbZNHMqMAI)
