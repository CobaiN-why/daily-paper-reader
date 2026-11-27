---
title: Making Large Language Models Efficient Dense Retrievers
title_zh: 让大模型成为高效的稠密检索器
authors: "Yibin Lei, Shwai He, Ang Li, Andrew Yates"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://aclanthology.org/2026.acl-long.587.pdf"
tags: ["query:ai-se"]
score: 4.0
evidence: 面向高效LLM稠密检索的层剪枝分析
tldr: 直接微调大模型做稠密检索性能优异，但参数量庞大导致计算效率低下。作者系统分析LLM检索器中的层冗余，发现与生成任务不同，MLP层更易剪枝而注意力层对语义聚合仍关键。基于此提出剪枝方案，在保持检索效果的同时显著提升效率，为高效自然语言处理检索技术提供了可复用思路。
source: ACL-2026-Long
selection_source: conference_retrieval
motivation: 直接微调大模型做稠密检索虽效果好，但参数庞大导致计算效率低下。
method: 系统分析LLM检索器的层冗余，发现MLP层更易剪枝而注意力层关键，并据此设计剪枝方案。
result: 在保持检索性能的同时显著提升模型效率。
conclusion: 为高效稠密检索这一自然语言处理技术提供了可复用的剪枝思路。
---

## Abstract
Recent work has shown that directly fine-tuning large language models (LLMs) for dense retrieval yields strong performance, but their substantial parameter counts make them computationally inefficient. While prior studies have revealed significant layer redundancy in LLMs for generative tasks, it remains unclear whether similar redundancy exists when these models are adapted for retrieval tasks, which require encoding entire sequences into fixed representations rather than generating tokens iteratively. To this end, we conduct a comprehensive analysis of layer redundancy in LLM-based dense retrievers. We find that, in contrast to generative settings, MLP layers are substantially more prunable, while attention layers remain critical for semantic aggregation. Building on this insight, we propose EffiR, a framework for developing efficient retrievers that performs large-scale MLP compression through a coarse-to-fine strategy (coarse-grained depth reduction followed by fine-grained width reduction), combined with retrieval-specific fine-tuning. Across diverse BEIR datasets and LLM backbones, EffiR achieves substantial reductions in model size and inference cost while preserving the performance of full-size models.

---

## 论文详细总结（自动生成）

# 论文总结：Making Large Language Models Efficient Dense Retrievers（让大模型成为高效的稠密检索器）

## 1. 核心问题与整体含义

- **研究背景**：将大语言模型（LLM）直接微调为稠密检索器（dense retriever）已展现出强语义匹配与泛化能力，但动辄数十亿参数导致编码阶段计算开销巨大，难以实时部署。
- **已有认知的空白**：先前研究在**生成任务**中发现 LLM 存在显著层冗余——注意力层可大量剪除、MLP 层相对关键；但检索任务与生成任务本质不同：检索需将整条序列编码为**单一固定表示**（单次前向），而非自回归逐 token 生成，因此冗余模式未必相同。
- **三个核心问题**：(i) 基础模型架构在检索任务中是否也存在层冗余？(ii) 若存在，与生成任务有何差异？(iii) 如何利用该冗余构建更高效的检索模型？
- **整体含义**：论文系统揭示了"检索器冗余模式与生成器相反"这一新现象，并据此提出面向检索的压缩框架 **EffiR**，为高效检索器设计提供了可复用思路。

## 2. 方法论

### 2.1 层冗余分析（诊断阶段）
- 采用 He et al. (2024) 的层丢弃方法，对每个子层计算重要性分数：比较子层输出与输入，用余弦相似度度量增量贡献，即 `S_l = M(x^l, x^{l+1})`，其中 `M(x,y) = 1 − Cosine(x,y)`；输入与输出越接近，说明该层贡献越小、越可删。
- 将**注意力层**与 **MLP 层**视为两个独立组，各组按重要性保留 top-k（`T_Attn ← Argmax(S_Attn, k_Attn)`，`T_MLP ← Argmax(S_MLP, k_MLP)`）。
- 重要性分数用 256 条 C4 验证样本计算（embedding 与任务无关），评估在 13 个 BEIR 数据集上进行。
- **关键发现**：与生成任务相反，MLP 层冗余显著更大、可大幅剪除；注意力层对语义聚合至关重要，激进剪除会导致性能崩溃。

