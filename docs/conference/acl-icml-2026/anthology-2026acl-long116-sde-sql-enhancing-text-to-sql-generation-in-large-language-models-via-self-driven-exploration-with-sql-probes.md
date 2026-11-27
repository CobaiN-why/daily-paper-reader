---
title: "SDE-SQL: Enhancing Text-to-SQL Generation in Large Language Models via Self-Driven Exploration with SQL Probes"
title_zh: SDE-SQL：通过SQL探针自驱动探索增强大模型文本到SQL生成
authors: "Wenxuan Xie, Yaxun Dai, Wenhao Jiang"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://aclanthology.org/2026.acl-long.116.pdf"
tags: ["query:ai-se"]
score: 8.0
evidence: 大模型文本到SQL生成的自驱动数据库探索
tldr: 现有文本到SQL方法依赖推理时静态、预处理好的数据库信息，限制了大模型对底层数据的深入理解。SDE-SQL提出自驱动探索框架，让模型在推理中生成并执行SQL探针以主动查询和探索数据库。实验表明这种动态交互能显著提升文本到SQL生成准确率，为数据库场景下的代码生成提供新思路。
source: ACL-2026-Long
selection_source: conference_retrieval
motivation: 文本到SQL方法依赖静态预处理信息，模型无法自主探索数据库内容。
method: 让模型在推理时生成并执行SQL探针，实现对数据库的自驱动探索。
result: 实验表明自驱动探索显著提升文本到SQL任务的生成准确率。
conclusion: 动态数据库交互为增强大模型结构化查询生成提供有效途径。
---

## Abstract
Recent advances in large language models (LLMs) have led to substantial progress on the Text-to-SQL task. However, existing approaches typically depend on static, pre-processed database information supplied at inference time, which restricts the model’s capacity to deeply comprehend the underlying database content. In the absence of dynamic interaction, LLMs are limited to fixed, human-curated context and lack the ability to autonomously query or explore the data. To overcome this limitation, we introduce SDE-SQL , a novel framework that empowers LLMs to perform Self-Driven Exploration of databases during inference. This is achieved through the generation and execution of SQL probes , enabling the model to actively retrieve information and iteratively refine its understanding of the database. Unlike prior methods, SDE-SQL operates in a zero-shot setting, requiring no in-context demonstrations or question-SQL pairs. Evaluated on the BIRD benchmark with Qwen2.5-72B-Instruct , SDE-SQL achieves an 8.02 % relative improvement in execution accuracy over the vanilla Qwen2.5-72B-Instruct baseline, establishing a new state-of-the-art among open-source methods without supervised fine-tuning (SFT) or model ensembling. Furthermore, when combined with SFT, SDE-SQL delivers an additional 0.52 % performance gain.

---

## 论文详细总结（自动生成）

# SDE-SQL 论文结构化总结

## 1. 核心问题与研究动机

- **任务背景**：Text-to-SQL 旨在将自然语言问题翻译为可执行 SQL。基于 LLM 的方法在 Spider 上已超过 90% 执行准确率，但在 BIRD、Spider 2.0 等更真实、更复杂的基准上，与人类专家仍有明显差距。
- **核心痛点**：现有方法（schema linking → SQL 生成 → SQL 修正三段式）在推理时依赖**静态、预先处理、人工整理的数据库上下文**（schema 描述、列说明、少量示例值）。模型无法在推理过程中主动查询数据库，只能从固定的候选列/候选中“盲猜”。
- **问题根源**：真实数据库复杂且“脏”——多表存在语义相同但格式不同的列，某些值只存在于特定表中。信息不足时，模型对相似列/值的组合选择近乎随机，导致同一道题时而正确、时而错误（性能不稳定）。
- **被忽视的性质**：SQL 本身是数据库接口，具备**快速、信息量大的可交互性**，但此前主要被当作中间产物或最终输出，其“探询”能力未被利用。
- **整体含义**：论文主张把“与数据库动态交互”作为推理机制的核心，而非仅把执行结果当作辅助反馈，从而缩小 LLM 与人类专家在复杂真实库上的差距。

## 2. 方法论

### 2.1 核心思想
让 LLM 在推理过程中**自驱动地生成并执行一系列辅助查询（SQL Probes，SQL 探针）**，主动从数据库中获取证据，并将证据用于 SQL 的**生成阶段**与**修正阶段**，形成统一的“探索—生成—再探索—修正”流程。整个流程在**零样本**设定下运行（不使用问题-SQL 示范对）。

