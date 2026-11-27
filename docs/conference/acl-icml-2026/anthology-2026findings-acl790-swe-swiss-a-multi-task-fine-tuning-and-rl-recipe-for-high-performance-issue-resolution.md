---
title: "SWE-Swiss: A Multi-Task Fine-Tuning and RL Recipe for High-Performance Issue Resolution"
title_zh: SWE-Swiss：面向高性能问题修复的多任务微调与强化学习方案
authors: "Zhenyu He, Qingping Yang, Wei Shen, Xiaojian Zhong, Kechi Zhang, Chenxin An, Wenlei Shi, Tianle Cai, Di He, Jiaze Chen, Jingjing Xu"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://aclanthology.org/2026.findings-acl.790.pdf"
tags: ["query:ai-se"]
score: 9.0
evidence: 面向问题修复与单元测试生成的LLM多任务微调与强化学习
tldr: 针对大模型在SWE-bench等真实问题修复上能力不足的问题，SWE-Swiss提出两阶段训练方案：先将问题修复分解为定位、修复与单元测试生成三项技能并进行多任务监督微调，再用测试执行反馈做强化学习强化代码修复。实验表明所得32B模型在问题解决基准上取得领先表现，为自动化软件工程提供可复用训练配方。
source: ACL-2026-Findings
selection_source: conference_retrieval
motivation: 大模型在真实代码仓库问题修复上仍面临显著挑战，缺乏系统化训练方案。
method: 先多任务监督微调构建定位、修复、测试生成三项技能，再用测试执行反馈强化学习提升修复能力。
result: 训练出的SWE-Swiss-32B在SWE-bench类问题解决基准上取得领先性能。
conclusion: 分阶段多任务微调加强化学习是提升LLM自动修复能力的有效通用配方。
---

## Abstract
Automated software engineering, particularly resolving real-world issues on benchmarks like SWE-bench, remains a significant challenge for Large Language Models (LLMs). To address this, we introduce SWE-Swiss, a two-phase training recipe that systematically develops these capabilities. Our approach first decomposes issue resolution into three core skills: Localization, Repair, and Unit Test Generation. In the first phase, we perform multi-task Supervised Fine-Tuning (SFT) on three new, meticulously curated datasets to build a versatile foundation. The second phase applies targeted Reinforcement Learning (RL), using direct feedback from test execution to boost the critical skill of code repair. The resulting model, SWE-Swiss-32B, establishes a new state-of-the-art for open-source models in its size class, achieving a 60.2% score on the SWE-bench Verified benchmark and placing it in the same top-tier performance bracket as much larger models. Finally, we show that despite its specialized training, SWE-Swiss-32B demonstrates strong generalization to other common LLM benchmarks. To accelerate research in the community, we are open-sourcing the models and our complete training datasets.

---

## 论文详细总结（自动生成）

# SWE-Swiss 论文结构化总结

## 1. 核心问题与研究动机

- **背景**：大语言模型（LLM）在自动化软件工程（SWE）方向进展迅速，代表性评测为 SWE-bench 及其人工核验子集 SWE-bench Verified（500 个真实 GitHub issue）。
- **核心问题**：顶尖专有模型与开源模型之间存在明显性能鸿沟；DeepSeek-R1 等少数开源权重模型虽能接近专有模型水平，但其“训练配方”（SFT/RL 数据组成、训练技巧与超参）不透明，阻碍了可复现研究与社区进步。
- **方法论层面的追问**：Agentless 等工作已证明“定位→修复→验证”的结构化工作流有效，但**如何训练模型在每一阶段都足够强**尚缺乏系统答案。
- **论文定位**：提出 SWE-Swiss——一套面向“问题修复”的可复现两阶段训练配方（多任务 SFT + 强化学习），并开源模型与全部训练数据。

## 2. 方法论

### 2.1 核心思想：三技能课程分解
将复杂的问题修复任务分解为三项可分别训练、彼此协同的核心技能：
- **Localization（定位）**：找出需要修改的文件；
- **Repair（修复）**：生成正确的代码补丁；
- **Unit Test Generation（单元测试生成）**：生成可验证修复的新测试。

三项技能在整体补丁生成与验证流程中协同工作（对应论文图 3）。

