---
title: "Beyond Query Memorization: Large Language Model Routing with Query Decomposition and Historical Matching"
title_zh: 超越查询记忆：基于查询分解与历史匹配的大语言模型路由
authors: "Bo Lv, Jingbo Sun, Jianwei Lv, Chen Tang, Shaojie Zhang, Nayu Liu, Guoxin Yu, Zihao Li, Qichao Zhang, Dongbin Zhao, Ping Luo, Yue Yu"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://aclanthology.org/2026.acl-long.1852.pdf"
tags: ["query:ai-se"]
score: 5.0
evidence: 基于查询分解与历史匹配的大模型路由
tldr: 大模型部署需在预测性能与计算成本间权衡，现有路由方法依赖表层特征直接映射，易陷入记忆陷阱且泛化性差。作者提出DecoR框架，将路由重构为从历史日志中筛选相似查询的匹配过程，并引入查询能力解构以分离语言表层形式与任务意图。该方法有效缓解记忆陷阱，提升了分布外场景下的路由泛化能力。
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1852/fig-001.webp\", \"caption\": \"\", \"page\": 1, \"index\": 1, \"width\": 1300, \"height\": 800}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1852/fig-002.webp\", \"caption\": \"\", \"page\": 1, \"index\": 2, \"width\": 1300, \"height\": 800}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1852/fig-003.webp\", \"caption\": \"\", \"page\": 7, \"index\": 3, \"width\": 1440, \"height\": 840}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1852/fig-004.webp\", \"caption\": \"\", \"page\": 8, \"index\": 4, \"width\": 800, \"height\": 600}]"
motivation: 现有大模型路由方法依赖表层特征直接映射，易陷入记忆陷阱并在分布外数据上泛化性差。
method: 提出DecoR框架，将路由转化为从历史日志筛选相似查询的匹配过程，并解构查询能力以分离形式与意图。
result: 该方法有效缓解记忆陷阱，提升了分布外场景下模型路由的泛化能力。
conclusion: DecoR为大模型性能与成本权衡提供了更具泛化性的路由方案。
---

## Abstract
Optimizing the trade-off among predictive performance and computational cost is a central focus in the deployment of Large Language Models (LLMs). Current routing methods primarily rely on direct mapping from queries to models based on surface-level features, making them susceptible to the memorization trap and leading to poor generalizability on out-of-distribution (OOD) data. In this paper, we propose DecoR, a novel routing framework that recasts the routing task as a matching process of sifting similar queries from historical logs, effectively mitigating the memorization trap. To enhance matching accuracy, we introduce a query capability deconstruction method that decouples linguistic surface forms from task-intrinsic requirements, directing matching toward capability dimensions to ground decisions in essential task attributes. Furthermore, we develop CodaSet, a comprehensive benchmark for assessing routing generalization, where experimental results demonstrate that DecoR maintains superior accuracy while substantially lowering inference costs across both in-distribution and OOD settings.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义

- **研究背景**：大语言模型（LLM）部署需要在预测性能与推理成本之间权衡。不同查询的复杂度差异很大，并非所有任务都需要调用最大、最贵的模型，因此“模型路由”成为关键环节。
- **核心问题**：现有路由方法大多把查询到模型的决策简化为“黑盒映射”，依赖查询表层语义特征直接预测模型 ID。这容易陷入**记忆陷阱**：路由器记住训练查询的表层模式，而非理解任务真正需要的能力，导致在分布外（OOD）数据上泛化崩溃。
- **整体含义**：论文主张将路由从“查询→模型”的直接映射，重构为“查询能力需求→历史相似日志→模型历史表现”的匹配与经验复用过程，从而缓解记忆陷阱，提高 OOD 鲁棒性，并支持通过更新日志迭代系统而无需重新训练路由模型。

### 2. 论文提出的方法论

#### 核心思想

提出 **DecoR**（Decomposition-based Routing）框架，将路由任务转化为：从历史查询-响应日志中筛选与当前查询在**能力需求**上相似的记录，再根据这些历史记录中各模型的表现与成本做经验决策。

#### 关键技术流程

