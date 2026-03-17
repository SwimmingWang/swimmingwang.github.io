---
layout: page
title: "Rubric RL文章阅读"
categories: [research, paper, 中文]
search_only: false
date: 2025-03-17 09:00:00 +0800
# external_embed: ""
# external_link: ""
# external_label: "测试引入谷歌文档"
---
Note: 2026年2月份阅读的市面上的rubric rl的文章。

# Rubric 文章阅读分类

## Rubric 生成
1. [Rubrics as Rewards: Reinforcement Learning Beyond Verifiable Domains](https://arxiv.org/pdf/2507.17746) (scale ai) 类似用rubric生成rubric
2. [DR Tulu: Reinforcement Learning with Evolving Rubrics for Deep Research](https://arxiv.org/pdf/2511.19399) (UW and AI2) 动态更新rubric，动态维护rubric库
3. [META-REWARDING LANGUAGE MODELS: Self-Improving Alignment with LLM-as-a-Meta-Judge](https://arxiv.org/pdf/2407.19594) meta judge
4. [Compute as Teacher: Turning Inference Compute Into Reference-Free Supervision](https://arxiv.org/pdf/2509.14234) (meta) Anchor结合多条rollouts合成参考回答, 再生成对应 rubrics

## Rubric 应用
[Reinforcement Learning with Rubric Anchors](https://arxiv.org/pdf/2508.12790) (Ant) The first paper to propose rubric rl.

### 在多个正确轨迹中一致出现的步骤才被视为合理推理步骤
1. [AUTORUBRIC-R1V: RUBRIC-BASED GENERATIVE REWARDS FOR FAITHFUL MULTIMODAL REASONING](https://arxiv.org/pdf/2510.14738)

### 在生成回答的时候就引入部分rubric
1. [Breaking the Exploration Bottleneck: Rubric-Scaffolded Reinforcement Learning for General LLM Reasoning](https://arxiv.org/pdf/2508.16949)

# 其他
1. [DeepTravel: An End-to-End Agentic Reinforcement Learning Framework for Autonomous Travel Planning Agents](https://arxiv.org/pdf/2509.21842) (Didi travel) interact with a sandbox (iclr:2448)
2. [Self-Rewarding Rubric-Based Reinforcement Learning for Open-Ended Reasoning](https://arxiv.org/pdf/2509.25534) (ant) rubric-based reward model (iclr:2446)
3. https://arxiv.org/pdf/2506.02355 (cmu) 提升grpo中概率低但是正确回答的reward


# My thoughts
Rubric生成与Rubric应用

生成方面分成hardcode和dynamic update

hardcode的问题是颗粒度不够细致，不能涵盖到各个方面，优势是简单易编写

dynamic update的问题是难以维护rule library，优势是能够根据不同的query来动态调整，更加适配

(UW and AI2)的有篇文章研究了rubric的更新方法，见[分析](https://chatgpt.com/share/6969d9df-a544-8006-bd23-54725663397f)

我的想法是是否需要看note来进行rubric的生成，以及供给侧的data所包含的多样性与模型真正认为的多样性也是有区别的

蒙特卡洛是生成多样性的一种方法，通过寻找同级节点或父子级节点来生成多样性

## Paper Reading

[ArenaRL: Scaling RL for Open-Ended Agents via Tournament-based Relative Ranking](https://arxiv.org/pdf/2601.06487v1) 

将传统的grpo的组内打分比较方式变成两两LLM-as-a-judge比较，通过使用种子轮，瑞士轮等排序方法探索低复杂度的拓扑排序方法，数据集是自建的

[Rubric-Based Benchmarking and Reinforcement Learning for Advancing LLM Instruction Following](https://arxiv.org/pdf/2511.10507v1) 

训练两个模型：Rubric Generator and Rubric Verifier. Rubric Generator用于自动生成训练数据中的指令对应的 rubrics，以便在大规模数据上生成训练奖励。先基于小规模专家数据训练一个生成器，然后应用到更大规模数据。


[OpenRubrics: Towards Scalable Synthetic Rubric Generation for Reward Modeling and LLM Alignment](https://arxiv.org/pdf/2510.07743) 

使用提示（Prompt + 优选回答 + 被拒回答）作为上下文，训练一个 Rubric 生成模型。把 Rubrics 分成Hard Rules和Principles，有些评价标准是必须被严格满足的，有些评价标准是只能被模糊地权衡的，但奖励模型不能用同一种语义地位去对待这两种东西。

[AUTO-RUBRIC: Learning to Extract Generalizable Criteria for Reward Modeling](https://arxiv.org/pdf/2510.17314)

<details>
<summary> method intro </summary>
1. Query-Specific Rubric Inference（查询特定准则提取）

对每一个偏好样本（query + 正回答 + 负回答）构造一个Propose–Evaluate–Revise 循环：

Propose（提出）：用一个生成模型生成初步的评价准则草案；

Evaluate（评估）：评估模型按这个准则是否能正确区分正/负回答；

Revise（修正）：如果评估失败，则用修订模型修正准则，并再次验证。

这个循环像是在围绕每个样本“反向推理出它内在的评判标准”。这样对每个偏好样本都能生成较高质量的“query-specific rubric”。

2. Query-Agnostic Rubric Aggregation（跨查询准则聚合）

把所有 query-specific 准则放在一起，因为它们可能重复、过于具体或互相冲突，需要精炼成一个更小的通用准则集。

这个阶段用一种**信息论驱动的最大化编码率（coding rate）**算法来选择一个紧凑集合，使最终的规则具有：

高覆盖度：能适用于不同查询；

低冗余性：避免重复或类似内容；

高信息量：最大化语义表达能力。

最终输出的结构化规则被称作 “Theme–Tips” 结构：高层 Theme（总体主题，如“逻辑性优先”） 下有具体 Tips（具体提示，如“确保回答因果关系清晰”）。</details>

[Reward and Guidance through Rubrics: Promoting Exploration to Improve Multi-Domain Reasoning](https://arxiv.org/pdf/2511.12344)

<details><summary>method intro</summary>
对于每一个训练迭代：
    1. 使用当前策略生成多个回答/推理轨迹
    2. 用 Rubric 评估这些轨迹（Factual + Process）
    3. 计算稠密奖励，更新策略参数（基于 GRPO）
    4. 离线收集高评分但未完美的轨迹
    5. 对这些轨迹进行分析生成指导信号
    6. 将指导信号用于离线策略 refinement
</details>

[Chasing the Tail: Effective Rubric-based Reward Modeling for Large Language Model Post-Training](https://arxiv.org/pdf/2509.21500) 
步骤 1 — Rubric 构造。选取一批离策略响应（高质量候选）。由 proposer LLM（例如 GPT-4.1）分析候选响应之间的差异。为每个候选对构建细粒度判别标准（rubric criterion），例如某一个输出是否包含一些核心要素。

步骤 2 — Rubric 细化（Iterative Refinement。通过迭代流程，从最好的响应候选开始，每轮：用当前 rubric 对候选集排序；选出当前评分最高的两个响应；再次提取更细粒度的标准，将其加入现有 rubric；持续迭代直到完成一个高判别能力的 rubric 集。

[Inference-Time Scaling for Generalist Reward Modeling](https://arxiv.org/pdf/2504.02495)

[RubricRL: Simple Generalizable Rewards for Text-to-Image Generation](https://arxiv.org/pdf/2511.20651) 这篇是图片生成的。给定输入提示词 Prompt p，RubricRL 使用一个 Rubric Generation Model（如 GPT-o4-mini） 自动生成一组细粒度评估标准（Rubrics）

[An Efficient Rubric-based Generative Verifier for Search-Augmented LLMs](https://arxiv.org/pdf/2510.14660) 