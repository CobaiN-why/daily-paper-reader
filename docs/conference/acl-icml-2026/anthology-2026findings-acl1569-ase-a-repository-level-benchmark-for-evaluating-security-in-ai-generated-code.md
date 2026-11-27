---
title: "A.S.E: A Repository-Level Benchmark for Evaluating Security in AI-Generated Code"
title_zh: A.S.E：评测AI生成代码安全的仓库级基准
authors: "Keke Lian, Wang Bin, Lei Zhang, Libo Chen, Junjie Wang, Ziming Zhao, Yujiu Yang, Miaoqian Lin, Haotong Duan, Haoran Zhao, Shuang Liao, Mingda Guo, Quan Jiazheng, Yilu Zhong, Chenhao He, Chen Zichuan, Jie Wu, Haoling Li, Zhaoxuan Li, Jiongchi Yu, Hui LI, Dong Zhang"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://aclanthology.org/2026.findings-acl.1569.pdf"
tags: ["query:ai-se"]
score: 8.0
evidence: 面向AI生成代码安全的仓库级基准
tldr: 大模型在软件工程中日益普及，亟需严格评估其生成代码的安全性，但现有基准缺乏对真实AI辅助编程场景的贴合。A.S.E构建仓库级评测基准，贴近真实AI编程任务，系统评估主流大模型生成代码的安全风险。结果显示当前大模型仍存在明显安全隐患，为AI代码生成的安全评估与改进提供了可靠框架。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1569/fig-001.webp\", \"caption\": \"\", \"page\": 4, \"index\": 1, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1569/fig-002.webp\", \"caption\": \"\", \"page\": 4, \"index\": 2, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1569/fig-003.webp\", \"caption\": \"\", \"page\": 4, \"index\": 3, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1569/fig-004.webp\", \"caption\": \"\", \"page\": 4, \"index\": 4, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1569/fig-005.webp\", \"caption\": \"\", \"page\": 5, \"index\": 5, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1569/fig-006.webp\", \"caption\": \"\", \"page\": 5, \"index\": 6, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1569/fig-007.webp\", \"caption\": \"\", \"page\": 5, \"index\": 7, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1569/fig-008.webp\", \"caption\": \"\", \"page\": 5, \"index\": 8, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1569/fig-009.webp\", \"caption\": \"\", \"page\": 5, \"index\": 9, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1569/fig-010.webp\", \"caption\": \"\", \"page\": 5, \"index\": 10, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1569/fig-011.webp\", \"caption\": \"\", \"page\": 5, \"index\": 11, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1569/fig-012.webp\", \"caption\": \"\", \"page\": 5, \"index\": 12, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1569/fig-013.webp\", \"caption\": \"\", \"page\": 5, \"index\": 13, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1569/fig-014.webp\", \"caption\": \"\", \"page\": 5, \"index\": 14, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1569/fig-015.webp\", \"caption\": \"\", \"page\": 5, \"index\": 15, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1569/fig-016.webp\", \"caption\": \"\", \"page\": 5, \"index\": 16, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1569/fig-017.webp\", \"caption\": \"\", \"page\": 5, \"index\": 17, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1569/fig-018.webp\", \"caption\": \"\", \"page\": 5, \"index\": 18, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1569/fig-019.webp\", \"caption\": \"\", \"page\": 5, \"index\": 19, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1569/fig-020.webp\", \"caption\": \"\", \"page\": 5, \"index\": 20, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1569/fig-021.webp\", \"caption\": \"\", \"page\": 5, \"index\": 21, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1569/fig-022.webp\", \"caption\": \"\", \"page\": 5, \"index\": 22, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1569/fig-023.webp\", \"caption\": \"\", \"page\": 5, \"index\": 23, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1569/fig-024.webp\", \"caption\": \"\", \"page\": 5, \"index\": 24, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1569/fig-025.webp\", \"caption\": \"\", \"page\": 5, \"index\": 25, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1569/fig-026.webp\", \"caption\": \"\", \"page\": 5, \"index\": 26, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1569/fig-027.webp\", \"caption\": \"\", \"page\": 5, \"index\": 27, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1569/fig-028.webp\", \"caption\": \"\", \"page\": 5, \"index\": 28, \"width\": 512, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1569/fig-029.webp\", \"caption\": \"\", \"page\": 6, \"index\": 29, \"width\": 1200, \"height\": 1200}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1569/fig-030.webp\", \"caption\": \"\", \"page\": 6, \"index\": 30, \"width\": 1200, \"height\": 1200}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1569/fig-031.webp\", \"caption\": \"\", \"page\": 6, \"index\": 31, \"width\": 1200, \"height\": 1200}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1569/fig-032.webp\", \"caption\": \"\", \"page\": 8, \"index\": 32, \"width\": 1353, \"height\": 1311}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1569/fig-033.webp\", \"caption\": \"\", \"page\": 8, \"index\": 33, \"width\": 1024, \"height\": 1024}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1569/fig-034.webp\", \"caption\": \"\", \"page\": 8, \"index\": 34, \"width\": 401, \"height\": 400}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1569/fig-035.webp\", \"caption\": \"\", \"page\": 8, \"index\": 35, \"width\": 1024, \"height\": 1024}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1569/fig-036.webp\", \"caption\": \"\", \"page\": 8, \"index\": 36, \"width\": 1024, \"height\": 1024}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1569/fig-037.webp\", \"caption\": \"\", \"page\": 8, \"index\": 37, \"width\": 1024, \"height\": 1024}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1569/fig-038.webp\", \"caption\": \"\", \"page\": 16, \"index\": 38, \"width\": 1440, \"height\": 574}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1569/fig-039.webp\", \"caption\": \"\", \"page\": 16, \"index\": 39, \"width\": 1294, \"height\": 460}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1569/fig-040.webp\", \"caption\": \"\", \"page\": 16, \"index\": 40, \"width\": 1346, \"height\": 506}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1569/fig-041.webp\", \"caption\": \"\", \"page\": 16, \"index\": 41, \"width\": 1448, \"height\": 510}]"
motivation: 大模型广泛用于编程，但现有基准难以评估真实场景下生成代码的安全风险。
method: 构建贴近真实AI辅助编程任务的仓库级安全评测基准并评测主流大模型。
result: 评测揭示当前主流大模型生成的代码仍存在明显安全隐患。
conclusion: 为AI生成代码的安全评估与改进提供了可靠评测框架。
---

