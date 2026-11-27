---
title: "Program Structure-aware Language Models: Targeted Software Testing beyond Textual Semantics"
title_zh: 程序结构感知语言模型：超越文本语义的定向软件测试
authors: "Khang Tran, Khoa Nguyen, Cristian Borcea, Hai Phan"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://aclanthology.org/2026.findings-acl.540.pdf"
tags: ["query:ai-se"]
score: 9.0
evidence: 基于程序结构的LLM定向测试用例生成
tldr: 现有大模型测试生成虽通过提示变异提升分支覆盖率，却缺乏引导模型针对高风险分支的原则性机制。GLMTest提出首个程序结构感知的LLM框架，用图神经网络与语言模型融合代码属性图与语义，将测试生成条件化到具体执行分支。实验表明其能实现可控的分支定向测试生成，有助于发现隐蔽缺陷与安全漏洞。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl540/fig-001.webp\", \"caption\": \"\", \"page\": 3, \"index\": 1, \"width\": 511, \"height\": 316}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl540/fig-002.webp\", \"caption\": \"\", \"page\": 4, \"index\": 2, \"width\": 4367, \"height\": 1434}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl540/fig-003.webp\", \"caption\": \"\", \"page\": 7, \"index\": 3, \"width\": 3469, \"height\": 1741}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl540/fig-004.webp\", \"caption\": \"\", \"page\": 7, \"index\": 4, \"width\": 583, \"height\": 284}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl540/fig-005.webp\", \"caption\": \"\", \"page\": 7, \"index\": 5, \"width\": 583, \"height\": 284}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl540/fig-006.webp\", \"caption\": \"\", \"page\": 7, \"index\": 6, \"width\": 583, \"height\": 284}]"
motivation: 现有LLM测试生成缺乏引导模型针对高风险执行分支的原则性机制。
method: 用图神经网络与语言模型融合代码属性图和语义，将测试生成条件化到执行分支。
result: 实现可控的分支定向测试生成，提升对隐蔽缺陷的发现能力。
conclusion: 程序结构感知的条件化方法增强LLM定向测试的有效性。
---

## Abstract
Recent advances in large language models for test case generation have improved branch coverage via prompt-engineered mutations. However, they still lack principled mechanisms for steering models toward specific high-risk execution branches, limiting their effectiveness for discovering subtle bugs and security vulnerabilities. We propose GLMTest , the first program structure-aware LLM framework for targeted test case generation that seamlessly integrates code property graphs and code semantics using a graph neural network and a language model to condition test case generation on execution branches. This structured conditioning enables controllable and branch-targeted test case generation, thereby potentially enhancing bug and security risk discovery. Experiments on real-world projects show that GLMTest built on a Qwen2.5-Coder-7B-Instruct model improves branch accuracy from 27.4% to 50.2% on TestGenEval benchmark compared with state-of-the-art LLMs, i.e., Claude-Sonnet-4.5 and GPT-4o-mini.

---

## 论文详细总结（自动生成）

# 论文结构化总结：GLMTest —— 程序结构感知的定向软件测试

## 1. 核心问题与研究动机

- **背景**：大语言模型（LLM）已被广泛用于自动化测试用例生成，现有方法（提示工程变异、微调、检索增强）在整体分支覆盖率上有所提升。
- **核心痛点**：
  - 现有方法主要依赖**提示工程启发式**，受 LLM 随机性影响，生成过程**难以控制**，缺乏将模型引导至特定执行分支的原则性机制。
  - **纯文本表示**无法充分刻画代码对象间的结构依赖关系，限制模型对程序结构与执行行为的理解，难以精准引导执行路径。
  - 结果：提示工程生成的测试用例常**无法覆盖安全关键路径**，对隐蔽缺陷与安全漏洞的发现能力受限。
- **研究目标**：提出首个**程序结构感知（program structure-aware）**的 LLM 框架，实现**可控、以分支为目标**的测试用例生成，服务高风险分支测试与覆盖率驱动测试流水线。

## 2. 方法论（GLMTest）

### 核心思想
将程序表示为**代码属性图（CPG）**，用**异构图神经网络（GNN）**提取与目标分支对齐的结构嵌入，并与 LLM 的文本嵌入**联合训练、拼接注入**，从而让测试生成以具体执行分支为条件。

