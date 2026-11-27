---
title: "SemPA: Improving Sentence Embeddings of Large Language Models through Semantic Preference Alignment"
title_zh: SemPA：通过语义偏好对齐提升大语言模型的句向量表示
authors: "Ziyang Chen, Zhenxuan Huang, Yile Wang, Weiqin Wang, Lu Yin, Hui Huang"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://aclanthology.org/2026.findings-acl.1858.pdf"
tags: ["query:ai-se"]
score: 6.0
evidence: 通过语义偏好对齐改进大模型句向量表示
tldr: 现有基于生成式大模型的句向量方法或依赖固定提示模板缺乏优化，或改动模型结构损害生成能力。SemPA提出语义偏好对齐，在保持生成能力的同时利用句子级直接偏好优化提升句表示质量。实验表明其性能优于既有方法，为NLP中的表示学习提供了一种兼顾生成与嵌入的新思路。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1858/fig-001.webp\", \"caption\": \"\", \"page\": 4, \"index\": 1, \"width\": 426, \"height\": 474}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1858/fig-002.webp\", \"caption\": \"\", \"page\": 4, \"index\": 2, \"width\": 399, \"height\": 400}]"
motivation: 现有生成式大模型句向量方法或缺乏优化、或损害模型生成能力。
method: 提出句子级语义偏好对齐，在保持生成能力前提下优化句表示。
result: 在句向量任务上取得优于固定模板与改结构方法的性能。
conclusion: 表明偏好对齐可兼顾大模型生成能力与表示质量。
---

## Abstract
Traditional sentence embedding methods employ token-level contrastive learning on non-generative pre-trained models. Recently, there have emerged embedding methods based on generative large language models (LLMs). These methods either rely on fixed prompt templates or involve modifications to the model architecture. The former lacks further optimization of the model and results in limited performance, while the latter alters the internal computational mechanisms of the model, thereby compromising its generative capabilities. We propose SemPA, a novel approach that boosts the sentence representations while preserving the generative ability of LLMs via semantic preference alignment. We leverage sentence-level Direct Preference Optimization (DPO) to efficiently optimize LLMs on a paraphrase generation task, where the model learns to discriminate semantically equivalent sentences while preserving inherent generative capacity. Theoretically, we establish a formal connection between DPO and contrastive learning under the Plackett-Luce model framework. Empirically, experimental results on both semantic textual similarity tasks and various benchmarks for LLMs show that SemPA achieves better semantic representations without sacrificing the inherent generation capability of LLMs.

---

## 论文详细总结（自动生成）

# SemPA：通过语义偏好对齐提升大语言模型的句向量表示——论文深度总结

## 1. 核心问题与研究背景

- **句向量（sentence embedding）是 NLP 的基础设施**，服务于文本分类、聚类、检索等下游任务。传统做法是在 BERT/RoBERTa 等**编码器模型**上做 token 级对比学习（SimCSE 等），依赖 `[CLS]` 或池化隐状态。
- **生成式 LLM 句向量方法存在两条路线，但各有硬伤**：
  - **提示工程路线**（PromptEOL、MetaEOL、Contrastive Prompting）：不训练模型，仅靠模板提取最后一层末 token 隐状态。优点是保留生成能力，缺点是**缺乏进一步优化，性能天花板明显**。
  - **改结构路线**（LLM2Vec、Token Prepending、Hierarchical Token Prepending）：修改注意力模式或在层间插入句向量，虽能提升表示质量，但**侵入式改动破坏了模型原本的生成机制与生成能力**。
- **核心矛盾**：如何在不牺牲 LLM 生成能力、不改动模型架构的前提下，显著提升其句向量质量？
- **论文的整体含义**：作者主张把"偏好对齐"（原本用于真实性/安全性对齐）迁移到表示学习，提出 **SemPA**——一种**句子级、轻量、非侵入式**的语义偏好对齐方法，并试图从理论上说明"偏好对齐为何能像对比学习一样改善表示"。

## 2. 方法论

### 2.1 核心思想
不直接让模型做"输入→释义"的序列生成（那会让模型退化成释义模型），而是让模型在**给定锚句的条件下，偏好生成语义等价的句子、排斥语义矛盾的句子**，从而在句子级别习得细粒度语义判别力；训练后仍用 PromptEOL 模板提取句向量。

### 2.2 关键流程（三步）

- **（a）释义生成偏好数据构造**
  - 复用 NLI 数据集（即 SimCSE 所用的 275K 三元组数据），遵循 Gao et al. (2021) 的做法：
    - 前提（premise）→ 锚句 `x*`
    - 蕴含（entailment）句 → 偏好回答 `y+`
    - 矛盾（contradiction）句 → 被拒回答 `y-`
  - 与"释义识别"（分类头判别）不同，本文把它转化为**释义生成任务**，要求模型具备细粒度语义理解。

