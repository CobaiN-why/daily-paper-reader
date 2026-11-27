---
title: "Escaping Whack-a-Mole: Optimizing Documentation as Repo-Specific Playbooks for Coding Agents"
title_zh: 逃离打地鼠：将文档优化为面向编码代理的仓库专属手册
authors: "Yutong Cheng, Haifeng Chen, Wenchao Yu, Xujiang Zhao, Peng Gao, Wei Cheng"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf/d8a3af5022f656c06ce5c771b7ecf9a05130b126.pdf"
tags: ["query:ai-se"]
score: 9.0
evidence: 面向编码代理的文档自动生成与优化
tldr: 随着大模型成为自主编码代理，文档应从面向人类可读转向面向代理可执行，成为精确描述行为的仓库级手册。作者将代理导向的文档生成建模为文档空间上的黑盒优化，以下游代码正确性作为唯一质量信号，并提出DocSearch以处理程序实体相互依赖导致的输出耦合与反复修补问题。实验表明该方法能有效提升代理依文档执行任务的正确性。这为编码代理的文档生成与软件工程自动化提供了新范式。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 编码代理依赖文档执行任务，但传统面向人类可读的文档难以支撑代理的精确行为需求。
method: 把代理导向的文档生成形式化为黑盒优化问题，提出DocSearch缓解实体间输出耦合导致的反复修补。
result: 以下游代码正确性为评价信号，方法在文档优化上优于常规大模型迭代精炼。
conclusion: 工作确立了面向代理可执行性的文档生成新范式，服务于编码代理的自动化软件开发。
---

## Abstract
As large language models increasingly function as autonomous coding agents, code documentation should be designed not for human readability, but for agent executability — serving as repo-specific playbooks that specify precise behaviors agents can follow. We formulate agent-oriented documentation generation as a black-box optimization problem over the documentation space, where quality is defined solely by downstream code correctness. A central challenge for conventional LLM refinement methods is output coupling—program entities are interdependent, and refining the documentation of one entity can invalidate its callers, resulting in a persistent whack-a-mole phenomenon during inference-time scaling. We propose DocSearch, a dependency-guided bi-level search framework that systematically exploits test-time feedback. The outer level conducts a priority search over the program-entity dependency DAG, enforcing a callee-before-caller refinement order to prevent downstream interference. The inner level performs a beam search over documentation refinements, using diversified error message sampling from self-generated unit tests to better exploit diagnostic signals and escape local optima. On DevEval+, DocSearch achieves 90.7\% solve rate with GPT-4o, outperforming the strongest baseline by 32.6\%. Cross-language experiments further demonstrate that optimized documentation transfers effectively to different target programming languages. Code is available at https://github.com/ccsnow127/docsearch.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
面向编码代理的文档自动生成与优化。

### 2. 核心内容
随着大模型成为自主编码代理，文档应从面向人类可读转向面向代理可执行，成为精确描述行为的仓库级手册。作者将代理导向的文档生成建模为文档空间上的黑盒优化，以下游代码正确性作为唯一质量信号，并提出DocSearch以处理程序实体相互依赖导致的输出耦合与反复修补问题。实验表明该方法能有效提升代理依文档执行任务的正确性。这为编码代理的文档生成与软件工程自动化提供了新范式。

### 3. 对应检索需求
coding agents for automated test generation and documentation。

### 4. 来源与原文
- Source：ICML-2026-Accepted
- OpenReview：[https://openreview.net/forum?id=88NO4CL9EQ](https://openreview.net/forum?id=88NO4CL9EQ)
