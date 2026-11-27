---
title: "When TableQA Meets Noise: A Dual Denoising Framework for Complex Questions and Large-scale Tables"
title_zh: 当表格问答遇到噪声：面向复杂问题与大规模表格的双重去噪框架
authors: "Shenghao Ye, Yu Guo, Dong Jin, Yuxiang Wang, Yikai Shen, Yunpeng Hou, Shuangwu Chen, Jianyang, Xiaofeng Jiang"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://aclanthology.org/2026.acl-long.1102.pdf"
tags: ["query:ai-se"]
score: 5.0
evidence: 利用大模型推理改进NLP表格问答去噪
tldr: 表格问答是自然语言处理的基础任务，但随着问题更复杂、表格更大，噪声数据严重削弱大模型推理性能。作者提出EnoTab双重去噪框架，一方面做相关性过滤，保留真正参与推理的信息，另一方面进行表格剪枝，在压缩规模的同时保留关键内容。实验表明该框架能有效缓解噪声带来的推理退化，提升复杂表格问答的准确性，为真实场景下的表格理解提供了可迁移的去噪思路。
source: ACL-2026-Long
selection_source: conference_retrieval
motivation: 真实场景中复杂问题与大规模表格引入大量噪声，显著削弱大模型在表格问答中的推理性能。
method: 提出EnoTab双重去噪框架，结合相关性过滤以保留关键信息，以及表格剪枝以压缩规模并保留核心内容。
result: 该框架缓解了噪声导致的推理退化，提升了复杂问题与大规模表格上的问答表现。
conclusion: 为噪声环境下的表格问答提供了相关性过滤与表格剪枝相结合的有效方案。
---

## Abstract
Table question answering (TableQA) is a fundamental task in natural language processing (NLP). The strong reasoning capabilities of large language models (LLMs) have brought significant advances in this field. However, as real-world applications involve increasingly complex questions and larger tables, substantial noisy data is introduced, which severely degrades reasoning performance. To address this challenge, we focus on improving two core capabilities: Relevance Filtering, which identifies and retains information truly relevant to reasoning, and Table Pruning, which reduces table size while preserving essential content. Based on these principles, we propose EnoTab, a dual denoising framework for complex questions and large-scale tables. Specifically, we first perform Evidence-based Question Denoising by decomposing the question into minimal semantic units and filtering out those irrelevant to answer reasoning based on consistency and usability criteria. Then, we propose Evidence Tree-guided Table Denoising, which constructs an explicit and transparent table pruning path to remove irrelevant data step by step. At each pruning step, we observe the intermediate state of the table and apply a post-order node rollback mechanism to handle abnormal table states, ultimately producing a highly reliable sub-table for final answer reasoning. Finally, extensive experiments show that EnoTab achieves outstanding performance on TableQA tasks with complex questions and large-scale tables, confirming its effectiveness.

---

## 论文详细总结（自动生成）

## 1. 核心问题与整体含义

- **研究背景**：表格问答（TableQA）是 NLP 的基础任务，LLM 的推理能力推动了该领域发展。但真实应用（如医疗、金融）中问题越来越复杂、表格越来越大，问题和表格两侧都引入大量噪声。
- **核心问题**：噪声主要来自两方面：
  - **复杂问题中的虚假相关**：问题中的某些短语看似是约束，但表格中没有对应数据，模型误将其当作推理条件。
  - **大规模表格中的无关数据**：大量行/列与答案无关，增加推理难度和计算成本。
- **整体含义**：论文认为现有方法在两个核心能力上不足：
  - **Relevance Filtering（相关性过滤）**：难以准确区分问题中的虚假相关与真正相关信息。
  - **Table Pruning（表格剪枝）**：剪枝过程常是黑箱，容易误删答案相关数据，且出错后往往需整体重做。
- **论文目标**：在推理前显式去除问题与表格中的噪声，形成聚焦的证据集合和可靠子表，从而提升复杂问题与大规模表格场景下的 TableQA 性能。

## 2. 方法论：EnoTab 双重去噪框架

### 2.1 核心思想

- 提出 **EnoTab**，包含两个模块：
  - **Evidence-based Question Denoising（EQD）**：将复杂问题分解为最小语义单元（Evidence），过滤与答案推理无关的单元。
  - **Evidence Tree-guided Table Denoising（ETD）**：基于可靠证据构建显式、可观察的表格剪枝路径，逐步生成子表，并通过回滚机制防止答案相关数据丢失。
- 形式化目标：原始 TableQA 为  
  \(Y=\arg\max \prod_i P_\theta(y_i\mid y_{<i},Q,T;\theta)\)；  
  去噪后使用聚焦证据集 \(E\subseteq Q\) 和子表 \(T_{sub}\subseteq T\)：  
  \(Y=\arg\max \prod_i P_\theta(y_i\mid y_{<i},E,T_{sub};\theta)\)。

