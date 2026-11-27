---
title: "BOLT: Benchmarking Open-World Learning for Text Classification"
title_zh: BOLT：面向文本分类的开放世界学习基准
authors: "Chuan Qin, Xi Chen, Jinpeng Li, Hengshu Zhu"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://aclanthology.org/2026.findings-acl.667.pdf"
tags: ["query:ai-se"]
score: 4.0
evidence: 面向开放世界文本分类的NLP基准
tldr: 文本分类长期以闭世界设定为主，假设类别事先已知，而开放世界学习更贴近真实应用却缺乏系统评测。作者提出BOLT，一个支持开放世界文本分类的统一基准与评测工具包，涵盖开放集文本分类即区分分布内样本并拒识未知类别，以及新类别发现等任务。该工作弥补了现有基准只关注分布外检测而忽视更广泛挑战的不足，为构建更鲁棒的NLP分类系统提供了评测基础。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl667/fig-001.webp\", \"caption\": \"\", \"page\": 3, \"index\": 1, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl667/fig-002.webp\", \"caption\": \"\", \"page\": 3, \"index\": 2, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl667/fig-003.webp\", \"caption\": \"\", \"page\": 3, \"index\": 3, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl667/fig-004.webp\", \"caption\": \"\", \"page\": 3, \"index\": 4, \"width\": 350, \"height\": 350}]"
motivation: 现有文本分类基准多为闭世界设定，忽视开放世界中的拒识与新类别发现等挑战。
method: 构建统一的开放世界文本分类基准与工具包BOLT，覆盖开放集分类和新类发现任务。
result: 基准系统化评估了模型在分布内分类与未知类别处理上的表现。
conclusion: BOLT为更鲁棒的NLP文本分类研究提供了标准化开放世界评测平台。
---

## Abstract
Text classification has long been a cornerstone of NLP, yet most prior work and benchmarks have been limited to closed-world settings, where all classes are assumed to be known in advance. In contrast, open-world learning has recently emerged as a critical paradigm for building more robust and realistic systems. However, existing benchmarks largely focus on out-of-distribution (OOD) detection, while overlooking broader challenges such as the discovery of novel categories. To address this gap, we introduce BOLT, a unified Benchmark and evaluation toolkit supporting Open-world Learning for Text classification. BOLT encompasses two representative tasks: Open-set Text Classification (OSTC), which requires models to classify in-distribution (ID) samples while rejecting OOD inputs, and Generalized Category Discovery (GCD), which aims to identify both known and novel categories from partially labeled corpora. We carefully curate 12 publicly available datasets spanning diverse domains and benchmark 22 methods, including 15 for OSTC and 7 for GCD, under a standardized protocol that explicitly accounts for varying labeled ratios and known class ratios. Our results reveal key challenges: most current methods tend to overfit training distributions and struggle to generalize to unseen classes. Moreover, by comparing our lightweight LLM-based variants with prior open-set baselines, we demonstrate the promise of leveraging LLMs for open-world text classification. BOLT provides standardized evaluation protocols that enable fair comparison and support future research in this emerging area. All datasets, baselines, and tools are available at https://github.com/CNIC-DSL/BOLT.

---

## 论文详细总结（自动生成）

# BOLT：面向文本分类的开放世界学习基准 —— 论文结构化总结

## 1. 核心问题与整体含义

- **背景**：文本分类是 NLP 的核心任务（情感分析、主题标注、意图识别等），但绝大多数研究建立在**闭世界假设**上——目标类别在训练前已完全确定并可见，这与真实场景中标签空间开放、新类别不断涌现的事实不符。
- **开放世界文本分类（OTC）的两类代表任务**：
  - **OSTC（开放集文本分类）**：仅用已知类标注数据训练，测试时需正确分类分布内（ID）样本并拒识分布外（OOD）样本。
  - **GCD（广义类别发现）**：利用部分标注语料，同时识别已知类并发现新类。
- **现有基准的三大缺口**：
  - 评测多局限于少数意图识别数据集（如 BANKING、CLINC），任务类型单一、文本域同质（长度集中、以英文为主）。
  - 实验协议不一致（已知类比例、标注量、评价指标各异），难以公平比较（见表 1）。
  - OSTC 很少在低资源下评测，GCD 对监督信号强度的探索有限；LLM 在 OTC 中的潜力（如作为表示学习骨干）基本未被挖掘。
- **论文目标**：提出 **BOLT**——首个统一支持 OSTC 与 GCD 的开放世界文本分类基准与评测工具包，提供标准化协议、多样化数据与系统化方法对比。

## 2. 方法论

### 2.1 问题形式化

