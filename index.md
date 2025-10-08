---
layout: default
title: Home
permalink: /
nav_order: 1
full_bleed: true
---

<style>
  /* Fade-in */
  @keyframes fadeInUp { from{opacity:0;transform:translateY(25px)} to{opacity:1;transform:translateY(0)} }

  /* Move down + fade-in */
  .eyebrow.shifted{
    margin-top:40px; opacity:0; transform:translateY(10px);
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

  /* HERO stacking so logo stays on top */
  .hero-video{position:relative; z-index:2; overflow:hidden;}
  .hero-overlay{position:absolute; inset:0; z-index:1;}
  .hero-content{position:relative; z-index:2;}

  /* Secondary video below hero */
  .promo-video{
    position:relative; z-index:0;
    width:100%; margin:-1270px 0 0; /* (ta valeur) */
  }
  .promo-video-frame{
    position:relative; width:100%; aspect-ratio:16/9; overflow:hidden;
    background:#000; border-top:1px solid #222; border-bottom:1px solid #222;
  }
  @supports not (aspect-ratio:16/9){
    .promo-video-frame{padding-top:56.25%}
    .promo-video-el{position:absolute;left:0;top:0;width:100%;height:100%}
  }
  .promo-video-el{
    position:absolute; inset:0; width:100%; height:100%;
    object-fit:cover; filter:brightness(.8) contrast(1.05) saturate(1.05);
  }
  .promo-scrim{
    position:absolute; inset:0;
    background:linear-gradient(180deg,rgba(0,0,0,.35) 0%,rgba(0,0,0,.55) 65%,rgba(0,0,0,.7) 100%);
    pointer-events:none;
  }

  /* ===== MONOGRAMME "SH" façon Goldman ===== */
  .hero-logo{
    position:absolute;
    right:2.2vw;
    top:44%;                 /* ← remonte le logo (45–48% selon goût) */
    transform:translateY(-44%);
    text-align:center;
    z-index:3;               /* au-dessus de tout le hero */
    opacity:0;
    animation:fadeInLogo 1.6s ease-out 1.2s forwards;
    user-select:none; pointer-events:none;
    font-family:"Times New Roman", Georgia, serif;
    line-height:.78;         /* serrer l’empilement */
  }
  .hero-logo span{
    display:block;
    font-weight:700;
    font-size:clamp(6rem, 13vw, 15rem);   /* responsive */
    color:rgba(255,255,255,.10);          /* remplissage doux */
    -webkit-text-stroke:1.5px rgba(255,255,255,.25); /* fin liseré clair */
    letter-spacing:-.04em;
  }
  /* Chevauchement subtil pour un monogramme stylé */
  .hero-logo .s{
    transform:translateX(6%);             /* décale légèrement le S */
    margin-bottom:-.22em;                 /* chevauche le H */
  }
  .hero-logo .h{
    transform:translateX(-4%);            /* léger décalage inverse */
  }

  @keyframes fadeInLogo{
    from{opacity:0; transform:translateY(-44%) translateX(40px)}
    to  {opacity:1; transform:translateY(-44%) translateX(0)}
  }

  /* Ajustements mobile */
  @media (max-width: 880px){
    .hero-logo{ right:3vw; top:46%; transform:translateY(-46%); }
    .hero-logo span{ font-size:clamp(4.5rem, 18vw, 10rem); -webkit-text-stroke:1.2px rgba(255,255,255,.22); }
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