### 2.2 模块一：基于实体的 Schema Linking
- **实体化取值检索（Value Retrieval）**：先用 few-shot 提示让 LLM 从问题中抽取实体；再用基于**局部敏感哈希（LSH）+ 语义相似度**的检索器在库中匹配相似取值。
- **软 Schema Linking**：以 one-shot 方式提示 LLM 按实体选择相关列。
  - 被选中的列：提供尽可能详细的信息（列名、类型、列描述、取值示例、取值描述）；
  - 未被选中的列：仅保留列名与类型（不删除）。
  - 作用：既压缩输入长度、聚焦相关 schema，又通过“保留但降权”提高容忍度，避免误删有用列。

### 2.3 模块二：基于自驱动探索的生成（两阶段探索）
- **问题拆解视角**：自然语言问题 Q 分为**目标（Target）**与**若干条件（Condition）**，分别对应 SELECT 子句与 WHERE 等子句。
- **阶段一：候选探索（Candidates Exploration）**
  - 先为每个目标实体生成若干 **Base SQL Probes**（只查询目标列，不带其他条件）；
  - 再为每个条件实体在 Base Probe 上追加“候选列 + 可能候选值”，生成 **Condition SQL Probes**；
  - 若某实体对应多个同义候选列，则用探针逐一验证该值是否存在于各候选列中；
  - 生成过程可视为树形结构，每条根到叶路径对应一个条件描述候选。
- **阶段二：组合探索（Combinations Exploration）**
  - 依据阶段一的执行结果（空 / 非空）剔除明显无效的候选列；
  - 对所有条件做笛卡尔式组合生成新探针（如 1×2×1×3=6 条），凡是返回空结果的候选组合直接判定为不适用。
- **零样本生成**：LLM 仅依据 schema + 两阶段探索结果生成 SQL，**不使用问题分解策略、不使用 few-shot 示范**；并采用**自一致性（self-consistency）**：生成多条 SQL，按执行结果的一致性投票选出最终答案。
- **设计论点**：作者认为，相比于设计更复杂的分解提示、多候选搜索或 MCTS，**“给模型足够的信息”**带来的收益更大。

### 2.4 模块三：基于自驱动探索的修正
- **可执行报错（语法/模式错误）**：执行反馈已含足够信息，直接据此改写。
- **可执行但结果为空**：分三阶段处理。
  1. **错误原因识别阶段**：自研基于 **SQLGlot** 的分解器，将 SQL 转为 **AST**，按节点类型与关系识别“不可再分的条件单元”，生成语义合法的 **Sub-SQL 探针**并执行，把执行结果（空/非空）交给 LLM 做细粒度诊断。
  2. **解决方案探索阶段**：归纳五类空结果成因，并据此生成针对性探针验证假设：
     - 条件冲突（同一实体对应多候选列，只有特定列与其他条件组合才有数据）；
     - 条件重复（同一条件被多个同义列重复描述，互相排斥）；
     - 不必要的表连接（JOIN 交集为空）；
     - 列与值不匹配（值格式不符，或选了“看起来像”但实际不含该值的列）；
     - 子查询作用域不一致（如子查询用 MIN/MAX 取到的行不在 JOIN 结果中）。
  3. **修改阶段**：综合探针结果输出修正 SQL。
- **目标检查模块（Target Checking）**：修正后校验 SELECT 子句是否与问题目标一致。为**避免引入新错误**，只允许模型判断并**删除多余的目标列**，不做其他改动；输出为 JSON（`Modification` / `Final SQL`）。

### 2.5 模块四：监督微调（SFT）
- 数据来源：BIRD 训练集，用 Qwen2.5-72B-Instruct 通过**基于提示的 rollout 流水线**采样，仅保留最终生成正确 SQL 的样本。
- 规模：9,428 条中筛出 **5,231 条有效样本**；每条推理轨迹拆为两部分——**探索阶段**（生成 SQL 探针）与**预测阶段**（基于探索结果生成最终 SQL），据此分别微调 Explorer 与 Generator。

## 3. 实验设计

