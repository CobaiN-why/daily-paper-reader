---
title: "CodeScout: Contextual Problem Statement Enhancement for Software Agents"
title_zh: CodeScout：面向软件智能体的上下文问题描述增强
authors: "Manan Suri, Xiangci Li, Mehdi Shojaie, Songyang Han, Chao-Chun Hsu, Shweta Garg, Aniket Anand Deshmukh, Varun Kumar"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://aclanthology.org/2026.findings-acl.2032.pdf"
tags: ["query:ai-se"]
score: 8.0
evidence: 面向软件智能体的问题描述上下文增强
tldr: AI代码助手常因问题描述含糊、缺少任务上下文而失败，软件智能体在此类请求上易过度探索或反复尝试同一修复。作者提出CodeScout，通过对目标代码库进行轻量预探索，将模糊用户请求系统性地转化为完整可执行的问题描述。分析表明智能体失败与过长轨迹高度相关，而该方法可缩短轨迹并改善结果。工作为提升自主编码智能体的任务理解与执行效率提供了实用方案。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl2032/fig-001.webp\", \"caption\": \"\", \"page\": 7, \"index\": 1, \"width\": 792, \"height\": 327}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl2032/fig-002.webp\", \"caption\": \"\", \"page\": 7, \"index\": 2, \"width\": 1431, \"height\": 355}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl2032/fig-003.webp\", \"caption\": \"\", \"page\": 7, \"index\": 3, \"width\": 1433, \"height\": 355}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl2032/fig-004.webp\", \"caption\": \"\", \"page\": 8, \"index\": 4, \"width\": 1341, \"height\": 446}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl2032/fig-005.webp\", \"caption\": \"\", \"page\": 8, \"index\": 5, \"width\": 2678, \"height\": 1773}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl2032/fig-006.webp\", \"caption\": \"\", \"page\": 9, \"index\": 6, \"width\": 1071, \"height\": 713}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl2032/fig-007.webp\", \"caption\": \"\", \"page\": 9, \"index\": 7, \"width\": 1071, \"height\": 713}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl2032/fig-008.webp\", \"caption\": \"\", \"page\": 9, \"index\": 8, \"width\": 1071, \"height\": 713}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl2032/fig-009.webp\", \"caption\": \"\", \"page\": 9, \"index\": 9, \"width\": 2438, \"height\": 1592}]"
motivation: AI代码助手面对含糊问题描述时易过度探索或重复无效修复，导致任务失败。
method: 提出CodeScout，通过轻量预探索目标代码库，将模糊请求转化为完整可执行的问题描述。
result: 该方法有效缩短智能体执行轨迹并提升在软件开发任务上的成功率。
conclusion: 表明问题描述上下文化是提升自主编码智能体表现的关键手段。
---

## Abstract
Current AI-powered code assistance tools often struggle with ambiguous problem statements that lack sufficient task context and requirements specification. Recent analysis of software engineering agents reveals that failures on such ambiguous requests are highly correlated with longer trajectories involving either over-exploration or repeated attempts at applying the same fix without proper evolution or testing, leading to suboptimal outcomes across software development tasks. We introduce CodeScout, a breakthrough contextual query refinement approach that systematically converts ambiguous user requests into comprehensive, actionable problem statements through lightweight pre-exploration of the target codebase. Our key innovation is demonstrating that structured analysis before task execution can supplement existing agentic capabilities without requiring any modifications to their underlying scaffolds. CodeScout performs targeted context scoping, conducts multi-perspective analysis examining potential fixes and exploration opportunities, then synthesizes these insights into enhanced problem statements with reproduction steps, expected behaviors, and targeted exploration hints. This pre-exploration directly addresses the identified failure patterns by reducing non-converging agent trajectories while clarifying user intent in natural language space. We evaluate CodeScout using state-of-the-art agentic scaffolds and language models on SWEBench-Verified, demonstrating a 20% improvement in resolution rates with up to 27 additional issues resolved compared to the default baseline method. Our results suggest that systematic query refinement through contextual analysis represents a promising direction for enhancing AI code assistance capabilities.

---

## 论文详细总结（自动生成）

# CodeScout 论文结构化总结

## 1. 核心问题与研究动机

- **背景**：LLM 驱动的代码助手与软件工程智能体（SWE agents）已广泛用于软件开发，但其失败往往并非源于模型推理能力不足，而是源于**输入的问题描述本身质量低**——开发者常给出简短、依赖上下文、省略复现步骤与技术细节的请求。
- **实证依据**：
  - Meng et al. (2024)：可解决的 bug 报告描述质量分数显著高于不可解决报告，相对差异达 110%–2700%。
  - Nam et al. (2025)：Google LLM 开发工具中被拒绝的代码建议与低质量用户输入强相关。
  - Bouzenia & Pradel (2025)：agent 失败表现为两类行为模式——**过度探索**（上下文过载导致找不到根因）与**重复应用同一修复**（缺乏测试与演进）。
