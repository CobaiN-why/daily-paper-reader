---
title: "CollabCoder: Plan-Code Co-Evolution via Collaborative Decision-Making for Efficient Code Generation"
title_zh: CollabCoder：通过协同决策实现高效代码生成的计划-代码协同演化
authors: "Duy Tung Doan, Quang Huy Phung, Dzung Nguyen, Khac-Hoai Nam Bui"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://aclanthology.org/2026.findings-acl.1393.pdf"
tags: ["query:ai-se"]
score: 9.0
evidence: 面向自动代码生成的多智能体计划-代码协同框架
tldr: 传统多智能体代码生成框架受限于静态规划、孤立执行与高计算开销，难以适应复杂任务。本文提出 CollabCoder，一个计划-代码协同演化框架，通过计划模块与代码模块之间的协同决策来确定调试阶段由哪个模块执行。在多个常用基准上的实验表明，该方法持续提升代码质量与鲁棒性，为自动化代码生成提供了更灵活高效的协作范式。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1393/fig-001.webp\", \"caption\": \"\", \"page\": 1, \"index\": 1, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1393/fig-002.webp\", \"caption\": \"\", \"page\": 1, \"index\": 2, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1393/fig-003.webp\", \"caption\": \"\", \"page\": 1, \"index\": 3, \"width\": 1200, \"height\": 800}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1393/fig-004.webp\", \"caption\": \"\", \"page\": 1, \"index\": 4, \"width\": 1200, \"height\": 800}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1393/fig-005.webp\", \"caption\": \"\", \"page\": 1, \"index\": 5, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1393/fig-006.webp\", \"caption\": \"\", \"page\": 8, \"index\": 6, \"width\": 2379, \"height\": 780}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1393/fig-007.webp\", \"caption\": \"\", \"page\": 8, \"index\": 7, \"width\": 567, \"height\": 455}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1393/fig-008.webp\", \"caption\": \"\", \"page\": 16, \"index\": 8, \"width\": 740, \"height\": 490}]"
motivation: 传统多智能体代码生成框架存在静态规划、执行孤立与开销高等问题。
method: 设计计划模块与代码模块的协同决策机制，实现计划-代码的动态协同演化。
result: 在多个基准上持续提升生成代码的质量与鲁棒性。
conclusion: 动态协同决策为多智能体自动代码生成提供了更高效的范式。
---

## Abstract
Automated code generation remains a persistent challenge in software engineering, as conventional multi-agent frameworks are often constrained by static planning, isolated execution, high computational overhead, and limited adaptability to complex tasks. This paper introduces CollabCoder, a novel Plan-Code Co-Evolution framework that improves code generation through dynamic multi-agent collaboration. The core idea is to design a collaborative decision-making process between the plan module and the code module to decide which module should be executed for the debugging process. Extensive experiments on widely used benchmarks demonstrate that CollabCoder consistently improves code quality and robustness across tasks. Importantly, CollabCoder achieves performance comparable to or exceeding current state-of-the-art methods while reducing computational overhead, with efficiency gains becoming more pronounced as benchmark difficulty increases. On the more challenging LiveCodeBench and xCodeEval benchmarks, our approach improves performance by 11-20% over strong baselines while reducing the number of API calls by an average of 4-10 per execution.

---

## 论文详细总结（自动生成）

# CollabCoder 论文结构化总结

## 1. 核心问题与研究动机

- **背景**：LLM 已能实现端到端代码生成，但复杂需求下的正确性仍是难题。主流做法是“先规划后编码”（plan-before-code）的双阶段范式：先由规划生成代码，再对结果进行调试/精炼。
- **现有方法的两个根本缺陷**：
  - **调试是反应式的**：仅依据错误日志做浅层修补，缺乏上下文学习与显式错误归因，导致修订重复、边际收益低，无法定位根因或复用失败经验。
  - **规划是静态的**：整个调试过程中计划固定不变，不随代码修订与中间反馈更新，规划器与调试器无法共同适应，只能在“错误计划”下反复改代码。
- **整体含义**：论文主张代码生成的瓶颈不只是“写对代码”，而是**计划层错误与实现层错误难以区分**；因此需要让“计划”和“代码”在迭代中协同演化，并在每轮显式决定“该改计划还是改代码”，从而同时提升准确率与推理效率。
- **效率动机**：MapCoder、CodeSIM 等智能体框架的推理复杂度约为 O(nk)（计划探索数 × 调试轮数），在初始计划错误时会大量浪费 API 调用；CollabCoder 希望把复杂度降为仅依赖精炼迭代次数。

## 2. 方法论

### 2.1 总体架构

