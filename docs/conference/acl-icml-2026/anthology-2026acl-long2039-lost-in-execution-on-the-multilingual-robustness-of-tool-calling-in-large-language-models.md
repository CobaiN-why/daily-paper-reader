---
title: "Lost in Execution: On the Multilingual Robustness of Tool Calling in Large Language Models"
title_zh: 迷失于执行：大语言模型工具调用的多语言鲁棒性研究
authors: "Zheng Luo, T Pranav Kutralingam, Ogochukwu N. Okoani, Wanpeng Xu, Hua Wei, Xiyang Hu"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://aclanthology.org/2026.acl-long.2039.pdf"
tags: ["query:ai-se"]
score: 6.0
evidence: 大模型作为智能体调用外部工具的鲁棒性
tldr: 现有工具调用评测多在英语环境下进行，跨语言交互下的鲁棒性尚未被充分探索。作者提出MLCL诊断基准，系统评估中文、印地语及低资源伊博语中的多语言工具调用表现。细粒度错误分析表明，即便意图理解与工具选择正确，参数值语言不匹配仍是主要失败模式。该工作揭示了LLM智能体在多语言工具调用上的关键脆弱点，为后续改进提供依据。
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long2039/fig-001.webp\", \"caption\": \"\", \"page\": 5, \"index\": 1, \"width\": 262, \"height\": 734}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long2039/fig-002.webp\", \"caption\": \"\", \"page\": 5, \"index\": 2, \"width\": 374, \"height\": 496}]"
motivation: 现有工具调用评测偏重英语场景，多语言交互下大模型智能体调用工具的鲁棒性缺乏系统研究。
method: 构建MLCL诊断基准，覆盖中文、印地语与伊博语，并对多语言工具调用进行细粒度错误分析。
result: 实验发现大量失败发生在意图理解与工具选择正确之后，参数值语言不匹配成为主要失败模式。
conclusion: 多语言工具调用仍存在显著鲁棒性缺陷，需针对参数生成的语言一致性加以改进。
---

## Abstract
Large Language Models (LLMs) are increasingly deployed as agents that invoke external tools through structured function calls. While recent work reports strong tool-calling performance under standard English-centric evaluations, the robustness of tool calling under multilingual user interactions remains underexplored. In this work, we introduce MLCL, a diagnostic benchmark, and conduct a systematic evaluation of multilingual tool calling across Chinese, Hindi, and the low-resource language Igbo. Through fine-grained error analysis, we show that many failures occur despite correct intent understanding and tool selection. We identify parameter value language mismatch as a dominant failure mode, where models generate semantically appropriate parameter values in the user’s language, violating language-invariant execution conventions. We further evaluate several inference-time system strategies and find that while these strategies substantially reduce language-induced execution errors, none of them can fully recover English-level performance.

---

## 论文详细总结（自动生成）

# 《Lost in Execution: On the Multilingual Robustness of Tool Calling in Large Language Models》论文中文总结

## 1. 核心问题与研究动机

- **背景**：LLM 正从单纯的对话系统转变为能够通过结构化函数调用（tool calling）与外部 API 交互的智能体。已有工作（SFT、强化学习、BFCL 等基准）在**以英语为中心的标准化评测**下报告了很强的工具调用性能。
- **被忽视的缺口**：真实部署中用户会用多种语言提问，但工具执行接口（函数名、参数键、参数值的字符串形式）通常是**语言无关、实际为英语**的。现有基准几乎默认用户查询是英语，因此"语言变化 × 执行接口约定"这一交叉地带缺乏系统研究。
- **核心现象（论文命名的失败模式）**：**参数值语言不匹配（parameter value language mismatch）**——模型正确理解意图、正确选择函数，却把用户语言中的表达（如"纽约市""न्यू यॉर्क सिटी"）直接填入参数值，生成**语义上合理但不可执行**的调用。
- **整体含义**：多语言工具调用的性能下降**主要不是语义理解问题，而是"语言—执行边界"上的系统级/接口级问题**；这提示需要 execution-aware 的系统设计，而非仅提升语言理解能力。

## 2. 方法论

### 2.1 核心思想
构建一个**诊断性（diagnostic）**基准 MLCL，而非简单地把数据集翻译成多语言。设计目标是**把"查询语言变化导致的错误"与"执行接口约定导致的错误"分离开**，通过控制变量使任何性能下降都可归因于自然语言输入的变化，而工具 schema、API、评测标准保持完全固定。

### 2.2 基准的两个正交维度

| 维度 | 取值 | 含义 |
|---|---|---|
| 查询语言构成 | **NT**（Not Translated） | 原始英语查询，参考设置 |
| | **PAR**（Partially Translated） | 上下文翻译为目标语言，但 ground-truth 参数值保持英文（混合语言） |
| | **FT**（Fully Translated） | 整句查询完全翻译为目标语言 |
| 语义扰动 | **NO / PARA（改写）/ SYNO（同义词替换）** | 保持意图的表面形式变化 |

