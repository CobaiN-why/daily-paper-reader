---
title: "CodeSense: a Real-World Benchmark and Dataset for Code Semantic Reasoning"
title_zh: CodeSense：面向代码语义推理的真实世界基准与数据集
authors: "Monoshi Kumar Roy, Simin Chen, Benjamin Steenhoek, Jinjun Peng, Gail Kaiser, Baishakhi Ray, Wei Le"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=ehXVDJm0PS"
tags: ["query:ai-se"]
score: 8.0
evidence: 面向真实软件工程推理的代码大模型基准
tldr: 现有代码推理基准多依赖合成数据或教学题目，任务粒度粗，难以反映真实软件工程场景。本文提出CodeSense，从真实Python、C、Java仓库采集项目并执行测试以收集执行轨迹，构建覆盖细粒度代码语义推理任务的基准与数据集。该基准能更真实地评估代码大模型在实践软件工程任务中的推理能力，为改进代码模型提供可靠评测依据。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 现有代码推理基准依赖合成或教学数据且任务粒度粗，难以评估真实软件工程场景下的代码大模型。
method: 从真实Python、C、Java仓库采集项目，执行测试收集执行轨迹，构建覆盖细粒度推理任务的基准与数据集。
result: 提供了可真实评估代码大模型软件工程推理能力的一系列细粒度任务。
conclusion: 为代码大模型在真实软件工程场景下的语义推理评测提供了可靠基准。
---

## Abstract
Understanding and reasoning about code semantics is essential for enhancing code LLMs' abilities to solve real-world software engineering (SE) tasks. Although several code reasoning benchmarks exist, most rely on synthetic datasets or educational coding problems and focus on coarse-grained reasoning tasks such as input/output prediction, limiting their effectiveness in evaluating LLMs in practical SE contexts. To bridge this gap, we propose CodeSense, the first benchmark that makes available a spectrum of fine-grained code reasoning tasks concerned with the software engineering of real-world code. We collected Python, C and Java software projects from real-world repositories. We executed tests from these repositories, collected their execution traces, and constructed a ground truth dataset for fine-grained semantic reasoning tasks.  We then performed comprehensive evaluations on state-of-the-art LLMs. Our results show a clear performance gap for the models to handle fine-grained reasoning tasks. Although prompting techniques such as chain-of-thought and in-context learning helped, the lack of code semantics in LLMs fundamentally limit models' capabilities of code reasoning. Besides dataset, benchmark and evaluation, our work produced an execution tracing framework and tool set that make it easy to collect ground truth for fine-grained SE reasoning tasks, offering a strong basis for future benchmark construction and model post training. Our code and data are located at \url{https://codesense-bench.github.io/}.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
面向真实软件工程推理的代码大模型基准。

### 2. 核心内容
现有代码推理基准多依赖合成数据或教学题目，任务粒度粗，难以反映真实软件工程场景。本文提出CodeSense，从真实Python、C、Java仓库采集项目并执行测试以收集执行轨迹，构建覆盖细粒度代码语义推理任务的基准与数据集。该基准能更真实地评估代码大模型在实践软件工程任务中的推理能力，为改进代码模型提供可靠评测依据。

### 3. 对应检索需求
application of large language models to software engineering tasks such as code generation and defect detection。

### 4. 来源与原文
- Source：ICLR-2026-Accepted
- OpenReview：[https://openreview.net/forum?id=ehXVDJm0PS](https://openreview.net/forum?id=ehXVDJm0PS)
