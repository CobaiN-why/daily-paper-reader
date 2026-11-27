---
title: "SWE-QA: Can Language Models Answer Repository-level Code Questions?"
title_zh: SWE-QA：语言模型能回答仓库级代码问题吗？
authors: "Weihan Peng, Yuling Shi, Yuhang Wang, Xinyun Zhang, Beijun Shen, Xiaodong Gu"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://aclanthology.org/2026.findings-acl.402.pdf"
tags: ["query:ai-se"]
score: 8.0
evidence: 评估大模型回答仓库级代码问题的基准
tldr: 现有代码问答基准多聚焦小型自包含代码片段，难以反映真实仓库中跨文件导航与架构理解的需求。本文提出 SWE-QA，一个仓库级代码问答基准，包含 720 个高质量问答对，要求模型在多文件与长程依赖上进行推理并给出有依据的答案。该工作为评估语言模型在真实软件工程环境下的代码理解与推理能力提供了更贴近实际的测试集。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl402/fig-001.webp\", \"caption\": \"\", \"page\": 2, \"index\": 1, \"width\": 455, \"height\": 432}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl402/fig-002.webp\", \"caption\": \"\", \"page\": 2, \"index\": 2, \"width\": 455, \"height\": 432}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl402/fig-003.webp\", \"caption\": \"\", \"page\": 2, \"index\": 3, \"width\": 455, \"height\": 433}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl402/fig-004.webp\", \"caption\": \"\", \"page\": 2, \"index\": 4, \"width\": 455, \"height\": 433}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl402/fig-005.webp\", \"caption\": \"\", \"page\": 2, \"index\": 5, \"width\": 455, \"height\": 433}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl402/fig-006.webp\", \"caption\": \"\", \"page\": 12, \"index\": 6, \"width\": 899, \"height\": 1094}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl402/fig-007.webp\", \"caption\": \"\", \"page\": 12, \"index\": 7, \"width\": 899, \"height\": 1094}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl402/fig-008.webp\", \"caption\": \"\", \"page\": 12, \"index\": 8, \"width\": 899, \"height\": 416}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl402/fig-009.webp\", \"caption\": \"\", \"page\": 12, \"index\": 9, \"width\": 899, \"height\": 416}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl402/fig-010.webp\", \"caption\": \"\", \"page\": 12, \"index\": 10, \"width\": 897, \"height\": 261}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl402/fig-011.webp\", \"caption\": \"\", \"page\": 12, \"index\": 11, \"width\": 897, \"height\": 261}]"
motivation: 现有代码问答基准局限于小片段，无法体现真实仓库的跨文件推理难度。
method: 构建包含 720 个问答对的仓库级代码问答基准，强调多文件导航与长程依赖。
result: 该基准表明语言模型在真实仓库级代码理解上仍有较大提升空间。
conclusion: SWE-QA 为智能软件工程工具的代码理解能力评估提供了真实场景。
---

## Abstract
Understanding and reasoning about entire soft-ware repositories is an essential capability for intelligent software engineering tools. While existing benchmarks such as CoSQA and CodeQA have advanced the field, they predominantly focus on small, self-contained code snippets. These setups fail to capture the complexity of real-world repositories, where effective understanding and reasoning often require navigating multiple files, understanding software architecture, and grounding answers in long-range code dependencies. In this paper, we present SWE-QA, a repository-level code question answering (QA) benchmark designed to facilitate research on automated QA systems in realistic code environments. SWE-QA involves 720 high-quality question-answer pairs spanning diverse categories, including intention understanding, cross-file reasoning, and multi-hop dependency analysis. To construct SWE-QA, we first crawled 77,100 GitHub issues from 12 popular repositories. Based on an analysis of naturally occurring developer questions extracted from these issues, we developed a two-level taxonomy of repository-level questions and constructed a set of seed questions for each category. For each category, we manually curated and validated questions and collected their corresponding answers. We evaluate six advanced LLMs on SWE-QA under various context augmentation strategies. Experimental results highlight the promise of LLMs.

---

## 论文详细总结（自动生成）

# SWE-QA 论文结构化总结

## 1. 核心问题与研究动机

- **核心问题**：现有代码问答基准（如 CoSQA、CodeQA）大多聚焦于**小型、自包含的代码片段、函数或 API**，难以反映真实软件仓库中的代码理解任务。
- **真实需求**：开发者回答仓库级问题时，往往需要跨多个文件导航、理解软件架构、追踪调用链与依赖关系，并在长程代码依赖上给出有依据的答案。
- **论文含义**：作者提出 **SWE-QA**，一个仓库级代码问答基准，用于评估语言模型在真实开源仓库环境下进行代码理解、跨文件推理和多跳依赖分析的能力。
- **基准规模**：720 个高质量问答对，覆盖 15 个 Python 开源仓库，涉及 13,300 个文件、22,522 个类、142,404 个函数和超过 340 万行代码。

## 2. 方法论

### 2.1 核心思想

SWE-QA 不是简单从代码片段生成问答，而是从真实 GitHub Issue 中挖掘开发者问题模式，建立仓库级问题分类体系，再结合代码结构解析、LLM 生成和人工校验构建高质量问答对。

