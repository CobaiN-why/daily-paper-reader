---
title: "CodeWiki: Evaluating AI’s Ability to Generate Holistic Documentation for Large-Scale Codebases"
title_zh: CodeWiki：评估AI为大型代码库生成整体文档的能力
authors: "Anh Nguyen Hoang, Minh Le-Anh, Bach Le, Nghi D. Q. Bui"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://aclanthology.org/2026.findings-acl.288.pdf"
tags: ["query:ai-se"]
score: 9.0
evidence: 由LLM智能体自动生成仓库级文档
tldr: 全面的软件文档至关重要却制作成本高昂，而仓库级、架构感知的文档生成因代码库庞大超出大模型上下文而颇具挑战。作者提出CodeWiki统一框架，结合自顶向下层次分解、分治式智能体系统与自底向上综合，以保留架构上下文并扩展文档生成规模。该框架覆盖七种主流编程语言，能够产出整体性文档。工作为LLM驱动的自动化文档生成提供了可扩展方案。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl288/fig-001.webp\", \"caption\": \"\", \"page\": 2, \"index\": 1, \"width\": 3184, \"height\": 1610}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl288/fig-002.webp\", \"caption\": \"\", \"page\": 5, \"index\": 2, \"width\": 1380, \"height\": 1858}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl288/fig-003.webp\", \"caption\": \"\", \"page\": 12, \"index\": 3, \"width\": 2470, \"height\": 2517}]"
motivation: 仓库级文档制作成本高，且复杂代码库超出大模型上下文，现有自动化方法难以刻画架构结构。
method: 提出CodeWiki框架，结合自顶向下层次分解、分治式智能体系统与自底向上综合来生成整体文档。
result: 该框架覆盖七种主流编程语言，可在保留架构上下文的同时扩展到仓库级文档生成。
conclusion: 为LLM驱动的自动化软件文档生成建立了统一且可扩展的评估与方法框架。
---

## Abstract
Comprehensive software documentation is crucial yet costly to produce. Despite recent advances in large language models (LLMs), generating holistic, architecture-aware documentation at the repository level remains challenging due to complex and evolving codebases that exceed LLM context limits. Existing automated methods struggle to capture rich semantic dependencies and architectural structure. We present CodeWiki , a unified framework for automated repository-level documentation across seven mainstream programming languages. CodeWiki combines top-down hierarchical decomposition with a divide-and-conquer agent system to preserve architectural context and scale documentation generation, and a bottom-up synthesis that integrates textual descriptions with visual artifacts such as architecture and data-flow diagrams. We also introduce CodeWikiBench , a benchmark with hierarchical rubrics and LLM-based evaluation protocols. Experiments show that CodeWiki achieves a 68.79% quality score with proprietary models, outperforming the closed-source DeepWiki baseline by 4.73%, with especially strong gains on scripting languages. CodeWiki is released as open source to support future research.

---

## 论文详细总结（自动生成）

## 1. 核心问题与整体含义

- **研究动机**：软件文档对理解、维护和协作至关重要，但仓库级文档制作成本高、易过时；开发者大量时间用于程序理解。
- **核心问题**：现有 LLM 文档生成多集中在函数/文件级，难以处理超出上下文窗口的大型代码库，也难以刻画模块交互、数据流、架构模式等仓库级语义。
- **评估缺口**：传统 BLEU/ROUGE 等文本相似度指标难以评价仓库级文档的完整性、准确性和架构一致性；缺乏标准化 benchmark。
- **整体含义**：论文提出 **CodeWiki** 框架与 **CodeWikiBench** benchmark，试图把 LLM 文档生成从“组件级摘要”推进到“仓库级、架构感知、多语言、可扩展”的整体文档生成，并建立基于层次化 rubric 与 LLM judge 的评估体系。

## 2. 方法论

### 2.1 核心思想

- 采用 **自顶向下层次分解 + 分治式智能体 + 自底向上综合**：
  - 自顶向下：把大型仓库分解为可管理的模块树，保留架构上下文。
  - 分治式智能体：每个叶模块由专门 agent 生成文档，复杂时动态委派子模块。
  - 自底向上：父模块由子模块文档综合生成，最终形成仓库级概览，并整合架构图、数据流图等视觉工件。

### 2.2 关键技术细节

- **依赖图构建**：
  - 使用 Tree-Sitter 解析 AST，识别函数、方法、类、结构体、模块及依赖关系。
  - 将函数调用、继承、属性访问、模块导入统一为 `depends_on` 关系，形成有向图 \(G=(V,E)\)。
