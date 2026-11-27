---
title: "PerfCoder: Large Language Models for Interpretable Code Performance Optimization"
title_zh: PerfCoder：面向可解释代码性能优化的大语言模型
authors: "Jiuding Yang, Shengyao Lu, Hongxuan Liu, Shayan Shirahmad Gale Bagi, Zahra Fazel, Tomasz Czajkowski, Di Niu"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://aclanthology.org/2026.findings-acl.675.pdf"
tags: ["query:ai-se"]
score: 8.0
evidence: 大模型生成可解释的高性能代码
tldr: 大模型在自动代码生成上进步显著，但生成高性能代码能力有限，根源在于缺乏引导可解释性能优化的监督。PerfCoder基于带人类可读注释的真实优化轨迹微调，并利用运行时反馈进行强化对齐，使其能产出可解释且性能更优的代码。实验显示其在代码性能优化上效果显著，拓展了大模型在软件工程代码生成中的应用。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl675/fig-001.webp\", \"caption\": \"\", \"page\": 2, \"index\": 1, \"width\": 1767, \"height\": 467}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl675/fig-002.webp\", \"caption\": \"\", \"page\": 4, \"index\": 2, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl675/fig-003.webp\", \"caption\": \"\", \"page\": 4, \"index\": 3, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl675/fig-004.webp\", \"caption\": \"\", \"page\": 4, \"index\": 4, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl675/fig-005.webp\", \"caption\": \"\", \"page\": 4, \"index\": 5, \"width\": 3840, \"height\": 3840}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl675/fig-006.webp\", \"caption\": \"\", \"page\": 4, \"index\": 6, \"width\": 512, \"height\": 512}]"
motivation: 大模型能生成代码但难以产出高性能代码，缺乏可解释优化的监督信号。
method: 用带注释的真实优化轨迹微调，并以运行时反馈进行强化对齐训练。
result: 模型可生成可解释且性能更优的代码，超越单纯正确性目标。
conclusion: 为面向性能优化的代码生成提供了可解释的监督与对齐方法。
---

## Abstract
Large language models (LLMs) have achieved remarkable progress in automatic code generation, yet their ability to produce high-performance code remains limited, despite its importance in real-world software systems. We argue that this limitation stems not only from data scarcity, but more fundamentally from the lack of supervision that guides interpretable and effective performance improvements. We introduce PerfCoder, a family of LLMs designed to generate performance-enhanced code through interpretable and customized optimization strategies. PerfCoder is fine-tuned on curated real-world optimization trajectories with human-readable annotations and further aligned via reinforcement fine-tuning using runtime feedback, enabling it to generate input-specific strategies and apply them directly without iterative refinement. On the PIE code performance benchmark, PerfCoder outperforms all existing models in both runtime speedup and effective optimization rate, demonstrating that code performance optimization requires strategy awareness rather than scale alone. Moreover, PerfCoder produces interpretable feedback that can guide larger LLMs in a planner–optimizer workflow, substantially improving the performance of 32B models and GPT-5 on code optimization.

---

## 论文详细总结（自动生成）

# PerfCoder 论文结构化总结

## 1. 核心问题与整体含义

- **研究背景**：以 Codex、GPT-4/5、Code Llama 为代表的 LLM 在自动代码生成上进步显著，但生成的代码在运行时性能上普遍不佳，难以满足实际软件系统对延迟、吞吐和可扩展性的要求。
- **核心问题**：作者认为，LLM 生成高性能代码能力不足的根源**不仅在于高质量数据稀缺**，更在于**缺乏引导“可解释且有效”性能改进的监督信号**。现有模型即便见到更优解，也往往只能做不透明的试错式启发式修改，无法解释或证明其代码改动的合理性。
- **研究含义**：论文将“代码性能优化”重新定义为一个**策略感知（strategy awareness）** 任务，主张性能优化能力并非单纯依赖模型规模，而是需要显式的优化策略建模与监督。目标是让模型能生成**人类可读、可定制、可迁移**的优化策略，并直接应用于给定代码。

## 2. 方法论

### 2.1 总体框架
- **PerfCoder** 是一个经过微调的 LLM 系列，通过**两阶段**训练获得能力：
  1. **监督微调（SFT）** → 得到 *PerfCoder Jr.*，可在**单步**内同时生成“优化策略 + 优化后代码”。
  2. **强化微调（GRPO）** → 将模型训练为**规划器（planner）**，在“规划器–优化器”协作框架下生成策略，引导外部冻结的更大模型完成优化。

