---
title: "Simplify-Pro: A Two-level and Progressive LLM-based Framework for Auto Long Text Simplification"
title_zh: Simplify-Pro：面向长文本自动简化的两级渐进式大模型框架
authors: "Peng Zhou, Guangxin Li, Xiaoying Huang, Yiming Tang"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://aclanthology.org/2026.findings-acl.1112.pdf"
tags: ["query:ai-se"]
score: 6.0
evidence: 基于大模型的长文本自动简化框架
tldr: 自动长文本简化需在简化效率与流畅性、语法正确性、语义完整性等细粒度质量间取得平衡，颇具挑战。作者提出Simplify-Pro，一种两级渐进式大模型框架，将段落级训练、简化生成、指标辅助分析与选择性精修整合为统一多阶段流水线。实验表明该框架在域内与域外场景均取得优越性能，为长文本简化提供了有效范式。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1112/fig-001.webp\", \"caption\": \"\", \"page\": 1, \"index\": 1, \"width\": 6204, \"height\": 4266}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1112/fig-002.webp\", \"caption\": \"\", \"page\": 3, \"index\": 2, \"width\": 7910, \"height\": 7386}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1112/fig-003.webp\", \"caption\": \"\", \"page\": 20, \"index\": 3, \"width\": 7998, \"height\": 7038}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1112/fig-004.webp\", \"caption\": \"\", \"page\": 21, \"index\": 4, \"width\": 6040, \"height\": 5882}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1112/fig-005.webp\", \"caption\": \"\", \"page\": 22, \"index\": 5, \"width\": 8028, \"height\": 7650}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1112/fig-006.webp\", \"caption\": \"\", \"page\": 23, \"index\": 6, \"width\": 6040, \"height\": 6325}]"
motivation: 自动长文本简化难以在简化效率与流畅性、语法正确性、语义完整性等细粒度质量之间取得平衡。
method: 提出两级渐进式大模型框架，整合段落级训练、简化生成、指标辅助分析与选择性精修的多阶段流水线。
result: 该框架在域内与域外多种测试场景下均取得优于基线的简化性能。
conclusion: Simplify-Pro为长文本自动简化建立了一种兼顾效率与细粒度质量的有效范式。
---

## Abstract
Text simplification plays a vital role in natural language processing, yet auto long text simplification remains challenging due to the difficulty in the joint balancing of simplification efficiency and fine-grained quality requirements, such as fluency, grammatical correctness and semantic completeness. To address these challenges, we propose Simplify-Pro, a two-level and progressive LLM-based framework that establishes an effective paradigm for automatic long text simplification under diverse test scenarios. By integrating paragraph-level training, simplification generation, metric-assisted analysis and selective refinement into a unified multi-stage pipeline, our framework achieves superior performance across in-domain and out-of-domain simplification tasks, which matches or even outperforms advanced and proprietary LLMs. Furthermore, comprehensive experiments and qualitative analyses cover the simplification performance, generalization ability and the contribution of each individual stage, demonstrating the effectiveness, robustness and modular design advantages of Simplify-Pro.

---

## 论文详细总结（自动生成）

# Simplify-Pro 论文结构化总结

## 1. 核心问题与研究背景

- **任务定位**：文本简化（Text Simplification）旨在提升复杂文本的可理解性，同时保留原意，对教育普及、阅读障碍人群可及性、专业领域理解等具有重要价值。
- **研究缺口**：现有研究多集中于**词汇级与句子级**简化，长文本级简化相对被忽视；而已有的长文本方法通常依赖**大规模高质量平行语料**。
- **核心痛点**：随着输入长度增加，简化错误更频繁、更明显，包括**关键信息丢失、语义扭曲、过渡不连贯**。因此，如何在**简化效率**与**流畅性、语法正确性、语义完整性**等细粒度质量要求之间取得联合平衡，是长文本简化的关键挑战（见论文 Figure 1）。
- **整体含义**：作者提出 Simplify-Pro，试图建立一种在段落级与文档级、域内与域外多种测试场景下都有效的长文本自动简化范式。

