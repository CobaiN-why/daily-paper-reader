---
title: "AgentHijack: Benchmarking Computer Use Agent Robustness to Common Environment Corruptions"
title_zh: AgentHijack：评测计算机使用智能体对常见环境干扰的鲁棒性
authors: "Jingwei Sun, Jianing Zhu, Yuanyi Li, Tongliang Liu, Xia HU, Bo Han"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf/f84044826146bada20f3a545c79c9b42e8939d59.pdf"
tags: ["query:ai-se"]
score: 5.0
evidence: 评测计算机使用智能体在环境干扰下的鲁棒性
tldr: 由多模态大模型驱动的计算机使用智能体正成为完成数字工作流的助手，但真实环境充满弹窗、分辨率变化等干扰。AgentHijack构建基准，引入9种可配置的常见干扰来复现不完美场景，评测多类桌面任务中智能体的鲁棒性。研究揭示环境不确定性会破坏执行流程，为提升大模型智能体的安全与稳定性提供了评测工具。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 真实执行环境中的弹窗、分辨率变化等干扰会影响智能体感知与控制。
method: 构建含9种可配置常见干扰的基准，评测多类桌面任务中的智能体。
result: 揭示环境不确定性会显著扰乱智能体的执行流程与稳定性。
conclusion: 为提升大模型智能体在真实环境下的鲁棒与安全提供了评测手段。
---

## Abstract
Autonomous computer use agents that powered by multimodal large language models (MLLMs) are emerging as capable assistants for completing complex digital workflows. However, real-world execution environments are far from ideal: pop-ups, resolution changes, and competing applications frequently interfere with agent perception and control. We introduce AgentHijack, a benchmark designed to evaluate the robustness of computer-use agents under common corruptions, where the uncertainties in dynamic environment disrupt the execution flow without direct adversarial intent. Specifically, AgentHijack introduces 9 configurable common corruptions to replicate realistic imperfect scenarios. We evaluate a variety of desktop tasks that utilize MLLM-based agents and discover that even minor instances of corruption can result in substantial performance degradation, which emphasizes the fragility of agents and underscores the necessity of robustness evaluation. Afterward, we propose AgentHijack-Agent, a framework that integrates an action generator with enhanced grounding capabilities and an onlooker responsible for behavior summarization and environment checking. Extensive experiments validate its effectiveness. Our code, environment, baseline models and data are publicly available at: \url{https://AgentHijack.github.io}.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
评测计算机使用智能体在环境干扰下的鲁棒性。

### 2. 核心内容
由多模态大模型驱动的计算机使用智能体正成为完成数字工作流的助手，但真实环境充满弹窗、分辨率变化等干扰。AgentHijack构建基准，引入9种可配置的常见干扰来复现不完美场景，评测多类桌面任务中智能体的鲁棒性。研究揭示环境不确定性会破坏执行流程，为提升大模型智能体的安全与稳定性提供了评测工具。

### 3. 对应检索需求
大模型安全。

### 4. 来源与原文
- Source：ICML-2026-Accepted
- OpenReview：[https://openreview.net/forum?id=0H5Im3Xvuf](https://openreview.net/forum?id=0H5Im3Xvuf)