- **核心论点**：输入质量而非模型容量是 AI 辅助软件工程的关键瓶颈。现有 agent 采用 reason-execute-observe 逐步循环，边规划边执行，缺乏长程战略理解，只能被动反应式探索，累积偏离真实问题范围。
- **论文目标**：在**不修改下游 agent scaffold** 的前提下，通过执行前的结构化预探索，把模糊请求转化为完整、可执行的问题描述。

## 2. 方法论：CodeScout

### 核心思想
将问题描述增强建模为预处理变换：给定原始问题 $P_0$、仓库 $R$、下游 agent $A$，学习变换 $T$ 生成增强描述 $P_{aug}=T(P_0,R,S)$，使得 $M(A(P_{aug},R)) \ge M(A(P_0,R))$，其中 $S$ 为从仓库提取的结构化上下文知识。

### 三阶段流水线（对应算法 1）

1. **仓库知识图谱构建**：用 AST visitor 遍历语法树，构建有向图 $G(R)=(V,E)$，顶点为代码实体（名称、类型、位置、元数据），边为语义关系（类继承、函数签名与参数、导入依赖、变量声明与作用域）。
2. **高层上下文范围界定（High Level Scoping）**：LLM 结合 $P_0$ 与 $G(R)$ 生成探索目标集合 $T=\text{LLM}_{scope}(P_0,G(R))$，依据直接实体提及、常见调试模式、结构关系、命名约定判断相关性；约束 $|T|\le 15$，每个目标含实体类型、名称与推理理由。
3. **细粒度上下文分析**：对每个目标 $t_i$ 从 $R$ 检索代码 $c_i$，LLM 产出结构化分析 $i_i=\text{LLM}_{analyze}(P_0,c_i,t_i)$，包含四类信息：角色评估、修复位置提示（带置信度）、技术洞察、替代假设；同时打相关性分数，按阈值 $\tau_{rel}$ 过滤得到 $I_{filtered}$。
4. **问题综合（Problem Synthesis）**：LLM 将 $P_0$ 与 $I_{filtered}$ 合成为 $P_{aug}$，输出结构化章节：增强问题描述、复现步骤、期望行为、探索提示（待查文件/类函数/关注区域）、修复提示（高置信位置、实现建议及局限、替代假设），并保持生成内容与源码分析的可追溯性。

### 关键设计细节
- **计算复杂度**：每条问题需 $2+|T_{valid}|$ 次 LLM 调用（1 次目标识别 + 每目标 1 次分析 + 1 次综合），实践中约 7 个有效目标、约 9 次 API 调用。
- **鲁棒性**：检索失败时跳过该目标而非中止流水线。
- **即插即用**：增强阶段与下游 agent 架构解耦，无需修改 scaffold。

## 3. 实验设计

- **Benchmark**：SWEBench-Verified（真实 GitHub issue 解决任务）。
- **Scaffold（3 个）**：SWE-agent、OpenHands、Mini-SWE-Agent。
- **运行时 LLM（3 个）**：GPT-5-mini、DeepSeek R1（开启推理）、Qwen3-Coder 480B，覆盖闭源/开源、不同推理与编码特性、不同成本区间。
- **配置约束**：SWE-agent 每模型成本上限分别为 1.0 / 1.0 / 0.75 USD；OpenHands 最多 80 步；其余为默认设置。
- **对比方法**：
  - Default（无增强基线）
  - CodeScout（完整流水线）
  - Agentic Intra-trajectory Augmentation（改系统提示让 agent 在轨迹中自我增强）
  - CodeScout（No Filtering，去掉相关性过滤）
  - CodeScout（BM25 Entity Selection，用 BM25 替代 LLM scoping）
- **评估维度**：解决率、文件级/函数级定位准确率、token 消耗、美元成本、端到端运行时间、问题陈述长度分布、工具调用轨迹演化。
- **Cross-synthesis 实验**：增强模型与运行时模型交叉组合（3×3 矩阵）。

## 4. 资源与算力

- **未明确说明 GPU 型号、数量或训练时长**：本方法为推理期预处理增强，**不涉及模型训练**，因此无训练算力报告。
- 文中给出的相关开销信息：
  - **API 成本上限**：SWE-agent 下三个模型分别为 1.0 / 1.0 / 0.75 USD/实例。
  - **增强运行时间**：GPT-5-mini 平均 6.6 分钟、Qwen3-Coder 7.8 分钟、DeepSeek-R1 4.6 分钟，差异源于模型冗长度、探索目标数量与推理速度。
  - **调用开销**：每条约 9 次 LLM 调用。
- 伦理声明中提及计算资源带来能耗与环境影响，但无具体量化。

## 5. 实验数量与充分性

- **规模概览**：
  - 主实验：3 scaffold × 3 LLM 共 9 组 default vs. CodeScout 对比（含 Figure 3 汇总）。
  - 消融实验：SWE-agent 上 5 种设置 × 3 模型（Table 1）。
  - Cross-synthesis：3 运行时模型 × 3 增强模型组合（Table 2）。
  - 定位分析：文件级与函数级两类粒度。
  - 成本/Token 分析、问题陈述长度分布分析、工具调用轨迹分析。
  - 附录：5 个代表性实例 × 3 模型的完整流水线可视化、相关性分数分布/最大分数/目标数量分布、目标覆盖 Venn 图、Bland-Altman 一致性分析、分数一致性热力图。
