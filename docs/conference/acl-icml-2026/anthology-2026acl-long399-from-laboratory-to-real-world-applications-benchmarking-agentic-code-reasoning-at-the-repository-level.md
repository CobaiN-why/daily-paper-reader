---
title: "From Laboratory to Real-World Applications: Benchmarking Agentic Code Reasoning at the Repository Level"
title_zh: 从实验室到真实应用：在仓库级别对智能体代码推理进行基准测试
authors: "Jia Li, Yuxin Su, Michael R. Lyu"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://aclanthology.org/2026.acl-long.399.pdf"
tags: ["query:ai-se"]
score: 9.0
evidence: 面向仓库级智能体代码推理的基准
tldr: 现有代码基准多在孤立片段与黑箱评估之间摇摆，难以衡量智能体在真实仓库中的推理能力。作者提出RepoReason白盒诊断基准，以溯因断言验证为核心，并用执行驱动的变异框架防止记忆、借助动态程序切片构建细粒度诊断体系。实验表明该基准能更真实地揭示智能体在跨文件依赖中的逻辑一致性表现，为仓库级代码智能体评测提供了可复用的诊断工具。
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long399/fig-001.webp\", \"caption\": \"\", \"page\": 4, \"index\": 1, \"width\": 541, \"height\": 650}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long399/fig-002.webp\", \"caption\": \"\", \"page\": 4, \"index\": 2, \"width\": 478, \"height\": 650}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long399/fig-003.webp\", \"caption\": \"\", \"page\": 4, \"index\": 3, \"width\": 519, \"height\": 654}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long399/fig-004.webp\", \"caption\": \"\", \"page\": 4, \"index\": 4, \"width\": 524, \"height\": 653}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long399/fig-005.webp\", \"caption\": \"\", \"page\": 4, \"index\": 5, \"width\": 507, \"height\": 626}]"
motivation: 现有基准难以评估智能体在真实大型仓库中维持跨文件逻辑一致性的推理能力。
method: 提出RepoReason白盒诊断基准，采用执行驱动变异框架与动态程序切片构建细粒度评测。
result: 该基准可消除记忆捷径并更真实地刻画智能体在仓库级依赖中的推理表现。
conclusion: 为仓库级代码智能体的能力评估提供了可复用的白盒诊断方案。
---

## Abstract
As large language models (LLMs) evolve into autonomous agents, evaluating repository-level reasoning, the ability to maintain logical consistency across massive, real-world, interdependent file systems, has become critical. Current benchmarks typically fluctuate between isolated code snippets and black-box evaluations. We present RepoReason, a white-box diagnostic benchmark centered on abductive assertion verification. To eliminate memorization while preserving authentic logical depth, we implement an execution-driven mutation framework that utilizes the environment as a semantic oracle to regenerate ground-truth states. Furthermore, we establish a fine-grained diagnostic system using dynamic program slicing, quantifying reasoning via three orthogonal metrics: ESV (reading load), MCL (simulation depth), and DFI (integration width). Comprehensive evaluations of frontier models (e.g., Claude-4.5-Sonnet, DeepSeek-v3.1-Terminus) reveal a prevalent aggregation deficit, where integration width serves as the primary cognitive bottleneck. Our findings provide granular white-box insights for optimizing the next generation of agentic software engineering.

---

## 论文详细总结（自动生成）

## 一、核心问题与研究动机

- **背景转变**：软件工程正从“人类编码”转向“智能体自主开发”，LLM 作为自主软件智能体，核心能力要求已从“在孤立代码片段内做局部执行推理”升级为“在庞大、相互依赖的文件系统中维持逻辑一致性”，作者将其定义为**仓库级推理（Repository-Level Reasoning）**。
- **现有基准的两极分化**：
  - 一侧是函数级数据集（CRUXEval、REval 等），分析严谨但处于“实验室环境”，缺乏跨文件依赖与真实架构上下文；
  - 另一侧是 SWE-bench 等真实仓库评估，但属于**黑箱**：只判断问题是否解决，不解释失败原因，难以指导改进。
