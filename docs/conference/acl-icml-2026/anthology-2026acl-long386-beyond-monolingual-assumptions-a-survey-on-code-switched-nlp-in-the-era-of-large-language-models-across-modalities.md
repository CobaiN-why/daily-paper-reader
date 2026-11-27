---
title: "Beyond Monolingual Assumptions: A Survey on Code-Switched NLP in the Era of Large Language Models across Modalities"
title_zh: 超越单语假设：大模型时代跨模态语码转换 NLP 综述
authors: "Rajvee Sheth, Samridhi Raj Sinha, Mahavir Patil, Himanshu Beniwal, Mayank Singh"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://aclanthology.org/2026.acl-long.386.pdf"
tags: ["query:ai-se"]
score: 6.0
evidence: 综述大模型时代语码转换 NLP 的最新进展
tldr: 大模型虽快速发展，但多数模型仍难以处理混合语言输入，且语码转换数据稀缺、评测存在偏差，制约其在多语社会中的部署。本文首次系统综述语码转换感知的大模型研究，覆盖 327 项工作、五类研究领域、15 个以上 NLP 任务与 80 多种语言，按架构、训练策略与评测方法进行归类。文章最后给出面向包容性数据、公平评测与语言学基础模型的发展路线图。
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long386/fig-001.webp\", \"caption\": \"\", \"page\": 2, \"index\": 1, \"width\": 1794, \"height\": 534}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long386/fig-002.webp\", \"caption\": \"\", \"page\": 40, \"index\": 2, \"width\": 1682, \"height\": 748}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long386/fig-003.webp\", \"caption\": \"\", \"page\": 40, \"index\": 3, \"width\": 1103, \"height\": 676}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long386/fig-004.webp\", \"caption\": \"\", \"page\": 41, \"index\": 4, \"width\": 1256, \"height\": 1128}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long386/fig-005.webp\", \"caption\": \"\", \"page\": 41, \"index\": 5, \"width\": 1477, \"height\": 590}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long386/fig-006.webp\", \"caption\": \"\", \"page\": 42, \"index\": 6, \"width\": 1389, \"height\": 824}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long386/fig-007.webp\", \"caption\": \"\", \"page\": 42, \"index\": 7, \"width\": 1580, \"height\": 665}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long386/fig-008.webp\", \"caption\": \"\", \"page\": 43, \"index\": 8, \"width\": 1590, \"height\": 789}]"
motivation: 大模型在混合语言输入上表现不佳，语码转换数据稀缺且评测存在偏差。
method: 系统综述 327 项研究，按架构、训练策略与评测方法对语码转换 NLP 进行分类。
result: 梳理出大模型重塑语码转换建模的进展与仍待解决的挑战。
conclusion: 提出面向包容性数据、公平评测与语言学基础模型的研究路线图。
---

## Abstract
Amidst the rapid advances of large language models (LLMs), most LLMs still struggle with mixed-language inputs, limited Code-switching (CSW) datasets, and evaluation biases, which hinder their deployment in multilingual societies. This survey provides the first comprehensive analysis of CSW-aware LLM research, reviewing 327 studies spanning five research areas, 15+ NLP tasks, 30+ datasets, and 80+ languages. We classify recent advances by architecture, training strategy, and evaluation methodology, outlining how LLMs have reshaped CSW modelling and what challenges persist. The paper concludes with a roadmap emphasizing the need for inclusive datasets, fair evaluation, and linguistically grounded models to achieve truly multilingual intelligence. A curated collection of all resources is maintained at https://github.com/lingo-iitgn/awesome-code-mixing/.

---

## 论文详细总结（自动生成）

# 《超越单语假设：大模型时代跨模态语码转换 NLP 综述》中文结构化总结

## 1. 核心问题与整体含义（研究动机与背景）

