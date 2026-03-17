---
layout: page
title: ""
permalink: /hidden-blog/
---

{% include hidden-blog/hb-styles.html %}

<div class="hb-wrap">

  <div class="hb-header">
    <div class="hb-mark">NOTES</div>
    <div class="hb-sub">short thoughts, written for myself</div>
  </div>

  {% include hidden-blog/hb-music.html %}
  {% include hidden-blog/hb-post-nav.html %}
  {% include hidden-blog/hb-post-nav-script.html %}

  <div id="hb-list-container">
    {% include hidden-blog/hb-content.html %}
  </div>

  <div id="hb-post-view" hidden aria-hidden="true"></div>

  <div class="hb-quiet">—</div>
</div>

{% include hidden-blog/hb-filter-script.html %}
{% include hidden-blog/hb-spa-nav.html %}