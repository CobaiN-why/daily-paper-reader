---
title: "LiveLongBench: Tackling Long-Context Understanding for Spoken Texts from Live Streams"
title_zh: LiveLongBench：面向直播口语文本的长上下文理解
authors: "Yongxuan Wu, Runyu Chen, Peiyu Liu, Hongjin Qian"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://aclanthology.org/2026.findings-acl.1485.pdf"
tags: ["query:ai-se"]
score: 4.0
evidence: 面向直播口语文本的长上下文理解基准
tldr: 长上下文理解是自然语言处理的重要挑战，而直播对话文本冗余高、信息密度不均，现有基准难以反映其复杂性。作者构建首个源自直播的口语长文本数据集LiveLongBench，设计检索、推理与混合三类任务，并评测主流大模型与专用方法。结果揭示现有模型在冗余口语长文本上的不足，为相关NLP研究提供了更贴近实际的评测平台。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1485/fig-001.webp\", \"caption\": \"\", \"page\": 5, \"index\": 1, \"width\": 6000, \"height\": 3375}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1485/fig-002.webp\", \"caption\": \"\", \"page\": 8, \"index\": 2, \"width\": 2322, \"height\": 2160}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1485/fig-003.webp\", \"caption\": \"\", \"page\": 14, \"index\": 3, \"width\": 971, \"height\": 728}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1485/fig-004.webp\", \"caption\": \"\", \"page\": 15, \"index\": 4, \"width\": 6000, \"height\": 3375}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1485/fig-005.webp\", \"caption\": \"\", \"page\": 19, \"index\": 5, \"width\": 6000, \"height\": 3375}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1485/fig-006.webp\", \"caption\": \"\", \"page\": 20, \"index\": 6, \"width\": 6000, \"height\": 3375}]"
motivation: 现有长上下文基准无法反映直播口语文本冗余高、信息密度不均的真实复杂性。
method: 构建首个源自直播的口语长文本数据集，并设计检索、推理与混合三类任务进行评测。
result: 评测显示主流大模型与专用方法在冗余口语长文本上仍存在明显不足。
conclusion: 为贴近实际的长上下文自然语言处理研究提供了新的评测平台。
---

## Abstract
Long-context understanding poses significant challenges in natural language processing, particularly for real-world dialogues characterized by high redundancy and uneven information density. Although large language models (LLMs) achieve impressive results on existing benchmarks, these datasets fail to reflect the complexities of such texts, limiting their applicability to practical scenarios. To bridge this gap, we construct the first spoken long-text dataset, derived from live streams, designed to reflect the redundancy-rich and conversational nature of real-world scenarios. We construct tasks in three categories: retrieval, reasoning, and hybrid tasks. We then evaluate both popular LLMs and specialized methods to assess their ability to understand long contexts in these tasks. Our results show that current methods exhibit strong task-specific preferences and perform poorly on highly redundant inputs, with no single method consistently outperforming others. We propose a new baseline that better handles redundancy in spoken text and achieves strong performance across tasks. Our findings highlight key limitations of current methods and suggest future directions for improving long-context understanding. Finally, our benchmark fills a gap in evaluating long-context spoken language understanding and provides a practical foundation for developing real-world e-commerce systems. The code and benchmark are available at https://github.com/Yarayx/livelongbench.

---

## 论文详细总结（自动生成）

# LiveLongBench 论文结构化总结

## 1. 核心问题与研究动机

- **背景缺口**：长上下文理解是 NLP 的重要挑战，现有长文本基准（LongBench、∞Bench、Loong、L-Eval、M4LE、TCELongBench、FinTextQA 等）几乎都聚焦于**正式书面文本**，无法反映真实口语对话的复杂性。
- **口语文本的独特挑战**：
  - **非正式语言**：句法简化（无动词句、右偏置）、话题漂移（从商品细节突然跳到无关私人话题）。
  - **高冗余**：填充词（um、uh、you know）、重复促销话术、非信息性 token，显著拉长序列并稀释信息密度。
- **两个核心研究问题**：
  - **Q1**：基础大模型能否有效处理具有非正式语言特征的长口语文本？
  - **Q2**：现有上下文压缩方法能否通过多技术组合实现更高压缩率并保持性能？
