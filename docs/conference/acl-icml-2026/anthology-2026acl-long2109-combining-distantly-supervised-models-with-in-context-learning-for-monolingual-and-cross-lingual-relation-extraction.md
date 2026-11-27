---
title: Combining Distantly Supervised Models with In Context Learning for Monolingual and Cross-Lingual Relation Extraction
title_zh: 结合远程监督模型与上下文学习的单语及跨语言关系抽取
authors: "Vipul Kumar Rathore, Malik Hammad Faisal, Parag Singla, Mausam ."
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://aclanthology.org/2026.acl-long.2109.pdf"
tags: ["query:ai-se"]
score: 6.0
evidence: 结合远程监督与上下文学习的关系抽取
tldr: 远程监督关系抽取需从含噪包级标注学习并做句级预测，而将其与大模型上下文学习结合仍待探索，主要难点是噪声标注导致大模型难以正确学习关系语义。作者提出HYDRE混合框架，先用远程监督模型筛出候选关系，再通过动态示例检索进行上下文学习。该框架提升了单语与跨语言关系抽取的表现，展示了传统模型与大模型协同的潜力。
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long2109/fig-001.webp\", \"caption\": \"\", \"page\": 3, \"index\": 1, \"width\": 1105, \"height\": 786}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long2109/fig-002.webp\", \"caption\": \"\", \"page\": 8, \"index\": 2, \"width\": 640, \"height\": 480}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long2109/fig-003.webp\", \"caption\": \"\", \"page\": 19, \"index\": 3, \"width\": 312, \"height\": 908}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long2109/fig-004.webp\", \"caption\": \"\", \"page\": 23, \"index\": 4, \"width\": 281, \"height\": 820}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long2109/fig-005.webp\", \"caption\": \"\", \"page\": 23, \"index\": 5, \"width\": 321, \"height\": 790}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long2109/fig-006.webp\", \"caption\": \"\", \"page\": 25, \"index\": 6, \"width\": 945, \"height\": 695}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long2109/fig-007.webp\", \"caption\": \"\", \"page\": 25, \"index\": 7, \"width\": 945, \"height\": 695}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long2109/fig-008.webp\", \"caption\": \"\", \"page\": 25, \"index\": 8, \"width\": 945, \"height\": 695}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long2109/fig-009.webp\", \"caption\": \"\", \"page\": 25, \"index\": 9, \"width\": 945, \"height\": 695}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long2109/fig-010.webp\", \"caption\": \"\", \"page\": 25, \"index\": 10, \"width\": 945, \"height\": 695}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long2109/fig-011.webp\", \"caption\": \"\", \"page\": 25, \"index\": 11, \"width\": 945, \"height\": 695}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long2109/fig-012.webp\", \"caption\": \"\", \"page\": 26, \"index\": 12, \"width\": 945, \"height\": 695}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long2109/fig-013.webp\", \"caption\": \"\", \"page\": 26, \"index\": 13, \"width\": 1018, \"height\": 695}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long2109/fig-014.webp\", \"caption\": \"\", \"page\": 26, \"index\": 14, \"width\": 945, \"height\": 695}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long2109/fig-015.webp\", \"caption\": \"\", \"page\": 26, \"index\": 15, \"width\": 945, \"height\": 695}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long2109/fig-016.webp\", \"caption\": \"\", \"page\": 26, \"index\": 16, \"width\": 945, \"height\": 695}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long2109/fig-017.webp\", \"caption\": \"\", \"page\": 26, \"index\": 17, \"width\": 945, \"height\": 695}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long2109/fig-018.webp\", \"caption\": \"\", \"page\": 27, \"index\": 18, \"width\": 777, \"height\": 570}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long2109/fig-019.webp\", \"caption\": \"\", \"page\": 27, \"index\": 19, \"width\": 622, \"height\": 452}]"
motivation: 远程监督关系抽取标注噪声大，且其与大模型上下文学习的结合尚待探索。
method: 提出HYDRE框架，先用远程监督模型选出候选关系，再通过动态示例检索进行上下文学习。
result: 该框架在单语与跨语言关系抽取任务上取得优于基线的表现。
conclusion: HYDRE表明传统远程监督模型与大模型上下文学习可有效协同提升关系抽取效果。
---

