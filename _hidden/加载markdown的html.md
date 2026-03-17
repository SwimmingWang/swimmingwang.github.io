---
layout: page
title: "加载Markdown的HTML.md"
categories: [tool, code, 中文]
search_only: false
date: 2025-03-17 09:00:00 +0800
# external_embed: ""
# external_link: ""
# external_label: "测试引入谷歌文档"
---

用于加载统计文件下的markdown文件作为html可视化展示的代码。

<div class="html-playground">
  <div class="hp-toolbar">
    <div class="hp-title">HTML 代码预览</div>
    <div class="hp-actions">
      <button class="hp-btn" id="copyBtn">复制代码</button>
      <button class="hp-btn" id="runBtn">刷新预览</button>
    </div>
  </div>

  <div class="hp-grid">
    <div class="hp-panel">
      <div class="hp-panel-title">代码</div>
      <textarea id="codeInput" spellcheck="false">
<!doctype html>
<html lang="zh-CN">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Markdown Viewer</title>
  <style>
    :root{
      --bg: #0b1020;
      --panel: rgba(255,255,255,0.06);
      --border: rgba(255,255,255,0.10);
      --text: rgba(255,255,255,0.92);
      --muted: rgba(255,255,255,0.65);
      --shadow: 0 14px 40px rgba(0,0,0,0.45);
      --radius: 16px;
      --maxw: 980px;
      --mono: ui-monospace, SFMono-Regular, Menlo, Monaco, Consolas, "Liberation Mono", "Courier New", monospace;
      --sans: ui-sans-serif, system-ui, -apple-system, Segoe UI, Roboto, Helvetica, Arial, "Apple Color Emoji","Segoe UI Emoji";
    }

    body{
      margin:0;
      font-family: var(--sans);
      background: radial-gradient(1200px 800px at 10% 10%, rgba(124,58,237,0.18), transparent 60%),
                  radial-gradient(1000px 700px at 90% 30%, rgba(34,197,94,0.14), transparent 55%),
                  linear-gradient(180deg, #060815, var(--bg));
      color: var(--text);
      min-height: 100vh;
    }

    .wrap{
      max-width: var(--maxw);
      margin: 24px auto 64px;
      padding: 0 16px;
    }

    .topbar{
      display:flex;
      gap: 12px;
      align-items:center;
      justify-content:space-between;
      background: var(--panel);
      border: 1px solid var(--border);
      border-radius: var(--radius);
      padding: 14px 14px;
      box-shadow: var(--shadow);
      backdrop-filter: blur(10px);
    }

    .left{
      display:flex;
      align-items:center;
      gap: 10px;
      min-width: 0;
    }

    .badge{
      width: 10px;
      height: 10px;
      border-radius: 999px;
      background: rgba(124,58,237,0.95);
      box-shadow: 0 0 0 4px rgba(124,58,237,0.18);
      flex: 0 0 auto;
    }

    .title{
      font-size: 14px;
      font-weight: 650;
      letter-spacing: 0.2px;
      white-space: nowrap;
      overflow:hidden;
      text-overflow: ellipsis;
      max-width: 520px;
    }

    .controls{
      display:flex;
      align-items:center;
      gap: 10px;
      flex: 0 0 auto;
    }

    input[type="text"]{
      width: 260px;
      max-width: 40vw;
      padding: 9px 10px;
      border-radius: 12px;
      border: 1px solid var(--border);
      background: rgba(255,255,255,0.05);
      color: var(--text);
      outline: none;
    }
    input[type="text"]::placeholder{ color: rgba(255,255,255,0.45); }

    button{
      padding: 9px 12px;
      border-radius: 12px;
      border: 1px solid var(--border);
      background: rgba(255,255,255,0.07);
      color: var(--text);
      cursor: pointer;
    }
    button:hover{ background: rgba(255,255,255,0.10); }

    .panel{
      margin-top: 16px;
      background: var(--panel);
      border: 1px solid var(--border);
      border-radius: var(--radius);
      padding: 22px 22px;
      box-shadow: var(--shadow);
      backdrop-filter: blur(10px);
    }

    .hint{
      margin: 0 0 14px 0;
      color: var(--muted);
      font-size: 13px;
      line-height: 1.5;
    }

    /* Markdown 渲染的基础排版（由 marked 输出的 HTML 直接套用） */
    .md h1,.md h2,.md h3{ margin: 20px 0 10px; line-height:1.2; }
    .md h1{ font-size: 28px; }
    .md h2{ font-size: 22px; }
    .md h3{ font-size: 18px; color: rgba(255,255,255,0.88); }
    .md p{ line-height: 1.75; margin: 10px 0; color: rgba(255,255,255,0.88); }
    .md a{ color: rgba(124,58,237,0.95); text-decoration: none; }
    .md a:hover{ text-decoration: underline; }
    .md hr{ border: none; border-top: 1px solid rgba(255,255,255,0.12); margin: 18px 0; }
    .md blockquote{
      margin: 12px 0;
      padding: 10px 12px;
      border-left: 3px solid rgba(124,58,237,0.85);
      background: rgba(124,58,237,0.08);
      border-radius: 10px;
      color: rgba(255,255,255,0.86);
    }
    .md code{
      font-family: var(--mono);
      font-size: 0.95em;
      padding: 0.1em 0.35em;
      border-radius: 8px;
      background: rgba(255,255,255,0.08);
      border: 1px solid rgba(255,255,255,0.10);
    }
    .md pre{
      overflow:auto;
      padding: 14px 14px;
      border-radius: 14px;
      background: rgba(0,0,0,0.35);
      border: 1px solid rgba(255,255,255,0.10);
    }
    .md pre code{
      padding: 0;
      border: none;
      background: transparent;
      font-size: 13px;
      line-height: 1.6;
    }
    .md ul,.md ol{ margin: 10px 0 10px 22px; line-height:1.7; }
    .md table{
      width: 100%;
      border-collapse: collapse;
      margin: 14px 0;
      overflow: hidden;
      border-radius: 12px;
      border: 1px solid rgba(255,255,255,0.10);
    }
    .md th,.md td{
      border-bottom: 1px solid rgba(255,255,255,0.10);
      padding: 10px 10px;
      text-align: left;
      vertical-align: top;
    }
    .md th{
      background: rgba(255,255,255,0.06);
      font-weight: 650;
    }

    .error{
      white-space: pre-wrap;
      color: rgba(255,180,180,0.95);
      background: rgba(239,68,68,0.10);
      border: 1px solid rgba(239,68,68,0.25);
      padding: 12px 12px;
      border-radius: 12px;
      font-family: var(--mono);
      font-size: 12px;
      line-height: 1.55;
    }
  </style>
</head>
<body>
  <div class="wrap">
    <div class="topbar">
      <div class="left">
        <div class="badge"></div>
        <div class="title" id="title">Markdown Viewer</div>
      </div>
      <div class="controls">
        <input id="mdPath" type="text" value="README.md" placeholder="例如：worklog.md" />
        <button id="loadBtn">加载</button>
      </div>
    </div>

    <div class="panel">
      <p class="hint" id="hint">
        <span id="pathText" style="font-family: var(--mono);"></span><br/>
      </p>
      <div id="content" class="md"></div>
    </div>
  </div>

  <!-- marked: Markdown -> HTML（CDN 方式引入） -->
  <script src="https://cdn.jsdelivr.net/npm/marked/marked.min.js"></script>

  <script>
    const mdPathInput = document.getElementById('mdPath');
    const loadBtn = document.getElementById('loadBtn');
    const content = document.getElementById('content');
    const title = document.getElementById('title');
    const pathText = document.getElementById('pathText');

    function escapeHtml(s){
      return s.replace(/[&<>"']/g, (c) => ({
        "&":"&amp;","<":"&lt;",">":"&gt;","\"":"&quot;","'":"&#039;"
      }[c]));
    }

    async function loadMarkdown(path){
      pathText.textContent = path;
      title.textContent = `Markdown Viewer — ${path}`;
      content.innerHTML = '';

      try{
        const res = await fetch(path, { cache: "no-store" });
        if(!res.ok){
          throw new Error(`HTTP ${res.status} ${res.statusText}\n无法加载：${path}`);
        }
        const md = await res.text();
        // 渲染
        const html = marked.parse(md, {
          gfm: true,
          breaks: false
        });
        content.innerHTML = html;
      }catch(err){
        content.innerHTML =
          `<div class="error">加载失败：\n${escapeHtml(String(err))}\n\n常见原因：\n1) 直接用 file:// 打开导致 fetch 被拦截\n2) Markdown 文件路径/文件名不对\n3) 服务器未启动或跨域限制</div>`;
      }
    }

    loadBtn.addEventListener('click', () => {
      const path = mdPathInput.value.trim() || 'README.md';
      loadMarkdown(path);
    });

    mdPathInput.addEventListener('keydown', (e) => {
      if(e.key === 'Enter'){
        const path = mdPathInput.value.trim() || 'README.md';
        loadMarkdown(path);
      }
    });

    // 初次加载
    loadMarkdown(mdPathInput.value.trim() || 'README.md');
  </script>