### 2.2 基准构建流程

论文将构建流程分为四个阶段：

1. **种子问题收集与分类体系构建**
   - 爬取 SWE-bench 使用的 12 个热门仓库中的 **77,100 个 GitHub Issue**。
   - 过滤正文长度不少于 1,000 字符的 Issue，得到 **41,955 个 Issue**。
   - 使用 LLM 提取代码理解相关问题，得到 **127,415 个问题**，平均每个 Issue 3.04 个问题。
   - 人工分析 1,000 个问题，建立两级分类体系：
     - 一级：**What、Why、Where、How**
     - 二级：12 种意图，包括架构探索、概念/定义、依赖追踪、设计理由、目的探索、性能、数据/控制流、功能定位、标识符定位、系统设计、算法实现、API/框架支持。
   - 问题分布：How 约 35.2%，Where 约 28.4%，Why 约 23.1%，What 约 13.3%。

2. **问题实例化与扩展**
   - 使用 **tree-sitter** 解析仓库结构，构建包含 Repository、File、Class、Method、Function、Attribute、Variable 等节点及其关系的类型图。
   - 记录函数调用关系、文件导入关系等，以支持跨文件和多跳推理。
   - 围绕目标类/方法选取局部子图，结合每个类别的种子模板，由 LLM 生成具体、非复合、具有多跳推理难度的仓库级问题。
   - 最终从 15 个仓库生成候选问题：12 个来自 SWE-Bench，3 个来自 SWE-Bench-Live。

3. **答案收集**
   - 构建仓库代码元素索引，包括函数、类及其依赖关系。
   - 通过语义相似度匹配和结构依赖分析检索相关代码片段、文档和架构元数据。
   - 使用强 LLM 在检索上下文基础上生成初步答案，并要求引用代码位置、避免幻觉。
   - 4 名具有至少三年开发经验的专家使用 Cursor 等工具辅助审核和修正答案。

4. **数据验证**
   - 每道题由两名专家独立回答并交叉验证；若分歧显著，由第三名专家参与讨论达成共识。
   - 进行质量过滤：剔除歧义问题、事实错误答案、不完整答案或无法充分基于仓库代码和文档的答案。
   - 按仓库和一级类别平衡，最终每个仓库约 48 个问答对，总计 720 个。

### 2.3 基准统计特征

- 平均问题长度：**28.62 词**。
- 平均答案长度：**266.64 词**。
- 平均每个问题涉及 **8.71 个函数、3.19 个文件**。
- 平均推理链深度 **4.72**，依赖链深度 **2.96**。
- **90.9%** 的问题推理链深度大于 1；**77.6%** 需要跨文件知识。

## 3. 实验设计

### 3.1 数据集与 Benchmark

- 使用论文构建的 **SWE-QA** 基准：
  - 720 个问答对；
  - 15 个 Python 仓库；
  - 覆盖 What、Why、Where、How 四类及 12 种细粒度意图；
  - 强调跨文件、多跳依赖和仓库级理解。

### 3.2 对比模型

评估了 6 个代表性 LLM：

- Kimi K2
- Qwen3-Coder-30B-A3B-Instruct
- Qwen3-Coder-480B-A35B-Instruct
- GLM-4.6
- Gemini 2.5 Pro
- GPT-5.1

### 3.3 对比方法

每个模型测试 5 类方法：

1. **Direct Prompting**：不提供仓库上下文，直接回答。
2. **Function Chunking RAG**：按函数语义边界切分代码，使用 voyage-code-3 嵌入，Top-K=10。
3. **Sliding Window RAG**：以 500 行窗口、100 行重叠切分代码，Top-K=10。
4. **SWE-agent**：将原用于 Issue 解决的 agent 适配到问答任务。
5. **OpenHands**：使用 OpenHands SDK，包含 terminal、file_editor、task_tracker、finish、think 等工具。

另外还评估了两个商业编程工具作为系统级基线：

- **Tongyi Lingma**
- **Cursor-agent**

### 3.4 评价指标

- 采用 **LLM-as-Judge**，评委模型为 **Claude Sonnet 4.5**。
- 五个维度各 20 分，总分 100：
  - Correctness
  - Completeness
  - Relevance
  - Clarity
  - Coherence / Reasoning
- 每个实例每维度评估 5 次，采用多数投票。
- 为减少偏差：系统匿名、答案顺序随机化、评委与候选模型严格分离。
- 另进行小规模人类评估验证自动评分可靠性。

## 4. 资源与算力

- 论文明确提到的硬件环境：
  - **Intel Xeon Gold 6254 CPU**
  - **NVIDIA A100-80G GPU**
- 未明确说明：
  - GPU 数量；
  - 训练时长；
  - 总算力消耗。
- 该工作主要是基准构建与推理评估，未涉及大规模模型训练。实验设置中所有 LLM 解码温度设为 0，OpenHands 和 SWE-agent 默认最多 10 轮推理-动作迭代。

## 5. 实验数量与充分性

### 5.1 实验规模

