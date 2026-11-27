---
title: "AutoUE: Automated Generation of 3D Games in Unreal Engine via Multi-Agent Systems"
title_zh: AutoUE：基于多智能体系统在虚幻引擎中自动生成 3D 游戏
authors: "Lei Yin, Wentao Cheng, Zhida Qin, Tianyu Huang, Yidong Li, Gangyi Ding"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://aclanthology.org/2026.findings-acl.111.pdf"
tags: ["query:ai-se"]
score: 7.0
evidence: 包含代码合成与自动化测试的多智能体系统
tldr: 在商业游戏引擎中自动生成 3D 游戏涉及场景、蓝图与代码等复杂工作流。本文提出多智能体系统 AutoUE，协调多个智能体端到端完成模型检索、场景生成、玩法与交互代码合成以及自动化游戏测试，并引入检索增强生成以缓解工具使用幻觉。实验表明该系统能生成可运行的完整 3D 游戏，展示了多智能体在代码合成与测试上的协同潜力。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl111/fig-001.webp\", \"caption\": \"\", \"page\": 1, \"index\": 1, \"width\": 598, \"height\": 344}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl111/fig-002.webp\", \"caption\": \"\", \"page\": 1, \"index\": 2, \"width\": 597, \"height\": 345}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl111/fig-003.webp\", \"caption\": \"\", \"page\": 1, \"index\": 3, \"width\": 597, \"height\": 345}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl111/fig-004.webp\", \"caption\": \"\", \"page\": 3, \"index\": 4, \"width\": 465, \"height\": 261}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl111/fig-005.webp\", \"caption\": \"\", \"page\": 6, \"index\": 5, \"width\": 1852, \"height\": 854}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl111/fig-006.webp\", \"caption\": \"\", \"page\": 11, \"index\": 6, \"width\": 1674, \"height\": 2030}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl111/fig-007.webp\", \"caption\": \"\", \"page\": 12, \"index\": 7, \"width\": 1674, \"height\": 2411}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl111/fig-008.webp\", \"caption\": \"\", \"page\": 13, \"index\": 8, \"width\": 1674, \"height\": 3412}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl111/fig-009.webp\", \"caption\": \"\", \"page\": 14, \"index\": 9, \"width\": 1901, \"height\": 602}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl111/fig-010.webp\", \"caption\": \"\", \"page\": 14, \"index\": 10, \"width\": 1900, \"height\": 2148}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl111/fig-011.webp\", \"caption\": \"\", \"page\": 15, \"index\": 11, \"width\": 4190, \"height\": 7936}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl111/fig-012.webp\", \"caption\": \"\", \"page\": 16, \"index\": 12, \"width\": 4180, \"height\": 7658}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl111/fig-013.webp\", \"caption\": \"\", \"page\": 17, \"index\": 13, \"width\": 1914, \"height\": 3021}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl111/fig-014.webp\", \"caption\": \"\", \"page\": 18, \"index\": 14, \"width\": 1901, \"height\": 3603}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl111/fig-015.webp\", \"caption\": \"\", \"page\": 19, \"index\": 15, \"width\": 1907, \"height\": 2660}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl111/fig-016.webp\", \"caption\": \"\", \"page\": 20, \"index\": 16, \"width\": 2461, \"height\": 5306}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl111/fig-017.webp\", \"caption\": \"\", \"page\": 21, \"index\": 17, \"width\": 1905, \"height\": 2145}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl111/fig-018.webp\", \"caption\": \"\", \"page\": 22, \"index\": 18, \"width\": 1901, \"height\": 2341}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl111/fig-019.webp\", \"caption\": \"\", \"page\": 23, \"index\": 19, \"width\": 4180, \"height\": 5395}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl111/fig-020.webp\", \"caption\": \"\", \"page\": 24, \"index\": 20, \"width\": 4189, \"height\": 5321}]"
motivation: 商业引擎中自动生成 3D 游戏流程复杂，且 LLM 易出现工具使用幻觉。
method: 提出多智能体系统，分工完成资产检索、场景生成、代码合成与自动化测试，并用检索增强约束工具调用。
result: 系统可端到端生成可运行的 3D 游戏，并自动完成测试评估。
conclusion: 多智能体协同加检索增强能有效支撑复杂引擎工作流下的代码生成与测试。
---

