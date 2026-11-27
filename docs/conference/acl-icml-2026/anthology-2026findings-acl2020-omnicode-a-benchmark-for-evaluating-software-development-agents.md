---
title: "OmniCode: A Benchmark for Evaluating Software Development Agents"
title_zh: OmniCode：评估软件开发智能体的基准
authors: "Atharv Sonwane, Eng-Shen Tu, Wei-Chung Lu, Claas Beger, Carter Larsen, Debjit Dhar, Simon Alford, Rachel Chen, Ronit Pattanayak, Tuan Anh Dang, Guohao Chen, Gloria Geng, Kevin Ellis, Saikat Dutta"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://aclanthology.org/2026.findings-acl.2020.pdf"
tags: ["query:ai-se"]
score: 8.0
evidence: 评估LLM驱动的软件开发智能体的基准
tldr: LLM驱动的编码智能体正重塑软件开发方式，但HumanEval、SWE-Bench等流行基准只覆盖竞赛编程、补丁生成等狭窄任务，难以反映工程师面对的更广泛工作。作者提出OmniCode基准，包含跨三类编程任务共1794个任务，覆盖比代码或补丁生成更广的软件工程任务类别。该基准旨在更严格地评估编码智能体在真实开发中的综合能力。工作为智能体式软件工程研究提供了更具挑战性的评测工具。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl2020/fig-001.webp\", \"caption\": \"\", \"page\": 1, \"index\": 1, \"width\": 5298, \"height\": 188}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl2020/fig-002.webp\", \"caption\": \"\", \"page\": 1, \"index\": 2, \"width\": 422, \"height\": 421}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl2020/fig-003.webp\", \"caption\": \"\", \"page\": 1, \"index\": 3, \"width\": 481, \"height\": 468}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl2020/fig-004.webp\", \"caption\": \"\", \"page\": 1, \"index\": 4, \"width\": 2039, \"height\": 649}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl2020/fig-005.webp\", \"caption\": \"\", \"page\": 1, \"index\": 5, \"width\": 2610, \"height\": 694}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl2020/fig-006.webp\", \"caption\": \"\", \"page\": 1, \"index\": 6, \"width\": 2610, \"height\": 694}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl2020/fig-007.webp\", \"caption\": \"\", \"page\": 1, \"index\": 7, \"width\": 2610, \"height\": 345}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl2020/fig-008.webp\", \"caption\": \"\", \"page\": 1, \"index\": 8, \"width\": 5298, \"height\": 188}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl2020/fig-009.webp\", \"caption\": \"\", \"page\": 1, \"index\": 9, \"width\": 518, \"height\": 518}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl2020/fig-010.webp\", \"caption\": \"\", \"page\": 1, \"index\": 10, \"width\": 459, \"height\": 459}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl2020/fig-011.webp\", \"caption\": \"\", \"page\": 1, \"index\": 11, \"width\": 501, \"height\": 500}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl2020/fig-012.webp\", \"caption\": \"\", \"page\": 1, \"index\": 12, \"width\": 411, \"height\": 411}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl2020/fig-013.webp\", \"caption\": \"\", \"page\": 1, \"index\": 13, \"width\": 456, \"height\": 443}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl2020/fig-014.webp\", \"caption\": \"\", \"page\": 4, \"index\": 14, \"width\": 1457, \"height\": 376}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl2020/fig-015.webp\", \"caption\": \"\", \"page\": 4, \"index\": 15, \"width\": 675, \"height\": 318}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl2020/fig-016.webp\", \"caption\": \"\", \"page\": 4, \"index\": 16, \"width\": 1366, \"height\": 504}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl2020/fig-017.webp\", \"caption\": \"\", \"page\": 4, \"index\": 17, \"width\": 675, \"height\": 212}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl2020/fig-018.webp\", \"caption\": \"\", \"page\": 4, \"index\": 18, \"width\": 348, \"height\": 349}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl2020/fig-019.webp\", \"caption\": \"\", \"page\": 4, \"index\": 19, \"width\": 348, \"height\": 349}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl2020/fig-020.webp\", \"caption\": \"\", \"page\": 4, \"index\": 20, \"width\": 1457, \"height\": 375}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl2020/fig-021.webp\", \"caption\": \"\", \"page\": 4, \"index\": 21, \"width\": 770, \"height\": 248}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl2020/fig-022.webp\", \"caption\": \"\", \"page\": 4, \"index\": 22, \"width\": 1457, \"height\": 695}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl2020/fig-023.webp\", \"caption\": \"\", \"page\": 4, \"index\": 23, \"width\": 1656, \"height\": 319}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl2020/fig-024.webp\", \"caption\": \"\", \"page\": 4, \"index\": 24, \"width\": 1656, \"height\": 319}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl2020/fig-025.webp\", \"caption\": \"\", \"page\": 4, \"index\": 25, \"width\": 695, \"height\": 248}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl2020/fig-026.webp\", \"caption\": \"\", \"page\": 4, \"index\": 26, \"width\": 1724, \"height\": 422}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl2020/fig-027.webp\", \"caption\": \"\", \"page\": 4, \"index\": 27, \"width\": 1724, \"height\": 421}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl2020/fig-028.webp\", \"caption\": \"\", \"page\": 5, \"index\": 28, \"width\": 695, \"height\": 401}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl2020/fig-029.webp\", \"caption\": \"\", \"page\": 5, \"index\": 29, \"width\": 644, \"height\": 643}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl2020/fig-030.webp\", \"caption\": \"\", \"page\": 5, \"index\": 30, \"width\": 1232, \"height\": 616}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl2020/fig-031.webp\", \"caption\": \"\", \"page\": 5, \"index\": 31, \"width\": 1232, \"height\": 616}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl2020/fig-032.webp\", \"caption\": \"\", \"page\": 5, \"index\": 32, \"width\": 1177, \"height\": 1177}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl2020/fig-033.webp\", \"caption\": \"\", \"page\": 5, \"index\": 33, \"width\": 557, \"height\": 279}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl2020/fig-034.webp\", \"caption\": \"\", \"page\": 6, \"index\": 34, \"width\": 504, \"height\": 582}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl2020/fig-035.webp\", \"caption\": \"\", \"page\": 6, \"index\": 35, \"width\": 446, \"height\": 362}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl2020/fig-036.webp\", \"caption\": \"\", \"page\": 6, \"index\": 36, \"width\": 552, \"height\": 428}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl2020/fig-037.webp\", \"caption\": \"\", \"page\": 6, \"index\": 37, \"width\": 600, \"height\": 596}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl2020/fig-038.webp\", \"caption\": \"\", \"page\": 8, \"index\": 38, \"width\": 1264, \"height\": 956}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl2020/fig-039.webp\", \"caption\": \"\", \"page\": 8, \"index\": 39, \"width\": 630, \"height\": 470}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl2020/fig-040.webp\", \"caption\": \"\", \"page\": 11, \"index\": 40, \"width\": 1180, \"height\": 780}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl2020/fig-041.webp\", \"caption\": \"\", \"page\": 11, \"index\": 41, \"width\": 1180, \"height\": 780}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl2020/fig-042.webp\", \"caption\": \"\", \"page\": 11, \"index\": 42, \"width\": 1380, \"height\": 980}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl2020/fig-043.webp\", \"caption\": \"\", \"page\": 13, \"index\": 43, \"width\": 1980, \"height\": 1180}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl2020/fig-044.webp\", \"caption\": \"\", \"page\": 14, \"index\": 44, \"width\": 1472, \"height\": 1756}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl2020/fig-045.webp\", \"caption\": \"\", \"page\": 20, \"index\": 45, \"width\": 4469, \"height\": 4466}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl2020/fig-046.webp\", \"caption\": \"\", \"page\": 21, \"index\": 46, \"width\": 4468, \"height\": 4466}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl2020/fig-047.webp\", \"caption\": \"\", \"page\": 24, \"index\": 47, \"width\": 4468, \"height\": 4466}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl2020/fig-048.webp\", \"caption\": \"\", \"page\": 26, \"index\": 48, \"width\": 2992, \"height\": 2379}]"
motivation: 现有编码基准如HumanEval与SWE-Bench只考察补丁生成等狭窄任务，无法反映真实开发的多样需求。
method: 构建OmniCode基准，涵盖三类编程任务共1794个任务，覆盖比代码生成更广的软件工程类别。
result: 该基准提供了更广泛多样的任务集合，用于严格评估LLM编码智能体的综合开发能力。
conclusion: 为推进更强大的自主编码智能体研究提供了更具挑战性和代表性的评测基础。
---