- **（b）语义 DPO 训练**
  - 将锚句填入释义指令模板 `T_para`：
    > `Keep the same meaning of this sentence: "x*", while making some changes.`
  - 以 `T_para(x*)` 作为 DPO 中的输入 `x`，`y+` 作 `y_w`，`y-` 作 `y_l`，套用标准 DPO 损失：
    - `L_DPO = -E[ log σ( β·log(π_θ(y_w|x)/π_ref(y_w|x)) − β·log(π_θ(y_l|x)/π_ref(y_l|x)) ) ]`
  - 等价改写为 softmax 形式：`L = -E[ log( e^{β log π_θ(y_w|x)/π_ref(y_w|x)} / ( e^{β log π_θ(y_w|x)/π_ref(y_w|x)} + e^{β log π_θ(y_l|x)/π_ref(y_l|x)} ) ) ]`，这一形式与对比学习的 InfoNCE 结构同构。

- **（c）句向量提取**
  - 对齐后的模型 `M_SemPA` 沿用 PromptEOL 模板：
    > `This sentence: "S" means in one word: "`
  - 取最后一层**最后一个 token 的隐状态**作为句向量：`Emb(S) = h^L_last`。

### 2.3 理论贡献：对比学习与 DPO 的统一视角
- 二者都可视为 **Plackett–Luce 模型**的特例：完整排序概率为 `P(σ|x) = ∏_k exp(s_θ(x,y_(k))) / Σ_{j≥k} exp(s_θ(x,y_(j)))`。
- 只关注"最优候选"的选择概率时，退化为 `P(y1 is best|x) = exp(s_θ(x,y1)) / Σ_j exp(s_θ(x,y_j))`。
- **唯一差别在打分函数与目标**（论文 Table 2）：
  - 对比学习：`s_θ = sim(e_θ(x), e_θ(y))`，候选集为 1 正 + N−1 负，目标为 InfoNCE。
  - DPO：`s_θ = β·log(π_θ(y|x)/π_ref(y|x))`，候选集为 1 偏好 + 1 被拒，目标为二分类 log-sigmoid。

## 3. 实验设计

### 3.1 数据与评测场景
- **训练数据**：SimCSE 所用 NLI 数据集（275K 三元组），实际按开发集表现取 **40K–80K 子集**。
- **主评测 benchmark**：7 个语义文本相似度（STS）数据集——STS12/13/14/15/16、STS-B、SICK-R，指标为 **Spearman 相关系数 ×100**。
- **生成能力评测 benchmark**（5 个维度）：
  - 数学推理 GSM8K、多任务理解 MMLU、常识推理 HellaSwag、阅读理解 DROP、真实性 TruthfulQA。
- **骨干模型**：LLaMA2-7B、LLaMA3-8B。

### 3.2 对比方法
- **编码器类**：BERT-avg、Sentence-T5-avg、PromptBERT、SBERT-NLI-base/large。
- **LLM 类**：LLM2Vec-LLaMA2（改结构 + 对比学习）、Mean Pooling、Echo Embedding、PromptEOL、Contrastive Prompting、Token Prepending。
- **生成能力对照**：额外训练一个"PromptEOL 表示 + 对比学习"的模型，与 SemPA 对比对生成能力的破坏程度。

## 4. 资源与算力

- **GPU**：4 张 **NVIDIA RTX 5090**。
- **微调方式**：LoRA（覆盖除 LM head 外所有线性层，rank r=8，α=32），**仅 0.3% 参数可训练**；框架为 SWIFT。
- **超参**：每步 batch 8，梯度累积 8（等效 batch 256）；AdamW，峰值学习率 1e-4，warmup 比例 0.05，后接余弦退火；每 20K 样本保存一次 checkpoint。
- **未明确说明**：论文**没有报告训练总时长、总 GPU 小时数、单次训练 epoch 数或能耗成本**，仅给出硬件配置与超参。

## 5. 实验数量与充分性评估

### 5.1 实验组数（约 8 类）
1. **主实验**：2 个骨干 × 7 个 STS 数据集 × 10+ 基线（Table 3）。
2. **生成能力实验**：2 个骨干 × 5 个任务 × 3 种状态（原始 / 对比学习 / SemPA）（Table 6）。
3. **训练数据规模消融**：0–27 万样本多个 checkpoint，在 STS-B dev 与 STS test 上曲线分析（Figure 3）。
4. **模板消融**：5 种释义模板 × 2 种向量提取模板（PromptEOL / Pretended CoT）× 2 个骨干（Table 4）。
5. **表示空间质量**：PCA 可视化（Figure 4）+ Uniformity / Isotropy 两项定量指标（Table 5）。
6. **词表对齐分析**：3 个样例的 top-10 对齐 token（Table 7）+ 10K 维基样本的 GAR 分数（0.185→0.324）。
7. **随机种子稳定性**：LLaMA3-8B 三次重复，均值 78.10，标准差 0.36（附录 B）。

### 5.2 充分性与公平性评价
- **优点**：
  - 覆盖"表示质量 + 生成能力"两个维度，直接回应了论文的核心动机（不牺牲生成能力），这是最有说服力的设计。
  - 有随机种子重复实验与标准差报告，稳定性可信。
  - 与 Token Prepending、Contrastive Prompting 等基线统一使用 PromptEOL 提取方式，控制变量较规范。