- 框架由三个智能体构成：规划智能体 A_plan、编码智能体 A_code、调试智能体 A_debug，即 CollabCoder = ⟨A_plan, A_code, A_debug⟩。
- 调试智能体被重构为两个模块：**协同决策模块（CDM）** 与 **推理轨迹模块（RT）**，即 A_debug = ⟨A_CDM, A_RT⟩。
- 输入：问题描述 P、编码模板 T、Q 个测试用例 {(x_i, y_i)}、执行 oracle O。
- 第 t 轮维护计划 π(t) 与可执行程序 c(t)；执行后把失败用例汇总为失败日志 F(t)；循环直至全部通过或迭代预算耗尽。

### 2.2 协同决策模块（CDM）

- **分析阶段**：一次 LLM 调用同时产出三类诊断：
  - 计划级分析 E_π：判断计划中的算法推理是否与观测失败一致，定位计划层根因；
  - 代码级分析 E_c：在假定计划正确的前提下诊断实现错误；
  - 计划-代码对齐分析 E_align：评估计划语义与代码实现之间的一致性，捕捉“计划对但实现错/不全”的情形。
- **决策阶段**：决策空间 D = {0, 1}，0 表示更新计划，1 表示更新代码。通过共识函数 F_cons 聚合三路分析，参数为固定信任权重 W_trust = {w_π, w_c, w_align}，满足 Σw_i = 1。
- **决策公式（文字版）**：在决策空间上取最大化聚合得分，每路分析的贡献 = 权重 × 该分析对决策 d 的置信度 φ × 其余分析对同一决策的一致性 ϕ；置信度与一致性分数在一次 LLM 调用中联合给出，取值均在 [0,1]。
- **默认超参**：w_π = 0.4，w_c = 0.3，w_align = 0.3（略偏向计划层），迭代上限 t = 5。

### 2.3 推理轨迹模块（RT）

- 维护一个跨轮持久的推理状态 R(t)，记录历史调试洞见与精炼模式，实现“从错误中学习”。
- **状态更新**：R(t) = A_RT(R(t−1), E_X(t), P, X(t), F(t))，其中 X(t) 为本轮被选中的精炼目标（由 CDM 决定是 π(t) 还是 c(t)），E_X(t) 为对应诊断。
- **精炼更新**：X(t+1) = A_X(X(t), P, R(t), T(t), F(t))，算子 A_X ∈ {A_plan, A_code} 由决策 D(t) 选择；编码模板 T 仅在“改代码”分支注入，保证结构约束，计划精炼则与模板无关。
- **作用**：显式建模调试为有状态推理过程，突出复发错误模式、修正启发式、避免重复无效修复，提升收敛稳定性。

### 2.4 算法流程（伪代码要点）

1. 初始化 R(0)=∅，生成初始计划 π(0)，再据其生成初始代码 c(0)；
2. 执行 c(t) 得失败日志 F(t)，若全部通过则返回；
3. CDM 产出三路分析，再打分得到决策 D(t)；
4. 依据 D(t) 选定目标 X(t)，更新推理轨迹 R(t+1)；
5. 若改计划：重写 π(t+1) 并由新计划重新生成代码；若改代码：计划不变，对现有代码做补丁式精炼；
6. 循环至预算耗尽，返回最终代码。

## 3. 实验设计

- **数据集 / 场景**：
  - 基础：HumanEval（164 题）、MBPP（397 题），以及加严测试的扩展版 HumanEval-ET、MBPP-ET；
  - 竞赛级：LiveCodeBench（v6，仅保留 112 道 stdin/stdout 题）、xCodeEval。
- **评价指标**：零样本 Pass@1；效率指标为平均 Token 输入/输出（Token I/O）与每题 API 调用次数；另用计划/代码更新率（PU Rate、CU Rate）分析决策行为。
- **对比方法**：
  - 直接提示、CoT、Self-Planning、ThinkCoder（轻量方法）；
  - MapCoder、CodeSIM（强多智能体基线）；
  - 附录另比 Best-of-N 与 Reflexion 两类推理时自改进基线。
- **骨干模型**：Seed-Coder-8B、Qwen2.5-Coder-32B、GPT-4o mini；附录补充 GPT-5.2 与 Qwen3-Coder-Next（80B）。
- **公平性设置**：所有方法在相同骨干下评测；基线采用各自论文的最优预算配置（MapCoder/CodeSIM：k=5、n=5；ThinkCoder：k=1、n=20），CollabCoder 统一 t=5；结果在官方隐藏测试上执行得到，公开用例仅用于开发期调试。

## 4. 资源与算力

