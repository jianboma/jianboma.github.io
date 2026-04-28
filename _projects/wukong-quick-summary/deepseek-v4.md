---
layout: distill
title: "DeepSeek V4：开源大模型新王者的实力与野望"
description: "参数规模最大、性价比最高的开源模型来了——但它真的能撼动 Anthropic 和 OpenAI 的地位吗？"
importance: 1
category: Wukong-Quick-Summary
display_on_home: false

bibliography: deepseek-v4.bib

toc:
  - name: TL;DR
  - name: V4 发布：参数怪兽来了
  - name: 性能对比：与顶流差距多大？
  - name: 定价：价格屠夫再出手
  - name: 局限与挑战
  - name: 行业影响

_styles: >
  .fake-img {
    background: #bbb;
    border: 1px solid rgba(0, 0, 0, 0.1);
    box-shadow: 0 0px 4px rgba(0, 0, 0, 0.1);
    margin-bottom: 12px;
  }
---

## TL;DR

- **DeepSeek V4** 发布了两个版本：V4 Flash（284B 参数）和 V4 Pro（1.6T 参数）
- V4 Pro 是目前**参数规模最大的开源模型**（1.6T 总参数，49B 激活）
- 1M token 上下文，MoE 架构，主打高效推理
- 推理能力接近 GPT-5.4，但知识储备仍落后顶级模型 3-6 个月
- **价格屠夫**：比 GPT-5.4、Gemini 3.1 Pro、Claude Opus 4.7 都便宜一个数量级
- 纯文本模型，暂不支持多模态

---

## V4 发布：参数怪兽来了

2026 年 4 月 24 日，DeepSeek 正式发布 V4 系列 —— 继 V3.2 之后的又一重磅更新。

### 核心参数

| 模型 | 总参数 | 激活参数 | 上下文 |
|------|--------|----------|--------|
| **V4 Flash** | 284B | 13B | 1M |
| **V4 Pro** | 1.6T | 49B | 1M |

V4 Pro 的 1.6T 总参数让它成为**当前规模最大的开源模型**，超过了：
- Moonshot AI 的 Kimi K2.6（1.1T）
- MiniMax 的 M1（456B）
- DeepSeek V3.2（671B）

### 技术亮点

- **Mixture-of-Experts（MoE）**：只激活部分参数完成任务，大幅降低推理成本
- **1M token 上下文**：足以处理大型代码库或长文档
- 架构优化带来比 V3.2 更高的效率和性能

---

## 性能对比：与顶流差距多大？

### DeepSeek 官方声称

- **推理 benchmark**：V4 Pro-Max 在开源模型中领先，在部分任务上**超越 GPT-5.2 和 Gemini 3.0 Pro**
- **编程能力**：V4 系列在编程竞赛 benchmark 上**与 GPT-5.4 相当**
- **知识储备**：略落后于 GPT-5.4 和 Gemini 3.1 Pro，差距约 **3-6 个月**

### Arena Leaderboard 参考（2026年4月）

| 排名 | 模型 | 分数 |
|------|------|------|
| 1 | Claude Opus 4.7 Thinking | 1503 |
| 2 | Claude Opus 4.6 Thinking | 1503 |
| 3 | Claude Opus 4.6 | 1496 |
| 4 | Claude Opus 4.7 | 1494 |
| 5 | Gemini 3.1 Pro | 1493 |
| 9 | GPT-5.4 High | 1481 |

*注：DeepSeek V4 尚未出现在 Arena 公开榜单上，以上为顶流模型参考。*

### 关键差距

1. **推理能力**：V4 已经「几乎闭合」与前沿模型的差距
2. **知识储备**：仍是短板，落后约一个季度
3. **多模态**：纯文本输出，暂无图像/音频/视频理解能力

---

## 定价：价格屠夫再出手

DeepSeek 延续了一贯的**低价策略**：

| 模型 | 输入价格 | 输出价格 |
|------|----------|----------|
| **V4 Flash** | $0.14/M | $0.28/M |
| **V4 Pro** | $0.145/M | $3.48/M |

### 对比竞品

