---
title: "FHE-Coder: Benchmarking Secure Agentic Code Generation for Fully Homomorphic Encryption"
title_zh: FHE-Coder：面向全同态加密的安全智能体代码生成基准
authors: "Mayank Kumar, Jiaqi Xue, Mengxin Zheng, Qian Lou"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=4F1py5vQXm"
tags: ["query:ai-se"]
score: 8.0
evidence: 大模型智能体从规格生成安全代码
tldr: 全同态加密的落地依赖专业密码知识与易错的参数配置，门槛较高。本文研究大模型智能体能否从自然语言规格可靠生成安全的FHE代码，提出FHE-Coder三阶段智能体框架，包含提示形式化器、专用检索增强模块等以应对语义歧义、API误用与密码学不安全等失败模式。该工作将代码生成与大模型安全结合，为安全代码生成提供了新基准与框架。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: FHE落地受限于专业密码知识与易错参数配置，需要可靠的安全代码生成。
method: 提出三阶段智能体框架，含提示形式化与专用检索增强生成等模块。
result: 框架针对语义歧义、API误用与密码不安全等失败模式进行了系统评测。
conclusion: 为结合安全需求的大模型代码生成提供了基准与可复用框架。
---

## Abstract
Fully Homomorphic Encryption (FHE) is a foundational technology for confidential computing, yet its practical adoption remains limited by the need for specialized cryptographic expertise and error-prone parameter configuration. To lower this barrier, we investigate whether Large Language Model (LLM) agents can reliably generate secure FHE code from natural-language specifications. We present FHE-Coder, a three-phase agentic framework that addresses the key failure modes of FHE code generation: semantic ambiguity, API misuse, and cryptographic insecurity. The framework integrates (1) a Prompt Formalizer that structures user intent and enforces secure parameterization, (2) a specialized retrieval-augmented generation (RAG) module that supplies scheme-specific API and documentation knowledge, and (3) an automated Security Verifier that performs iterative validation and feedback to detect and correct cryptographic flaws. We evaluate FHE-Coder across four leading LLMs on a benchmark of ten FHE programming tasks spanning increasing functional and security complexity. While baseline agents frequently produce code that compiles and passes functional tests, they often violate security constraints or misuse cryptographic parameters. In contrast, FHE-Coder consistently generates solutions that are compilable, functionally correct, and verifiably secure across schemes including TFHE and CKKS. Our work establishes a systematic methodology and benchmark for agentic FHE code generation, providing a practical step toward democratizing secure computation without compromising cryptographic guarantees.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
大模型智能体从规格生成安全代码。

### 2. 核心内容
全同态加密的落地依赖专业密码知识与易错的参数配置，门槛较高。本文研究大模型智能体能否从自然语言规格可靠生成安全的FHE代码，提出FHE-Coder三阶段智能体框架，包含提示形式化器、专用检索增强模块等以应对语义歧义、API误用与密码学不安全等失败模式。该工作将代码生成与大模型安全结合，为安全代码生成提供了新基准与框架。

### 3. 对应检索需求
application of large language models to software engineering tasks such as code generation and defect detection。

### 4. 来源与原文
- Source：ICLR-2026-Accepted
- OpenReview：[https://openreview.net/forum?id=4F1py5vQXm](https://openreview.net/forum?id=4F1py5vQXm)
