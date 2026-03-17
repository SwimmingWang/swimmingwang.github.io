---
layout: page
title: 番剧评价记录
# permalink: /anime-reviews/
categories: [others, 中文]
search_only: false
date: 2025-02-28 09:00:00 +0800
---

<style>
.anime-page {
  max-width: 860px;
  margin: 0 auto;
  padding: 1rem 0 3rem 0;
}

.anime-hero {
  margin-bottom: 2rem;
  padding: 2rem 1.5rem;
  border-radius: 22px;
  background: linear-gradient(135deg, #fff8fb 0%, #f7f8ff 100%);
  border: 1px solid rgba(0,0,0,0.06);
  box-shadow: 0 10px 30px rgba(0,0,0,0.06);
}

.anime-hero h1 {
  margin: 0 0 0.6rem 0;
  font-size: 2rem;
  line-height: 1.2;
}

.anime-hero p {
  margin: 0;
  color: #666;
  line-height: 1.8;
}

.anime-list {
  display: grid;
  gap: 1.5rem;
}

.anime-card {
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

.anime-card:hover {
  transform: translateY(-3px);
  box-shadow: 0 14px 32px rgba(0,0,0,0.08);
}

.anime-poster img {
  width: 100%;
  display: block;
  border-radius: 14px;
  object-fit: cover;
}

.anime-title {
  margin: 0 0 0.6rem 0;
  font-size: 1.35rem;
}

.anime-meta {
  display: flex;
  flex-wrap: wrap;
  gap: 0.6rem;
  margin-bottom: 0.9rem;
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
  .anime-card {
    grid-template-columns: 1fr;
  }

  .anime-poster {
    max-width: 240px;
  }
}
</style>

<div class="anime-page">

  <div class="anime-hero">
    <!-- <h1>番剧评价记录</h1> -->
    <p>
      这里记录我看过的一些番剧，包括观看时间、海报，以及看完后的即时感受。
    </p>
  </div>


  <!-- <div class="anime-card">
      <div class="anime-poster">
        <img src="" alt="海报">
      </div>

      <div class="anime-content">
        <h2 class="anime-title">名字</h2>

        <div class="anime-meta">
          <span class="meta-tag">观看时间：</span>
          <span class="meta-tag rating">评分：* / 10</span>
        </div>

        <div class="review-box">
          感想
        </div>
      </div>
    </div> -->

  <div class="section-title">已观看番剧列表</div>

  <div class="anime-list">
    <div class="anime-card">
      <div class="anime-poster">
        <img src="https://lain.bgm.tv/pic/cover/l/f1/fd/349441_uND33.jpg" alt="水星的魔女 海报">
      </div>

      <div class="anime-content">
        <h2 class="anime-title">水星的魔女</h2>

        <div class="anime-meta">
          <span class="meta-tag">观看时间：2026-03-17</span>
          <span class="meta-tag rating">评分：7 / 10</span>
        </div>

        <div class="review-box">
        玩派的时候看到导线管的新联动皮肤觉得风灵很好看，就想着找个高达看看，发现op居然是
        <span class="video-toggle" onclick="toggleBiliVideo()">祝福</span>
        ，好像只有op是正片啊。
        </div>

        <div id="bili-video" class="bilibili-player" style="display: none;">
        <iframe
            src="https://player.bilibili.com/player.html?bvid=BV18N4y1P7av&page=1"
            scrolling="no"
            border="0"
            frameborder="no"
            framespacing="0"
            allowfullscreen="true">
        </iframe>
        </div>

        <style>
        .video-toggle {
        color: #ff4d6d;
        cursor: pointer;
        font-weight: 600;
        }
        .video-toggle:hover {
        text-decoration: underline;
        }

        .bilibili-player {
        margin-top: 12px;
        border-radius: 12px;
        overflow: hidden;
        max-width: 720px;
        }
        .bilibili-player iframe {
        width: 100%;
        aspect-ratio: 16 / 9;
        display: block;
        }
        </style>

        <script>
        function toggleBiliVideo() {
        const video = document.getElementById("bili-video");
        if (video.style.display === "none") {
            video.style.display = "block";
        } else {
            video.style.display = "none";
        }
        }
        </script>
      </div>
    </div>

    <div class="anime-card">
      <div class="anime-poster">
        <img src="https://lain.bgm.tv/pic/cover/l/83/14/401783_x6496.jpg" alt="租借女友 海报">
      </div>

      <div class="anime-content">
        <h2 class="anime-title">租借女友（1 2 3）</h2>

        <div class="anime-meta">
          <span class="meta-tag">观看时间：2026-03-13</span>
          <span class="meta-tag rating">评分：* / 10</span>
        </div>

        <div class="review-box">
          看的胃疼，真有人能写出来这种故事的，第四季都没啥看的想法了。这男主这么拉完了还有一堆女的喜欢，真是小宅男的最终幻想。
        </div>
      </div>
    </div>
    <div class="anime-card">
      <div class="anime-poster">
        <img src="https://lain.bgm.tv/r/400/pic/cover/l/38/44/398951_973Z3.jpg" alt="更衣人偶第二季">
      </div>

      <div class="anime-content">
        <h2 class="anime-title">更衣人偶第二季</h2>

        <div class="anime-meta">
          <span class="meta-tag">观看时间：2026-3-8</span>
          <span class="meta-tag rating">评分：10 / 10</span>
        </div>

        <div class="review-box">
          喜多川我老婆，节奏不快看的很舒服。
        </div>
      </div>
    </div>
  </div>
</div>