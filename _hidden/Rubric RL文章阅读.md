---
layout: page
title: Rubric RL 相关文章
categories: [research, paper, 中文]
search_only: false
date: 2025-03-17 09:00:00 +0800
pinned: false
---

<style>
:root {
  --blue:    #4a7cf7;
  --green:   #3ab87a;
  --purple:  #8b5cf6;
  --orange:  #f59e0b;
  --red:     #ef4444;
  --surface: #f5f7fc;
  --border:  #e0e6f0;
  --dim:     #6b7a99;
  --radius:  10px;
}

/* ── Section cards ── */
.ps {
  background: var(--surface);
  border: 1px solid var(--border);
  border-left: 4px solid var(--blue);
  border-radius: var(--radius);
  padding: 1.3rem 1.6rem;
  margin: 1.2rem 0;
}
.ps.green  { border-left-color: var(--green); }
.ps.purple { border-left-color: var(--purple); }
.ps.orange { border-left-color: var(--orange); }
.ps h4 { margin: 0 0 .8rem; font-size: .9rem; color: var(--dim); font-weight: 600; letter-spacing: .05em; text-transform: uppercase; }

/* ── Paper rows ── */
.pe {
  display: flex;
  align-items: flex-start;
  gap: .75rem;
  padding: .55rem 0;
  border-bottom: 1px dashed var(--border);
}
.pe:last-child { border-bottom: none; }
.pb {
  display: inline-flex;
  align-items: center;
  font-size: .66rem;
  font-weight: 700;
  letter-spacing: .07em;
  text-transform: uppercase;
  padding: .2em .6em;
  border-radius: 4px;
  white-space: nowrap;
  margin-top: .15rem;
  flex-shrink: 0;
  min-width: 54px;
  justify-content: center;
}
.b-scale  { background:#dbeafe; color:#1d4ed8; }
.b-uw     { background:#dcfce7; color:#15803d; }
.b-meta   { background:#fce7f3; color:#be185d; }
.b-ant    { background:#fef3c7; color:#92400e; }
.b-cmu    { background:#ede9fe; color:#6d28d9; }
.b-arxiv  { background:#f1f5f9; color:#475569; }
.b-iclr   { background:#fff7ed; color:#c2410c; }

.pi { flex: 1; line-height: 1.5; }
.pt { font-weight: 600; font-size: .92rem; }
.pd { font-size: .82rem; color: var(--dim); margin-top: .16rem; }

/* ── Highlight tag ── */
.tag {
  display: inline-block;
  font-size: .68rem;
  padding: .1em .5em;
  border-radius: 4px;
  margin-left: .4em;
  vertical-align: middle;
  font-weight: 600;
}
.tag-first { background:#fef3c7; color:#92400e; }

/* ── Thought box ── */
.thought {
  background: linear-gradient(135deg, #f0f4ff 0%, #f9f0ff 100%);
  border: 1px solid #d4d8f0;
  border-radius: var(--radius);
  padding: 1.2rem 1.5rem;
  margin: 1.4rem 0;
  font-size: .9rem;
  line-height: 1.7;
}
.thought h3 { margin-top: 0; font-size: 1rem; }
.thought ul { margin-bottom: 0; }

/* ── Details (collapsible) ── */
details { margin: .4rem 0 0; }
summary {
  cursor: pointer;
  font-size: .78rem;
  color: var(--blue);
  font-weight: 600;
  user-select: none;
}
summary:hover { text-decoration: underline; }
details[open] summary { margin-bottom: .5rem; }
.method-box {
  background: #fff;
  border: 1px solid var(--border);
  border-radius: 8px;
  padding: .9rem 1.1rem;
  font-size: .83rem;
  line-height: 1.65;
  color: #374151;
}
.method-box ol, .method-box ul { margin: .4rem 0; padding-left: 1.3rem; }
.method-box li { margin: .25rem 0; }

/* ── TOC ── */
.toc {
  background: #fff;
  border: 1px solid var(--border);
  border-radius: var(--radius);
  padding: 1rem 1.4rem;
  display: inline-block;
  margin-bottom: 1.6rem;
  font-size: .87rem;
  min-width: 280px;
}
.toc-title { font-weight: 700; margin-bottom: .5rem; color: var(--dim); font-size: .75rem; letter-spacing: .1em; text-transform: uppercase; }
.toc ol, .toc ul { margin: 0; padding-left: 1.2rem; }
.toc li { margin: .28rem 0; }
.toc a  { color: var(--blue); text-decoration: none; }
.toc a:hover { text-decoration: underline; }
</style>

> **阅读背景：** 2026 年 2 月系统梳理了市面上关于 **Rubric-based RL** 的工作，从 Rubric 生成、应用到周边方法进行分类整理。

<div class="toc">
  <div class="toc-title">📑 目录</div>
  <ol>
    <li><a href="#rubric-gen">Rubric 生成</a></li>
    <li><a href="#rubric-app">Rubric 应用</a>
      <ul>
        <li><a href="#consistent-steps">一致推理步骤筛选</a></li>
        <li><a href="#scaffold">生成时引入 Rubric</a></li>
      </ul>
    </li>
    <li><a href="#more">更多相关工作</a></li>
    <li><a href="#thoughts">个人思考</a></li>
    <li><a href="#reading">Paper Reading 摘要</a></li>
  </ol>
</div>

---

## 📐 Rubric 生成 {#rubric-gen}

<div class="ps">

<div class="pe">
  <span class="pb b-scale">Scale AI</span>
  <div class="pi">
    <div class="pt"><a href="https://arxiv.org/pdf/2507.17746">Rubrics as Rewards: Reinforcement Learning Beyond Verifiable Domains</a></div>
    <div class="pd">用 LLM 基于已有 Rubric 生成新 Rubric，突破可验证域的限制</div>
  </div>
</div>

<div class="pe">
  <span class="pb b-uw">UW / AI2</span>
  <div class="pi">
    <div class="pt"><a href="https://arxiv.org/pdf/2511.19399">DR Tulu: Reinforcement Learning with Evolving Rubrics for Deep Research</a></div>
    <div class="pd">动态更新 Rubric，维护随训练演化的 Rubric 库，更好适配 query 分布变化</div>
  </div>
</div>

<div class="pe">
  <span class="pb b-arxiv">arXiv</span>
  <div class="pi">
    <div class="pt"><a href="https://arxiv.org/pdf/2407.19594">META-REWARDING LANGUAGE MODELS: Self-Improving Alignment with LLM-as-a-Meta-Judge</a></div>
    <div class="pd">引入 Meta Judge 机制，模型自我提升对齐能力，判断者与被判断者互相强化</div>
  </div>
</div>

<div class="pe">
  <span class="pb b-meta">Meta</span>
  <div class="pi">
    <div class="pt"><a href="https://arxiv.org/pdf/2509.14234">Compute as Teacher: Turning Inference Compute Into Reference-Free Supervision</a></div>
    <div class="pd">Anchor 结合多条 rollouts 合成参考回答，再基于参考回答生成对应 Rubric，无需人工标注参考答案</div>
  </div>
</div>

</div>

---

## 🎯 Rubric 应用 {#rubric-app}

<div class="ps green">

<div class="pe">
  <span class="pb b-ant">Ant</span>
  <div class="pi">
    <div class="pt">
      <a href="https://arxiv.org/pdf/2508.12790">Reinforcement Learning with Rubric Anchors</a>
      <span class="tag tag-first">🏆 First Paper</span>
    </div>
    <div class="pd">首个提出 Rubric RL 框架的工作，将结构化评分标准引入强化学习奖励设计</div>
  </div>
</div>

</div>

### 一致推理步骤筛选 {#consistent-steps}

> 只有在多条正确轨迹中**一致出现**的步骤，才被视为合理的推理步骤。

<div class="ps green">

<div class="pe">
  <span class="pb b-arxiv">arXiv</span>
  <div class="pi">
    <div class="pt"><a href="https://arxiv.org/pdf/2510.14738">AUTORUBRIC-R1V: Rubric-Based Generative Rewards for Faithful Multimodal Reasoning</a></div>
    <div class="pd">通过跨轨迹一致性过滤噪声推理步骤，生成更可信的多模态推理奖励信号</div>
  </div>
</div>

</div>

### 生成时引入 Rubric {#scaffold}

> 在生成回答的过程中就注入部分 Rubric 作为脚手架（Scaffold），引导探索方向。

<div class="ps green">

<div class="pe">
  <span class="pb b-arxiv">arXiv</span>
  <div class="pi">
    <div class="pt"><a href="https://arxiv.org/pdf/2508.16949">Breaking the Exploration Bottleneck: Rubric-Scaffolded RL for General LLM Reasoning</a></div>
    <div class="pd">在生成阶段嵌入 Rubric 结构约束，缓解 RL 训练中的探索瓶颈问题</div>
  </div>
</div>

</div>

---

## 📚 Paper Reading 摘要 {#reading}

<div class="ps orange">

<div class="pe">
  <span class="pb b-arxiv">arXiv</span>
  <div class="pi">
    <div class="pt"><a href="https://arxiv.org/pdf/2601.06487v1">ArenaRL: Scaling RL for Open-Ended Agents via Tournament-based Relative Ranking</a></div>
    <div class="pd">将 GRPO 的组内打分替换为两两 LLM-as-a-Judge 比较；采用种子轮、瑞士轮等排序方法探索低复杂度拓扑排序，数据集自建</div>
  </div>
</div>

<div class="pe">
  <span class="pb b-arxiv">arXiv</span>
  <div class="pi">
    <div class="pt"><a href="https://arxiv.org/pdf/2511.10507">AdvancedIF: Rubric-Based Benchmarking and Reinforcement Learning for Advancing LLM Instruction Following
</a></div>
    <div class="pd">训练 <strong>Rubric Generator</strong> + <strong>Rubric Verifier</strong> 双模型：Generator 基于小规模专家数据训练后扩展到大规模，自动为训练数据生成对应 Rubric</div>
  </div>
</div>

<div class="pe">
  <span class="pb b-arxiv">arXiv</span>
  <div class="pi">
    <div class="pt"><a href="https://arxiv.org/pdf/2510.07743">OpenRubrics: Towards Scalable Synthetic Rubric Generation for Reward Modeling and LLM Alignment</a></div>
    <div class="pd">以「Prompt + 优选回答 + 被拒回答」为上下文训练 Rubric 生成模型；将 Rubric 分为 <em>Hard Rules</em>（必须严格满足）和 <em>Principles</em>（可模糊权衡），避免奖励模型混淆两类标准</div>
  </div>
</div>
<div class="pe">
  <span class="pb b-arxiv">arXiv</span>
  <div class="pi">
    <div class="pt"><a href="https://arxiv.org/pdf/2508.16949v3">Breaking the Exploration Bottleneck: Rubric-Scaffolded Reinforcement Learning for General LLM Reasoning</a></div>
    <div class="pd">Rubric 不应该只在训练结束后拿来评分，它还应该在生成过程中作为“外部认知脚手架”，帮助模型走出自己原本想不到的推理路径。</div>
  </div>
</div>
 

<div class="pe">
  <span class="pb b-arxiv">arXiv</span>
  <div class="pi">
    <div class="pt"><a href="https://arxiv.org/pdf/2510.17314">AUTO-RUBRIC: Learning to Extract Generalizable Criteria for Reward Modeling</a></div>
    <div class="pd">两阶段框架：① Query-Specific Rubric Inference（Propose–Evaluate–Revise 循环）；② Query-Agnostic Rubric Aggregation（信息论驱动的最大化编码率选出紧凑通用准则集），输出 Theme–Tips 层次结构</div>
    <details>
      <summary>展开方法细节</summary>
      <div class="method-box">
        <strong>阶段一：Query-Specific Rubric Inference</strong>
        <ol>
          <li><strong>Propose：</strong>用生成模型为偏好样本（query + 正回答 + 负回答）生成初步评价准则草案</li>
          <li><strong>Evaluate：</strong>评估模型检验准则是否能正确区分正/负回答</li>
          <li><strong>Revise：</strong>若评估失败，修订模型修正准则并重新验证，循环直至收敛</li>
        </ol>
        <strong>阶段二：Query-Agnostic Rubric Aggregation</strong>
        <ul>
          <li>用信息论驱动的<strong>最大化编码率（Coding Rate）</strong>算法，从所有 query-specific 准则中选出紧凑集合</li>
          <li>目标：高覆盖度 × 低冗余性 × 高信息量</li>
          <li>输出 <strong>Theme–Tips</strong> 层次结构（高层主题 + 具体提示）</li>
        </ul>
      </div>
    </details>
  </div>
</div>

<div class="pe">
  <span class="pb b-arxiv">arXiv</span>
  <div class="pi">
    <div class="pt"><a href="https://arxiv.org/pdf/2511.12344">Reward and Guidance through Rubrics: Promoting Exploration to Improve Multi-Domain Reasoning</a></div>
    <div class="pd">稠密 Rubric 奖励（Factual + Process）+ GRPO 策略更新；离线收集高评分未完美轨迹生成指导信号，用于离线策略 refinement</div>
    <details>
      <summary>展开训练流程</summary>
      <div class="method-box">
        <ol>
          <li>使用当前策略生成多个回答 / 推理轨迹</li>
          <li>用 Rubric 评估轨迹（Factual + Process 两维度）</li>
          <li>计算稠密奖励，基于 GRPO 更新策略参数</li>
          <li>离线收集高评分但未完美的轨迹</li>
          <li>分析这些轨迹，生成指导信号</li>
          <li>将指导信号用于离线策略 refinement</li>
        </ol>
      </div>
    </details>
  </div>
</div>

<div class="pe">
  <span class="pb b-arxiv">arXiv</span>
  <div class="pi">
    <div class="pt"><a href="https://arxiv.org/pdf/2509.21500">Chasing the Tail: Effective Rubric-based Reward Modeling for LLM Post-Training</a></div>
    <div class="pd">两步 Rubric 构造：① Proposer LLM（如 GPT-4.1）分析离策略响应差异，生成细粒度判别标准；② 迭代细化——从最优响应出发逐步添加更精细标准，直到获得高判别力 Rubric 集</div>
  </div>
</div>

<div class="pe">
  <span class="pb b-arxiv">arXiv</span>
  <div class="pi">
    <div class="pt"><a href="https://arxiv.org/pdf/2504.02495">Inference-Time Scaling for Generalist Reward Modeling</a></div>
    <div class="pd">在推理阶段扩展计算量以提升通用奖励模型的评估质量，探索 Test-Time Scaling 在 RM 场景的有效性</div>
  </div>
</div>

<div class="pe">
  <span class="pb b-arxiv">arXiv</span>
  <div class="pi">
    <div class="pt"><a href="https://arxiv.org/pdf/2511.20651">RubricRL: Simple Generalizable Rewards for Text-to-Image Generation</a></div>
    <div class="pd">将 Rubric RL 扩展到图像生成领域，由 GPT-o4-mini 自动为输入 Prompt 生成细粒度评估标准</div>
  </div>
</div>

<div class="pe">
  <span class="pb b-arxiv">arXiv</span>
  <div class="pi">
    <div class="pt"><a href="https://arxiv.org/pdf/2510.14660">An Efficient Rubric-based Generative Verifier for Search-Augmented LLMs</a></div>
    <div class="pd">面向检索增强 LLM 的高效 Rubric 生成式验证器，兼顾验证精度与推理效率</div>
  </div>
</div>

</div>

---

## 🗂 更多相关工作 {#more}

<div class="ps purple">

<div class="pe">
  <span class="pb b-arxiv">Didi</span>
  <div class="pi">
    <div class="pt"><a href="https://arxiv.org/pdf/2509.21842">DeepTravel: An End-to-End Agentic RL Framework for Autonomous Travel Planning</a></div>
    <div class="pd">Agent 与沙箱环境交互的端到端旅行规划 RL 框架 <span class="tag" style="background:#e0f2fe;color:#0369a1;">ICLR 2448</span></div>
  </div>
</div>

<div class="pe">
  <span class="pb b-ant">Ant</span>
  <div class="pi">
    <div class="pt"><a href="https://arxiv.org/pdf/2509.25534">Self-Rewarding Rubric-Based RL for Open-Ended Reasoning</a></div>
    <div class="pd">基于 Rubric 的自奖励强化学习，无需外部评分器即可处理开放式推理任务 <span class="tag" style="background:#e0f2fe;color:#0369a1;">ICLR 2446</span></div>
  </div>
</div>

<div class="pe">
  <span class="pb b-cmu">CMU</span>
  <div class="pi">
    <div class="pt"><a href="https://arxiv.org/pdf/2506.02355">Improving Reward for Low-Probability Correct Answers in GRPO</a></div>
    <div class="pd">提升 GRPO 训练中概率低但正确回答的奖励权重，缓解少数正确样本被忽视的问题</div>
  </div>
</div>

</div>

---

## 💡 个人思考 {#thoughts}

<div class="thought">

<h3>Rubric 生成 vs. Rubric 应用</h3>

生成方面分为 **Hardcode** 和 **Dynamic Update** 两种策略：

- **Hardcode** — 简单易编写，但粒度不够细，难以覆盖所有评估维度
- **Dynamic Update** — 能根据不同 query 动态调整，适配性更强，但 Rule Library 的维护成本较高

UW & AI2 的工作专门研究了 Rubric 更新方法，见[分析笔记](https://chatgpt.com/share/6969d9df-a544-8006-bd23-54725663397f)。

---

**几个悬而未决的问题：**

- 是否应该结合笔记（Note）来辅助 Rubric 生成？
- 供给侧数据所包含的多样性，与模型真正感知到的多样性之间存在差距，如何弥合？
- **蒙特卡洛树搜索**可能是生成多样性的有效手段——通过寻找同级节点或父子节点来构造多样化的推理轨迹

</div>

---