</body>
</html>

      </textarea>
    </div>

    <div class="hp-panel">
      <div class="hp-panel-title">预览</div>
      <iframe id="previewFrame" class="hp-preview"></iframe>
    </div>
  </div>

  <div id="copyMsg" class="hp-copy-msg"></div>
</div>

<style>
  .html-playground{
    margin: 24px 0;
    border: 1px solid #e5e7eb;
    border-radius: 18px;
    overflow: hidden;
    background: #fff;
    box-shadow: 0 12px 32px rgba(0,0,0,0.06);
  }

  .hp-toolbar{
    display:flex;
    align-items:center;
    justify-content:space-between;
    gap:12px;
    padding:14px 16px;
    border-bottom:1px solid #e5e7eb;
    background:#f9fafb;
  }

  .hp-title{
    font-size:15px;
    font-weight:700;
    color:#111827;
  }

  .hp-actions{
    display:flex;
    gap:10px;
  }

  .hp-btn{
    border:none;
    background:#111827;
    color:white;
    padding:8px 12px;
    border-radius:10px;
    cursor:pointer;
    font-size:14px;
  }

  .hp-btn:hover{
    opacity:.9;
  }

  .hp-grid{
    display:grid;
    grid-template-columns: 1fr 1fr;
  }

  .hp-panel{
    min-width:0;
    border-right:1px solid #e5e7eb;
  }

  .hp-panel:last-child{
    border-right:none;
  }

  .hp-panel-title{
    padding:12px 16px;
    font-size:13px;
    font-weight:600;
    color:#6b7280;
    border-bottom:1px solid #e5e7eb;
    background:#fcfcfd;
  }

  #codeInput{
    width:100%;
    min-height:520px;
    border:none;
    outline:none;
    resize:vertical;
    padding:16px;
    font: 13px/1.65 ui-monospace, SFMono-Regular, Menlo, Monaco, Consolas, monospace;
    color:#111827;
    background:#ffffff;
    box-sizing:border-box;
  }

  .hp-preview{
    width:100%;
    min-height:520px;
    border:none;
    background:white;
    display:block;
  }

  .hp-copy-msg{
    padding:10px 16px 14px;
    font-size:13px;
    color:#16a34a;
  }

  @media (max-width: 900px){
    .hp-grid{
      grid-template-columns: 1fr;
    }
    .hp-panel{
      border-right:none;
      border-bottom:1px solid #e5e7eb;
    }
    .hp-panel:last-child{
      border-bottom:none;
    }
  }
</style>

<script>
  (function(){
    const codeInput = document.getElementById('codeInput');
    const previewFrame = document.getElementById('previewFrame');
    const copyBtn = document.getElementById('copyBtn');
    const runBtn = document.getElementById('runBtn');
    const copyMsg = document.getElementById('copyMsg');

    function renderPreview() {
      const html = codeInput.value;
      previewFrame.srcdoc = html;
    }

    async function copyCode() {
      try {
        await navigator.clipboard.writeText(codeInput.value);
        copyMsg.textContent = '已复制到剪贴板。';
        setTimeout(() => copyMsg.textContent = '', 1800);
      } catch (e) {
        copyMsg.textContent = '复制失败，请手动选择代码复制。';
        setTimeout(() => copyMsg.textContent = '', 1800);
      }
    }

    copyBtn.addEventListener('click', copyCode);
    runBtn.addEventListener('click', renderPreview);

    codeInput.addEventListener('input', renderPreview);

    renderPreview();
  })();
</script>