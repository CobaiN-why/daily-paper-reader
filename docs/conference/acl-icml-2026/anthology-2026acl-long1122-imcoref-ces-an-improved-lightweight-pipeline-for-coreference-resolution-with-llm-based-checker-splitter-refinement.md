---
title: "ImCoref-CeS: An Improved Lightweight Pipeline for Coreference Resolution with LLM-based Checker-Splitter Refinement"
title_zh: ImCoref-CeS：基于大模型检查-拆分精炼的轻量级指代消解流水线
authors: "Kangyang Luo, Yuzhuo Bai, Shuzheng Si, Cheng Gao, Zhitong Wang, Yingli Shen, Wenhao Li, Zhu Liu, Yufeng Han, Jiayi Wu, Cunliang Kong (孔存良), Maosong Sun (孙茂松)"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://aclanthology.org/2026.acl-long.1122.pdf"
tags: ["query:ai-se"]
score: 7.0
evidence: 结合监督模型与大模型推理的自然语言指代消解
tldr: 指代消解研究长期在小型监督模型的高效流水线与大模型推理能力之间取舍。ImCoref-CeS提出融合框架，先以改进的监督模型ImCoref提升检测-聚类流水线性能，再引入大模型进行检查与拆分精炼。实验显示该轻量流水线在指代消解任务上取得更优效果，展示了监督方法与LLM协同的可行路径。
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1122/fig-001.webp\", \"caption\": \"\", \"page\": 3, \"index\": 1, \"width\": 1024, \"height\": 1024}]"
motivation: 指代消解需在小型监督模型效率与大模型推理能力之间取得平衡。
method: 在改进的监督式检测-聚类模型基础上引入大模型检查-拆分模块进行迭代精炼。
result: 该轻量流水线在指代消解任务上性能优于现有基线方法。
conclusion: 监督神经方法与LLM推理相结合可有效提升NLP指代消解效果。
---

## Abstract
Coreference Resolution (CR) is a critical task in Natural Language Processing (NLP). Current research faces a key dilemma: whether to further explore the potential of supervised neural methods based on small language models, whose detect-then-cluster pipeline still delivers top performance, or embrace the powerful capabilities of Large Language Models (LLMs). However, effectively combining their strengths remains underexplored. To this end, we propose ImCoref-CeS , a novel framework that integrates an enhanced supervised model with LLM-based reasoning. First, we present an improved CR method ( ImCoref ) to push the performance boundaries of the supervised neural method by introducing a lightweight bridging module to enhance long-text encoding capability, devising a biaffine scorer to comprehensively capture positional information, and invoking a hybrid mention regularization to improve training efficiency. Importantly, we employ an LLM acting as a multi-role Checker-Splitter agent to validate candidate mentions (filtering out invalid ones) and coreference results (splitting erroneous clusters) predicted by ImCoref. Extensive experiments demonstrate the effectiveness of ImCoref-CeS, which achieves superior performance compared to existing state-of-the-art (SOTA) methods.

---

## 论文详细总结（自动生成）

# 论文结构化总结：ImCoref-CeS

## 1. 核心问题与研究动机

- **领域困境**：指代消解（CR）当前面临路线抉择——是继续挖掘小型监督神经模型（SpanBERT / DeBERTa + detect-then-cluster 流水线，代表作为 Maverick）的潜力，还是转向大语言模型（LLM）。
- **监督方法优势与短板**：训练成本低、推理快、域内性能仍是 SOTA；但模型规模小、任务专用，**域外数据上易产生大量无效指代（invalid mentions）**，域内也存在无效指代与聚类错误，成为性能瓶颈。
- **LLM 的优势与短板**：推理能力强，在**给定 gold mentions** 时可达甚至超过监督方法（如 GPT-4 在 gold mention 设定下 Avg.F1 达 88.4%）；但自身**指代检测能力弱**，端到端性能远逊于监督方法。
- **核心问题**：能否用 LLM 的推理能力弥补监督神经方法固有的无效指代与聚类错误？论文给出肯定回答，提出 **ImCoref-CeS** 框架，在推理阶段协同二者优势（低资源效率 + 深度推理），且不增加 LLM 训练成本。