## 2. 方法论

### 2.1 核心思想
- 构建**两级（段落级 + 文档级）、渐进式**的 LLM 多阶段流水线，四个模块化阶段依次为：**段落级训练 → 简化生成 → 指标辅助分析 → 选择性精修**，各阶段渐进提升简化质量。

### 2.2 关键技术细节

**(1) 段落级训练（GRPO + 混合奖励）**
- 仅使用**有限段落级平行数据**，采用 **GRPO（Group Relative Policy Optimization）** 训练简化模型：对每个问题采样 G 个回答，用组内归一化奖励计算优势，最大化带 clip 的代理目标，并加 KL 正则约束偏离参考策略。
- **结构化输出与推理**：通过指令引导 prompt，要求模型在 `<think>` 与 `<answer>` 标签内分别输出推理过程与最终简化。
- **奖励设计**（总奖励 = 推理长度奖励 + 质量奖励 + 格式奖励）：
  - **格式验证奖励**：符合预设格式正奖励，否则惩罚。
  - **动态推理长度奖励 R_CoT**：当推理长度 L_CoT 低于下界 L_lower 或高于上界 L_upper 时按偏离程度比例惩罚，避免推理过短限制策略探索、过长引入优化噪声。
  - **质量奖励 R_quality**：由三部分组合——**SARI**（词法编辑操作 F1）、**BERTScore**（语义相似度）、**LENS**（人类偏好对齐，0–100 分）。按配置分为三种变体：
    - **RS**：仅 R_lex；
    - **RD**：R_lex + R_hpa；
    - **RT**：R_lex + R_sem + R_hpa。

**(2) 简化生成（段落级 + 文档级）**
- 段落级输入由训练好的模型直接简化。
- 文档级采用**动态语义感知分段**：
  - 用预训练句嵌入模型编码每个句子，计算相邻句余弦相似度；
  - 相似度显著下降处视为潜在语义/话题边界（低于阈值 τ）；
  - 再用**带软长度约束的贪婪合并策略**迭代合并相邻块，使每块 token 长度尽量落在目标区间 [0.75·L_src/N, 1.25·L_src/N]，其中块数 N 由输入长度与预定义值 L_pre 计算；
  - 各块独立简化后按原顺序拼接，避免超长输入导致性能骤降。

**(3) 指标辅助分析（Metric-assisted Analysis, MA）**
- 设计评估器量化生成简化的**结构与内容变换**：
  - **结构变化**：统计增、删、复制操作比例（P_add、P_del、P_copy）；
  - **内容变化**：Levenshtein 相似度（LevSim）衡量编辑幅度，词汇复杂度（LexC，基于词频的对数负均值）衡量是否使用更简单词汇。

**(4) 选择性精修（Selective Refinement, SR）**
- 模仿人类专家“多稿对比 + 词法打磨”流程：
  - 对同一输入生成 **K = 4 个候选简化**；
  - 每个候选配对对应的 MA 分析，形成 (Y_i, A(Y_i))；
  - 由 LLM 编辑器（实验中用 GPT-4o，温度 0.3）选出最合适候选，并在**严格保持整体结构与事实**的约束下进行词法级精修（替换生僻/复杂词为简单同义词、修正明显语法错误，禁止增删事实/实体/实验数据、避免句级合并/拆分/重排）。

## 3. 实验设计

### 3.1 数据集与场景
| 数据集 | 级别 | 领域 | 规模（测试） | 平均输入长度 |
|---|---|---|---|---|
| Cochrane | 段落 | 医学 | 480 | 478 |
| D-Wikipedia | 段落 | 维基 | 434 | 385 |
| Cell | 文档 | 医学 | 352 | 1145 |
| Swipe | 文档 | 维基 | 252 | 1095 |
| OneStopEnglish (News) | 文档（域外） | 新闻 | 189 | 1033 |

