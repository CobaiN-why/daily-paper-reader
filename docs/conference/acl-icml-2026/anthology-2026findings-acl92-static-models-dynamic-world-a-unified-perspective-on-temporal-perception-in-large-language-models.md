---
title: "Static Models, Dynamic World: A Unified Perspective on Temporal Perception in Large Language Models"
title_zh: 静态模型与动态世界：大模型时间感知的统一视角
authors: "Chenhao Li, Dandan Song, Changzhi Zhou, Jun Yang, Yuhang Tian, Huipeng Ma, Guangyuan Feng, Luan Zhang, Xudong Li, Ke Duan"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://aclanthology.org/2026.findings-acl.92.pdf"
tags: ["query:ai-se"]
score: 4.0
evidence: 大模型时间推理综述
tldr: 大模型在静态语料上训练却部署于动态世界，导致时间表达错位、时间线不一致和知识过时等系统性失败。本文以参数可达性为核心的信息论框架形式化时间查询，统一梳理大模型时间表示与推理研究。综述整合了时间知识图谱、检索增强、幻觉与知识编辑等碎片化工作，为理解与改进大模型时间感知提供整体视角。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl92/fig-001.webp\", \"caption\": \"\", \"page\": 3, \"index\": 1, \"width\": 2720, \"height\": 1568}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl92/fig-002.webp\", \"caption\": \"\", \"page\": 3, \"index\": 2, \"width\": 2580, \"height\": 1415}]"
motivation: 大模型训练语料静态而部署环境动态，导致系统性的时间感知失败。
method: 以参数可达性为基础的信息论框架形式化时间查询，统一梳理相关研究。
result: 综述整合了时间知识图谱、检索增强、幻觉与知识编辑等分散方向。
conclusion: 该统一视角为理解与改进大模型时间推理提供理论框架。
---

## Abstract
Large language models are trained on static corpora but deployed in a dynamic world, leading to systematic temporal failures—from mis-anchored expressions and inconsistent timelines to hallucinated future events, stale world knowledge, and related issues. Existing surveys on temporal knowledge graphs, retrieval-augmented generation, hallucination, and knowledge editing cover only isolated fragments of this space: they are typically task-centric and do not offer a holistic theoretical account of how frozen LLMs represent and reason about time. This survey provides a unified perspective on temporal reasoning in LLMs. We formalize temporal queries in an information-theoretic framework based on the parametric reachability of temporal premises and answers, which induces four temporal information regimes corresponding to internal reasoning, answer recency, premise anchoring, and genuine world indeterminacy. Under this lens, we delineate the landscape of temporal failure modes, consolidate methodologies for diagnosing temporal deficiencies, and synthesize mitigation approaches into a coherent design space. Together, these contributions provide a systematic roadmap toward reliable time-aware large language models.

---

## 论文详细总结（自动生成）

# 《Static Models, Dynamic World: A Unified Perspective on Temporal Perception in Large Language Models》中文结构化总结

> 说明：本文是一篇**综述（Survey）**，发表于 ACL 2026 Findings（pp. 1913–1932），作者来自北京理工大学计算机学院。因此第 3–5 点涉及“实验设计 / 算力 / 实验充分性”的部分需按综述类论文的性质来解读。

---

## 1. 核心问题与整体含义

### 1.1 研究动机
- **根本张力**：LLM 是把世界知识“静态压缩”进神经参数的一次性快照，却部署在一个本质上**动态**的世界中。时间并非可有可无的语言修饰，而是对话系统（跨轮次时间线追踪）、RAG（区分新鲜证据与过期报道）、自主智能体（时序规划、协调与因果推理）等能力的底层支撑。
- **由此产生的系统性时间失败**，作者归纳为四类：
  1. **解析与锚定错误**：叙事时间 vs. 报道时间混淆、上下文参照系漂移、干扰项诱发的伪锚点；
  2. **时序逻辑与常识失败**：区间关系（before/after、overlap/during）混乱、典型时长/前置条件被违反；
  3. **事实性与时效性失真**：知识过时、幻觉式“未来事件”、变体–不变量混淆（同一问题因参照时间/时区/历法变化而答案漂移）；
  4. **鲁棒性与不确定性缺失**：对“recently”等欠定表达强行单一解读并高置信输出，而非澄清或拒答。