- **核心问题**：如何构建一个既能保留真实仓库复杂度、又能抵御数据污染、还能定位失败认知根源的**白盒诊断型**代码推理基准。
- **整体含义**：论文主张从“结果预测/代码生成”转向“**溯因断言验证**”（给定仓库执行历史，推断当前系统状态），从而把核心逻辑推理与表层语法噪声（格式、缩进、API 名称幻觉）解耦。

## 二、方法论：RepoReason 的五阶段流水线

### 2.1 核心思想
- 以**单元测试断言**作为“语义锚点”：断言是开发者意图的凝练检查点，天然要求模型回溯并重建前置执行历史。
- 采用**掩码-推理（Mask-and-Reason）**策略：把 `assert len(cache) == 5` 变为 `assert len(cache) == <mask>`，使任务成为溯因推理，无法通过阅读邻近赋值语句走捷径。
- 明确拒绝两种范式：I/O 预测（真实仓库输出状态体量大、噪声多、边界模糊）与原始轨迹查询（可被浅层静态分析短路，导致伪相关）。

### 2.2 五阶段流程

- **阶段 1：真实仓库精选**
  - 从 PyPI/GitHub 选成熟、活跃维护、以纯 Python 实现核心逻辑的项目，排除 NumPy/Pandas/PyTorch 等 C/C++/Cython 扩展（无法用 `sys.settrace` 做行级追踪）。
  - 文件级人工筛查，剔除三类低价值测试：平凡 API 校验、浅层计算模式、非确定性/外部依赖。

- **阶段 2：基于轨迹的结构过滤（保证逻辑深度）**
  - 用 `sys.settrace()` 采集完整调用序列（函数名、模块路径、行号、调用栈深度、参数、返回值等），入口为测试函数，`max_call_depth=3`。
  - 复杂度加权评分公式：
    `Score = (N_files/4)×0.1 + (N_funcs/15)×0.2 + (N_calls/30)×0.5 + (D/4)×0.2`
    其中调用次数权重 50%、栈深 20%、函数数 20%、跨文件数 10%；保留 Score ≥ 0.30（约 3 星）的用例，过滤约 13% 的琐碎测试。

- **阶段 3：执行驱动的变异引擎（EDME，反记忆化）**
  - 把运行环境当作“**语义预言机**”：保持调用图逻辑不变、扰动程序输入，切断模型的记忆检索路径。
  - 教师 LLM 一次性完成**视觉变异**（重命名变量、重构控制流、去注释）与**逻辑变异**（改常量、改输入参数），并严格保留原始 API 调用序列。
  - **探针注入**：把断言替换为 `print(f"DEBUG_RESULT: {expr}")`，真实执行后捕获运行时值作为真值。
  - **断言重建**：以捕获值为准、模仿原代码风格（`is` vs `==`、`FiniteSet(...)` vs `{...}`、`Rational(a,b)` vs 浮点）重建断言。
  - **严格验证门**：必须同时满足可执行性、断言有效性、API 序列保持，否则丢弃。

- **阶段 4：确定性值协议（DVP，保证可评估性）**
  - **语义确定性漏斗**：剔除表示漂移（内存地址）、外部扰动（时间戳、UUID、随机）、多解语义（`>`、`<`、`!=`、近似比较）。
  - **形态确定性漏斗**：答案白名单优先级为 字面量 > 全局常量 > 稳定属性访问 > 参数可解析构造器 >（SymPy 特例）符号表达式；拒绝纯变量引用与动态函数调用。
  - 若答案是变量名，触发受限的 **LLM 变量解析器**展开为字面量，并再次通过双漏斗校验。

