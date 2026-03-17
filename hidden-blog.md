---
layout: page
title: ""
permalink: /hidden-blog/
---

<style>
/* ---- Minimal philosophical notes style (scoped via .hb-wrap) ---- */
.hb-wrap{
  max-width: 720px;
  margin: 3.5rem auto;
  padding: 0 1.25rem;
  line-height: 1.85;
  letter-spacing: 0.01em;
  box-sizing: border-box;
}
.hb-wrap, .hb-wrap * { box-sizing: border-box; }
.hb-wrap a { color: inherit; }
.hb-wrap a:hover { text-decoration: none; }

.hb-wrap button,
.hb-wrap input{
  font: inherit;
}

.hb-header{
  margin-bottom: 1.5rem;
  opacity: 0.95;
}

.hb-header .hb-mark{
  font-size: 0.95rem;
  letter-spacing: 0.12em;
  text-transform: uppercase;
  opacity: 0.55;
}

.hb-header .hb-sub{
  margin-top: 0.6rem;
  font-size: 0.95rem;
  opacity: 0.65;
}

/* filter bar */
.hb-filter-bar{
  display: flex;
  flex-wrap: wrap;
  align-items: center;
  gap: 0.5rem;
  margin-bottom: 1.5rem;
}

.hb-search{
  flex: 1 1 180px;
  max-width: 280px;
  width: 100%;
  border-radius: 999px;
  border: 1px solid rgba(0,0,0,0.12);
  padding: 0.45rem 0.9rem;
  font-size: 0.9rem;
  background: #fff;
  outline: none;
}
.hb-search:focus{
  border-color: rgba(0,0,0,0.28);
  box-shadow: 0 0 0 3px rgba(0,0,0,0.06);
}

.hb-chips{
  display: flex;
  flex-wrap: wrap;
  gap: 0.4rem;
}

.hb-chip{
  appearance: none;
  -webkit-appearance: none;
  border-radius: 999px;
  padding: 0.25rem 0.7rem;
  font-size: 0.8rem;
  border: 1px solid rgba(0,0,0,0.08);
  cursor: pointer;
  opacity: 0.75;
  background: #fff;
  line-height: 1.2;
  white-space: nowrap;
  user-select: none;
}
.hb-chip:focus{ outline: none; }
.hb-chip:focus-visible{
  box-shadow: 0 0 0 3px rgba(0,0,0,0.10);
}

.hb-chip-active{
  background: #000;
  color: #fff;
  border-color: #000;
  opacity: 1;
}

.hb-list{
  display: flex;
  flex-direction: column;
}

.hb-year{
  margin-top: 1.5rem;
  margin-bottom: 0.2rem;
  font-size: 0.85rem;
  letter-spacing: 0.16em;
  text-transform: uppercase;
  opacity: 0.55;
}

.hb-item{
  padding: 1.1rem 0;
  border-top: 1px solid rgba(0,0,0,0.08);
}

.hb-item:first-of-type{
  border-top: 1px solid rgba(0,0,0,0.08);
}

.hb-title{
  font-size: 1.05rem;
  font-weight: 600;
  text-decoration: none;
  color: inherit;
  display: inline-block;
  overflow-wrap: anywhere;
  word-break: break-word;
}

.hb-meta{
  margin-top: 0.35rem;
  font-size: 0.85rem;
  opacity: 0.55;
}

.hb-excerpt{
  margin-top: 0.75rem;
  font-size: 0.98rem;
  opacity: 0.92;
  overflow-wrap: anywhere;
  word-break: break-word;
}

.hb-quiet{
  font-size: 0.9rem;
  opacity: 0.5;
  margin-top: 2.5rem;
}

.hb-external{
  margin-bottom: 2.5rem;
  padding-bottom: 1.5rem;
  border-bottom: 1px solid rgba(0,0,0,0.08);
}

.hb-external-title{
  font-size: 0.95rem;
  font-weight: 600;
  letter-spacing: 0.08em;
  text-transform: uppercase;
  opacity: 0.6;
  margin-bottom: 0.75rem;
}

.hb-external iframe{
  width: 100%;
  min-height: 420px;
  border: none;
  border-radius: 8px;
  box-shadow: 0 10px 30px rgba(0,0,0,0.04);
}

.hb-external-note{
  margin-top: 0.6rem;
  font-size: 0.85rem;
  opacity: 0.6;
}

/* Dark mode (best-effort; won’t affect other pages) */
@media (prefers-color-scheme: dark){
  .hb-item{ border-top: 1px solid rgba(255,255,255,0.12); }
  .hb-item:first-of-type{ border-top: 1px solid rgba(255,255,255,0.12); }
  .hb-search{
    background: transparent;
    color: inherit;
    border-color: rgba(255,255,255,0.22);
  }
  .hb-search:focus{
    border-color: rgba(255,255,255,0.35);
    box-shadow: 0 0 0 3px rgba(255,255,255,0.10);
  }
  .hb-chip{
    background: transparent;
    border-color: rgba(255,255,255,0.22);
  }
  .hb-chip:focus-visible{
    box-shadow: 0 0 0 3px rgba(255,255,255,0.12);
  }
}

