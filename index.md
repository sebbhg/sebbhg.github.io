---
layout: default
title: Home
permalink: /
nav_order: 1
full_bleed: true
---

<!-- Import police style GS -->
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@700;800&display=swap" rel="stylesheet">

<style>
  /* Fade-in animation */
  @keyframes fadeInUp { 
    from { opacity: 0; transform: translateY(25px); } 
    to { opacity: 1; transform: translateY(0); } 
  }

  /* Move down + fade-in */
  .eyebrow.shifted {
    margin-top: 40px;
    opacity: 0;
    transform: translateY(10px);
    animation: fadeInUp 1.4s ease-out 0.3s forwards;
  }

  .hero-content h1 {
    opacity: 0;
    transform: translateY(20px);
    animation: fadeInUp 1.4s ease-out 0.8s forwards;
  }

  .hero-content .subtitle {
    opacity: 0;
    transform: translateY(20px);
    animation: fadeInUp 1.4s ease-out 1.3s forwards;
  }

  /* HERO + overlay setup */
  .hero-video { position: relative; z-index: 2; overflow: hidden; }
  .hero-overlay { position: absolute; inset: 0; z-index: 1; }
  .hero-content { position: relative; z-index: 2; }

  /* Second video below */
  .promo-video {
    position: relative;
    z-index: 0;
    width: 100%;
    margin: -1270px 0 0;
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

  /* ===== MONOGRAMME "SH" façon Goldman améliorée ===== */
  .hero-logo {
    position: absolute;
    right: -0.15em;              /* bord droit très proche, légèrement coupé */
    top: 43%;                    /* position verticale équilibrée */
    transform: translateY(-43%);
    text-align: center;
    line-height: .7;             /* interlignage serré */
    z-index: 3;
    opacity: 0;
    animation: fadeInLogo 1.8s ease-out 1.2s forwards;
    font-family: 'Playfair Display', serif; /* typographie premium */
    user-select: none;
    pointer-events: none;
  }

  .hero-logo span {
    display: block;
    font-weight: 800;
    font-size: min(17vw, 49vh); /* taille massive responsive */
    background: linear-gradient(to bottom, #fff 20%, #e8e8e8 100%);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    letter-spacing: -0.03em;
  }

  /* Ajustements optiques du S */
  .hero-logo .s {
    transform: scale(1.08) translateX(0.03em);
    margin-bottom: -0.22em;
  }

  /* Ajustements du H pour symétrie */
  .hero-logo .h {
    transform: translateX(-0.01em);
  }

  @keyframes fadeInLogo {
    from { opacity: 0; transform: translateY(-43%) translateX(30px); }
    to { opacity: 1; transform: translateY(-43%) translateX(0); }
  }

  /* Mobile adjustments */
  @media (max-width: 880px) {
    .hero-logo { right: -0.1em; top: 46%; transform: translateY(-46%); }
    .hero-logo span { font-size: min(22vw, 34vh); }
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

  <!-- Monogramme vertical stylé -->
  <div class="hero-logo">
    <span class="s">S</span>
    <span class="h">H</span>
  </div>
</section>

<!-- Secondary video -->
<section class="promo-video">
  <div class="promo-video-frame">
    <video class="promo-video-el" autoplay muted loop playsinline preload="auto"
           poster="/assets/images/trading-broll-poster.jpg">
      <source src="/assets/videos/trading-broll.mp4" type="video/mp4">
    </video>
    <div class="promo-scrim"></div>
  </div>
</section>
