---
layout: page
title: VLM-R1 异常检测相关文章
categories: [research, paper, 中文]
search_only: false
date: 2025-03-31 09:00:00 +0800
pinned: false
---

<style>
/* ── Page-level variables ── */
:root {
  --accent:   #5b8dee;
  --accent2:  #ee8b5b;
  --surface:  #f4f6fb;
  --border:   #dde3f0;
  --text-dim: #6b7a99;
  --radius:   10px;
}

/* ── Section cards ── */
.paper-section {
  background: var(--surface);
  border: 1px solid var(--border);
  border-left: 4px solid var(--accent);
  border-radius: var(--radius);
  padding: 1.4rem 1.6rem;
  margin: 1.6rem 0;
}
.paper-section.orange { border-left-color: var(--accent2); }
.paper-section h3 {
  margin-top: 0;
  font-size: 1.05rem;
  letter-spacing: .02em;
}

/* ── Paper entry rows ── */
.paper-entry {
  display: flex;
  align-items: flex-start;
  gap: .7rem;
  padding: .55rem 0;
  border-bottom: 1px dashed var(--border);
}
.paper-entry:last-child { border-bottom: none; }
.paper-badge {
  display: inline-block;
  font-size: .68rem;
  font-weight: 700;
  letter-spacing: .06em;
  text-transform: uppercase;
  padding: .18em .55em;
  border-radius: 4px;
  white-space: nowrap;
  margin-top: .15rem;
  flex-shrink: 0;
}
.badge-cvpr  { background:#dbeafe; color:#1d4ed8; }
.badge-iccv  { background:#fce7f3; color:#be185d; }
.badge-aaai  { background:#dcfce7; color:#15803d; }
.badge-eccv  { background:#fef9c3; color:#a16207; }
.badge-arxiv { background:#f3e8ff; color:#7e22ce; }
.badge-misc  { background:#f1f5f9; color:#475569; }

.paper-info { flex: 1; line-height: 1.45; }
.paper-title { font-weight: 600; font-size: .93rem; }
.paper-desc  { font-size: .83rem; color: var(--text-dim); margin-top: .18rem; }

/* ── Dataset grid ── */
.dataset-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
  gap: .9rem;
  margin-top: .8rem;
}
.dataset-card {
  background: #fff;
  border: 1px solid var(--border);
  border-radius: var(--radius);
  padding: .8rem 1rem;
  font-size: .85rem;
}
.dataset-card strong { display: block; margin-bottom: .25rem; font-size: .9rem; }
.dataset-card a { color: var(--accent); text-decoration: none; font-size: .78rem; word-break: break-all; }
.dataset-card a:hover { text-decoration: underline; }

/* ── Table of Contents ── */
.toc {
  background: #fff;
  border: 1px solid var(--border);
  border-radius: var(--radius);
  padding: 1rem 1.4rem;
  display: inline-block;
  margin-bottom: 1.6rem;
  font-size: .88rem;
  min-width: 260px;
}
.toc-title { font-weight: 700; margin-bottom: .5rem; color: var(--text-dim); font-size: .78rem; letter-spacing: .1em; text-transform: uppercase; }
.toc ol { margin: 0; padding-left: 1.2rem; }
.toc li { margin: .3rem 0; }
.toc a  { color: var(--accent); text-decoration: none; }
.toc a:hover { text-decoration: underline; }
</style>

> 整理了**异常检测**与 **Vision-Language Reasoning (VLM-R1)** 两条研究脉络下的核心论文，截止2026年3月。

<div class="toc">
  <div class="toc-title">📑 目录</div>
  <ol>
    <li><a href="#anomaly-detection">Anomaly Detection</a>
      <ol>
        <li><a href="#early-dl">早期深度学习方法</a></li>
        <li><a href="#vlm-llm">Foundation Model / VLM / LLM</a></li>
        <li><a href="#datasets">数据集</a></li>
      </ol>
    </li>
    <li><a href="#vision-r1">Vision R1 推理应用</a>
      <ol>
        <li><a href="#applications">多领域应用</a></li>
        <li><a href="#orm">ORM 结果监督</a></li>
        <li><a href="#prm">PRM 过程监督</a></li>
        <li><a href="#survey">综述</a></li>
      </ol>
    </li>
  </ol>
</div>

---

## 🔍 Anomaly Detection {#anomaly-detection}

### 早期深度学习方法 {#early-dl}

> 从依赖手工特征（光流、稀疏编码、背景减除）逐步演进到基于深度重建与预测的范式。

<div class="paper-section">

<div class="paper-entry">
  <span class="paper-badge badge-cvpr">CVPR 18</span>
  <div class="paper-info">
    <div class="paper-title"><a href="https://openaccess.thecvf.com/content_cvpr_2018/html/Liu_Future_Frame_Prediction_CVPR_2018_paper.html">Future Frame Prediction for Anomaly Detection</a></div>
    <div class="paper-desc">基于未来帧预测的深度重建框架，以重建误差判断异常</div>
  </div>
</div>

<div class="paper-entry">
  <span class="paper-badge badge-iccv">ICCV 19</span>
  <div class="paper-info">
    <div class="paper-title"><a href="https://openaccess.thecvf.com/content_ICCV_2019/html/Gong_Memorizing_Normality_to_Detect_Anomaly_Memory-Augmented_Deep_Autoencoder_for_Unsupervised_ICCV_2019_paper.html">Memorizing Normality to Detect Anomaly</a></div>
    <div class="paper-desc">记忆增强深度自编码器，存储正常模式原型以无监督检测异常</div>
  </div>
</div>

<div class="paper-entry">
  <span class="paper-badge badge-cvpr">CVPR 18</span>
  <div class="paper-info">
    <div class="paper-title"><a href="https://openaccess.thecvf.com/content_cvpr_2018/html/Sultani_Real-World_Anomaly_Detection_CVPR_2018_paper.html">Real-World Anomaly Detection in Surveillance Videos</a></div>
    <div class="paper-desc">提出深度 MIL 排序损失函数，奠定弱监督视频异常检测基础，并发布 UCF-Crime 数据集</div>
  </div>
</div>

<div class="paper-entry">
  <span class="paper-badge badge-cvpr">CVPR 21</span>
  <div class="paper-info">
    <div class="paper-title"><a href="https://openaccess.thecvf.com/content/CVPR2021/html/Feng_MIST_Multiple_Instance_Self-Training_Framework_for_Video_Anomaly_Detection_CVPR_2021_paper.html">MIST: Multiple Instance Self-Training Framework</a></div>
    <div class="paper-desc">自训练编码器迭代细化伪标签，减少对精确标注的依赖</div>
  </div>
</div>

<div class="paper-entry">
  <span class="paper-badge badge-iccv">ICCV 21</span>
  <div class="paper-info">
    <div class="paper-title"><a href="https://openaccess.thecvf.com/content/ICCV2021/html/Tian_Weakly-Supervised_Video_Anomaly_Detection_With_Robust_Temporal_Feature_Magnitude_Learning_ICCV_2021_paper.html">RTFM: Robust Temporal Feature Magnitude Learning</a></div>
    <div class="paper-desc">选取前 k 个高幅度片段进行监督，提升弱监督信号的利用效率</div>
  </div>
</div>

<div class="paper-entry">
  <span class="paper-badge badge-aaai">AAAI 23</span>
  <div class="paper-info">
    <div class="paper-title"><a href="https://ojs.aaai.org/index.php/AAAI/article/view/25112">MGFN: Magnitude-Contrastive Glance-and-Focus Network</a></div>
    <div class="paper-desc">引入带幅度对比损失的「注视与聚焦」注意力模块，强化局部异常感知</div>
  </div>
</div>

</div>

---

### Foundation Model / VLM / LLM 方法 {#vlm-llm}

> 借助预训练大模型的强泛化能力，探索零样本、少样本及开放词汇的异常检测新范式。

<div class="paper-section orange">

<div class="paper-entry">
  <span class="paper-badge badge-aaai">AAAI 24</span>
  <div class="paper-info">
    <div class="paper-title"><a href="https://ojs.aaai.org/index.php/AAAI/article/view/27963">AnomalyGPT</a></div>
    <div class="paper-desc">在模拟异常数据上微调大型视觉语言模型，实现工业图像异常理解</div>
  </div>
</div>

<div class="paper-entry">
  <span class="paper-badge badge-arxiv">arXiv</span>
  <div class="paper-info">
    <div class="paper-title"><a href="https://arxiv.org/abs/2310.18961">AnomalyCLIP</a></div>
    <div class="paper-desc">学习与对象无关的提示，捕捉通用正常/异常状态，突破类别限制</div>
  </div>
</div>

<div class="paper-entry">
  <span class="paper-badge badge-cvpr">CVPR 23</span>
  <div class="paper-info">
    <div class="paper-title"><a href="https://openaccess.thecvf.com/content/CVPR2023/html/Jeong_WinCLIP_Zero-Few-Shot_Anomaly_Classification_and_Segmentation_CVPR_2023_paper.html">WinCLIP</a></div>
    <div class="paper-desc">滑动窗口 + 手动文本提示，实现工业场景零样本 / 少样本异常分类与分割</div>
  </div>
</div>

<div class="paper-entry">
  <span class="paper-badge badge-eccv">ECCV 24</span>
  <div class="paper-info">
    <div class="paper-title"><a href="https://link.springer.com/chapter/10.1007/978-3-031-72890-7_18">VCP-CLIP</a></div>
    <div class="paper-desc">视觉上下文提示 CLIP，增强零样本工业异常检测能力</div>
  </div>
</div>

<div class="paper-entry">
  <span class="paper-badge badge-cvpr">CVPR 24</span>
  <div class="paper-info">
    <div class="paper-title"><a href="https://openaccess.thecvf.com/content/CVPR2024/html/Zanella_Harnessing_Large_Language_Models_for_Training-free_Video_Anomaly_Detection_CVPR_2024_paper.html">LAVAD</a></div>
    <div class="paper-desc">VLM 生成帧描述 + LLM 时序聚合与异常评分，无需训练即可检测视频异常</div>
  </div>
</div>

<div class="paper-entry">
  <span class="paper-badge badge-cvpr">CVPR 24</span>
  <div class="paper-info">
    <div class="paper-title"><a href="https://openaccess.thecvf.com/content/CVPR2024/html/Wu_Open-Vocabulary_Video_Anomaly_Detection_CVPR_2024_paper.html">Open-Vocabulary VAD</a></div>
    <div class="paper-desc">基于 CLIP 的伪新异常合成，支持检测和分类从未见过的异常类型</div>
  </div>
</div>

<div class="paper-entry">
  <span class="paper-badge badge-cvpr">CVPR 24</span>
  <div class="paper-info">
    <div class="paper-title"><a href="https://openaccess.thecvf.com/content/CVPR2024/html/Yang_Text_Prompt_with_Normality_Guidance_for_Weakly_Supervised_Video_Anomaly_CVPR_2024_paper.html">TPWNG</a></div>
    <div class="paper-desc">可学习文本提示 + 正常视觉提示微调 CLIP，引导弱监督异常检测</div>
  </div>
</div>

<div class="paper-entry">
  <span class="paper-badge badge-eccv">ECCV 24</span>
  <div class="paper-info">
    <div class="paper-title"><a href="https://link.springer.com/chapter/10.1007/978-3-031-73004-7_18">AnomalyRuler</a></div>
    <div class="paper-desc">归纳-演绎推理框架：LLM 从少量正常样本中归纳正常性规则，再演绎标记异常帧</div>
  </div>
</div>

</div>

---

### 数据集 {#datasets}

<div class="dataset-grid">

<div class="dataset-card">
  <strong>🎬 UCF-Crime</strong>
  真实监控视频，13 类犯罪事件，128h+
  <br><a href="https://openaccess.thecvf.com/content_cvpr_2018/html/Sultani_Real-World_Anomaly_Detection_CVPR_2018_paper.html">论文 (CVPR 18) →</a>
</div>

<div class="dataset-card">
  <strong>💥 XD-Violence</strong>
  多场景暴力检测，含音频模态
  <br><a href="https://link.springer.com/chapter/10.1007/978-3-030-58577-8_20">论文 (ECCV 20) →</a>
</div>

<div class="dataset-card">
  <strong>🏙️ MSAD</strong>
  多场景异常检测基准
  <br><a href="https://msad-dataset.github.io/">主页 →</a>
</div>

<div class="dataset-card">
  <strong>🎥 ECVA</strong>
  基于事件摄像机的视频异常数据集
  <br><a href="https://github.com/Dulpy/ECVA">GitHub →</a>
</div>

<div class="dataset-card">
  <strong>🚦 TAD</strong>
  交通场景异常检测数据集
  <br><a href="https://github.com/ktr-hubrt/WSAL">GitHub →</a>
</div>

</div>

---

## 🧠 Vision R1 推理应用 {#vision-r1}

### 多领域应用 {#applications}

> VLM-R1 范式（强化学习驱动的视觉推理）已在多个垂直方向取得突破。

<div class="paper-section">

<div class="paper-entry">
  <span class="paper-badge badge-misc">医疗</span>
  <div class="paper-info">
    <div class="paper-title"><a href="https://link.springer.com/chapter/10.1007/978-3-032-04981-0_32">MedVLM-R1</a></div>
    <div class="paper-desc">医疗影像多模态推理，提升诊断可解释性</div>
  </div>
</div>

<div class="paper-entry">
  <span class="paper-badge badge-arxiv">arXiv</span>
  <div class="paper-info">
    <div class="paper-title"><a href="https://arxiv.org/abs/2503.07365">MM-Eureka</a></div>
    <div class="paper-desc">多模态数学推理，强化学习驱动的符号与视觉融合</div>
  </div>
</div>

<div class="paper-entry">
  <span class="paper-badge badge-arxiv">arXiv</span>
  <div class="paper-info">
    <div class="paper-title"><a href="https://arxiv.org/abs/2509.25026">GeoVLM-R1</a></div>
    <div class="paper-desc">遥感 / 地球观测方向的视觉推理</div>
  </div>
</div>

<div class="paper-entry">
  <span class="paper-badge badge-arxiv">arXiv</span>
  <div class="paper-info">
    <div class="paper-title"><a href="https://arxiv.org/abs/2603.06958">Chart-RL</a></div>
    <div class="paper-desc">图表理解方向，强化学习增强图表问答与解析</div>
  </div>
</div>

<div class="paper-entry">
  <span class="paper-badge badge-aaai">AAAI</span>
  <div class="paper-info">
    <div class="paper-title"><a href="https://ojs.aaai.org/index.php/AAAI/article/view/37602">Drive-R1</a></div>
    <div class="paper-desc">自动驾驶方向，强化学习赋能端到端驾驶决策推理</div>
  </div>
</div>

<div class="paper-entry">
  <span class="paper-badge badge-arxiv">arXiv</span>
  <div class="paper-info">
    <div class="paper-title"><a href="https://arxiv.org/abs/2505.23504">VAU-R1</a></div>
    <div class="paper-desc">视频异常理解（安防 / 城市安全），推理链驱动的异常定位与解释</div>
  </div>
</div>

<div class="paper-entry">
  <span class="paper-badge badge-arxiv">arXiv</span>
  <div class="paper-info">
    <div class="paper-title"><a href="https://arxiv.org/abs/2401.05702">VAD-LLaMA</a></div>
    <div class="paper-desc">基于大语言模型的视频异常检测与自然语言解释生成</div>
  </div>
</div>

<div class="paper-entry">
  <span class="paper-badge badge-arxiv">arXiv</span>
  <div class="paper-info">
    <div class="paper-title"><a href="https://arxiv.org/pdf/2508.04175">AD-FM</a></div>
    <div class="paper-desc">异常检测基础模型，探索统一的跨域异常检测框架</div>
  </div>
</div>

</div>

---

### ORM 结果监督 {#orm}

<div class="paper-section">

<div class="paper-entry">
  <span class="paper-badge badge-arxiv">arXiv 25</span>
  <div class="paper-info">
    <div class="paper-title"><a href="https://arxiv.org/abs/2501.12948">DeepSeek-R1</a></div>
    <div class="paper-desc">通过强化学习（GRPO）激发 LLM 推理能力，ORM 结果监督的里程碑工作</div>
  </div>
</div>

<div class="paper-entry">
  <span class="paper-badge badge-arxiv">arXiv 24</span>
  <div class="paper-info">
    <div class="paper-title"><a href="https://arxiv.org/abs/2402.03300">DeepSeekMath</a></div>
    <div class="paper-desc">数学推理专项强化学习，验证 ORM 在数学领域的有效性</div>
  </div>
</div>

</div>

---

### PRM 过程监督 {#prm}

<div class="paper-section orange">

<div class="paper-entry">
  <span class="paper-badge badge-arxiv">arXiv 25</span>
  <div class="paper-info">
    <div class="paper-title"><a href="https://arxiv.org/abs/2503.11926">Monitoring Reasoning Models for Misbehavior</a></div>
    <div class="paper-desc">分析推理模型行为监控与混淆规避的风险，PRM 过程监督安全研究</div>
  </div>
</div>

<div class="paper-entry">
  <span class="paper-badge badge-arxiv">arXiv 25</span>
  <div class="paper-info">
    <div class="paper-title"><a href="https://arxiv.org/abs/2503.20752">Reason-RFT</a></div>
    <div class="paper-desc">推理驱动的强化微调，过程奖励引导多步视觉推理</div>
  </div>
</div>

<div class="paper-entry">
  <span class="paper-badge badge-misc">IJRR</span>
  <div class="paper-info">
    <div class="paper-title"><a href="https://journals.sagepub.com/doi/abs/10.1177/0278364919887447">Learning Dexterous In-Hand Manipulation</a></div>
    <div class="paper-desc">灵巧手操作强化学习，过程监督在物理机器人中的早期探索</div>
  </div>
</div>

</div>

---

### 综述 {#survey}

<div class="paper-section">

<div class="paper-entry">
  <span class="paper-badge badge-arxiv">arXiv 25</span>
  <div class="paper-info">
    <div class="paper-title"><a href="https://arxiv.org/pdf/2504.21277v1">Reinforced MLLM: A Survey on RL-Based Reasoning in Multimodal LLMs</a></div>
    <div class="paper-desc">系统综述多模态大模型中基于强化学习的推理方法，覆盖算法、数据与评估</div>
  </div>
</div>

<div class="paper-entry">
  <span class="paper-badge badge-arxiv">arXiv 25</span>
  <div class="paper-info">
    <div class="paper-title"><a href="https://arxiv.org/pdf/2509.19012v1">Pure Vision Language Action (VLA) Models: A Comprehensive Survey</a></div>
    <div class="paper-desc">纯视觉语言动作模型全面综述，梳理从感知到决策的端到端架构演进</div>
  </div>
</div>

</div>

---

<p style="font-size:.8rem; color:#9aa3b8; text-align:center; margin-top:2rem;">
  最后更新：2025-03-31 &nbsp;·&nbsp; 如有遗漏欢迎 PR / Issue 补充
</p>