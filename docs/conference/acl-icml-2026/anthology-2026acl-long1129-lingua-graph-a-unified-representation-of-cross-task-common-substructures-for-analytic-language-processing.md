---
title: "Lingua-Graph: A Unified Representation of Cross-Task Common Substructures for Analytic Language Processing"
title_zh: Lingua-Graph：跨任务公共子结构的统一表示用于分析式语言处理
authors: "Mingming Sun, Runze Jiang, Zhu Zhangchenxi, Minlong Peng, Yunfeng Cai"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://aclanthology.org/2026.acl-long.1129.pdf"
tags: ["query:ai-se"]
score: 6.0
evidence: 面向分析式自然语言处理的统一图表示
tldr: 自然语言的结构化理解需要显式恢复实体、事实与嵌套关系，但现有结构分析任务因数据集要求不一致而彼此割裂。作者提出分析式自然语言处理视角，将任务重构为表示后决策范式，并给出表示层方案Lingua-Graph，用带标签节点和边的显式图统一刻画实体、事实与关系。该表示提升了跨任务结构理解的稳健性，为统一NLP结构建模提供了可复用基础。
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1129/fig-001.webp\", \"caption\": \"\", \"page\": 6, \"index\": 1, \"width\": 4400, \"height\": 2232}]"
motivation: 结构分析类NLP任务因数据集要求不一致而碎片化，缺乏统一的结构理解表示。
method: 提出表示后决策范式，并用显式图结构Lingua-Graph统一编码实体、事实与关系。
result: 统一表示在跨任务结构理解上表现稳健，缓解了任务间不一致问题。
conclusion: 该工作为分析式NLP提供了可共享的结构表示层，推动统一语言理解建模。
---

## Abstract
Structural understanding of natural language requires explicit recovery of internal meaning structures (entities, facts, nested relations), yet current structural-analytic tasks are fragmented by inconsistent task requirements across datasets. We investigate the problem of robust cross-task structural understanding under heterogeneous requirements across structural-analytic tasks and outline a perspective called Analytic NLP in which tasks can be reformulated into a representation-then-decision paradigm. In this paper, we suggest a solution for the representation layer, called Lingua-Graph, which explicitly captures entities, facts, and relations. By representing predictions as explicit graphs with labeled nodes and edges, Lingua-Graph also improves interpretability, enabling transparent inspection and error analysis of intermediate meaning structures. We construct a labeled Lingua-Graph dataset and train a baseline parser. Experiments show that Lingua-Graph provides substantially higher entity-structure hostability than alternative representations on average, and OpenIE systems based on Lingua-Graph achieve superior performance on three benchmarks, demonstrating that better intermediate structures translate into downstream gains. The data, code and the trained model are publicly released at https://github.com/rudaoshi/Lingua .

---

## 论文详细总结（自动生成）

# Lingua-Graph 论文详细中文总结

## 1. 核心问题与研究动机

- **核心问题**：自然语言的结构化理解需要显式恢复实体、事实、嵌套关系等内部语义结构，但当前的结构分析类任务（实体识别/分类、共指消解、开放信息抽取、语义角色标注、关系抽取等）高度碎片化——每个场景都有自己的标签体系和数据集，各自训练任务专用模型。
- **背景痛点**：
  - 传统范式在固定设定下有效，但学到的结构绑定于特定标注规范，跨任务/跨领域迁移性差。
  - LLM 虽尝试用提示统一抽取，但难以协调不同数据集之间异构甚至冲突的标注惯例；实际系统常退化为数据集特定的指令微调，且对提示变体、分块/上下文选择敏感。
  - 因此，"异构需求下的鲁棒跨任务结构理解"仍是开放问题。
- **核心主张**：应恢复语言中潜在的**共享全局结构**，让不同任务对应同一底层表示中不同局部子结构的选择与标注。由此提出 **Analytic NLP（分析式自然语言处理）** 视角：先构建公共中间结构层，再把下游任务实现为该层上的决策（representation-then-decision 范式）。这一视角同时提升跨任务复用性与可解释性。

## 2. 方法论

### 2.1 Analytic NLP 形式化框架
- 任务被分解为两层：`x --fθ--> G --Dt--> ŷt`
  - **表示层 R**：解析器 `fθ: x → G` 将文本映射为结构化对象（图、树、超图等），并配备候选单元生成器 `ΓR(G) ⊆ 2^V(G)`，枚举可作为分析单元的可接受子结构。
  - **决策层 Dt**：`ŷt = Dt(ΓR(G), x)`，可为纯数据驱动、纯逻辑/优化，或概率关系推理。