### 2.2 数据构建：基于执行验证的拒绝采样
- **总体流程**：用强生成器（DeepSeek-R1-0528）为每项技能生成大量候选，再用真实执行环境（测试套件/Docker）作为 oracle 严格过滤，只保留可验证成功的样本（对应论文图 2 的三条并行流水线）。
- **Localization 数据**：来源为 SWE-bench 与 SWE-Gym-Raw；排除与 SWE-bench 测试集仓库重叠的实例以防污染。接受标准为：预测文件数 ≤ 5 且召回率 = 1.0。最终得到 **5,302** 条高质量样本。
- **Repair 数据**：来源为 SWE-gym 与 SWE-smith 的 12,097 个 issue（得到 12,087 条 prompt）；提示中给出 issue、oracle 文件及“干扰文件”（distractor files）。接受标准为补丁必须通过 Docker 环境中的单元测试。最终得到 **3,935** 条成功样本。
- **Unit Test Generation 数据**：同样基于 12,097 个 issue 生成测试；接受标准为生成测试的行为须与真实测试一致——对已知正确补丁通过、对已知错误补丁失败。最终得到 **1,017** 条验证样本。
- 三者合计 **10,254** 条样本，构成多任务 SFT 课程。

### 2.3 两阶段训练策略

**第一阶段：多任务监督微调（SFT）**
- 基座为 **Qwen2.5-32B-Instruct**，混合三类数据做多任务 SFT，将三项技能内化到单一模型中。
- 仅 SFT 阶段在 SWE-bench Verified 上（无测试时扩展）即达 **36.0%**，称为 SWE-Swiss-SFT。

**第二阶段：基于可验证奖励的强化学习（RL）**
- 聚焦最关键技能 **Repair**：模型自行生成补丁，立即在仓库真实测试套件上评估，奖励为直接二元信号：
  - \(R_{repair} = 1\)（补丁通过单元测试），否则 \(R_{repair} = -1\)。
- 算法采用 **GRPO**，并吸收 **DAPO** 的若干技巧：无 KL 损失、clip higher、动态采样、token 级策略梯度损失。目标函数为带非对称裁剪的 PPO 式目标：
  \[
  J_{DAPO}(\theta)=\mathbb{E}\left[\frac{1}{\sum_i|o_i|}\sum_{i}\sum_{t}\min\left(r_{i,t}(\theta)\hat A_{i,t},\ \mathrm{clip}(r_{i,t}(\theta),1-\varepsilon_{low},1+\varepsilon_{high})\hat A_{i,t}\right)\right]
  \]
  其中 \(r_{i,t}(\theta)\) 为逐 token 重要性采样比，\(\hat A_{i,t}\) 为组内相对奖励（减去组均值、除以组标准差）计算的优势。
- **课程学习式两阶段 RL**（借鉴 POLARIS）：
  - **Stage One**：在完整 prompt 集上训练 200 步，建立广泛能力；
  - **Stage Two**：按性能剪枝——移除模型已达成 >90% 准确率的 prompt（也试过 75%，效果更差），在更具挑战性的子集上再训练 90 步。
- 效果：单补丁生成从 SFT 后 36.0% 提升至 **45.0%**（超过同设置下 DeepSeek-R1-0528 的 43.2%）。

### 2.4 测试时扩展：增强自一致性（Enhanced Self-consistency）
- 针对代码生成中“语义等价但字符级差异大”导致普通多数投票失效的问题，提出混合打分：
  \[
  \mathrm{Score}(c)=\mathrm{Score}_{EM}(c)+\mathrm{Score}_{Sim}(c)
  \]
  - \(\mathrm{Score}_{EM}\)：标准精确匹配频次；
  - \(\mathrm{Score}_{Sim}\)：用 Levenshtein 距离计算两两相似度，取每个候选 top-k 近邻的平均相似度（k 设为生成补丁总数的一半）。
- 取得分最高者为最终答案。

## 3. 实验设计

- **Benchmark**：SWE-bench Verified（500 个真实、人工确认可解的 issue）。
- **评测流程**：改编自 Agentless 与 Agentless Mini，包含三项修改：
  1. 简化定位（只需预测相关文件，而非 file→class/function 的层级定位）；
  2. 单元测试生成阶段在 prompt 中直接注入定位阶段找到的相关文件全文；
  3. 补丁选择使用本文的增强自一致性替代普通多数投票。