- **阶段 5：认知诊断框架**
  - 以断言为根做**动态程序切片**，沿数据/控制依赖回溯，得到最小因果计算子图。
  - 三个正交指标：
    - **ESV（Effective Sliced Volume，阅读负载）**：切片内相关函数的去重代码行数，刻画语义上下文恢复成本；
    - **MCL（Mutation Chain Length，模拟深度）**：切片内相关语句按执行频次加权的动态状态更新步数；
    - **DFI（Dependency Fan-in，集成宽度）**：切片内被读取但未被重新赋值的独立上游变量数（过滤关键字、导入等结构噪声）。

## 三、实验设计

- **Benchmark 构成**：7 个 Python 仓库，规模 1.2k–776k LoC，总样本 **N = 2492**：
  - cachetools（1.2k LoC / 88 测试）、yarl（2.3k / 369）、toolz（3.7k / 92）、attrs（6.3k / 209）、jinja2（14k / 527）、networkx（67k+ / 534）、sympy（776k / 913）。
- **难度分层**：Easy（N=1009）/ Medium（N=838）/ Hard（N=645），由独立 LLM（GPT-5.2）按结构化提示标注，与被测模型无关。
- **评估框架**：OpenHands 0.60.0，统一配置 **ReadOnlyAgent**（只读探索 + 检索，禁止修改仓库），以隔离“读—导航—推理”能力与“编辑/规划”能力。
- **对比模型（5 个前沿模型）**：Claude-Sonnet-4.5、GPT-5.2、DeepSeek-v3.1-Terminus、Kimi-K2、Qwen3-Coder-480B-A35B。
- **推理配置**：temperature=0、max_tokens=8192；沙箱 1800 秒超时；答案比对采用数学等价（SymPy 化简）、结构归一化（包装剥离、集合对齐）与启发式语义匹配（构造器感知、路径限定、引号不敏感）。
- **分析维度**：按仓库、按难度、按三认知指标分桶的准确率曲线、Pearson 相关、偏相关分析、2 个高 DFI 失败案例、消融、温度稳健性、轨迹深度影响。

## 四、资源与算力

- 论文**未报告任何训练算力**（GPU 型号、数量、训练时长），因为该工作属于基准构建与推理评估，不涉及模型训练。
- 文中仅给出推理/构造成本相关配置：
  - 评估端：OpenHands 0.60.0 + ReadOnlyAgent，temperature=0，max_tokens=8192，单任务沙箱超时 1800 秒，增量 checkpoint。
  - 变异引擎端：教师模型 gpt-5.2，temperature=0.7，max_tokens=16384，单次变异最多重试 3 次，单次执行超时 180 秒。
  - 追踪配置：`max_trace_size=1000`、`max_call_depth=3`。
- 结论：**算力细节缺失，无法据此评估构建成本或复现的硬件门槛**。

## 五、实验数量与充分性

- **主要实验组**：
  1. 5 模型 × 7 仓库的总体准确率（1 组主表）+ 3 难度分层准确率；
  2. 三认知指标分桶性能曲线（ESV 6 桶、MCL 5 桶、DFI 5 桶）与 Pearson 相关（5 模型 × 3 指标）；
  3. 偏相关分析（控制另两指标，N=2492）；
  4. 2 组消融：EDME 有无（73.15% → 60.96%，成对记忆率 10.71%）、结构过滤前后复杂度变化（ESV +20.1%、MCL +10.1%、DFI +38.3%）；
  5. 稳健性：Claude-Sonnet-4.5 在 T=0 与 T=1.0 下的仓库级对比（总体 +1.00pp）及相关性稳定性；
  6. 轨迹深度消融（depth=3 vs ∞，整体膨胀 6.2×）；
  7. 2 个高 DFI 失败案例的机制分析。