- **整体含义**：作者构建首个源自直播的口语长文本基准 **LiveLongBench**，填补"长上下文口语理解"评测空白，并为真实电商系统提供实践基础。

## 2. 方法论

### 2.1 数据集构建
- **数据来源**：抖音直播电商，覆盖 11 大类、32 子类（服饰、电子、家居等），以主播独白为主，含重复促销与观众 Q&A。
- **处理流程**：Whisper 转录 → 保留重复与填充词以维持真实性 → 去隐私标识 → 轻度过滤极端噪声（如重复超 10 次的句子）。
- **规模**：967 个评测实例，平均约 **97K tokens**，分布呈幂律，最长超过 **500K tokens**；以中文为主，含少量英文。

### 2.2 任务设计（三类六任务）
| 类别 | 任务 | 说明 |
|---|---|---|
| 检索依赖 | **Single**（单品检索）、**Policy**（政策/售后条款识别） | 从长冗余文本中定位具体信息 |
| 推理依赖 | **Class**（商品分类）、**Summary**（直播摘要） | 借助外部知识推断、去噪提炼要点 |
| 混合 | **Multi**（多品问答）、**Price**（价格比较） | 先检索分散片段再综合推理 |

- 引入**语义多跨度（semantic multi-span）**任务：要求整合语义相关但分散的片段，而非仅结构上分离的段落。
- 覆盖闭域/开域、单跨度/多跨度/全局跨度，兼顾知识回忆与泛化。

### 2.3 评测指标
- **Exact Match (EM)**：严格全匹配，缺一项即 0 分。
- **Score**：软性指标，对部分正确（不完整但事实正确、轻微数值偏差）给部分分。

### 2.4 上下文压缩方法
- **Token 剪枝**：LLMLingua（2×、4×）。
- **注意力稀疏化**：MInference。
- **量化**：KIVI（4bit、2bit）。
- **混合策略（核心贡献）**：将上述方法组合（如 MInference+LLMLingua、KIVI+MInference+LLMLingua），并系统评估。

### 2.5 DEA 效率分析
- 采用**输出导向 CCR 数据包络分析**：以内存占用（GB）为输入、Overall Score 为输出，将每种压缩配置视为决策单元（DMU），用线性规划（Python PuLP）求解效率前沿；±5% 内存扰动下排序稳定。

## 3. 实验设计

- **基准**：LiveLongBench（967 实例，中英混合，以中文为主）。
- **对比模型**：
  - 闭源：GPT-4o（128K）、Gemini-1.5-pro（1000K）、Claude-3.7-sonnet（200K）、GLM4plus（131K）。
  - 开源：Qwen2.5-7B（131K）、LLaMA-3.1-8B（128K）、Mistral-7B（32K）。
  - 领域微调：eCeLLM-M（基于 Mistral-7B-Instruct 的电商微调模型）。
  - **人类基线**：独立标注者在完整转录上作答。
- **压缩方法对比**：KIVI 4bit/2bit、MInference、LLMLingua 2×/4× 及其 7 种组合，共 12 种配置（在 LLaMA-3.1-8B 上）。
- **补充实验**：Needle-in-a-Haystack（NIAH）压力测试（8 种方法 × 多深度/长度）、Self-Extend 集成实验（表 7）、案例研究（图 8、9）。
- **质量控制**：5 名标注者，Cohen's κ / Fleiss' κ 为 0.77–0.91；6 步质控流程（指南培训、试点、交叉核验、共识裁决、随机复审、反馈闭环）。

## 4. 资源与算力

- **论文未明确报告** GPU 型号、数量、训练/推理时长等算力细节。
- 仅披露**标注成本**：5 名学生助理各 2 个工作日，每人 800 元，合计 4,000 元人民币。
- ASR 部分提及在 48 小时人工校对转录上计算 WER/CER（Whisper+人工：WER 0.53%、CER 0.31%）。
- 推理实验使用各模型原生最大上下文窗口；对 Mistral-7B（32K）等短窗口模型做了截断处理，但未说明硬件配置。

## 5. 实验数量与充分性

- **实验规模**：
  - 表 2：8 个模型 × 6 任务 × 2 指标的系统评测。
  - 图 2 / 表 6：12 种压缩配置的 Score 与 EM 完整对比。
  - 图 3：DEA 效率排序；表 7：Self-Extend 增强实验（4 组）。
  - 图 7：NIAH 8 个子图的深度-长度热力图。
  - 附录含案例研究、数据统计、ASR 对比等。
