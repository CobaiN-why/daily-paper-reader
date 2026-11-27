---
title: "CoreCodeBench: Decoupling Code Intelligence via Fine-Grained Repository-Level Tasks"
title_zh: CoreCodeBench：通过细粒度仓库级任务解耦代码智能
authors: "Lingyue Fu, Hao Guan, Bolun Zhang, Haowei Yuan, Yaoming Zhu, Lin Qiu, ZongYu Wang, Xuezhi Cao, Xunliang Cai, Weiwen Liu, Weinan Zhang, Yong Yu"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://aclanthology.org/2026.acl-long.1196.pdf"
tags: ["query:ai-se"]
score: 8.0
evidence: 细粒度仓库级基准剖析大模型编码能力
tldr: 现有面向软件工程的大模型评测多依赖粗粒度通过率，将编程能力视为单一整体，掩盖了具体认知瓶颈且易受数据污染。作者提出CoreCodeBench可配置仓库级基准，借助自动框架CorePipe将Python仓库转化为一系列原子化任务，以分离不同编码能力。该基准能更精细地诊断大模型的编码短板，为代码智能评估提供新工具。
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1196/fig-001.webp\", \"caption\": \"\", \"page\": 1, \"index\": 1, \"width\": 1148, \"height\": 606}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1196/fig-002.webp\", \"caption\": \"\", \"page\": 1, \"index\": 2, \"width\": 350, \"height\": 350}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1196/fig-003.webp\", \"caption\": \"\", \"page\": 1, \"index\": 3, \"width\": 789, \"height\": 789}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1196/fig-004.webp\", \"caption\": \"\", \"page\": 1, \"index\": 4, \"width\": 792, \"height\": 336}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1196/fig-005.webp\", \"caption\": \"\", \"page\": 3, \"index\": 5, \"width\": 575, \"height\": 257}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1196/fig-006.webp\", \"caption\": \"\", \"page\": 3, \"index\": 6, \"width\": 691, \"height\": 336}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1196/fig-007.webp\", \"caption\": \"\", \"page\": 13, \"index\": 7, \"width\": 468, \"height\": 414}]"
motivation: 现有仓库级评测依赖粗粒度通过率，将编程能力视为单一整体，掩盖具体瓶颈且易受数据污染。
method: 提出CoreCodeBench可配置基准，借助CorePipe自动将Python仓库转化为原子化任务以分离不同编码能力。
result: 该基准通过细粒度任务揭示了大模型在各类编码认知能力上的具体差异与瓶颈。
conclusion: CoreCodeBench为更精细、抗污染的大模型代码智能评测提供了可配置方案。
---

## Abstract
The evaluation of Large Language Models (LLMs) for software engineering has shifted towards complex, repository-level tasks. However, existing benchmarks predominantly rely on coarse-grained pass rates that treat programming proficiency as a monolithic capability, obscuring specific cognitive bottlenecks. Furthermore, the static nature of these benchmarks renders them vulnerable to data contamination and performance saturation. To address these limitations, we introduce CoreCodeBench, a configurable repository-level benchmark designed to dissect coding capabilities through atomized tasks. Leveraging our automated framework, CorePipe, we extract and transform Python repositories into a comprehensive suite of tasks that isolate distinct cognitive demands within identical code contexts. Unlike static evaluations, CoreCodeBench supports controllable difficulty scaling to prevent saturation and ensures superior data quality. It achieves a 78.55% validity yield, significantly surpassing the 31.7% retention rate of SWE-bench-Verified. Extensive experiments with state-of-the-art LLMs reveal a significant capability misalignment, evidenced by distinct ranking shifts across cognitive dimensions. This indicates that coding proficiency is non-monolithic, as strength in one aspect does not necessarily translate to others. These findings underscore the necessity of our fine-grained taxonomy in diagnosing model deficiencies and offer a sustainable, rigorous framework for evolving code intelligence. Code of CorePipe framework and data of CoreCodeBench are available in https://github.com/AGI-Eval-Official/CoreCodeBench and https://huggingface.co/collections/tubehhh/corecodebench.

