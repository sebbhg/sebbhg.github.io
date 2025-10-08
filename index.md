---
layout: default
title: Home
permalink: /
nav_order: 1
full_bleed: true
---

<style>
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

  /* === HERO VIDEO SECTION (ensure logo is on top of everything here) === */
  .hero-video { position: relative; z-index: 2; overflow: hidden; }
  .hero-overlay { position:absolute; inset:0; z-index: 1; }
  .hero-content { position: relative; z-index: 2; }

  /* === Secondary video styling (adjusted position) === */
  .promo-video {
    position: relative;   /* needed for stacking with z-index */
    z-index: 0;           /* keep this BELOW the hero section */
    width: 100%;
    margin: -1270px 0 0;  /* Adjust vertical position (your value) */
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

  @supports not (aspect-ratio: 16 / 9) {
    .promo-video-frame { padding-top: 56.25%; }
    .promo-video-el { position: absolute; left: 0; top: 0; width: 100%; height: 100%; }
  }

  .promo-video-el {
    position: absolute; inset: 0; width: 100%; height: 100%;
    object-fit: cover; filter: brightness(.8) contrast(1.05) saturate(1.05);
  }

  .promo-scrim {
    position: absolute; inset: 0;
    background: linear-gradient(180deg, rgba(0,0,0,.35) 0%, rgba(0,0,0,.55) 65%, rgba(0,0,0,.7) 100%);
    pointer-events: none;
  }

  /* === Logo initials (à droite comme Goldman Sachs) === */
  .hero-logo {
    position: absolute;
    right: 3vw;
    bottom: 16vh;
    font-size: clamp(4rem, 12vw, 14rem);
    font-weight: 700;
    color: rgba(255,255,255,0.12); /* un peu plus visible */
    line-height: 0.8;
    letter-spacing: -0.05em;
    font-family: "Times New Roman", serif;
    user-select: none;
    pointer-events: none;
    z-index: 3; /* above overlay + content */
    opacity: 0;
    transform: translateX(40px);
    animation: fadeInLogo 2s ease-out 1.5s forwards;
  }

  @keyframes fadeInLogo {
    to { opacity: 1; transform: translateX(0); }
  }

  /* Fade-in animation */
  @keyframes fadeInUp {
    from { opacity: 0; transform: translateY(25px); }
    to   { opacity: 1; transform: translateY(0); }
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

  <!-- Logo initials (SH) like Goldman Sachs -->
  <div class="hero-logo">SH</div>
</section>

<!-- ===== Full-width secondary video (no text overlay) ===== -->
<section class="promo-video">
  <div class="promo-video-frame">
    <video class="promo-video-el" autoplay muted loop playsinline preload="auto"
           poster="/assets/images/trading-broll-poster.jpg">
      <source src="/assets/videos/trading-broll.mp4" type="video/mp4">
    </video>
    <div class="promo-scrim"></div>
  </div>
</section>