- 输入空间 \(X\)，标签空间 \(Y = Y_k \cup Y_n\)，其中 \(Y_k\) 为已知类、\(Y_n\) 为新类。
- 数据组成：标注集 \(D_l\)（仅含 \(Y_k\)）、无标注集 \(D_u\)（可混合已知/新类）、测试集 \(D_t\)（含已知+新类）。
- **OSTC**：学习 \(K+1\) 分类器 \(f_{OOD}: X \to Y_k \cup \{\text{Unknown}\}\)，将新类统一映射为“未知”。
- **GCD**：从 \(D_l \cup D_u\) 学习 \(f_{GCD}: X \to Y_k \cup Y_n\)，假设新类数量 \(|Y_n|\) 已知，评测同时覆盖已知与新类。

### 2.2 开放世界构造机制（核心设计）

- **KCR（Known Class Ratio）**：控制已知类占全部标签的比例（0.25 / 0.50 / 0.75），模拟不同开放程度。
- **LAR（Labeled Ratio）**：控制已知类中标注样本比例（0.1 / 0.5 / 1.0），模拟不同监督强度。
- **统一五折标签划分**：将整个标签空间均匀切成 5 个低重叠子集，每折轮流作为已知类集合，其余作为未知类测试，降低随机划分带来的不稳定性。
- 用户只需提供标准 CSV 格式的训练/验证/测试集并指定 KCR、LAR，工具包自动生成对应标签划分，保证可复现与可扩展。

### 2.3 评测指标

- **OSTC**：ACC、Macro-F1、K-F1（已知类平均 F1）、N-F1（所有新类合并为“unknown”后的 F1）。
- **GCD**：ACC、K-ACC、N-ACC（基于匈牙利匹配的分组聚类精度）、H-Score（K-ACC 与 N-ACC 的调和平均）、ARI、NMI。

### 2.4 方法集成框架

- **OSTC 三类方法族**：
  - 传统非 PLM：DOC（one-vs-rest sigmoid）、DeepUnk（大间隔余弦损失）。
  - PLM 基：ADB（自适应球形边界）、SCL（监督对比学习）、AB（角度边界）、KNNCon（KNN 对比 + LOF 检测）、DyEn（动态集成 + 早退）。
  - **本文新提出的 LLM 基框架**：微调 LLM + MLP 分类头作为判别骨干，并叠加 8 种后处理 OOD 打分：MSP、OpenMax、TempScale、Energy、LogitNorm、Entropy、KLMatching、MaxLogit。
- **GCD 两类方法族**：
  - PLM 聚类：DAL（对齐伪标签）、GeoID（几何感知聚类）、SDC（自去偏校准）、DPN（双路径原型）、TAN（迁移对齐网络）。
  - LLM 增强：LOOP（LLM 在环的邻域对比）、ALUP（LLM 主动伪标签精炼）。

## 3. 实验设计

### 3.1 数据集与场景

- **12 个公开数据集**，覆盖三大场景：
  - **主题分类**：20NG、THUCNews、Yahoo、X-Topic（多语言，含英/日/西/希）。
  - **意图检测**：BANKING、CLINC、StackOverflow、HWU、TREC、ECDT（中文）、MCID。
  - **本体分类**：DBPedia（219 类）。
- **多样性维度**：文本域（新闻、对话查询、问答、维基）、平均长度 8–1856 词、标签数 10–219、多语言（英、中、日、西、希）。
- 大规模语料统一采样 1 万条；全部去重并标准化格式。

### 3.2 Benchmark 设置

- KCR ∈ {0.25, 0.50, 0.75} × LAR ∈ {0.1, 0.5, 1.0}，共 9 种配置，每配置 5 折平均。
- 另有：LLM 骨干规模对比（Qwen2.5-3B/7B/32B）、标签采样策略对比（随机 vs 语义相似）、运行时间对比。

### 3.3 对比方法

- **共 22 个方法**：OSTC 15 个（2 传统 + 5 PLM + 8 LLM 后处理），GCD 7 个（5 PLM + 2 LLM 增强）。
- 默认 LLM 骨干 LLaMA-3.1-8B；PLM 基线用 bert-base-uncased / bert-base-chinese；LLM 增强方法额外接入 DeepSeek-V3.1 做伪标签验证与语义校准。
- 所有实现尽量遵循官方代码，统一训练/评测协议与超参。

## 4. 资源与算力

- **硬件**：8 块 NVIDIA RTX 5090（每块 32 GB 显存），512 GB 系统内存。
- **训练时长**（BANKING，KCR=0.25，LAR=0.1，见表 S3）：
  - OSTC 的 BERT 类基线约 5–9 分钟（AB 5m10s、DOC/DeepUnk 5m20s、ADB/SCL 6m40s、KnnCon 9m10s），DyEn 18m50s；LLM+OOD 检测 19m02s。
  - GCD 普遍更耗时：SDC 11m20s、DAL 14m00s、DPN 28m50s、TAN 27m50s、GeoID 47m10s；LLM 增强的 LOOP 1h00m20s、ALUP 1h22m20s。