### 关键技术细节
- **CPG 建模**：$G=(V,E)$，节点 $v$ 对应语句/表达式/变量/函数，特征向量 $x_v\in\mathbb{R}^d$；边按关系类型划分为 $E=\bigcup_j E_j$，构成异构多关系图。
- **分支掩码**：对目标分支 $b$，依据执行行号与节点源码位置区间对齐，构造二值掩码 $m\in\{0,1\}^{|V|}$，标记与分支相关的节点集合 $V_b$。
- **异构 GNN 编码**：采用 $K$ 层异构 GNN（默认 3 层 GAT，每层 8 头），按关系类型做邻域聚合与消息传递；最后一层用 pooling 融合各关系嵌入，得到节点嵌入 $h^K_v$。
- **分支嵌入**：将 $V_b$ 内节点嵌入堆叠为 $e_b\in\mathbb{R}^{|V_b|\times d_h}$，保留节点级细粒度结构信息（而非池化为单一向量）。
- **注入 LLM**：在提示模板中设置图占位符 `<|graph_pad|>`，用分支嵌入 $e_b$ 替换其嵌入，与文本嵌入拼接为 $e_{inp}$，输入 LLM（默认 Qwen2.5-Coder-7B-Instruct）。
- **端到端训练**：GNN 与 LLM 联合优化，目标为最小化 token 级损失加 $\ell_2$ 正则：
  $$\theta^*=\arg\min_\theta \sum_{i=1}^{|D|}\ell(t_i,\hat t_i)+\lambda\|\theta\|^2,\quad \hat t_i=f_{lm}(e_{p_i},f_g(G,m_i))$$
  由于拼接操作可微，梯度可回传至 GNN，实现结构条件化的联合训练。
- **训练数据构建**：从真实项目的人工测试套件出发，拆解单个测试用例、去除冗余 import/死代码、在 Docker 环境执行并用 `coverage.py` 记录执行分支，形成 `(program, branch, test case)` 三元组。

### 推理方式
- **定向模式**：开发者指定代码位置（行/块/函数），框架自动导出分支并生成针对性测试。
- **覆盖驱动模式**：枚举静态可分析分支，逐分支生成测试，汇总为测试套件以提升覆盖率。

## 3. 实验设计

- **数据集 / Benchmark**：基于 **TestGenEval**（源自 SWEBench，含 68,647 个测试用例、1,210 个模块、Docker 可执行环境）。经处理后得到 **40,868 个训练数据点、1,344 个测试实例**，覆盖 7 个 Python 项目（astropy、django、xarray、pytest、scikit-learn、sympy 等，见表 2）。
- **评价指标**：Pass@1（可执行性/正确性）、Branch Coverage（BranchCov，覆盖率）、Branch Accuracy（BranchAcc，是否命中目标分支）、Branch Overlap（BranchOverlap，目标分支被覆盖比例）。
- **对比方法**：
  - **提示工程（PE）**：Claude-Sonnet-4.5、GPT-4o-mini（TestGenEval 原始提示模板）。
  - **纯文本微调（FT）**：同一 Qwen2.5-Coder-7B 骨干，去掉 GNN，仅用文本分支描述。
  - **执行反馈基线**：提供生成测试与执行分支，要求模型迭代修正。
  - **RAG 增强基线**：检索 top-3 相似训练样本作为上下文示例。
  - （说明）ASTER、CodaMOSA 因与 TestGenEval 容器化设置不兼容，未能复现，未报告其数字。

## 4. 资源与算力

- **GPU**：4 × A100（每卡占用约 50GB 显存）。
- **训练配置**：2,048 个优化步，每设备 batch size 8，梯度累积 32，最大序列长度 8,192；采用 LoRA（rank 8）与 DeepSpeed。
- **时长 / 成本**：约 48 小时墙钟时间（约 **192 GPU-hours**），处理约 $5.37\times10^8$ tokens；在 Vast.ai 上花费约 **$119.56**。
- 结论：微调预算较小，实践可负担。

## 5. 实验数量与充分性