## Abstract
LLM-powered coding agents are redefining how real-world software is developed. To drive the research towards better coding agents, we require challenging benchmarks that can rigorously evaluate the ability of such agents to perform various software engineering tasks. However, popular coding benchmarks such as HumanEval and SWE-Bench focus on narrowly scoped tasks such as competition programming and patch generation. In reality, software engineers have to handle a broader set of tasks for real-world software development. To address this gap, we propose OmniCode, a novel software engineering benchmark that contains a broader and more diverse set of task categories beyond code or patch generation. Overall, OmniCode contains 1794 tasks spanning three programming languages – Python, Java, and C++ – and four key categories: bug fixing, test generation, code review fixing, and style fixing. In contrast to prior software engineering benchmarks, the tasks in OmniCode are (1) manually validated to eliminate ill-defined problems, and (2) synthetically crafted or recently curated to avoid data leakage issues, presenting a new framework for synthetically generating diverse software tasks from limited real-world data. We evaluate OmniCode with popular agent frameworks such as SWE-Agent and show that while they may perform well on bug fixing for Python, they fall short on tasks such as Test Generation and in languages such as C++ and Java. For instance, SWE-Agent achieves a maximum of 25.0% with DeepSeek-V3.1 on C++ Test Generation. OmniCode aims to serve as a robust benchmark and spur the development of agents that can perform well across different aspects of software development.

