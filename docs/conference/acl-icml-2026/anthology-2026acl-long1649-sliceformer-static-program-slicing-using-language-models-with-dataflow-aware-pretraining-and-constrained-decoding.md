---
title: "SLICEFORMER: Static Program Slicing Using Language Models With Dataflow-Aware Pretraining and Constrained Decoding"
title_zh: SLICEFORMER：结合数据流感知预训练与约束解码的语言模型静态程序切片
authors: "Pengfei He, Shaowei Wang, Tse-Hsun Chen, Muhammad Asaduzzaman"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://aclanthology.org/2026.acl-long.1649.pdf"
tags: ["query:ai-se"]
score: 8.0
evidence: 基于语言模型的软件工程静态程序切片
tldr: 静态程序切片是软件工程的基础技术，但已有基于语言模型的方法依赖建模不准且生成不受约束，切片中常出现幻觉语句。作者提出SliceFormer，将切片重构为序列到序列任务，采用小型语言模型CodeT5+，并引入数据流感知预训练与约束解码两项创新。方法直接针对依赖建模与生成约束两大缺陷，实验显示切片精度提升且幻觉显著减少。该工作为大模型辅助的程序分析与软件工程自动化提供了有效路径。
source: ACL-2026-Long
selection_source: conference_retrieval
motivation: 现有基于语言模型的切片方法依赖建模不精确，生成不受约束导致幻觉语句。
method: 将静态切片重构为序列到序列任务，使用CodeT5+等小模型，并引入数据流感知预训练与约束解码。
result: 两项创新直接针对依赖建模与生成约束问题，使切片预测更准确并减少幻觉token。
conclusion: 表明小型语言模型配合结构化预训练与解码约束可有效自动化程序切片任务。
---

## Abstract
Static program slicing is a fundamental software engineering technique for isolating code relevant to specific variables. While recent learning-based approaches using language models (LMs) show promise in automating slice prediction, they suffer from inaccurate dependency modeling and unconstrained generation, where LMs fail to capture precise data flow relations and produce slices containing hallucinated tokens and statements. To address these challenges, we propose SliceFormer, a novel approach that reformulates static program slicing as a sequence-to-sequence task using small language models such as CodeT5+. introduces two key innovations that directly target the identified limitations. First, to improve dependency modeling, we design dataflow-aware pretraining objectives that leverage data flow graphs DFG to teach models data dependencies through dataflow-preserving statement permutation and dataflow-aware span corruption. Second, to eliminate hallucination, we develop a constrained decoding mechanism that enforces both lexical and syntactic constraints. We evaluate SliceFormer on Java and Python program slicing benchmarks, demonstrating consistent improvements over state-of-the-art baselines with up to 22% gain in ExactMatch.

---

## 论文详细总结（自动生成）

# SLICEFORMER 论文结构化总结

## 1. 核心问题与研究背景

- **静态程序切片**是软件工程的基础技术，用于从程序中提取与特定变量（切片准则）语义相关的语句，广泛应用于漏洞分析、调试、变更影响分析等场景。与动态切片不同，它基于静态分析构建的依赖图，无需执行程序，实用性更广。
- **传统方法**（JavaSlicer、CPP-Slicer 等）依赖系统依赖图（SDG）的图可达性计算切片，但构建成本高、语言相关性强。
- **近期学习型方法**（NS-Slicer 的二元分类、基于 GPT 类大模型的提示工程）暴露出两大缺陷：
  1. **依赖建模不准确**：模型依赖表层模式或位置邻近性，漏掉相关语句或纳入无关语句（如图 1 例 1 错误纳入 `temp = A; A = C;`）。
  2. **生成不受约束**：产生原程序中不存在的幻觉内容，包括 token 级替换（如把 `codepoint` 写成 `keta`）和语句级伪造逻辑（如 `y * 10 * y * y * y * z * ten ...`）。
- **形式化要求**：切片必须是输入语句的**精确子序列**，需同时满足"准确性"（不多不少）与"元素保持性"（不得修改或幻觉）。

## 2. 方法论

### 核心思想
将静态切片重构为**序列到序列任务**，基于小型编码器-解码器模型 CodeT5+（0.7B），通过"数据流感知预训练 + 约束解码"两个互补手段，分别解决依赖建模不准与幻觉生成两大问题。

