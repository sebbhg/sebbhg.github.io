---
layout: default
title: Home
permalink: /
nav_order: 1
full_bleed: true
---

<section class="hero-video">
  <!-- Vidéo de fond -->
  <video class="hero-bg" autoplay muted loop playsinline preload="auto" poster="{{ '/assets/images/hero-poster.jpg' | relative_url }}">
    <source src="{{ '/assets/videos/trading-hero.mp4' | relative_url }}" type="video/mp4">
    <!-- Optionnel :
    <source src="{{ '/assets/videos/trading-hero.webm' | relative_url }}" type="video/webm"> -->
  </video>

  <!-- Overlay sombre -->
  <div class="hero-overlay"></div>

  <!-- Texte de présentation -->
  <div class="hero-content">
    <p class="eyebrow">Quantitative Finance & Trading</p>
    <h1>Sébastien HAAG</h1>
    <p class="subtitle">
      Building robust pricing, risk & XVA tooling — <strong>CFA Level I holder</strong>.<br/>
      IRS / XCCY / Swaptions · EE/EEE · CVA/XVA · LGM-1F · GPR & Bayesian Quadrature
    </p>

    <div class="hero-actions">
      <a class="btn primary" href="{{ '/resumes' | relative_url }}">View CV</a>
      <a class="btn" href="{{ '/theses' | relative_url }}">Theses</a>
      <a class="btn" href="{{ '/cours' | relative_url }}">Courses</a>
      <a class="btn" href="{{ '/reading' | relative_url }}">Reading</a>
      <a class="btn" href="{{ '/what-i-do' | relative_url }}">What I do</a>
    </div>
  </div>
</section>

<!-- ===== Bandeau vidéo pleine largeur sous le hero ===== -->
<section class="promo-video">
  <div class="promo-video-frame">
    <video class="promo-video-el" autoplay muted loop playsinline preload="auto"
           poster="{{ '/assets/images/trading-broll-poster.jpg' | relative_url }}">
      <source src="{{ '/assets/videos/trading-broll.mp4' | relative_url }}" type="video/mp4">
      <!-- Optionnel :
      <source src="{{ '/assets/videos/trading-broll.webm' | relative_url }}" type="video/webm"> -->
    </video>

    <!-- Voile sombre pour lisibilité -->
    <div class="promo-scrim"></div>

    <!-- Texte (on ajustera le contenu à ta demande) -->
    <div class="promo-caption">
      <h2>Markets. Models. Risk.</h2>
      <p>From pricing to XVA, I build reliable tooling for trading desks.</p>
    </div>
  </div>
</section>
