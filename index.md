---
layout: page
title: Home
permalink: /
nav_order: 1
full_bleed: true   # <<< active le rendu plein écran uniquement pour la Home
---

<section class="hero-video">
  <!-- Vidéo de fond (mets ton fichier ici : /assets/videos/trading-hero.mp4) -->
  <video class="hero-bg" autoplay muted loop playsinline preload="auto" poster="{{ '/assets/images/hero-poster.jpg' | relative_url }}">
    <source src="{{ '/assets/videos/trading-hero.mp4' | relative_url }}" type="video/mp4">
    <!-- Optionnel : <source src="{{ '/assets/videos/trading-hero.webm' | relative_url }}" type="video/webm"> -->
  </video>

  <!-- Overlay sombre pour lisibilité -->
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