- 主实验：**6 个模型 × 5 种方法 = 30 组系统配置**，另加 2 个商业工具基线。
- 分类分析：使用 OpenHands，在 12 种问题意图上比较 6 个模型。
- 跨仓库分析：使用 OpenHands，在 15 个仓库上比较 6 个模型。
- 人类评估：3 名专业软件工程师对 GPT-5.1 的 5 种方法进行盲评。
- 成本分析：统计不同方法的输入/输出 token 消耗。
- 案例研究：分析 GPT-5.1 + OpenHands 的典型错误，并收集 100 个错误案例。

### 5.2 充分性与公平性评价

- **优点**：
  - 模型覆盖较广，包含开源与闭源、不同规模模型。
  - 方法覆盖从直接提示、RAG 到 agent 框架，能够体现上下文增强的增益。
  - 同时报告自动评分和人类评估，趋势一致。
  - 使用匿名、随机顺序、固定评委、温度 0 等措施降低偏差。
- **不足**：
  - 人类评估规模较小，仅 3 名评估者，且只评估 GPT-5.1 的 5 种方法。
  - 基准仅覆盖 Python 仓库。
  - 部分分析主要基于 OpenHands 一种 agent 配置。
  - 未进行传统意义上的大规模消融实验，更多是方法间横向比较。
  - 统计表中存在轻微不一致：正文称每个仓库 48 个问答对、总计 720，但表 6 中 flask 显示 47 个。

## 6. 主要结论与发现

- **直接提示效果最差**：无仓库上下文时性能最低，例如 Kimi K2 仅 51.47 分。
- **RAG 显著提升**：例如 Kimi K2 使用 Sliding Window RAG 提升至 62.44。
- **Agent 框架进一步提升**：
  - Kimi K2 + SWE-agent 达到 67.72；
  - GLM-4.6 + OpenHands 达到 70.15；
  - GPT-5.1 + OpenHands 达到最佳 **70.79**。
- **商业工具表现强**：
  - Cursor 达到 70.66；
  - Tongyi Lingma 达到 69.07。
- **小模型受益有限**：Qwen3-Coder-30B-A3B-Instruct 使用 agent 框架时并不稳定优于 RAG，说明 agent 规划、工具调用和长期记忆对模型能力要求较高。
- **问题类型差异明显**：
  - Why 类问题平均最高，约 69.77，尤其是设计理由类 71.48；
  - What 类最低，约 65.81，其中架构探索仅 61.84；
  - Where 类约 66.76，数据/控制流定位约 65.05；
  - 模型更擅长自然语言中已有解释的问题，较弱于需要跨文件追踪和隐式控制流重建的问题。
- **仓库间差异显著**：
  - Flask 最容易，平均 75.42；
  - Requests 73.28，Matplotlib 72.78；
  - Pylint 最难，仅 62.01；Conan 64.51。
  - SWE-Bench 仓库平均 68.59，SWE-Bench-Live 仓库平均 64.98，后者更具挑战性，可能与数据泄漏更少有关。
- **成本与性能存在权衡**：
  - RAG 的 token 消耗超过直接提示 10 倍；
  - Agent 框架约消耗直接提示的 100 倍、RAG 的 10 倍；
  - 但 agent 在完整性和正确性上提升明显。

## 7. 优点

- **基准定位清晰**：聚焦真实仓库级代码问答，弥补片段级基准的不足。
- **分类体系有实证基础**：从 77,100 个 GitHub Issue 中挖掘开发者真实问题，再建立两级 taxonomy。
- **数据质量较高**：LLM 生成结合多轮人工审核、交叉验证和质量过滤。
- **强调多跳与跨文件推理**：统计显示绝大多数问题需要跨文件知识和非平凡推理链。
- **实验维度丰富**：覆盖多种模型、多种上下文增强方法、商业工具、问题类型、仓库类型和成本分析。
- **评估设计较严谨**：LLM-as-Judge 配合人类评估，匿名化、随机顺序、固定评委，降低部分偏差。
- ** pipeline 可扩展**：提出可复用的问答生成流程，可迁移到新仓库。

## 8. 不足与局限

- **语言覆盖有限**：仅覆盖 Python 仓库，结论向其他编程语言推广需谨慎。
- **静态快照**：基准基于静态代码快照，不反映仓库持续演化、版本迁移和动态开发过程。
- **评估偏差风险**：
  - LLM-as-Judge 可能引入评分偏差；
  - 人类评估规模有限，仅 3 人且只覆盖 GPT-5.1 的部分方法；
  - 答案由强 LLM 辅助生成并经人工修正，可能仍存在构造偏差。
- **仓库覆盖有限**：15 个仓库虽多样，但未必覆盖小型项目、领域特定项目或非 Python 生态。
- **agent 实验配置有限**：分类和跨仓库分析主要基于 OpenHands，其他 agent 配置的系统性分析较少。
- **成本较高**：agent 方法 token 消耗巨大，实际部署需权衡成本与收益。
- **统计细节存在小瑕疵**：正文与表 6 在 flask 样本数上存在 47/48 的不一致，虽不影响整体结论，但反映数据统计需进一步核对。

（完）