## 2. 方法论

### 2.1 ImCoref：对 Maverick 的三点改进

- **轻量桥接模块（LBM）**：解决长文本分段编码导致的**语义隔离**问题。编码每段时前置 `[CLS]`、后置 `[SEP]`，将前一段 `[SEP]` 的隐表示作为整段语义摘要，用于调制下一段表示：
  - 更新式：`H_{i+1} ← Norm(LBM(h_i^[SEP], H_{i+1}) + H_{i+1})`
  - 两个变体：**LBM-FC**（全连接 + 广播拼接）与 **LBM-MHA**（以 `h_i^[SEP]` 为 query、`H_{i+1}` 为 key/value 的多头注意力），仅用于 independent 分段策略。
- **双仿射增强的指代检测（Biaffine Scorer）**：Maverick 的 `p_end = σ(MLP(concat))` 对位置信息利用不足，改为双仿射打分：
  - `X_s = FC_1(H̃_s)`，`X_e = FC_2(H_e)`
  - `S = X_s^T U X_e + W(X_s ⊕ X_e) + b`，再 `p_end = σ(MLP(S))`
  - 通过双线性项 `U` 与线性项 `W` 联合建模起止 token 的位置交互。
- **混合指代正则化（HyMR）**：Maverick 仅用 `L_s = L_s^EOS`（到最近 EOS 的距离）约束，易诱导过长无效指代；HyMR 改为 `L_s = min{L_max, L_s^EOS}`：
  - `L_max` 限制超长 span，`L_s^EOS` 防止跨句，二者互补；同时进一步降低训练开销（默认 `L_max = 30`）。
- 聚类阶段沿用 Maverick mes 的策略。

### 2.2 LLM Checker-Splitter：推理期动态精炼

- **Mention Checker（M-Ce）**：将 ImCoref 输出的候选指代在原文本中以 `[...]` 标注，附局部上下文（所在句 + 少量前文），由 LLM 判定 `Yes / No / Pending`，过滤无效指代（如 "man" 缺失限定词 "another"）。
- **Coreference Checker（C-Ce）**：对含 ≥2 个指代的聚类，用 `[(#X) ... ](#X)` 唯一编号标注，判断是否同指。
- **Coreference Splitter（C-S）**：对判为错误的聚类重新分组，约束为**组内一致性、组间互斥、完整性、不引入新指代**；若无法判断则单列新组或报告失败。
- **成本控制过滤器**：
  - **Mention Filter**：代词（固定词表）直接跳过；非代词按 `p_end` 降序，仅对置信度最低的 `η_1` 比例调用 LLM。
  - **Cluster Filter**：仅处理多指代聚类；构造置信度 `p_fc = p̄_c − ρ·sqrt(mean((p_c − p_{c,j})^2))`，按 `p_fc` 降序只验证最低的 `η_2` 比例（默认 `η_1 = η_2 = 0.6`，`ρ = 1e-3`）。
  - 设计依据：预测概率越低 → 不确定性越高 → 越需要 LLM 介入（借鉴 Double-checker 思路）。

## 3. 实验设计

- **数据集**：
  - **OntoNotes**（CoNLL-2012，2802/343/348 篇，域内主基准，不标注 singleton）
  - **LitBank**（100 部文学作品，80/10/10，长文档，标注 singleton）
  - **WikiCoref**（30 篇维基文章，域外泛化测试，最长约 9869 词）
