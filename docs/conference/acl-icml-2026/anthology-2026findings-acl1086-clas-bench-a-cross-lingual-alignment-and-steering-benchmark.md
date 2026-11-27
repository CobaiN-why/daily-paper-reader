---
title: "CLaS-Bench: A Cross-Lingual Alignment and Steering Benchmark"
title_zh: CLaS-Bench：跨语言对齐与引导基准
authors: "Daniil Gurgurov, Yusser Al Ghussin, Tanja Baeumel, Cheng-Ting Chou, Patrick Schramowski, Marius Mosbach, Josef van Genabith, Simon Ostermann"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://aclanthology.org/2026.findings-acl.1086.pdf"
tags: ["query:ai-se"]
score: 5.0
evidence: 多语言大模型行为引导评测基准
tldr: 通过推理期操纵内部表示的语言引导是比提示或微调更高效可解释的适配手段，但此前缺乏量化其效果的基准与评测协议。作者提出CLaS-Bench，一个覆盖32种语言的平行问题基准，用于系统评测大模型的语言强制行为及多种引导技术，包括残差流DiffMean干预与探针方法。实验给出不同引导方法的比较结果，揭示了其在多语言场景下的有效性与局限。该基准为多语言NLP与大模型行为控制研究提供了标准化评测工具。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1086/fig-001.webp\", \"caption\": \"\", \"page\": 32, \"index\": 1, \"width\": 884, \"height\": 849}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1086/fig-002.webp\", \"caption\": \"\", \"page\": 32, \"index\": 2, \"width\": 884, \"height\": 849}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1086/fig-003.webp\", \"caption\": \"\", \"page\": 33, \"index\": 3, \"width\": 884, \"height\": 849}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1086/fig-004.webp\", \"caption\": \"\", \"page\": 33, \"index\": 4, \"width\": 884, \"height\": 849}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1086/fig-005.webp\", \"caption\": \"\", \"page\": 34, \"index\": 5, \"width\": 884, \"height\": 849}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1086/fig-006.webp\", \"caption\": \"\", \"page\": 34, \"index\": 6, \"width\": 884, \"height\": 849}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1086/fig-007.webp\", \"caption\": \"\", \"page\": 35, \"index\": 7, \"width\": 884, \"height\": 849}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1086/fig-008.webp\", \"caption\": \"\", \"page\": 35, \"index\": 8, \"width\": 884, \"height\": 849}]"
motivation: 语言引导技术虽高效可解释，但缺少专门基准来量化其对大模型多语言行为的效果。
method: 构建覆盖32种语言的平行问题基准，系统评测残差流干预、探针等多种引导方法。
result: 实验比较了各类引导技术在大模型语言强制行为上的效果差异。
conclusion: 该基准为多语言NLP中的大模型行为控制研究提供了标准化评测协议。
---

## Abstract
Understanding and controlling the behavior of large language models (LLMs) is an increasingly important topic in multilingual NLP. Beyond prompting or fine-tuning, language steering , i.e., manipulating internal representations during inference, has emerged as a more efficient and interpretable technique for adapting models to a target language. Yet, no dedicated benchmarks or evaluation protocols exist to quantify the effectiveness of steering techniques. We introduce CLaS-Bench , a lightweight parallel-question benchmark for evaluating language-forcing behavior in LLMs across 32 languages, enabling systematic evaluation of multilingual steering methods. We evaluate a broad array of steering techniques, including residual-stream DiffMean interventions, probe-derived directions, language-specific neurons, PCA/LDA vectors, Sparse Autoencoders, and prompting baselines. Steering performance is measured along two axes: language control and semantic relevance, combined into a single harmonic-mean steering score. We find that across languages simple residual-based DiffMean method consistently outperforms all other methods. Moreover, a layer-wise analysis reveals that language-specific structure emerges predominantly in later layers and steering directions cluster based on language family. CLaS-Bench is the first standardized benchmark for multilingual steering, enabling both rigorous scientific analysis of language representations and practical evaluation of steering as a low-cost adaptation alternative.

