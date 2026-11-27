---
title: "Breaking the Code: Security Assessment of AI Code Agents Through Systematic Jailbreaking Attacks"
title_zh: 破解代码：通过系统化越狱攻击评估AI代码智能体安全性
authors: "Shoumik Saha, Jifan Chen, Sam Mayers, Sanjay Krishna Gouda, Zijian Wang, Varun Kumar"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=dpVhlf13tk"
tags: ["query:ai-se"]
score: 9.0
evidence: 面向AI代码智能体的安全越狱评估
tldr: 代码大模型智能体被广泛嵌入软件工程流程，可读写并执行代码，使越狱攻击风险超出纯文本场景。本文提出CodeAgentJail基准，覆盖空、单文件与多文件三种升级工作区，并设计可执行感知的层级评判框架。该框架检验合规性、攻击成功率、语法正确性与运行时可行性。工作揭示了智能体真实执行恶意程序的安全缺口，为大模型安全评估提供新工具。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 代码智能体可读写执行代码，越狱攻击风险超出纯文本，现有评估只看拒答或有害文本。
method: 提出CodeAgentJail基准及可执行感知的层级评判框架，检验攻击是否真正编译运行恶意程序。
result: 框架覆盖合规、攻击成功、语法正确与运行时可行四个维度，揭示真实执行层面的安全缺口。
conclusion: 该工作为大模型代码智能体的安全评估提供了超越文本检测的实用基准。
---

## Abstract
Code-capable large language model (LLM) agents are increasingly embedded into software engineering workflows where they can read, write, and execute code, raising the stakes of safety-bypass (“jailbreak”) attacks beyond text-only settings. Prior evaluations emphasize refusal or harmful-text detection, leaving open whether agents actually compile and run malicious programs. We present **CodeAgentJail**, a benchmark spanning three escalating workspace regimes that mirror attacker capability: empty (CAJ-0), single-file (CAJ-1), and multi-file (CAJ-M). We pair this with a hierarchical, executable-aware **Judge Framework** that tests (i) compliance, (ii) attack success, (iii) syntactic correctness, and (iv) runtime executability, moving beyond refusal to measure deployable harm. Using seven LLMs from five families as backends, we find that under prompt-only conditions in CAJ-0, code agents accept 61\% of attacks on average; 58\% are harmful, 52\% parse, and 27\% run end-to-end. Moving to single-file regime in CAJ-1 drives compliance to $\sim$100\% for capable models and yields a mean ASR (*Attack Success Rate*) $\approx$71\%; the multi-file regime (CAJ-M) raises mean ASR to $\approx$75\%, with 32\% being instantly deployable attack code. Across models, wrapping an LLM in an agent substantially increases vulnerability -- ASR raises  by 1.6$\times$ -- by frequently overturning initial refusals during planning/tool-use steps. We further observe similar jailbreak trends when replacing OpenHands with SWE-Agent and OpenAI Codex, suggesting that CodeAgentJail is agent-agnostic.
Category-level analyses identify which attack classes are most vulnerable and most readily deployable, while others exhibit large execution gaps. These findings motivate execution-aware defenses, code-contextual safety filters, and mechanisms that preserve refusal decisions throughout the agent’s multi-step reasoning and tool use.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
面向AI代码智能体的安全越狱评估。

### 2. 核心内容
代码大模型智能体被广泛嵌入软件工程流程，可读写并执行代码，使越狱攻击风险超出纯文本场景。本文提出CodeAgentJail基准，覆盖空、单文件与多文件三种升级工作区，并设计可执行感知的层级评判框架。该框架检验合规性、攻击成功率、语法正确性与运行时可行性。工作揭示了智能体真实执行恶意程序的安全缺口，为大模型安全评估提供新工具。

### 3. 对应检索需求
大模型安全。

### 4. 来源与原文
- Source：ICLR-2026-Public
- OpenReview：[https://openreview.net/forum?id=dpVhlf13tk](https://openreview.net/forum?id=dpVhlf13tk)