## Abstract
Automatically generating 3D games in commercial game engines remains a non-trivial challenge, as it involves complex engine-related workflows for generating assets such as scenes, blueprints, and code. To address this challenge, we propose a novel multi-agent system, AutoUE, which coordinates multiple agents to end-to-end generate 3D games, covering model retrieval, scene generation, gameplay and interaction code synthesis, and automated game testing for evaluation. In order to mitigate tool-use hallucinations in LLMs, we introduce a retrieval-augmented generation mechanism that grounds agents with relevant UE tool documentation. Additionally, we incorporate game design patterns and engine constraints into the code generation process to ensure the generation of correct and robust code. Furthermore, we design an automated play-testing pipeline that generates and executes runtime test commands, enabling systematic evaluation of dynamic behaviors. Finally, we construct a game generation dataset and conduct a series of experiments that demonstrate AutoUE’s ability to generate 3D games end-to-end, and validate the effectiveness of these designs.

---

## 论文详细总结（自动生成）

# AutoUE 论文中文结构化总结

## 1. 核心问题与研究背景

- **研究对象**：在商业游戏引擎（本文聚焦 Unreal Engine 5）中，由自然语言描述端到端自动生成完整、可玩的 3D 游戏。
- **核心痛点**：
  - 3D 游戏生成涉及场景布局、玩法逻辑、蓝图/代码、交互对象等多个子系统，且引擎工作流高度耦合，远难于 2D 或纯文本游戏。
  - 已有工作多只覆盖**孤立环节**：如仅生成 3D 场景（SceneX、UnrealLLM、3D-GPT）、仅生成引擎代码（UniGen、Hassan 2025），组件之间难以直接组合成完整游戏。
  - LLM 在调用引擎工具时存在**工具使用幻觉**（节点参数、引脚连接、API 用法编造）。
  - 生成代码缺乏游戏开发设计模式约束，导致不可维护、不可扩展、甚至无法编译。
  - 既有评估多依赖人工检查或静态检查，而游戏的核心价值在于**动态可玩性**，缺少自动化、客观的运行时评估手段。
- **整体含义**：论文试图把"场景生成 + 玩法代码生成 + 交互实现 + 自动化试玩评估"整合为一条可复用的多智能体流水线，为引擎内 3D 游戏自动生成建立基准与基础设施。

## 2. 方法论

### 2.1 核心思想
- 构建 **5 个 LLM 智能体**协同工作：模型检索智能体、场景生成智能体、玩法代码智能体、交互对象智能体、自动化试玩智能体。
- 智能体之间通过**结构化规格（structured specifications）**传递上下文，保证跨阶段一致性。
- 以 **MCP（Model Context Protocol）** 作为智能体与 UE 之间的标准化接口，负责把结构化输出导入工程并触发引擎工作流（论文将其定位为工程集成层，未展开细节）。

### 2.2 问题形式化
- 输入游戏描述 `x` 常把"场景内容"与"玩法意图"混在一起，故先用提示词 `Decompose` 拆分为：
  - `DescS`：场景上下文与关键物体；
  - `DescG`：玩法机制与玩家交互。

### 2.3 模型检索智能体
- `GenerateObj(DescS)` → `List[AttrsObj]`，每个物体属性含：名称、类别、描述、空间摆放指引。
- 资产库基于 **TexVerse**（Sketchfab 来源，858K 带文本描述的 3D 模型）。
- 流程：
  1. 用文本编码器为全部模型描述建立向量库；
  2. 按 Sketchfab 的 **18 个类别**做预过滤，缩小候选集；
  3. 计算物体描述与候选模型描述的**余弦相似度**，降序取 Top-k；
  4. 由 LLM 结合 `AttrsObj` 对 Top-k 重排序，取 **Top-1** 作为该物体的 3D 资产。

### 2.4 场景生成智能体（基于 UE PCG）
- 不直接生成硬编码坐标，而是生成 **PCG（Procedural Content Generation）节点图**，天然可视化、可编辑。
- **节点链规划**：`PlanNode(DescS, AttrsObj)` → 每个物体一条有序节点链 `List[Node(x,y)]`，节点带编辑器坐标。
- **两类规范模式（关键设计）**：
  - **大型物体模式**（建筑等）：需稳定采样与间距，链尾为"剪枝 + 边界控制 + 直接生成"，避免重叠与越界；
  - **小型散布物体模式**（树木、岩石）：加入**排除节点**减去禁止区域，避免与主要 Actor 相交。
