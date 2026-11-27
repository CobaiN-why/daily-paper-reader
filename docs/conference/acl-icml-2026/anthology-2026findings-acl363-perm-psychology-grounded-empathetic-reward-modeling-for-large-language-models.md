---
title: "PERM: Psychology-grounded Empathetic Reward Modeling for Large Language Models"
title_zh: PERM：面向大模型的心理学驱动共情奖励建模
authors: "Chengbing Wang, Wuqiang Zheng, Yang Zhang, Fengbin Zhu, Junyi Cheng, Yi Xie, Wenjie Wang, Fuli Feng"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://aclanthology.org/2026.findings-acl.363.pdf"
tags: ["query:ai-se"]
score: 4.0
evidence: 面向大模型共情能力提升的奖励建模
tldr: 大模型在情感支持场景中常难给出实质回应，现有共情奖励模型仅从单一视角评估。PERM依据共情循环理论，从支持者与求助者双向分解共情评估维度，构建心理学驱动的奖励模型并用于强化学习。实验表明该方法能提升模型共情表达质量，为大模型人本应用提供更可靠的优化信号。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl363/fig-001.webp\", \"caption\": \"\", \"page\": 3, \"index\": 1, \"width\": 768, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl363/fig-002.webp\", \"caption\": \"\", \"page\": 3, \"index\": 2, \"width\": 768, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl363/fig-003.webp\", \"caption\": \"\", \"page\": 3, \"index\": 3, \"width\": 768, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl363/fig-004.webp\", \"caption\": \"\", \"page\": 3, \"index\": 4, \"width\": 768, \"height\": 512}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl363/fig-005.webp\", \"caption\": \"\", \"page\": 17, \"index\": 5, \"width\": 5737, \"height\": 1587}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl363/fig-006.webp\", \"caption\": \"\", \"page\": 18, \"index\": 6, \"width\": 1024, \"height\": 1024}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl363/fig-007.webp\", \"caption\": \"\", \"page\": 19, \"index\": 7, \"width\": 512, \"height\": 512}]"
motivation: 大模型在情感支持应用中常缺乏实质共情，现有奖励模型评估视角单一。
method: 依据共情循环理论从支持者与求助者双向分解共情维度，构建心理学驱动奖励模型用于强化学习。
result: 实验表明该奖励模型能有效提升大模型共情回应质量。
conclusion: 双向心理学奖励建模为大模型人本交互优化提供新思路。
---

## Abstract
Large Language Models (LLMs) are increasingly deployed in human-centric applications, yet they often fail to provide substantive emotional support. While Reinforcement Learning (RL) has been utilized to enhance empathy of LLMs, existing reward models typically evaluate empathy from a single perspective, overlooking the inherently bidirectional interaction nature of empathy between the supporter and seeker as defined by Empathy Cycle theory. To address this limitation, we propose Psychology-grounded Empathetic Reward Modeling (PERM). PERM operationalizes empathy evaluation through a bidirectional decomposition: 1) Supporter perspective, assessing internal resonation and communicative expression; 2) Seeker perspective, evaluating emotional reception. Additionally, it incorporates a bystander perspective to monitor overall interaction quality. Extensive experiments on a widely-used emotional intelligence benchmark and an industrial daily conversation dataset demonstrate that PERM outperforms state-of-the-art baselines by over 10%. Furthermore, a blinded user study reveals a 70% preference for our approach, highlighting its efficacy in generating more empathetic responses.

---

## 论文详细总结（自动生成）

# PERM：面向大语言模型的心理学驱动共情奖励建模 —— 论文结构化总结

## 1. 核心问题与研究动机

- **背景**：LLM 越来越多地部署于人本（human-centric）场景，用户在袒露心理脆弱或敏感信念时，期待获得实质性情感支持；但已有研究表明当前先进 LLM 的共情理解有限、回应策略不当（模板化、说教式、情感空洞）。
- **技术脉络**：早期用 SFT 提升共情，但依赖高质量示范、泛化差；随后转向 RL，通过奖励函数将共情操作化（用户反馈型或回应属性型），泛化性更好。
- **核心批评**：作者认为现有 RL 共情方法的**奖励建模只取单一视角**——要么只看支持者（LLM）的回应质量，要么只看求助者（用户）的反馈，忽略了心理学 **Empathy Cycle（共情循环，Barrett-Lennard, 1981）** 所强调的**双向闭环**本质：共情只有在"支持者共鸣并表达 → 求助者感知并回应"这一循环闭合时才成立。
- **后果**：单视角奖励导致两类失败模式——只建模 LLM 回应会产生通用、表层、客服式套话；只建模用户需求会产生"解决问题但情感冷漠"的回复（图 1 示例）。
- **论文主张**：将共情奖励建模重构为心理学驱动的多视角分解，提出 **PERM** 框架，并用于 RL 训练。