## Abstract
Distantly Supervised Relation Extraction (DSRE) remains a long-standing challenge in NLP, where models must learn from noisy bag-level annotations while making sentence-level predictions. While existing state-of-the-art (SoTA) DSRE models rely on task-specific training, their integration with in-context learning (ICL) using large language models (LLMs) remains underexplored. A key challenge is that the LLM may not learn relation semantics correctly, due to noisy annotation.In response, we propose HYDRE – HY brid D istantly Supervised R elation E xtraction framework. It first uses a trained DSRE model to identify the top- k candidate relations for a given test sentence, then uses a novel dynamic exemplar retrieval strategy that extracts reliable, sentence-level exemplars from training data, which are then provided in LLM prompt for outputting the final relation(s).We further extend HYDRE to cross-lingual settings for RE in low-resource languages. Using available English DSRE training data, we evaluate all methods on English as well as a newly curated benchmark covering four diverse low-resource Indic languages - Oriya, Santali, Manipuri, and Tulu. HYDRE achieves up to 20 F1 point gains in English and, on average, 17 F1 points on Indic languages over prior SoTA DSRE models and naive prompting baselines. Detailed ablations exhibit HYDRE ’s efficacy compared to other prompting strategies.

---

## 论文详细总结（自动生成）

# 论文总结：HYDRE —— 结合远程监督模型与上下文学习的单语及跨语言关系抽取

## 1. 核心问题与研究背景

- **任务背景**：关系抽取（RE）旨在识别文本中实体对之间的语义关系，是知识库构建、问答等下游应用的基础。监督式 RE 依赖昂贵的句级标注，而远程监督关系抽取（DSRE）通过将文本与知识库三元组对齐，自动生成弱标注数据，大幅降低标注成本。
- **核心矛盾**：DSRE 的训练监督是**包级（bag-level）且含噪的**——同一实体对的所有句子被归入一个包，并继承 KB 中该实体对的全部关系；但推理通常在**句级（sentence-level）**进行。这种粒度错配加上标签噪声，使现有 SoTA 模型（如 PARE、CIL）容易混淆细粒度关系（如 `Nationality` vs. `Place_of_Birth`、`Founder` vs. `CEO`）。
- **研究空白**：现有 DSRE 方法主要依赖对 BERT/RoBERTa 等中等规模模型的任务特定微调，**LLM 的上下文学习（ICL）能力在该任务上几乎未被系统探索**。直接套用 LLM 面临两大障碍：噪声远程监督会污染示例质量，且缺乏干净的句级示例，导致 ICL 失效。
- **核心洞察**：作者初步分析发现，强 DSRE 模型（如 PARE）在句级 Recall@5 上已达约 85%（英语）和 70%（印度语言），说明其适合作为**高召回候选生成器**，而 LLM 可作为**精度导向的选择器**。由此提出将二者结合的混合框架 HYDRE。

## 2. 方法论：HYDRE 框架

### 2.1 核心思想
- 采用「**DSRE 模型做高召回候选筛选 + LLM 做精排消歧**」的混合范式：先用微调 DSRE 模型过滤明显负例，再由 LLM 在精心构造的 ICL 示例引导下输出最终关系。
- 关键创新在于**从含噪远程监督数据中动态抽取可靠的句级示例**，解决 ICL 示例质量问题。

### 2.2 三阶段示例选择流程（Algorithm 1）

- **Stage 1：候选关系选择**
  - 训练好的 DSRE 模型（如 PARE）对查询句 $q$ 的每个关系 $r$ 给出置信度 $f_{PARE}(q,r)$。
  - 取置信度最高的 top-$k$ 个关系构成候选集 $R'$，过滤明显负例、缩短 prompt。

- **Stage 2：包选择（Bag Selection）**
  - 对每个候选关系 $r$，从标注包含 $r$ 的包集合 $\mathcal{B}_r$ 中选出最相关的包 $B_r$。
  - 打分函数融合语义相似度与 DSRE 置信度：
    $$\text{score}(B_j, r) = (1-\lambda)\,\text{sim}(q, B_j) + \lambda\, f_{PARE}(B_j, r)$$
    其中 $\text{sim}(q,B_j)=\max_{s\in B_j}\text{sim}(q,s)$，$f_{PARE}(B_j,r)=\max_{s\in B_j}f_{PARE}(s,r)$。
  - 超参 $\lambda$ 控制语义相似度与标签置信度的权衡，按语言在开发集上分别调优（英语 $\lambda=0.5$，印度语言 translate-train $\lambda=0.1$）。