- **任务诱导单元集** `Ut(x) ⊆ 2^I`（如 NER 的金标实体 token 集）。
- **表示诱导候选单元集** `UR(x) := { tokR(H) | H ∈ ΓR(G) }`，其中 `tokR` 把子结构映射回 token 索引。
- **两个核心评价指标**：
  - **表达性/神谕可恢复性**：`Exp(t; R, x) = |UR(x) ∩ Ut(x)| / |Ut(x)|`，衡量任务单元能被表示覆盖的比例。
  - **选择性/候选空间紧凑度**：`Sel(t; R, x) = |UR(x) ∩ Ut(x)| / |UR(x)|`，衡量候选单元中与金标任务单元对应的比例（类似精确率）。
- 强调"表示优先"协议：在归因决策模型成败之前，先检验表示能否承载任务诱导单元。

### 2.2 Lingua-Graph 表示
- 定义为单根有向无环图 `G = (V, E, τV, τE, α)`，节点/边带类型标签，并配有 token 划分映射 `α: V → 2^I`，节点 token 集构成输入索引集 `I` 的一个划分（互不重叠、覆盖完整）。
- **两个原始子结构构造器**：`SELF(v) = {v}`（单节点单元）与 `DESC(v)`（节点的有向后代闭包），据此定义子结构族 `ΓLG(G) = ∪v∈V {SELF(v), DESC(v)}`，文本域候选集 `ULG(x) = { tokLG(H) | H ∈ ΓLG(G) }`。
- **实现基础**：在 OIA-Graph 的谓词–函数–论元骨干上扩展，关键改进包括：
  - **分层架构**：每个节点连同其后代子图对应句中连贯的内部结构，契合语言的组合性与层次性。
  - **新结构**：引入 Expression（非修饰性组合关系，如 "48 to 49"、"Ca2+"）与 Attribute（⟨实体, 属性名, 值⟩ 三元组）。
  - **更细粒度单元**：把名词短语等分解为更细单元并显式建模其间关系（OIA-Graph 常把名词短语当作单节点）。
- **与其他语义表示的区别**：
  - 目标是"可复用任务诱导子结构的表示接口"，而非抽象/整体语义（AMR、UCCA）或表层句法（依存/成分句法）。
  - 强调**子图局部性**：局部子事实（如"we saw the film"排除 "yesterday"）在 Lingua-Graph 中是干净的祖先后代子图，而在 AMR/UCCA/OIA 中不易自然隔离。
  - 相比 AMR 更贴近表层可观察结构，便于 span 锚定、组合复用与错误诊断；相比 OIA 具有更强的层次化嵌套事实建模。

### 2.3 任务重构
- 大量任务可重构为在共享图容器内识别/分类（成对的）子图：
  - **实体检测**：每个节点标注 `SelfIsEntity` 与 `DescendantIsEntity` 两个布尔属性，天然支持嵌套实体。
  - **实体类型**：对应 `SelfType` / `DescendantType`，可为节点分类或开放域生成。
  - **语义角色标注**：以 FactualPredicator 节点为起点，识别论元节点并以带标签边（如 Agent/Theme/Instrument）编码角色，即边预测。
  - **关系抽取与共指**：均为链接预测；共指用专门的 `Ref` 边连接回指与先行词。
  - **开放信息抽取**：识别 FactualPredicator 节点及其论元节点构成完整事实三元组。

### 2.4 解析器学习流程
- **数据构建**：
  - **OIA-to-Lingua 流水线**：从标注好的 OIA-Graph 数据集出发，引入 Lingua-Graph 特有结构、分解复杂名词短语节点、强制层次化组织，再转换为 Lingua-Graph 格式。
  - **LLM 解析任务样本**：从多个结构分析数据集训练集采样句子，用 LLM 抽取语义关系，再经规则化转换系统转为 Lingua-Graph。
  - **主动学习 + 人工标注**：通过折外评估识别离群与低置信样本，由受训语言学学生人工审校，约 20% 样本经人工审计。
  - 最终规模约 **11K 训练 / 1K 开发 / 1K 测试**；100 样本双人标注，保守估计准确率约 84%，Cohen's kappa ≈ 0.63（实质性一致）。分歧主要来自修饰范围/层次挂接的歧义及部分 schema 元素（如 Expression）的规范解读差异。
- **解析模型**：先设计可无损互转的**词级 Lingua-Graph**（每节点对应一个词），再用 **BERT-based 双仿射关系解析器**（Dozat & Manning, 2017）预测词间关系；解码采用贪心搜索，增量加入高分边并施加 schema 与结构约束保证合法性，最后转回原始 Lingua-Graph。

## 3. 实验设计