- 论文**未报告**任何训练算力信息（GPU 型号、数量、训练时长均无）。
- 该方法本身是**纯推理侧的智能体框架，不涉及模型训练或微调**，成本体现为 LLM API 调用：如 GPT-4o mini 上每题约 2993/1781 tokens、5.06 次调用；竞赛级基准上每题约 15156/4491 tokens、12.27 次调用。
- 因此“算力”实为推理开销，论文以 Token 与 API 调用次数间接刻画，但未给出硬件或货币成本估算。

## 5. 实验数量与充分性

- **实验组数概览**：
  - 主实验：3 个骨干 × 4 个数据集 × 6 种方法（表 1）；
  - 竞赛级实验：2 个基准 × 3 种方法（表 2，GPT-4o mini）；
  - 前沿骨干扩展：2 个模型 × 2 个基准 × 3 种方法（附录表 4）；
  - 消融：2 个骨干 × 4 个数据集 × 3 种配置（有/无 CDM、有/无 RT）；
  - 分析性实验：难度分层解题分布、精度-预算曲线（LCB 与 xCodeEval）、CDM 计划/代码更新率统计（3 骨干 × 3 数据集）、信任权重敏感性（12 组归一化配置，90 题子集）、与 Best-of-N / Reflexion 的预算对比（前 90 题）。
- **充分性评价**：覆盖面较广，从简单函数级到竞赛级、从 8B 开源模型到前沿闭源模型均有覆盖；消融、敏感性、难度分层、预算曲线形成了较完整的证据链。
- **客观与公平性**：统一骨干、统一预算约定、使用官方隐藏测试、报告效率指标，整体较为客观；但竞赛级主实验仅用 GPT-4o mini（作者以“弱模型性能普遍偏低、差异被掩盖”为由排除另两个骨干），且 LCB 仅取 112 题、部分分析仅用 90 题子集，规模偏小；信任权重为人工固定而非学习得到，存在一定调参空间。

## 6. 主要结论与发现

- **准确率全面提升**：平均 Pass@1 在三骨干上分别为 76.26 / 82.50 / 83.25，均优于 CodeSIM（75.51 / 80.22 / 81.52）与 MapCoder（68.78 / 79.84 / 77.80）。
- **难题优势更明显**：LCB 41.96%、xCodeEval 47.16%，较 MapCoder 高约 6.6–7.1 个点、较 CodeSIM 高 4.7–5.3 个点；难度分层显示随难度上升性能衰减更平缓（最难档 1600–1800 解出 7 题 vs MapCoder 3、CodeSIM 5）。
- **效率显著更优**：相比 MapCoder 总 token 降约 30–50%（竞赛级约 57%），相比 CodeSIM 降 10–25%（竞赛级约 42%）；API 调用从 22.41/17.16 降至 12.27。
- **消融结论**：去掉 CDM（退回“总是改代码”）性能下降最大，去掉 RT 次之，二者互补；模型越强，完整框架收益越明显。
- **CDM 行为规律**：数据集越难，更新触发率越高；代码专用模型以代码级更新为主（计划更新率约为代码的 1/2–1/3），通用模型 GPT-4o mini 反而以计划级更新为主，可解释为“跳出局部最优”。
- **自改进优于广度采样**：Best-of-N 很快饱和（32→33/90），Reflexion 停在 37/90，CollabCoder 随迭代稳步升至 44/90，说明收益来自结构化计划-代码协同，而非单纯增加预算。
- **权重鲁棒**：默认 (0.4, 0.3, 0.3) 与 (0.4, 0.2, 0.4) 并列最佳（48.9%），过度偏向代码级（如 0.1/0.8/0.1）性能降至 37.8%。

## 7. 优点

- **问题切分清晰**：把“该改计划还是改代码”显式建模为二值决策，直击静态规划与反应式调试两大痛点，动机与设计高度一致。
- **机制设计有新意**：三路互补诊断（计划/代码/对齐）+ 置信度×一致性的共识打分，比单纯看错误日志更细粒度；RT 把调试变成有状态推理，抑制重复无效修复。
- **效率与效果双赢**：在准确率不降反升的前提下显著减少 token 与 API 调用，且难度越高收益越大，具备实用价值。
- **实验较立体**：多骨干、多难度层级、消融、权重敏感性、与 Best-of-N/Reflexion 的预算对比，并给出逐轮案例（如 0-based/1-based 索引修复）佐证机制有效性。
- **可复现性好**：开源代码，附录给出完整伪代码与全部提示词模板，评测在官方隐藏测试上进行。
- **可扩展性验证**：在 GPT-5.2、Qwen3-Coder-Next 等前沿模型上仍保持最佳 Pass@1 与效率优势。

## 8. 不足与局限

-