- **GPT-5.4 Nano / Mini**：$0.15-0.6/M 输入
- **Gemini 3.1 Flash**：$0.075/M 输入（但 Pro 更贵）
- **GPT-5.5 / Claude Opus 4.7**：$3-15/M 输出

V4 Pro 的输出价格（$3.48/M）**显著低于** Claude Opus 4.7（$15/M）和 GPT-5.5（$3+/M），但高于 Gemini 3.1 Pro。

**结论**：DeepSeek 依然是**最具性价比的选择**之一，尤其对于大规模部署场景。

---

## 局限与挑战

1. **多模态缺失**：目前仅支持文本，而竞品纷纷集成图像、音频、视频理解
2. **知识滞后**：承认落后顶级模型 3-6 个月
3. **安全争议**：
   - 德国、韩国等地已封禁 DeepSeek App
   - 美国 Accused 中国「偷窃 AI 知识产权」
   - Anthropic 和 OpenAI 曾指控 DeepSeek **模型蒸馏**
4. **数据隐私**：Pentagon 曾因员工连接中国服务器而屏蔽 DeepSeek

---

## 行业影响

DeepSeek V4 的发布意味着：

1. **开源模型天花板再次刷新**：1.6T 参数的 MoE 模型开源，社区可以直接部署
2. **价格战继续**：前沿模型的价格被进一步压低
3. **推理能力逼近顶流**：但在知识广度上仍有差距
4. **地缘政治风险**：中国 AI 公司面临的审查和限制可能加剧

---

## Technical Report Summary
Source: [DeepSeek V4 Technical Report (PDF)](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro/resolve/main/DeepSeek_V4.pdf)

---

### Overview

DeepSeek-V4 is a series of Mixture-of-Experts (MoE) language models comprising two variants:
- **DeepSeek-V4-Pro**: 1.6T total parameters, 49B activated per token
- **DeepSeek-V4-Flash**: 284B total parameters, 13B activated per token

Both support **1 million token context length** and represent a major architectural evolution from DeepSeek-V3, focused primarily on breaking the efficiency barrier for ultra-long-context processing.

---

### Architecture

#### DeepSeek-V4-Pro Specific Configuration
- **61 Transformer layers**, hidden dimension d = 7168
- **First 2 layers**: HCA (Heavily Compressed Attention)
- **Remaining layers**: CSA and HCA interleaved
- **MoE in all layers**: 1 shared expert + 384 routed experts per layer, intermediate hidden dimension 3072 per expert, 6 experts activated per token
- **First 3 MoE layers** use Hash routing (routing based on input token ID)
- **mHC expansion factor** n_hc = 4, Sinkhorn-Knopp iterations t_max = 20
- **MTP depth**: 1

##### CSA Parameters (V4-Pro)
- Compression rate m = 4
- Indexer query heads n_h^I = 64, indexer head dimension c_I = 128
- Attention top-k = 1024
- Query heads n_h = 128, head dimension c = 512, query compression dimension d_c = 1536
- Output projection groups g = 16, intermediate output dimension d_g = 1024
- Sliding window size n_win = 128

##### HCA Parameters (V4-Pro)
- Compression rate m' = 128
- Same query heads (128), head dimension (512), query compression dimension (1536) as CSA
- Same grouped output projection (g=16, d_g=1024)

---

#### Key Innovation 1: Hybrid CSA/HCA Attention

This is the most critical architectural innovation, designed to make million-token contexts computationally feasible.

##### Compressed Sparse Attention (CSA)
CSA operates in two stages:

1. **KV Compression**: Computes two series of KV entries (C^a, C^b) and compression weights (Z^a, Z^b) from hidden states. Every m tokens are compressed into one entry using learned softmax weights and positional biases. The compression uses overlapping windows — C^b indices for block i overlap with C^a indices for block i-1 — so the effective compression ratio is 1/m.

2. **Lightning Indexer for Sparse Selection**: After compression, a lightweight indexer selects top-k compressed KV entries per query token. Indexer queries are produced in a low-rank manner (down-projection → up-projection). Index scores are computed as a weighted sum of ReLU-activated dot products across multiple indexer heads.

