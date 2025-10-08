---
layout: default
title: Home
permalink: /
nav_order: 1
full_bleed: true
---

<style>
  /* Fade-in global */
  @keyframes fadeInUp { from { opacity:0; transform:translateY(25px);} to { opacity:1; transform:translateY(0);} }

  /* Eyebrow + titles fade-in */
  .eyebrow.shifted{
    margin-top:40px;
    opacity:0; transform:translateY(10px);
    animation:fadeInUp 1.4s ease-out .3s forwards;
  }
  .hero-content h1{
    opacity:0; transform:translateY(20px);
    animation:fadeInUp 1.4s ease-out .8s forwards;
  }
  .hero-content .subtitle{
    opacity:0; transform:translateY(20px);
    animation:fadeInUp 1.4s ease-out 1.3s forwards;
  }

  /* HERO layers so the logo sits above */
  .hero-video{ position:relative; z-index:2; overflow:hidden; }
  .hero-overlay{ position:absolute; inset:0; z-index:1; }
  .hero-content{ position:relative; z-index:2; }

  /* ===== Image logo (replaces text SH) ===== */
  .hero-logo-img{
    position:absolute;
    right:-4.0vw;              /* 🔥 plus plaqué encore (presque bord coupé) */
    top:38%; 
    transform:translateY(-36%);
    z-index:3;
    width:min(17vw, 50vh);
    height:auto;
    opacity:0;
    animation:fadeInLogo 1.2s ease-out 1.0s forwards;
    pointer-events:none; 
    user-select:none;
  }

  @keyframes fadeInLogo{
    from{ opacity:0; transform:translateY(-36%) translateX(40px); }
    to  { opacity:1; transform:translateY(-36%) translateX(0); }
  }

  @media (max-width:880px){
    .hero-logo-img{
      right:-1.2vw;  /* léger décalage sur mobile */
      top:42%;
      transform:translateY(-42%);
      width:min(24vw, 34vh);
    }
  }

  /* ===== Secondary video ===== */
  .promo-video{ position:relative; z-index:0; width:100%; margin:-1270px 0 0; }
  .promo-video-frame{ position:relative; width:100%; aspect-ratio:16/9; overflow:hidden; background:#000; border-top:1px solid #222; border-bottom:1px solid #222; }
  @supports not (aspect-ratio:16/9){ .promo-video-frame{padding-top:56.25%} .promo-video-el{position:absolute;left:0;top:0;width:100%;height:100%} }
  .promo-video-el{ position:absolute; inset:0; width:100%; height:100%; object-fit:cover; filter:brightness(.8) contrast(1.05) saturate(1.05); }
  .promo-scrim{ position:absolute; inset:0; background:linear-gradient(180deg,rgba(0,0,0,.35) 0%,rgba(0,0,0,.55) 65%,rgba(0,0,0,.7) 100%); pointer-events:none; }
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

  <!-- Image logo -->
  <img class="hero-logo-img" src="/assets/images/sh-logo.png" alt="SH monogram">
</section>

<!-- ===== Full-width secondary video ===== -->
<section class="promo-video">
  <div class="promo-video-frame">
    <video class="promo-video-el" autoplay muted loop playsinline preload="auto"
           poster="/assets/images/trading-broll-poster.jpg">
      <source src="/assets/videos/trading-broll.mp4" type="video/mp4">
    </video>
    <div class="promo-scrim"></div>
  </div>
</section>