- 翻译与扰动由 **GPT-5** 生成，并由**掌握中文、印地语、伊博语的组员人工核验**；核验只要求**语义/意图等价**，不要求字面一致（例如 "queen-size bed" 允许译为语义等价的"大床"）。
- 执行接口全程保持英语、语言无关；函数名、参数键、工具描述**不翻译**。

### 2.3 错误分类体系（按严重程度排序）
1. **Syntax Error**：输出格式错误，无法解析。
2. **Function-Level Error**：函数名错误、缺参数等 schema 违规。
3. **Language Mismatch（本文重点）**，再按语义正确性细分：
   - *Wrong Value*：非英语且语义无关；
   - *Relevant but Incorrect*：非英语且相关但不精确；
   - *Exactly Same Meaning*：非英语但语义正确（仅语言不合规）。
4. **无语言不匹配的参数错误**：Wrong Value / Relevant but Incorrect / Exactly Same Meaning（英文但表面形式不同）。
5. **Other Error**。

评测沿用 **BFCL 协议**（函数名、参数键、参数值严格精确匹配），报告**总体错误率 + 结构化错误分解**，而非单一准确率。

### 2.4 推理期缓解策略（不改权重、可部署）
- **PT（Prompt-Level Instruction）**：完全翻译查询 + 在系统提示中显式要求"所有参数值用英文"（提示中插入 `IMPORTANT: Pass all parameter values in English.`）。
- **PRE（Pre-Translation）**：在调用工具前先把非英语查询翻译成英语，作为输入归一化的"上界"。
- **POST（Post-Translation）**：先生成工具调用，再把参数值翻译成英语后执行，直接针对参数值语言不匹配。
- 为控制翻译质量与模型能力的混淆，**翻译与工具调用使用同一个模型**。

## 3. 实验设计

- **基础数据集**：**BFCL V4** 的 `BFCL_v4_multiple.json` 子集（单轮查询 + 多个候选函数），选择理由是它具有严格的执行级 ground truth，且避免了多轮对话与真实执行等混淆因素。
- **语言**：英语（参考）、**中文**（高资源、表意文字）、**印地语**（高资源、形态丰富、语序灵活）、**伊博语 Igbo**（低资源、训练数据中代表性弱），覆盖类型学差异。
- **模型（15 个，跨 5 个家族/多规模）**：
  - GPT-5 / GPT-5 mini / GPT-5 nano；
  - DeepSeek V3.2；
  - Llama 3.1-8B / 70B Instruct；
  - Qwen3-8B / 14B / 30B-A3B / 32B / Next-80B-A3B-Instruct；
  - Granite 4.0-h-tiny / h-small。
  - 均使用官方推荐的 tool-calling 接口与解码配置；作者**自行实现**了各家族的 IO 协议转换与解析（未用 BFCL 官方实现）。
- **对比条件**：
  - 语言构成 NT / PAR / FT × 语义扰动 NO / PARA / SYNO 的交叉组合；
  - 三种缓解策略 PT / PRE / POST 与 NT、FT 基线的对比；
  - 附录中按模型家族做**规模与架构（稠密 vs MoE）分析**；
  - 翻译导致语义漂移的**案例研究**（"queen size bed" → "king-size bed"）。

## 4. 资源与算力

- **论文未报告任何具体算力信息**：没有 GPU 型号、数量、训练时长或推理 token 消耗的说明。
- 仅能从致谢推断：使用了 **Google 与 OpenAI 的 API credits**（用于 GPT-5 系列等闭源模型调用与数据生成），以及 **Arizona State University 的 Research Computing** 计算资源；受 NSF #2442477、#2550203 及 Amazon/Cisco/Toyota 教师研究奖资助。
- 由于本工作**不涉及训练/微调**，算力消耗主要来自推理评测与 GPT-5 数据生成，但具体规模无法从文中得知。

## 5. 实验数量与充分性

- **规模概览**：
  - 主实验：15 个模型 × 4 种语言 × 3 种语言构成（NT/PAR/FT）；
  - 语义扰动实验：5 个代表性模型（DeepSeek V3.2、GPT-5、Llama 3.1-70B、Qwen3-Next-80B、Granite 4.0-H-Small）× 3 种扰动 × 多设置，覆盖中文（图 5、13）与印地语（图 14）；
  - 缓解策略实验：PT / PRE / POST × 多模型 × 中文/印地语/伊博语；
  - 附录：4 个模型家族的规模/架构趋势分析（GPT-5 系列、Llama 3.1、Qwen3、Granite 4），每族含 FT/PAR/PT 三张图。
