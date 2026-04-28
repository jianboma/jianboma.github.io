---
layout: distill
title: "AI 科学家：从辅助到自主的演进"
description: "自动做研究不再只是科幻——当前 AI Agent 系统的全景图与未来展望"
importance: 1
category: AutoResearch
display_on_home: false
bibliography: auto_research.bib

toc:
  - name: 引言
  - name: AI Agent 做研究：现在能做什么？
  - name: 主流系统横评
  - name: 为什么跨模型评审很重要？
  - name: 挑战与局限
  - name: 未来展望
  - name: 结语

_styles: >
  .fake-img {
    background: #bbb;
    border: 1px solid rgba(0, 0, 0, 0.1);
    box-shadow: 0 0px 4px rgba(0, 0, 0, 0.1);
    margin-bottom: 12px;
  }
  .fake-img p {
    font-family: monospace;
    color: white;
    text-align: left;
    margin: 12px 0;
    text-align: center;
    font-size: 16px;
  }
---

## 引言：当 AI 开始"搞科研"

想象一下：你在睡觉，AI 在跑实验；你醒来时，发现它已经完成了文献调研、做了 20 组实验、写了论文初稿、还自己审了一轮。

这不是远景——**多个开源项目已经实现了这个流程**。

从 Andrej Karpathy 的「睡前 запусти 实验」到 SakanaAI 的「完全自动化科学发现」，从单人作战的科研助手到多智能体协作的研究团队，AI 正在重塑科学研究的范式。

这篇文章会：
1. 聊聊 AI Agent 做研究的可能性
2. 横向对比当前主流系统
3. 展望未来

---

## 一、AI Agent 做研究：现在能做什么？

### 1.1 核心能力

现代 LLM-based AI Agent 已经可以独立完成：

| 能力 | 描述 |
|------|------|
| **文献调研** | 搜索 arXiv、Zotero、Obsidian、CrossRef，自动总结 |
| **想法生成** | 基于已有工作提出新研究方向 |
| **实验执行** | 写代码、改代码、跑训练、调参 |
| **结果分析** | 可视化、统计分析、发现规律 |
| **论文写作** | LaTeX 排版、图表生成、格式规范 |
| **同行评审** | 模拟审稿人给出评分和改进建议 |

### 1.2 两种范式

- **Human-in-the-loop**：人主导，AI 打下手（写代码、查文献）
- **Human-on-the-loop**：AI 主导，人在关键节点审批（EvoScientist 的定位）

---

## 二、主流系统横评

### 2.1 SakanaAI / AI-Scientist 🧪

> *首个完全自动化的开源科学发现系统*

**定位**：从想法到论文的端到端自动化

**核心能力**：
- 自动生成研究想法（基于模板）
- 自主设计并执行实验
- 撰写完整论文（LaTeX + PDF）
- 模拟同行评审

**支持的领域**：NanoGPT 训练、2D 扩散模型、Grokking 现象

**局限**：目前依赖预设模板，通用性有限

---

### 2.2 EvoScientist ⚙️

> *自进化的 AI 科学家框架*

**定位**：多智能体研究团队

**核心架构**：
- 6 个子智能体：plan → research → code → debug → analyze → write
- 持久记忆（跨会话）
- MCP 集成（可动态接入工具）
- 多渠道（CLI + Telegram + Slack + 飞书 + 微信）

**特点**：
- "Human-on-the-loop"：AI 是研究伙伴，与人共同进化
- 多模型支持：Anthropic、OpenAI、Google、NVIDIA
- 技能系统：可从 GitHub 安装研究技能

---

### 2.3 karpathy / autoresleep 🚀

> *Andrej Karpathy 的个人实验*

**定位**：单 GPU 上的自动化训练实验

**核心理念**：
- 极简：只有 3 个文件（prepare.py, train.py, program.md）
- 固定 5 分钟预算：每次实验都是 5 分钟，便于比较
- Agent 只改 train.py，其他保持固定

**优势**：
- 极其轻量，适合个人研究者
- 可复现性强
- 约每小时 12 次实验，睡觉时能跑 ~100 次

**局限**：只管训练实验，不涉及文献和写作

---

### 2.4 ARIS (Auto-Research-In-Sleep) 🌙