- **数据集 / 基准**
  - **BIRD**（主实验）：95 个大规模真实数据库、含脏值，12,751 条问题-SQL 对，带列描述与外部知识；报告 **dev** 集结果。
  - **Spider**：200 个数据库、10,181 问题 / 5,693 SQL，跨域；报告 **dev 与 test** 结果（仅在 BIRD 上 SFT，用于检验泛化）。
- **评价指标**：**执行准确率（Execution Accuracy, EX）**；因超时约束下执行存在波动，执行脚本**重复运行 5 次取平均**，每次对每条预测 SQL 单次执行判定。
- **对比方法**
  - 闭源模型系：GPT-4 零样本、DIN-SQL+GPT-4、DAIL-SQL+GPT-4、MAC-SQL+GPT-4、MCS-SQL、CHESS、Distillery+GPT-4、OpenSearch-SQL v2+GPT-4o、XiYan-SQL、CHASE-SQL+Gemini、AskData+GPT-4o。
  - 开源模型系（无模型集成）：DTS-SQL+DeepSeek-7B、SFT CodeS-15B、SQL-o1+Llama3-8B、OneSQL-v0.1-Qwen-32B、XiYanSQL-QwenCoder-32B，以及基线 **Qwen2.5-72B-Instruct**。
- **其他实验**
  - 逐模块消融（7 种去除配置）+ 微调模块组合（3 种）；
  - 按难度分层（Simple / Moderate / Challenging）的结果与延迟分析；
  - 端到端时延与各阶段耗时分解（vLLM 本地部署）；
  - 附录含错误成因示例、AST 分解示例、5 个阶段的完整提示模板。

## 4. 资源与算力

- **训练**：SFT 在 **8 张 NVIDIA A800 GPU** 上进行，探索任务与生成任务各训练 **24 小时**；采用 **LoRA**（rank=16），学习率 1.0e-4，2 个 epoch，per-device batch size 1，梯度累积 8 步，cosine 调度。
- **推理**：本地部署，使用 **vLLM**；平均每实例 **35.19 s**（BIRD-dev 全集 1,534 条）。
- **未明确说明**：论文未给出各阶段 API 调用总次数、总 token 消耗、单卡显存占用，也未报告零样本（免训练）流程的总推理成本与多轮探针的平均调用轮数。

## 5. 实验数量与充分性

- **实验组数（约）**
  - 主实验 2 个基准（BIRD dev；Spider dev+test），合计 3 个评测设置；
  - 消融 7 组 + 微调变体 3 组，共 **10 组配置**；
  - 延迟实验：4 个难度/总体统计 × 5 个阶段耗时；并与 MAG-SQL、CHESS 在采样子集上对比；
  - 另含按难度分层的性能拆解与多组定性示例。
- **充分性评价**
  - **较充分**：覆盖两个主流基准、含跨数据集泛化测试、逐模块消融、效率分析，且对执行波动做了 5 次重复取平均，方法学上较严谨；消融设计能定位“探索”这一核心贡献（去掉两处探索共降 3.20 个百分点，是单项最大降幅）。
  - **可加强之处**：
    - 未与同样引入“执行反馈/多轮交互”的最新方法（如 ReEx-SQL、CHASE-SQL 的完整流水线）在同一模型上做**受控对比**，跨论文比较存在模型与提示差异；
    - 缺少对**探针数量、探索轮数、候选列数**等超参的敏感性分析；
    - 未报告方差/置信区间（仅说明 5 次取平均），小幅度提升（如 SFT 的 +0.52）显著性不明；
    - 延迟对比仅在“采样子集”上进行，与全集的 35.19 s 口径不完全一致。
- **公平性**：基线选择较为全面，且区分了“闭源 + 集成”与“开源 + 无集成”两类；但 SDE-SQL 用 72B 开源模型对比部分 7B/8B/15B/32B 开源方法与 GPT-4 系闭源方法，模型规模不完全对齐，绝对数值的可比性需谨慎解读。

## 6. 主要结论与发现

- **BIRD dev**：零样本 **67.67%**，SFT 后 **68.19%**；相比原始 Qwen2.5-72B-Instruct 的 60.17%，绝对提升 **7.50** 个百分点，在“无 SFT、无模型集成”的开源方法中达到新的 SOTA，并超过多数基于 GPT-4 的方法。
- **Spider**：仅在 BIRD 上 SFT 即在 Spider 取得 dev **87.5** /