---

## 论文详细总结（自动生成）

# CLaS-Bench：跨语言对齐与引导基准——论文结构化总结

## 1. 核心问题与研究动机

- **背景**：理解并控制大语言模型（LLM）行为是多语言 NLP 的重要议题。除提示（prompting）与微调（fine-tuning）外，**语言引导（language steering）**——在推理期直接操纵模型内部表示——被视为更高效、更可解释的多语言适配手段。
- **研究空白**：现有引导评测基准（如 AxBench、MIB、Steer-Bench）几乎全部聚焦英语与"概念级"引导任务（如真实性、毒性、人口群体风格），**没有专门针对多语言/跨语言语言引导的标准化基准或评测协议**。
- **核心问题**：
  1. 与提示等成熟方法相比，引导在控制输出语言上效果如何？
  2. 考虑到 LLM 预训练以英语为主，引导在不同语言上是否同样有效？
- **整体含义**：可解释性研究长期以英语为中心；将语言引导研究扩展到广泛语言集合，对科学理解与"可操作的可解释性"（actionable interpretability）都至关重要。CLaS-Bench 是**首个多语言引导标准化基准**。

---

## 2. 方法论

### 2.1 基准构造

- **语言覆盖**：32 种类型学与地理上多样的语言，兼顾高/低资源、不同语系与文字系统（如藏语、马尔他语、格鲁吉亚语、哈萨克语、斯瓦希里语等）。
- **评测数据**：从 Vicuna 数据集选取 70 个开放式问题（原由 Tang et al. 2024 引入），人工标注为 5 类领域（推理、知识、个人观点、创意、专业写作），并用 Google Translate API 译为其余 31 种语言。
- **质量保障**：由母语者逐条校对，强调语义忠实、流利地道、语气一致（附录 A 给出协议与伦理说明）。
- **规模**：每个目标语言可配 70×32 = **2,240 个实例**，总计超过 **71,680 个跨语言问答对**。

### 2.2 任务定义

给定源语言 $s$ 的问题 $x_s$，目标是生成目标语言 $t$ 的答案 $y_t$。引导方法 $S(\cdot)$ 要么改写输入（提示类），要么在层 $\ell$ 对隐藏表示 $h_\ell$ 施加干预 $\delta_\ell$，模型参数 $\theta$ 保持固定：

$$\hat{y}_t = M_\theta(S(x_s))$$

目标：输出为语言 $t$，同时保持与问题的语义相关性。

### 2.3 评测指标（双轴 + 调和平均）

- **语言强制成功率（LFS）**：用 FastText LID 分类器检测输出语言，统计目标语言输出占比。
- **输出相关性（OR）**：用 **Qwen-3-8B 作 LLM-as-a-judge**，按 0/1/2 三档打分后归一化；评判提示明确要求"忽略语言、只看内容"。
- **语言引导分数（LSS）**：两指标的调和平均
  $$LSS = \frac{2 \cdot LFS \cdot OR}{LFS + OR}$$
  对任一指标极低的情况施加惩罚。

### 2.4 被评测的引导方法（共 8 类）

