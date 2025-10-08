---
layout: default
title: Home
permalink: /
nav_order: 1
full_bleed: true
---

<style>
  /* Fade-in general animation */
  @keyframes fadeInUp {
    from { opacity: 0; transform: translateY(25px); }
    to { opacity: 1; transform: translateY(0); }
  }

  /* Move down the "Quantitative Finance & Trading" line + fade-in */
  .eyebrow.shifted {
    margin-top: 40px;
    opacity: 0;
    transform: translateY(10px);
    animation: fadeInUp 1.4s ease-out 0.3s forwards;
  }

  /* Main title fade-in */
  .hero-content h1 {
    opacity: 0;
    transform: translateY(20px);
    animation: fadeInUp 1.4s ease-out 0.8s forwards;
  }

  /* Subtitle fade-in */
  .hero-content .subtitle {
    opacity: 0;
    transform: translateY(20px);
    animation: fadeInUp 1.4s ease-out 1.3s forwards;
  }

  /* === HERO VIDEO SECTION === */
  .hero-video {
    position: relative;
    z-index: 2;
    overflow: hidden;
  }

  .hero-overlay { position: absolute; inset: 0; z-index: 1; }
  .hero-content { position: relative; z-index: 2; }

  /* === Secondary video styling (below hero) === */
  .promo-video {
    position: relative;
    z-index: 0;
    width: 100%;
    margin: -1270px 0 0; /* adjust as before */
  }

  .promo-video-frame {
    position: relative;
    width: 100%;
    aspect-ratio: 16/9;
    overflow: hidden;
    background: #000;
    border-top: 1px solid #222;
    border-bottom: 1px solid #222;
  }

  .promo-video-el {
    position: absolute;
    inset: 0;
    width: 100%;
    height: 100%;
    object-fit: cover;
    filter: brightness(.8) contrast(1.05) saturate(1.05);
  }

  .promo-scrim {
    position: absolute;
    inset: 0;
    background: linear-gradient(180deg, rgba(0,0,0,.35) 0%, rgba(0,0,0,.55) 65%, rgba(0,0,0,.7) 100%);
    pointer-events: none;
  }

  /* === LOGO INITIALS (vertical style like Goldman Sachs) === */
  .hero-logo {
    position: absolute;
    right: 2.5vw;
    top: 50%;
    transform: translateY(-50%);
    text-align: center;
    line-height: 0.8;
    z-index: 3;
    font-family: 'Times New Roman', serif;
    color: rgba(255, 255, 255, 0.9);
    font-weight: 700;
    opacity: 0;
    animation: fadeInLogo 2s ease-out 1.5s forwards;
  }

  .hero-logo span {
    display: block;
    font-size: clamp(6rem, 13vw, 15rem);
    letter-spacing: -0.05em;
  }

  .hero-logo .s { margin-bottom: 0.1em; }

  @keyframes fadeInLogo {
    to {
      opacity: 1;
      transform: translateY(-50%);
    }
  }
</style>

<section class="hero-video">
  <!-- Background video -->
  <video class="hero-bg" autoplay muted loop playsinline preload="auto"
         poster="{{ '/assets/images/hero-poster.jpg' | relative_url }}">
    <source src="{{ '/assets/videos/trading-hero.mp4' | relative_url }}" type="video/mp4">
  </video>

  <!-- Dark overlay -->
  <div class="hero-overlay"></div>

  <!-- Main title and content -->
  <div class="hero-content">
    <p class="eyebrow shifted">Quantitative Finance & Trading</p>
    <h1>Turning Models into Market Impact</h1>
    <p class="subtitle">
      Quantitative Finance Engineer — <strong>CFA Level I Holder</strong>.<br/>
    </p>

    <div class="hero-actions">
      <a class="btn primary" href="{{ '/resumes' | relative_url }}">View CV</a>
      <a class="btn" href="{{ '/theses' | relative_url }}">Theses</a>
      <a class="btn" href="{{ '/cours' | relative_url }}">Courses</a>
      <a class="btn" href="{{ '/reading' | relative_url }}">Reading</a>
      <a class="btn" href="{{ '/what-i-do' | relative_url }}">What I do</a>
    </div>
  </div>

  <!-- Vertical SH logo -->
  <div class="hero-logo">
    <span class="s">S</span>
    <span class="h">H</span>
  </div>
</section>

<!-- ===== Full-width secondary video (no overlay text) ===== -->
<section class="promo-video">
  <div class="promo-video-frame">
    <video class="promo-video-el" autoplay muted loop playsinline preload="auto"
           poster="/assets/images/trading-broll-poster.jpg">
      <source src="/assets/videos/trading-broll.mp4" type="video/mp4">
    </video>
    <div class="promo-scrim"></div>
  </div>
</section>