- **Stage 3：句子选择（Sentence Selection）**
  - 从选中包 $B_r$ 中抽取单句 $s_r$ 作为示例，先计算覆盖度：
    $$c(s)=\sum_{r_a\in\text{labelset}(B_r)} \mathbb{I}[f_{PARE}(s,r_a)>\tau]$$
  - 在覆盖度最大的句子集合中，选聚合置信度 $\sum_{r_a}f_{PARE}(s,r_a)$ 最高者。
  - **设计动机**：① 支持多标签场景（包中共同出现但不在 $R'$ 中的关系也被保留进 prompt）；② 提升标签多样性/覆盖度；③ 用多标签聚合置信度而非单标签噪声置信度来筛选强证据句。

- **示例排序与提示**：示例按 $f_{PARE}(q,r)$ 升序排列，使最相关候选靠近查询（缓解位置偏差）。Prompt 包含任务指令、候选关系及定义、ICL 示例、查询四部分；输出用部分字符串匹配解析，无匹配则判为 "NA"。

### 2.3 跨语言扩展
- 用英语 DSRE 训练数据，在三种迁移设置下适配低资源语言：
  - **English-only**：仅用英语数据；印度语言查询时因 PARE 无跨语言置信度，改用多语言编码器 BGE-M3 做纯语义检索。
  - **Translate-train**：将英语训练数据译为目标语言，微调 PARE-X（置信度）与 CIL-X（语义检索）。
  - **Translate-test**：将目标语言测试查询译为英语后走标准英语流程。

### 2.4 新基准构建
- 为 Oriya（奥里亚语，印欧语系/奥里亚文）、Santali（桑塔利语，南亚语系/Ol Chiki 文）、Manipuri（曼尼普尔语，藏缅语系/Meitei 文）、Tulu（图卢语，达罗毗荼语系/卡纳达文）四种低资源印度语言构建金标准测试集。
- 从 NYT-10m 测试集分层采样 538 句多标签查询（722 个标签，含 30 个 "NA"），用 CODEC+IndicTrans2 翻译并做实体投影（Tulu 用 Google Translate），由母语者人工校验，超 70% 无需修正，标注者间一致性超 90%。

## 3. 实验设计

### 3.1 数据集与场景
- **主数据集**：NYT-10m（英语 + 4 种印度语言翻译版），句级与包级两种评估。
- **泛化数据集**：Wiki-20m（81 种关系的大本体），结果放附录。
- **评估场景**：英语单语 + 三种跨语言迁移设置（English-only / Translate-train / Translate-test）。

### 3.2 对比基线
- **监督 DSRE 模型**：HFMRE、HiCLRE、CIL、PARE，及其目标语言版本 PARE-X、CIL-X。
- **0-shot prompting**：Qwen3-235B-A22B、GPT-4o、Llama3.1-8B、Llama3.1-8B-FT；含 Direct 与 Definition-based 两种变体。
- **Few-shot 示例检索基线**：Random-K、TopK-sim、LM-MMR（多样性感知 MMR）。

### 3.3 评估指标
- 报告 micro-F1 与 macro-F1；因 LLM 方法无校准置信度，省略 AUC；用 McNemar 检验做 micro-F1 显著性检验。

## 4. 资源与算力

- **本地推理与微调**：单块 **NVIDIA A100 40GB GPU** 节点。
- **Llama3.1-8B 微调**：LoRA（`lora_alpha=64, r=16, dropout=0.0`），Cosine 学习率调度、10% warmup，`per_device_train_batch_size=8`、梯度累积 4、最大 5000 步，NYT-10m 共 41624 个包，约等效 4 个 epoch。
- **PARE-X 训练**：先对 mBERT 在目标语言语料上持续预训练（扩充最多 10000 个新词表 token），再用 adapter 微调。
- **API 调用**：Qwen3 经 TogetherAI、GPT-4o 经 OpenAI API 推理。
- **未明确说明**：论文未报告总训练时长、总 GPU 小时数、API 调用总 token 成本等，算力规模描述较为简略。

## 5. 实验数量与充分性

- **实验规模**：
  - 英语 + 4 种印度语言 × 3 种迁移设置，覆盖 4 个 LLM（2 个开源、2 个闭源/微调），主表即含数十种配置。
  - 消融实验：6 类变体（去候选选择、去包选择、去句子选择、去语义相似度、去 PARE 置信度、去 ICL），并在多个 LLM 上重复；附录还给出逐语言消融（Tables 14–17）。
  - 附加分析：k 敏感性分析（k=5~10 峰值）、包级评估鲁棒性、Wiki-20m 泛化、混淆矩阵与 12 对易混关系分析、多标签覆盖召回、缺失候选瓶颈分析、Stage 3 设计消融、翻译质量与标注者间一致性评估。