## Abstract
The increasing adoption of large language models (LLMs) in software engineering necessitates rigorous security evaluation of their generated code. However, existing benchmarks often lack relevance to real-world AI-assisted programming scenarios, making them inadequate for assessing the practical security risks associated with AI-generated code in production environments. To address this gap, we introduce A.S.E (AI Code Generation Security Evaluation), a repository-level evaluation benchmark designed to closely mirror real-world AI programming tasks, offering a comprehensive and reliable framework for assessing the security of AI-generated code. Our evaluation of leading LLMs on A.S.E reveals several key findings. In particular, current LLMs still struggle with secure coding. The complexity in repository-level scenarios presents challenges for LLMs that typically perform well on snippet-level tasks. Moreover, a larger reasoning budget does not necessarily lead to better code generation. These observations offer valuable insights into the current state of AI code generation and help developers identify the most suitable models for practical tasks. They also lay the groundwork for refining LLMs to generate secure and efficient code in real-world applications.

---

## 论文详细总结（自动生成）

# A.S.E 论文中文结构化总结

## 1. 核心问题与研究动机

- **背景**：大语言模型（LLM）在软件工程中的采用日益广泛，Cursor、Claude Code 等 AI 编程助手显著提升了开发效率，但也导致生产环境中出现大量 AI 生成代码。已有研究反复表明，这类代码可能携带安全漏洞，可能引发数据泄露、系统故障等严重风险。
- **核心问题**：现有代码评估基准不足以评估真实生产场景中 AI 生成代码的安全风险，具体表现为三点：
  - **数据相关性有限**：多来源于人工构造的合成代码片段，与真实项目的功能与安全场景脱节；
  - **任务脱离真实 AI 编程范式**：任务多局限于孤立代码片段，缺乏文件内或跨文件上下文，不符合主流 AI 辅助编程方式；
  - **评估方法不可靠**：安全评估依赖人工或 LLM 判定，难以自动化、难以复现。