- 训练/验证数据：医学域 3,568/411，维基域 3,600/400（段落级），刻意只用“几千级”少量数据以检验数据效率。

### 3.2 评价指标（Benchmark）
- **SARI**：词法编辑操作质量；
- **D-SARI**：文档级扩展 SARI，惩罚三项编辑组件；
- **FKGL**：可读性（越低越简单）；
- **BERTScore**：语义相似度；
- **LENS**：面向简化的可学习人类判断预测指标（0–100）。

### 3.3 对比方法
- **传统基线**：Keep-It-Simple（多段落无监督）、Bart-Large-Wiki（维基数据微调 BART）——因设计限制仅报告段落级结果。
- **强开源 LLM**：Qwen2.5-72B-Instruct（ICL）、Llama3.3-70B-Instruct（ICL）、DeepSeek-V3.2（ICL+CoT）。
- **强闭源 LLM**：Qwen3-Max、GPT-5.2、Claude-Sonnet-4.5、Gemini-3-Pro-Preview（ICL+CoT）。
- **骨干基线**：Qwen2.5-14B-Instruct 及其 SFT 版本。
- **本文变体**：Simplify-Pro-RS / RD / RT。

## 4. 资源与算力

- 文中明确说明：所有模型在 **8 块 NVIDIA A800 80G GPU** 上训练 **2 个 epoch**。
- 训练配置：batch size 16、采样温度 1.0、恒定学习率 1e-6、最大生成 2,048 token；KL 系数 β = 0、clip-ratio-high = 0.28（参考 DAPO 经验）；实现基于 **verl** 框架。
- SFT 使用 LLaMA-Factory：LoRA Rank 128、Alpha 256、target all、3 epochs、学习率 1e-4、batch size 16。
- 推理：开源模型用 vLLM，闭源模型走官方 API；选择性精修用 GPT-4o。
- **未明确说明**：总训练时长/GPU 小时数、不同阶段的具体耗时、API 调用成本等。

## 5. 实验数量与充分性

### 实验组数概览
- **主实验**：表 1（段落级、医学+维基）、表 2（文档级、医学+维基）、表 3（域外文档级新闻），共覆盖 5 个数据集、3 种奖励变体、10 余个基线。
- **跨模型验证**：表 4（文档级医学，Qwen vs Llama）、表 9（段落级医学，附录）。
- **消融实验**：表 5（医学域，段落+文档级，w/o MA、w/o MA&SR）、表 10（维基域，附录）。
- **简化行为分析**：图 3（医学域）、图 6（维基域）五类编辑分布对比 gold 与 GPT/DeepSeek。
- **人工评估**：表 6，80 个随机样本（4 数据集各 20），3 个维度 + 总体偏好。
- **训练动态分析**：图 4、图 5（SARI/LENS/响应长度随训练步变化）。
- **案例研究与 CoT 对比**：附录 I–K。

### 充分性与公平性评估
- **优点**：覆盖域内/域外、段落/文档、多模型骨干、消融、人工评估、编辑分布与训练动态，维度较全面；基线包含强开源与闭源模型并统一使用 ICL/ICL+CoT 提示，比较相对公平；人工评估补充了自动指标不足。
- **不足**：
  - 传统基线仅能参与段落级比较，文档级缺少传统方法对照；
  - 消融主表仅报告医学域 RT 变体，维基域与 RS/RD 的消融放在附录且较简略；
  - 人工评估仅 80 例，统计效力有限，未报告标注者间一致性；
  - 部分结论（如“超过专有 LLM”）依赖指标组合，单一指标上并非全面领先。

## 6. 主要结论与发现

