---
layout: default
title: Home
permalink: /
nav_order: 1
full_bleed: true
---

<style>
  /* Fade-in global */
  @keyframes fadeInUp { from { opacity: 0; transform: translateY(25px);} to { opacity: 1; transform: translateY(0);} }

  /* Eyebrow + titles fade-in */
  .eyebrow.shifted {
    margin-top: 40px;
    opacity: 0; transform: translateY(10px);
    animation: fadeInUp 1.4s ease-out .3s forwards;
  }
  .hero-content h1 {
    opacity: 0; transform: translateY(20px);
    animation: fadeInUp 1.4s ease-out .8s forwards;
  }
  .hero-content .subtitle {
    opacity: 0; transform: translateY(20px);
    animation: fadeInUp 1.4s ease-out 1.3s forwards;
  }

  /* HERO layers so logo sits above */
  .hero-video { position: relative; z-index: 2; overflow: hidden; }
  .hero-overlay { position: absolute; inset: 0; z-index: 1; }
  .hero-content { position: relative; z-index: 2; }

  /* Secondary video below hero (unchanged) */
  .promo-video { position: relative; z-index: 0; width: 100%; margin: -1270px 0 0; }
  .promo-video-frame { position: relative; width: 100%; aspect-ratio: 16/9; overflow: hidden; background: #000; border-top: 1px solid #222; border-bottom: 1px solid #222; }
  @supports not (aspect-ratio: 16 / 9) { .promo-video-frame{padding-top:56.25%} .promo-video-el{position:absolute;left:0;top:0;width:100%;height:100%} }
  .promo-video-el { position: absolute; inset: 0; width: 100%; height: 100%; object-fit: cover; filter: brightness(.8) contrast(1.05) saturate(1.05); }
  .promo-scrim { position: absolute; inset: 0; background: linear-gradient(180deg,rgba(0,0,0,.35) 0%,rgba(0,0,0,.55) 65%,rgba(0,0,0,.7) 100%); pointer-events: none; }

  /* ===== Monogram “S / H” — EXACT Goldman style (solid white, serif, cropped right) ===== */
  .hero-logo{
    position: absolute;
    right: -0.12em;          /* bord droit légèrement coupé, comme GS */
    top: 44%;                /* remonte un peu */
    transform: translateY(-44%);
    text-align: center;
    line-height: .68;        /* interlignage serré, lettres qui se touchent */
    z-index: 3;
    user-select: none; pointer-events: none;
    opacity: 0; animation: fadeInLogo 1.2s ease-out 1.0s forwards;
    font-family: "Times New Roman", Times, Georgia, serif;  /* serif système, proche GS */
    -webkit-font-smoothing: antialiased; text-rendering: optimizeLegibility;
  }
  .hero-logo span{
    display: block;
    font-weight: 800;
    font-size: min(16vw, 48vh);   /* taille massive, même valeur pour S et H */
    color: #ffffff;               /* PLEIN BLANC */
    letter-spacing: -0.02em;
  }
  /* Micro-chevauchement pour l’effet monogramme sans fausser la taille */
  .hero-logo .s{ margin-bottom: -.20em; } /* rapproche S et H, pas de scale */
  .hero-logo .h{ }

  @keyframes fadeInLogo { from{opacity:0; transform:translateY(-44%) translateX(30px)} to{opacity:1; transform:translateY(-44%) translateX(0)} }

  /* Mobile: plus petit et un peu recentré verticalement */
  @media (max-width: 880px){
    .hero-logo{ right: -0.08em; top: 46%; transform: translateY(-46%); }
    .hero-logo span{ font-size: min(22vw, 34vh); }
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

  <!-- Monogram vertical “S / H” -->
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