- **充分性评价**：
  - **优点**：模型覆盖面广（闭源+开源、稠密+MoE、8B–80B+），语言类型学跨度合理，控制变量设计清晰，错误分解比单一准确率信息量大得多；对"高资源 vs 低资源"的差异化结论有交叉验证（多模型趋势一致）。
  - **局限**：只有**单轮、无对话上下文**场景；扰动实验只做了 5 个代表模型（中文/印地语，伊博语未做扰动）；缓解策略是**刻意设计的简单探针**而非优化方法，未与任何训练式方案对比；没有人工评估下游任务成功率；翻译由 GPT-5 生成，可能引入系统性偏差；Llama 3.1-70B 只能输出整数导致 PAR 表现反低于 8B 的现象作者也承认"无法解释"，说明存在未控因素。
  - **公平性**：所有模型使用同一任务抽象、同一错误分类、同一严格匹配标准，且翻译与调用用同一模型以控制语言能力差异，整体比较是**客观且可复现**的（代码与数据已匿名开源）。

## 6. 主要结论与发现

1. **FT 显著抬高执行级错误**，且错误以**参数值语言不匹配**为主导；多数情况下这些参数值**语义仍然正确**，说明意图理解与工具选择已经成功，失败发生在语言—执行边界。
2. **错误构成随语言系统性变化**：参数值语言不匹配在**中文最常见，印地语次之，伊博语最少**——模型倾向于把高资源语言的 token 直接复用为参数值，而对低资源语言较少这样做；相应地，**伊博语的错误更多来自查询语义理解**（语义 grounding 不稳、自然语言到参数 schema 的映射不精确）。
3. **PAR 能有效隔离执行接口违规**：保留英文参数串、只翻译上下文后，GPT-5、Llama 3.1-70B 等模型的执行级错误明显低于 FT，**部分情况下追平甚至优于英语参考**。这说明一旦控制住接口违规，许多模型解读非英语查询的可靠性可与英语相当。
4. **语义扰动主要在"需要严格表面匹配"时才放大错误**：在 NT（英语）下 PARA/SYNO 显著增加执行失败（改写后不再匹配期望参数值）；在 FT 下影响有限（错误已被语言不匹配主导）；PAR 居中（扰动可能替换掉被保留的英文参数串，重新引入违规）。
5. **缓解策略能减少但不能消除差距**：PT 依从性不稳定；PRE 因能看到完整查询上下文而总体优于 POST；但**没有任何策略恢复到英语水平**，翻译引入**语义漂移与表面形式归一化**，把"语言不匹配"替换成新的执行级错误（案例：中文"大号床"回译成 "king-size bed" 导致 Relevant but Incorrect）。
6. **低资源语言上缓解策略收益有限甚至有害**：伊博语本身语言不匹配就少，PT/POST 几乎没有改进空间，剩余失败由**查询理解错误**主导。
7. **规模/架构效应不单调**：GPT-5 系列跨规模稳定；Llama 3.1 越大越好（语法错误更少、指令遵循更强、对英文参数约定有隐性意识）；Qwen3 的 **MoE 模型未随规模单调提升**（30B-A3B 不如 14B，Next-80B-A3B 相对 32B 增益有限），但在伊博语上 Next-80B-A3B 最好；Granite 4 呈**反向趋势**（大模型中文更差、伊博语更好），提示其工具调用行为与训练期约定耦合更紧、对指令式缓解不敏感。

## 7. 优点

- **诊断式而非"翻译式"的基准设计**：NT/PAR/FT × NO/PARA/SYNO 的正交分解，能干净地把"语言理解失败"与"执行接口违规"归因开，方法论上比单纯扩多语言数据更有解释力。
- **提出并命名了一个具体、可操作、此前被忽视的失败模式**（参数值语言不匹配），并用细粒度错误分类（按严重程度 + 按语义正确性二维细分）加以量化，这类错误在标准准确率指标下会被"总体错误率"掩盖。
- **PAR 作为"反事实探针"的巧妙使用**：通过只保留英文参数串来验证因果假设——若错误随之消失，则证明瓶颈在执行接口而非理解。
- **纳入低资源语言伊博语**，并给出与高资源语言**定性不同**的结论（理解瓶颈 vs 执行瓶颈），避免了"多语言=单一趋势"的过度概括。
- **模型覆盖广**（闭源/开源、稠密/MoE、8B–80B+），且多模型趋势一致，说明发现的是**共享机制**而非个别模型缺陷。
- **实践导向**：三种零训练、可部署的缓解策略给出了"能减多少、为什么减不干净"的明确答案；代码与数据开源。

## 8. 不足与局限