@media (max-width: 600px){
  .hb-wrap{
    margin-top: 2.5rem;
  }
  .hb-filter-bar{
    gap: 0.6rem;
  }
  .hb-search{
    max-width: 100%;
  }
}
</style>

<div class="hb-wrap">

  <div class="hb-header">
    <div class="hb-mark">NOTES</div>
    <div class="hb-sub">short thoughts, written for myself</div>
  </div>

  {% assign filtered = site.hidden | default: site.pages %}

  {% comment %}
    Collect all categories that appear in filtered posts
    去掉像 "b" 这种只是文件夹名的类别
  {% endcomment %}
  {% assign all_categories = "" | split: "" %}
  {% for post in filtered %}
    {% assign clean_cats = "" | split: "" %}
    {% for cat in post.categories %}
      {% unless cat == 'b' %}
        {% assign clean_cats = clean_cats | push: cat %}
      {% endunless %}
    {% endfor %}
    {% for cat in clean_cats %}
      {% unless all_categories contains cat %}
        {% assign all_categories = all_categories | push: cat %}
      {% endunless %}
    {% endfor %}
  {% endfor %}

  <div class="hb-filter-bar">
    <input
      id="hb-search"
      class="hb-search"
      type="search"
      placeholder="Searching for title or content...">
    <div class="hb-chips" id="hb-chips">
      <button class="hb-chip hb-chip-active" data-cat="all">ALL</button>
      {% for cat in all_categories %}
        <button class="hb-chip" data-cat="{{ cat | downcase | escape_once }}">{{ cat }}</button>
      {% endfor %}
    </div>
  </div>

  {% if filtered == empty or filtered.size == 0 %}
    <div class="hb-quiet">Nothing here yet.</div>
  {% else %}
    {% assign sorted = filtered | sort: "date" | reverse %}
    <div id="hb-list" class="hb-list">
      {% for post in sorted %}
        {% assign clean_cats = "" | split: "" %}
        {% for cat in post.categories %}
          {% unless cat == 'b' %}
            {% assign clean_cats = clean_cats | push: cat %}
          {% endunless %}
        {% endfor %}
        {% assign search_only_flag = post.search_only | default: false %}
        <div class="hb-item"
             data-categories="{{ clean_cats | join: ' ' | downcase | escape_once }}"
             data-title="{{ post.title | downcase | escape_once }}"
             data-text="{{ post.content | strip_html | strip_newlines | downcase | escape_once }}"
             data-search-only="{{ search_only_flag }}">
          <a class="hb-title" href="{{ post.url | relative_url }}">{{ post.title }}</a>
          {% assign display_date = post.last_modified_at | default: post.date %}
          <div class="hb-meta">
            {{ display_date | date: "%Y-%m-%d" }}
            {% if clean_cats and clean_cats.size > 0 %}
              ·
              {% for cat in clean_cats %}
                <span>{{ cat }}</span>{% unless forloop.last %}, {% endunless %}
              {% endfor %}
            {% endif %}
          </div>
          <div class="hb-excerpt">
            {{ post.content | strip_html | strip_newlines | truncate: 160 }}
          </div>
        </div>
      {% endfor %}
    </div>
  {% endif %}

  <div class="hb-quiet">—</div>
</div>

<script>
(function() {
  var searchInput = document.getElementById('hb-search');
  var chips = document.querySelectorAll('#hb-chips .hb-chip');
  var items = document.querySelectorAll('#hb-list .hb-item');
  if (!searchInput || chips.length === 0 || items.length === 0) return;

  var activeCat = 'all';

  function normalize(str) {
    return (str || '').toLowerCase();
  }

  function applyFilter() {
    var q = normalize(searchInput.value.trim());
    var anyVisible = false;
    items.forEach(function(item) {
      var cats = normalize(item.getAttribute('data-categories') || '');
      var title = normalize(item.getAttribute('data-title') || '');
      var text = normalize(item.getAttribute('data-text') || '');
      var searchOnly = (item.getAttribute('data-search-only') || 'false') === 'true';

      // 带 search_only 标记的文章，在没有输入搜索词时不展示
      if (searchOnly && !q) {
        item.style.display = 'none';
        return;
      }

      var matchCat = (activeCat === 'all') || cats.split(/\s+/).indexOf(activeCat) !== -1;
      var matchText = !q || (title.indexOf(q) !== -1 || text.indexOf(q) !== -1);

      if (matchCat && matchText) {
        item.style.display = '';
        anyVisible = true;
      } else {
        item.style.display = 'none';
      }
    });
  }

  chips.forEach(function(chip) {
    chip.addEventListener('click', function() {
      activeCat = chip.getAttribute('data-cat');
      chips.forEach(function(c) { c.classList.remove('hb-chip-active'); });
      chip.classList.add('hb-chip-active');
      applyFilter();
    });
  });

  searchInput.addEventListener('input', applyFilter);

  // 初次加载页面时就执行一次过滤，
  // 把带 search_only 标记但没有搜索词的文章隐藏
  applyFilter();
})();
</script>