- **评价指标**：MUC、B³、CEAF-φ4 的 P/R/F1，取三者 F1 均值为 **Avg.F1（CoNLL-F1）**；消融中另报指代检测的 P/R/F1。
- **对比方法（三大类）**：
  1. 监督神经方法：c2f-coref、ICoref、CorefQA、s2e-coref、longdoc、wl-coref、f-coref、LingMess、Dual-cache、Maverick mes
  2. 生成式方法：ASP、Link-Append、seq2seq
  3. LLM 方法：InstructGPT、GPT-3.5-turbo、GPT-4、LLMLink
- **本文模型**：ImCoref（DeBERTa-large 底座）；ImCoref-CeS 分别搭配 Qwen2.5-72B-Instruct、DeepSeek-R1-250528、GPT-4（API，temperature=0）。
- **公平性处理**：与 Maverick 对齐文本编码策略（对比实验不使用 LBM），LBM 仅在消融中单独评估。

## 4. 资源与算力

- **训练/推理硬件**：单张 **RTX 4090（24GB）**；作者有 8 张该卡可并行跑多组实验，但**不使用数据/模型并行**。
- **训练时长**：OntoNotes 上 ImCoref 约 **13 小时**（Maverick 为 14h）；LitBank 约 **3 小时**；参数量 531M（Maverick 504M）。
- **推理开销**：ImCoref 约 **15 秒/文档**、显存约 4.05 GiB；ImCoref-CeS 约 **2–5 分钟/文档**（受网络与 API 影响）。
- **LLM 调用**：全部通过远程 API，temperature=0；**未报告 API 调用次数与费用**，也未给出 LLM 侧的 token 消耗统计。

## 5. 实验数量与充分性

- **主实验 3 组**：OntoNotes（Table 2/15）、LitBank（Table 3/16）、WikiCoref 跨域（Table 4/17），均给出完整 P/R/F1。
- **消融/分析实验约 5 组**：
  1. 分段策略对比：baseline / independent / overlap(T/2) / LBM-FC / LBM-MHA（Fig. 3a、Table 18）
  2. `L_max` 扫描：{10, 20, 30, 40, +∞}（Fig. 3b、Table 19）
  3. Checker-Splitter 留一消融：完整 / w/o M-Ce / w/o C-CeS / ImCoref（Table 5/20）
  4. 过滤比例 `η` 扫描：{0, 0.2, …, 1.0}（Fig. 4）
  5. 阈值 `ρ` 扫描：1e-5 ~ 1e0（Fig. 6）
- **评价**：覆盖域内、长文档、跨域三类场景，消融覆盖各创新点与超参，并同时报告性能与时间/显存，**整体较为充分、客观**。
- **需注意的公平性问题**：
  - LLMLink 需训练多个 LLM，与本文"零训练 LLM"路线成本不对等，直接比较略有不公（论文亦有说明）。
  - 三个 LLM 通过 API 调用，结果受模型版本与网络波动影响，**可复现性弱**。
  - 仅 3 个英文数据集，未涉及中文/多语言或其他域（如生物医学、对话）。

## 6. 主要结论与发现

- **ImCoref 稳定超越 SOTA 监督方法**：OntoNotes Avg.F1 **84.3%** vs. Maverick 83.6%，且训练时间更短（13h vs. 14h）、推理开销相当；LitBank **79.7%** vs. 78.4%；WikiCoref 67.6% vs. 66.8%。
- **LLM 精炼带来显著增益**：OntoNotes 上 ImCoref-CeS_gpt4 达 **86.0%**（全表最佳）；LitBank 上 ImCoref-CeS_dpsk 达 **81.8%**；WikiCoref 上 ImCoref-CeS_gpt4 达 **73.2%**，相较 ImCoref **平均提升 4.7%**，说明推理期引入 LLM 显著增强**跨域泛化**。
- **两组件均必要，且 C-CeS 更关键**：去掉 C-CeS 的损失大于去掉 M-Ce（OntoNotes 84.5% vs. 85.0%），说明直接纠正聚类比仅过滤指代收益更大。
- **η = 0.6 为性价比拐点**：性能在 η ≤ 0.6 时单调上升，之后饱和；而推理时间随 η 线性增长，全量调用（η=1.0）徒增延迟而无收益。
- **L_max = 30 最优**：性能先升后稳（OntoNotes）或略降（LitBank），训练时间随 `L_max` 单调上升，HyMR 在不损性能前提下节省算力。
- **LBM 缓解分段损失**：分段必然导致性能下降，但 LBM-FC / LBM-MHA 均优于 independent 与 overlapping，且训练时间增加有限。
- **LLM 的定位被再次确认**：无 gold mention 时纯 LLM 方法（GPT-4 端到端仅 62.9%）远落后于监督方法，印证"LLM 弱于指代检测、强于同指推理"的判断。