### 2.2 EffiR 框架（粗到细压缩）
- **核心思想**：沿"深度"和"宽度"两个互补维度压缩 MLP，再配合检索特定微调。
- **第一阶段：粗粒度深度缩减**——整层删除低重要性的 MLP 层（如从 Mistral-7B 删除 16 个 MLP 层）。
- **第二阶段：细粒度宽度缩减（self-slimming）**——在每个 MLP 的中间神经元引入可训练重要性指示 `z ∈ R^n`，将 MLP 重写为：
  `MLP(x) = W_down(ReLU(z)·Act(W_gate x) ⊙ (W_up x)) + x`
  - `ReLU(z)` 保证非负并起软掩码作用；`z` 初始化为全 1 向量以兼容原始行为。
  - 训练目标：`L = L_InfoNCE + λ·L_norm`，其中 `L_norm` 为 `ReLU(z)` 的 ℓ0 范数，λ 控制稀疏度。
  - 因 ℓ0 不可微，采用 **sigmoid 松弛** `R̃(x) = Σ σ(β|x_i|)`（β=5.0）作为可微代理。
  - 仅训练 500 步后即学得稀疏激活模式；随后对所有 MLP 层的缩放因子做**全局排序**，将最不重要者冻结为 0、其余置 1，形成二值门控掩码；最后用 InfoNCE 正常训练并永久移除被置 0 的中间维度（实验中削减 30%）。
- **训练细节**：LoRA（rank 32、α=64）应用于 v/q/k/gate/down/o/up 投影；学习率 1e-4；每样本 1 正 7 负 + in-batch 负样本；用 KL 散度从 BGE-reranker 蒸馏排序分数；self-slimming 阶段 λ=1e-8；温度 τ=0.02。

## 3. 实验设计

- **数据集**：训练用 **MS MARCO**；评估用 **BEIR 13 个数据集**（Arguana、Climate-FEVER、DBPedia、FEVER、FiQA、HotpotQA、NFCorpus、NQ、Quora、SCIDOCS、SciFact、TREC-COVID、Touche-2020），指标为 **nDCG@10**。
- **主干模型**：主实验用 Mistral-7B-v0.1；泛化性验证覆盖 LLaMA3-8B、Qwen-2.5-1.5B/3B/7B、ModernBERT-base，以及 LLaMA2-7B（与 Sheared-LLaMA 对比）。
- **对比方法**：
  - 强基线 **RepLLaMA**（同用 MS MARCO 训练）；
  - 同监督训练的小模型：LLaMA-3.2-1B、Gemma-2-2B、Qwen-1.5-4B；
  - 稀疏化剪枝：**Wanda**、**SparseGPT**（2:4 结构化，finetune-then-prune 与 prune-then-finetune 两种设定）；
  - 结构剪枝：**Sheared-LLaMA**；
  - 量化兼容性：bitsandbytes **NF4**（含双重量化）；
  - 自身消融：仅粗粒度层丢弃变体（EffiR-8A/16A/8B/16B/8M/16M/20M/24M/16M8A）。
- **效率度量**：参数量 + 相对全模型的推理加速（query 侧与 doc 侧分别测），在**单张 H100** 上用 1000 条 NQ 随机样本、torch.compile 测量；另在 CPU 上测检索延迟（Faiss Flat）。

## 4. 资源与算力

- **明确提及**：推理速度测量使用**单张 H100 GPU**；检索延迟在 AMD EPYC 7763 单核 CPU 上测；训练使用荷兰研究理事会授予的 **LUMI 超级计算机**（EuroHPC，项目号 NWO-2024.050）。
- **未明确说明**：论文**未报告** GPU 数量、总训练时长/GPU 小时数、能耗等具体算力开销；仅给出训练配置（1 epoch LoRA、self-slimming 500 步全参数训练、约 0.03B token 的训练量级）。