### 2.2 Evidence 定义与问题去噪

- **Evidence 三元组**：\(e=(area, condition, action)\)。
  - `area`：对应表格列；
  - `condition`：该列中满足语义单元的单元格值；
  - `action`：匹配方式，如字符串匹配、数值比较、日期判断。
- **Evidence Generation**：用 LLM 将问题分解为多个 Evidence，输入包括问题 \(Q\)、表头 \(H\)、采样得到的 \(k\) 个代表性行 \(R\)。
- **两阶段检索**：
  - 先用 LLM 提取关键词，通过 LSH 粗筛候选行；
  - 再用 embedding 相似度和编辑距离重排，选 top-\(k\) 行。
  - 超参数：\(k=10\)，\(\lambda=0.7\)，候选池 \(C=\min(256,\lceil 0.1N\rceil)\)，关键词提取用 GPT-4o-mini，embedding 用 bge-large-en-v1.5。
- **Evidence Evaluation**：从两个标准判断 Evidence 是否相关：
  - **一致性（Consistency）**：多轮生成中 Evidence 是否稳定出现。对同一 `(area, action)` 分组，用语义判别器判断 condition 是否等价，计算一致性分数  
    \(S(e_i)=c/(|G_j|-1)\)，其中 \(c\) 为同组中语义等价 Evidence 数；若 \(S(e_i)\ge \alpha\) 则保留。默认 \(n=5\) 轮，\(\alpha=0.8\)，判别器为 Llama-2-7b-chat-hf。
  - **可用性（Usability）**：Evidence 能否在表格中落地。工具包 \(P\) 根据 `area` 选列，按 `action` 调用字符串/数值/日期匹配 API；若匹配结果非空则可用，否则丢弃。
- 最终得到可靠证据集 \(E_r\)。

### 2.3 Evidence Tree 与表格去噪

- **Evidence Tree 定义**：二叉树 \(T=(N_{leaf},N_{inter})\)。
  - 叶节点对应 \(E_r\) 中的 Evidence，对原始表过滤后输出子表；
  - 内部节点为 `And` 或 `Or`，合并左右子表。
- **树构建**：用 LLM 根据问题、表头、代表性行和可靠证据集生成 Evidence Tree。
- **子表生成**：对 Evidence Tree 做后序遍历：
  - 叶节点用工具包 \(P\) 过滤原表；
  - 内部节点按 `And`/`Or` 合并子表。
- **异常处理与回滚**：
  - 若 `And` 节点产生空表，执行 **And2Or**：依次将左子节点、右子节点、当前节点的 `And` 替换为 `Or`，直到得到非空子表。
  - 使用 **Table Verifier** 判断子表是否包含回答所需全部信息；若失败，回滚到上一节点生成的子表并再次验证；最多验证两次，仍失败则使用完整表格。
- **答案生成**：将最终子表 \(T_{final}\) 与用 \(E_r\) 高亮后的问题 \(Q_{final}\) 输入 LLM，生成答案。

## 3. 实验设计

- **数据集 / 场景**：
  - **WikiTQ**：表格推理标准数据集，4,344 样本、421 张表。
  - **TabFact**：表格事实核验数据集，2,024 样本、298 张表。
  - **STQA-L**：基于 Spider 构建的自然大规模表格数据集。
  - **STQA-N**：基于 Spider 构建并注入噪声的大规模表格数据集。
  - 补充：**FeTaQA** 自由形式表格问答；以及向 WikiTQ 注入噪声内容的鲁棒性实验。
- **Benchmark 与指标**：
  - STQA-N、STQA-L、WikiTQ 使用 exact match accuracy；
  - TabFact 使用二分类准确率；
  - FeTaQA 使用 BLEU、ROUGE-1/2/L。
- **对比方法**：
  - 通用方法：End-to-End QA、Chain-of-Thought、Text-to-SQL；
  - 分解类：Dater、Chain-of-Table、TabLaP；
  - 剪枝类：Binder、TabSQLify、H-Star；
  - FeTaQA 中还对比 T5-small/base/large 等。
- **主要结果**：
  - STQA-N：EnoTab 在 GPT-4o 上 80.3（+8.3），GPT-4o-mini 上 78.2（+9.5）。
  - STQA-L：GPT-4o 上 75.3（+8.2），GPT-4o-mini 上 72.5（+9.1）。
  - WikiTQ：74.6（+1.8）；TabFact：89.2（+2.3）。
  - 表格压缩率：TabFact 37.0%、WikiTQ 53.1%、STQA-L 75.7%、STQA-N 89.2%。
- **消融实验**：去掉 Consistency Assessment、Usability Assessment、And2Or、Table Verifier 均导致性能下降；其中去掉一致性或可用性评估下降最明显。