### 2.2 单步优化模式与 SFT
- **结构化输出序列**：引入控制 token `[SUGG/] … [/SUGG] [OPT/] … [/OPT]`，模型一次性自回归生成：
  - 策略集合 `s = {s1,…,sk}`，每条策略为元组 `(name_i, desc_i)`；
  - `name_i` 取自**固定的 15 个规范优化类别**（如算法设计优化、循环效率技术、I/O 吞吐优化等）；
  - `desc_i` 为针对输入代码的上下文相关解释（“为什么这样改能提速”）。
- **训练目标**：标准因果语言建模损失（逐 token 交叉熵）。
- **双推理模式**：
  - *plan+code*：继续解码到 `[OPT/]` 段，直接输出优化代码；
  - *plan-only*：在 `[/SUGG]` 处停止，仅输出可解释策略，用于引导外部更大模型。

### 2.3 自动化策略合成
- 使用**32B 开源指令微调模型**作为提取器 `fθ`，对每个慢–快代码对自动生成策略：
  `s(u,p) = fθ(x_slow, x_fast)`。
- 先直接抽取，再进行**去重 + 归类**（人工检查 1000 个名称构建 15 类分类体系，其余自动分类），超过 90.27% 的策略可对齐到定义类别。
- 这种“类别（what）+ 上下文解释（why）”的分离设计带来**结构正则化**，防止高频浅层技巧主导训练，并保留长尾策略。

### 2.4 数据集重建与平衡采样
- 基于原始 PIE 数据集（77,967 对）重建：
  - **最终提交过滤**：只保留用户最后一次提交作为优化目标，明确优化端点；
  - **全局最优替换**：若最终提交运行时间 `T(final) > 2·T(best)`，则替换为问题级全局最优解；
  - 重建后得到 **D_ref = 30,649 对**（其中 12,350 对跨用户）。
- **平衡策略采样**：为每对计算稀有度加权分数 `S = (1/k) Σ 1/f(si)`，按分数排序后**轮询采样**，得到 **D_b = 5,000 对**平衡子集，提升长尾策略（如多线程、缓存局部性）的占比。

### 2.5 GRPO 强化微调（规划器模式）
- 小型 PerfCoder 作为**规划器**仅输出策略；**冻结的大型外部模型**作为优化器依据策略生成代码。
- **奖励设计**（基于实测运行时间与加速比 `Δ = T_slow / T_gen`）：
  - 无法编译：`-ω`（ω=100，严重惩罚）；
  - `Δ < 1`（变慢）：`-1`；
  - `Δ ≥ 1`（提速）：`Δ²`（二次奖励，鼓励显著提速）。
- 每个输入采样一组（如 4 个）策略，分别引导优化器生成代码并计算奖励，按**组内相对优势** `A_i = (R(si) − μ_R)/σ_R` 计算优势，采用带裁剪和 KL 正则的 GRPO 目标优化规划器策略。
- 仅微调规划器、冻结优化器，使奖励信号**精准作用于策略生成能力**，而非指令跟随能力。

## 3. 实验设计

- **主 Benchmark**：**PIE**（978 个未优化 C++ 程序，来自 41 道竞赛编程题），遵循 PIE 官方评估协议，使用 **gem5 模拟器**做确定性运行时测量。
- **评估指标**：
  - **Speedup**（加速比，主指标）；
  - **Effective Optimization rate**（正确且 ≥1.1× 提速的比例）；
  - **Code Accuracy**（通过全部功能测试的比例）。
- **对比方法**（覆盖多种规模与类型）：
  - 通用大模型：GPT-4、GPT-5、Qwen2.5-Inst-32B、Qwen2.5-Coder-Inst-32B、DeepSeek-R1-Distill-Qwen-32B；
  - 小模型：CodeLlama-Inst-7B、Olympic-Coder-7B；
  - 在 PIE 高质量子集上微调的基线：PIE-CodeLlama-HQ、PIE-Qwen2.5-Coder-HQ；
  - 迭代式方法：**Effi-Learner**（32B，五轮；作者将其 Python profiler 替换为 gcov 与端到端运行时以适配 C++，并区分 w/ 与 w/o history）。
- **推理设置**：单步（直接生成优化代码）与两步（先策略后代码）；两步又分“模型自生成策略”与“PerfCoder 提供策略”两种配置。
- **迁移实验**：额外在 **PolyBenchC**（30 个循环密集型数值内核）上构建辅助 benchmark，22 个内核训练、8 个测试，验证跨领域迁移性。

## 4. 资源与算力

- 论文在附录 A 中明确说明：
  - 所有实验在**单节点 4× NVIDIA V100 32GB GPU** 上完成；
  - **GRPO 训练额外需要 8× NVIDIA V100 32GB GPU**；
  - 微调设置：2 个 epoch、batch size 64、学习率 2×10⁻⁵，遵循 PIE 论文协议；
  - 解码采用**贪心搜索**；
  - GRPO：1 个 epoch、每样本 4 次生成，优化器使用 Qwen-2.5-32B-Inst；
  - PolyBenchC 迁移实验：1 个 epoch、学习率 1×10⁻⁵、batch size 4。