- **充分性评价**：整体实验**相当充分**，覆盖多语言、多模型、多设置、多消融，并兼顾定量与定性分析。
- **公平性**：基线选择较全面（监督模型、0-shot、多种 few-shot 检索），超参在开发集上统一调优，使用 McNemar 检验。但需注意：不同 LLM 的能力差异较大，部分设置下消融因 prompt 过长无法进行（表中标 "–"），跨语言各语言结果差异悬殊（如 Santali、Manipuri 分数明显偏低），平均值的代表性需谨慎解读。

## 6. 主要结论与发现

- **性能提升**：HYDRE 在英语上最高提升约 **20 F1**，在印度语言上平均提升约 **17 F1**，稳定超过 SoTA DSRE 模型与朴素提示基线。GPT-4o 在英语达 63/60（micro/macro F1），翻译测试设置下达 56/54。
- **小模型受益更大**：Llama3.1、Qwen3 等较弱开源模型获得最高 +14 F1 增益，说明示例引导对弱 LLM 尤为有效。
- **跨语言有效**：即便零样本下 GPT-4o 在印度语言仅 22–33 F1，HYDRE 仍带来 +3~+11 F1；translate-train 下微调 Llama 甚至超过 PARE-X 约 +15 micro-F1。
- **组件互补**：英语中语义相似度主导（去除掉最多 7 F1），印度语言 translate-train 中 DSRE 置信度更关键（去除掉显著下降）；去 ICL 会掉 7（英语）至 12（跨语言）F1。
- **候选选择必要性**：给全部 25 个关系虽性能相当，但 prompt 成本约 5 倍，且弱模型显著退化。
- **句子选择价值**：提供整包会掉最多 6 micro/10 macro F1，说明只需少量精选句即可完成精准推理。
- **包级评估**：reduced-bag 表示比 full-bag 提升约 3 micro/7 macro F1，同时 token 数近乎减半（2451→1242）。
- **主要错误类型**：① 位置偏差（34% 错误为选中 PARE top-1）；② 候选瓶颈（约 14% 查询 gold 不在 top-5，此时落后零样本）；③ 持续语义重叠（如 nationality vs. ethnicity）。

## 7. 优点

- **范式创新**：首次系统地将 LLM 的 ICL 引入 DSRE 推理，提出「DSRE 高召回 + LLM 精排」的混合范式，并可与「LLM-as-Judge」框架对应。
- **示例检索设计精巧**：三阶段流水线用「置信度 × 语义相似度」联合打分 + 覆盖度/聚合置信度选句，显式利用远程监督的多标签特性，兼顾去噪与多样性。
- **基准贡献**：构建并开源 4 种类型学差异显著（四大语系、四种文字）的低资源印度语言金标准测试集，填补多语言 DSRE 空白。
- **实验扎实**：多语言 × 多设置 × 多模型 × 多消融，辅以混淆矩阵、错误分类、多标签召回、缺失候选分析等细致诊断。
- **实用价值**：揭示本地微调开源 LLM 在极低资源语言上可优于 GPT-4o 的成本-性能权衡，具备部署参考意义。

## 8. 不足与局限

- **成本与延迟**：从大包中检索示例开销高，低资源语言因 token 膨胀（token fertility）问题更严重；prompt 长度受限导致部分消融无法在印度语言上完成。
- **领域覆盖有限**：未测试生物医学、金融等低资源且语义关系更复杂的领域；仅覆盖 4 种印度语言，受限于 RE 数据可得性。
- **未验证监督场景**：核心的标签感知示例选择与三阶段过滤是否能推广到全监督/人工标注 RE 尚未验证。
- **固有误差**：位置偏差（近因偏差）导致约 34% 错误集中于 top-1 候选；约 14% 查询存在候选瓶颈；部分语义重叠关系（ethnicity/nationality、business/location vs. place_founded）仍持续混淆，且部分与噪声金标本身有关。
- **翻译噪声**：translate-test 因翻译引入轻度性能下降；印度语言基准依赖机器翻译 + 人工校验，仍可能存在残余偏差。
- **算力报告不完整**：未给出总训练时长、GPU 小时或 API 成本，复现与成本评估的透明度有限。

（完）