- **现实背景**：语码转换（Code-Switching, CSW）指在同一句话或同一语篇内交替使用两种及以上语言，是全球多语社会中的普遍现象。全球约 43% 人口为双语者、13% 为三语者，合计超过 45 亿多语使用者；社交媒体使混合语言文本无处不在。
- **技术落差**：现有 NLP 系统建立在“单语假设”之上。文中引用数据指出：单语 ASR 处理混合语言输入时词错率上升 30–50%，即使多语模型也出现约 15% 的语义准确率下降，说明这是**架构层面的根本缺口**，而非简单的数据不足。
- **研究缺口（Research Gap）**：LLM 时代虽带来指令微调、PEFT、多模态等新手段，但：
  - 零样本迁移到真实 CSW 场景仍表现不佳；
  - 多语 LLM 常不如微调过的小模型，“多语能力 ≠ 语码转换能力”；
  - 存在**不对称性**：英语语境中夹入非英语词会降低性能，而其他语言中夹入英语词反而提升性能；
  - 既有综述（Winata et al. 2023；Sitaram et al. 2019）主要覆盖前 LLM 时代与纯文本场景。
- **核心立场（Position）**：作者主张应把语码转换视为**核心建模挑战**，而不是多语能力的下游副产物；低资源 CSW 中语言切换与文字系统交替、拼写变异、口语随意性交织，需要语言/文字系统感知的专门架构，而非笼统的多语后训练。
- **整体含义**：本文定位为**首篇系统梳理 LLM 时代 CSW NLP 的综述**，横跨文本、语音、视觉-语言三类模态，覆盖 327 篇研究、5 大研究领域、15+ 个 NLP 任务、30+ 个数据集、80+ 种语言，并给出研究路线图。

---

## 2. 方法论：综述的组织框架与核心技术线索

> 说明：本文是**综述/立场论文**，不含新模型训练，因此“方法论”体现为**文献筛选流程 + 分类体系（taxonomy）+ 分析框架**。

### 2.1 文献检索与筛选流程（附录 A）

- **关键词维度**：三组核心维度——code-mixing/code-switching、multilingual NLP、large language models。
- **数据源**：通过 API 检索 ACL Anthology、arXiv、Semantic Scholar；检索截止日期为 **2025 年 10 月**（对齐 ACL Rolling Review 的时效规范）。
- **初检规模**：约 **500 篇**。
- **去重与筛选**：用 DOI 与标题去重，优先同行评审来源；人工筛查相关性，纳入标准为“涉及任一 NLP 任务下的 code-mixing/code-switching，或探索多语与 LLM 适配方法”。
- **最终集合**：**327 篇**（含前 LLM 时代与 LLM 时代工作）。
- **归类维度**：
  1. 任务类型（LID、POS、NER、Intent、Speech/ASR、MT 等）；
  2. 模态（文本 / 语音 / 视觉-语言）；
  3. 模型架构（Transformer、指令微调、多模态）。
- **重叠处理**：多标签归类，在最主要章节讨论并交叉引用；高/中/低资源划分沿用多语 NLP 惯例。
- **量化陈述原则**：文中所有定量结论均为**引用原始论文的代表性数值**，而非元分析聚合值（作者在 Limitations 中明确声明）。

### 2.2 分类体系（Taxonomy，附录 B 图 2）

四大维度构成统一框架：

| 维度 | 内容 |
|---|---|
| 任务成熟度 | 传统任务（LID、POS、NER、MT、情感/情绪、句法分析）已趋饱和；推理与多模态任务仍存缺口 |
| 方法论演进 | 统计模型 → 表示学习 → 上下文理解（BERT/XLM/T5）→ 基础模型（GPT-3/LLaMA 级） |
| 语言对覆盖 | 呈强烈英语中心偏置（约 72%） |
| 性能差距 | 随任务复杂度递增：LID 约 4% 退化 → 推理类任务 >33% |

任务被划分为三层：