- **整体性能**：Simplify-Pro 在多数指标上优于或匹敌强开源与专有 LLM。段落级：RS 取得最佳 SARI（44.99/48.80）与 D-SARI；RD 取得最佳 FKGL（6.29/2.15）与 LENS（90.14/90.74）；RT 在 D-SARI 与 BERTScore 上领先或接近领先。文档级趋势一致。
- **域外泛化**：在 OneStopEnglish 新闻域、且**未做任何域内训练**的情况下，RT 取得第三低 FKGL（6.36）与第二高 LENS（84.73），RD 取得最低 FKGL（4.01）与最高 LENS（87.23），体现跨域稳健性。
- **跨模型泛化**：换用 Llama3.1-8B 作骨干时整体略降，但仍优于多数基线，说明框架效果不依赖特定模型系列；更大参数（Qwen2.5-14B）在语义保持与偏好对齐上更优。
- **消融结论**：移除 MA 导致 SARI/D-SARI/BERTScore 下降；再移除 SR 进一步损害 LENS 等质量指标，证明两阶段均必要，完整框架在平衡性上最佳。
- **简化行为**：Simplify-Pro 的五类编辑分布（词法、句法、篇章、语义、信息）显著更接近人工 gold；语义编辑占比最高，说明有效长文本简化主要由语义级内容选择与转换驱动。
- **人工评估**：RT 取得最高 Simplicity（4.58）与最高总体偏好（19/80），且 Meaning Preservation 第二（4.08），说明简化提升未以严重语义损失为代价。
- **训练动态**：R_lex 使 SARI 提升最稳但 LENS 偏低；加入 R_hpa 显著提升 LENS 但 SARI 变缓；三重混合奖励在两者间更平衡，且输出长度更短更可控。

## 7. 优点

- **框架设计模块化、渐进式**：四阶段职责清晰、可插拔，段落级训练成果可迁移到文档级，工程上易复用与扩展。
- **数据效率高**：仅用几千条段落级平行数据 + GRPO 强化学习即取得竞争性结果，降低对大规模人工标注的依赖。
- **奖励设计细致**：格式奖励、动态推理长度奖励、多维质量奖励（SARI + BERTScore + LENS）组合，并通过 RS/RD/RT 三种配置显式刻画“结构编辑 vs 可读性 vs 语义保持”的权衡，便于按场景选型。
- **文档级分段策略合理**：语义边界检测 + 软长度约束贪婪合并，兼顾语义连贯与长度可控，缓解超长输入性能衰减。
- **可解释的中间信号**：MA 阶段提供增/删/复制比例、Levenshtein 相似度、词汇复杂度等可量化、可解释的候选对比依据，支撑选择性精修。
- **实验较全面**：域内/域外、段落/文档、跨骨干、消融、人工评估、编辑分布与训练动态多角度验证，结论有支撑。

## 8. 不足与局限

- **语言与领域覆盖有限**：仅在英文上系统评估，多语言与低资源场景未验证（作者在 Limitations 中亦承认）。
- **模型规模与架构探索不足**：主要基于 Qwen2.5-14B-Instruct，虽补充 Llama3.1-8B，但对更大/更小参数、不同架构的系统性分析欠缺。
- **指标间存在权衡**：不同变体各有短板（如 RD 的 BERTScore 偏低、RS 的 FKGL 偏高），“全面超越”需结合指标组合解读；部分消融变体在个别指标上反而更优，说明结论对指标选择敏感。
- **对外部强模型有依赖**：选择性精修使用 GPT-4o 作为编辑器，引入额外成本与可复现性/公平性隐忧（与基线对比时相当于借用了更强模型能力）。
- **实验细节缺口**：未报告训练总时长、能耗、API 成本；人工评估样本量小且未报告标注者一致性；传统基线无法参与文档级比较，削弱了文档级对比的完整性。
- **应用限制**：医学域简化涉及事实准确性，框架虽有“不增删事实”的约束，但缺乏专门的事实性/安全性评估；长文档分块独立简化可能损失跨块连贯性，论文未深入量化该风险。
- **数据规模限制**：训练数据仅数千条，结论在更大规模数据下的可扩展性尚不明确。

（完）