1. **查询解构阶段（Query Deconstruction）**
   - 使用查询解构器 \(f_{dec}\) 将原始查询 \(q\) 转换为结构化能力画像：
     \[
     p=\{S,K,D\}
     \]
   - **S（Skill Set）**：完成任务所需的原子技能，如信息抽取、摘要、推理、写作等，并给出理由。
   - **K（Knowledge Domain）**：所需知识领域，如医学、法律、数学等，并给出理由。
   - **D（Difficulty）**：离散为 \(D_0\) 到 \(D_3\) 四个难度等级，并给出理由。
   - 技能与知识类别不预定义，由解构器根据查询动态生成。训练数据由 GPT-5 合成，并经三名计算机博士生专家审核，采用 SFT 训练。

2. **分层日志筛选阶段（Hierarchical Log-Sifting）**
   - **Substage A：字符级能力约束筛选**
     - 用 Jaccard 相似度计算技能集合 \(S\) 和知识集合 \(K\) 的重叠：
       \[
       Sim_{sk}=\frac{|S_u\cap S_i|}{|S_u\cup S_i|}+\frac{|K_u\cap K_i|}{|K_u\cup K_i|}
       \]
     - 用难度匹配函数 \(w(D_i,D_u)\) 校准：历史难度不低于当前查询则权重为 1；每低一级扣 0.25。
     - 最终得分 \(Score_A=Sim_{sk}\times w\)，保留 \(Score_A\ge \tau\) 的日志。若没有日志通过，则判定为 OOD，直接进入回退策略。
   - **Substage B：精细排序**
     - 使用 BGE-M3 编码“查询文本 + 能力画像”，计算余弦相似度，保留 Top-\(k\) 日志。
   - **Substage C：日志对齐评估**
     - 使用 Log Evaluator（基于 Qwen3-0.6B，GRPO 训练）对候选日志做长上下文判断，输出真正有代表性的日志索引集合 \(V\)；若没有有效日志则输出空集。
     - GRPO 奖励函数鼓励高召回、惩罚幻觉和检索失败：完全匹配得 +6；真实为空但预测非空得负分；真实非空但完全无交集得 -6；其他情况按命中数与误报数计算。

3. **经验决策阶段（Empirical Decision）**
   - 若 Substage A 判定 OOD 或 Substage C 输出 \(V=\varnothing\)，触发回退机制，调用预设高性能模型。
   - 否则，对匹配日志中每个候选模型统计平均性能 \(\bar V_j\) 和平均成本 \(\bar C_j\)，做 min-max 归一化，得到性能效用 \(V_j^{norm}\) 和成本效用 \(C_j^{norm}\)。
   - 用平衡因子 \(\lambda\in[0,1]\) 计算综合效用：
     \[
     U_j=\lambda V_j^{norm}+(1-\lambda)C_j^{norm}
     \]
   - 选择 \(m^*=\arg\max_j U_j\) 作为最终模型。

#### 训练与参数

- 查询解构器与 Log Evaluator 均以 **Qwen3-0.6B** 为基座。
- 解构器使用 SFT，学习率 \(2\times10^{-5}\)。
- Log Evaluator 使用 **VERL** 框架和 GRPO，学习率 \(1\times10^{-6}\)。
- 默认参数：阈值 \(\tau=0.5\)，Top-\(k=3\)，平衡因子 \(\lambda=0.5\)。

### 3. 实验设计

- **Benchmark**：作者构建 **CodaSet**，用于评估路由泛化能力。
- **ID 数据集**：
  - MMLU-Pro：多学科复杂推理；
  - GSM8K：数学应用题；
  - IFEval：指令遵循；
  - BBH：逻辑推理。
- **OOD 数据集**：
  - Math500：高难度数学；
  - MT-bench：多轮对话；
  - MBPP：Python 代码生成。
- **LLM 池**：8 个代表性模型，包括 Kimi-K2-Instruct、DeepSeek-V3.1-Terminus、DeepSeek-V3.2-Exp、Qwen3-235B-A22B、gpt-oss-120b、gemma-3-27b-it、Mistral-Small-3.2-24B、gemma-3-12b-it。推理与成本通过 DeepInfra API 获取。
- **对比方法**：
  - Random Router；
  - LLM Router；
  - RouterDC；
  - KNN Router；
  - EmbedLLM；
  - MODEL-SAT。