- **传统任务**：语言识别、词性标注、命名实体识别、机器翻译、句法分析、情感与情绪分析；
- **新兴当代任务**：NLI、QA、意图分类与槽填充、代码混合文本生成、跨语言迁移、文本摘要、音译（transliteration）；
- **未充分探索的前沿任务**：对话与语音、安全与多模态（越狱、后门攻击、梗图毒性）、推理与抽象（数学、隐喻、类比）、创意与代码生成。

### 2.3 分析主线（模型训练与适配的三段式框架）

1. **预训练（Pre-training）**
   - 专用代码混合模型：HingBERT/HingRoBERTa、CONFLATOR（切换点旋转位置编码）、CMLFormer（双解码器 + 切换点学习）、BERTologiCoMix；
   - 任务自适应预训练（TAPT）：边界感知 MLM、模型合并（model merging）、对齐式预训练、联合 LID–POS 多任务；
   - 跨语言对齐：CoSwitchMap、MVMLT（梯度显著性关键词替换）、AIMLT（注意力引导生成 CS 句）、X-CIT（跨语言持续指令微调）。
2. **微调（Fine-tuning）**
   - 任务特定微调：XLM-R + S-index、mBART/mT5 + 回译与集成、Whisper/FastConformer 单语微调；
   - 多任务微调：句法感知联合训练、中间任务微调、AdapterFusion、对比式多任务预训练；
   - 指令微调：COMMIT、CSCL（课程式）、sPhinX（N-shot 引导）、PLUG（枢轴语言）、LinguaLIFT；
   - 参数高效方法：LoRA / QLoRA / 软提示 / 量化感知 PEFT；
   - 强化学习：RLAIF、CHAI（GPT-4o 生成偏好对 + PPO 优化英–Hinglish 翻译）。
3. **后训练与推理期适配**
   - 零样本：提示生成、实体驱动切换、数据增强（CoSDA-ML、MALM）；
   - 一/少样本：相似度检索提示、RAG（DweshVaani）、PRO-CS（实例级提示组合）、GLOSS（自训练合成未见语言对）、In-Context Mixing（ICM）。

### 2.4 评测方法学梳理（附录 F）

- **传统指标**：F1、Accuracy、BLEU、ROUGE、METEOR；
- **CSW 专用指标**：CMI（混合强度）、SyMCoM（句法混合度）、M-Index、I-Index、切换点分析、PIER（切换点错误率）、SAER（语义感知错误率）、PhoBLEU、chrF++；
- **质量与内评价**：GAME 指标（免金标）、困惑度、语法性评分、自然度/可接受度人工判断、Cohen's κ / Fleiss' κ 标注者一致性。

---

## 3. “实验设计”：综述的证据组织方式与对比分析

> 本文无自建模型实验，其“实验”体现为**文献计量分析、对比表格、失败案例探测（probing）与统计可视化**。

### 3.1 文献计量与可视化分析（附录 H，图 6–9）

- **数据集规模分布**：条形图对比主流数据集实例数，COMI-LINGUA（125,615）与 MEGAVERSE（100,000）最大；饼图显示“大型”（50–100k）数据集占比最高（40%）。
- **语言对分布**：统计 **202 个 CSW 数据集/基准**，Hinglish 与 Spanish–English 绝对主导（图 7 列出 Top-15 语言对）。
- **任务分布**：情感分析（SA）占 26.2%、机器翻译（MT）占 18.5%；按大类划分为“其他”55.9%、“理解类”31.1%，显示研究集中于低层任务。

### 3.2 对比性汇总表（8 张表）