- **RAG 节点规格化**：规划只给出"有哪些节点"，缺少参数与引脚连接。将工具文档切分为统一文本块，对每个目标节点做语义检索取 Top-c 块，再由 `GenerateNode` 输出参数与连接 `AttrsNode`。
- 最后通过 MCP 工具把 `AttrsNode` 写入 UE PCG 编辑器；新增节点能力只需补充文档，扩展性好。

### 2.5 玩法代码智能体
- `PlanCode(DescG)` → `List[AttrsM]`，模块属性含设计目的、用途、依赖模块。
- 按模块依赖做**拓扑排序**，逐个生成 C++：`GenerateCode(DescG, List[AttrsM], DepsMi)`。
- 提示中注入**代码模板**与**引擎约束**：导出/注册宏、include 白名单、日志、跨模块访问规范等。
- 设计通用**模块管理框架**（经 MCP 暴露），使玩法模块可被交互对象以受控方式调用，保证可复用、可组合、可扩展。

### 2.6 交互对象智能体
- `PlanInt(List[AttrsObj], List[CodeM])` → `AttrsInt`：交互描述、模块依赖、交互流程、是否需要调用战斗/导航等外部插件系统。
- `GenerateInt(AttrsInt, List[CodeM])` 生成交互对象的 C++ 实现，把玩法模块方法按推断出的顺序串起来（拾取、对话等）。

### 2.7 自动化试玩智能体
- `GenerateTest(DescS, DescG, List[CodeM], List[CodeInt])` → `List[Cmd]`。
- 测试命令两类：**移动到目标物体**、**执行特定交互**；通过 MCP 在 UE 运行时自动执行。
- 收集运行时截图、执行日志、PCG 节点链、玩法/交互代码及中间规格，作为最终评估依据。

## 3. 实验设计

### 3.1 数据集 / Benchmark
- 自建 **PlayGen-20**：20 个游戏生成任务，覆盖拾取、开启、对话、检视、战斗等常见交互。
- 按场景复杂度与交互复杂度分三档：
  - **Easy（5 个）**：单一或低复杂度交互、反馈清晰、失败代价低，用于测端到端可玩性与基础交互正确性；
  - **Medium（7 个）**：多交互对象、偏探索与收集，测多交互组织与场景内容丰富度；
  - **Hard（8 个）**：显式进度约束与强交互依赖、状态转换更紧耦合，测复杂流程下的鲁棒性与代码可靠性。
- 引擎：Unreal Engine 5；默认骨干 LLM 为 **Qwen-Plus**（生成与评估均用）；Q2 场景美学评估改用 **GPT-4o** 以对齐基线设置。

### 3.2 四组研究问题与对应实验
- **Q1 整体质量**：LLM-as-judge 从 Scene、Gameplay、Visual 三维度各 1–10 打分，加权 0.35/0.35/0.30 得 Game 总分（评估提示见附录 Fig.16）。
- **Q2 场景美学**：与 7 个基线比较 **GAS（GPT Aesthetic Score）**：
  - 生成式基线：DreamFusion（4.83）、Magic3D（6.39）、WonderJourney/WonderJ（7.38）；
  - 过程式基线：Infinigen（6.61）、3D-GPT（6.76）、SceneX（7.31）、UnrealLLM（7.71）；
  - AutoUE：**7.8**。
- **Q3 PCG 图消融**：3 个变体 × 4 个指标：
  - 变体：`W/o patterns`（去掉两类节点链模式，自由构图）、`W/o params`（文档语料删除节点参数内容）、`W/o conns`（删除引脚连接内容）；
  - 指标：SNode（节点创建成功率）、SParam（参数填充成功率）、SPin（引脚连接成功率）、SPCG（LLM 评判的 PCG 图质量 1–10）。
- **Q4 玩法代码消融**：3 个变体 × 4 个指标：
  - 变体：`W/o dependencies`（去掉模块依赖知识）、`W/o code templates`（去掉代码模板）、`W/o engine constraints`（去掉引擎约束）；
  - 指标：MAS（模块规划质量）、MCS（模块代码质量）、IIS（交互集成质量）、GCS = 0.3·MAS + 0.3·MCS + 0.4·IIS；**编译失败则 MCS、IIS 记 0**。