3. **Shared Key-Value MQA**: Each compressed KV entry serves as *both* key and value (shared key-value). Attention is Multi-Query Attention (MQA) style — all query heads share the single KV head. Queries share the same compressed latent vector used for the indexer.

4. **Grouped Output Projection**: Because c·n_h is very large, outputs are split into g groups, each projected to a d_g-dimensional intermediate, then all intermediates are projected to the final d-dimensional output.

##### Heavily Compressed Attention (HCA)
Similar to CSA but with much heavier compression (m' = 128 vs m = 4) and **no sparse selection** — all compressed KV entries are attended to densely. Does not use overlapping compression. Same shared KV MQA and grouped output projection strategies.

##### Additional Attention Details
- **Partial RoPE**: Applied only to the last 64 dimensions of queries, KV entries, and attention outputs. Since KV entries serve as both keys and values, RoPE with position -i is applied to outputs to cancel absolute position embeddings and restore relative positional information.
- **Sliding Window Attention Branch**: Both CSA and HCA include an uncompressed sliding window (n_win = 128 tokens) for fine-grained local dependencies, since queries cannot access tokens within their own unfinished compression block.
- **Attention Sink**: Learnable per-head sink logits added to the softmax denominator, allowing attention scores to sum to less than 1.
- **QK Normalization**: RMSNorm applied to each query head and the single KV head before core attention.

---

#### Key Innovation 2: Manifold-Constrained Hyper-Connections (mHC)

mHC replaces standard residual connections. The residual stream is expanded from ℝ^d to ℝ^(n_hc × d) (n_hc = 4). Three mappings transform this state:

- **Input mapping** A_l ∈ ℝ^(1×n_hc): Selects what goes into the actual layer
- **Residual transformation** B_l ∈ ℝ^(n_hc × n_hc): Transforms the residual stream
- **Output mapping** C_l ∈ ℝ^(n_hc × 1): Injects layer output back into the stream

**Key constraint**: B_l is constrained to the **Birkhoff polytope** (doubly stochastic matrices), ensuring spectral norm ≤ 1 and non-expansive residual transformation for numerical stability. This is achieved via the **Sinkhorn-Knopp algorithm** (20 iterations) applied to exp(B̃_l).

Parameters are **dynamically generated** — decomposed into input-dependent components (via small projection matrices from the flattened, RMSNorm'd residual state) and static biases, with small learnable gating factors. A_l uses Sigmoid for non-negativity; C_l uses 2·Sigmoid.

---

#### Key Innovation 3: Muon Optimizer

**Muon optimizer** for most parameters, **AdamW** for embeddings, prediction head, mHC static biases/gating factors, and RMSNorm weights.

**Muon specifics**:
- Momentum = 0.95, weight decay = 0.1
- Update RMS rescaled to 0.18 for learning rate reutilization
- **Hybrid Newton-Schulz iterations** (10 total): 8 steps with coefficients (3.4445, -4.7750, 2.0315) for rapid convergence, then 2 steps with (2, -1.5, 0.5) for precise stabilization
- Nesterov momentum trick applied
- No QK-Clip needed due to attention architecture's built-in QK normalization

---

### Efficiency Analysis

At 1M tokens, DeepSeek-V4-Pro achieves:
- **27% of single-token inference FLOPs** compared to DeepSeek-V3.2
- **10% of KV cache size** compared to DeepSeek-V3.2
- **~2% of KV cache** compared to BF16 GQA8 with head dim 128

Efficiency comes from:
1. Hybrid CSA (1/4 compression + top-k sparsity) and HCA (1/128 compression)
2. Mixed precision KV storage: BF16 for RoPE dimensions, FP8 for the rest
3. FP4 precision for lightning indexer attention computation
4. Smaller attention top-k than DeepSeek-V3.2
5. FP4 for routed expert parameters (currently same peak FLOPs as FP8 on existing hardware, but theoretically 1/3 more efficient on future hardware)

---

### Training

#### Pre-Training Data
- **33T tokens** for V4-Pro (32T for V4-Flash)
- Corpus: math, code, web pages, long documents, multilingual data
- Emphasis on long-document curation (scientific papers, technical reports)
- Filtering to remove auto-generated/templated content
- Agentic data incorporated during mid-training
- Sample-level attention masking (different from V3)
- Document packing from different sources to minimize truncation

#### Training Schedule (V4-Pro)
- Peak LR: 2.0 × 10⁻⁴, end LR: 2.0 × 10⁻⁵
- Linear warmup for first 2000 steps, cosine decay near end
- Max batch size: 94.4M tokens
- Sequence length progression: 4K → 16K → 64K → 1M
- **Dense attention warmup** (longer than V4-Flash) before introducing sparse attention
- Sparse attention introduced at 64K sequence length with two-stage method: first warm up the lightning indexer, then full sparse training

#### Training Stability Techniques

1. **Anticipatory Routing**: Decouples backbone and routing network updates. At step t, uses current parameters θ_t for features but routing indices from θ_{t-Δt}. Data for step t is fetched at step t-Δt and routing indices are pre-computed and cached. Adds ~20% wall-clock overhead. Applied dynamically — triggered only when loss spikes are detected, then reverts to standard training.

2. **SwiGLU Clamping**: Linear component clamped to [-10, 10], gate component upper-bounded at 10. Eliminates outliers without performance degradation.

---

### Infrastructure

#### Expert Parallelism: Fine-Grained Communication-Computation Overlap
- Single fused kernel for MoE that overlaps computation, communication, and memory access
- Experts split into **waves** — computation begins as soon as one wave's communication completes
- In steady state: current wave computation, next wave dispatch, and completed expert combine all proceed concurrently
- **1.50-1.73× speedup** for general inference, up to **1.96×** for latency-sensitive scenarios
- Open-sourced as **MegaMoE** (component of DeepGEMM)

#### TileLang Kernel Development
- Domain-Specific Language for fused kernels
- Host Codegen reduces per-invocation overhead from tens/hundreds of μs to <1 μs
- Z3 SMT solver integration for formal integer analysis (vectorization, barrier insertion, etc.)
- Bitwise reproducibility support with IEEE-754 compliant intrinsics

---

### Post-Training

#### Pipeline
Two-stage paradigm:
1. **Specialist Training**: Independent domain experts (math, coding, agent, instruction following)
   - SFT on domain-specific data → RL with GRPO
2. **On-Policy Distillation (OPD)**: Unified model consolidation — replaces mixed RL from V3.2

#### Reasoning Modes
Three modes: Non-think, Think High, Think Max — differentiated by length penalties and context windows during RL. Think Max includes a special system prompt instruction for maximum reasoning effort. Response format uses `<think></think>` tags.

#### Generative Reward Model (GRM)
For hard-to-verify tasks, the **actor network itself functions as the GRM** — RL is applied directly to optimize both evaluative (judging) and generative capabilities jointly. Uses rubric-guided RL data, minimal human annotations needed.

#### Tool-Call Schema
New XML-based format using "|DSML|" special token — mitigates escaping failures and tool-call errors.

#### Interleaved Thinking
- **Tool-calling scenarios**: All reasoning content preserved across entire conversation (including user message boundaries) — leverages 1M context
- **General conversation**: Previous reasoning discarded at new user messages (unchanged from V3.2)

---


## 结语

DeepSeek V4 是**目前最强开源模型**——参数规模最大、价格最低、推理能力最接近顶流。

但它并非完美：无多模态、知识储备稍逊、政治敏感度偏高。

如果你的场景需要：
- **高性价比的代码/推理能力** → V4 值得一试
- **最新知识或多模态** → 仍需 GPT-5.4 / Claude Opus 4.7 / Gemini 3.1 Pro

V4 的出现让「前沿模型民主化」更进一步，但对普通人来说，**选哪个模型取决于你的具体需求和风险承受能力**。

---

## 参考

- [TechCrunch: DeepSeek previews new AI model that 'closes the gap' with frontier models](https://techcrunch.com/2026/04/24/deepseek-previews-new-ai-model-that-closes-the-gap-with-frontier-models/) (2026-04-24)
- [Arena AI Leaderboard](https://arena.ai/leaderboard) (2026-04-25)

---

*本文写于 2026 年 4 月 25 日，基于公开信息整理。*