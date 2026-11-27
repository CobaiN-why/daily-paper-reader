---
title: "ICE-Coder: Integrating White-box and Black-box Testing in Execution-guided Multi-agent Code Generation"
title_zh: ICE-Coder：执行引导多代理代码生成中融合白盒与黑盒测试
authors: "Jed Koh Jin Keat, LI YUSU, Tianyi Zhang, BINGZHENG GAN, Yangkai Ding"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=EDgdbdjr4c"
tags: ["query:ai-se"]
score: 9.0
evidence: 融合白盒与黑盒自动测试生成的多代理代码生成
tldr: 基于大模型的编码代理在复杂编程问题上常因隐蔽边界用例而失效。本文提出ICE-Coder，在模拟软件工程环境的多代理代码生成中，借鉴代码覆盖率与代码评审生成白盒测试，并叠加已有黑盒测试生成，以更充分暴露边界缺陷。方法提升了复杂问题下生成代码的可靠性，为自动化测试与多代理代码生成结合提供了有效方案。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 现有编码代理在复杂编程问题中难以发现隐蔽的边界用例缺陷。
method: 在多代理代码生成中借鉴覆盖率与代码评审生成白盒测试，叠加黑盒测试。
result: 更充分地暴露边界缺陷，提升了复杂问题下生成代码的可靠性。
conclusion: 证明了白盒与黑盒测试结合可增强多代理自动代码生成。
---

## Abstract
LLM-based coding agents are programs that utilise LLMs to automate code generation tasks. Typically, they incorporate code execution capabilities which, together with automated test generation and/or debugging methods, enhance the reliability of the generated code. However, the effectiveness of these approaches remains limited in complex problems (such as competitive programming problems) where bugs surface only in convoluted edge cases. This work builds upon multi-agent code generation techniques which emulate software engineering environments. In particular, to address obscure edge cases, we take inspiration from code coverage tools and code reviews to generate white-box tests, on top of existing black-box test generation approaches. Test case outputs are validated through a process of deliberation using the LLM. By increasing the quantity and quality of the test cases, we obtain more reliable generated code. We evaluated ICE-Coder on LiveCodeBench-Hard. Out of the 90 problems, it solves 72, compared to the baseline of 55.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
融合白盒与黑盒自动测试生成的多代理代码生成。

### 2. 核心内容
基于大模型的编码代理在复杂编程问题上常因隐蔽边界用例而失效。本文提出ICE-Coder，在模拟软件工程环境的多代理代码生成中，借鉴代码覆盖率与代码评审生成白盒测试，并叠加已有黑盒测试生成，以更充分暴露边界缺陷。方法提升了复杂问题下生成代码的可靠性，为自动化测试与多代理代码生成结合提供了有效方案。

### 3. 对应检索需求
coding agents for automated test generation and documentation。

### 4. 来源与原文
- Source：ICLR-2026-Rejected-Public
- OpenReview：[https://openreview.net/forum?id=EDgdbdjr4c](https://openreview.net/forum?id=EDgdbdjr4c)
