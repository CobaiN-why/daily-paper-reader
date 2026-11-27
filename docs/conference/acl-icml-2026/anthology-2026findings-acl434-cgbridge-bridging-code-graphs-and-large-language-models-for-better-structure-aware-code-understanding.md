---
title: "CGBridge: Bridging Code Graphs and Large Language Models for Better Structure-Aware Code Understanding"
title_zh: CGBridge：连接代码图与大语言模型以实现结构感知的代码理解
authors: "Zeqi Chen, Zhaoyang Chu, Yi Gui, Feng Guo, Yao Wan, Chuan Shi"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://aclanthology.org/2026.findings-acl.434.pdf"
tags: ["query:ai-se"]
score: 8.0
evidence: 用代码图增强大模型以提升代码智能任务
tldr: 大模型在代码生成、摘要与翻译等代码智能任务上表现优异，但其依赖线性化token序列，对长距离程序依赖和标识符重命名等表层变化较为脆弱。已有结构化方法多以序列化提示或辅助训练目标引入结构，易膨胀上下文且推理时缺乏显式引导。作者提出CGBridge，一种即插即用的方法，通过外部可训练模块将代码图信息注入大模型。实验表明该方法在推理阶段提供显式结构引导，提升结构感知的代码理解能力。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl434/fig-001.webp\", \"caption\": \"\", \"page\": 3, \"index\": 1, \"width\": 884, \"height\": 776}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl434/fig-002.webp\", \"caption\": \"\", \"page\": 4, \"index\": 2, \"width\": 298, \"height\": 780}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl434/fig-003.webp\", \"caption\": \"\", \"page\": 8, \"index\": 3, \"width\": 4750, \"height\": 2635}]"
motivation: 大模型依赖线性token序列，对长距离程序依赖和标识符重命名等表层变化脆弱。
method: 提出即插即用的CGBridge，通过外部可训练模块在推理时向大模型注入代码图结构信息。
result: 该方法在不膨胀上下文的前提下为推理提供显式结构引导，提升代码理解效果。
conclusion: 说明将程序结构图与大模型结合是增强代码智能任务的有效且通用途径。
---

## Abstract
Large Language Models (LLMs) have demonstrated remarkable performance in code intelligence tasks such as code generation, summarization, and translation. However, their reliance on linearized token sequences makes them brittle to long-range program dependencies and superficial lexical shifts such as identifier renaming. Existing structure-aware approaches typically treat structure as serialized text prompts or auxiliary training objectives, which often inflate context length or rely on internalized structural priors, failing to provide explicit guidance during inference. To address these limitations, we propose CGBridge, a novel plug-and-play method that enhances LLMs with Code Graph information through an external, trainable Bridge module. It aligns Code Property Graph structure with code semantics and compresses them into compact soft-prefixes, decoupling structural reasoning from textual generation without updating the backbone. Experiments across multiple code LLM backbones and scales show consistent gains over both text-only adaptation and graph-augmented baselines. Furthermore, CGBridge remains robust under identifier renaming and enables over 4× faster inference than LoRA-tuned models, demonstrating both effectiveness and efficiency in structure-aware code understanding.

---

## 论文详细总结（自动生成）

## 1. 核心问题与研究动机

- **背景**：代码大模型（Code Llama、Qwen-Coder、DeepSeek-Coder 等）在代码生成、摘要、翻译等任务上表现突出，但它们把代码当作**线性 token 序列**处理，忽略了程序的图结构语义（AST 语法树、CFG 控制流图、DFG 数据流图，三者可统一为 Code Property Graph, CPG）。
- **核心问题**：“code-as-text”范式迫使模型依赖表层线索（如变量/函数命名），对**长距离程序依赖**和**标识符重命名**等表层扰动十分脆弱（图 1 示例：`price` 被混淆为 `efg` 后基线模型即失效）。
- **对已有工作的批评**（作者归纳为三条路线）：
  - **结构感知神经代码模型**（GraphCodeBERT、UniXcoder）：面向小规模编码器、需任务特定头，与当前指令跟随式 decoder-only LLM 不兼容；
  - **图转文本提示**（GRACE、GraphText 等）：简单通用，但膨胀上下文、稀释高阶依赖；
  - **图增强 LLM 训练/改架构**（Graphix-T5、GALLa）：成本高，结构先验在推理时是**隐式**的，分布漂移下易出现“结构丢失 + 词法猜测”。