### 问题形式化
- 输入：`x = {s1, s2, ..., sN; v; [n]}`，其中 `si` 为语句、`v` 为切片准则变量、`[n]` 为变量所在行号。
- 输出：后向切片 `y = {si1, ..., sik} ⊆ {s1,...,sn}`，且下标严格递增。

### 关键技术一：数据流感知预训练
基于数据流图 DFG（节点为 AST 叶子变量，有向边表示变量间数据依赖），设计两个预训练目标：

- **数据流保持的语句置换（Algorithm 1）**：在同一基本块内、且两语句间不存在任何数据依赖边的条件下，随机交换语句对，构造语义等价的代码变体；模型学习恢复/生成合法排列，从而学会判断语句间的数据独立性。每个样本最多置换 3 条语句。
- **数据流感知的 Span Corruption（Algorithm 2）**：随机选取 DFG 中的变量节点，定位其父节点（值从何而来）与子节点（值流向何处），按 50% 概率选择两种掩码粒度：
  - 细粒度：直接掩码相关变量；
  - 粗粒度：掩码包含这些变量的整条语句。
  
  目标是重建被掩码的数据流链条（如图 2 中由 `a = 1` 到 `c = a + b` 中 `c` 的链），掩码比例为 25%。
- **监督微调（SFT）**：在 CodeNet-Slice 标注数据上微调，并引入 `<code>`、`<criterion>`、`<slice>` 等控制标记，引导结构化输出。

### 关键技术二：约束解码（Algorithm 3）
在 beam search（beam size = 3）中施加两类约束：

- **词汇约束**：将所有未在输入代码中出现的 token 的 logit 置为 −∞，强制严格抽取式生成，杜绝 token 级幻觉。
- **语法约束**：利用树相似度编辑距离 TSED 的**单调性**——由于合法切片是输入的子序列，随着正确语句逐条追加，生成结果与输入 AST 的 TSED 应在语句边界处单调上升。若某候选在语句边界处 TSED 下降，则判定为结构错误并剪枝该 beam 路径。TSED 定义为 `1 − Σw(op_i)/max(Nodes(Tx), Nodes(Ty))`，按 AST 最大节点数归一化。

## 3. 实验设计

### 数据集
- **评测基准**：CodeNet-Slice 的 Java 与 Python 子集。Java：训练 30.8K / 验证 3.5K / 测试 8.7K，平均约 19 SLOC；Python：训练 23.8K / 验证 5.1K / 测试 5.1K，平均约 25 SLOC。
- **真值来源**：Java 用 JavaSlicer，Python 用改编自 JavaSlicer 的切片器。
- **预训练语料**：CodeSearchNet 的 Java/Python 子集，约 100 万函数。

### 评价指标
Dependence Accuracy（Acc-D）、ExactMatch、CodeBLEU、TSED。

### 对比方法
1. **LLM 提示型切片器**：GPT-4o-mini 与 GPT-5，搭配 Zero-shot、RAG、CoT 三种提示策略。
2. **NS-Slicer**：基于 CodeBERT / GraphCodeBERT 的二元分类方法（当前 SOTA）。
3. **直接 SFT 的模型**：CodeLlama-7B（QLoRA）、Qwen3-8B（QLoRA）、CodeT5+。

## 4. 资源与算力

- 论文明确说明使用 **4 块 NVIDIA RTX 3090（24GB）** 完成全部实验。
- 预训练：上下文长度 512 token、batch size 32、训练 **100K steps**。
- 微调：AdamW 优化器、batch size 32、学习率 5×10⁻⁵、1,000 步 warmup、共 10 个 epoch；输入输出长度均 512 token。
- 大模型基线（CodeLlama/Qwen3）使用 QLoRA 降低显存需求。
- 未报告具体的总 GPU 小时数或墙钟训练时长，仅给出 step 数与硬件配置，这一点说明不够充分。

## 5. 实验数量与充分性

### 实验规模
- **主实验**：2 种语言 × 4 个指标 × 约 11 个对比系统（表 1），覆盖 LLM 提示、分类式、SFT 式三类基线。
- **消融实验**（图 4）：在 Java 与 Python 上分别移除语句置换、Span Corruption、语法约束、词汇约束四个组件，共 4 组变体 + 完整模型。
- **效率实验**（表 2）：在 Java 上与全部基线比较单任务推理延迟。
- **架构兼容性实验**（表 4，附录 D）：CodeT5、CodeT5+、CodeLlama-7B、Qwen3-8B 四种架构 × 是否使用预训练/约束解码的组合对比。
- **定性分析**（附录 C）：分析 NS-Slicer 因逐语句独立嵌入而无法区分不同分支中相同语句的缺陷。