| 表 | 内容 | 对比维度 |
|---|---|---|
| 表 1 | 按任务划分的顶级 CSW 数据集 | 语言、领域、关键特性、优缺点（如 SemEval-2022 Task 11、TB-OLID、WMT22 MixMT、AfroCS-xs、GupShup、X-RiSAWOZ、EmoMix-3L、ASCEND、SEAME） |
| 表 2 | Top-5 模型对比 | XLM-RoBERTa、MuRIL、mBERT、GPT-4、IndicBERT 的方法、优势与短板 |
| 表 3 | 主要基准 | CodeMixBench、COMI-LINGUA、CroCoSum、CS-Sum、CS3-Bench、GLUECoS、LinCE、Lost in the Mix、MEGAVERSE、PACMAN、SwitchLingua、X-RiSAWOZ |
| 表 4 | 代表性数据集（约 30 个） | 语言、任务、来源（人工/混合/合成）、新颖贡献 |
| 表 5 | 语音数据集 | ASCEND、TALCS（580h）、ArzEn、MUCS（约 600h）、ESCWA、Mixat、Saudilang |
| 表 6 | 文本场景 LLM 失败模式 | 语言混淆、推理缺口、安全越狱、语用失败 |
| 表 7 | 语音/多模态失败模式 | 声学歧义、图文冲突、安全规避、OCR 碎片化 |
| 表 8 | 评测指标失效模式 | BLEU/ROUGE 对音译拼写过敏、EM 对同义切换零容忍、CMI 对不合语法“词沙拉”给出高分、BERTScore 跨语言对齐偏差 |

### 3.3 定性失败案例探测（作者自行构造的提示实验）

- **ChatGPT**（Odia–罗马化印地语混合）：询问“度假国家”却输出印度各邦与联邦属地列表，且语法错误；
- **GLM-4.6**（孟加拉语–英语）：对孟加拉词 *Ohoroho* 做连读（sandhi）分析时误解任务；
- **Perplexity**（孔卡尼语–英语）：询问“被葡萄牙人摧毁的果阿神庙”，模型忽略约束只给现存古庙；
- 另引用文献中的典型失败：Hinglish 数学题（“do apples 吃 ek”答错算术）、罗马化印地语汽车热接线越狱成功、Spanglish 讽刺被字面理解、图文冲突梗图被判正面情感。

### 3.4 关键对比结论（跨研究横向比较）

- 专用代码混合预训练模型（HingBERT 等）**稳定优于** mBERT/XLM-R 等通用多语基线；
- 单语 ASR 微调在 Yoruba–English 上显著降低 WER，**优于更大的零样本多语模型**，但会损害非目标语言（英语）性能；
- 合成数据质量权衡：AfroCS-xs 中 **100 条专家句胜过 10,000 条合成句**；LLM 生成数据的母语者接受度仅 60–65%；
- 安全评估：Qorgau 框架下哈萨克–俄语混合输入越狱成功率 67%，单语仅 12%。

---

## 4. 资源与算力

- **本文未进行任何模型训练或推理实验，因此未报告 GPU 型号、数量、训练时长或能耗数据**。
- 论文中出现的算力相关信息均为**被引工作的转述**，例如：PEFT/量化（LoRA、QLoRA）被描述为降低算力成本的手段；低资源语言因分词效率低而带来更高计算开销（Nag et al., 2024）；RLAIF 流程存在较高计算需求。
- 唯一可核查的“资源产出”是作者维护的公开资源库：`https://github.com/lingo-iitgn/awesome-code-mixing/`，以及文中提到的交互式分类体系（interactive taxonomy）。

---

## 5. “实验”数量与充分性评估

### 5.1 规模

- **文献层面**：约 500 篇初检 → 327 篇纳入，覆盖 5 大领域、15+ 任务、30+ 数据集、80+ 语言；
- **分析产物**：9 张图（含分类体系图、失败案例截图、4 张统计图）、8 张表（含 5 张数据集/模型/基准对比表、3 张失败模式表）；
- **定性探测**：3 个商用/开源模型的代码混合提示失败案例（ChatGPT、GLM-4.6、Perplexity）；
- **横向对比组**：模型对比 5 组、基准对比 12 组、数据集对比约 30 组、失败模式 12 类、指标失效 4 类。
- **无消融实验**（因无自建模型），也无统计显著性检验或元分析。

### 5.2 充分性与客观性