## 4. 资源与算力

- 论文**未明确报告** GPU 型号、数量、训练时长或总推理成本。
- 文中主要使用闭源 API 模型 GPT-4o、GPT-4o-mini，以及开源模型 LLaMA-2-70B、Qwen-1.5-70B 进行推理/评估；还使用 Llama-2-7b-chat-hf 作为语义判别器、bge-large-en-v1.5 作为 embedding 编码器。
- 论文报告了超参数和重复实验设置：开源模型取 3 次运行平均，闭源 API 做 2 次运行确认稳定性，标准差约在 1% 绝对准确率以内；但**没有给出算力消耗、延迟或费用分析**。

## 5. 实验数量与充分性

- **实验组数量大致包括**：
  - 4 个主数据集上的主实验：STQA-N、STQA-L、WikiTQ、TabFact；
  - 4 个关键模块 × 2 个大规模数据集 × 2 个模型（GPT-4o、GPT-4o-mini）的消融实验；
  - 4 种基础模型（GPT-4o、GPT-4o-mini、Qwen-1.5-70B、LLaMA-2-70B）的适应性实验；
  - 4 个数据集上的剪枝压缩率分析；
  - WikiTQ 上按难度分级（easy/m

edium/hard）分析、WikiTQ 噪声注入鲁棒性实验、FeTaQA 自由形式问答实验，以及若干案例/错误分析。整体上，实验覆盖了“主效果—模块贡献—模型泛化—压缩效率—难度分层—噪声鲁棒性—自由形式生成”多个维度，实验组数量较充足，能够支撑论文关于双重去噪有效性的主要 claim。

- **充分性评价**：
  - **优点**：主实验覆盖标准 TableQA、事实核验、大规模表格与噪声注入场景；消融实验针对 EQD、ETD 的关键组件分别验证；基础模型适应性实验说明方法不局限于单一闭源模型；压缩率与难度分层分析补充了“为什么有效”和“在何种问题上有效”的证据。
  - **不足**：缺少统计显著性检验与置信区间报告；未系统分析推理延迟、API 调用次数与费用；对剪枝错误传播、回滚触发频率、Table Verifier 误判率的定量分析仍有限；FeTaQA 仅作为补充生成任务，未深入讨论自由形式答案下的去噪收益边界；跨领域真实大规模表格（医疗、金融等）验证不足。

## 6. 批判性分析与潜在问题

- **方法优势**：
  - 将问题去噪与表格剪枝统一到“Evidence”这一可解释中间表示上，使“哪些问题片段被保留、哪些表格区域被保留”变得可观察。
  - Evidence Tree 的后序遍历与 And2Or、Table Verifier 回滚机制，针对剪枝中“误删答案相关数据”的核心风险提供了工程化补救。
  - 在 STQA-N 等噪声场景下提升明显，说明显式去噪对复杂问题和大表噪声确实有针对性价值。

- **主要局限与风险**：
  - **对 LLM 生成质量的依赖较强**：Evidence 生成、Evidence Tree 构建、语义等价判别均依赖模型能力；若初始 Evidence 遗漏关键约束，后续过滤与剪枝可能系统性丢失信息。
  - **超参数与工具覆盖问题**：一致性阈值、采样行数、候选池大小、匹配 API 的类型覆盖等均影响效果；对非结构化单元格、复合条件、跨列推理的覆盖可能不足。
  - **成本与可扩展性**：多轮 Evidence 生成、语义判别、树构建、验证与回滚会增加调用次数；论文未报告延迟和费用，实际部署时需权衡收益与开销。
  - **错误恢复的上限**：回滚最多验证两次，失败后回退完整表格，虽保证保守性，但可能削弱去噪收益；And2Or 的替换策略也可能引入语义偏差。
  - **评估维度**：以 exact match / 分类准确率为主，对中间剪枝质量、证据召回率、子表充分性缺少细粒度人工评估；生成任务仅用 BLEU/ROUGE 也难全面反映事实一致性。

## 7. 总体结论

论文围绕复杂问题与大规模表格中的双侧噪声问题，提出 EnoTab 双重去噪框架：在问题侧以 Evidence 为单位过滤虚假相关，在表格侧以 Evidence Tree 指导可观察剪枝，并通过回滚与验证降低误删风险。实验表明，该方法在噪声大规模表格场景下收益显著，在标准 WikiTQ、TabFact 上也有稳定提升，同时具有较高表格压缩率。其核心贡献在于把“相关性过滤”和“表格剪枝”从隐式模型行为转化为显式、可追踪的中间过程。与此同时，方法仍受限于 LLM 生成可靠性、调用成本、工具覆盖与细粒度评估不足等问题，适合作为复杂 TableQA 场景下“先聚焦证据、再推理”的框架性方案，而非低成本通用替代方案。

（完）