---

## 论文详细总结（自动生成）

# CoreCodeBench 论文详细总结

## 1. 核心问题与整体含义（研究动机与背景）

- **背景**：面向软件工程的大模型（LLM）评测已从函数级代码片段（HumanEval、MBPP）演进到复杂的仓库级任务（SWE-bench、BigCodeBench 等）。
- **核心问题一：粗粒度评测掩盖认知瓶颈**。现有基准普遍以单一的 pass rate（通过率）衡量编程能力，将编程视为“单一整体能力”。然而真实软件工程需要在**生成代码（Development）、推理逻辑错误（BugFix）、规划验证约束（TDD）** 等不同认知维度间切换，单一指标会掩盖具体的认知短板。
- **核心问题二：静态基准的双重脆弱性**。固定快照式基准易受**数据污染**（模型记忆开源训练数据）和**性能饱和**（新模型迅速攻克固定难度）影响，评测寿命有限。
- **关键观察（图 1b）**：在同一代码上下文下拆解任务后，模型表现出显著的**能力错位（capability misalignment）**——例如 Kimi-K2 在 Development 上强，但在 BugFix 与 TDD 上弱，通过率差距超过 35%。这说明编码能力**并非单一整体**。
- **整体含义**：亟需一个自动化、可扩展、支持动态难度调节、能隔离不同认知维度的细粒度仓库级评测框架，作为“移动靶”持续对齐代码智能前沿。

---

## 2. 方法论：核心思想与关键技术细节

### 2.1 核心思想
- 提出 **CoreCodeBench**：可配置的仓库级基准，通过**原子化任务（atomized tasks）** 在**相同代码上下文**下隔离不同认知需求。
- 提出 **CorePipe** 自动化流水线，将静态 Python 仓库转化为动态、可扩展的评测任务，分三阶段：**上下文抽取 → 原子任务生成 → 复合任务扩展**。

### 2.2 阶段一：仓库上下文抽取
- 从 PyPI 选取 **12 个开源 Python 仓库**，标准为：(1) 近 6 个月活跃维护；(2) 测试文件占比 >15%；(3) >5,000 LOC 且存在跨模块依赖。
- 采用“LLM 结构分析 + 规则匹配”混合方法建立 `<源码, 测试>` 映射；用定制版 **pycallgraph** 动态追踪构建 **Function Call Tree**（节点=函数，边=调用依赖），作为核心逻辑识别与复杂任务组合的骨架。

### 2.3 阶段二：原子任务生成（认知隔离）
- **核心代码识别**：用 LLM 识别语义核心的 AST 块，过滤琐碎工具函数；通过**掩码长度（mask length）** 调节难度；仅保留“掩码后导致单测失败”的函数，确保缺失逻辑对正确性必要（人工抽检 50 例，100% 准确）。
- **Development（开发）**：掩码核心代码块，用 GPT-4o 生成结构化功能描述，Claude-3.5-Sonnet 作为 critic 迭代改进；引入 **Information Gain (IG) 过滤器**剔除无效描述（IG = AC Rate_exp − AC Rate_no-exp）。
- **BugFix（缺陷修复）**：采用**级联逻辑-实现合成**——大模型（如 GPT-4o）设计复杂逻辑谬误（边界疏忽、状态管理错误），小模型（如 Qwen3-Coder-30B）实现，模拟真实开发者失误，避免人工痕迹明显的语法扰动。
- **TDD（测试驱动开发）**：掩码核心代码，提供对应单元测试作为规格；通过调用树映射确保测试约束直接约束目标实现。