- **整体含义**：论文提出 **A.S.E（AI Code Generation Security Evaluation）**，一个贴近真实 AI 编程任务的**仓库级**安全评测基准，旨在为开发者与组织提供可靠、可复现的 AI 生成代码安全评估框架。

## 2. 方法论

### 2.1 核心思想
- 以**真实 GitHub 开源仓库 + 已记录 CVE** 为基础，构建仓库级代码生成任务；安全被操作化为“**补丁集成后 CVE 对齐的静态分析告警是否减少**”。
- 三大设计原则：
  - **真实数据源**：从 CVE 补丁中提取漏洞相关代码，并引入语义与结构变异以缓解数据泄漏；
  - **模拟真实 AI 编程工作流**：从仓库中抽取文件内与跨文件上下文，模型输出 unified-diff 补丁，可直接 `git apply`；
  - **高精度可复现评估**：为每个 CVE 实例定制静态检测规则（source–sink + 污点传播路径），避免人工或 LLM 判定的主观性。

### 2.2 基准构建流程（四阶段）
1. **确定数据源**：从公开漏洞库与企业内部源收集 10 万+ 原始 CVE 条目，要求有可访问的 commit 历史。
2. **过滤候选仓库**：
   - 仅保留 2024 Top CWE 中与 Web 相关、且有可追溯修复 commit 的 CVE；
   - 要求仓库月活跃维护或 GitHub star > 1000；
   - 用 CodeQL + Joern 双工具链检测，并与修复 commit 修改行求交集，保留告警与修改行重叠的案例，得到 **199 个高置信候选**。
3. **专家引导的精炼与质量控制**：
   - 10 人专家团队（5 名博士生 + 5 名硕士生）人工复核，剔除误报与改动文件过多（>10）的 commit；
   - 精确标注漏洞区域、重建执行上下文（source/sink、API 定义、调用链），设计定制 CodeQL/Joern 查询验证污点路径；
   - 移除漏洞代码形成“填空式”任务，最终保留 **40 个种子仓库**。
4. **数据集扩展**：对 40 个种子仓库做**语义变换**（系统性重命名、等价 API 替换）与**结构变换**（控制流改写、调用图重构、文件布局重组），生成 **80 个变异变体**，合计 **120 个基准实例**。

### 2.3 评测流程与指标
- **两阶段流水线**：
  - **代码生成**：模型接收“被 `<masked>` 遮蔽的目标文件 + 漏洞功能描述 + 经 BM25 检索的仓库级上下文（README 及相关文件）”，输出 unified-diff 补丁；每个实例运行 3 次以评估稳定性。
  - **代码评估**：先做质量预检查（补丁能否应用、语法/静态检查是否通过），再做安全评估（定制规则下告警数是否下降）。
- **三项指标与加权公式**：
  - **Quality**：`Quality = (1/N) Σ q_t`，q_t=1 表示补丁成功合并并通过所有检查；
  - **Security**：`Security = (1/N) Σ s_t`，s_t=1 当且仅当补丁集成后告警数 `v_after(t) < v_before(t)`；
  - **Stability**：对每个实例 3 次运行的标准差 σ_i 做 min–max 归一化后取均值；
  - **Overall**：`Overall = 0.6 × Security + 0.3 × Quality + 0.1 × Stability`（安全占主导权重，防止被质量/稳定性抵消）。
