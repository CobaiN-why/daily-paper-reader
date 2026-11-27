---
title: "SWE-QA-Pro: A Representative Benchmark and Scalable Training Recipe for Repository-Level Code Understanding"
title_zh: SWE-QA-Pro：面向仓库级代码理解的代表性基准与可扩展训练配方
authors: "Songcheng Cai, Zhiheng Lyu, Yuansheng Ni, Xiangchao Chen, Baichuan Zhou, Shenzhe Zhu, Yi Lu, Haozhe Wang, Chi Ruan, Benjamin Schneider, Weixu Zhang, Xiang Li, Andy Zheng, Yuyu Zhang, Ping Nie, Wenhu Chen"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://aclanthology.org/2026.findings-acl.837.pdf"
tags: ["query:ai-se"]
score: 9.0
evidence: 智能体仓库级代码理解基准
tldr: 仓库级代码理解是自动化软件工程的关键，但现有评测依赖热门仓库，模型可借记忆作弊且忽视长尾主题。作者构建SWE-QA-Pro基准，选取多样长尾仓库并配备可执行环境，通过问题驱动聚类保证主题平衡并严格过滤易被直接回答的样本。结果显示智能体工作流在该基准上显著优于直接作答基线，为仓库级代码理解提供了更可靠的评测与训练方案。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl837/fig-001.webp\", \"caption\": \"\", \"page\": 2, \"index\": 1, \"width\": 813, \"height\": 595}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl837/fig-002.webp\", \"caption\": \"\", \"page\": 2, \"index\": 2, \"width\": 612, \"height\": 490}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl837/fig-003.webp\", \"caption\": \"\", \"page\": 2, \"index\": 3, \"width\": 480, \"height\": 317}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl837/fig-004.webp\", \"caption\": \"\", \"page\": 2, \"index\": 4, \"width\": 490, \"height\": 490}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl837/fig-005.webp\", \"caption\": \"\", \"page\": 2, \"index\": 5, \"width\": 600, \"height\": 600}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl837/fig-006.webp\", \"caption\": \"\", \"page\": 2, \"index\": 6, \"width\": 814, \"height\": 598}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl837/fig-007.webp\", \"caption\": \"\", \"page\": 2, \"index\": 7, \"width\": 811, \"height\": 598}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl837/fig-008.webp\", \"caption\": \"\", \"page\": 2, \"index\": 8, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl837/fig-009.webp\", \"caption\": \"\", \"page\": 2, \"index\": 9, \"width\": 600, \"height\": 360}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl837/fig-010.webp\", \"caption\": \"\", \"page\": 4, \"index\": 10, \"width\": 1776, \"height\": 1476}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl837/fig-011.webp\", \"caption\": \"\", \"page\": 4, \"index\": 11, \"width\": 1776, \"height\": 1476}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl837/fig-012.webp\", \"caption\": \"\", \"page\": 4, \"index\": 12, \"width\": 2100, \"height\": 1320}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl837/fig-013.webp\", \"caption\": \"\", \"page\": 8, \"index\": 13, \"width\": 7045, \"height\": 2790}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl837/fig-014.webp\", \"caption\": \"\", \"page\": 8, \"index\": 14, \"width\": 3005, \"height\": 2632}]"
motivation: 现有仓库级代码理解评测依赖热门仓库且忽视长尾主题，模型可借记忆作弊。
method: 构建基于多样长尾仓库与可执行环境的基准，并用问题驱动聚类与难度校准筛选样本。
result: 在过滤易解问题后，智能体工作流在该基准上显著优于直接作答基线。
conclusion: 为仓库级代码理解提供了更可靠且可扩展的评测与训练基础。
---