- **入口识别与模块分解**：
  - 通过拓扑排序识别零入度组件作为入口点（main、API、CLI、公共接口等）。
  - 递归划分高层组件，输入仅使用组件 ID/相对路径以控制上下文；分组考虑依赖关系和语义一致性，形成面向功能的模块树。
- **递归文档生成**：
  - 每个叶模块分配 agent，具备源码访问、完整模块树、文档工作区工具、依赖图遍历能力。
  - agent 分析组件、探索依赖、生成 Markdown 文档，包括描述、用法示例、API 说明和架构洞察。
  - **动态委派**：当模块复杂度超出单次处理能力时，agent 创建子模块并交给子 agent；委派依据包括代码复杂度、语义多样性和上下文窗口使用率。
  - **跨模块引用管理**：通过全局注册表记录已文档化组件，遇到外部组件时创建交叉引用而非重复内容。
- **层次化综合**：
  - 父模块由 LLM 基于子文档、模块树、依赖信息和综合指令生成。
  - 综合内容包括主题/模式分析、架构概览、功能摘要、使用指南、架构图和数据流图等。

### 2.3 CodeWikiBench 评估方法

- **层次化 rubric 生成**：
  - 从项目官方文档按目录结构和 Markdown 语法解析为结构化 JSON。
  - Rubric Generator Agent 生成与仓库功能结构对应的层次化 rubric。
  - 使用多个模型家族独立生成 rubric 后综合，降低单模型偏差。
- **文档评估**：
  - Judge Agents 接收生成文档的结构化 JSON 和仓库特定 rubric。
  - 仅评估**叶级具体需求**，做二值充分性判断并给出简要理由。
  - 多个不同模型家族的 judge 独立评估，叶节点分数取平均。
- **分数聚合与可靠性**：
  - 叶节点分数为多次评估均值，标准差衡量 judge 共识。
  - 内部节点按子节点权重加权平均；不确定度按权重平方进行传播。
  - 最终得到仓库级质量分数 \(S(R)\in[0,1]\) 及标准差 \(\sigma_R\)，同时提供质量与可靠性度量。

## 3. 实验设计

- **Benchmark**：CodeWikiBench，包含 7 个开源仓库，覆盖 7 种语言：
  - Python：OpenHands，约 229,909 LOC
  - JavaScript：svelte，约 124,576 LOC
  - TypeScript：puppeteer，约 136,302 LOC
  - C#：ml-agents，约 86,106 LOC
  - Java：logstash，约 117,485 LOC
  - C：wazuh，约 1,446,730 LOC
  - C++：electron，约 184,234 LOC
- **评估场景**：仓库级文档生成，评价整体质量与 leaf-level rubric 覆盖率。
- **对比方法**：
  - 开源基线：OpenDeepWiki、deepwiki-open。
  - 闭源基线：DeepWiki。
  - 未直接定量比较 RepoAgent、DocAgent 等函数级系统，作者解释其输出范式不同（N 个组件文档 vs 层次化模块文档）。
- **生成与评估模型配置**：
  - 文档生成：Claude Sonnet 4，temperature 0.0，max tokens 16,384，上下文 200K。
  - Rubric 生成：Claude Sonnet 4、Gemini 2.5 Pro、Kimi K2 Instruct。
  - Judge：Gemini 2.5 Flash、GPT OSS 120B、Kimi K2 Instruct，二值评分。
  - 模块分解阈值：每个叶模块 32,768 tokens；最大委派深度 3 层。
- **防数据泄漏**：使用 2025 年 8–9 月的仓库快照，晚于所用模型知识截止时间（如 Claude Sonnet 4 为 2025 年 3 月）。

## 4. 资源与算力

- 论文**未明确报告** GPU 型号、数量、训练时长或总推理成本。
- 该工作主要是基于现有 LLM 的推理/agent pipeline，而非模型训练；但文中也未报告 API 调用量、总 token 消耗、运行时间或经济成本。
- 仅提供了模型配置、上下文窗口、最大 token 数、委派深度等实现参数，无法据此准确估算算力开销。

## 5. 实验数量与充分性

- **主实验规模**：7 个仓库 × 4 个系统（CodeWiki + 3 个基线）≈ 28 组文档生成与评估结果。
- **分析维度**：
  - RQ1：整体质量与覆盖率。
  - RQ2：按脚本语言、托管语言、系统编程语言分组比较。
  - RQ3：跨 86K–1.4M LOC 的规模分析、评估可靠性分析。
  - Rubric 可靠性：7 个仓库上的语义与结构一致性统计。
  - 人类评估 pilot：3 名参与者 × 3 个仓库 = 9 次偏好判断。