## 2. 方法论

### 2.1 理论基座：共情循环的三重分解
- **支持者视角（Supporter）**：
  - **Resonation（共鸣）**：是否正确理解求助者的内部心理状态，包括识别情绪、定位成因/情境触发、推断潜在心理需求（被认可、被安慰、被指导、自主性等）。
  - **Expression（表达）**：是否将这种理解以恰当方式传达，要求情绪对齐（如对方沮丧时表现温暖）、类人、流畅、有支持性语气；反例是"我懂你""我知道你的感受"这类公式化回应。
- **求助者视角（Seeker）**：**Reception（接收）**——模拟用户，判断回复是否满足其潜在需求、是否让其感到被支持/被理解/被打动，或仅是"安全但无感"。
- **旁观者视角（Bystander）**：不评估共情，而监控交互的**整体语言质量**（简洁、清晰、事实准确、无冗余重复与谄媚），用于防止模型以牺牲连贯性与信息量为代价"表演共情"。

### 2.2 奖励形式化流程
1. **两段式生成**：支持者 πθ 先对情境与用户情绪生成**分析** `y_a`，再生成**回复** `y_r`。
2. **三项共情打分**（均由 LLM-as-judge 按细粒度 rubric 打 1–5 分，再归一化到 [0,1]）：
   - `r_res = R_res(x, y_a)`：只评分析，奖励"内部推理"的正确性；
   - `r_exp = R_exp(x, y_r)`：评回复的表达质量；
   - `r_rec = R_rec(x, y_r)`：以用户视角评估回复被接收的效果。
3. **聚合方式**：采用**调和平均**
   `r_emp = 3 / (1/r_res + 1/r_exp + 1/r_rec)`
   设计意图是"任一维度短板会显著拉低总分"，逼迫模型在各维度均衡提升（对比实验中也试了 softmin 聚合，β=1）。
4. **旁观者惩罚项**：`r_bys = R_bys(x, y_r) − 1.0 ∈ [−1, 0]`，仅作惩罚，不作正奖励。
5. **总奖励**：`r = r_emp + λ_bys · r_bys`，主实验 λ_bys = 0.5。
6. **优化算法**：GRPO（Group Relative Policy Optimization）。
7. **附加长度惩罚**（附录）：`r_len = λ_len · max(|y_r| − l, 0)`，l = 768，λ_len = −0.001，防止输出过长。

## 3. 实验设计

### 3.1 数据与场景
- **训练数据**：基于 **EmpatheticDialogues**，随机抽取 4,981 条（覆盖 32 种基本情绪），用 GPT-4o 扩充场景描述并添加轻量用户 persona；实际训练用 3,000 条样本。
- **评测一：EQ-Bench3**（LLM 判官、复杂社会情境），7 个子维度 + Overall：Inner Resonation（DoI 洞察深度、ER 情绪推理）、Expression Style（DE 共情展示、WRM 温暖度、HL 类人性）、Interpersonal Competence（PEI 语用情商、SD 社交技巧）；子项 0–20 分，Overall 0–100。
- **评测二：工业日常对话 benchmark**：415 条真实需求型日常对话（含用户画像、交互历史），6 个 1–5 分指标：Empathy、Topic Guidance、Value Guidance、Intention Following、Fluency、Colloquial Expression。
- **评测三：真人盲测**：CloudResearch Connect 平台，68 名参与者，80 个场景，每人随机 5 例，比较 Empathy 与 Overall EI 两个维度。

### 3.2 对比基线
- **SFT 类**：SFT-Human（人类撰写回应监督）、SFT-GPT（GPT-4o-mini 回应蒸馏）。
- **RL 类**：RLVER（用户模拟器反馈奖励）、Partner（RoBERTa 回应属性奖励）、RM（通用奖励模型 Skywork-Reward-V2）、Rubric-ERL（评分准则奖励）。
- **参照**：Best-of-N（N=8，取多次采样的最高分）。

### 3.3 骨干与判官
- 主实验骨干：Qwen2.5-7B-Instruct；附录扩展到 Llama-3.1-8B-Instruct、Qwen3-4B-Instruct-2507。
- 判官：主实验 GPT-4o-mini；附录对比 Qwen3-4B-Instruct-2507。