- **单补丁模式**：定位模块预测文件 → 结合 text-embedding-3-small 检索文件 → 生成单个补丁。
- **多补丁模式（测试时过滤）**：多次定位、多补丁生成 → 先用仓库既有回归测试初筛 → 再用 LLM 自生成复现测试二次过滤（测试本身先经自一致性筛选）→ 最后用增强自一致性选出最终补丁。
- **对比方法**：
  - **专有模型**：GPT-4o（Agentless-1.5）、o1、GPT-4.1、o3-mini、o4-mini、Claude-3.7-Sonnet、Claude-4-Sonnet（含 OpenHands 与内部 scaffold 两种框架）。
  - **开源模型**：Devstral-Small-2505、SWE-Gym-32B、Qwen2.5-32B-Instruct、SWE-Dev-32B、SWE-agent-LM-32B、Skywork-SWE-32B、R2E-Gym-32B、SWESynInfer + Lingma SWE-GPT-72B、SWE-Fixer-72B、CGM-SWE-PY-72B、DeepSeek-V3/R1/R1-0528（671B）。
- **消融实验**：基线 Qwen2.5-32B-Instruct → +Repair → +Repair+Localization → +Repair+Localization+UT → 再加 RL 阶段。
- **泛化实验**：12 个基准 × 3 个模型（基座、SFT 模型、最终模型），覆盖通用（MMLU、MMLU-pro、GPQA-Diamond、SuperGPQA）、数学（AIME2024/2025、ZebraLogic）、代码（MBPP+、BigCodeBench (C)、BigCodeBench-Hard (C)、Aider-Polyglot、LiveCodeBench）。

## 4. 资源与算力

- **论文明确给出的训练配置**：
  - SFT：2 个 epoch，100k 上下文窗口，动态 batch 平均约 60，学习率 \(2\times10^{-5}\)，权重衰减 0.1，AdamW。
  - RL：rollout 的 prompt batch 为 128、每 prompt 采样 8 条；训练 mini-batch 为 128、每 rollout 做 8 次梯度更新；学习率 \(1\times10^{-6}\)；最大 prompt/response 长度 65,536 / 32,768 tokens；裁剪参数 \(\varepsilon_{low}=0.2\)、\(\varepsilon_{high}=0.28\)；AdamW。
- **未明确说明的部分**：论文**没有报告** GPU 型号、GPU 数量、总训练时长或总算力开销等具体资源信息。对于一套以“可复现配方”为卖点的工作，缺少算力披露是一个可指出的缺口。

## 5. 实验数量与充分性

- **实验规模概览**：
  - 主结果表 1 组（表 1，覆盖约 20 余个对比条目）；
  - 消融实验 1 组（表 2，4 个 SFT 配置 + 1 个 RL 配置）；
  - 泛化实验 1 组（表 3，12 个基准 × 3 个模型，共 36 个结果点）；
  - RL 训练过程曲线 1 张（图 5，两阶段 RL 单补丁性能随步数变化）；
  - 测试时扩展曲线 1 张（图 6，增强 vs 普通自一致性随生成补丁数变化）；
  - 数据构建流水线示意（图 2、图 4）。
- **充分性评价**：
  - **优点**：消融清晰地拆分了 R/L/UT 三份数据的边际贡献与 RL 阶段的增益；泛化实验覆盖面广，能有效回应“专用训练是否损害通用能力”的质疑；测试时扩展曲线给出了 60.2% 峰值对应的补丁数（120）。
  - **不足**：缺少对**数据规模/质量的缩放分析**（例如不同数据量、不同过滤阈值的影响）；缺少对**生成器模型选择**（DeepSeek-R1-0528）的敏感性分析；缺少对**课程剪枝阈值**（90% vs 75% 只给出一次对比且未给详细数据）的系统分析；增强自一致性中的相似度度量只用了 Levenshtein 距离，未做消融。
- **客观性与公平性**：
  - 论文对基座模型 Qwen2.5-32B-Instruct 在 Agentless 与“Agentless-Ours”两种框架下都报告了结果（30.2% 与 22.2%），并标注了哪些是自测（⋆）、哪些引自他人论文/博客，这一点较为透明。
  - 但需注意：**不同对比方法使用的框架不同**（Agentless、OpenHands、内部 scaffold、SWE-Agent、R