- **实验组数概览**：
  - RQ1：与 PE（两个商用 LLM）、FT、执行反馈、RAG 四类基线对比（含逐仓库结果，如 django、xarray）。
  - RQ2：分支定向推理下的 Pass@1 与 BranchCov；另设无分支目标的自由生成对照。
  - RQ3：消融实验——GNN 结构（GAT vs GraphSAGE vs 无 GNN）、聚合机制（节点级 vs 图级池化）、模型规模（7B vs 14B）、训练成本。
- **充分性评价**：
  - 消融覆盖较全面，能有效隔离 GNN 结构条件化的贡献（如 xarray 上 FT 的 BranchAcc 为 0.00，GLMTest 为 0.61，信号明显）。
  - 对比基线类型多样（提示、微调、执行反馈、RAG），并统一解码预算与评测流程，**公平性较好**。
  - **局限**：训练/测试来自**同一批项目**（仅测试用例不重叠），跨项目泛化未验证；受容器环境限制未能与 ASTER/CodaMOSA 直接对比；正文与附录在数据规模上存在细微不一致（正文 40,868/1,344，附录提及 45,831/1,489，表 2 采用前者），需注意。

## 6. 主要结论与发现

- **分支命中能力大幅提升**：BranchAcc 从 0.274（GPT-4o-mini）/ 0.292（Claude-Sonnet-4.5）提升至 **0.502**（相对提升 **71.9%**）；BranchOverlap 从约 0.615 提升至 **0.794**。
- **小模型 + 结构条件化可媲美/超越大模型**：7B 开源模型经结构条件化后优于商用大模型；django 上 BranchAcc 从 0.46 升至 0.68，覆盖比例从 0.63 升至 0.91。
- **GNN 贡献显著**：相比纯文本 FT，BranchAcc 0.44→0.50，BranchOverlap 0.71→0.80。
- **优于执行反馈与 RAG**：执行反馈基线仅 26.5%/28.5% BranchAcc；RAG 基线 31.8%/30.1%，均明显低于 GLMTest。
- **测试套件质量更高**：分支定向设置下 Pass@1 约 **0.85**，远超 PE 的约 0.41；自由生成设置下仍最高（0.85 vs 0.71/0.67）。
- **消融结论**：GAT 优于 GraphSAGE（0.502 vs 0.465）；节点级掩码显著优于图级池化（0.502 vs 0.399）；14B 模型 BranchAcc 略降（49.3%）但 BranchCov 略升（17.63% vs 16.91%），说明结构条件化在中等规模已能提供强分支推理能力。

## 7. 优点

- **方法创新性**：首个将 CPG 结构信息以**节点级、分支对齐**方式注入 LLM 的测试生成框架，实现细粒度、可解释、可控的分支定向生成。
- **端到端联合训练**：GNN 与 LLM 共享目标函数、梯度可回传，避免了“图特征仅作序列级辅助”的浅层融合。
- **实用性强**：可无缝接入安全分析（定向高风险路径）与模糊测试（高质量种子）流水线；支持覆盖驱动模式。
- **成本友好**：$119.56、192 GPU-hours 的微调预算，降低了复现与落地门槛。
- **实验设计严谨**：多类基线对比、统一解码预算、逐仓库分析、四组消融，且公开数据集与代码。
- **诚实披露**：明确说明 ASTER/CodaMOSA 的不兼容性与复现尝试，附录详述数据构建与实现细节。

## 8. 不足与局限

- **泛化性有限**：训练仅覆盖 TestGenEval 中少数项目，且测试与训练共享项目，**跨项目/跨仓库泛化未验证**。
- **大规模系统开销高**：对含数千可行分支的大型模块逐分支生成不现实，需依赖分支优先级机制（作者亦指出需结合静态安全风险检测）。
- **静态 CPG 的固有缺陷**：语法上存在的分支可能因死代码或不可满足的运行时约束而**不可达**，需动态分析（如 PyAnalyzer）辅助。
- **语言覆盖单一**：实验仅限 Python；虽声称 Joern 支持多语言，但数据构建需语言特定环境。
- **基线覆盖受限**：未能与 ASTER、CodaMOSA 等直接对比，削弱了与最相关工作的可比性。
- **训练范式单一**：仅用 SFT，未探索 RLHF 等对齐方法（作者列为未来工作）。
- **数据规模表述存在细微不一致**（正文 vs 附录），可能影响复现时的数据核对。

（完）