- **表达性实验**：10 个数据集——ACE05、CoNLL03、GENIA、MultiNERD、OntoNotes、PolyglotNER、WikiANN，以及域外评估的 CrossNER、MIT-Restaurant、MIT-Movie。对比表示：**LLM 抽取基线、依存句法、成分句法、AMR、Lingua-Graph**（UCCA 因依赖过时未纳入）。指标为 `Exp(D)`，即金标实体 span 能被某节点或其祖先后代子图实现的比例。
- **选择性实验**：同样数据集与候选构造，对比依存、成分、AMR、Lingua（LLM 因不暴露候选集不参与），指标为 `Sel(D)`。
- **解析器评估**：在测试集上评估词级与恢复后 Lingua-Graph 的节点匹配（含标签与类型精确匹配）和边匹配（三元组 ⟨起始词, 边标签, 结束词⟩），节点词集采用"至少共享一词"的近似匹配。
- **下游 OpenIE 评估**：benchmark 为 **OIE2016、Re-OIE2016、BenchIE**，指标为 AUC 与 F1。对比方法包括 ClauseIE、OpenIE（Christensen 等）、BIO、SpanOIE、BiLSTM+BERT、Multi2OIE、OIE@OIA，以及本文的 **OIE@Lingua**（以 Lingua-Graph 替换 OIA-Graph 并适配规则决策层）。

## 4. 资源与算力

- **论文未明确说明** GPU 型号、数量、训练时长或总算力开销。
- 仅给出训练超参：BERT-base 为骨干，arc-bilinear 与 label-bilinear 嵌入维度分别为 512 和 256，训练 50 个 epoch，学习率 1×10⁻⁵，按验证集最优选择 checkpoint。
- 数据集构建中使用 LLM（附录 C 指明为 DeepSeek V3）做实体抽取基线。

## 5. 实验数量与充分性

- **实验组数概览**：
  - 表达性：10 数据集 × 5 种表示（含 LLM 基线）。
  - 选择性：10 数据集 × 4 种结构化表示。
  - 解析器性能：2 个层级（词级、恢复后）× 2 类指标（节点、边）。
  - 下游 OpenIE：3 个 benchmark × 8 个对比系统。
- **充分性评价**：
  - 覆盖面较广，包含域外数据集（CrossNER、MIT 两个）以检验泛化，指标设计（表达性 + 选择性互补）较为严谨。
  - 但**缺少消融实验**：未单独量化分层架构、Expression/Attribute 新结构、细粒度分解等各改进的贡献。
  - **决策层研究缺失**：论文明确将任务无关决策层留作未来工作，仅在 OpenIE 上用一个下游案例验证表示价值，任务覆盖有限。
  - 数据集规模中等（11K 训练），标注一致性 kappa 0.63 表明仍存在不可忽视的歧义，可能影响上限评估的客观性。
  - 表达性评估以**实体 span 作为代理**，虽作者论证实体是多数任务的锚点，但对 SRL、关系、共指等任务本身未直接做承载性评测。
  - 公平性方面：对比方法来自不同来源，部分基线（如 BIO/SpanOIE）在 BenchIE 上无结果（表中以 "–" 表示），横向比较存在一定不完整；UCCA 因工程原因缺席，作者已说明。

## 6. 主要结论与发现

- **表达性显著领先**：Lingua-Graph 平均表达性 **89.82**，高于成分句法 80.41、依存 76.08、AMR 73.29、LLM 基线 67.55；在 ACE05（92.99）、GENIA（89.65）、CoNLL03（95.74）等上优势明显，域外数据集也保持较强承载能力。
- **选择性未牺牲**：Lingua 平均选择性 **8.28**，与依存（7.77）、成分（7.27）相当，低于 AMR（9.80），说明其高表达性并非靠膨胀候选空间换取，而是更有效地组织了任务相关结构。
- **解析器可用**：词级节点 F1 96.1、边 F1 84.9；恢复后节点 F1 93.4、边 F1 82.9；多数错误归因于数据标注不一致。
- **下游收益可迁移**：OIE@Lingua 在三个 benchmark 上全面优于 OIE@OIA 及其他基线（如 Re-OIE2016 F1 87.4 vs. OIE@OIA 85.3；OIE2016 AUC 67.2 vs. 54.3），证明更好的中间结构能转化为下游性能提升。
- 约 10% 不可承载的 span 主要涉及当前监督未覆盖的复杂语言现象，预期可通过更多数据与更强学习/解码算法改善。

## 7. 优点

- **范式清晰**：将"表示–决策"分解形式化，并明确表示层应跨任务共享且可显式评估，提出表达性/选择性两个互补的神谕指标，方法论上有可操作性。
- **表示设计有针对性**：层次化 Modification 结构、Expression/Attribute 新结构、细粒度名词短语分解，使局部子事实对应干净的子图，直接服务于下游局部决策。
- **可解释性强**：预测结果为带标签节点和边的显式图，便于透明检查与中间结构错误分析。
- **实验设计较周全**：同时报告表达性与选择性，避免"靠候选爆炸刷覆盖率"的陷阱；引入多个域外数据集检验泛化

