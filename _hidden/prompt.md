---
layout: page
title: "Prompt"
categories: [tool]
search_only: false
date: 2025-03-17 09:00:00 +0800
pinned: false
---

<div class="prompt-page">
  <div class="prompt-card">
    <div class="prompt-card-header">
      <div>
        <div class="prompt-card-title">GPT论文阅读模板</div>
      </div>
      <div class="prompt-actions">
        <button class="toggle-btn" onclick="toggleCode(this)">展开</button>
        <button class="copy-btn" onclick="copyCode(this)">复制</button>
      </div>
    </div>

    <pre id="prompt-pre" class="collapsed"><code id="paper-prompt-code">你是一名深度学习的研究者，需要你帮我辅助阅读论文。我会发送给你论文的pdf，需要你阅读论文并且输出总结。

在你输出的总结中，尽量以故事的结构来介绍这个工作。我说的故事结构是指，包含以下成分：

1. 研究背景：
论文的相关工作 or 研究背景是什么？这些领域是做什么的（简要概括就好）。

2. 问题（Challenge）：
论文要解决什么问题，它是什么意思？
这个问题为什么有挑战性？
这个问题难在哪里？
这个问题有什么价值？
为什么要解决它？
为什么某个目标很难达到？

Challenge 本身是一个因果性的表述，因为 XX，所以很难达到 XX 目标。
这里一般就是对于问题的分析，比如说这个事情内在有什么矛盾。

3. Finding：
作者的发现是什么？
作者的新观点是什么？
这个 finding 为什么能解决上面提到的问题？
请把其中的因果关系 or 逻辑关系说明白。

这里我要额外说明什么是 finding：
It is your key insight.
It is the insight that nobody had before.
It is the idea that takes a problem that could not be solved and turns it into one that can be solved.
The finding is how you see the world differently from everyone who has come before you.
It is what makes the unsolvable solvable.
The finding is not your technical contribution.
I repeat: it is not your technical contribution.
It is the insight that leads to your contribution.
If you can articulate your insight and share it with the reader, you have done most of your job.
The rest is details.
This finding connects to what people already knew and then flips it all around, creating a new opportunity.
It is about seeing the world differently.

4. 方法：
作者具体是怎么做的？
输入数据是什么？
先怎么做，然后又怎么做？
每个步骤干的是什么事情？

5. 结论：
论文的实验结果是什么？
作者通过实验得到了什么？
有什么要额外补充或者发现？

此外，请对必要的关键术语和概念进行总结并加以解释，格式是：
英文名称 + 中文翻译 + 解释，最好能举个例子。

中文输出就好，多举例子（尤其是实验中的 finding 和结论）。</code></pre>
  </div>
</div>

<style>
:root {
  --prompt-bg: linear-gradient(180deg, #fafafc 0%, #f4f7fb 100%);
  --prompt-card-bg: rgba(255, 255, 255, 0.88);
  --prompt-border: rgba(15, 23, 42, 0.08);
  --prompt-shadow: 0 10px 30px rgba(15, 23, 42, 0.08);
  --prompt-text: #0f172a;
  --prompt-subtext: #475569;
  --prompt-muted: #64748b;
  --prompt-accent: #2563eb;
  --prompt-accent-soft: rgba(37, 99, 235, 0.12);
  --prompt-code-bg: #0b1220;
  --prompt-code-text: #e2e8f0;
}

.prompt-page {
  padding: 24px 0 40px;
}

.prompt-card {
  border: 1px solid var(--prompt-border);
  border-radius: 24px;
  overflow: hidden;
  background: var(--prompt-card-bg);
  backdrop-filter: blur(10px);
  box-shadow: var(--prompt-shadow);
}

.prompt-card-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 16px;
  padding: 20px 20px 16px;
  border-bottom: 1px solid rgba(15, 23, 42, 0.06);
  background: linear-gradient(180deg, rgba(255,255,255,0.9) 0%, rgba(248,250,252,0.9) 100%);
}

.prompt-card-title {
  font-size: 1.05rem;
  font-weight: 700;
  color: var(--prompt-text);
}

.prompt-actions {
  display: flex;
  align-items: center;
  gap: 10px;
  flex-shrink: 0;
}

.copy-btn,
.toggle-btn {
  border: none;
  outline: none;
  color: white;
  padding: 10px 14px;
  border-radius: 12px;
  cursor: pointer;
  font-size: 13px;
  font-weight: 600;
  transition: transform 0.18s ease, box-shadow 0.18s ease, opacity 0.18s ease;
}

.copy-btn {
  background: linear-gradient(135deg, #2563eb 0%, #1d4ed8 100%);
  box-shadow: 0 8px 20px rgba(37, 99, 235, 0.24);
}

.toggle-btn {
  background: linear-gradient(135deg, #334155 0%, #1e293b 100%);
  box-shadow: 0 8px 20px rgba(30, 41, 59, 0.22);
}

.copy-btn:hover,
.toggle-btn:hover {
  transform: translateY(-1px);
  opacity: 0.96;
}

.copy-btn:active,
.toggle-btn:active {
  transform: translateY(0);
}

.prompt-card pre {
  margin: 0;
  padding: 22px;
  overflow-x: auto;
  background: var(--prompt-code-bg);
  transition: max-height 0.25s ease;
}

.prompt-card code {
  font-family: "SFMono-Regular", "Menlo", "Consolas", "Liberation Mono", monospace;
  font-size: 13.5px;
  line-height: 1.85;
  color: var(--prompt-code-text);
  white-space: pre-wrap;
  word-break: break-word;
  display: block;
}

/* 折叠后只保留前两行 */
.prompt-card pre.collapsed {
  overflow: hidden;
}

.prompt-card pre.collapsed code {
  display: -webkit-box;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
  overflow: hidden;
}

@media (max-width: 640px) {
  .prompt-card-header {
    flex-direction: column;
    align-items: flex-start;
  }

  .prompt-actions {
    width: 100%;
  }

  .copy-btn,
  .toggle-btn {
    flex: 1;
  }

  .prompt-card pre {
    padding: 18px;
  }
}
</style>

<script>
function copyCode(btn) {
  const code = document.getElementById("paper-prompt-code").innerText;
  navigator.clipboard.writeText(code).then(() => {
    const originalText = btn.innerText;
    btn.innerText = "已复制";
    btn.disabled = true;
    setTimeout(() => {
      btn.innerText = originalText;
      btn.disabled = false;
    }, 1500);
  });
}

function toggleCode(btn) {
  const pre = document.getElementById("prompt-pre");
  pre.classList.toggle("collapsed");
  btn.innerText = pre.classList.contains("collapsed") ? "展开" : "折叠";
}
</script>