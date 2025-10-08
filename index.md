---
layout: default
title: Home
permalink: /
nav_order: 1
full_bleed: true
---

<style>
  /* === Styles de secours pour la deuxième vidéo === */
  .promo-video{width:100%;margin:-980px 0;}
  .promo-video-frame{position:relative;width:100%;aspect-ratio:16/9;overflow:hidden;background:#000;border-top:1px solid #222;border-bottom:1px solid #222;}
  @supports not (aspect-ratio: 16 / 9) {
    .promo-video-frame{padding-top:56.25%;}
    .promo-video-el{position:absolute;left:0;top:0;width:100%;height:100%;}
  }
  .promo-video-el{position:absolute;inset:0;width:100%;height:100%;object-fit:cover;filter:brightness(.8) contrast(1.05) saturate(1.05);}
  .promo-scrim{position:absolute;inset:0;background:linear-gradient(180deg,rgba(0,0,0,.35) 0%,rgba(0,0,0,.55) 65%,rgba(0,0,0,.7) 100%);pointer-events:none;}
  .promo-caption{position:absolute;left:clamp(16px,4vw,48px);bottom:clamp(14px,4vw,48px);max-width:min(78ch,60vw);}
  .promo-caption h2{margin:0 0 .25rem;font-weight:800;line-height:1.05;font-size:clamp(1.4rem,3.2vw,2.4rem);text-shadow:0 2px 18px rgba(0,0,0,.45);}
  .promo-caption p{margin:0;opacity:.95;font-size:clamp(.95rem,1.2vw,1.15rem);}
</style>

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
           poster="/assets/images/trading-broll-poster.jpg">
      <source src="/assets/videos/trading-broll.mp4" type="video/mp4">
    </video>

    <!-- Voile sombre pour lisibilité -->
    <div class="promo-scrim"></div>

    <!-- Texte (personnalisable) -->
    <div class="promo-caption">
      <h2>Markets. Models. Risk.</h2>
      <p>From pricing to XVA, I build reliable tooling for trading desks.</p>
    </div>
  </div>
</section>
