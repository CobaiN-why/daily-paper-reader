---
title: "RedCodeAgent: Automatic Red-teaming Agent against Diverse Code Agents"
title_zh: RedCodeAgent：针对多样代码智能体的自动红队智能体
authors: "Chengquan Guo, Chulin Xie, Yu Yang, Zhaorun Chen, Zinan Lin, Xander Davies, Yarin Gal, Dawn Song, Bo Li"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=IyIaAOihmZ"
tags: ["query:ai-se"]
score: 8.0
evidence: 自动红队智能体揭示代码智能体的安全漏洞
tldr: 代码智能体具备强大代码生成与执行能力，却带来严重安全风险，而现有静态安全基准和红队工具难以覆盖复杂越狱组合等边界场景。本文提出首个自动红队智能体RedCodeAgent，借助自适应记忆模块系统性地挖掘各类代码智能体的漏洞。该工作针对大模型代码智能体的安全测试问题，为发现真实世界中新兴风险场景提供了自动化手段。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 代码智能体带来安全风险，现有静态基准与红队工具难以覆盖越狱组合等边界场景。
method: 提出首个自动红队智能体RedCodeAgent，用自适应记忆模块系统挖掘代码智能体漏洞。
result: 该方法能发现静态基准遗漏的多样风险场景与安全漏洞。
conclusion: RedCodeAgent为大模型代码智能体的安全评估与红队测试提供了自动化方案。
---

## Abstract
Code agents have gained widespread adoption due to their strong code generation capabilities and integration with code interpreters, enabling dynamic execution, debugging, and interactive programming capabilities. While these advancements have streamlined complex workflows, they have also introduced critical safety and security risks. Current static safety benchmarks and red-teaming tools are inadequate for identifying emerging real-world risky scenarios, as they fail to cover certain boundary conditions, such as the combined effects of different jailbreak tools.
In this work, we propose RedCodeAgent, the first automated red-teaming agent designed to systematically uncover vulnerabilities in diverse code agents. 
With an adaptive memory module, RedCodeAgent can leverage existing jailbreak knowledge, dynamically select the most effective red-teaming tools and tool combinations in a tailored
toolbox for a given input query, thus identifying vulnerabilities that might otherwise be overlooked.
For reliable evaluation, we develop simulated sandbox environments to additionally evaluate the execution results of code agents, mitigating potential biases of LLM-based judges that only rely on static code.
Through extensive evaluations across multiple state-of-the-art code agents, diverse risky scenarios, and various programming languages, RedCodeAgent consistently outperforms existing red-teaming methods, achieving higher attack success rates and lower rejection rates with high efficiency. We further validate RedCodeAgent on real-world code assistants, e.g., Cursor and Codeium, exposing previously unidentified security risks. By automating and optimizing red-teaming processes, RedCodeAgent enables scalable, adaptive, and effective safety assessments of code agents.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
自动红队智能体揭示代码智能体的安全漏洞。

### 2. 核心内容
代码智能体具备强大代码生成与执行能力，却带来严重安全风险，而现有静态安全基准和红队工具难以覆盖复杂越狱组合等边界场景。本文提出首个自动红队智能体RedCodeAgent，借助自适应记忆模块系统性地挖掘各类代码智能体的漏洞。该工作针对大模型代码智能体的安全测试问题，为发现真实世界中新兴风险场景提供了自动化手段。

### 3. 对应检索需求
大模型安全。

### 4. 来源与原文
- Source：ICLR-2026-Accepted
- OpenReview：[https://openreview.net/forum?id=IyIaAOihmZ](https://openreview.net/forum?id=IyIaAOihmZ)