## Abstract
Agentic repository-level code understanding is essential for automating complex software engineering tasks, yet the field lacks reliable benchmarks. Existing evaluations often overlook the long tail topics and rely on popular repositories where Large Language Models (LLMs) can cheat via memorized knowledge. To address this, we introduce SWE-QA-Pro, a benchmark constructed from diverse, long-tail repositories with executable environments. We enforce topical balance via issue-driven clustering to cover under-represented task types and apply a rigorous difficulty calibration process: questions solvable by direct-answer baselines are filtered out. This results in a dataset where agentic workflows significantly outperform direct answering (e.g., a ~13-point gap for Claude Sonnet 4.5), confirming the necessity of agentic codebase exploration. Furthermore, to tackle the scarcity of training data for such complex behaviors, we propose a scalable synthetic data pipeline that powers a two-stage training recipe: Supervised Fine-Tuning (SFT) followed by Reinforcement Learning from AI Feedback (RLAIF). This approach allows small open models to learn efficient tool usage and reasoning. Empirically, a Qwen3-8B model trained with our recipe surpasses GPT-4o by 2.3 points on SWE-QA-Pro and substantially narrows the gap to state-of-the-art proprietary models, demonstrating both the validity of our evaluation and the effectiveness of our agentic training workflow.

---

## 论文详细总结（自动生成）

# SWE-QA-Pro 论文总结

## 一、核心问题与整体含义（研究动机与背景）

- **研究背景**：仓库级代码理解是 LLM 辅助软件工程的核心能力。真实任务要求模型跨多个文件导航、追踪跨模块的控制流与数据流，并验证实现是否符合设计意图。然而，现有的代码问答基准多聚焦于片段级（snippet-centric）问题，无法反映上述行为；仅靠知识提示（knowledge-only prompting）会掩盖模型在导航与证据定位上的弱点。
- **两个关键缺口**：
  - **多样性不足**：现有基准集中在少数热门仓库（如 SWE-Bench 中的经典项目），大量自然任务分布未被覆盖，某些语义类别（配置、数据管道、基础设施胶水代码等）代表性不足。
  - **工具必要性不明确**：许多基准问题可仅凭预训练知识或公开文档直接回答，导致无法区分"真正理解并操作仓库"与"简单记忆召回"。
- **整体含义**：作者提出 **SWE-QA-Pro**——一个由长尾仓库构成、带可执行环境、经过严格难度校准的仓库级代码理解基准，并配套提出可扩展的合成数据流水线与两阶段训练配方（SFT → RLAIF），使小型开源模型也能习得高效的仓库探索与推理能力。论文的核心主张是：**评测必须隔离出真正需要智能体式代码库探索的问题，且这类能力可以通过训练获得，而不只是靠模型规模**。

## 二、方法论

### 2.1 基准构建：四阶段流水线（图 1a）

1. **数据来源与分类体系构建（Taxonomy Construct）**
   - 对 SWE-Rebench 中 **1,687,638 条 issue**（跨 **3,468 个仓库**）做标题+正文拼接，过滤长度为 10 Byte–16KB 的文本。
   - 用 **Qwen3-8B-Embedding** 计算表示，采用**分层 K-Means**（第一层 10 类、第二层扩展到 50 类）。
   - 用 **GPT-4.1** 为每个簇抽取语义标签，再经人工校验分类体系、消除语义冗余，最终得到 **48 个任务子类**（附录 F）。

2. **数据合成与采样（Data Synthesis）**
   - 复用 SWE-Rebench 的沙箱环境保证可执行性。
   - 每个合成任务从对应簇/仓库随机采样 **20 条现有 issue** 作为参考上下文，由 **Claude Code** 自动探索代码库，生成自包含的"问题–解答"对。
   - **测试集**：选 **26 个仓库**高效覆盖全部 48 类（兼顾人工标注的认知负荷）；**训练集**：在全量数据上均匀采样，覆盖 **1,484 个仓库**。