---

## 论文详细总结（自动生成）

# OmniCode：评估软件开发智能体的基准 — 论文总结

## 1. 核心问题与研究动机

- **背景**：LLM 驱动的编码智能体正在重塑真实软件开发流程，亟需具有挑战性的基准来严格评估其能力并推动研究进步。
- **现有基准的局限**：HumanEval、SWE-Bench、CodeContests 等主流基准任务范围狭窄，集中于竞赛编程与补丁生成（patch generation），无法反映真实软件工程中更广泛、异构的任务谱系。
- **研究缺口**：真实开发还涉及编写测试、响应代码评审、执行风格规范等大量活动；同时已有基准存在数据泄漏、问题定义不清等隐患。
- **整体含义**：作者提出 OmniCode——一个覆盖多任务类别、多语言、经人工验证且规避数据泄漏的软件工程基准，旨在更全面、严格地衡量编码智能体的综合开发能力。

## 2. 方法论

### 2.1 核心思想
- 以真实 GitHub Pull Request 及其关联 issue、patch 构成 **base instance**，再通过 LLM 与工具增强，从有限的真实数据中**合成生成多种任务类型**，实现“一份真实数据、多种任务视图”的评估框架。
- 覆盖 **4 类任务**（bug fixing、test generation、review response、style fixing）× **3 种语言**（Python、Java、C++），共 **1794 个任务**（Python 963、Java 418、C++ 413）。

### 2.2 数据收集与基础实例
- 来源：SWE-Bench-Verified、Multi-SWE-Bench，以及从热门开源仓库新采集的 PR。
- 筛选标准：(1) 解决某个 issue；(2) 至少引入一个测试；再经人工过滤，剔除定义不清、依赖无法安装、测试不稳定、仅涉及文档/配置的实例。
- 规模：**494 个 base instance**，覆盖 **28 个仓库**（如 Scikit-learn、Sympy、Fmt、Simdjson、Django、Logstash、Jackson、Mockito），并为每个实例构建可执行代码的容器化环境（手动确定依赖并以测试套件验证）。