- **充分性评价**：
  - **优点**：任务维度覆盖全面（检索/推理/混合、单/多/全局跨度、闭/开域），模型覆盖闭源/开源/领域微调，压缩方法覆盖三大类及组合，并辅以 NIAH 与 DEA 效率分析，整体较为系统。
  - **不足**：压缩方法实验仅在 LLaMA-3.1-8B 单一模型上进行，跨模型泛化性未验证；消融主要围绕压缩组合，对任务设计本身的消融（如语义多跨度 vs 普通多跨度）缺少定量对比；人类基线样本与评分细节披露有限。

## 6. 主要结论与发现

- **Q1 结论**：闭源模型整体最强（Gemini-1.5-pro Overall 66.7），但**仍显著低于人类（76.3）**；**检索类任务对当前模型最具挑战性**；更长上下文窗口显著提升检索与混合任务表现（Gemini 检索 65.8 vs GLM4plus 28.5）。
- **领域微调的双刃性**：eCeLLM-M 在混合任务上表现突出（Score 40.2、EM 28.0%），但推理能力受损（Reasoning 仅 20.9，EM 0.0%）。
- **单一压缩方法的任务偏好**：
  - **低比特量化（KIVI）擅长检索**（Policy 任务检索分 80.0），因保留完整信息，但过度压缩导致其他任务下降。
  - **稀疏化/剪枝（LLMLingua、MInference）擅长推理**，因其去除冗余起到**去噪**作用；LLMLingua-4× 在推理任务上甚至优于 2×（36.7 vs 33.3），说明高冗余场景下更重压缩更有效。
- **组合方法**：
  - **MInference + LLMLingua-4×** 整体性能最佳（Overall 39.8），兼顾检索与推理。
  - **KIVI + MInference + LLMLingua-2×** 经 DEA 分析为**内存-性能最均衡**配置（内存仅 7.6 GB，Overall 23.6）。
- **NIAH 验证**：KIVI 在保留检索信息上具独特优势；MInference+KIVI 组合检索表现稳定。
- **Self-Extend 集成**：在资源最优配置上可进一步提升推理性能。

## 7. 优点与亮点

- **首创性**：首个源自直播的口语长文本基准，明确刻画非正式语言与高冗余两大真实挑战，填补评测空白。
- **任务设计细致**：三类六任务 + 语义多跨度 + 闭/开域 + 单/多/全局跨度，评测框架层次清晰。
- **数据真实性强**：保留填充词与重复、ASR 后人工校对（WER 0.53%）、严格隐私处理与 6 步质控、公开 κ 一致性。
- **双指标设计**：EM 严格 + Score 软性，兼顾严格性与细粒度区分。
- **方法学贡献**：系统揭示"压缩即去噪"的反直觉现象（4× 优于 2×），并提出混合压缩策略；引入 DEA 做成本-效益排序，为部署选型提供可操作参考。
- **实验互补性好**：主实验 + NIAH 压力测试 + 案例研究 + Self-Extend 扩展，形成较完整证据链。

## 8. 不足与局限

- **领域覆盖有限**：仅基于直播电商，未必代表学术讲座、新闻广播等其他口语场景（作者自述局限）。
- **语言偏差**：以中文普通话为主，英文样本较少，跨语言泛化性未充分验证。
- **算力信息缺失**：未报告 GPU 型号/数量/时长，影响可复现性与效率结论的可比性。
- **压缩实验单一模型**：仅在 LLaMA-3.1-8B 上评测压缩方法，结论向其他模型迁移需谨慎。
- **标注成本高**：依赖人工长文档审阅，规模化扩展受限；未来需自动化方案。
- **人类基线波动**：如 Policy 任务人类 EM 达 100%，而 Summary 类任务人类分较低，任务难度不均衡可能影响整体可比性。
- **ASR 误差风险**：即便校对后仍有残余错误，可能对细粒度检索/价格任务造成噪声。
- **DEA 结论敏感性**：效率排序依赖输入输出选择（仅内存 vs 性能），未纳入延迟、吞吐等其他部署约束。

（完）