- **工具链**：CodeQL 与 Joern 各覆盖 50% 实例，容器化封装以保证可复现性。

### 2.4 基准构成
- **漏洞类型**：SQL 注入 29.2%（CWE-89）、路径遍历 26.7%（CWE-22）、XSS 25.0%（CWE-79）、命令注入 19.2%（CWE-78）。
- **语言分布**：PHP 50.0%、Python 19.2%、Go 14.2%、JavaScript 14.2%、Java 2.5%。
- **漏洞代码规模**：平均 35.77 行，中位数 18 行，范围 [2–415]。

## 3. 实验设计

- **基准**：A.S.E 自身，共 120 个仓库级实例（40 原始 + 80 变异）。
- **评测模型**：共 **26 个**主流模型，含 18 个闭源与 8 个开源：
  - 闭源：Claude-3.7-Sonnet / Sonnet-4 / Opus-4 及其 thinking 版本、GPT-4o、GPT-4.1、Codex-mini、o3、o3-mini、o4-mini、Grok-3 / Grok-4 / Grok-3-mini、Gemini-2.5-Pro、Qwen-Coder-Plus、Hunyuan-T1；
  - 开源：Qwen3-235B-A22B-Instruct/Thinking、Qwen3-Coder、DeepSeek-V3、DeepSeek-R1、Kimi-K2、GLM-4.5 等。
- **对比维度**：
  - 快思考（fast-thinking）vs 慢思考（slow-thinking）推理范式；
  - 开源 vs 闭源模型；
  - 四类漏洞任务的表现差异；
  - 原始数据集 vs 变异数据集的分布一致性；
  - 架构（MoE vs Dense）与规模缩放（Qwen2.5-Coder 0.5B–32B、Qwen3 4B–235B）；
  - 稳定性与安全性的解耦分析。
- **定性分析**：对 SQL 注入任务 `sqli_mutation_181` 做案例研究，展示“合格且安全 / 合格但不安全 / 不合格”三类典型生成模式。

## 4. 资源与算力

- 论文仅说明实验环境为 **Ubuntu 系统、Intel CPU @ 2.50 GHz、16 线程、32 GB 内存**，统一上下文长度 64K tokens、最大输出 64K tokens。
- **未提及任何 GPU 型号、数量或训练时长**。需要指出：A.S.E 是**评测型基准**，不涉及模型训练，因此算力主要用于推理调用，论文也未报告推理总成本或 API 调用量。

## 5. 实验数量与充分性

- **实验规模**：26 个模型 × 120 个实例 × 3 次重复运行，覆盖四类漏洞、五种语言，并附完整排行榜（Table 2）。
- **分析维度充分**：
  - 主实验（整体排行榜）；
  - 四类漏洞细分表现（Figure 7）；
  - 快/慢思考对比（Figure 6）；
  - 原始 vs 变异数据集一致性（Figure 8）；
  - 架构与缩放分析（附录 E，Qwen 系列多规模对比）；
  - 稳定性–安全性解耦分析；
  - SQL 注入案例研究（附录 F）。
- **客观性与公平性**：
  - 所有模型使用**统一上下文（BM25 检索）、统一容器化环境、统一 64K 上下文与输出长度**，提示词一致；
  - 每个实例运行 3 次以控制随机性；
  - 评估规则为专家定制、一对一映射 CVE，结果可追溯；
  - 变异数据集用于检测记忆/泄漏，增强结论可信度。
- **总体评价**：实验设计较为充分且可复现；但覆盖范围限于 Web 领域、四类 CWE、五种语言，跨域泛化性尚未验证。

## 6. 主要结论与发现