## 5. 实验数量与充分性

- **实验规模**（粗略统计）：
  - 表 1（E5-Mistral 直接剪枝，7 变体 × 13 数据集）；
  - 表 2（Mistral-7B 剪枝后微调，10 变体 × 13 数据集）；
  - 表 3（主结果，10 模型 × 13 数据集 + 速度）；
  - 表 4（vs. Wanda/SparseGPT）、表 5（vs. Sheared-LLaMA）、表 6（量化，3 模型 × 2 精度）；
  - 附录表 8–12（5 个额外主干 × 多剪枝变体）；
  - 图 2–7（层丢弃热图、层-wise 维度、深度 vs 宽度对比、last-token vs mean-pooling 案例研究）。
- **充分性评价**：覆盖多主干、多压缩策略、多基线、量化兼容、嵌入空间对齐（isotropy 0.28 vs 0.34）、检索侧延迟，实验设计**较充分**。
- **客观/公平性**：所有基线使用相同训练配置与相同 MS MARCO 数据，EffiR 仅用单阶段标准数据，而 Sheared-LLaMA 需约 10 倍（0.4B vs 0.03B）token，比较条件对 EffiR 有利但也说明其高效；Wanda/SparseGPT 对比中明确区分了两种剪枝顺序并指出其加速依赖专用内核，比较维度较全面。

## 6. 主要结论与发现

- **冗余模式与生成任务相反**：检索器中 MLP 层冗余大、可大幅剪枝；注意力层不可激进剪除，因其负责跨 token 的上下文聚合与细粒度语义匹配。
- **深层更冗余**：层丢弃与宽度缩减的热图均显示模型上部（深层）更可剪，与"深层过参数化"一致；该模式在检索微调前后基本保持。
- **粗到细优于纯深度剪枝**：EffiR-3.4B（全框架）nDCG@10 达 54.3，超过仅层丢弃的 EffiR-20M-3.6B（53.7），且参数更少；30% self-slimming 也优于 EffiR-20M。
- **主结果**：EffiR 以约 **48% 参数**达到 54.3 vs 全模型 56.1，query 侧 **1.97×**、doc 侧 1.82× 加速，并优于同规模小模型（LLaMA-1B 51.5、Gemma-2B 51.5、Qwen-4B 52.6）。
- **与其他剪枝对比**：与 Wanda/SparseGPT 在 prune-then-finetune 下性能相当，但 EffiR 为硬结构剪枝，带来真实计算/内存节省且无需专用内核；与 Sheared-LLaMA 性能接近而训练数据少约 10 倍；仅保留约 19% MLP 参数仍可达相近效果。
- **与量化兼容**：EffiR 不损害 4bit 量化表现（如 EffiR-16MLP 4bit 仍 55.3，体积降至 3.0 GB）。
- **嵌入空间保持**：EffiR 与原模型 isotropy 接近，基本保留几何结构；检索延迟无额外开销（~2.28 ms/query）。
- **pooling 方式影响鲁棒性**：last-token 嵌入对注意力剪除极敏感，mean-pooling 因聚合全序列信息而更鲁棒。

## 7. 优点

- **洞察新颖且反直觉**：首次系统对比检索与生成任务的层冗余差异，明确指出"MLP 可剪、注意力关键"，为检索器压缩提供原则性指导。
- **方法简洁实用**：仅剪 MLP、单阶段标准 MS MARCO 数据即可，无需复杂多阶段数据增强；粗到细两级压缩兼顾深度与宽度。
- **结构剪枝带来真实收益**：整层删除 + 维度削减实现真实计算与内存节省，不依赖稀疏矩阵专用