- 论文**未报告总 GPU 小时数**或全部实验的累计能耗，仅给出单数据集单配置的代表性时长。

## 5. 实验数量与充分性

- **规模**：12 数据集 × 3 KCR × 3 LAR × 5 折 × 22 方法，另加骨干规模（3 档）、采样策略（2 种）、运行时对比，附录 S4–S33 给出 OSTC 四指标、GCD 六指标的完整逐数据集结果。
- **充分性**：
  - 覆盖任务（OSTC/GCD）、开放度（KCR）、监督强度（LAR）、数据域、语言、文本长度、标签粒度多个维度，网格化设计较为系统。
  - 消融/分析较完整：KCR 影响、LAR 影响、LLM 规模影响、采样策略影响、运行时对比。
- **客观与公平性**：
  - 统一五折划分、统一阈值（OOD 阈值固定 0.5）、统一骨干与超参，横向可比性较好。
  - 但 LLM 基 OSTC 方法为本文首次提出，其调优投入与已有基线是否完全对等难以从文中判断；部分基线（如 SCL、DOC）在特定数据集上表现异常（如 ECDT 上概率趋近均匀），可能受实现/语言适配影响。

## 6. 主要结论与发现

- **OSTC**：
  - PLM 方法普遍 K-F1 高、N-F1 低，说明**过拟合训练分布、难以泛化到未见类**；LLM 方法缓解了这种失衡。
  - 已知类识别上 ADB、KNNCon、DyEn 表现稳健（结构化主题、意图数据各有优势）；新类检测上 **LLM-Energy / LLM-MaxLogit 几乎全面领先**，体现 LLM 在不确定性估计上的潜力。
  - LLM 变体在 OSTC 上并未稳定超越强 PLM 基线，直接使用 LLM 做 OSTC 仍有待探索。
  - 非 PLM 方法在中文 ECDT 上因缺乏语义先验导致概率近均匀、大量判为 OOD，K-F1 极低而 N-F1 虚高。
- **GCD**：
  - PLM 聚类在长文本、信息丰富语料（20NG、DBPedia、THUCNews）上已知类判别强（TAN 最稳）。
  - LLM 增强方法（ALUP、LOOP）在短文本意图数据与低资源下新类发现更强，但仍存在对已知类的过拟合。
  - SDC 因校准机制在噪声伪标签下表现相对突出，提示 logit 校准是 GCD 的有效方向。
- **KCR 影响**：OSTC 中 KCR 升高提升 K-F1 但明显拉低 N-F1（闭集偏置增强）；GCD 中该负面效应弱得多，因无标注数据支持 K+N 联合伪标签学习。
- **LAR 影响**：标注增多主要提升已知类性能；开放集鲁棒性对标注量不敏感，LLM 类方法在低标签下仍保持优势。
- **LLM 规模**：非单调——32B 平均 N-F1 最佳（65.86），3B 平均 K-F1 最佳（52.89），7B 反而偏弱；在 DBPedia 这类高基数、标签描述极短的场景，增大规模甚至会同时降低 K-F1 与 N-F1，瓶颈在于**标签空间歧义而非表示容量**。
- **采样策略**：语义相似的类别划分（更贴近真实场景）一致优于随机划分，说明 OTC 方法在实际应用中表现更好。

## 7. 优点

- **首个统一 OSTC 与 GCD 的 OTC 基准与工具包**，填补“只关注 OOD 检测、忽视新类发现”的空白。
- **数据多样性突出**：12 数据集横跨三场景、八领域、多语言、8–1856 词长度、10–219 类，比以往单任务单域评测更具代表性。
- **协议标准化**：KCR/LAR 双因素控制 + 五折低重叠划分 + 统一指标，显著提升可复现性与跨方法可比性。
- **方法覆盖系统**：从传统、PLM 到 LLM 增强三代范式，并**首次提出 LLM 基 OSTC 框架**（8 种后处理 OOD 打分），为后续研究提供基线。
- **工程友好**：提供统一命令行入口、YAML 配置、自动标签划分，支持新数据集与新算法接入，开源可扩展。
- **分析维度丰富**：除主结果外，还考察 KCR/LAR 敏感性、LLM 规模、采样策略与运行时成本，结论有实践指导意义。

## 8. 不足与局限

- **作者自述局限**：
  - 未深入探究不同 LLM 骨干对性能的影响（仅用 Qwen2.5 做了规模对比，默认骨干单一）。
  - 多语言数据集仍可扩充，跨语言适用性有待加强。