### 2.3 四类任务的构建
- **Bug Fixing**：直接使用 base instance，提供 issue 描述与区分修复前后状态的测试，要求生成 patch，并检查回归。
- **Test Generation**：引入 **bad patch** 概念——由 Agentless 等模型失败尝试收集，或由 LLM（Gemini-2.5-Flash）扰动正确 patch 生成“看似合理但错误”的补丁。生成的测试须**通过 gold patch 且失败于所有 bad patch** 才算成功，模拟变异测试思想。
- **Review Response**：用 LLM（Gemini-2.5-Flash）基于 bad patch、gold patch 与问题描述生成代码评审意见，要求智能体依据评审修正错误补丁。
- **Style Fixing**：用语言特定工具（Python 用 pylint、C++ 用 clang-tidy、Java 用 PMD）扫描仓库风格违规，剔除琐碎规则后按文件分组为实例（Python 144、C++ 147、Java 124，平均约 9 个违规/实例）；修复后重新运行风格检查与测试套件。

### 2.4 关键公式与评估指标
- **Patch 复杂度**：`ΔFiles + ΔHunks + ΔLines/10`，综合反映改动广度、碎片化程度与文本变更量；据此得出难度排序 **C++ > Java > Python**，与下游智能体表现一致。
- **Style-Fixing Score**：
  - 若测试全部通过：`max((resolved − new) / original, 0)`；
  - 否则记 0 分。该指标同时惩罚引入新风格错误、奖励解决原有问题，并保证功能不被破坏。

## 3. 实验设计

- **评估对象（Benchmark）**：OmniCode 全部 1794 个任务，按 4 类任务 × 3 种语言切分。
- **智能体框架**：
  - **SWE-Agent**（默认设置，单实例成本上限 $2.0）；
  - **Aider**（仅用 Gemini-2.5-Flash，timeout 20 分钟，重试 3 次）。
- **对比模型**（SWE-Agent 下）：Gemini-2.5-Flash、Claude-4.6-Sonnet、GPT-5-mini、DeepSeek-V3.1、Qwen3-32B，共 5 个来自不同家族的 SOTA 模型。
- **分析维度**：
  - 主表（Table 2）跨语言、跨模型、跨任务性能；
  - SWE-Agent vs. Aider 的智能体式 vs. 流水线式对比（Table 3）；
  - 任务间相关性分析（Table 4，Pearson 系数）；
  - Patch 复杂度与解决率关系（Table 6、Figure 5）；
  - 是否纳入 bad patch 对测试评估的影响（Figure 6）；
  - Style-Fixing 的 Fix Rate 与 Error Ratio 分析（Table 5）；
  - Patch 生成率与预算约束分析（Table 7、Table 8）；
  - 失败模式分类（Appendix C）、人工评估（Appendix H）、置信区间（Appendix I）。

## 4. 资源与算力

- 论文**未明确报告** GPU 型号、数量或训练时长——因为该工作本质是**评估基准**，不涉及模型训练。
- 仅提及推理侧成本约束：SWE-Agent 单实例成本上限 **$2.0**；Aider 使用 Gemini-2.5-Flash，超时 20 分钟、重试 3 次。
- 作者指出 Claude-4.6-Sonnet 在 Java/C++ 上因 $2 预算在生成 patch 前即耗尽，导致分数被低估（Table 7、Table 8 给出仅统计已生成 patch 的修正分数）。

## 5. 实验数量与充分性

- **实验规模**：主实验为 5 模型 × 4 任务 × 3 语言（SWE-Agent）+ 1 模型 × 4 任务 × 3 语言（Aider），另有相关性、复杂度、bad patch 消融、风格错误类型、失败模式、人工评估、置信区间等多组分析，合计十余组系统性实验。
- **充分性**：
  - 覆盖多语言、多模型、多任务，且对每类任务均给出细粒度指标；
  - 通过 bad patch 消融（Figure 6）证明仅用 gold patch 会显著高估测试能力（如 Qwen C++ 从 4.5% 虚高至 22.7%）；
  - 提供 95% 置信区间，增强结论可靠性；
  - 人工评估（6 名研究者、20 个实例）验证合成 bad patch 与 review 的质量（98.9% review 至少部分正确，70% 无泄漏）。