> *让 Claude Code 帮你做研究*

**定位**：端到端 Claude Code 技能包

**核心创新**：**跨模型评审**
- Claude Code 执行（快）
- Codex (GPT-5.4) 评审（慢但严谨）
- 对抗性审查，避免自我审查盲点

**工作流**：
1. `/idea-discovery`：文献 → 8-12 个想法 → GPU 试点
2. `/auto-review-loop`：4 轮自主评审，5/10 → 7.5/10
3. `/paper-writing`：叙事 → LaTeX → PDF → 8.5/10
4. `/research-pipeline`：一键端到端

**特色功能**：
- Zotero + Obsidian + 本地 PDF + arXiv 多源文献
- DBLP/CrossRef 真实 BibTeX 防幻觉
- 飞书/微信通知

---

### 2.5 openags / auto-research 🏗️

> *通用科学家框架*

**定位**：从文献调研到投稿的全流程

**两阶段规划**：
- Phase 1：纯软件智能体
- Phase 2：+ 机器人（物理实验）

**覆盖环节**：文献综述 → 提案 → 实验 → 写作 → 投稿 → 审稿

---

### 2.6 对比矩阵

| 系统 | 自动化程度 | 智能体数 | 写作能力 | 评审能力 | 适用场景 |
|------|-----------|---------|---------|---------|---------|
| AI-Scientist | ★★★★★ | 1 | ✅ | ✅ | 完全自动化科研 |
| EvoScientist | ★★★★☆ | 6 | ✅ | ❌ | 团队协作、可扩展 |
| ARIS | ★★★★☆ | 2+ | ✅ | ✅ | Claude Code 用户 |
| auto-research | ★★★☆☆ | 多 | ✅ | ❌ | 全流程管理 |
| karpathy | ★★☆☆☆ | 1 | ❌ | ❌ | 训练实验自动化 |

---

## 三、为什么跨模型评审很重要？

ARIS 论文[1] 提到了一个深刻洞见：

> *单一模型自我审查 = 随机 bandit（可预测的奖励噪声）*  
> *跨模型审查 = 对抗性 bandit（审查者主动探测执行者未预料的弱点）*

两人对弈收敛到 Nash 均衡的效率，远高于多人混战。**从 1→2 的收益最大，2→4 边际收益递减。**

这也是为什么 ARIS 用 Claude Code + Codex，而不是让同一个模型既执行又评审。

---

## 四、挑战与局限

1. **科学品味**：AI 能执行指令，但"什么是好的研究方向"仍需人类判断
2. **幻觉风险**：文献引用、实验设计仍可能出错
3. **物理实验**：目前只能做模拟，真实世界的实验还需机器人
4. **评估标准**：如何衡量"科学发现"的质量？现有基准有限
5. **安全风险**：AI 写的代码可能调用危险包，需要容器化隔离

---

## 五、未来展望

### 短期（1-2 年）
- 更多领域模板（生物、化学、材料科学……）
- 更强的多模态能力（读图、分析数据）
- 与真实实验设备集成

### 中期（3-5 年）
- AI 科学家 vs 人类科学家合作论文
- 自动同行评审系统
- 跨领域迁移能力

### 长期
- 真正的 "AI Nobel Prize"
- 自我改进的科学研究循环

---

## 结语

AI 不会取代科学家，但**会用 AI 的科学家会取代不会用 AI 的**。

现在的系统已经从"写代码的助手"进化到"能自主做研究的伙伴"。无论你是：
- 想自动化实验流程 → **karpathy/autoresearch**
- 想端到端写论文 → **ARIS** 或 **AI-Scientist**
- 想搭建团队级研究系统 → **EvoScientist**

都有现成的开源项目可以尝试。

*唯一的问题是：你准备好让 AI 帮你做研究了吗？*

---

## 参考

- [1] ARIS: Auto-Research-In-Sleep. wanshuiyin et al. 2026.
- [2] EvoScientist: Towards Multi-Agent Evolving AI Scientists. Lyu et al. arXiv:2603.08127
- [3] The AI Scientist: Towards Fully Automated Open-Enented Scientific Discovery. SakanaAI, 2024.

---

*本文基于 2026 年 3 月的开源项目调研，后续可能有更新。*