- **充分性评价**：
  - 优点：主实验 + 消融 + 统计检验 + 案例研究形成“统计—机制”互证，偏相关有效分离了三个指标，稳健性检验覆盖了温度与轨迹深度，设计较为完整。
  - 局限：每模型仅单次贪心解码的 Pass@1，无多 seed 方差报告；难度标注依赖单一 LLM，缺乏人工一致性校验；仅 Python 单语言；仓库仅 7 个且 attrs 样本量偏小（58）；未与 SWE-bench 等在同一智能体上做交叉对照。
  - 公平性：统一框架、统一提示模板、统一 ReadOnlyAgent、temperature=0，比较条件基本对齐；但不同模型 API 的上下文窗口、工具调用能力差异未被显式控制。

## 六、主要结论与发现

- **总体性能**：Claude-Sonnet-4.5 最高（66.98%），其后为 DeepSeek-v3.1-Terminus（60.96%）、GPT-5.2（56.86%）、Kimi-K2（54.74%）、Qwen3-Coder（50.56%）；Hard 档骤降至 30.85%–47.39%，说明高熵逻辑仍是普遍短板。
- **仓库差异三类**：
  - 显式算法模式（cachetools、toolz）表现稳定（78%–82%）；
  - 隐式元编程（attrs、jinja2）分化严重（Claude 72.41% vs Kimi 43.10%），反映对 Python 动态对象模型的内化差异；
  - 高熵符号/结构推理（sympy、networkx）是当前推理天花板（sympy 仅 36%–51%）。
- **聚合缺陷（Aggregation Deficit）**：DFI 是**首要认知瓶颈**——DFI > 20 时多数模型跌破 40%；Pearson 相关最强（GPT-5.2 达 −0.234）；控制 ESV/MCL 后偏相关仍显著（r = −0.127, p < 10⁻⁹），而 ESV、MCL 的偏相关不再显著。
- **ESV 悬崖效应**：因果相关代码量超过约 600 LoC 后准确率骤降，标志进入上下文过载。
- **MCL 一致性衰减**：超过约 100 个执行步后状态追踪显著失稳。
- **失败机制**：呈现“**部分整合后断裂**”模式——智能体正确处理前几层信息，却随独立来源增多系统性丢弃最终约束（如 jinja2 忽略 groupby 的隐式排序，networkx 忽略 `cutoff=2`）。
- **模型画像差异**：DeepSeek-v3.1 对高 DFI 最稳健（−0.157），Claude 擅长深模拟但对多源整合脆弱（−0.225），Qwen3-Coder 抗上下文体积最好（ESV −0.148），GPT-5.2 全局最脆弱。
- **消融结论

- **消融结论**：
  - **EDME 是基准有效性的关键支柱**：移除执行驱动变异后，模型准确率从 73.15% 降至 60.96%，同时“成对记忆率”升至 10.71%，直接证明未变异样本中存在可被参数记忆检索短路的捷径，也说明“掩码 + 运行时真值”组合确实把任务从记忆复述拉回到执行语义推理。
  - **结构过滤提升的是“推理密度”而非“题目数量”**：过滤后 ESV +20.1%、MCL +10.1%、DFI +38.3%，三项指标同向上升且 DFI 增幅最大，表明该过滤器精准剔除了“调用多但依赖扁平”的伪复杂用例，使基准的难度来源从“代码体量”转向“跨源整合”。
  - **轨迹深度设定合理**：`max_call_depth=3` 相对无界追踪仅带来 6.2× 的体积膨胀控制，说明深度截断在保留因果链主干的同时显著降低了追踪与切片成本，是精度—成本之间的可接受折中。
  - **温度稳健性良好**：Claude-Sonnet-4.5 在 T=0 与 T=1.0 下总体仅差 +1.00pp，且指标—准确率的相关结构保持稳定，说明结论并非贪心解码的偶然产物，基准对不同采样策略具有一定不变性。

## 七、讨论与启示