### 2.4 阶段三：复合任务生成（多函数问题）
- 在全局调用树 G=(V,E) 上，按超参数 **依赖深度 d** 与 **任务数量 ν** 随机采样连通子图 G′（|V(G′)|≤ν，深度≤d）。
- **节点约束**：
  - Multi-Dev：至少一个核心节点为 Development；叶/辅助节点可变为 **Empty-Function**（仅签名）。
  - Multi-BugFix：全部节点为 BugFix，禁止混入 Development（贴合真实调试场景）。
  - Multi-TDD：至少一个核心节点为 TDD，其余为 Development 或 Empty-Function。
- **有效性验证**：验证 G′ 为有效调用层级（根可达所有叶），且单测执行轨迹经过每个 Empty-Function 节点，防止规格不足。
- **Difficult 子集**：ν=∞ 且 |V(G′)|≥3，用于探测模型推理上限。

### 2.5 评测指标与协议
- **预生成执行（retest）**：在模型推理前先在掩码/注入 bug 的代码上跑测试，确认测试确实失败，剔除“掩码后仍通过”的无效任务。
- **AC@1**：生成解通过全部单测的比例。
- **AC Rate**（细粒度）：`AC Rate = (N_pass − N_retest) / (N_total − N_retest)`，严格衡量模型对“原本失败测试”的修复贡献。

---

## 3. 实验设计

### 3.1 数据集 / Benchmark
- **CoreCodeBench**：12 个 Python 仓库共 **1,524 个问题**。

| 类别 | 任务类型 | 平均函数数 | 平均代码行 | 题目数 |
|---|---|---|---|---|
| 原子 | Development | 1.00 | 17.00 | 511 |
| 原子 | BugFix | 1.00 | 38.00 | 315 |
| 原子 | TDD | 1.00 | 14.00 | 278 |
| 复合 | Multi-Dev | 3.85 | 53.92 | 167 |
| 复合 | Multi-BugFix | 2.00 | 62.34 | 10 |
| 复合 | Multi-TDD | 4.07 | 67.30 | 152 |
| 复合 | Difficult | 4.75 | 65.66 | 91 |

### 3.2 对比模型
- **9 个主模型**：GPT-5.2、Claude-4.5-Opus、Gemini-3-Pro、Doubao-Seed1.6（闭源 API）；Kimi-K2、DeepSeek-V3.2、Qwen3-Coder-480B-A3B-Instruct、GLM-4.6、MiniMax-M2（开源）。
- **扩展 3 个**（用于相关性分析，共 12 个）：Claude-3.7-Sonnet、Qwen3-Max-Instruct、Llama-3.1。
- 全部采用 **zero-shot、greedy decoding（temperature=0, top_p=1.0）**。

### 3.3 外部基准对比
- 与 **8 个外部基准**计算 Spearman 相关性并做层次聚类：HumanEvalPlus、MBPP-Plus、MultiPL-E、NL4Code、LiveCodeBench、BigCodeBench、FullStackBench、SWE-bench。

### 3.4 辅助验证实验
- **人工检查**：360 个 Development 问题（占 70.5%），三名专业标注员，IAA >95%。
- **微调验证**：Qwen3-8B 在 11 个仓库训练、1 个（skfolio）留出测试（983 训练 / 121 测试）。
- **鲁棒性**：生成器敏感性（4 个 backbone）、IG 过滤消融、提示词改写稳定性（MAPD vs 置信区间）、上下文长度 Kendall τ、依赖深度 d=2 vs d=3。

---

## 4. 资源与算力

- **微调实验（附录 M）**：
  - 模型：Qwen3-8B，全参数 SFT，**DeepSpeed ZeRO-3**，BFloat16。
  - 硬件：**8 块 GPU**，per-device batch size = 1，梯度累积 4，全局 batch size = 32。
  - 优化器：AdamW，峰值学习率 1.0×10⁻⁵，余弦衰减；最大序列长度 **32,768 tokens**。
