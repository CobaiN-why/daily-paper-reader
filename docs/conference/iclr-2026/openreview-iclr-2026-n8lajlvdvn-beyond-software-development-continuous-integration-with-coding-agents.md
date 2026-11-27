---
title: "Beyond Software Development: Continuous Integration with coding agents"
title_zh: 超越软件开发：编码智能体驱动的持续集成
authors: "Jiawei Wang, Leonhard Applis, Abhik Roychoudhury"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=n8lAJLVdVN"
tags: ["query:ai-se"]
score: 8.0
evidence: 编码智能体在持续集成与测试中的应用
tldr: 编码智能体已能通过问题解决维护代码库，但很少参与将改动集成并落地到复杂软件项目中。本文研究维护者在整合AI生成建议时会遇到的技术挑战，如构建问题和系统测试，并比较多种软件工程智能体应对这些运维化任务的能力。研究揭示了现有编码智能体在持续集成与测试环节的局限，为让智能体真正参与软件交付流程提供了分析基础。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 编码智能体能修复缺陷和新增功能，却难以将改动集成到复杂项目中，带来构建与测试挑战。
method: 研究维护者整合AI生成建议时的技术难题，并对比多种软件工程智能体处理这些任务的表现。
result: 比较显示现有编码智能体在构建、测试等运维化环节仍存在明显能力局限。
conclusion: 该工作揭示了编码智能体参与持续集成与测试的挑战，为后续改进指明方向。
---

## Abstract
Coding agents are popular aids for software development today. Starting from code completion mechanisms in GitHub co-pilot, they have evolved much beyond programming to be active aids for software development by managing and maintaining a code-base via issue resolution. Resolving software issues takes care of program improvement tasks such as bug fixes and feature additions. 
Yet they do not contribute to the integration and operationalization of such changes into a complex software project. 
In this work, we study technical challenges that maintainers will face with integrating AI-generated suggestions such as build-problems and testing software systems. We compare how a variety of existing software engineering agents can cope with such operationalization and systems integration.  This includes the open-source agent \texttt{OpenHands}, an existing agent to help in project builds called \texttt{ExecutionAgent}, and USEAgent, a general purpose SE agent ensemble.  Furthermore, we introduce USEAgentPlus, an enhanced agentic system that extends prior agents by incorporating dedicated tools for environment management. This enables effective solutions for systems-integration tasks and facilitates experimental comparison. Our results suggest that the proposed solution outperforms existing approaches, achieving success on diverse open-source projects evaluated against a standard software engineering research benchmark.
At a broad level, our work contributes in taking the automation offered by AI agents to the next stage of the software lifecycle - from  software development and maintenance to software systems integration.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
编码智能体在持续集成与测试中的应用。

### 2. 核心内容
编码智能体已能通过问题解决维护代码库，但很少参与将改动集成并落地到复杂软件项目中。本文研究维护者在整合AI生成建议时会遇到的技术挑战，如构建问题和系统测试，并比较多种软件工程智能体应对这些运维化任务的能力。研究揭示了现有编码智能体在持续集成与测试环节的局限，为让智能体真正参与软件交付流程提供了分析基础。

### 3. 对应检索需求
coding agents for automated test generation and documentation。

### 4. 来源与原文
- Source：ICLR-2026-Rejected-Public
- OpenReview：[https://openreview.net/forum?id=n8lAJLVdVN](https://openreview.net/forum?id=n8lAJLVdVN)