- **对智能体能力建设的启示**：论文把“仓库级推理”拆解为可测量的三个正交维度（读多少、模拟多深、整合多宽），其价值在于把“模型不行”这一笼统判断转化为可归因的诊断。DFI 的主导性意味着，当前智能体的主要短板不是“看不懂单条语句”，而是**在多条独立信息源汇合处维持约束不丢失**；这对上下文管理、显式依赖记账、约束清单式中间表示等智能体架构设计具有直接指向性。
- **对基准设计方法论的贡献**：
  - **“环境即预言机”**：以真实执行结果而非人工标注作为真值来源，既保证语义正确性，又天然规避了标注者的直觉偏差；
  - **“掩码—溯因”任务形式**：把断言验证转化为“由果推因”，在保留真实仓库复杂度的同时切断浅层静态分析捷径，是对 SWE-bench 式黑箱评估与函数级白盒数据集之间空白的实质性填补；
  - **“确定性双漏斗”**：语义确定性 + 形态确定性的两级筛选，是自动化构建可机器比对答案时较少被系统化处理、却对基准可信度至关重要的工程环节。
- **与既有基准的关系**：RepoReason 并不替代 SWE-bench 类端到端任务，而是提供其“上游诊断层”——SWE-bench 回答“能否修好”，RepoReason 回答“在哪一类认知负荷上先断裂”。二者结合可形成“诊断—干预—验证”的闭环，这也是论文定位为“白盒诊断型基准”的合理依据。

## 八、局限与未来工作

- **覆盖范围**：仅覆盖 Python 单语言，且因依赖 `sys.settrace` 行级追踪而系统性排除了 C/Cython 扩展主导的仓库，使得科学计算、高性能库等真实工程中占比很大的场景未被纳入；7 个仓库虽在规模上跨越三个数量级，但生态多样性仍有限。
- **统计效力**：每模型仅单次贪心解码的 Pass@1，缺少多 seed 方差与置信区间，模型间几个百分点的差距（如 GPT-5.2 与 Kimi-K2 相差约 2pp）是否显著难以判定；难度分层由单一 LLM 标注且未报告人工一致性（如 Cohen's κ），分层结论的稳健性有待加强。
- **公平性控制**：虽统一了 OpenHands 框架、提示模板与 ReadOnlyAgent，但各模型的上下文窗口、工具调用格式兼容性、tokenizer 差异未被显式建模，可能对长上下文仓库（sympy）的结果产生混杂影响。
- **指标效度**：ESV/MCL/DFI 均为静态切片上的结构代理量，与真实认知负荷之间是相关性而非因果映射；偏相关虽分离出 DFI 的独立效应，但仍属观察性证据，缺乏干预式验证（如人为构造仅 DFI 变化的对照样本）。
- **可能的延伸方向**：多语言与含编译扩展的仓库、引入人工校验的难度标注、增加 seed 方差与跨基准对照、以及在诊断结论基础上做“干预实验”（如为智能体注入依赖清单）以验证因果性。

## 九、总体评价

- **贡献层次**：论文的贡献不止于“又一个基准”，而是提出了一套可复用的构建范式——真实仓库精选 → 轨迹驱动的复杂度过滤 → 执行驱动的反记忆变异 → 确定性答案协议 → 切片式认知诊断。其中 EDME 与 DVP 两个环节具有较强的方法迁移价值。
- **证据强度**：主实验、两组消融、偏相关分析与失败案例形成了“统计相关—机制解释”的互证链条，尤其是“聚合缺陷”这一发现与“部分整合后断裂”的失败模式在定性案例上相互印证，结论可信度较高。
- **主要不足**：算力与构建成本信息缺失，影响可复现性与成本评估；单次解码、单标注者、单语言三项限制削弱了结论的外推性；指标为结构代理，尚未完成因果闭环。
- **定位判断**：作为**诊断型**基准，RepoReason 在“可解释的失败归因”这一维度上确实填补了现有真实仓库评估的空白，其“聚合缺陷”结论对当前智能体能力边界给出了有价值的刻画；但作为**排行型**基准，其统计严谨性与覆盖面尚不足以支撑细粒度的模型优劣排序。二者应区别对待——这也是阅读和使用该基准时最需要注意的一点。

（完）
