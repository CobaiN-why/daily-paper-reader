---
title: "CodeStructEval: A Holistic Evaluation Framework of Code Structure Generation and Comprehension"
title_zh: CodeStructEval：代码结构生成与理解的整体评估框架
authors: "Zhanyue Qin, jia feng, Xin-Cheng Wen, Cuiyun Gao, Qing Liao"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=5koD6h0ep1"
tags: ["query:ai-se"]
score: 8.0
evidence: 评估大模型代码结构生成与理解的框架
tldr: 现有代码评测基准多关注从自然语言需求生成顺序代码，难以反映模型对程序逻辑与结构的深层理解。作者提出CodeStructEval，正式定义代码结构生成与结构理解两类任务，构建整体性评估框架，考察大模型的结构感知与逻辑推理能力。该工作为软件工程任务中的代码生成评测提供了更全面的视角，有助于揭示模型在结构化代码方面的真实能力边界。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 现有基准多评估顺序代码生成，难以反映模型对程序结构的深层理解。
method: 定义代码结构生成与理解两类任务，构建考察结构感知与逻辑推理的整体评估框架。
result: 框架为代码生成评测提供了更全面视角，揭示模型结构化能力边界。
conclusion: 该工作丰富了软件工程中代码生成能力的评估维度。
---

## Abstract
As Large Language Models (LLMs) rapidly evolve and demonstrate strong performances in software engineering tasks, a growing number of researchers are focusing on evaluating LLMs' code generation capabilities. Different from previous benchmarks that primarily focus on evaluating LLMs' ability to generate sequential code from natural language requirements, we propose to assess their capabilities in generating and comprehending code structures. The two aspects represent a deeper, more fundamental understanding of program logic that better reflects the model's capacity for logical reasoning and structural awareness.
Specifically, in the paper, we formally propose two tasks: CSG ($\textbf{C}$ode $\textbf{S}$tructure $\textbf{G}$eneration) and CSC ($\textbf{C}$ode $\textbf{S}$tructure $\textbf{C}$omprehension). The former requires LLMs to generate code structural information from given code, while the latter requires it to generate code from given code structural information. Then, we design a holistic evaluation framework called CodeStructEval to assess LLMs' code structure generation and comprehension capabilities. This programming language agnostic evaluation framework has three main parts: 1) data preprocessing, 2) model inference, and 3) automated evaluation. For evaluation metrics, we introduce SAR ($\textbf{S}$emantic $\textbf{A}$ccuracy $\textbf{R}$ate) and StAR ($\textbf{St}$ructure $\textbf{A}$ccuracy
$\textbf{R}$ate) to assess LLM' output quality semantically and structurally, respectively. Then, using the CodeStructEval framework and the HumanEval seed dataset, we built a benchmark with 157 samples across three difficulty levels (Easy, Medium, Hard). At last, we use this benchmark to thoroughly evaluate the code structure generation and comprehension abilities of 18 mainstream LLMs. Our experimental results show that closed-source commercial LLMs demonstrate strong code structure generation and comprehension capabilities, while smaller open-source LLMs still have room for improvement.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
评估大模型代码结构生成与理解的框架。

### 2. 核心内容
现有代码评测基准多关注从自然语言需求生成顺序代码，难以反映模型对程序逻辑与结构的深层理解。作者提出CodeStructEval，正式定义代码结构生成与结构理解两类任务，构建整体性评估框架，考察大模型的结构感知与逻辑推理能力。该工作为软件工程任务中的代码生成评测提供了更全面的视角，有助于揭示模型在结构化代码方面的真实能力边界。

### 3. 对应检索需求
application of large language models to software engineering tasks such as code generation and defect detection。

### 4. 来源与原文
- Source：ICLR-2026-Rejected-Public
- OpenReview：[https://openreview.net/forum?id=5koD6h0ep1](https://openreview.net/forum?id=5koD6h0ep1)