- **实验覆盖与偏差风险**：
  - 大规模语料统一采样 1 万条，可能损失原始分布特性；X-Topic 本身是多标签任务，处理方式可能被简化。
  - 英文数据占主导，中文仅 THUCNews/ECDT，多语言结论的外推性有限。
  - OOD 阈值固定为 0.5，未做阈值敏感性分析，可能影响部分方法的公平比较。
  - LLM 基 OSTC 方法由作者提出，与已有基线的调优力度是否对等缺乏说明

- **评测协议层面**：主结果以点估计呈现，未见置信区间或显著性检验，方法间小幅差距（尤其 OSTC 的 K-F1/N-F1 权衡处）是否稳定缺乏统计支撑；未讨论类别不平衡对 Macro-F1 与 H-Score 的影响，而真实 OTC 场景中长尾分布极为常见。
- **任务假设层面**：GCD 设定假设新类数量 \(|Y_n|\) 已知，真实开放世界中新类数目往往未知且随时间增长；评测仅覆盖单标签分类，未涉及多标签、层次标签或标签描述（label description）可用等更贴近 LLM 应用形态的设定。
- **方法层面**：LLM 基 OSTC 框架仅在**后处理打分**层面使用 LLM，未探索端到端训练目标（如能量正则、对比式 OOD 目标）与 LLM 表示的结合；LLM 增强 GCD 方法依赖外部强模型（DeepSeek-V3.1）生成/校验伪标签，其收益中有多少来自 BOLT 协议、多少来自外部模型能力，缺少解耦分析。
- **成本与可复现性**：LLM 类方法在运行时上显著高于 PLM 基线（GCD 的 LLM 增强方法达小时级），论文未给出“精度—成本”的帕累托分析，也未讨论在单卡或消费级硬件上的可行配置，社区复现门槛偏高。
- **工具包边界**：虽宣称支持新数据集与新算法接入，但未系统评估接入第三方方法时的适配成本（如方法自带阈值策略、特殊数据预处理与统一协议冲突时的处理方式）。

## 9. 对后续研究的启示

- **评测应双指标并报**：K-F1 与 N-F1（或 GCD 的 K-ACC/N-ACC/H-Score）必须成对呈现，单一闭集精度会系统性高估方法能力，并掩盖“闭集偏置”这一核心失效模式。
- **标签划分方式应成为默认设计变量**：语义相似类别的划分更贴近真实部署，建议后续工作将其作为主设置、随机划分作为对照，而非相反。
- **LLM 的定位宜聚焦“不确定性估计与伪标签精炼”**：实验显示 LLM 在 OOD 打分与低资源新类发现上优势明显，但直接替代判别骨干并不稳定；这提示更合理的路线是“PLM/小模型做判别 + LLM 做校准与发现”。
- **规模不是万能解**：LLM 规模对 OTC 性能呈非单调影响，瓶颈在于标签空间歧义；未来可探索标签语义增强、层次化标签建模来缓解，而非单纯堆参数。
- **校准是跨任务共性抓手**：SDC 在 GCD、LogitNorm/Energy 在 OSTC 的相对优势共同指向 logit 校准，可作为统一改进方向。
- **协议可作为“压力测试”模板**：KCR × LAR 的二维网格便于刻画方法在“开放度—监督强度”平面上的失效区域，值得被其他开放世界任务（视觉、跨模态）借鉴。

## 10. 适用人群与使用建议

- **适用人群**：开放集识别、类别发现、LLM 不确定性估计方向的研究者；需要在真实业务中处理“新意图/新主题不断出现”的工程团队；希望以统一协议复现并对比 OTC 方法的评测者。
- **使用建议**：
  - 新方法接入时优先在低资源格点（KCR=0.25、LAR=0.1）与语义相似划分下验证，这是最具区分度的设置。
  - 报告结果时同时给出逐数据集明细与跨数据集平均，避免仅报平均而掩盖域间差异（如中文 ECDT、长文本 20NG 的异常表现）。
  - 若以 LLM 为骨干，应固定并公开骨干版本、提示/模板与后处理打分实现，否则跨论文比较仍会失真。

## 11. 总体评价

BOLT 的核心贡献不在于提出某个 SOTA 方法，而在于**把碎片化的 OTC 评测收敛为一套可复现、可扩展、覆盖三代方法的标准化协议**，并用系统实验揭示了“闭集偏置”“LLM 规模非单调”“校准有效”等具有普遍意义的经验规律；其主要短板在于统计严谨性、任务假设的现实性以及 LLM 方法的成本透明度。作为基准与工具包，它更可能成为后续 OTC 研究的**对照基线与实验基础设施**，而非终点。

（完）