（接上文）

- **实验设计较周全**：同时报告表达性与选择性，避免“靠候选爆炸刷覆盖率”的陷阱；引入多个域外数据集检验泛化，并用下游 OpenIE 跨 benchmark 验证表示改进能否转化为实际收益。
- **任务重构具有统一性**：将 NER、实体类型、SRL、关系抽取、共指、OpenIE 等统一为共享图上的子图识别、节点分类或边预测，减少了“每个任务一套结构”的碎片化设计。
- **工程实现相对完整**：从数据构建、词级图转换、双仿射解析到约束解码形成闭环，并报告了节点/边匹配结果，便于后续复现与比较。
- **错误分析有指向性**：将解析错误较多归因于标注不一致与 schema 解读差异，而非单纯模型容量，为后续数据规范化和标注协议改进提供了方向。

## 8. 局限与潜在风险

- **表示层仍依赖特定 schema 与标注规范**：Lingua-Graph 虽试图成为跨任务共享容器，但其节点类型、Expression/Attribute、Modification 层次等设计仍带有较强先验；当目标任务的标注惯例与 schema 不一致时，表达性上限和决策层适配可能受影响。
- **神谕指标衡量的是“上限”而非端到端能力**：表达性和选择性均基于金标或解析图上的候选单元计算，不能直接等价于真实解析器条件下的任务性能；解析错误会通过候选集传播到下游。
- **任务覆盖与代理指标有限**：表达性实验主要以实体 span 为代理，尚未对 SRL、关系抽取、共指等任务逐一做承载性评估；因此“共享表示适用于广泛结构任务”的结论仍主要是原则性论证加 OpenIE 单点验证。
- **缺少系统性消融**：分层结构、Expression/Attribute、细粒度名词短语分解等设计各自贡献多少尚不明确；若某些结构对指标提升有限，可能增加 schema 复杂度与标注成本。
- **决策层研究尚未展开**：论文将任务无关决策层留作未来工作，当前主要证明“好表示”的价值，但表示与决策的联合优化、不同决策器（规则/优化/概率推理）的适用边界仍不清楚。
- **标注成本与一致性约束**：约 11K 训练样本、约 20% 人工审计、双人标注 kappa≈0.63，说明高质量图标注仍较昂贵且存在歧义；扩展到新领域/新语言时，规范维护和一致性控制可能成为瓶颈。
- **效率与可扩展性报告不足**：论文未明确给出推理延迟、吞吐、显存占用或大图解码复杂度；对于长文档、大规模部署和实时场景，图解析与候选枚举的成本仍需评估。
- **跨语言与跨领域稳健性仍有限**：域外数据集主要仍为英文实体相关场景，尚未系统验证多语言、低资源领域或高度专业文本上的表现。
- **基线公平性存在客观限制**：部分对比系统来自不同论文与实验设置，个别 benchmark 上存在缺失结果；UCCA 因工程原因缺席，LLM 基线也未参与选择性比较，横向结论需结合这些限制理解。

## 9. 对后续研究的启示

- **“先表示、后决策”可作为结构理解任务的通用实验协议**：在比较不同决策模型前，先报告任务单元在候选表示中的表达性与选择性，有助于区分“表示不足”与“决策器不足”。
- **共享中间结构需要配套候选单元接口**：仅有一个语义图还不够，必须定义可枚举、可锚定回文本的子结构族，否则下游任务难以复用。
- **局部子图隔离能力是表示设计的关键指标**：Lingua-Graph 强调局部事实对应干净的祖先后代子图，这提示未来表示学习应重视“局部可分离性”，而不仅是整体语义相似度。
- **数据规范与模型学习应协同设计**：标注歧义和 schema 解读差异是当前错误的重要来源，未来可引入更明确的标注指南、一致性校验和主动学习闭环。
- **下游验证应多任务化**：OpenIE 的成功只是初步证据，后续可在 SRL、关系抽取、共指、事件抽取等任务上检验同一表示的迁移收益，并研究任务特定决策器的组合方式。

## 10. 总体评价

总体而言，论文提出了一个清晰且可操作的 Analytic NLP 框架，并以 Lingua-Graph 作为共享结构表示的具体实现。其最大贡献不在于单一任务指标，而在于将“跨任务结构理解”转化为可度量的问题：表示是否承载任务单元、候选空间是否足够紧凑、解析器能否稳定恢复结构、以及更好的结构能否带来下游收益。实验在表达性、选择性和 OpenIE 下游验证上给出了较有说服力的证据，但也留下了消融不足、决策层未展开、任务覆盖偏窄和效率未报告等空间。作为一项面向统一结构理解的基础性工作，它为后续“共享表示 + 任务决策”的研究提供了有价值的范式与评测思路。

（完）
