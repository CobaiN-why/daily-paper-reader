---
title: "KoCo-Bench: Can Large Language Models Leverage Domain Knowledge in Software Development?"
title_zh: KoCo-Bench：大语言模型能否在软件开发中运用领域知识？
authors: "Xue Jiang, Ge Li, Jiaru Qian, Xianjie Shi, Chenjie Li, Hao Zhu, Ziyu Wang, Jielun Zhang, Zeyu Zhao, Kechi Zhang, Jia Li, Wenpin Jiao, Zhi Jin, Yihong Dong"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://aclanthology.org/2026.acl-long.1311.pdf"
tags: ["query:ai-se"]
score: 8.0
evidence: 评估大模型在软件开发中领域知识的基准
tldr: 大模型擅长通用编程，但在领域特定软件开发中表现不佳，而现有代码基准多只考察模型已具备的知识，缺乏用于研究知识获取与应用的语料。作者提出KoCo-Bench，覆盖6个新兴领域、11个软件框架和25个项目，并提供精选知识语料以评估领域专门化方法。该基准强调模型如何学习并运用新领域知识，为面向真实软件开发的领域适配研究提供了系统评测基础。
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1311/fig-001.webp\", \"caption\": \"\", \"page\": 2, \"index\": 1, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1311/fig-002.webp\", \"caption\": \"\", \"page\": 2, \"index\": 2, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1311/fig-003.webp\", \"caption\": \"\", \"page\": 2, \"index\": 3, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1311/fig-004.webp\", \"caption\": \"\", \"page\": 2, \"index\": 4, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1311/fig-005.webp\", \"caption\": \"\", \"page\": 2, \"index\": 5, \"width\": 977, \"height\": 1360}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1311/fig-006.webp\", \"caption\": \"\", \"page\": 2, \"index\": 6, \"width\": 2625, \"height\": 1595}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1311/fig-007.webp\", \"caption\": \"\", \"page\": 2, \"index\": 7, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1311/fig-008.webp\", \"caption\": \"\", \"page\": 2, \"index\": 8, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1311/fig-009.webp\", \"caption\": \"\", \"page\": 2, \"index\": 9, \"width\": 512, \"height\": 512}]"
motivation: 大模型擅长通用编程却难以胜任领域特定软件开发，现有基准只考察已有知识而非知识的获取与应用。
method: 构建KoCo-Bench基准，涵盖6个领域、11个软件框架与25个项目，并提供精选知识语料支持领域专门化评估。
result: 该基准为衡量大模型获取和应用领域知识的能力提供了系统化的评测环境。
conclusion: 推动面向真实软件开发的领域专门化方法研究与评测。
---

## Abstract
Large language models (LLMs) excel at general programming but struggle with domain-specific software development. This gap motivates research into domain specialization methods that enable LLMs to learn and utilize domain knowledge and data. However, existing domain-specific code benchmarks focus on assessing what knowledge LLMs possess rather than how they acquire and apply new knowledge, lacking explicit knowledge corpora for developing domain specialization methods. To this end, we present KOCO-bench, a novel benchmark designed for evaluating domain specialization methods in real-world software development. KOCO-bench contains 6 emerging domains with 11 software frameworks and 25 projects, featuring curated knowledge corpora alongside multi-granularity evaluation tasks including domain code generation (from function-level to project-level with rigorous test suites) and domain knowledge understanding (via multiple-choice Q A). Unlike previous benchmarks that only provide test sets for direct evaluation, KOCO-bench requires acquiring and applying diverse domain knowledge (APIs, rules, constraints, etc.) from the corpora to solve evaluation tasks. Our evaluations reveal that KOCO-bench poses significant challenges to state-of-the-art LLMs. Even with domain specialization methods (e.g., SFT, RAG, kNN-LM) applied, improvements remain marginal. Best-performing coding agent, Claude Code, achieves only 34.2%, highlighting the urgent need for more effective domain specialization methods. We release KOCO-bench, evaluation code, and baselines to advance further research at https://github.com/jiangxxxue/KOCO-bench.

---

## 论文详细总结（自动生成）

# KoCo-Bench 论文中文总结

## 1. 核心问题与整体含义（研究动机与背景）

- **研究背景**：大语言模型（LLM）在通用编程任务上表现优异（如 HumanEval 上 Pass@1 超过 90%），但在**领域特定软件开发**中表现明显不足。领域开发依赖专有规则、流程、API、协议、依赖与约束等专门知识，而这些知识分散在文档、源码和示例中，训练语料有限且快速演化。
- **核心问题**：现有领域特定代码基准（如 EvoCodeBench、DomainEval、DomainCodeBench、MultiCodeBench）只评估模型"已经掌握什么知识"，而不是"如何学习并应用新知识"；它们只提供测试集与仓库上下文，**缺少显式的领域知识语料**，因此无法支撑领域专门化方法（SFT、RAG、kNN-LM 等）的研究与建模。
- **研究意义**：作者提出 **KoCo-Bench**，通过"知识语料 + 配套测试集"的配对设计，模拟开发者基于陌生框架开发新项目的真实场景，系统评估 LLM 获取、理解并应用领域知识的能力，从而推动更有效的、面向软件工程的领域专门化方法研究。