- **覆盖面较充分**：任务、模态、语言对、训练范式、评测方法五个切面均有系统梳理，且附录提供了细粒度支撑材料，可复现性较好（检索式、截止日期、纳入标准均披露）。
- **客观性较好之处**：明确声明定量数值为“代表性引用值”而非聚合统计，避免了综述中常见的过度概括；对合成数据的负面证据（接受度仅 60–65%、合成数据收益递减）如实呈现。
- **公平性隐忧**：
  - 文献筛选为**人工相关性判断**，未报告双人标注与一致性系数（κ），存在选择偏倚风险；
  - 检索截止 2025 年 10 月，LLM 领域迭代极快，部分结论可能迅速过时（作者亦自陈）；
  - “Top-N 数据集/模型”的选取标准为“引用量 + 社区采用度的加权组合”，但**未披露具体权重与计算方法**，带有主观性；
  - 三个失败案例为**单次提示、非系统性评测**，无重复采样与提示变体控制，只能作为示意而非证据。

---

## 6. 主要结论与发现

1. **LLM 重塑了 CSW 研究范式**：从任务特定的统计/神经方法，转向统一的多语与指令驱动框架；ICM 提示、指令微调、课程学习、PEFT、RLAIF 等成为主流手段。
2. **收益高度不均衡**：进步几乎集中在高资源语言对（英–西、英–印地、英–中），英–西与英–印地系统可达 90 分

- **（承接第 6 节第 2 点）**……英–西与英–印地系统可达 90 分上下，而非洲语言、南亚低资源语言、原住民语言以及三语及以上混合场景仍大幅落后；论文明确指出“多语覆盖广度”与“CSW 能力深度”并不成正比，许多被宣称支持上百种语言的模型，在真实混合语料上接近不可用。
3. **模态间进展不平行**：文本侧因预训练语料天然含混合文本而受益最大；语音侧受制于混合语音数据稀缺与声学边界模糊，ASR/语音翻译的 CSW 退化仍最严重；视觉-语言侧问题被重新定义为“图文语言不一致”，失败主要表现为 OCR 碎片化、图文冲突下的情感误判与安全对齐被绕过。
4. **失败模式具有系统性而非偶发性**：作者归纳的失败并非随机错误，而是集中于语言混淆（输出语言漂移）、推理缺口（切换点处算术/逻辑断裂）、语用失败（讽刺、隐喻被字面化）、安全规避（混合语越狱）四类，说明模型缺乏对“切换”这一事件本身的显式建模。
5. **评测体系是当前最薄弱环节**：现有指标要么对音译与拼写变异过敏（BLEU/ROUGE/EM），要么可被无意义“词沙拉”刷高（CMI 类混合度指标），缺乏同时衡量**语义保真、切换自然度、语法合法性**的综合指标；作者据此呼吁建立切换点级别的细粒度诊断评测。
6. **数据质量优先于数据规模**：多项被引证据一致指向“少量专家标注 > 大规模合成”，LLM 合成 CSW 数据的母语者接受度有限，且存在放大模型自身偏置的风险；数据构建应从“造句子”转向“造场景”（真实语用、真实切换动机）。
7. **安全与公平是被低估的维度**：混合语输入显著提高越狱成功率，且现有安全对齐几乎只在英语上验证，意味着多语用户实际处于“保护盲区”；同时英语中心偏置使非英语母语者的真实使用场景在基准中长期缺席。

---

## 7. 局限与批判性评估

### 7.1 作者自陈的局限（Limitations）

- **定量结论非元分析**：所有数值均为对原始论文代表性结果的引用，任务定义、数据划分、指标口径不一致，跨研究数字不可直接相加或严格比较。
- **时效性风险**：检索截止 2025 年 10 月，LLM 与多模态模型迭代迅速，部分“前沿任务”判断可能短期内失效。
- **语言与来源偏置**：虽覆盖 80+ 语言，但受发表语种（以英文为主）与 ACL/arXiv 生态影响，非英语学界（如区域会议、本地语言期刊）的工作可能系统性缺席。
- **任务边界模糊**：code-switching、code-mixing、borrowing、transliteration、romanization 在不同文献中定义不一，综述采用宽口径合并，可能掩盖机制差异。