### 1.2 与已有综述的差异（研究空白）
- 现有时序知识图谱/TKGQA 综述：假设结构化时间戳三元组，面向任务类型与解法范式；
- 时序信息抽取综述：面向抽取流水线（时间表达式识别/归一化、时序关系抽取）；
- 时序 IR/QA 综述：面向检索/QA 场景的目标、数据与评测协议；
- RAG 综述：把“时间”处理为知识新鲜度与外部证据更新问题；
- 知识编辑综述：聚焦事后更新过期事实。
- **共同缺陷**：均为 **task-centric（任务中心）**，缺少一个跨任务的、关于“冻结参数的 LLM 如何表征、锚定与推理时间”的**整体理论解释**。

### 1.3 整体含义与贡献
本文主张以 **LLM 时间能力本身**为第一研究对象，提出统一视角，贡献三条：
1. 一个**信息论框架**（基于前提与答案的参数可达性）划分四类时间信息情境；
2. 在该坐标系下绘制**失败模式全景图**；
3. 整合**诊断方法学**与**缓解方法设计空间**，形成通往可靠“时间感知 LLM”的路线图。

---

## 2. 方法论：核心思想与关键形式化

### 2.1 核心思想
用**“参数可达性”（parametric reachability）**这一信息论视角，把“模型答不对时间问题”拆解为两个可分离的来源：
- 模型是否**有能力重建时间前提**（解析、锚定、约束）；
- 模型参数中是否**存有该答案**（是否在训练截止前确定且被充分表征）。

二者组合即得到一个**与任务无关、与模型无关**的四象限坐标系，从而区分“知识缺失”“结构能力缺失”与“世界本身未定”。

### 2.2 关键定义
- **定义 2.1（时间原子查询）**：令 $X$ 为自然语言输入空间、$C$ 为上下文空间（参照时间、地区等），时间原子查询空间 $\mathcal{Q} := X \times C$。所谓“原子”指该查询只针对**单一不可再分的时间变量**（某个时间戳、时长或布尔状态），不可分解为独立子查询。对给定世界–时间结构 $M$，每个 $q$ 有语义解释：
  $$\big(H_{\text{time}}(q),\, a^*(q)\big)$$
  其中 $H_{\text{time}}(q)$ 为解释该查询所需的时间前提（相对表达的锚点、历法约定等），$a^*(q)$ 为真值答案。
- **定义 2.2（参数可达性）**：设模型 $f_\theta$、训练截止时间 $t_{\text{cut}}$，定义两个二值指示函数：
  - **前提可达性** $K_{\text{prem}}(q;\theta)=1$：$\theta$ 编码了足以重建 $H_{\text{time}}(q)$ 的知识，即存在正确解析时间锚点与约束的推理路径；
  - **答案可达性** $K_{\text{ans}}(q;\theta)=1$：$a^*(q)$ 在 $t_{\text{cut}}$ 之前已确定，且在预训练语料中被充分表征从而可被召回。

### 2.3 四类时间信息情境（核心分类）
由 $(K_{\text{prem}}, K_{\text{ans}})$ 的取值组合划分：