3. **数据过滤与难度校准（Difficulty Calibration）**
   - 先去除多查询提示，用 Qwen3-8B 嵌入做语义去重。
   - 核心思路：**若强模型在不看仓库的情况下（direct-answer baseline）就能答好，则丢弃该题**。
   - 具体做法：用 **GPT-4o、Claude Sonnet 4.5、Gemini 2.5 Pro** 三个强模型生成"无仓库"直接答案，与 Claude Code 生成的"有仓库"参考答案对比，用 LLM-as-Judge 在 5 个维度打分；对每个模型做 **z-score 标准化**：
     $$z_m(q)=\frac{\bar{s}_m(q)-\mu_m}{\sigma_m}$$
     并以**负的跨模型共识分**定义难度：
     $$\text{Difficulty}(q)=-\frac{1}{|M|}\sum_{m\in M} z_m(q)$$
     高难度题保留、低难度题过滤。最终从 1,908 个候选中保留 696 个，再在仓库/簇/QA 类型平衡约束下选出 **260 题**（仍可被无仓库回答的仅 10 题，误保留率约 3.8%）。

4. **数据验证（Data Validation）**
   - Claude Code 在沙箱中生成"有仓库依据"的参考答案；人工标注者独立探索代码库作答、修正歧义题、核对 QA 类型与语义簇；两者比对后仅保留满足 5 维度质量要求的答案；最后经专家复核裁定剩余不一致。
   - 最终基准：**260 题、26 个长尾仓库、每簇 4–9 题、QA 类型近似均衡**。

### 2.2 SWE-QA-Pro Agent 工作流

- 采用 **ReAct 风格循环**，**完全放弃 RAG 与预建索引**，直接探索仓库。
- 动作空间（长度受限、只读）：
  - **Search**：基于关键词匹配定位相关文件；
  - **View**：按范围查看文件内容或目录结构；
  - **CommandLine**：受约束的只读命令，用于目录遍历、符号匹配、按行抽取等轻量结构/模式分析；
  - **Finish**：证据充分后终止并输出答案。
- 最多 **25 轮**，在 32k 上下文预算下增量收集证据、跨文件推理。

### 2.3 两阶段训练配方（SFT → RLAIF）

- **训练数据构造**：从基准构建流水线去重后得到 1,464 个原始问题，随机划分为 **1,000 题用于 SFT、464 题用于 RL**。SFT 阶段用 **Claude Sonnet 4.5** 在给定动作空间下生成 1,000 条高质量多轮工具调用轨迹；RL 阶段每题配一条 Claude Code 生成的高质量参考答案作为奖励真值。
- **第一阶段 SFT**：在 Qwen3-8B 上监督微调，教会模型工具调用语法与工具语义/使用模式。
- **第二阶段 RLAIF**：对 SFT 初始化模型做强化学习。由于答案复杂、无法用精确匹配或规则奖励，采用 **LLM-as-Judge 奖励**，沿 5 个维度（正确性、完整性、相关性、清晰度、推理质量）打分：
  $$s=\text{RM}(\hat{a},a^*)\in[1,10]^5,\qquad r=\frac{w^\top s}{10},\quad w=(0.3,0.2,0.2,0.1,0.2)$$
  即**加大正确性权重、降低清晰度权重**，抑制"流畅但错误"的答案。为防止奖励作弊，**奖励评判模型与评测评判模型不同**。用 **GRPO** 优化策略，奖励在 rollout 组内归一化后再算策略梯度。

## 三、实验设计

### 3.1 数据集 / 基准 / 场景

- **基准**：SWE-QA-Pro Bench（260 题、26 个长尾 Python 仓库、48 个语义簇、4 类问题意图：What / Why / Where / How）。
- **两种评测设置**：**直接回答**（无工具、单轮）与 **Agent 工作流**（SWE-QA-Pro Agent）。

### 3.2 对比方法（共 11 个 LLM）

- **闭源模型**：GPT-4o、GPT-4.1、Claude Sonnet 4.5、Gemini 2.5 Pro、DeepSeek-V3.2；
- **开源模型**：Qwen3-8B、Qwen3-32B、Devstral-Small-2-24B-Instruct、LLaMA-3.3-70B-Instruct；
- **自训练模型**：SWE-QA-Pro-8B（SFT）与 SWE-QA-Pro-8B（SFT+RL）。

### 3.3 评估协议