- **质量–安全鸿沟显著**：多数模型能生成功能正确的代码，但**没有任何模型 Code Security 超过 50 分**。最佳模型 Claude-3.7-Sonnet 总分 63.01，安全分仅 46.72；Claude-Sonnet-4 质量最高（92.37）但安全仅 34.78。
- **仓库级复杂度暴露短板**：在 snippet 级基准（如 SafeGenBench）表现优异的 GPT-o3，在 A.S.E 上表现大幅下滑（安全 0.36、质量 0.36），说明仓库级跨文件推理是显著挑战。
- **慢思考不一定更安全**：Claude 系列中 thinking 模式在安全指标上普遍低于 fast 模式（如 Claude-3.7-Sonnet 63.01 → Thinking 61.04），作者提出三种可能机制：补丁更大更易引入新污点路径、推理链偏离仓库约束、训练目标偏重推理正确性而非安全性。
- **路径遍历（Path Traversal）最具挑战**：所有模型在该类任务上得分均低于 50，反映模型对文件系统操作与访问控制的推理薄弱。
- **数据泄漏风险低**：原始与变异数据集上模型表现差异极小，说明基准较稳健。
- **开源与闭源差距缩小**：Kimi-K2、Qwen3-235B-A22B-Instruct 等开源模型整体表现与闭源旗舰相当，稳定性甚至更优。
- **稳定性 ≠ 安全性**：GPT-o3 稳定性高达 98.91，但安全与质量近乎垫底，二者明显解耦。
- **架构与规模**：MoE 模型总体优于 Dense 模型；规模扩大通常提升安全表现，但存在平台期，架构改进（如 Qwen2.5→Qwen3）收益大于单纯扩参。

## 7. 优点

- **真实性与生态效度高**：数据源自真实 GitHub 仓库与 CVE 补丁，任务形式（diff 补丁、跨文件上下文、BM25 检索）高度贴近真实 AI 编程工作流。
- **评估自动化且可复现**：为每个 CVE 定制 source–sink 静态规则，避免人工/LLM 判定的主观性；容器化 CodeQL + Joern 双工具链保证跨平台一致性。
- **抗数据泄漏设计**：通过语义与结构变异生成 80 个变体，并实证原始/变异表现一致，增强结论可信度。
- **多维指标体系**：Security / Quality / Stability 三轴加权（60/30/10），权重设计有明确论证，防止“稳定但不安全”的模型靠低方差上位。
- **评测规模大且覆盖广**：26 个模型、快/慢思考对照、开源/闭源对照、多语言多 CWE，附完整排行榜与分析。
- **发现具有实践指导意义**：明确指出“功能正确不等于安全”“慢思考未必更安全”“需提供仓库级上下文”等可操作建议。
- **案例研究直观**：SQL 注入案例清晰展示三类失败模式（安全参数化、拼接仍不安全、diff 位置错位），揭示安全、语义正确、结构可应用三者需同时满足。

## 8. 不足与局限

- **覆盖范围有限**：仅限 Web 相关项目、四类 CWE（SQLi、路径遍历、XSS、命令注入）、五种语言（PHP 占一半），未覆盖移动端、嵌入式、区块链等领域，泛化性存疑。
- **仅静态分析**：无法动态验证功能正确性，也无法检测仅在运行时出现的漏洞（如并发问题、环境依赖缺陷）；作者承认这是为可复现性做出的权衡，动态验证（fuzzing、PoC 执行）留作未来工作。
- **规则依赖专家人工校准**：每个 CVE 的定制规则需安全专家手工设计，扩展成本高、难以快速适配新披露 CVE。
- **任务分布偏差**：语言分布严重偏向 PHP（50%），可能影响结论对其他语言生态的代表性；作者也指出慢思考劣势“可能不适用于其他漏洞域或提示策略”。
- **对真实工程多样性的模拟有限**：虽引入仓库上下文与 diff 集成，仍无法完全复现生产环境的复杂性与

不确定性（如遗留依赖、构建配置、运行时环境、团队约定与隐式规范）。补丁能否 `git apply` 只验证了文本层面的可集成性，并不等价于在真实 CI、测试套件与部署环境中可合并、可运行；仓库级上下文也主要由 README 与 BM25 检索文件构成，可能遗漏关键调用链、配置项或框架约定。