- **核心主张**：不再把结构当作辅助特征、提示产物或隐式先验，而是把 **CPG 视为一种独立的结构模态**，在推理时作为**显式结构锚点**注入冻结的 LLM。

## 2. 方法论：CGBridge

### 2.1 总体思想
- 即插即用框架：冻结 LLM 主干，仅训练外部 **Bridge 模块**，将 CPG 结构对齐到代码语义并压缩为**紧凑 soft-prefix**，实现“结构推理”与“文本生成”解耦。
- 形式化目标：最大化 `log P(y_t | y_<t, G, C, I; θ)`，即在指令 `I`、代码 `C`、图 `G` 条件下生成目标序列。

### 2.2 三阶段训练流程

**Stage 1：自监督结构预训练（构建可复用结构专家 CGE）**
- 用 L_g 层 GNN 编码异构 CPG，节点更新为边条件消息聚合：`h_i^(l) = φ(h_i^(l-1), ⊕_{j∈N(i)} ψ(h_j^(l-1), e_ji))`；边类型条件化是关键，用于区分 AST/CFG/DFG 关系。
- 两个自监督目标：
  - **图级对比学习**（特征掩码、边丢弃生成两视图，InfoNCE，L_cl）；
  - **边类型预测**（对采样节点对分类边类型，含负采样得到的“NO_EDGE”类，L_edge）。
- 总损失：`L_Stage1 = λ_cl·L_cl + λ_edge·L_edge`。

**Stage 2：跨模态语义对齐（训练 Bridge 模块）**
- Bridge 为 L_b 层 Transformer，含 **N_q=32 个可学习 query token**（用 BERT-base 初始化），每层三步：
  1. **共享自注意力**融合 query 与代码文本嵌入：`[Q_sa^(l), H_C,sa^(l)] = Self-Attn([Q^(l-1), H_C^(l-1)])`；
  2. **交叉注意力**从图嵌入 H_G 抽取结构信息：`Q_cross^(l) = Cross-Attn(Q=Q_sa^(l), K=V=H_G)`；
  3. 分离的 **FFN** 分别更新 query 与文本表示。
- 输出 `B_Q = Q^(L_b)`，经投影得到 soft prompt `P_G = Proj_LLM(B_Q)`。
- 三个对齐目标（不涉及 LLM 主干）：
  - **GTC**：对称 InfoNCE，相似度取 N_q 个 query 与文本 [CLS] 嵌入的**最大余弦相似度**，温度 τ 可学习；
  - **GTM**：二分类判断图文是否匹配，带**硬负样本挖掘**；
  - **GTG**：以 B_Q 为条件自回归重构代码文本，迫使 soft prompt 承载图的完整语义。
  - `L_Stage2 = L_GTC + L_GTM + L_GTG`。

**Stage 3：指令驱动的任务适配**
- 冻结 LLM，将 soft prompt 与指令/代码的连续嵌入拼接：`C_LLM = [P_G; E(I); E(C)]`；
- 仅更新 Bridge 参数 θ_B，最小化目标序列负对数似然 `L_Stage3(θ_B)`。

### 2.3 关键实现选择
- CGE 默认用 **2 层 Graph Transformer**（对比 GCN/GAT），节点/边特征由 UniXcoder-base 编码；
- 超参：L_g=2、N_q=32、L_b=12、d_model=768，Stage1/2/3 学习率分别为 1e-5 / 5e-7 / 1e-6，Stage 3 用 bfloat16。

## 3. 实验设计