- **评价指标**：
  - MMLU-Pro、GSM8K、BBH 使用 Exact Match 准确率；
  - Math500 使用 OpenAI simple-evals；
  - MBPP 使用 EvalPlus；
  - MT-Bench 使用 FastChat LLM-as-a-Judge，GPT-5.1 评分；
  - IFEval 使用官方自动脚本。
  - 准确率类指标采用五次独立运行多数投票，MT-bench 取平均；整体结果三次独立试验平均。

### 4. 资源与算力

- 论文明确提到实验在**配备 8 块 NVIDIA H100 GPU 的服务器集群**上进行。
- 使用 Qwen3-0.6B 作为解构器和 Log Evaluator 的基座，训练框架包括 SFT 和 VERL/GRPO。
- 给出了学习率、batch size、优化器、序列长度、训练 epoch 等超参数。
- **未明确说明**：总 GPU 小时、具体训练时长、能耗、每个模块的实际训练成本。论文仅说明硬件配置，未给出训练时间统计。

### 5. 实验数量与充分性

- **主要实验**：
  - ID 场景：4 个数据集，比较 8 个候选模型、6 个路由基线、2 个 DecoR 回退变体。
  - OOD 场景：3 个数据集，同样比较候选模型、基线和 DecoR。
- **消融实验**：
  - 在 GSM8K、MMLU-Pro、BBH 上分别移除 Stage A、Stage B、Stage C，共 3 个消融设置。
- **规模分析**：
  - 比较 Qwen3-0.6B、1.7B、4B 作为解构器/评估器基座，在 ID 和 OOD 上评估。
- **超参数敏感性**：
  - 分析 \(\lambda\) 对性能与成本的影响；
  - 分析阈值 \(\tau\in[0.1,0.9]\) 的影响。
- **案例分析**：
  - 提供两个案例：一个触发回退机制，一个成功匹配历史日志。
- **充分性评价**：
  - 实验覆盖面较广，涵盖 ID/OOD、多个任务类型、多个基线和消融，整体较充分。
  - 公平性方面：所有基线均使用 CodaSet 训练集训练；候选模型池和成本口径统一；多次运行取平均。
  - 但仍存在一些不足：未报告标准差或显著性检验；主要 benchmark 由作者构建；成本依赖特定时间点的 API 定价；部分评估依赖 LLM-as-a-Judge，可能引入偏差。

### 6. 论文的主要结论与发现

- DecoR 在 ID 和 OOD 场景下均能在保持较高准确率的同时显著降低推理成本。
- 在 ID 设置中，DecoR 平均性能接近最强单模型 Qwen3-235B，但成本明显更低；例如平均性能 89.35%、成本 2.1x，而 Qwen3-235B 为 90.60%、成本 5.0x。
- 在 OOD 设置中，现有路由基线普遍显著退化，部分甚至不如 Random Router；DecoR 通过回退机制保持较稳定的性能。
- 消融表明查询解构 Stage A 最关键：移除后准确率下降且成本最高可增至 2.1 倍。
- 增大解构器/评估器基座规模带来的收益有限：4B 相比 0.6B 在 ID 上仅提升约 0.11%，OOD 上约 0.89%，因此 0.6B 是更经济的默认选择。
- \(\lambda=0.5\) 在性能与成本之间达到较优平衡；\(\tau=0.5\) 在性能提升与成本增长之间取得折中。
- 系统可通过更新历史日志实现迭代，而不必重新训练路由模型。

### 7. 优点

- **问题重构有新意**：将路由从黑盒映射改为“能力画像 + 历史日志匹配”，直接针对记忆陷阱和 OOD 泛化问题。
- **能力解构设计合理**：将查询拆成技能、知识、难度三个维度，减少表层语言形式对路由的干扰。
- **分层筛选兼顾效率与精度**：倒排索引/Jaccard 做粗筛，BGE-M3 做精排，Log Evaluator 做语义对齐，流程清晰。
- **回退机制增强鲁棒性**：在无可靠历史经验时调用高性能模型，避免 OOD 场景下的错误路由。
- **成本意识强**：显式建模性能与成本，并通过 \(\lambda\) 调节偏好；使用 0.6B 小模型做路由组件，部署成本低。
- **实验较全面**：覆盖 ID/OOD、多个任务、多个基线、消融、规模分析和超参数敏感性。
- **可扩展性**：日志更新即可迭代，不需要因模型池变化而重新端到端训练路由器。