### 3.3 主要数值结果
- **Q1**：Easy 10.0/8.30/7.70 → 8.72；Medium 9.79/8.29/8.14 → 8.74；Hard 9.94/8.19/7.50 → 8.59；总体 9.90/8.25/7.78 → **8.68**。
- **Q3**：AutoUE 在全部难度上 SNode/SParam/SPin 均 **100%**，SPCG **8.42**；`W/o patterns` 降至 79.6/99.6/64.0、4.77；`W/o params` 为 100/55.2/99.9、4.63；`W/o conns` 为 100/100/80.4、5.02。
- **Q4**：三个变体**全部编译失败**，MCS=IIS=0，GCS 仅 2.44–2.51；AutoUE 为 MAS 8.05、MCS 7.55、IIS 6.74、GCS **7.38**。

## 4. 资源与算力

- 论文**未报告任何训练算力信息**：没有 GPU 型号、数量、训练时长、显存或调用成本等细节。
- 从方法看，系统本身**不涉及模型训练**，全部依赖现成 LLM 的 API 调用（Qwen-Plus 作生成与评估骨干，Q2 评估用 GPT-4o），因此算力主要体现在推理调用与 UE5 运行时执行上。
- 资产侧仅说明使用 TexVerse 的 858K 模型与公开工具文档构建向量库，未说明索引构建开销。
- **评价**：这一点属于可复现性上的信息缺口，读者无法估算系统的实际部署成本与延迟。

## 5. 实验数量与充分性

- **实验组数**：
  - 1 个自建数据集（20 任务，3 个难度档）；
  - Q1：1 组整体评估（4 行结果，按难度分层）；
  - Q2：1 组对比，7 个外部基线 + 本方法；
  - Q3：1 组消融，3 变体 × 3 难度 + 总体；
  - Q4：1 组消融，3 变体 × 3 难度 + 总体；
  - 共 4 张结果表，覆盖 4 个研究问题，另附大量提示词附录（Fig.7–18）与 20 个任务的描述与截图（Fig.4–6）。
- **充分性判断**：
  - **优点**：四个研究问题与四张表一一对应，消融设计与主张（模式先验、RAG 参数/连接、依赖/模板/约束）匹配度高；消融指标针对性强（结构、参数、连线分开度量）。
  - **不足**：
    - 数据集仅 20 个任务、且为预定义描述，规模与多样性有限，未覆盖真实项目的长流程与开放需求；
    - **全部评估均为 LLM-as-judge**，无人类评分、无用户研究、无玩家可玩性测试；
    - 未报告多次运行的方差、置信区间或显著性检验，单次结果难以判断稳定性；
    - Q4 的消融过于"全或无"——三个变体全部编译失败，导致 MCS/IIS 直接归零，虽然结论明确，但无法反映各因素的部分贡献差异；
    - 缺少失败案例分析（哪些任务失败、失败原因分布）；
    - 未与 Dream

Fusion、Magic3D 等生成式基线在完整游戏生成任务上做端到端对比，仅在场景美学维度比较 GAS，因此 Q2 的结论更接近“场景观感不落后”，而非“端到端游戏生成优于生成式 3D 方案”。
    - 未报告跨骨干模型的泛化实验（如更换 GPT-4o、Claude 等作为生成骨干），结论对 Qwen-Plus 的依赖程度未知；
    - 未报告资产检索、PCG 生成、代码生成、自动试玩各阶段的耗时与失败率分解，难以定位系统瓶颈；
    - 自动试玩智能体生成的测试命令覆盖面有限（主要为移动与交互），对战斗、长流程状态机等复杂玩法的验证能力尚未充分证明。

## 6. 与相关工作的定位

- **相对 3D 场景生成工作**（SceneX、3D-GPT、UnrealLLM、Infinigen 等）：AutoUE 不止生成场景，还把场景作为玩法与交互的承载环境，强调“场景—玩法—交互”跨阶段一致性；其 PCG 节点图路线使场景在引擎内可编辑、可复用，而非仅输出静态资产或硬编码布局。
- **相对引擎代码生成工作**（UniGen、Hassan 2025 等）：AutoUE 引入模块规划、依赖拓扑排序、代码模板与引擎约束，并用模块管理框架把玩法代码封装为可被交互对象调用的受控接口，试图解决“能生成代码但难以组合成游戏”的问题。
- **相对 LLM 智能体/工具使用方法**：以 MCP 作为智能体与 UE 的标准化集成层，配合 RAG 缓解工具使用幻觉；这一思路对其它商业软件（如 Unity、Blender）的自动化流水线具有可迁移性。
- **相对游戏自动测试/试玩工作**：将 LLM 生成的测试命令接入引擎运行时，形成“生成—执行—截图/日志—评估”的闭环，是把动态可玩性纳入自动评估的尝试，但测试策略仍较浅。