内核，部署友好；同时与 4bit 量化正交，可叠加使用以进一步降低显存与存储开销。
- **分析维度较全面**：除主性能表外，还提供层丢弃热图、层-wise 维度保留比例、深度剪枝与宽度剪枝对比、last-token 与 mean-pooling 的案例研究、嵌入空间 isotropy 分析以及 CPU 检索延迟测量，支撑结论较为扎实。
- **对比设置较公平**：主要基线使用相同训练数据与训练配置；与 Sheared-LLaMA 对比时明确指出 token 消耗差异；与 Wanda/SparseGPT 对比时区分 prune-then-finetune 与 finetune-then-prune，并说明稀疏加速对专用内核的依赖。

## 8. 局限与不足

- **压缩维度相对单一**：方法主要压缩 MLP 的深度与宽度，几乎不剪注意力层。虽然这符合论文发现，但也意味着压缩上限受注意力参数占比约束，未充分探索注意力头剪枝、低秩分解、KV 压缩等方向。
- **模型与任务覆盖有限**：主实验为 Mistral-7B，泛化验证覆盖 1.5B–8B 级模型，但未覆盖更大规模模型、多语言检索、跨模态检索、多向量检索或 late-interaction 检索器。
- **评估指标较集中**：以 BEIR 13 个数据集的 nDCG@10 为主，未系统报告召回率、MRR、长文档场景、生成式检索或端到端 RAG 任务效果。
- **额外训练与超参依赖**：self-slimming 需额外 500 步全参数训练，并依赖 λ、β、稀疏比例等超参；论文未充分展示这些超参的敏感性分析与调参成本。
- **效率测量的部署代表性有限**：推理加速在单张 H100 上结合 torch.compile 测量，实际框架、批大小、序列长度和 CPU 部署可能改变加速比；CPU 延迟仅基于 Faiss Flat 检索场景。
- **训练数据较单一**：训练仅使用 MS MARCO，虽在 BEIR 上评估域外泛化，但训练分布多样性有限；排序蒸馏还依赖 BGE-reranker。
- **冗余分析稳定性讨论不足**：重要性分数仅用 256 条 C4 样本计算，样本敏感性、评分稳定性及不同校准集的影响未深入分析。
- **与稀疏剪枝的效率对比不完整**：论文指出 Wanda/SparseGPT 的实际加速依赖专用稀疏内核，但未在相同内核与部署条件下给出完整效率曲线。

## 9. 启发与未来方向

- **任务感知压缩**：检索与生成任务的层冗余模式相反，说明 LLM 压缩不应沿用生成任务的默认假设，而应按下游任务特性定制剪枝策略。
- **注意力层的高效化**：在保留跨 token 聚合能力的前提下，可探索注意力头剪枝、低秩注意力、线性注意力、KV 缓存压缩等，以突破当前压缩上限。
- **粗到细范式可迁移**：深度整层删除加宽度 self-slimming 的两阶段思路，可扩展到多向量检索器、重排器、多模态检索器及 RAG 编码器。
- **与其它压缩技术组合**：可进一步研究 EffiR 与量化、蒸馏、MoE、动态计算分配的结合；例如按 query 难度动态选择深度或宽度。
- **非对称部署**：query 侧与 doc 侧可采用不同压缩率，doc 侧因离线编码可承受更激进的压缩，query 侧则优先保证低延迟。
- **理论解释**：可进一步解释为何检索更依赖注意力层、深层 MLP 为何更冗余，以及压缩后表示几何与鲁棒性之间的关系。

## 10. 总体评价

该论文围绕“LLM 作为稠密检索器时的层冗余是否与生成任务相同”这一清晰问题展开，得出了反直觉但证据较强的结论：检索器中 MLP 层冗余显著、注意力层更关键。基于此提出的 EffiR 方法简洁、实用，仅压缩 MLP 即可在约 48% 参数下取得接近全模型的检索性能，并获得真实推理加速，且与量化兼容。实验覆盖多主干、多基线、多数据集，整体较充分、客观。主要不足在于压缩维度仍偏单一、评估任务与部署场景有限，但这些局限也为后续任务感知压缩研究提供了明确方向。总体而言，这是一项对高效检索器设计与 LLM 任务特定压缩均具有参考价值的工作。

（完）