- **不足**：
  - **缺少关键消融**：没有"仅做释义任务 SFT（监督微调）"的对照，无法证明增益来自 DPO 的偏好结构而非仅仅"多训了一遍释义任务"；也未对 β、负样本构造方式（矛盾句 vs. 难负例挖掘）做消融。
  - **骨干单一**：仅两个 LLaMA 系列模型，未验证 Qwen、Mistral 等其他架构。
  - **语言单一**：仅英文 STS，无跨语言 / 多语言评测。
  - **下游任务缺失**：未评测检索（BEIR）、聚类、分类等真实应用场景，仅用 STS 相似度作代理。
  - **未与强嵌入模型正面比较**：作者自述"目标不是与 SOTA 嵌入模型竞争"，但因此也削弱了"可替代传统方案"这一论断的说服力。

## 6. 主要结论与发现

- **句向量性能显著提升**：LLaMA2-7B 平均 **77.69**（7 个数据集中 5 个最优），LLaMA3-8B 平均 **78.10**（6 个最优），优于 PromptEOL（70.03 / 71.90）、Contrastive Prompting、Token Prepending（77.19 / 75.34）等，并超过 SBERT-NLI-large（76.55）等编码器模型。
- **生成能力基本无损**：对比学习版本在生成任务上大幅崩塌（LLaMA2 平均 −7.59，LLaMA3 −17.71，GSM8K 从 55.80 跌至 9.86）；SemPA 反而平均 **+0.92 / +2.09**，TruthfulQA 提升 **9.18–10.77** 点。
- **数据高效**：40K–80K 样本即达最佳；超过 100K 后出现轻微"过度对齐"导致性能回落但仍高于基线。
- **表示空间改善**：SemPA 使 embedding 分布更各向同性（Uniformity 从 −1.0066 降至 −1.9139，Isotropy 从 0.4173 升至 0.4882），正负样本分离更清晰。
- **对齐更"语义化"**：top-10 对齐 token 从 `<0x0A>` 等无意义符号转为 `After / Master / August / member` 等实词，GAR 从 0.185 升至 0.324。
- **模型越强收益越大**：LLaMA3-8B 相对基线的提升幅度大于 LLaMA2-7B。

## 7. 优点（亮点）

- **视角新颖**：首次把偏好对齐（DPO）系统性地用于**改进 LLM 的句向量表示**，而非传统的安全性/真实性对齐，开辟了一条轻量、非侵入式的第三条路线。
- **"既要有要"的平衡做得好**：不改架构、不换注意力、只动 0.3% 参数，同时守住生成能力——这恰是改结构路线和纯提示路线都做不到的。
- **理论统一有解释力**：用 Plackett–Luce 框架把 InfoNCE 与 DPO 放在同一坐标系下，直观说明了"DPO 的 log-ratio 打分扮演了对比学习中相似度函数的角色"，为后续工作提供了可延展的分析工具。
- **数据成本极低**：直接复用现成 NLI 数据集构造偏好对，无需人工标注偏好、无需奖励模型、无需大规模高质量指令数据。
- **分析维度丰富**：不仅有主指标，还从几何性质（uniformity/isotropy）、词表对齐（GAR）、模板鲁棒性、数据规模曲线多个角度交叉验证结论，论证链条较完整。
- **诚实的定位**：明确声明不与 SOTA 嵌入模型比拼绝对性能，而是提供"轻量偏好对齐"的新思路，学术定位清晰。

## 8. 不足与局限

- **理论部分偏"重述"而非"证明"**：对比学习与 DPO 同属 Plackett–Luce 特例这一点在偏好优化文献中已被广泛讨论，本文的推导属于形式化对照，未给出"DPO 必然改善表示"的收敛性或泛化性保证。
- **缺少最关键的对照实验**：无 SFT-only 基线，难以排除"任何句子级释义训练都能带来类似增益"的可能；也无负样本类型、β 值、pairwise vs. listwise 的消融。
- **负样本质量受限**：直接用 NLI 的矛盾句作 `y-`，并非针对语义相似度挖掘的**难负例**，负例与锚句往往差异过大，可能限制了偏好信号的精细度。
- **实验覆盖不足**：仅 2 个 LLaMA 骨干、仅英文、仅 STS 代理任务；未涉及检索/聚类/分类等真实下游场景；GAR 分析只在 LLaMA2-7B 上做。
- **CoT 模板下 LLaMA2 性能下降未解释**：作者归因于"不同基座对 CoT 提示诱发的语义表示不同"，但未深入分析，属于悬而未决的现象。
- **TruthfulQA 大幅提升（+9~11）值得审慎看待**：该指标方差较大，且提升机制未被解释，存在偶然性或评测噪声风险。
- **应用限制**：需为每个骨干单独做一次 DPO 训练（虽轻量但非 training-free）；推理时仍依赖固定 PromptEOL 模板，模板敏感性虽被测试但未被消除；DPO 需同时加载策略模型与参考模型，显存开销高于纯提示方法。
- **作者自述的局限**：数据规模与质量、自动提示优化、以及从 pairwise DPO 升级到 listwise 偏好优化（如 LiPO）是明确的未来方向。

（完）