## 4. 资源与算力

- 文中明确给出：**每轮训练使用 4 块 GPU，6 小时内完成，GPT API 成本低于 30 美元**。
- 工程栈：HuggingFace TRL + DeepSpeed + LoRA（降显存）+ vLLM（推理加速）。
- **未说明**：GPU 具体型号与显存、总实验轮次所消耗的总算力、是否使用 A100/H100 等；这些信息缺失，难以精确复现成本。

## 5. 实验数量与充分性评估

### 已开展的实验（约 8–9 组）
1. **主结果**（Table 1）：EQ-Bench3 全维度对比 8 个基线。
2. **消融**（Table 2）：逐一移除 Resonation / Expression / Reception / Bystander，以及 softmin 聚合替代调和平均。
3. **聚合与超参分析**（Table 7、图 4）：λ_bys ∈ {0.1, 0.5, 1.0} 的分数与训练曲线。
4. **数据增强消融**（Table 6）：增强数据 vs 原始 anchor 数据。
5. **日常对话实验**（图 3）：Base / RM / PERM 三方对比。
6. **用户研究**（Table 3）：PERM vs Base、PERM vs RM，两个数据集、两个维度。
7. **跨骨干验证**（Table 9）：Llama3、Qwen3 两个额外骨干。
8. **判官模型敏感性**（Table 8）：GPT-4o-mini vs Qwen3-4B。
9. **案例分析**（图 5、图 6）：EQ-Bench3 与 EmpatheticDialogues 各一例。

### 充分性与公平性判断
- **较充分之处**：覆盖"基准 + 工业数据 + 真人偏好"三层证据；消融覆盖每个奖励分量与聚合函数；跨骨干、跨判官模型验证了方法不依赖特定模型能力；提供了训练曲线与超参敏感性。
- **需谨慎之处**：
  - **RLVER 未在同一数据/设置下重训**（作者明言直接采用其发布模型），与其余基线的可比性不完全对等。
  - 训练仅 3,000 样本、单一英文数据集（EmpatheticDialogues），规模偏小。
  - 工业 benchmark 由公司合成且因匿名评审**未公开**（承诺接收后发布），第三方无法复现。
  - 用户研究 68 人、每人仅 5 例，胜率的 95% 置信区间达 ±9%–±10%，统计效力有限；且 ED 上 PERM vs RM 的 Empathy 恰为 50.0%±10.3%，即**在该项上未显著优于 RM**。
  - 判官为 GPT-4o-mini，而部分基线（如 Rubric-ERL）同样依赖 rubric/LLM 判官，存在"评测口径与训练口径相近"的潜在同源偏差，论文未做交叉判官（如人工评分）对 EQ-Bench3 结果的校验。

## 6. 主要结论与发现

- **主结果（Qwen2.5-7B）**：Overall EI 由 60.1 提升至 **66.6**（相对 +10.8%），优于最强基线 RM（62.3）与 Rubric-ERL（61.7）；DoI +15.0%、ER +12.9%、DE +13.5%、WRM +22.1%、HL +19.6%、PEI +17.5%、SD +13.0%，均超 10%。
- **SFT 泛化失败**：SFT-Human 全面崩塌（Overall 仅 38.2），SFT-GPT 仅小幅提升表达类维度——SFT 学到的是表层模式而非核心情绪能力。
- **单视角 RL 增益有限**：RLVER Overall 仅 +2.8%；Partner 只提升 WRM/HL，其他维度无改善——佐证"单视角不足"的核心论点。
- **消融结论**：Resonation 最关键（移除后 66.6→62.3）；Expression 主要影响 WRM/HL；Reception 影响所有维度；移除旁观者后 WRM 反升至 13.1 但 PEI 降至 12.5——说明旁观