## 2. 方法论：核心思想与关键技术细节

- **核心思想**：以"软件框架"作为领域知识的天然载体——框架既包含核心抽象、设计模式与实现逻辑，又配有文档与示例，且开发者基于框架构建项目，形成自然的知识复用生态。基准据此由**知识语料**与**测试集**两部分组成。
- **知识语料构建**：
  - 三个来源：框架官方文档、框架源代码、框架使用示例。
  - 筛选条件：2024 年 3 月之后创建、文档完善的 Python 框架，按 GitHub 星数取前 10，覆盖 RL、Agent、RAG、模型优化、具身 AI 五个领域；另加入两个昇腾（Ascend）AI 处理器的底层加速/支持框架（一个 Python、一个 C++），共 11 个框架。
  - 规模：平均每领域 77.0k 行，最大 400.5k 行。
- **领域代码生成任务**：
  - **需求描述分三级**：项目描述（整体需求概览）、模块划分描述（结构、职责与交互）、核心函数描述（核心方法细节）。撰写时聚焦问题域而非代码实现，排除 config/utils 等工具函数，避免冗余或歧义的非功能需求。
  - **需求澄清流程**：采用多智能体 + 人在回路——先让智能体按需求尝试写代码以暴露歧义，问题反馈给人工与另一智能体复核并增强需求，迭代直至人工确认清晰完整。
  - **测试套件**：单元测试针对核心函数（优先复用项目已有测试；缺失时先写覆盖全分支的输入并用 `coverage.py` 验证分支覆盖，运行真实代码获得期望输出，再由智能体生成测试代码）；对无显式输入输出的函数用插桩验证调用序列；集成测试复用项目流水线脚本或手写，验证多模块交互。所有测试须在 Docker 环境中对真实代码通过验证。
- **领域知识理解任务**：
  - 对无法匹配代码生成项目的框架（如昇腾相关框架）构建**多选题 Q&A**（支持单选与多选、可跳过），遵循四条原则：只考领域知识、答案可验证、每题原子性且答案唯一、题型多样化（含需跨多文件综合信息的复杂题）。
  - 流程：人工编写高质量示例作提示 → 智能体规模化生成 → 用三个训练截止早于数据集截止的 LLM（Qwen2.5-Coder-7B-Instruct、Llama-3.1-8B-Instruct、Deepseek-Coder-7b）过滤"三模型全对"的简单题 → 人工复核修订。
- **评估指标**：代码生成用 Pass@1（全部测试通过）、APR（AvgPassRate，平均测试通过比例）及 Pass@any（多次采样至少一次通过）；知识理解用 Accuracy（ACC）；默认贪心解码（temperature=0），Pass@any 用 temperature=0.8 采样 10 次。

## 3. 实验设计

- **数据集/场景**：KoCo-Bench 覆盖 6 个新兴领域（RL、Agent、RAG、模型优化、具身 AI、昇腾生态），11 个框架、25 个项目、131 个核心函数、978 个测试（每核心函数平均 8.6 个单元测试，每项目平均 2.3 个集成测试）、107 道 Q&A。代码生成任务实际覆盖 RL、Agent、RAG、模型优化四个领域；具身 AI 与昇腾生态仅做知识理解评测。
- **对比的 LLM（10 个）**：Gemini-2.5-pro、Claude-Sonnet-4-5、Kimi-K2-Instruct、DeepSeek-V3.1、GPT-5-mini、o4-mini、Qwen2.5-Coder-32B/7B-Instruct、Llama-3.1-8B-Instruct、Deepseek-Coder-7B，并标注各自训练数据截止日期。
- **领域专门化方法**：SFT（全参数微调）、LoRA、RAG（BM25 检索，函数级/类级分块，top-5）、kNN-LM；另适配代码专用方法 KNM-LM、DSCC；附录补充稠密 RAG（EmbeddingGemma）与指令微调式微调（用 Gemini-3-Flash 合成需求-代码对）。基座模型统一为 Qwen2.5-Coder-7B-Instruct（训练截止早于数据集截止）。
- **智能体方法**：SWE-Agent、OpenHands（均基于 Qwen2.5-Coder-32B-Instruct）与 Claude Code（基于 Claude-Sonnet-4-5），均可完整访问项目文件夹与知识语料，进行迭代探索、生成与执行验证。
- **附加分析实验**：
  - 持续学习中的知识遗忘/冲突（单框架、同领域多框架、跨领域多框架三种设置）；
  - 知识语料规模对 SFT/LoRA/RAG 效果的影响；
  - 错误类型分布分析；
  - 项目级代码生成的定性分析（附录 B）；
  - 数据污染检测（CDD 方法，附录 H）；
  - 性能-成本权衡分析（附录 I）；
  - 智能体控制实验（统一用 Claude-Sonnet-4-5 作基座，附录 G）；
  - SFT 最大序列长度消融（2048/4096/8192，附录 E）；
  - Pass@any 上界分析（附录 F）；
  - 两个失败案例研究（附录 J）。