### 充分性与公平性评价
- **优点**：消融维度完整，覆盖预训练与解码两个方向的全部组件；跨语言验证；包含效率与架构泛化分析，实验设计较系统。
- **潜在公平性问题**：
  - 基线参数量差异大：NS-Slicer 仅 125M，SliceFormer 为 770M，而 7B/8B 模型仅做 SFT 对比，未在同规模下比较预训练收益。
  - LLM 基线未做微调，仅用提示，ExactMatch 近乎为 0，对比存在"以训练对免训练"的不对称性。
  - 训练数据规模、预训练语料与基线不完全对等，可能放大自身优势。

## 6. 主要结论与发现

- **总体性能**：Java 上 ExactMatch 达 **92.20%**，Python 上达 **83.15%**；相较最强基线 NS-Slicer（GraphBERT）分别提升 **6.4%** 与 **21.9%**。
- **相对 SFT 的增益**：相比直接微调的 CodeT5+，Java 提升 5.0%（87.24→92.20），Python 提升 5.9%（77.24→83.15），证明数据流预训练与约束解码缺一不可。
- **LLM 提示方法表现最差**：最强组合（GPT-5 + CoT）ExactMatch 仅 14.00%（Java）与 13.00%（Python），远低于学习型方法，说明幻觉问题在抽取式任务中代价极高。
- **消融结论**：**Span Corruption 与词汇约束贡献最大**；语法约束影响相对较小，原因是预训练模型已具备基本语法知识，结构性错误发生率低于词汇性错误。
- **效率结论**：平均推理延迟 **0.296 s/任务**，远快于 7B/8B 微调模型（5.75–6.52 s）与 GPT-4/5 CoT（0.835–1.162 s），在精度与效率间取得良好平衡。
- **架构结论**：数据流预训练目标天然适配编码器-解码器架构；解码器-only 模型（CodeLlama、Qwen3）无法直接使用该预训练目标，但约束解码可带来约 2.5–3.1 个百分点的提升。

## 7. 优点

- **问题与方案高度对应**：两个创新点分别精确瞄准两个实证发现的缺陷，逻辑闭环清晰。
- **预训练目标具有原创性**：首次提出"数据流保持的语句置换"与"数据流感知 Span Corruption"用于代码预训练，相比 AST 掩码更轻量、更聚焦长程数据依赖。
- **约束解码为免训练、架构无关**：词汇约束保证抽取性，TSED 单调性提供一种简洁的在线结构校验信号，可迁移至解码器-only 模型。
- **小模型高性能**：0.7B 模型在精度上超越 125M 分类器与 7B/8B 通用模型，并显著快于后者，工程落地价值高。
- **实验体系较完整**：跨语言、多指标、消融、效率、架构泛化与定性分析齐备，且开源代码与数据。

## 8. 不足与局限

- **语言覆盖有限**：仅验证 Java 与 Python，对其他语言（如 C/C++、JavaScript）需额外工程适配与实证，泛化性未证实。
- **架构限制**：数据流预训练依赖编码器-解码器的双向编码与掩码重建能力，无法直接用于主流的解码器-only 大模型；表 4 显示这些模型只能受益于约束解码，收益有限。
- **抽取式假设的强约束**：词汇约束要求切片 token 必须原样出现在输入中，若未来任务需要重写或规范化输出（如重命名、格式化），该机制不再适用。
- **语法约束增益有限**：消融显示其贡献最小，说明该组件的边际价值不高，同时 TSED 在每次语句边界都要计算 AST 编辑距离，会带来额外解码开销（论文未单独量化）。
- **依赖前端解析质量**：DFG 构建依赖 Tree-sitter 与 GraphCodeBERT 的实现，解析失败或语言特性复杂时代码依赖图可能失真，进而影响预训练与切片质量。
- **数据与场景局限**：评测数据为 CodeNet 中的函数级短程序（平均 19–26 行），未在真实大型工业代码库上验证；预训练语料（CodeSearchNet）与评测集可能存在分布差异。
- **算力报告不完整**：只给出 GPU 型号数量与训练步数，缺少总训练时长/GPU 小时等可复现性关键信息。
- **基线公平性存疑**：与 LLM 提示方法的对比是"训练 vs 免训练"，与 NS-Slicer 的对比存在参数量差异，结论中"全面超越 SOTA"的表述宜更谨慎。

（完）