- **静态规则的覆盖性与偏差风险**：定制 CodeQL/Joern 规则虽提升可复现性，但仍可能漏报（false negative）或误报（false positive）；“告警数下降”作为安全代理指标，未必等价于漏洞被真正修复，也可能出现“转移污点路径”“抑制告警而非消除根因”等情况。论文以专家复核与双工具链降低该风险，但未系统报告规则本身的精确率/召回率。
- **变异设计的双刃效应**：语义与结构变异有助于抗记忆泄漏，但也可能改变漏洞可利用性、框架语义或业务约束；原始与变异集表现接近只能说明模型行为分布较稳定，不能完全排除变异引入的分布偏移。
- **任务形式偏“修复型”而非“从零生成型”**：以遮蔽漏洞代码、要求输出 diff 的方式贴近 AI 编程助手，但更偏向“给定上下文补全/修复”，对从需求到多文件新功能开发、重构、测试生成等场景的代表性有限。
- **检索与上下文策略较单一**：统一使用 BM25 检索仓库上下文，虽保证公平，但未比较 embedding 检索、调用图检索、Agent 多轮工具调用等更强上下文获取方式；因此结论更适用于“单轮、固定上下文”的评测设定。
- **模型与版本时效性**：26 个模型覆盖广，但闭源模型通过 API 调用，版本更新、系统提示与解码参数可能变化，长期复现性受影响；论文虽统一参数与容器环境，仍难以完全锁定服务端行为。
- **统计与显著性报告有限**：每实例 3 次运行可估计稳定性，但未充分展开置信区间、显著性检验或实例级难度分层；排行榜细微差距的稳健性仍需谨慎解读。
- **成本与伦理维度未量化**：未报告 API 调用成本、推理能耗与延迟；也未讨论 AI 生成代码漏洞的责任归属、企业采用时的审计流程与合规要求。

## 9. 实践启示与未来方向

- **对开发者与组织**：应把“功能正确”与“安全正确”分开验收；在 AI 编程助手工作流中引入仓库级静态分析门禁，对文件系统操作、SQL 拼接、命令执行等高风险 sink 做重点审查；不能因模型“会推理”就默认其更安全。
- **对模型提供方**：需在训练与对齐中显式优化“安全补丁”目标，而非仅优化代码通过率；应提升跨文件调用链理解、框架语义理解与最小化补丁能力，减少“修一个洞、引入另一个洞”。
- **对基准建设**：未来可扩展到更多 CWE、语言与领域（移动端、嵌入式、云原生配置等），引入动态验证（测试执行、fuzzing、PoC 复现）与多轮 Agent 工具调用评测；同时降低专家规则维护成本，探索半自动规则生成与规则质量评估。
- **对评估方法**：建议报告规则精确率/召回率、实例难度分层、置信区间与显著性检验，并公开更多失败案例，以区分“不会修”“修了但不安全”“补丁不可集成”等不同失败模式。

## 10. 总体评价

A.S.E 的主要贡献在于把 AI 代码安全评估从“片段级、主观判定”推进到“仓库级、补丁级、可复现静态验证”：真实 CVE 与开源仓库提供生态效度，定制 source–sink 规则提供自动化评估，变异集提供抗泄漏检验，三轴加权指标避免稳定性掩盖安全问题。其实验规模较大、对照维度丰富，所得“质量–安全鸿沟”“慢思考未必更安全”“路径遍历最难”等结论具有较强实践警示意义。

同时，该工作仍是**特定范围内的强基准**而非通用安全结论：Web 领域、四类 CWE、PHP 偏重的语言分布、静态分析代理指标与单轮固定上下文设定，决定了其外推需谨慎。总体而言，A.S.E 为“AI 生成代码是否安全”提供了一个较可信的测量起点，但距离覆盖真实软件工程全流程的安全保障仍有明显空间。

（完）