### 3.1 任务与数据集
- **代码摘要**：CodeSearchNet（Python 子集），需捕捉控制流、数据依赖与功能角色；
- **代码翻译**：XLCoST（Python→Java），需保持抽象语法与长距离依赖；
- 每个样本用 Tree-sitter 构建 CPG（AST+CFG+DFG），精炼后共约 **270K 样本**（CodeSearchNet 261,372；XLCoST 10,344）。
- 额外场景：CRUXEval-O（输出预测）、XLCoST Java→Python 跨语言、Qwen3-4B instruct/thinking 变体。

### 3.2 骨干与基线
- **4 个骨干、5 个规模**：Qwen2.5-Coder-1.5B/7B、CodeLlama-7B、DeepSeek-Coder-1.3B/6.7B（另加 Qwen3-4B 作兼容性检验）。
- **基线**：Zero-shot、+LoRA（纯文本 PEFT）、+GraphText（图转文本提示）；另与 **GraphLLM、GraphCLIP、GALLa** 三个图-LLM 方法在 Qwen2.5-Coder-1.5B 上做受控对比。

### 3.3 评价指标
- 摘要：**LLM-as-a-Judge（0–4，GPT-4-0613，按 Coherence/Consistency/Fluency/Relevance 打分，Consistency 权重最高）**为主，辅以 ROUGE-L、Sentence-BERT 余弦相似度、BERTScore；
- 翻译：**Execution Accuracy**为主，辅以 CodeBLEU、Syntax Match、Dataflow Match。

## 4. 资源与算力

- **硬件**：8 块 **NVIDIA H800 80GB** GPU（附录 J）。
- **未明确报告**总训练时长、总 GPU-hours 或各阶段实际训练 epoch 数（仅设 Max Epochs=200 + 早停）。
- 提供了**相对开销**：每 epoch 训练时间 7B 上 LoRA 110.5s vs CGBridge 272.1s（1.5B：56.2s vs 67.5s）；推理延迟 7B 上 CGBridge ~371ms vs LoRA ~1463ms vs 原生 ~299ms；离线图构建 ~281ms/样本、嵌入生成 ~0.42ms/样本。
- 可训练参数：Bridge 固定 **180.80M**（LoRA 7B 为 43.12M、1.5B 为 18.46M）。

## 5. 实验数量与充分性

- **主实验**：Table 1（3 组骨干 × 2 任务）、Table 6（DeepSeek 两个规模）、Table 2（与 3 个图-LLM 方法对比）。
- **鲁棒性**：Table 3/10（1.5B 与 7B 的标识符重命名）、Table 12（5 随机种子均值±方差）。
- **泛化性**：Table 7（CRUXEval-O，含 w/o 与 w/ Stage 3）、Table 8（Java→Python）、Table 9（instruct/thinking）。
- **效率**：Table 4/11（参数、训练时间、推理延迟）。
- **消融**：Table 5（图组件：AST/CFG/DFG 组合）、图 5（训练组件：w/o GTC/GTM/GTG/Stage1/2/3）、Table 17（GCN/GAT/GT 三种图编码器）。
- **超参与分析**：图 9（L_g、N_q 敏感性）、图 4（按代码长度分箱）、图 6/7（编码与解码期注意力）、表 21（query token 的节点类型注意力归因）、表 22–26 与图 8（成功/失败案例）。
- **统计检验**：Table 13（图组件消融的配对显著性，多数 p<0.05 乃至 p<1e-8）、Table 8/9 的 Wilcoxon 与 McNemar 检验。
- **评价**：实验覆盖面在同类工作中属较充分，主结果与消融、显著性检验、定性分析形成闭环；但存在若干公平性需注意之处：
  - **可训练参数不对等**：CGBridge（180.80M）显著多于 LoRA（43.12M/18.46M），并非同参数预算比较；
  - **训练成本更高**：每 epoch 训练时间约为 LoRA 的 1.2–2.5 倍，效率优势仅体现在**推理**侧；
  - **GraphText 基线表现异常差**（翻译 EA 低至 53.97–70.75），未讨论是否已充分