- **场景覆盖窄**：仅使用 BFCL 的 `BFCL_v4_multiple.json` **单轮**子集，未涉及多轮对话、有状态工具、真实执行反馈、并行/嵌套调用等更贴近部署的形态。
- **语言覆盖有限**：仅 3 种目标语言，无法覆盖所有语系与书写系统；作者自述目标是"识别系统模式"而非穷尽覆盖。
- **"英语为执行接口语言"是假设而非普遍事实**：结论依赖当前工具生态的常见设计；若接口本身支持本地化参数（如多语言地名库），失败模式与结论可能改变。论文分析的是"在该约定下的模型行为"，而非主张该约定合理。
- **严格精确匹配的代价**：BFCL 的 surface-form 精确匹配会惩罚良性变体（如 "NYC" vs "New York"），作者将其解释为"反映是否可无干预执行"，但这会**高估**实际可用性差距；同时 "Exactly Same Meaning" 类错误与真正不可执行的错误被混在同一指标下。
- **翻译质量与翻译伪影风险**：数据由 GPT-5 生成、人工核验只保证意图等价；PRE/POST 的翻译也由被测模型自身完成，可能与被测能力耦合（作者以此控混淆，但也意味着翻译误差无法独立评估）。
- **缓解策略过于简单**：PT/PRE/POST 是诊断探针而非优化方案，未与训练式方法（SFT、RL、接口层约束解码、参数值规范化后处理）对比，因此"无法恢复英语水平"的结论**只对这些简单策略成立**。
- **未评估下游影响**：没有测量错误调用在真实任务中的实际后果（静默失败率、用户可感知度），也没有人类评估。
- **存在未解释的异常**：Llama 3.1-70B 在 PAR 下反而略差于 8B，作者归因于其"只能输出整数"，但承认原因不明，提示评测框架或模型行为仍有未控变量。
- **无算力/成本报告**，可复现性在工程侧（15 个模型的 IO 协议自实现）依赖开源

……代码与数据，但未提供评测脚本的完整环境说明，复现仍需较大工程投入。

- **“语言不匹配”与“语义错误”的边界仍有模糊**：错误分类中 “Exactly Same Meaning” 被归入语言不匹配，但它与真正语义错误的可执行性差异很大；论文虽按严重程度排序，但在聚合指标里仍可能让读者高估“看似正确却失败”的比例。
- **未讨论安全/鲁棒性外溢**：参数值语言不匹配在真实系统中可能被恶意输入利用（如注入非英语字符串绕过校验），论文未涉及这一攻击面。

## 9. 启示与可拓展方向

- **对系统设计的启示**：工具调用层应引入**执行感知（execution-aware）的接口约束**，例如参数值规范化、语言白名单、schema 级类型/枚举校验、调用前参数值回译与一致性检查，而不是仅依赖模型“自觉”输出英文参数。
- **对评测的启示**：多语言工具调用基准应把**“理解正确性”与“执行合规性”分开报告**，并引入 PAR 这类反事实控制条件；单一准确率会掩盖本文揭示的核心失败模式。
- **对模型训练的启示**：可在 SFT/RL 阶段显式构造“非英语查询 + 英语参数值”的训练对，或加入参数值语言约束的奖励信号；但需注意低资源语言上瓶颈在理解而非执行，训练数据应差异化设计。
- **对后续研究的空间**：扩展到多轮、有状态、并行调用与真实执行反馈；覆盖更多语系与书写系统；将 PT/PRE/POST 与训练式方法、约束解码、后处理规范化做系统对比；引入人工评估与下游任务成功率；探究“接口语言本地化”场景下失败模式是否反转。

## 10. 总体评价

这是一篇**问题意识清晰、方法论克制且解释力强**的诊断性研究。其最大贡献不在于提出新模型或新训练方法，而在于**命名并量化了一个被英语中心评测掩盖的系统级失败模式**，并通过 NT/PAR/FT 的正交设计与细粒度错误分解，把“语言理解失败”与“执行接口违规”干净地分离开。PAR 作为反事实探针的使用尤为巧妙，使因果归因具有说服力。模型覆盖面广、多模型趋势一致，增强了结论的普适性。

其主要短板在于**场景与语言的覆盖有限、缓解策略过于简单、严格精确匹配可能高估实际差距、缺乏下游影响评估**，且部分异常（如 Llama 3.1-70B 在 PAR 下的反常表现）未获解释。但作为一篇“提出问题并给出诊断工具”的论文，这些局限更多是**边界声明**而非致命缺陷。总体而言，该工作对多语言智能体系统的工程实践与后续基准设计都具有明确的参考价值，尤其提醒社区：**多语言工具调用的瓶颈往往不在“听懂”，而在“说对接口的语言”**。

（完）