| 情境 | 名称 | 语义（应然） | 示例（Figure 1） |
|---|---|---|---|
| **Regime I** | Internal Frontier / 时间推理 | 前提与答案均可达：既有解析约束的结构能力，也有事实知识 | 一战 1914–1918 持续几年；阿波罗 11 号登月日期 |
| **Regime II** | Answer Frontier / 时效性（Recency） | **前提可重建**，但答案晚于训练截止或分布上缺席 | 2025-10-20 去卢浮宫该走哪个入口（10-19 失窃后当日闭馆）；截至 2025-12-07 英国首相是谁 |
| **Regime III** | Premise Frontier / 锚定（Anchoring） | **答案理论上已知**（如历史事实），但模型缺乏重建前提的内部表征 | 《Anora》在哪届奥斯卡获最佳影片 |
| **Regime IV** | World Frontier / 世界不确定性 | 前提与答案在查询时均未定或不可判定 | 2020 年元旦最后一位进入优胜美地国家公园的游客姓名；2032 年诺贝尔物理学奖得主 |

- 形式化表述：对固定 $\theta$，$\mathcal{Q}\approx R_{IF}(\theta)\,\dot\cup\,R_{AF}(\theta)\,\dot\cup\,R_{PF}(\theta)\,\dot\cup\,R_{WF}(\theta)$（理想化的不交并）。
- ⚠️ **原文的符号错位（需注意）**：正文中 Regime II 写作 $K_{\text{prem}}=0, K_{\text{ans}}=1$，但其文字解释是“模型能恢复前提、答案超出截止时间”；Regime III 写作 $K_{\text{prem}}=1, K_{\text{ans}}=0$，文字解释却是“答案已知、但无法重建前提”。按语义逻辑，二者取值应互换（Recency 应为 $K_{\text{prem}}=1, K_{\text{ans}}=0$；Anchoring 应为 $K_{\text{prem}}=0, K_{\text{ans}}=1$）。这属于原文表述不一致，阅读时需以文字语义为准。

### 2.4 重要的“非充分性”声明
- **参数可达性既非正确性的必要条件，也非充分条件**。正确的时间推理还依赖泛化、逻辑推理、上下文理解与指令遵循等综合能力；参数知识只是**有利条件**而非决定因素。正因如此，才有必要建立独立的失败模式分类学。

### 2.5 后续三节的展开逻辑（框架的“下游”）
- **§3 失败模式分类学**（四类失败，见下）；
- **§4 诊断方法学**（四族评测范式，见下）；
- **§5 缓解方法设计空间**（四族方法，见下）。

---

## 3. “实验设计”说明：本文为综述，无自建实验

- **本文不包含任何作者自建的实验、模型训练或人工评测**，其“证据基础”是对既有文献的系统性归纳与再组织（附录 Figure 3 给出三支柱全景分类图及代表性文献）。
- **所讨论的“Benchmark / 场景”即其梳理的评测资源**，主要在 §4 与附录 B（Table 1、Table 2）中系统列出，可视为本文的“评测蓝图”：

**（a）§4.1 锚点控制的对比测试（Anchor-Controlled Contrastive Testing）**
- 通用阅读理解源头：CNN/Daily Mail、NewsQA；
- 时序专项：**TORQUE**（叙事/问题重锚定下的事件顺序）、**TRACIE**（隐式事件远监督）、**TIMEDIAL**（对话时序常识）、**TRAVELER**（显式/隐式/模糊指称解耦）、**SPAN**（跨历法换算：公历/农历/伊斯兰历/日本和历）；
- 统一测试床：**TimeBench**、**TRAM**；时序敏感 RAG QA（**TS-RAG QA**，基于 30 万+ 新闻构建的 5.2K 问题）。

**（b）§4.2 基于约束的时序推理评测**
- 时序常识与语篇：**MC-TACO**（13K）、**TDDiscourse**（6.1K）；
- 诊断/合成：**Test of Time（ToT，1.8K）**、**TempReason（52.8K）**；
- 隐式约束与多跳：**TiQ（10K）**、**ComplexTempQA（1 亿级 QA）**；
- 结构化：**CronQuestions（410K）**、**Multi-granularity TKGQA（151K）**、**TKGQA Dataset（60K）**。

**（c）§4.3 版本敏感的知识评估**
- **TimeQA（41.2K）**、**SituatedQA（12.2K）**、**PAT-Questions（