- **说明**：论文**未报告具体训练时长（GPU 小时数）**，仅给出硬件配置与超参数；也未披露 GPT-5 等闭源模型的调用成本。

## 5. 实验数量与充分性

- **实验组数概览**：
  - 主表（Table 2）覆盖 **约 17 个模型/配置**，横跨单步、两步、GRPO、五轮迭代等多种设置；
  - **消融实验（Table 3）**：去掉策略监督（w/o Strategy）、去掉类别平衡（w/o Balancing），共 3 组对比；
  - **迁移实验（Table 5）**：PolyBenchC 上 4 个模型对比；
  - **案例研究（附录 G）**：展示 PerfCoder-QC、Qwen2.5-32B、PerfCoder+Qwen 引导下的真实优化案例与策略对比。
- **充分性评价**：
  - **较充分**：主实验覆盖面广（小模型、大模型、闭源模型、专用微调基线、迭代式方法），并做了关键组件消融与跨数据集迁移验证；
  - **公平性**：使用官方 PIE Docker 与评估脚本，保证运行时测量与先前工作可比；对 Effi-Learner 做了 C++ 适配以保证公平对比；对 PIE-HQ 基线在同一协议下复现；
  - **仍需注意**：消融维度较有限（仅两个组件），未系统分析策略数量、采样规模、GRPO 组大小等超参数敏感性；PolyBenchC 实验规模较小（8 个测试内核）。

## 6. 主要结论与发现

1. **单步性能 SOTA**：PerfCoder-QC-7B 取得 **2.50× 加速比、33.13% 有效优化率**，超过 PIE-Qwen2.5-Coder-HQ（1.98×）、32B 的 Effi-Learner（1.54×），甚至在加速比上超过 GPT-4（1.32×）与 GPT-5（1.96×），说明**策略感知监督可超越模型规模与专有预训练**。
2. **策略可迁移**：用 PerfCoder 策略引导 Qwen2.5-Inst-32B，加速比从 1.32× 提升到 **2.52×**，有效优化率从 20.76% 提升到 43.56%，证明策略具有高度可迁移性与可解释指导价值。
3. **强规划能力不依赖大模型**：1.5B 的 PerfCoder 经 1 个 epoch GRPO 即可引导 32B 模型达到 **3.03×** 加速比，引导 GPT-5 达到 **4.82×**（GPT-5 单独仅 1.96×）。
4. **无监督策略生成可能有害**：让通用大模型自行生成并遵循策略，性能反而下降（Qwen2.5-Inst 1.32×、Qwen2.5-Coder-Inst 1.38×），说明**策略监督不可或缺**，缺乏优化的通用模型易产生模糊甚至误导性策略。
5. **正确性 ≠ 优化性**：Qwen2.5-Inst 代码准确率最高（80.37%）但有效优化率仅 20.76%；PerfCoder 准确率 43.46% 却有 33.13% 有效优化率，说明**有效优化率是比纯正确性更实用的指标**。
6. **消融结论**：去掉策略监督（2.11×）或去掉类别平衡（2.09×）均导致性能下降，验证了**策略感知学习**与**平衡数据整理**两个组件的必要性。

## 7. 优点

- **可解释性强**：策略以“规范类别 + 上下文解释”的结构化形式输出，兼顾可读性与可复用性，便于人工审查与教学场景。
- **单步高效**：无需迭代自反思或多轮调用，一次前向即可同时产出策略与代码，显著降低推理成本。
- **灵活的双模式设计**：同一模型可作独立优化器（plan+code）或轻量规划器（plan-only），支持“即插即用”地引导 GPT-5 等闭源大模型。
- **数据工程细致**：通过最终提交过滤、全局最优替换、稀有度加权轮询采样，系统性地缓解数据噪声与策略长尾失衡问题。
- **规划器/优化器解耦的 RL 设计**：GRPO 仅微调小规划器、冻结优化器，使运行时奖励精准对齐“策略生成”这一缺失能力，避免把奖励浪费在指令跟随上。
- **评估严谨**：采用官方 PIE Docker 与 gem5 模拟器，保证确定性与可复现性；对 Effi-Learner 做 C++ 适配，提升对比公平性。
- **小模型大作用**：1.5B 规划器即可显著提升 32B 模型与 GPT-5，具有较高实用价值与部署友好性。

## 8. 不足与局限