- **评测环境（附录 J.3）**：Docker 容器隔离，标准 **CPU 实例（4 vCPU、16GB RAM）**，每次测试执行超时 120 秒；开源模型用 vLLM 推理。
- **未明确说明**：论文**未给出总 GPU 小时数、训练总时长、总算力预算**，也未说明生成阶段（GPT-4o/Claude 等 API 调用）的规模与成本。因此算力透明度有限。

---

## 5. 实验数量与充分性

### 实验规模（约 15+ 组）
- 原子任务主榜（表 2）、复合任务主榜（表 3）；
- 任务相关性矩阵（图 3）、任务间 IoU 错位分析（图 4）；
- 难度缩放：掩码长度（图 5a）、任务数量 ν（图 5b）、Difficult 子集（图 6）、依赖深度 d（表 7）；
- 与 8 个外部基准的相关性热图与层次聚类（图 7）；
- 生成器敏感性（附录 B，ρ=1.0）、IG 过滤消融（附录 C，表 5）、提示词改写稳定性（附录 I，表 6）、上下文长度独立性（图 11）；
- 微调验证（表 10）、置信区间（表 11/12）、逐仓库细分（表 13）、人工检查（附录 K）、TDD 定性验证（附录 E）、Difficult 有效性验证（附录 L）。

### 充分性评估
- **充分性较高**：覆盖多维度（相关性、难度、外部效度、鲁棒性、微调监督质量），并给出置信区间与逐仓库稳定性（Spearman ρ≥0.85）。
- **客观性**：采用 retest 预筛、AC Rate 扣除已有通过测试、双标注员 + IAA>95%、生成器 backbone 交叉验证，降低了单点偏差。
- **公平性**：统一 zero-shot、greedy decoding、统一 Docker 环境与超时，模型间可比性较好。
- **但需注意**：Multi-BugFix 仅 10 例，统计功效弱，作者也承认应“indicative”解读；部分结论（如 Difficult 子集低分）依赖小样本。

---

## 6. 主要结论与发现

- **能力错位普遍存在**：模型在 Development / BugFix / TDD 间排名显著漂移（如 Kimi-K2 Dev 强但 BugFix/TDD 弱，差距 >35%）；IoU 分析显示即使最强模型（Claude-4.5、Gemini-3-Pro）任务

间 IoU 也仅处于中低水平（多数任务对低于 0.5），表明三类任务捕捉的是**互补而非冗余**的能力维度；模型在某一任务上的高分不能外推为整体编码能力。
- **外部基准相关性呈“中等且分化”**：CoreCodeBench 与 HumanEvalPlus、MBPP-Plus 等函数级基准相关性偏弱，与 SWE-bench、BigCodeBench 等仓库级基准相关性中等偏强；层次聚类中 CoreCodeBench 自成一簇或与仓库级基准邻近，说明它提供了现有基准**未覆盖的独立信号**，而非又一个“同质排行榜”。
- **难度调节机制有效且单调**：随掩码长度增加、任务数量 ν 增大、依赖深度 d 从 2 升至 3，模型通过率呈**单调下降**；Difficult 子集（ν=∞、|V(G′)|≥3）上所有模型分数显著低于原子任务，揭示当前模型在**多函数长程推理**上的上限，且模型间差距在该子集被放大，区分度更高。
- **监督信号具下游价值**：Qwen3-8B 在 11 个仓库上微调后，在留出仓库 skfolio 上相对基座模型有稳定提升，说明 CoreCodeBench 生成的任务不仅是“考题”，也可作为**高质量训练数据**，反向验证了任务语义的有效性。
- **生成器与提示词鲁棒**：更换 4 个生成 backbone 后模型排名 Spearman ρ=1.0；提示词改写下 MAPD 落在置信区间内；上下文长度变化仅带来 Kendall τ 的小幅波动。这表明**结论对流水线实现细节不敏感**，基准具有可复现性。
- **IG 过滤器贡献可量化**：消融显示引入 Information Gain 过滤后，Development 任务的可解性与描述充分性均提升，验证了“用执行反馈筛选任务描述”这一设计的必要性。
- **逐仓库稳定性良好**：各仓库子集上的模型排名 Spearman ρ≥0.85，说明结论并非由个别仓库的偶然分布驱动。