### 8. 不足与局限

- **评估依赖作者构建的 CodaSet**：虽然覆盖多个任务，但仍是单一 benchmark，外部泛化性仍需更多独立数据集验证。
- **训练数据依赖 GPT-5 合成与专家审核**：解构器和 Log Evaluator 的训练数据质量受合成模型和人工审核影响，存在标注偏差与成本问题。
- **LLM-as-a-Judge 风险**：MT-Bench 等评估依赖 GPT-5.1 评分，可能引入评判偏差；历史日志中的性能分数也受 judge 影响。
- **OOD 回退会增加成本**：虽然保证稳定性，但 OOD 查询集中调用高性能模型会带来局部成本上升。
- **历史日志离线构建**：论文提到尚未实现完全自动的在线更新，新数据实时同步和去重过滤仍是未来工作。
- **实验统计信息不足**：未报告方差、置信区间或显著性检验；训练时长和总 GPU 小时未说明。
- **模型池与成本口径有限**：仅 8 个模型，成本基于特定时间点的 DeepInfra 定价，可能随部署环境变化。
- **基座模型单一**：解构器和评估器主要基于 Qwen3 系列，未验证其他模型家族作为路由组件的效果。
- **超参数调优范围有限**：

- **超参数调优范围有限**：论文主要考察了 \(\lambda\) 与 \(\tau\) 两个超参数，Top-\(k\)、难度折扣步长、Jaccard 相似度权重等同样影响路由行为，但未做系统扫描；此外默认参数在不同任务分布下是否普适仍缺乏证据。
- **能力画像粒度较粗**：技能与知识类别由解构器动态生成，存在同义表述不一致、类别漂移的风险；难度仅离散为四级，对细粒度难度差异不敏感，可能影响日志匹配的召回质量。
- **对历史日志覆盖度敏感**：方法本质是“经验复用”，当新任务领域或新模型在日志中样本稀少时，匹配质量下降，性能上限受日志规模与代表性约束；论文未系统分析日志规模/冷启动对效果的影响曲线。
- **候选模型池变化需重建日志**：虽然无需重训路由器，但新增模型仍需在历史查询上补齐响应与评分，冷启动成本不可忽略。
- **与强单模型的差距未充分讨论**：ID 场景下 DecoR 平均性能仍略低于最强单模型，论文未深入分析在何种任务分布下路由的相对收益最大、何时应直接使用大模型。

### 9. 总体评价与启示

- **定位**：DecoR 是一篇“问题重构型”工作，其核心贡献不在于提出更复杂的预测器，而在于把路由从**表层语义→模型 ID 的黑盒映射**转为**能力需求→历史经验→模型表现**的可解释检索式决策，直接回应了路由器的记忆陷阱与 OOD 泛化问题。
- **方法成熟度**：三阶段流水线（解构—分层筛选—经验决策）设计完整，粗筛/精排/对齐的分层结构在工程上兼顾了效率与精度；回退机制为 OOD 场景提供了安全网，使系统在缺乏可靠经验时不会做出高风险决策。
- **实证强度**：ID/OOD 双场景、多任务、多基线、消融、规模与超参数分析的组合较为扎实，尤其 OOD 上基线普遍退化而 DecoR 保持稳定的结果具有说服力；但单一自建 benchmark、缺少方差与显著性检验、评估部分依赖 LLM-as-a-Judge，使其结论的统计稳健性与外部有效性仍待独立复现验证。
- **实践启示**：对实际部署而言，该工作提示路由系统的关键资产是**结构化的历史日志**而非路由器参数本身——日志可增量更新、可审计、可解释，这为模型池快速迭代的工业场景提供了低摩擦的演进路径；同时 0.6B 小模型即可承担解构与评估，说明路由组件的算力门槛可以很低。
- **后续研究方向**：可探索在线/增量日志更新与去重、更细粒度且一致的能力本体、日志规模与冷启动的定量分析、跨模型家族的组件迁移性，以及引入方差报告与显著性检验的标准化评测协议。

（完）
