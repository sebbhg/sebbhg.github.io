---
layout: default
title: Home
permalink: /
nav_order: 1
full_bleed: true
---

<style>
  /* === Fade-in global === */
  @keyframes fadeInUp {
    from { opacity: 0; transform: translateY(25px); }
    to { opacity: 1; transform: translateY(0); }
  }

  /* === Hero titles fade-in === */
  .eyebrow.shifted {
    margin-top: -25px;
    opacity: 0;
    transform: translateY(10px);
    animation: fadeInUp 1.4s ease-out .3s forwards;
  }
  .hero-content h1 {
    opacity: 0;
    transform: translateY(20px);
    animation: fadeInUp 1.4s ease-out .8s forwards;
  }
  .hero-content .subtitle {
    opacity: 0;
    transform: translateY(20px);
    animation: fadeInUp 1.4s ease-out 1.3s forwards;
  }

  /* === HERO LAYERS === */
  .hero-video { position: relative; z-index: 2; overflow: hidden; }
  .hero-overlay { position: absolute; inset: 0; z-index: 1; }
  .hero-content { position: relative; z-index: 2; }

  /* === LOGO IMAGE === */
  .hero-logo-img {
    position: absolute;
    right: -4.0vw;
    top: 34%;
    transform: translateY(-34%);
    z-index: 3;
    width: min(13vw, 40vh);
    height: auto;
    opacity: 0;
    animation: fadeInLogo 1.2s ease-out 1.0s forwards;
    pointer-events: none;
    user-select: none;
  }
  @keyframes fadeInLogo {
    from { opacity: 0; transform: translateY(-34%) translateX(40px); }
    to { opacity: 1; transform: translateY(-34%) translateX(0); }
  }
  @media (max-width: 880px) {
    .hero-logo-img {
      right: -1.2vw;
      top: 42%;
      transform: translateY(-42%);
      width: min(22vw, 34vh);
    }
  }

  /* === SECONDARY VIDEO === */
  .promo-video {
    position: relative;
    z-index: 0;              /* ⬅ ensure below clocks */
    width: 100%;
    margin: -1250px 0 0;
  }
  .promo-video-frame {
    position: relative;
    width: 100%;
    aspect-ratio: 16/9;
    overflow: hidden;
    background: #000;
    border-top: 1px solid #222;
    border-bottom: 1px solid #222;
    z-index: 0;              /* ⬅ ensure below clocks */
  }
  @supports not (aspect-ratio: 16/9) {
    .promo-video-frame { padding-top: 56.25%; }
    .promo-video-el {
      position: absolute;
      left: 0;
      top: 0;
      width: 100%;
      height: 100%;
    }
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
    background: linear-gradient(180deg,
      rgba(0, 0, 0, .35) 0%,
      rgba(0, 0, 0, .55) 65%,
      rgba(0, 0, 0, .7) 100%);
    pointer-events: none;
    z-index: 0;              /* ⬅ ensure below clocks */
  }

  /* === WORLD CLOCK BAR (zéro transparence, fond noir, défilement fluide) === */
  .world-clock-bar{
    position: relative;
    overflow: hidden;
    background:#000 !important;     /* fond 100% noir */
    border-top:1px solid #333;
    border-bottom:1px solid #333;
    padding:12px 0;
    margin-top:-6px;
    opacity:1 !important;
    mix-blend-mode:normal !important;
    isolation:isolate;              /* évite tout mélange avec la vidéo */
    z-index: 5;                     /* au-dessus de la promo-video */
  }
  .world-clock-bar::before{
    content:"";
    position:absolute; inset:0;
    background:#000;                /* couche noire additionnelle */
    opacity:1;
    z-index:0;
  }

  .ticker-wrapper{
    position:relative;
    z-index:2;                      /* texte au-dessus du fond noir */
    display:flex;
    width:max-content;
    white-space:nowrap;
    animation:tickerMove 90s linear infinite;
    opacity:1 !important;
    filter:none !important;
    mix-blend-mode:normal !important;
    backface-visibility:hidden;     /* stabilité rendu */
    will-change:transform;
  }

  @keyframes tickerMove{
    0%{transform:translateX(0);}
    100%{transform:translateX(-50%);}
  }

  .clock{
    display:flex;
    flex-direction:column;
    align-items:center;
    justify-content:center;
    min-width:150px;
    margin:0 35px;
    text-align:center;
    opacity:1 !important;
    filter:none !important;
    mix-blend-mode:normal !important;
    -webkit-font-smoothing:antialiased;
    text-rendering:optimizeLegibility;
    z-index:3;
  }

  .clock .city{
    font-weight:900;
    color:#9ec8ff !important;  /* bleu clair intense et opaque */
    text-transform:uppercase;
    font-size:.92rem;
    letter-spacing:.05em;
    opacity:1 !important;
    text-shadow:0 0 6px rgba(0,0,0,.9);
  }

  .clock .time{
    font-weight:900;
    font-size:1.28rem;
    color:#ffffff !important;  /* blanc pur forcé */
    margin-top:2px;
    opacity:1 !important;
    text-shadow:
      0 0 0 #000,
      0 0 8px rgba(0,0,0,1),
      0 0 1px #000;
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

<!-- ===== World Clocks Continuous Ticker ===== -->
<div class="world-clock-bar">
  <div class="ticker-wrapper" id="clockTicker">
    <!-- Première série -->
    <div class="clock" data-city="New York" data-tz="America/New_York"></div>
    <div class="clock" data-city="Chicago" data-tz="America/Chicago"></div>
    <div class="clock" data-city="Los Angeles" data-tz="America/Los_Angeles"></div>
    <div class="clock" data-city="London" data-tz="Europe/London"></div>
    <div class="clock" data-city="Paris" data-tz="Europe/Paris"></div>
    <div class="clock" data-city="Zurich" data-tz="Europe/Zurich"></div>
    <div class="clock" data-city="Dubai" data-tz="Asia/Dubai"></div>
    <div class="clock" data-city="Mumbai" data-tz="Asia/Kolkata"></div>
    <div class="clock" data-city="Singapore" data-tz="Asia/Singapore"></div>
    <div class="clock" data-city="Hong Kong" data-tz="Asia/Hong_Kong"></div>
    <div class="clock" data-city="Tokyo" data-tz="Asia/Tokyo"></div>
    <div class="clock" data-city="Sydney" data-tz="Australia/Sydney"></div>
    <div class="clock" data-city="São Paulo" data-tz="America/Sao_Paulo"></div>
    <div class="clock" data-city="Toronto" data-tz="America/Toronto"></div>

    <!-- Copie exacte pour défilement infini -->
    <div class="clock" data-city="New York" data-tz="America/New_York"></div>
    <div class="clock" data-city="Chicago" data-tz="America/Chicago"></div>
    <div class="clock" data-city="Los Angeles" data-tz="America/Los_Angeles"></div>
    <div class="clock" data-city="London" data-tz="Europe/London"></div>
    <div class="clock" data-city="Paris" data-tz="Europe/Paris"></div>
    <div class="clock" data-city="Zurich" data-tz="Europe/Zurich"></div>
    <div class="clock" data-city="Dubai" data-tz="Asia/Dubai"></div>
    <div class="clock" data-city="Mumbai" data-tz="Asia/Kolkata"></div>
    <div class="clock" data-city="Singapore" data-tz="Asia/Singapore"></div>
    <div class="clock" data-city="Hong Kong" data-tz="Asia/Hong_Kong"></div>
    <div class="clock" data-city="Tokyo" data-tz="Asia/Tokyo"></div>
    <div class="clock" data-city="Sydney" data-tz="Australia/Sydney"></div>
    <div class="clock" data-city="São Paulo" data-tz="America/Sao_Paulo"></div>
    <div class="clock" data-city="Toronto" data-tz="America/Toronto"></div>
  </div>
</div>

<script>
function updateClocks(){
  document.querySelectorAll('.clock').forEach(el=>{
    const city = el.dataset.city;
    const tz = el.dataset.tz;
    const now = new Date().toLocaleTimeString('en-GB', {
      timeZone: tz,
      hour: '2-digit',
      minute: '2-digit',
      hour12: false
    });
    el.innerHTML = `<span class="city">${city}</span><span class="time">${now}</span>`;
  });
}
updateClocks();
setInterval(updateClocks, 1000);
</script>