### 7.2 分析者补充的批判

- **分类体系的操作性不足**：“任务成熟度—方法论演进—语言覆盖—性能差距”四维框架描述力强，但缺少可判定的边界规则，同一工作可能同时落入多个格子，导致后续统计（如图 6–9）的口径不完全透明。
- **“Top-N”选择的黑箱性**：数据集与模型的 Top 榜采用“引用量 + 社区采用度加权”，但权重未公开，实质上是一种专家判断，读者不宜将其当作客观排名。
- **失败案例的证据强度有限**：三个提示探测均为单次、无温度/提示变体控制、无重复采样，属于**示意性轶事（anecdote）**，可用于提出假设，但不能支撑“模型普遍失败于某类结构”的强结论。
- **因果归因偏强**：论文倾向于将性能退化归因于“架构层面的单语假设”，但被引研究中数据分布偏移、分词器覆盖不足、评测集构造偏差等混淆因素未被系统剥离，架构归因仍需控制实验支撑。
- **建设性方案偏“清单式”**：路线图提出语言/文字系统感知架构、切换点显式建模、混合语安全对齐等方向，但对“如何在同一模型中同时满足高资源与低资源、文本与语音”的权衡缺乏具体的架构级设计讨论。

---

## 8. 对未来研究的启示（论文路线图的提炼）

1. **把“切换”作为一等建模对象**：在位置编码、注意力掩码、分词器、损失函数层面显式引入语言边界/文字系统信号（如切换点感知的位置编码、脚本感知分词），而非依赖多语预训练的隐式泛化。
2. **重建评测范式**：从句子级单一指标转向**切换点级诊断 + 多维评分**（语义保真、语法合法性、自然度、语言一致性），并配套母语者标注协议与一致性报告。
3. **数据策略转向“质—量混合”**：以少量高质量专家数据为锚，合成数据仅作增广，并强制报告母语者接受度与偏置审计。
4. **模态协同**：利用文本侧较成熟的 CSW 理解能力反哺语音（如切换点感知的 ASR 重打分、语音-文本联合对齐），并针对视觉-语言建立“图文语言不一致”专项基准。
5. **安全对齐的多语扩展**：将混合语越狱纳入红队标准流程，建立跨语言、跨脚本的安全评测集，避免英语单语验证的虚假安全感。
6. **公平性与可及性**：优先覆盖非拉丁脚本、低资源语言与三语混合场景，报告分语言对的细粒度结果而非仅平均值。

---

## 9. 总体评价与适用读者

- **核心贡献**：作为首篇将 CSW 研究系统扩展到“LLM 时代 + 三模态”的综述，其最大价值不在提出新方法，而在于**提供了一个可导航的地图**——统一的任务/模态/方法/评测四轴坐标系，加上对失败模式与评测缺陷的显式归纳，使“CSW 为何仍未解决”从模糊直觉变为可定位的具体缺口。
- **最强之处**：立场鲜明（反对“多语能力即 CSW 能力”的默认假设）、证据组织克制（区分引用值与聚合值）、对负面证据（合成数据收益递减、专用小模型优于通用大模型）不回避。
- **最弱之处**：证据以二手引用为主，缺乏统一口径的再分析；失败探测与 Top-N 榜单的方法透明度不足；对“架构归因”的论证强于其证据所能支撑的程度。
- **适用读者**：多语/低资源 NLP 研究者（用于定位选题与基准选择）、语音与多模态工程师（用于了解模态特有失败模式）、评测与安全研究者（用于指标与红队设计）、以及需要快速建立领域全景的博士生与工程实践者。
- **一句话判断**：这是一篇**框架价值大于结论价值**的综述——其分类体系与问题清单值得作为研究议程长期引用，但其中的具体数值与排名应回到原始文献核验后再使用。

（完）