- **客观性与公平性**：
  - 统一容器环境、统一 prompt 模板（Appendix D）、统一成本预算；
  - 但也存在**预算约束导致的偏差**（Claude 在复杂任务上被低估），作者以 Table 8 部分修正，属有限的公平性处理。

## 6. 主要结论与发现

- **Bug Fixing**：Python 表现最好（Claude-4.6-Sonnet 68.9%），Java 骤降至 31.2%、C++ 仅 19.6%（均为 DeepSeek-V3.1）。
- **Test Generation 是最难任务**：三语言最高仅 **25.0%**（DeepSeek-V3.1 on C++）；若只要求通过 gold patch 而不要求失败于 bad patch，分数会大幅虚高，说明许多测试只捕捉表层行为。
- **Review Response**：Python 67.9%（Claude），Java 44.3%、C++ 22.7%（DeepSeek）；提供评审能帮助解决更多**独特实例**（Java 15 vs. 4，C++ 4 vs. 2，Python 22 vs. 20）。
- **Style Fixing**：Python 可达 61.2%，Java 27.3%、C++ 35.6%；Fix Rate 虽高，但 Java/C++ 的 **Error Ratio 高达 2–5 倍**，说明风格修复易引入新错误。
- **智能体 vs. 流水线**：SWE-Agent 总体优于 Aider，Aider 在 C++ 上低 3–5 倍，反映交互式、多轮编译-运行循环对复杂任务的重要性。
- **任务相关性**：Bug Fixing 与 Review-Response 强相关（Pearson 0.921），与 Test Generation 中等相关（0.764），与 Style Fixing 弱相关（0.512）。
- **复杂度是潜在难度因子**：解决实例集中在低复杂度区，未解决实例呈重尾分布；低复杂度为主的基准可能高估智能体能力。

## 7. 优点

- **任务多样性**：首次系统性地将 bug fixing 之外的测试生成、评审响应、风格修复纳入统一基准，贴近真实开发流程。
- **合成数据方法论**：提出从有限真实数据合成多种任务的可复用 pipeline，并通过“新采集 + 合成”规避数据泄漏。
- **评估鲁棒性**：bad patch 机制显著提升测试质量评估的判别力，避免空洞测试蒙混过关。
- **严格的人工验证**：对 bad patch 合理性与 review 泄漏性进行人工抽检并报告一致性。
- **分析深入**：复杂度公式、任务间相关性、失败模式分类、成本-复杂度-预算交互分析，均提供了超出单纯 leaderboard 的洞察。
- **可复现与可扩展**：容器化环境、公开 prompt、代码与数据开源（GitHub），pipeline 易扩展至新语言与新任务。

## 8. 不足与局限

- **语言覆盖有限**：仅 Python、Java、C++，未涵盖配置系统、性能剖析、设计讨论等真实开发活动。
- **合成数据偏差风险**：bad patch 与 review 均由 LLM 生成，30% 的 review 存在中度信息泄漏，bad patch 平均合理性仅 2.10/3，可能影响任务难度分布的真实性。
- **预算约束引入的不公平**：固定 $2 预算使 Claude 在 Java/C++ 上频繁未生成 patch，原始分数低估其能力；虽给出修正分数，但主表结论仍受影响。
- **部分实例 bad patch 不足**：约 1/3 Python 实例缺少 approach-1 的 bad patch，C++/Java 也存在类似情况，可能削弱测试评估的严格性。
- **Aider 对比不完整**：仅用 Gemini-2.5-Flash 一个模型，智能体式 vs. 流水线式的结论推广性受限。
- **算力信息缺失**：未报告推理总成本、GPU 使用等资源细节，影响可复现性与成本评估。
- **风格任务定义依赖工具**：风格违规由 pylint/clang-tidy/PMD 定义，可能与项目实际规范或团队约定存在偏差；且风格修复可能引入功能回归（虽以测试套件兜底）。
- **基准静态性**：任务集固定，随着模型迭代可能逐渐饱和，需要持续更新（作者亦在结论中提出扩展方向）。

（完）