- 沿用 SWE-QA 的 LLM-as-Judge 协议：严格评判者–候选者分离、匿名化、答案顺序随机化；
- 相比 SWE-QA 更严格：要求显式给出**文件路径与行号引用**，评判提示更严格；
- 每个答案独立评 3 次取平均以降方差。

### 3.4 主要实验组

- **主结果表（表 2）**：11 模型 × 2 设置；
- **工具使用分析（图 4）**：工具调用量与性能的关系；
- **训练策略分析（图 5）**：SFT-1000、SFT-1464、SFT-1000+RL-464 对比；
- **附录补充实验**：
  - 不确定性量化（95% CI、三次评分标准差，表 3、表 4）；
  - 与 **Function-Chunking RAG**、**SWE-QA Agent** 的受控对比（5 个代表模型，表 5）；
  - **评判者敏感性分析**（换用 DeepSeek V3.2 作 judge，表 6）；
  - 过滤有效性分析（1,908 候选的人工标注，误保留率 3.8%）；
  - **监督来源消融**：Claude 监督 vs. Devstral-Small-2 监督（表 7）；
  - 按 QA 类型、仓库、语义簇的细分结果（附录 H，表 16–21）；
  - 案例研究（附录 I）。

## 四、资源与算力

- **文中明确提到**：所有推理使用 **NVIDIA A100 80GB GPU**，温度 0、最多 25 轮、32k 上下文窗口；SFT 用 **SWIFT** 实现，RL 用 **Verl-Tool** 实现。
- **未明确说明**：GPU **具体数量**、训练**总时长/总 GPU 小时**、推理总开销等均未在正文或附录中给出。
- 附录 D 提供了训练超参数（bfloat16、最大序列长 32,768、AdamW、学习率 5×10⁻⁶、权重衰减 0.05、cosine 调度、warmup 0.05、每设备 batch size 1、梯度累积 2、4 个 epoch；RL 侧 max turns 25、max prompt 2,048、max response 8,192、max observation 28,000、温度 1.0、top-p 1.0、rollout 数 n=8、KL 系数 0.02、actor 学习率 1×10⁻⁶、batch size 8、PPO mini-batch 8、FSDP 策略、最大模型长 32,768），但**算力总量信息缺失**。

## 五、实验数量与充分性

- **实验规模**：主实验 11 个模型 × 2 种设置；训练策略 3 组对比；受控基线对比 5 模型 × 3 方法；评判者敏感性 6 模型；监督来源消融 2 组；另有按 QA 类型（12 子类）、仓库（26 个）、语义簇（48 个）的多维细分，以及不确定性量化与多个案例研究。整体实验组数较多、覆盖面较广。
- **充分性**：
  - **优点**：既有主结果又有大量消融与稳健性分析（CI、judge 替换、RAG 基线对照、监督来源对照），并公开了完整提示模板、超参数与分类体系，可复现性较好；对训练策略做了 SFT 数据量 vs. RL 的受控比较，能较清晰地区分两种监督信号的作用。
  - **不足**：测试集仅 260 题、26 个仓库，簇级样本仅 4–9 题，簇级 CI 较宽（作者自己也提示 1–3 分的簇间差异需谨慎解读）；仅覆盖 Python 生态。
- **客观性与公平性**：
  - 采用严格评判者分离、匿名化、随机顺序、三次平均，且做了**换 judge 的敏感性分析**，排名保持稳定，说明结论对 judge 选择不过度敏感；
  - 但 RLAIF 奖励与评测指标**同源（均为 LLM-as-Judge）**，存在指标与训练目标分布接近的隐忧；作者也承认这一点。
  - 训练数据来自 Claude，测试基准也部分由 Claude Code 参与构建，存在一定的"同源"偏差风险，作者通过 Devstral 监督消融部分回应了这一问题。

## 六、主要结论与发现

1. **智能体工作流显著优于直接回答**：直接回答与 agent 设置之间存在大幅性能差距（如 Claude Sonnet 4.5 约 **13 分**差距），