- **领域与语言覆盖有限**：主实验仅限 **C++ 竞赛编程（PIE）** 与少量 **PolyBenchC 数值内核**，未验证 Python、Java 等语言或真实工业代码库、系统级软件等场景。
- **基础模型规模受限**：受算力约束，未在更大/更强的基础模型上评估；作者也承认更强基座可能进一步提升策略质量与优化效果。
- **依赖 32B 提取器**：策略监督依赖一个 32B 开源指令模型做自动抽取，提取器本身的偏差与能力上限会传导到训练数据。
- **RL 训练规模较小

- **RL 训练规模较小**：GRPO 仅训练 1 个 epoch、每样本采样 4 条策略，规划器对策略空间的探索相对有限；奖励函数也较粗粒度（仅区分“无法编译 / 变慢 / 提速”三档），未针对不同优化类别的难度差异做归一化，也未在奖励中显式纳入正确性以外的质量信号。
- **奖励信号维度单一**：奖励完全基于实测加速比，未建模内存占用、功耗、代码可读性/可维护性等工程关注点；对加速比接近 1 的样本，二次奖励与线性惩罚之间的梯度过渡可能不够平滑，存在策略学习不稳定的风险。
- **代码正确率偏低**：PerfCoder-QC-7B 的代码准确率仅 43.46%，显著低于通用大模型（如 Qwen2.5-Inst 的 80.37%），说明策略驱动的激进优化可能以牺牲功能正确性为代价；实际部署时仍需额外的测试验证或自动修复环节兜底。
- **策略类别体系依赖人工构建**：15 类规范体系由人工检查约 1000 个策略名称归纳而来，虽然后续分类自动化，但类别粒度与覆盖度受构建者主观判断影响，且未必能直接迁移到其他语言或领域。
- **基准的竞赛编程偏向**：PIE 源自竞赛编程题，程序规模小、逻辑封闭、依赖少，与真实工业代码库（长调用链、框架依赖、并发与 I/O 密集）差异明显，结论外推需谨慎。
- **对比基线不完全对等**：GPT-4/GPT-5 等闭源模型未针对 PIE 微调，其提示设计、解码配置与迭代预算可能与 PerfCoder 不完全一致；Effi-Learner 的 C++ 适配虽已尽量公平，但 profiler 提供的信息量与迭代轮次仍可能引入偏差。
- **缺少统计显著性分析**：论文未报告多次运行的方差、置信区间或显著性检验；gem5 虽保证运行时确定性，但 GRPO 采样与数据子集选择带来的波动对结论稳定性的影响未被量化。
- **成本与效率指标缺失**：未报告训练 GPU 小时数、推理延迟/吞吐、token 消耗等实用性指标，难以评估“小规划器 + 大优化器”方案在真实部署中的性价比，尤其是引导 GPT-5 时的调用开销。

## 9. 启示与可拓展方向

- **“策略即监督”的范式价值**：论文表明，将“如何优化”显式建模为可解释策略，比单纯扩充数据或增大模型更能提升高性能代码生成能力；该思路可迁移至 bug 修复、代码重构、并行化、内存优化等其他代码变换任务。
- **小规划器 + 大优化器的协作架构**：解耦的 planner–optimizer 设计让弱模型负责“想策略”、强模型负责“写代码”，是一种高性价比的能力组合方式，适合在闭源强模型之上叠加领域专精层，也便于策略的人工审查与干预。
- **数据重建的普遍意义**：最终提交过滤与全局最优替换揭示了原始数据中“优化端点不明确”的噪声问题，提示同类研究需重视数据标注的语义一致性与优化目标的可界定性。
- **可拓展方向**：扩展到 Python/Java 等多语言与真实代码库；引入更细粒度、多目标的奖励（正确性、内存、可读性联合建模）；将策略库做成可检索、可组合的模块以支持复杂多阶段优化；结合静态分析与 profiler 信号增强策略生成的“接地性”（grounding），减少模糊或误导性策略。

## 10. 总体评价

PerfCoder 是一篇问题定义清晰、方法设计精巧、实验较为扎实的工作。其核心贡献在于**将代码性能优化从“黑箱试错”重构为“可解释策略生成”**，并通过 SFT + GRPO 的两阶段训练与 planner–optimizer 解耦架构，证明了小模型也能产出高质量、可迁移的优化策略。实验在 PIE 上取得 SOTA 加速比，并通过迁移实验与消融验证了策略监督与数据平衡两个组件的必要性。主要不足在于领域覆盖较窄（C++ 竞赛编程为主）、代码正确率偏低、RL 训练规模与奖励设计较简单，且缺少成本核算与统计显著性分析。总体而言，该工作为“策略感知的代码优化”提供了有说服力的实证基础与可复用的方法论框架，对后续“可解释 + 可迁移”的代码性能优化研究具有较强参考价值。

（完）