| 类别 | 方法 | 关键机制 |
|---|---|---|
| 基线-I（E） | 英语提示指定语言 | 问题 + "Respond in German" |
| 基线-II（T） | 目标语言提示指定语言 | 问题 + "Antworte auf Deutsch" |
| 神经元（⊙ LAPE） | 语言敏感神经元 | 每语言 10M token 统计激活概率，熵过滤选神经元，做加性/替换干预，可选零化非目标神经元 |
| 残差 DiffMean（⃗∆） | 残差流均值差向量 | $\delta_\ell = h_\ell + \alpha \cdot \vec{\Delta}_\ell/\|\vec{\Delta}_\ell\|_2$，$\vec{\Delta}_\ell = \bar{h}^{target}_\ell - \bar{h}^{source}_\ell$ |
| 探针（w） | 线性探针权重方向 | 二分类探针（目标 vs 负例语言），100K 样本，取权重向量方向 |
| PCA（u） | 主子空间重构 | 500K token 激活，取 top-$k{=}20$ 主成分投影重构 |
| LDA（v） | 线性判别方向 | $v_\ell = \Sigma_w^{-1}(\mu_{tgt}-\mu_{other})$，100K token |
| SAE-DiffMean（⃗∆S） | 稀疏自编码器潜空间均值差 | 用预训练 SAE 的 JumpReLU 编码，在潜空间做 DiffMean 干预后解码，并加重构误差修正项 |

所有引导向量均做 $\ell_2$ 归一化，以解耦"方向"与"强度 $\alpha$"。

---

## 3. 实验设计

- **模型**：Llama-3.1-8B-Instruct（主力）与 Aya-Expanse-8B（多语言替代模型）；主表报告 Llama，Aya 结果在附录 K。
- **数据来源**：评测用 32 语言 × 70 平行问题；引导向量估计数据来自 **CulturaX** 语料。
- **对比对象**：上述 8 类方法（含 2 个提示基线），每方法按消融选出最佳层与强度（附录 J 给出超参表）。
- **消融维度**：
  - 干预层（约 0–31 层逐层扫描）
  - 引导强度 $\alpha$（1.0 / 2.5 / 5.0，SAE 用 5/10/15）
  - LAPE 的 4 种干预配置（加性/替换 × 是否零化非目标神经元）与改变神经元比例（1%–5%）
- **可解释性分析**：余弦相似度随层变化、探针损失/准确率、LAPE 神经元层分布、LDA 准确率与 Fisher 比、语言族聚类热图、跨语言强制矩阵（附录 L）、定性样例（附录 M）。

---

## 4. 资源与算力

- **论文正文与附录均未明确说明 GPU 型号、数量或训练/推理总时长**，仅能从方法描述间接推断计算量：
  - DiffMean 与 LAPE 每语言处理 **10M token**；PCA 为 **500K**；LDA 与探针为 **100K** 样本。
  - 评测规模为每目标语言 2,240 实例 × 32 语言 × 2 模型。
- 作者在"局限性"中承认，**受计算约束**才采用不同方法不同数据量，并称遵循各方法既有实践。
- 结论：**算力披露不充分**，无法据此复现其计算预算或评估碳成本。

---

## 5. 实验数量与充分性

**规模概览**：
- 主实验：2 个模型 × 32 语言 × 8 类方法，报告 LFS、OR、LSS 三套逐语言指标（正文表 2 + 附录表 7–11）。
- 消融：层 × 强度 × 方法配置的二维网格扫描（正文图 2、附录图 15），覆盖 5 类表示方法。
- 可解释性：4 类工具（DiffMean 余弦、探针、LAPE 神经元、LDA）在两模型上的层间分析（图 3、图 14），外加 6 组语言向量相似度热图与 8 组跨语言强制矩阵。
- 定性：4 组源→目标语言对的生成样例对比（表 12–15）。

**充分性与公平性评估**：
- ✅ **覆盖广**：32 语言、双模型、8 方法、逐语言报告，是同类工作中覆盖最广的之一。
- ✅ **指标设计合理**：双轴 + 调和平均可惩罚"只换语言不管内容"的退化行为；评判提示明确排除语言因素，降低混淆。
- ⚠️ **公平性隐忧**：
  - 各方法使用的数据量差异巨大（10M vs 500K vs 100K），作者自认"可能影响可比性"。
  - 每种方法仅报告"最佳配置"下的分数，未给置信区间或多种子方差，方法间差距的统计显著性不明。
  - SAE 仅限 5 个预训练层（4/12/18/20/25），且 Aya 模型无可用 SAE，跨模型对比不完整。
  - 相关性由单一 LLM 评判（Qwen-3-8B），未做人评校准或评判者一致性检验。