- **Spider**：仅在 BIRD 上 SFT 即在 Spider 取得 dev **87.5** / test 集上同样保持较强泛化能力（具体数值见原文对应表格），说明在 BIRD 上学到的“探针式探索”策略能够迁移到跨域 schema，而非仅拟合 BIRD 的库结构。
- **消融结论**：逐模块去除实验显示，**候选探索 + 组合探索**是贡献最大的组件，二者同时移除时执行准确率下降 **3.20** 个百分点，为单项最大降幅；空结果修正、目标检查、实体化 schema linking 亦各有正贡献。SFT 在零样本流程之上再带来约 **+0.52** 个百分点，说明“探索能力”既可通过提示工程获得，也可通过监督微调进一步内化。
- **难度分层**：在 Simple 问题上各方法差距较小，SDE-SQL 的优势主要体现在 **Moderate / Challenging** 层，尤其是需要区分同义列、脏值格式和多表连接的真实库场景，这与“主动获取证据以消除歧义”的设计动机一致。
- **效率表现**：BIRD-dev 全集平均每实例 **35.19 s**（vLLM 本地部署），虽高于单次生成式基线，但低于部分依赖多轮 agent 编排或大规模候选搜索的方法；耗时主要分布在探针生成与执行、空结果修正的多阶段诊断上，属于“以可控延迟换取稳定性”的权衡。
- **定性发现**：案例表明探针能够有效识别“值存在但格式不同”“同义列中仅某一列含目标值”“JOIN 交集为空”“子查询作用域错位”等静态上下文难以暴露的问题；目标检查模块通过“只删不加”的保守策略，降低了修正阶段引入新错误的概率。

## 7. 局限性与可改进方向

- **探针规模与组合爆炸**：组合探索按条件做笛卡尔积，条件数较多时探针数量可能快速增长；论文未给出探针数量、探索轮数、候选列数的敏感性分析，实际部署时需配合剪枝或预算控制。
- **对 LLM 生成探针质量的依赖**：实体抽取、候选列/值枚举、空结果成因诊断均依赖模型判断，若模型遗漏关键候选列，后续探针无法弥补；错误会沿“探索→生成→修正”链路传播。
- **执行成本与安全边界**：方法要求对数据库执行大量只读查询，真实生产环境需考虑权限控制、查询限流、敏感数据暴露与审计问题；论文未讨论这些工程约束。
- **泛化范围有限**：SFT 数据仅来自 BIRD，虽在 Spider 上验证了迁移，但对 Spider 2.0 等涉及超长 schema、外部文档、企业级方言的场景尚未评估。
- **统计显著性不足**：仅报告 5 次执行取平均，未给出方差或置信区间，SFT 带来的小幅提升（+0.52）是否显著缺乏统计检验。
- **对比公平性**：与部分 7B/8B/15B/32B 开源方法及 GPT-4 系闭源方法比较时，模型规模与是否使用集成不完全对齐，绝对数值需谨慎解读；亦缺少与同样采用多轮执行反馈的最新方法在同一底座模型上的受控对比。

## 8. 总体评价与启示

- **核心贡献**：论文将 SQL 从“待生成的输出”重新定位为“可主动调用的数据库探询接口”，把动态证据获取嵌入生成与修正两个阶段，形成零样本即可运行的“探索—生成—再探索—修正”闭环；这一视角对 Text-to-SQL 乃至更广泛的“LLM + 数据库”推理具有方法论启发。
- **工程价值**：实体化 schema linking 的“选中列详述、未选中列保留降权”设计，以及空结果修正中基于 SQLGlot/AST 的 Sub-SQL 探针分解，具有较强的可复用性；目标检查“只删不加”的保守约束也体现了对“修正引入新错误”的务实权衡。
- **实验说服力**：主实验覆盖 BIRD 与 Spider、含跨数据集泛化与逐模块消融，执行波动做了 5 次重复，整体较为扎实；但超参敏感性、统计显著性与受控对比仍有提升空间。
- **适用边界**：该方法更适合 schema 复杂、取值脏乱、列语义重叠的真实分析型数据库；对于简单查询或对延迟极度敏感的场景，探针开销可能得不偿失，需按场景做预算裁剪。
- **未来方向**：可探索学习式/强化学习式的探针策略、探针缓存与去重、基于代价模型的预算分配、将探索能力扩展到多轮对话式查询与企业级方言，以及在 Spider 2.0 等更真实基准上的系统评估。

（完）