## 7. 优点

- **思路清晰、定位准确**：不做"LLM 替代监督模型"的激进路线，而是让 LLM 在**推理期做"审计员"**，规避其检测短板、发挥其推理长板，工程上务实。
- **轻量可插拔**：ImCoref 三项改进均为小改动（+27M 参数、训练时间反降），Checker-Splitter 无需训练、可替换任意 LLM，落地成本低。
- **成本可控的设计**：代词直通 + 概率排序过滤，把 LLM 调用限制在"最不确定"的少数样本上，并给出 η 的性能-时延曲线指导调参

- **成本可控的设计**：代词直通 + 概率排序过滤，把 LLM 调用限制在"最不确定"的少数样本上，并给出 η 的性能-时延曲线指导调参；`p_fc` 同时考虑聚类内平均置信度与离散度，用极小的 `ρ` 仅作排序扰动，避免阈值式硬过滤带来的误删。
- **实验呈现诚实**：论文明确指出分段编码必然带来性能损失，也未回避 LBM 在 LitBank 上增益有限、`L_max` 增大在部分数据集上反而略降等负面结果；对 LLMLink 等对比方法的成本不对等亦有说明，态度较为客观。
- **消融设计有针对性**：Checker-Splitter 采用留一法（完整 / w/o M-Ce / w/o C-CeS），能够分别定位"过滤指代"与"纠正聚类"两类错误的贡献，而不是笼统报告一个"LLM 增益"，结论可解释性强。
- **跨域泛化叙事完整**：从域内（OntoNotes）→ 长文档（LitBank）→ 域外（WikiCoref）逐级加难，且增益幅度随难度上升（域外提升最明显），与"LLM 补充监督模型的域外脆弱性"这一动机形成闭环，论证链条自洽。
- **工程细节可复现性较好**：给出了训练时长、显存占用、参数量、单文档推理耗时等具体数字，分段策略、`L_max`、`η`、`ρ` 等关键超参均给出扫描曲线，便于后续研究者对齐与复现 ImCoref 部分。

## 8. 不足与局限