者惩罚的作用是**抑制"表演式共情"**，而非直接提升温暖度——移除它反而使模型倾向于堆砌情绪词（WRM 上升），但语用得体性下降。
- **聚合函数**：以 softmin 替代调和平均后，总分略降，说明"短板惩罚"的软硬程度需要适中；调和平均在实验中表现更好。
- **旁观者权重**：λ_bys = 0.5 优于 0.1 与 1.0；权重过小时无法抑制冗余，过大时则压制共情表达（训练曲线在 λ_bys=1.0 时收敛更慢、方差更大）。
- **数据增强**：使用 GPT-4o 扩充的场景+persona 数据优于仅用原始 anchor 数据，说明情境信息越完整，模型对"内部心理状态"的推理越有依据。
- **日常对话场景**：在 415 条工业数据上，PERM 在 Empathy、Topic Guidance、Value Guidance 三项上明显优于 Base 与 RM，Intention Following 与 Fluency 持平或略优——表明共情提升未以牺牲任务完成度为代价（与"旁观者"设计意图一致）。
- **真人盲测**：在工业数据上 PERM 对 Base、对 RM 的胜率均显著高于 50%；但在 EmpatheticDialogues 场景中，PERM vs RM 的 Empathy 维度胜率为 50.0%±10.3%，即**未达统计显著**，仅在 Overall EI 上占优。作者对此的解释是 RM 在该数据集上已较强、且 ED 场景偏"短对话情绪回应"，单轮共情的区分度有限。
- **跨骨干**：Llama-3.1-8B 与 Qwen3-4B 上均取得一致方向的提升（Overall 分别 +4~6 分区间），说明方法不依赖特定基座；Qwen3-4B 因本身对齐更强，绝对增益略小。
- **判官敏感性**：换用 Qwen3-4B 作判官后，各方法的相对排序保持一致，PERM 仍居首，说明结论对判官模型选择具有一定鲁棒性。
- **案例分析**：EQ-Bench3 案例显示 PERM 的"分析"环节先定位了用户的**未言明需求**（如"希望被允许不坚强"），回复据此展开而非泛泛安慰；ED 案例显示基线 RM 给出"解决问题式"建议，PERM 则先做情绪确认再轻推行动。

## 7. 局限与未来工作

论文（含审稿视角）暴露的局限可归为四类：

1. **理论落地的不完全性**：Empathy Cycle 强调"求助者真实感知与回应"的闭环，但论文中的 Reception 仍是**LLM 模拟用户**打分，并未真正闭合循环（无真实用户的多轮反馈回路）。作者在结论中将"引入真实用户在线反馈 / 多轮交互中的动态共情"列为未来方向。
2. **判官依赖与偏差风险**：三项共情奖励全部由 LLM-as-judge 生成，存在判官偏好被"奖励黑客"利用的可能；虽做了跨判官验证，但缺少人工标注对奖励分数的校准（如判官分数与真人评分的相关性分析）。
3. **数据与场景规模**：训练仅 3,000 条、单一英文数据集、以单轮或短多轮为主；对长程咨询、危机干预（自伤/自杀风险）、跨文化共情等高风险或高差异场景未做验证，而这类场景恰恰对"错误共情"的代价最敏感。
4. **可复现性与成本披露**：工业 benchmark 未公开、GPU 型号未说明、RLVER 基线非同设置重训；此外调和平均在某一项接近 0 时会使总奖励剧烈塌缩，训练稳定性对判官分数分布较敏感（论文未给出该极端情形的分析）。

## 8. 学术价值与可借鉴之处

- **概念贡献**：把"共情"从"回应属性"重构为**多主体闭环中的多视角分解**，并用"旁观者"这一非共情视角约束"表演式共情"，是该文最具迁移价值的思想——可推广到任何"能力提升但易退化为风格表演"的对齐任务（如教学、劝导、客服）。
- **工程贡献**：给出了一套可直接复用的配方——两段式"先分析后回复"、细粒度 rubric 判官、调和平均聚合、惩罚型旁观者项、GRPO 训练，成本可控（<30 美元/轮）。
- **实证贡献**：SFT 全面崩塌、单视角 RL 增益有限这两组对照，为"共情需要结构化奖励"提供了较清晰的证据链；真人盲测与工业数据的加入提升了外部效度。

## 9. 总体评价

该文在动机（心理学理论驱动）与方法（多视角奖励分解）之间建立了较紧密的对应关系，实验矩阵覆盖基准、工业数据、真人偏好三个层次，消融与跨模型验证较为扎实，是一篇**问题定义清晰、方法可复用、结论方向可信**的工作。其主要短板在于：闭环中的"求助者"仍为模拟、判官同源偏差未充分排除、数据规模与场景多样性有限，且部分关键对比（RLVER）不完全对等、工业 benchmark 不可复现。因此更稳妥的表述是：PERM 在**单轮/短多轮的英文情感支持场景**下，相较单视角奖励方法具有稳定但幅度中等的优势；其在真实多轮、高风险与跨文化场景中的有效性仍待验证。

（完）
