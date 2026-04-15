---
layout: page
title: 大酒测评
permalink: /beer-reviews/
categories: [others, 中文]
search_only: true
date: 2025-03-23 09:00:00 +0800
pinned: true
---

<style>
.beer-page {
  max-width: 860px;
  margin: 0 auto;
  padding: 1rem 0 3rem 0;
}

.beer-hero {
  margin-bottom: 2rem;
  padding: 2rem 1.5rem;
  border-radius: 22px;
  background: linear-gradient(135deg, #fff8fb 0%, #f7f8ff 100%);
  border: 1px solid rgba(0,0,0,0.06);
  box-shadow: 0 10px 30px rgba(0,0,0,0.06);
}

.beer-hero h1 {
  margin: 0 0 0.6rem 0;
  font-size: 2rem;
  line-height: 1.2;
}

.beer-hero p {
  margin: 0;
  color: #666;
  line-height: 1.8;
}

.beer-list {
  display: grid;
  gap: 1.5rem;
}

.beer-card {
  display: grid;
  grid-template-columns: 180px 1fr;
  gap: 1.2rem;
  align-items: start;
  padding: 1.2rem;
  border-radius: 20px;
  background: #ffffff;
  border: 1px solid rgba(0,0,0,0.06);
  box-shadow: 0 8px 24px rgba(0,0,0,0.05);
  transition: transform 0.2s ease, box-shadow 0.2s ease;
}

.beer-card:hover {
  transform: translateY(-3px);
  box-shadow: 0 14px 32px rgba(0,0,0,0.08);
}

.beer-poster img {
  width: 100%;
  display: block;
  border-radius: 14px;
  object-fit: cover;
}

.beer-title {
  margin: 0 0 0.6rem 0;
  font-size: 1.35rem;
}

.beer-meta {
  display: flex;
  flex-wrap: wrap;
  gap: 0.6rem;
  margin-bottom: 0.9rem;
}

.beer-actions {
  display: flex;
  flex-wrap: wrap;
  gap: 0.6rem;
  margin: 0 0 0.9rem 0;
}

.beer-link-btn {
  display: inline-flex;
  align-items: center;
  gap: 0.4rem;
  padding: 0.34rem 0.85rem;
  border-radius: 999px;
  font-size: 0.92rem;
  background: #eef1ff;
  color: #3b4cca;
  text-decoration: none;
  border: 1px solid rgba(59, 76, 202, 0.18);
  transition: transform 0.15s ease, box-shadow 0.15s ease, background 0.15s ease;
}

.beer-link-btn:hover {
  background: #e7ebff;
  box-shadow: 0 8px 18px rgba(59, 76, 202, 0.12);
  transform: translateY(-1px);
}

.beer-link-btn:active {
  transform: translateY(0px);
  box-shadow: none;
}

.meta-tag {
  display: inline-block;
  padding: 0.28rem 0.72rem;
  border-radius: 999px;
  font-size: 0.92rem;
  background: #f5f6fb;
  color: #555;
}

.rating {
  background: #ffe9b8;
  color: #7a5600;
  font-weight: 600;
}

.review-box {
  padding: 1rem 1rem;
  border-radius: 14px;
  background: #fafafe;
  color: #333;
  line-height: 1.9;
  border-left: 4px solid #d9defa;
}

.section-title {
  margin: 2.2rem 0 1rem 0;
  font-size: 1.15rem;
  color: #444;
  letter-spacing: 0.02em;
}

.template-box {
  padding: 1rem 1.2rem;
  border-radius: 16px;
  background: #fbfbfd;
  border: 1px dashed rgba(0,0,0,0.12);
  color: #666;
  line-height: 1.8;
}

@media (max-width: 700px) {
  .beer-card {
    grid-template-columns: 1fr;
  }

  .beer-poster {
    max-width: 240px;
  }
}
</style>

<div class="beer-page">

  <div class="beer-hero">
    <!-- <h1>番剧评价记录</h1> -->
    <p>
      事先说明，本人只喝啤酒和鸡尾酒这类的小麦果汁，测评主要包括在便利店买的便宜的小酒，都是主观感受。
    </p>
  </div>


  <!-- <div class="beer-card">
      <div class="beer-poster">
        <img src="" alt="海报">
      </div>

      <div class="beer-content">
        <h2 class="beer-title">名字</h2>

        <div class="beer-meta">
          <span class="meta-tag">观看时间：</span>
          <span class="meta-tag rating">评分：* / 10</span>
        </div>

        <div class="review-box">
          感想
        </div>
      </div>
    </div> -->

  <div class="section-title">小麦果汁类表</div>

  <div class="beer-list">
    {% assign beer_reviews = site.hidden | where: "hb_kind", "alcohol_review" | sort: "date" | reverse %}
    {% for review in beer_reviews %}
      {% assign watched_date = review.date | date: "%Y-%m-%d" %}
      <div class="beer-card">
        <div class="beer-poster">
          <img src="{{ review.poster | escape_once }}" alt="{{ review.poster_alt | default: review.title | escape_once }}">
        </div>

        <div class="beer-content">
          <h2 class="beer-title">{{ review.title }}</h2>

          {% assign anime_links = review.anime_links %}
          {% assign single_url = review.anime_url | default: review.link %}
          {% if anime_links and anime_links.size > 0 %}
            <div class="beer-actions">
              {% for it in anime_links %}
                {% assign url = it.url | default: it %}
                {% assign label = it.label | default: '番剧链接' %}
                {% if url %}
                  <a class="beer-link-btn" href="{{ url | escape_once }}" target="_blank" rel="noopener noreferrer">
                    {{ label | escape_once }} ↗
                  </a>
                {% endif %}
              {% endfor %}
            </div>
          {% elsif single_url %}
            <div class="beer-actions">
              <a class="beer-link-btn" href="{{ single_url | escape_once }}" target="_blank" rel="noopener noreferrer">
                番剧链接 ↗
              </a>
            </div>
          {% endif %}

          <div class="beer-meta">
            <span class="meta-tag">品尝时间：{{ watched_date }}</span>
            {% if review.rating %}
              <span class="meta-tag rating">评分：{{ review.rating }} / 10</span>
            {% endif %}
          </div>

          <div class="review-box">
            {{ review.content | markdownify }}
          </div>
        </div>
      </div>
    {% endfor %}
  </div>
</div>