## 7. 主要贡献（按论文主张归纳）

1. **端到端多智能体流水线**：将模型检索、PCG 场景生成、玩法代码生成、交互对象生成与自动试玩整合为统一框架，并以结构化规格串联各阶段，缓解跨阶段语义漂移。
2. **面向引擎的 PCG 节点图生成方法**：用“节点链规划 + 两类规范模式 + RAG 节点规格化”生成可编辑的 PCG 图，把 LLM 的自由生成约束在引擎可执行的结构内；新增节点只需补充文档，具备扩展性。
3. **受约束的玩法代码与交互集成机制**：通过模块规划、依赖排序、代码模板、引擎约束和模块管理框架，提高代码可编译性、可组合性与可维护性。
4. **自动化试玩与运行时评估闭环**：以 MCP 在 UE 运行时执行测试命令，收集截图、日志与中间产物，为 3D 游戏生成提供动态评估手段。
5. **PlayGen-20 基准与多维评估协议**：构建 20 个分难度任务，并给出 Scene/Gameplay/Visual 加权评分、GAS、PCG 图指标与代码质量指标，为后续工作提供可比较的评测框架。

## 8. 局限与风险

- **基准规模小且预定义**：20 个任务难以代表真实游戏开发的开放性与长尾需求；任务描述与评估提示可能对方法存在适配偏差。
- **评估主观性强**：核心指标依赖 LLM-as-judge，缺少人类专家评分与玩家可玩性研究；LLM 评审可能偏好特定表述或与生成骨干同源，带来偏差。
- **动态可玩性验证不足**：自动试玩以简单命令为主，未覆盖复杂战斗、解谜、多分支叙事与长时序状态；截图与日志也难以完全证明“游戏可玩”。
- **工程集成细节披露有限**：MCP 工具实现、模块管理框架、UE 版本兼容性、资产导入与碰撞/导航配置等关键工程细节未充分展开，复现门槛较高。
- **成本与延迟未知**：未报告 API 调用量、 token 成本、各阶段耗时与失败重试开销，难以评估实际部署可行性。
- **统计严谨性不足**：缺少多次运行方差、置信区间与显著性检验；消融实验的“全或无”编译失败设计限制了对因素部分贡献的刻画。
- **安全与版权风险**：使用 Sketchfab/TexVerse 资产与自动生成代码，涉及资产许可、生成代码安全审查与引擎项目污染等问题，论文未讨论。

## 9. 启示与可拓展方向

- **从“生成即结束”转向“生成—试玩—修复”闭环**：可将自动试玩失败信号回传至代码/场景智能体，形成迭代修复，而不仅是单次生成后评估。
- **增强结构化规格**：为场景、玩法、交互定义更形式化的契约（如状态机、前置条件、后置条件），有助于跨智能体一致性与自动验证。
- **引入混合评估**：LLM 评审 + 人类评分 + 运行时覆盖率/任务完成率 + 编译与静态检查，多信号交叉验证可玩性。
- **扩展基准与骨干泛化**：增加任务数量、开放描述、多引擎与多 LLM 骨干实验，并报告方差与成本。
- **工程化重点**：资产许可过滤、碰撞/导航自动配置、版本兼容与回滚机制，是把原型系统推向可用的关键。

## 10. 总体评价

AutoUE 的价值主要在于**系统整合与工程约束**：它没有提出全新的生成模型，而是把多个 LLM 智能体、RAG、PCG 节点图、代码模板、模块管理框架与 MCP 运行时接口组织成一条面向 UE5 的端到端流水线，并用 PlayGen-20 与四组实验验证了“结构化约束能显著提升引擎内可执行性”这一核心主张。实验结果显示，其在场景美学上接近或略优于过程式基线，在 PCG 图生成与玩法代码可编译性上优势明显；但受限于小规模基准、纯 LLM 评审、浅层自动试玩与缺失的成本/方差报告，论文更适合被视为**方向性验证与基础设施雏形**，而非已充分证明的通用 3D 游戏自动生成方案。后续工作若能在更大基准、人类评估、迭代修复闭环与工程复现细节上补强，其框架思路具有较好的研究与应用潜力。

（完）
