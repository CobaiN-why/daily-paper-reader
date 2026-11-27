---
title: "InfiniteWeb: Scalable Web Environment Synthesis for GUI Agent Training"
title_zh: InfiniteWeb：面向GUI智能体训练的可扩展Web环境合成
authors: "Ziyun Zhang, Zezhou Wang, Xiaoyi Zhang, Zongyu Guo, Jiahao Li, Bin Li, Yan Lu"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://aclanthology.org/2026.acl-long.1313.pdf"
tags: ["query:ai-se"]
score: 4.0
evidence: 为GUI智能体训练自动合成Web环境
tldr: GUI智能体训练受限于稀缺且合适的交互环境，而用大模型生成单一网页易、构建多页互联的真实网站难。作者提出InfiniteWeb系统，通过统一规范、任务驱动的测试驱动开发以及网站种子变异与参考设计图结合，规模化自动生成可用Web环境。系统还生成可验证的任务评估器以提供强化学习的稠密奖励，为智能体训练提供了可扩展环境。
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1313/fig-001.webp\", \"caption\": \"\", \"page\": 1, \"index\": 1, \"width\": 5504, \"height\": 3072}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1313/fig-002.webp\", \"caption\": \"\", \"page\": 2, \"index\": 2, \"width\": 10312, \"height\": 4048}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1313/fig-003.webp\", \"caption\": \"\", \"page\": 7, \"index\": 3, \"width\": 5504, \"height\": 3072}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1313/fig-004.webp\", \"caption\": \"\", \"page\": 8, \"index\": 4, \"width\": 5504, \"height\": 3072}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1313/fig-005.webp\", \"caption\": \"\", \"page\": 8, \"index\": 5, \"width\": 5504, \"height\": 3072}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1313/fig-006.webp\", \"caption\": \"\", \"page\": 12, \"index\": 6, \"width\": 1920, \"height\": 1080}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1313/fig-007.webp\", \"caption\": \"\", \"page\": 12, \"index\": 7, \"width\": 1920, \"height\": 1080}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1313/fig-008.webp\", \"caption\": \"\", \"page\": 12, \"index\": 8, \"width\": 1920, \"height\": 1080}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1313/fig-009.webp\", \"caption\": \"\", \"page\": 12, \"index\": 9, \"width\": 1920, \"height\": 1080}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1313/fig-010.webp\", \"caption\": \"\", \"page\": 12, \"index\": 10, \"width\": 1920, \"height\": 1080}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1313/fig-011.webp\", \"caption\": \"\", \"page\": 13, \"index\": 11, \"width\": 1920, \"height\": 1080}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1313/fig-012.webp\", \"caption\": \"\", \"page\": 13, \"index\": 12, \"width\": 1920, \"height\": 1080}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1313/fig-013.webp\", \"caption\": \"\", \"page\": 13, \"index\": 13, \"width\": 1920, \"height\": 1080}]"
motivation: GUI智能体训练缺乏合适环境，大模型虽能生成单页，但构建多页互联的真实网站仍有困难。
method: 提出InfiniteWeb系统，结合统一规范、任务驱动的测试驱动开发与参考设计图，规模化合成Web环境并生成任务评估器。
result: 该系统可自动生成功能可用的多页网站环境，并提供可验证评估器以支撑强化学习的稠密奖励。
conclusion: InfiniteWeb为GUI智能体训练提供了可扩展的环境合成途径，但主要面向界面交互而非编码任务。
---

## Abstract
GUI agents that interact with graphical interfaces on behalf of users are a promising direction for practical AI assistants, yet training them is hindered by scarce suitable environments. We present InfiniteWeb, a system that automatically generates functional web environments at scale for GUI agent training. While LLMs perform well on generating a single webpage, building a realistic and functional website with many interconnected pages faces challenges. We address these challenges through unified specification, task-centric test-driven development, and combining website seed variation with reference design images. Our system also generates verifiable task evaluators enabling dense reward signals for reinforcement learning. Experiments show that our system surpasses commercial coding agents at realistic website construction, and GUI agents trained on our generated environments achieve significant performance improvements on OSWorld and Online-Mind2Web, demonstrating the effectiveness of the proposed system.

---

## 论文详细总结（自动生成）

# InfiniteWeb 论文中文结构化总结

## 1. 核心问题与整体含义

- **研究动机**：GUI 智能体（能看截图、理解 UI、执行点击/输入等操作）是实用 AI 助手的重要方向，但其训练受限于**合适交互环境稀缺**。
- **现有瓶颈**：MiniWoB++、WebArena、OSWorld 等 benchmark 多为人工构建，需设计网站/应用、定义任务、编写评估器，规模通常只有数十到数百个应用，难以支撑可泛化的智能体训练。
- **已有合成工作的不足**：已有任务/轨迹合成方法多在**原有 benchmark 环境内**生成数据，环境本身仍局限于少量特定应用。
- **核心问题**：能否**自动、规模化地生成完整可用的 Web 环境**，并同时生成任务与可验证评估器，用于 GUI 智能体强化学习训练？
- **整体含义**：论文将“环境合成”而非仅仅“任务/轨迹合成”作为扩展训练信号的关键路径，试图从源头解决 GUI 智能体训练环境不足的问题。生成多页互联网站面临三个挑战：**一致性**（跨页数据/接口/状态一致）、**正确性**（LLM 代码常有 bug，错误奖励会破坏 RL）、**多样性**（LLM 易生成重复任务与同质视觉风格）。

## 2. 方法论

### 2.1 核心思想

InfiniteWeb 输入一个**网站种子**（如“在线书店”）和一张**参考设计图**，输出一个可运行的网站、若干任务及对应自动评估器。系统以“任务”为中心组织生成流程：先由任务推导统一数据模型与接口，再并行生成后端业务逻辑与前端页面，最后生成任务评估器。后端与前端并行执行。

### 2.2 四个关键阶段

- **统一规范阶段（Unified Specification）**
  - 根据网站种子生成 realistic 用户任务，任务覆盖不同功能与复杂度。
  - 从任务中抽取数据模型（如 Product、Cart、Order 及字段/关系）、页面架构与统一编程接口。
  - 接口设计为“用户可见”形式：系统管理参数（如 `userId`、`sessionId`）被隐藏并由 `localStorage` 自动获取；例如 `addToCart(userId, sessionId, productId, quantity)` 包装为 `addToCart(productId, quantity)`。
  - 目的：保证所有页面共享相同 API 签名、数据格式和状态管理，解决跨页一致性。

- **任务中心后端（Task-Centric Backend）**
  - 先生成与