- **LLM 侧开销缺乏量化**：全文未报告 API 调用次数、token 消耗与费用，而 ImCoref-CeS 单文档 2–5 分钟的延迟在实际部署（尤其长文档批处理）中可能成为硬约束；与 ImCoref 的 15 秒/文档相比是数量级差距，"低成本"的说法主要针对**训练成本**而非**推理成本**。
- **可复现性受 API 制约**：三个 LLM 均为远程调用、temperature=0，但闭源模型版本漂移与网络波动会使结果难以完全复现；论文亦未说明重试、解析失败（LLM 输出不符合 `Yes/No/Pending` 格式）时的处理策略与失败率。
- **对 LLM 输出的鲁棒性讨论不足**：M-Ce 引入 `Pending` 类别，但论文未分析该类别的占比及其最终处理方式（保留 / 丢弃 / 交由下游），也未报告 Checker 的判定准确率（与人工标注对比），因此难以判断增益究竟来自 LLM 推理还是简单的噪声注入。
- **改进点偏经验性、缺乏机理分析**：LBM 的两种变体（FC / MHA）孰优孰劣、双仿射项 `U` 学到了什么、HyMR 中 `L_max = 30` 与数据集中平均指代长度是否相关，均只有结果层面的对比，缺少可视化或误差分析支撑。
- **数据集覆盖面有限**：仅 3 个英文数据集，未涉及中文/多语言、对话、生物医学等域；OntoNotes 不标注 singleton 而 LitBank 标注，两者评测设定不完全一致，跨数据集的结论可比性需谨慎对待。
- **基线时效性**：监督方法对比以 Maverick 为主要对手，LLM 对比中 GPT-4 为 API 版本，缺少与更新的端到端 LLM 指代方法（如基于长上下文模型直接 prompting、或 tool-use 式迭代方法）的比较，SOTA 主张的边界需进一步确认。
- **过滤器的先验假设未验证**：以 `p_end` / `p_fc` 低置信度作为"最需 LLM 介入"的代理指标，其有效性依赖"模型置信度与错误率单调相关"这一假设；论文未给出置信度分箱后的实际错误率曲线，若该假设在域外不成立（监督模型在 WikiCoref 上系统性过度自信），过滤器可能筛错对象。
- **误差传播未分析**：M-Ce 误删正确指代会直接破坏后续聚类（且 C-CeS 无法恢复），论文报告的是端到端指标，缺少"过滤器引入的新错误 vs. 修正的旧错误"的净收益拆解。

## 9. 启示与可拓展方向

- **"小模型检测 + 大模型审计"是可复用的范式**：该框架本质上把任务分解为"高召回、低精度的候选生成"与"低成本的判别式精炼"两段，可迁移到实体链接、事件抽取、关系抽取等同样存在"检测难、判定易"结构的任务。
- **推理期协同优于训练期融合**：不微调 LLM、仅在其外部加 Checker/Splitter，既保留了监督模型的效率，又避免了 LLM 训练的高成本与灾难性遗忘，为资源受限团队提供了可行路径。
- **不确定性驱动的调用策略值得深化**：当前用启发式概率排序 + 固定比例 `η`，未来可引入 conformal prediction、学习式 router 或预算约束下的最优停止策略，把"调用多少、调用谁"变成可优化问题。
- **LLM 可作为弱标注/蒸馏源**：Checker 的判定结果可回流用于再训练 ImCoref（伪标签或难例挖掘），形成"推理期精炼 → 训练期内化"的闭环，有望逐步降低对在线 LLM 的依赖。
- **长文档与分段问题是独立价值点**：LBM 针对分段语义隔离的轻量桥接思路，对任何需要切块编码的长文本任务（长文档摘要、跨段共指、文档级 IE）都具有参考意义。
- **评测层面建议**：后续工作宜同时报告"指代检测 F1 + 聚类 F1 + 端到端 F1"与"LLM 调用次数/费用"，并加入人工错误分析，才能真实刻画这类混合系统的性价比边界。

## 10. 总体评价

论文提出了一条务实且论证完整的中间路线：以轻量改进的监督模型 ImCoref 保证检测质量与效率，再以零训练的 LLM Checker-Splitter 在推理期修正其两类典型错误。实验在域内、长文档、跨域三个层面均取得稳定提升（OntoNotes 86.0%、LitBank 81.8%、WikiCoref 73.2%），消融清晰指出"纠正聚类"比"过滤指代"更关键，`η = 0.6`、`L_max = 30` 等结论具备直接的操作指导价值。主要短板在于 LLM 侧成本未量化、API 结果可复现性弱、改进点偏经验性且缺少细粒度误差分析，数据集覆盖也仅限英文。总体而言，这是一篇工程价值突出、动机与实验自洽的工作，其"检测交给小模型、判定交给大模型"的分工思路对指代消解乃至更广的信息抽取任务都具有借鉴意义。

（完）