---

## 7. 局限性

- **类别不均衡**：Multi-BugFix 仅 10 例，统计功效弱，相关结论只能作“indicative”解读；Difficult 子集 91 例，虽具区分度但样本仍偏小，置信区间较宽。
- **语言与领域覆盖有限**：仅覆盖 12 个 Python 仓库，未涉及 Java/Go/JS 等多语言，也未覆盖前端、嵌入式、并发/分布式等特殊领域；跨仓库、多文件级任务尚未纳入。
- **任务生成依赖 LLM**：尽管有 IG 过滤、retest 预筛与人工抽检（360 例、IAA>95%），人工检查主要覆盖 Development（70.5%），BugFix/TDD 的语义正确性更多依赖自动化验证，仍可能存在生成偏差或“测试通过但语义欠佳”的残余风险。
- **测试质量继承自原仓库**：任务有效性以原仓库单测为准，若上游测试覆盖不足或存在脆弱测试，会影响任务筛选与 AC Rate 的可靠性。
- **动态性为“半动态”**：虽支持难度调节与流水线复用，但论文实验基于固定仓库快照；要真正成为“移动靶”，仍需持续接入新仓库与新版本，论文未给出长期更新机制与污染监测方案。
- **评测协议单一**：统一 greedy decoding、单次采样，未报告 pass@k 或温度采样下的多样性表现，可能低估模型在多次尝试下的实际能力。
- **算力与成本透明度不足**：未披露生成阶段 API 调用规模、总 token 成本与训练总 GPU 小时，影响他人复现与成本评估。
- **能力维度仍不完整**：聚焦 Development/BugFix/TDD 三类认知需求，未覆盖代码审查、重构、性能优化、安全修复等真实工程维度。

---

## 8. 对研究的启发与意义

- **评测范式层面**：提出“**同一代码上下文、原子化隔离认知维度**”的设计，为仓库级基准从“单一通过率”走向“**能力剖面诊断**”提供了可复制的模板；其“预生成执行 + AC Rate 扣除已通过测试”的协议，可推广到其他需要排除“伪修复”的评测场景。
- **基准可持续性层面**：CorePipe 的“上下文抽取 → 原子任务生成 → 复合任务扩展”三阶段流水线，把基准构建从“人工标注一次性投入”转为“**可配置、可扩展的自动化生产**”，并通过掩码长度、ν、d 等超参数实现难度连续调节，为缓解数据污染与性能饱和提供了工程路径。
- **任务合成方法层面**：级联“大模型设计逻辑错误 + 小模型实现”的 BugFix 合成策略、基于调用树的连通子图采样、Empty-Function 节点与执行轨迹校验，均可迁移到其他语言的基准构建与课程学习数据生成。
- **模型研发层面**：能力错位现象提示训练数据配比与后训练策略应**按认知维度分别评估与补强**，尤其 TDD 与 BugFix 可能是当前模型的系统性短板；微调验证则说明此类基准可反哺小模型能力提升。
- **实践应用层面**：细粒度任务画像可用于团队选型（按任务类型匹配模型）、CI 中的回归门禁设计，以及面向新模型发布前的**快速能力体检**。

---

## 9. 一句话总结

CoreCodeBench 以“同上下文原子化任务 + 自动化可扩展流水线 + 严格 AC Rate 协议”，将仓库级代码评测从单一通过率推进到**可诊断、可调难度、可持续更新**的细粒度能力画像，并用系统性实验证明了模型在 Development/BugFix/TDD 间的显著能力错位与基准的独立外部效度。

（完）