## 4. 资源与算力

- **论文未明确报告所用 GPU 型号、数量与总训练时长**。
- 仅给出训练超参数：SFT 学习率 5×10⁻⁶、余弦衰减、5 个 epoch、最大序列长度 2048、BF16 精度；LoRA 学习率 1×10⁻⁴、rank r=16、alpha=32、dropout 0.05、5 个 epoch。
- 智能体实验设置：max_turns=30、每任务超时 3000 秒；并报告了各方法的平均每样本 token 消耗（如 Claude Code 约 619,923 tokens，SWE-Agent 约 26,583，OpenHands 约 26,005）。
- 基准构建成本：28.5 人月（代码生成标注 7 人 × 2 个月，Q&A 标注 3 人 × 1.5 个月）。

## 5. 实验数量与充分性

- **实验组数**：主体实验包括约 10 个 LLM × 6 领域的性能评测（表 3）、5 种领域专门化方法对比（表 4）、3 种智能体 + 基座对比（表 5）、持续学习三设置（表 6）、语料规模分析（图 3）、错误分布（图 4）；附录另有代码专用方法（表 8）、补充基线（表 9）、序列长度消融（表 10）、Pass@any（表 11–12）、智能体控制实验（表 13）、污染检测（表 14）、成本分析（图 5）及两个案例研究。整体实验规模较大、维度较丰富。
- **充分性**：在方法覆盖（训练式、检索式、混合式、智能体式）、分析深度（遗忘、规模效应、错误类型、成本）与污染控制方面较为充分；对开源/闭源智能体差异还做了控制实验。
- **客观性与公平性**：
  - 优点：所有测试须对真实代码通过验证，评估基于执行结果而非文本相似度或 LLM 打分，客观性强；基座模型训练截止早于数据集截止，并用 CDD 做污染检测（知识语料平均污染指数 0.08，测试集仅 0.005）。
  - 可质疑之处：智能体对比中开源智能体用 Qwen2.5-Coder-32B、Claude Code 用 Claude-Sonnet-4-5，存在基座模型混杂，虽附录 G 做了控制实验但智能体框架本身差异仍未完全隔离；RAG 领域所有非智能体方法均为 0 分，任务区分度与难度对齐存在争议；项目级生成仅做定性分析，缺乏定量结论。

## 6. 主要结论与发现

- ❶ 即便 SOTA 闭源 LLM 在领域代码生成上也很弱：最佳 Pass@1 仅 8.9%（Kimi-K2-Instruct）与 8.5%（Gemini-2.5-pro），知识理解最高仅 53.5% 准确率，与通用基准 90%+ 形成鲜明反差。
- ❷ 现有领域专门化方法提升有限且跨领域效果不一致：RAG 最佳（平均 Pass@1 7.4%，理解 30.3%），SFT 次之；代码专用方法 KNM-LM、DSCC 甚至低于基座模型。
- ❸ 智能体方法目前最有效：Claude Code 平均 Pass@1 达 34.2%，在 RAG 领域达 62.5%（证明任务在正确知识获取下可解），但距离实用仍有很大差距；开源智能体（SWE-Agent 4.5%、OpenHands 3.6%）受基座智能体能力弱、指令漂移、工具调用循环等问题制约。
- ❹ 基于学习的方法随知识语料增大效果反而下降（SFT、LoRA 呈负相关，RAG 基本不受影响）；跨领域持续学习

（接上文）