---

## 6. 主要结论与发现

1. **残差 DiffMean 全面领先**：Llama-3.1-8B 上平均 LSS 达 **84.5%**，显著超过两个提示基线（67.7% / 67.3%）；32 种语言中 **19 种超过 90%**。
2. **LAPE 次之（80.1%）**，证明语言特异神经元确实可用于控制输出语言，但跨语言方差更大。
3. **提示基线存在系统性失败**：如英语、藏语、波斯语等目标语言上，模型会忽略显式语言指令（表 3 给出俄语输入 + "Respond in English" 仍输出俄语的实例）。
4. **SAE 引导表现中等（42.3%）**：在高资源语言上好，在日语、斯洛伐克语上差；作者推测与 SAE 重构误差及训练语料语言覆盖有关。
5. **监督方法反而不如无监督**：探针（48.6%）与 LDA（23.6%）显著低于无监督的 DiffMean 与 LAPE；PCA 最差（15.1%）。作者认为监督目标可能过拟合语言特异特征，而均值差捕捉到更通用的语言方向。
6. **层与强度存在交互**：早期层用低强度（$\alpha{=}1.0$）即可达 80%+，后期层需更高强度（$\alpha{=}5.0$ 在约第 20 层达峰）；晚期层高强度干预对输出质量破坏小，早期层高强度会严重损害连贯性。
7. **语言信息集中于后层**：余弦相似度在第 22–32 层最低（可分性最强），探针从第 14 层起准确率 >99%，LAPE 神经元集中于 24–28 层，LDA 准确率与 Fisher 比也在后层达峰——多工具证据收敛于"前层语言无关、后层语言特异"的层级加工观点。
8. **语言族呈几何聚类**：罗曼、日耳曼、斯拉夫语族内部向量余弦相似度高；LAPE 神经元重叠主要发生在语族内部。这意味着**跨语族引导可能需要更大干预、更易损伤质量**。

---

## 7. 优点

- **首创性**：填补"多语言语言引导无标准基准"的空白，定位清晰。
- **语言覆盖与质量控制**：32 种类型学多样语言 + 母语者校对，并公开代码与数据（GitHub / HuggingFace），可复现、易扩展（只需翻译问题即可加语言）。
- **评测设计严谨**：LFS + OR 双轴 + 调和平均，能识别"语言换了但内容崩了"的伪成功；评判提示显式排除语言因素，避免指标污染。
- **方法对比全面**：同时覆盖提示、神经元、残差向量、探针、PCA、LDA、SAE 七类路线，是少见的"横向大比武"。
- **科学洞见与工程价值并重**：不仅排名方法，还通过多工具收敛证据给出"后层语言特异 + 语族几何聚类"的机制解释，对可解释性研究有独立价值。
- **轻量实用**：结论直接支持"DiffMean 作为低成本多语言适配替代方案"的工程

……工程价值。

---

## 8. 局限与不足

### 8.1 作者自述的局限

- **计算预算受限导致协议不完全统一**：不同引导方法使用了不同规模的估计数据（10M / 500K / 100K token），作者承认这可能影响方法间的严格可比性，只能以"遵循各方法原始实践"作为辩护。
- **SAE 覆盖不全**：受限于可用的预训练稀疏自编码器，SAE-DiffMean 仅在 Llama 的 5 个层上评测，且 Aya-Expanse-8B 无对应 SAE，导致该路线的跨模型结论缺失。
- **翻译数据的固有偏差**：评测问题由机器翻译 + 母语者校对生成，虽经质量保障，但仍是"英语原问题的译版"，可能不反映各语言母语者自然提出的问题分布（如文化特定话题、本地知识需求）。

### 8.2 分析者补充的方法论隐忧