- **充分性评价**：
  - **优点**：消融设计针对性强（分别验证“是否需要过滤”“LLM scoping vs BM25”“能否自我增强”）；cross-synthesis 揭示了非对称增益这一有实践价值的现象；定性示例丰富，可解释性好。
  - **客观性/公平性**：统一默认配置与明确成本/步数上限，对比条件基本一致；但主实验以“解决数”为主，统计显著性检验与多次运行方差未见报告，存在单次运行波动的隐忧。

## 6. 主要结论与发现

- **整体提升**：SWE-agent 子集上，完整流水线相对 Default 分别新增解决 {+11, +15, +24} 个 issue（DeepSeek R1 / GPT-5-mini / Qwen3-Coder），相对提升约 {9.6%, 7.7%, 13.1%}；摘要层面报告最高 20% 解决率提升、最多 27 个额外解决 issue。
- **弱者受益更大**：运行时 agent 越弱，增强带来的相对增益越明显；DeepSeek R1 在定位准确率上提升尤为突出（缺乏开箱即用的强 agentic 推理）。
- **自我增强不如外部结构化增强**：让 agent 在轨迹中自我增强，三个模型均**低于 Default**（−5 / −17 / −25），说明 agent 无法有效自我补全规格。
- **过滤与 LLM scoping 均必要**：去掉相关性过滤收益显著缩水；用 BM25 替代 LLM scoping 仍有提升但更小，说明 LLM 能捕捉词面之外的语义关系。
- **成本效率**：多数模型 tokens-per-resolved-issue 改善；把增强开销计入后优势仍在；GPT-5-mini 因轨迹极长（token 用量高一个数量级），增强开销占比小、影响有限。
- **Cross-synthesis 非对称性**：弱运行时模型受益于强增强器（DeepSeek R1 由 Qwen3-Coder 增强：108→164，+51.9%）；强运行时模型用弱增强器增益有限（GPT-5-mini：194→196）。
- **行为变化**：增强后 agent 早期更多使用 view/grep、更少 find，搜索词与文件目标更精准，减少无效广域探索；后期 patch/create/run 等主动操作增加。
- **描述质量**：增强后问题陈述平均更长，但分布更集中、长尾噪声（无关大日志/环境转储）减少，属“高价值技术上下文”而非无差别冗长。

## 7. 优点

- **即插即用、架构无关**：作为预处理层，不需改动任何 agent scaffold，可跨 SWE-agent / OpenHands / Mini-SWE-Agent 通用。
- **结构化与可追溯**：三阶段分解清晰，输出模板固定（描述/复现/期望/探索提示/修复提示），并保留生成指导与源码分析的对应关系。
- **验证维度全面**：除解决率外，还覆盖定位准确率、token/成本、运行时间、轨迹行为、描述长度分布，并做 cross-synthesis 与多组消融，结论支撑较扎实。
- **消融设计有针对性**：直接检验“自我增强是否可行”“过滤是否必要”“检索 vs LLM scoping”，回答了对方法合理性的关键质疑。
- **实用指导性强**：提出“用较便宜模型离线预计算增强、服务弱运行时 agent”的部署建议，具有工程落地价值。
- **定性材料丰富**：附录给出多实例、多模型的完整流水线可视化，便于理解增益来源。

## 8. 不足与局限

- **语言与基准覆盖窄**：仅在 Python 仓库与 SWEBench-Verified 上评估，作者自述受限于缺乏其他语言的可信评测基础设施；跨语言（不同类型系统、结构约定）有效性未知。
- **模型与 scaffold 数量有限**：3 个 LLM + 3 个 scaffold，虽具代表性但非穷尽，泛化性结论需谨慎。
- **开源 vs 工业代码差异**：开源仓库在架构模式、文档实践、代码质量、专有约束上可能与工业代码库系统性不同，未经闭源/领域特定代码验证。
- **运行时间开销不可忽视**：增强引入 4.6–7.8 分钟额外时延，延迟敏感场景需选择性部署。
- **长轨迹模型成本问题**：GPT-5-mini 的绝对 token 预算仍很高，增强无法缓解其成本结构。
- **静态定位指标偏差**：GPT-5-mini 常做运行时/动态编辑，静态文件级匹配低估其真实定位能力，说明评估指标存在度量盲区。
- **统计严谨性不足**：未见多次运行、方差或显著性检验报告，单次运行的波动风险未被量化。
- **增强质量依赖 LLM 自身**：若增强模型产生错误或噪声洞察，可能误导下游 agent；论文虽用相关性过滤缓解，但未系统分析错误传播与失败案例。
- **多仓库/更深程序分析未覆盖**：作者将多仓库场景与更深层程序分析列为未来工作，说明当前方案对跨仓库依赖与复杂静态分析支持有限。

（完）