- **充分性评价**：
  - 覆盖多语言和多规模仓库，具有一定广度；使用多模型 rubric 生成与多 judge 共识，评估设计较谨慎。
  - 但**缺少消融实验**：未单独量化层次分解、动态委派、跨模块引用、视觉工件、自底向上综合等组件的贡献。
  - 每种语言基本只有一个仓库，统计功效有限；7 个仓库不足以代表全部软件领域。
  - 未系统比较不同生成模型对 CodeWiki 的影响，生成端仅用 Claude Sonnet 4。
- **公平性评价**：
  - 统一 rubric、多 judge、多模型 rubric 生成和时间分离增强了公平性。
  - 但闭源 DeepWiki 的内部配置不可控；开源基线调用参数未充分披露；LLM judge 仍可能带来模型家族偏差；自动 rubric 未经过全面人工校验。
  - 人类评估规模很小，只能作为初步验证。

## 6. 主要结论与发现

- CodeWiki 平均质量分 **68.79%**，高于 DeepWiki 的 **64.06%**，提升 **4.73 个百分点**；相对 OpenDeepWiki 和 deepwiki-open 分别提升约 **21.66%** 和 **18.74%**。
- 在 7 个仓库中，CodeWiki 在 **5/7** 上优于所有基线；TypeScript（puppeteer）提升最大，达 **+18.54%**，Python（OpenHands）**+9.41%**，JavaScript（svelte）**+3.45%**。
- 语言差异明显：
  - 脚本语言平均 **79.14%**，比 DeepWiki 的 **68.67%** 高 **10.47%**。
  - 托管语言（C#、Java）平均 **68.84%**，高于 DeepWiki 的 **64.80%**。
  - 系统编程语言（C、C++）CodeWiki 平均 **53.24%**，低于 DeepWiki 的 **56.39%**，说明指针、手动内存管理、模板元编程等仍是难点。
- 性能差异主要与语言特性相关，而非仓库规模；层次分解可处理 86K–1.4M LOC 的仓库。
- Rubric 可靠性：语义一致性 **73.65%**，结构一致性 **70.84%**；评估标准差约 **3.84%**，与 DeepWiki 的 **3.60%** 接近。
- 人类 pilot 中 CodeWiki 在 **7/9** 次判断中被偏好，与自动评估方向初步一致。

## 7. 优点

- **方法创新性**：将自顶向下分解、递归 agent、动态委派和自底向上综合结合，针对仓库级文档的上下文限制提出较完整的工程化方案。
- **架构感知**：不仅生成文本，还整合架构图、数据流图、跨模块引用，贴近真实仓库文档需求。
- **多语言覆盖**：覆盖 Python、Java、JavaScript、TypeScript、C、C++、C#，较多数仅关注 Python 的工作更广。
- **Benchmark 设计有特色**：基于官方文档生成层次化 rubric，仅评叶级具体需求，并用多模型 judge 和标准差传播提供可靠性度量。
- **评估控制较谨慎**：多模型 rubric 生成、多 judge 共识、时间分离防泄漏、公开开源代码与 benchmark。
- **结果呈现较完整**：同时报告质量分、覆盖率、标准差、语言分组和规模分析，并附小规模人类验证。

## 8. 不足与局限

- **系统语言表现不足**：C/C++ 上低于 DeepWiki，说明当前解析与架构抽象对底层语言结构利用不足。
- **实验覆盖有限**：仅 7 个仓库，每种语言约一个项目，领域和项目类型覆盖有限；结论外推需谨慎。
- **缺少消融实验**：无法判断各模块（层次分解、动态委派、视觉工件、跨模块引用、自底向上综合）的具体贡献。
- **评估偏差风险**：依赖 LLM-as-a-Judge，多模型共识不能完全消除模型偏好；自动生成 rubric 未经过全面人工验证，部分 rubric 可能难解释。
- **人类评估规模小**：仅 3 名参与者、3 个仓库、9 次偏好判断，统计意义有限。
- **基线比较受限**：未与函数级系统定量比较；闭源 DeepWiki 不可复现，开源基线配置披露不足。
- **生成模型单一**：文档生成仅使用 Claude Sonnet 4，未评估不同生成模型下的鲁棒性。
- **资源与成本未报告**：缺少 GPU/算力、token 消耗、运行时间和经济成本，影响可复现性与实际部署评估。
- **版本演化未覆盖**：当前为固定快照文档生成，尚未实现与代码演进同步的版本感知文档。

（完）