- **单一评判模型的风险**：OR 完全依赖 Qwen-3-8B 打分，既未报告与人类评分的相关性，也未做多评判者一致性检验。若评判模型对某些语言的内容理解较弱（尤其低资源语言），OR 可能系统性偏高或偏低，进而扭曲 LSS 排名。
- **缺乏统计显著性**：所有方法仅报告单次运行的最佳配置分数，无置信区间、无多种子方差、无配对显著性检验。DiffMean（84.5%）与 LAPE（80.1%）之间的差距是否稳健，无法从论文判断。
- **"最佳配置"选择带来的乐观偏差**：层与强度是在同一评测集上扫描后选取的最优值，存在对测试数据的隐式过拟合；缺少独立的验证/测试划分，报告的绝对分数可能被高估。
- **LFS 的判定粒度较粗**：FastText 语言识别在近缘语言（如西班牙语/葡萄牙语、俄语/乌克兰语、印地语/马尔地语）与代码混合输出上易混淆，可能同时造成假阳性与假阴性，而论文未报告 LID 在 32 语言上的准确率基线。
- **任务范围偏窄**：评测仅覆盖"单轮开放式问答"这一种交互形态，未涉及多轮对话、长文本生成、指令跟随中的语言保持、工具调用等更贴近部署的场景；结论向实际应用的推广需谨慎。
- **只评测"强制切换"而非"语言控制"的完整谱系**：任务设定为源语言 ≠ 目标语言的跨语言强制，未系统考察同语言保持、语码转换、混合语言输出等更细粒度的控制需求。
- **机制解释仍属相关性证据**：余弦相似度、探针准确率、LAPE 神经元分布、LDA Fisher 比等多工具收敛于"后层语言特异"，但这些证据彼此并不独立（都基于同一批激活），且未通过因果干预实验（如针对性消融后层语言子空间并测量行为变化）加以确证。

---

## 9. 对研究与实践的启示

- **对工程实践**：若目标是低成本、免训练地把输出语言钉在指定语言上，**残差流均值差（DiffMean）** 是当前证据支持的首选——实现简单（仅需两语言的平均激活差）、无需标注、单点干预即可生效；提示词仍应作为兜底，因为其在多数高资源语言上可用，但在英语、藏语、波斯语等目标上会系统性失效。
- **对可解释性研究**：结果提示"语言"在表示空间中近似一个**低维、近似线性、按语族几何组织**的方向，这与"概念/风格"类引导的既有发现一致，也为跨语言表示共享假说提供了行为层面的支持；后续工作可进一步检验该方向是否与语法、文字系统等子因素可分离。
- **对基准建设**：CLaS-Bench 的"翻译平行问题 + 母语者校对 + 双轴调和指标"是一个可复用的模板，后续可扩展至多轮、长文本、语音或多模态语言控制，并补上统计检验与人工评判校准。
- **对公平性议题**：不同语言上引导效果的显著差异（尤其低资源语言与跨语族目标）意味着"可操作的可解释性"工具目前并非语言中立，部署时需按语言逐一验证，而不能假设英语上的成功可迁移。

---

## 10. 总体评价

CLaS-Bench 的核心贡献不在于提出新方法，而在于**把一个此前零散、以英语为中心的研究问题，转化为一个有 32 语言覆盖、双轴指标、8 类方法横向对比的标准化评测问题**，并顺带给出了"无监督均值差优于监督探针/LDA""语言信息后层集中且按语族聚类"两条有独立价值的实证结论。其最大优势是覆盖广度、指标设计的抗退化能力与开源可复现性；最大短板是计算预算不一致、缺少统计显著性与人评校准、任务形态单一，以及机制解释仍停留在相关性层面。总体而言，它更像一份**高质量的"领域地图与基线协议"**，为后续多语言引导研究设定了起点，但其绝对排名与分数应被视为方向性参考而非精确结论。

（完）