- ❹（续）**跨领域持续学习会显著加剧知识遗忘与知识冲突**。论文比较了单框架、同领域多框架、跨领域多框架三种持续学习设置，整体趋势是：学习框架越多、领域跨度越大，模型对先前框架知识的保持能力越差；同领域多框架尚可部分迁移，跨领域多框架则更容易出现“学新忘旧”和相互干扰。SFT/LoRA 在持续学习中遗忘更明显，RAG 相对稳健但绝对性能仍低，说明“外挂检索”能缓解遗忘，却不能替代真正的领域知识内化。
- ❺ **知识语料规模并非越大越好**。SFT、LoRA 的效果随知识语料增大呈负相关，RAG 基本不受影响。作者对此的解释可概括为：语料扩大后噪声、冗余与分布不匹配增加，而全参数/低秩微调容易过拟合表面模式或稀释目标任务信号；RAG 因按需检索，对语料规模不敏感，但也受检索质量上限约束。这一发现对“堆数据做领域适应”的直觉构成反例。
- ❻ **错误类型集中在领域知识缺口与工程约束遗漏**。据论文错误分布分析，失败主要来自：领域 API/参数误用、框架特有抽象与设计模式理解错误、跨模块交互与状态管理错误、隐含约束与非功能要求遗漏、以及生成代码与测试期望不匹配。单纯语法错误占比相对有限，说明瓶颈不在“会写 Python”，而在“不懂该领域如何正确写”。
- ❼ **智能体方法存在明显的性能—成本权衡**。Claude Code 平均 Pass@1 最高，但每样本 token 消耗约 62 万，远高于 SWE-Agent（约 2.66 万）和 OpenHands（约 2.60 万）；开源智能体成本低一个数量级，却受基座能力、指令漂移、工具调用循环与验证策略不足制约。论文的成本分析表明，当前智能体收益高度依赖强基座与充分的探索—验证循环。
- ❽ **数据污染风险较低但并非为零**。CDD 检测显示知识语料平均污染指数约 0.08、测试集约 0.005，配合基座训练截止早于数据集截止的设计，结论受污染影响的可能性较小；但新兴框架文档与示例仍可能通过模型预训练间接泄漏，需持续动态更新与复检。
- ❾ **定性案例显示“可解性”与“脆弱性”并存**。项目级案例中，智能体在能正确检索并理解框架文档/示例时，可以完成多模块协作与调试；失败案例则多表现为过早停止、反复调用工具而无有效验证、误解模块职责或忽略集成约束。这说明 KoCo-Bench 的任务在知识可得时并非不可解，但当前智能体的知识获取与验证流程仍很脆弱。

## 7. 局限性与可改进之处

- **领域与语言覆盖有限**：基准以 Python 框架为主，仅含少量 C++ 昇腾框架；6 个领域虽具代表性，但相对软件工程整体仍偏窄，结论向其他语言、传统企业软件、强合规/强实时系统外推需谨慎。
- **构建成本高、动态维护难**：28.5 人月的人工标注与多智能体+人在回路澄清流程保证了质量，但也意味着基准难以高频更新；新兴框架演化快，知识语料与测试集存在时效性衰减风险。
- **任务难度分布不均衡**：RAG 领域非智能体方法普遍为 0 分，虽凸显难度，但也可能降低方法间的区分度；部分框架仅用于知识理解 Q&A，代码生成覆盖不完整，跨领域可比性受影响。
- **评估以测试通过为主**：Pass@1/APR 客观可复现，但对非功能需求（性能、安全、可维护性、风格一致性）覆盖不足；项目级生成仅做定性分析，缺少规模化定量指标。
- **智能体对比存在混杂因素**：开源智能体与 Claude Code 的基座模型不同，附录控制实验缓解但未完全隔离“智能体框架”与“基座能力”的贡献；工具预算、超时与提示策略也可能影响结果。
- **知识语料质量与检索粒度仍有优化空间**：RAG 采用 BM25 与函数级/类级分块、top-5，稠密检索仅在附录补充；如何构建结构化知识图谱、分层检索、跨文件依赖感知的检索，仍是提升空间。
- **持续学习实验规模有限**：三种设置揭示了遗忘/冲突趋势，但未系统比较持续学习算法（回放、正则、适配器隔离等），对“如何学而不忘”的方法论指导仍偏初步。

## 8. 对后续研究的启发

- **从“评估已知”转向“评估学习”**：KoCo-Bench 的配对设计提示，领域代码基准应显式提供可学习知识语料，并区分“知识理解”与“知识应用”，以便公平比较 SFT、RAG、kNN-LM、智能体等不同专门化路径。
- **知识注入需要“少而准”而非“多而杂”**：语料规模负相关的结果提示，未来应研究数据筛选、去噪、难度课程、知识冲突检测与结构化组织，而非简单扩大领域语料。
- **检索与智能体结合是短期最有希望的方向**：RAG 稳健但上限受检索质量限制，智能体上限高但成本与脆弱性突出；将分层检索、依赖感知、执行反馈与自动验证结合，可能兼顾性能与成本。
- **持续学习需显式处理遗忘与冲突**：跨领域多框架场景是现实开发常态，未来可探索参数隔离、适配器路由、知识编辑、回放与检索增强的混合方案。
- **基准应持续动态化与多维化**：需要定期更新框架版本、引入更多语言与领域、补充非功能指标与项目级定量评估，并公开污染检测与成本报告，提升可复现性与公平性。

（完）
