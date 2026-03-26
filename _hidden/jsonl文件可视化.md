---
layout: page
title: "加载jsonl的HTML.md"
categories: [tool, code, 中文]
search_only: false
date: 2025-03-19 09:00:00 +0800
pinned: false
# external_embed: ""
# external_link: ""
# external_label: "测试引入谷歌文档"
---

用于加载统计文件下的jsonl文件作为html可视化展示的代码。

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

<!DOCTYPE html>
<html lang="zh-CN">
<head>
  <meta charset="UTF-8" />
  <title>JSONL Viewer</title>
  <style>
    body { font-family: system-ui, -apple-system, BlinkMacSystemFont; margin: 20px; background: #fafafa; }
    h1 { font-size: 18px; margin: 0 0 12px; }
    .row { display: flex; gap: 12px; align-items: center; flex-wrap: wrap; margin-bottom: 12px; }
    input[type="text"] { padding: 6px 8px; width: 360px; max-width: 90vw; }
    button { padding: 6px 10px; cursor: pointer; }
    .hint { color: #666; font-size: 13px; margin: 6px 0 14px; }
    .error { color: #b00020; font-size: 13px; }

    .table-wrapper { overflow-x: auto; }
    table { border-collapse: collapse; width: max-content; min-width: 100%; background: #fff; table-layout: fixed; }
    th, td { border: 1px solid #ddd; padding: 0; font-size: 13px; text-align: left; vertical-align: top; overflow: hidden; }
    th { background: #f0f0f0; white-space: nowrap; user-select: none; position: relative; padding: 8px; }
    tr:nth-child(even) td { background: #fafafa; }

    td.idx-cell, th.idx-cell {
      width: 36px; min-width: 36px; max-width: 36px;
      text-align: center;
      background: #f0f0f0 !important;
      position: sticky; left: 0; z-index: 1;
      border-right: 2px solid #ccc;
      font-size: 11px; color: #888;
      padding: 6px 4px;
    }

    /* 单元格内层：overflow-y: auto 实现纵向滚动 */
    .cell-inner {
      padding: 8px;
      overflow-y: auto;
      overflow-x: hidden;
      box-sizing: border-box;
      height: 100%;
      /* 细滚动条样式 */
      scrollbar-width: thin;
      scrollbar-color: #ccc transparent;
    }
    .cell-inner::-webkit-scrollbar { width: 6px; }
    .cell-inner::-webkit-scrollbar-thumb { background: #ccc; border-radius: 3px; }
    .cell-inner::-webkit-scrollbar-thumb:hover { background: #aaa; }
    .cell-inner::-webkit-scrollbar-track { background: transparent; }

    pre {
      margin: 0;
      white-space: pre-wrap;
      word-break: break-word;
      font-family: inherit;
    }

    tr.resize-row td {
      padding: 0; height: 5px;
      background: transparent;
      border-top: none; border-bottom: 1px solid #ddd;
      cursor: row-resize; user-select: none;
    }
    tr.resize-row:hover td,
    tr.resize-row.resizing td { background: #b0c4de; }

    .ctrl-bar { margin-bottom: 10px; display: flex; gap: 8px; align-items: center; flex-wrap: wrap; }
    .ctrl-bar label { font-size: 13px; color: #555; }
    .ctrl-bar input[type=number] { width: 60px; padding: 3px 6px; font-size: 12px; }
    .ctrl-bar span.tip { font-size: 12px; color: #999; }

    .col-resizer {
      position: absolute; right: 0; top: 0;
      height: 100%; width: 5px;
      cursor: col-resize; user-select: none; z-index: 3;
    }
    .col-resizer:hover, .col-resizer.resizing { background: #888; }
  </style>
</head>
<body>

<h1>JSONL 文件展示器</h1>

<div class="row">
  <label>JSONL 文件名（同级）：</label>
  <input id="jsonlName" type="text" value="output.jsonl" />
  <button id="btnLoad">加载</button>
  <span style="width:12px;"></span>
  <label>或者：本地选择文件</label>
  <input type="file" id="fileInput" accept=".jsonl" />
</div>

<div class="hint">注意：请用本地静态服务器打开本页面（不要用 file:// 直接打开），否则 fetch 读取本地 jsonl 可能被浏览器拦截。</div>

<div id="status" class="error"></div>

<div class="ctrl-bar" id="ctrlBar" style="display:none;">
  <label>默认行高：</label>
  <input type="number" id="defaultHeight" value="60" min="20" max="800" step="4" />
  <span class="tip">px &nbsp;|&nbsp; 拖动行底部蓝条调整行高 &nbsp;|&nbsp; 单元格内容超出时可滚动</span>
  <button id="btnResetAll">重置所有行高</button>
</div>

<div class="table-wrapper">
  <table id="table">
    <thead id="thead"></thead>
    <tbody id="tbody"></tbody>
  </table>
</div>

<script>
  const DEFAULT_COL_WIDTH = 180;
  let currentDefaultHeight = 60;
  const rowHeights = [];

  function parseJsonl(text) {
    return text.split(/\r?\n/).filter(l => l.trim()).map(line => {
      try { return JSON.parse(line); }
      catch { return { __parse_error__: line }; }
    });
  }

  function makeColResizer(th) {
    const r = document.createElement("div");
    r.className = "col-resizer";
    th.appendChild(r);
    let startX, startW;
    r.addEventListener("mousedown", e => {
      startX = e.pageX; startW = th.offsetWidth;
      r.classList.add("resizing");
      const onMove = e => {
        const w = Math.max(40, startW + (e.pageX - startX));
        th.style.width = w + "px"; th.style.minWidth = w + "px";
      };
      const onUp = () => {
        r.classList.remove("resizing");
        document.removeEventListener("mousemove", onMove);
        document.removeEventListener("mouseup", onUp);
      };
      document.addEventListener("mousemove", onMove);
      document.addEventListener("mouseup", onUp);
      e.preventDefault();
    });
  }

  function applyRowHeight(dataTr, h) {
    dataTr.style.height = h + "px";
    dataTr.querySelectorAll(".cell-inner").forEach(el => {
      el.style.height = h + "px";
      el.style.maxHeight = h + "px";
    });
  }

  function makeRowResizer(resizeTr, dataTr, rowIdx) {
    resizeTr.addEventListener("mousedown", e => {
      resizeTr.classList.add("resizing");
      const startY = e.pageY;
      const startH = dataTr.offsetHeight || currentDefaultHeight;
      const onMove = e => {
        const h = Math.max(20, startH + (e.pageY - startY));
        rowHeights[rowIdx] = h;
        applyRowHeight(dataTr, h);
      };
      const onUp = () => {
        resizeTr.classList.remove("resizing");
        document.removeEventListener("mousemove", onMove);
        document.removeEventListener("mouseup", onUp);
      };
      document.addEventListener("mousemove", onMove);
      document.addEventListener("mouseup", onUp);
      e.preventDefault();
    });
  }

  function renderTable(rows) {
    const thead = document.getElementById("thead");
    const tbody = document.getElementById("tbody");
    thead.innerHTML = ""; tbody.innerHTML = "";
    rowHeights.length = 0;
    document.getElementById("ctrlBar").style.display = rows.length ? "flex" : "none";
    if (!rows.length) return;

    const keys = new Set();
    rows.forEach(r => Object.keys(r).forEach(k => keys.add(k)));
    const columns = Array.from(keys);

    const trHead = document.createElement("tr");
    const thIdx = document.createElement("th");
    thIdx.className = "idx-cell"; thIdx.textContent = "#";
    trHead.appendChild(thIdx);
    columns.forEach(col => {
      const th = document.createElement("th");
      th.textContent = col;
      th.style.width = DEFAULT_COL_WIDTH + "px";
      th.style.minWidth = DEFAULT_COL_WIDTH + "px";
      makeColResizer(th);
      trHead.appendChild(th);
    });
    thead.appendChild(trHead);

    rows.forEach((row, i) => {
      const h = currentDefaultHeight;
      rowHeights[i] = h;

      const dataTr = document.createElement("tr");
      dataTr.dataset.rowIdx = i;

      const tdIdx = document.createElement("td");
      tdIdx.className = "idx-cell"; tdIdx.textContent = i;
      dataTr.appendChild(tdIdx);

      columns.forEach(col => {
        const td = document.createElement("td");
        const inner = document.createElement("div");
        inner.className = "cell-inner";
        const val = row[col];
        if (val !== null && val !== undefined && typeof val === "object") {
          const pre = document.createElement("pre");
          pre.textContent = JSON.stringify(val, null, 2);
          inner.appendChild(pre);
        } else {
          inner.textContent = (val ?? "").toString();
        }
        td.appendChild(inner);
        dataTr.appendChild(td);
      });

      applyRowHeight(dataTr, h);
      tbody.appendChild(dataTr);

      const resizeTr = document.createElement("tr");
      resizeTr.className = "resize-row";
      const resizeTd = document.createElement("td");
      resizeTd.colSpan = columns.length + 1;
      resizeTd.title = "拖动调整行高";
      resizeTr.appendChild(resizeTd);
      makeRowResizer(resizeTr, dataTr, i);
      tbody.appendChild(resizeTr);
    });
  }

  document.getElementById("defaultHeight").addEventListener("change", e => {
    currentDefaultHeight = Math.max(20, parseInt(e.target.value) || 60);
  });

  document.getElementById("btnResetAll").addEventListener("click", () => {
    const h = currentDefaultHeight;
    document.querySelectorAll("#tbody tr[data-row-idx]").forEach(dataTr => {
      const i = parseInt(dataTr.dataset.rowIdx);
      rowHeights[i] = h;
      applyRowHeight(dataTr, h);
    });
  });

  async function loadFromSameFolder(filename) {
    const status = document.getElementById("status");
    status.textContent = "";
    try {
      const resp = await fetch("./" + filename, { cache: "no-store" });
      if (!resp.ok) throw new Error(`HTTP ${resp.status}：无法读取 ${filename}`);
      renderTable(parseJsonl(await resp.text()));
    } catch (e) {
      status.textContent = `加载失败：${e.message}`;
    }
  }

  document.getElementById("fileInput").addEventListener("change", e => {
    const file = e.target.files[0]; if (!file) return;
    document.getElementById("status").textContent = "";
    const reader = new FileReader();
    reader.onload = ev => renderTable(parseJsonl(ev.target.result));
    reader.readAsText(file);
  });

  document.getElementById("btnLoad").addEventListener("click", () => {
    const name = document.getElementById("jsonlName").value.trim();
    if (name) loadFromSameFolder(name);
  });

  loadFromSameFolder(document.getElementById("jsonlName").value.trim());
</script>
</body>
</html>


<!-- 最下 -->
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