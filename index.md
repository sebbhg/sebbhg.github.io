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

  /* === LOGO IMAGE + halo pulsé === */
  .hero-logo-img {
    position: absolute;
    right: -4.0vw;
    top: 20%;
    transform: translateY(-34%);
    z-index: 3;
    width: min(13vw, 40vh);
    height: auto;
    opacity: 0;
    animation: fadeInLogo 1.2s ease-out 1.0s forwards, logoPulse 4s ease-in-out infinite;
    pointer-events: none;
    user-select: none;
    filter: drop-shadow(0 0 6px rgba(44,140,255,.6));
  }
  @keyframes fadeInLogo {
    from { opacity: 0; transform: translateY(-34%) translateX(40px); }
    to   { opacity: 1; transform: translateY(-34%) translateX(0); }
  }
  @keyframes logoPulse {
    0%,100% { filter: drop-shadow(0 0 6px rgba(44,140,255,.6)); }
    50%     { filter: drop-shadow(0 0 14px rgba(44,140,255,.95)); }
  }

  @media (max-width: 880px) {
    .hero-logo-img {
      right: -1.2vw;
      top: 42%;
      transform: translateY(-42%);
      width: min(22vw, 34vh);
    }
  }

  /* === SECONDARY VIDEO (raccourcie pour remonter horloges & statut) === */
  .promo-video {
    position: relative;
    z-index: 0;
    width: 100%;
    margin: -1250px 0 0;
  }
  @media (max-width: 1400px) { .promo-video { margin: -1450px 0 0; } }
  @media (max-width: 1200px) { .promo-video { margin: -1350px 0 0; } }
  @media (max-width: 1024px) { .promo-video { margin: -1250px  0 0; } }
  @media (max-width: 768px)  { .promo-video { margin: -1150px  0 0; } }
  @media (max-width: 560px)  { .promo-video { margin: -1050px  0 0; } }

  .promo-video-frame {
    position: relative;
    width: 100%;
    aspect-ratio: 16/9;
    overflow: hidden;
    background: #000;
    border-top: 1px solid #222;
    border-bottom: 1px solid #222;
  }
  @supports not (aspect-ratio: 16/9) {
    .promo-video-frame { padding-top: 56.25%; }
    .promo-video-el { position: absolute; left: 0; top: 0; width: 100%; height: 100%; }
  }
  .promo-video-el {
    position: absolute; inset: 0; width: 100%; height: 100%;
    object-fit: cover; filter: brightness(.8) contrast(1.05) saturate(1.05);
  }
  .promo-scrim {
    position: absolute; inset: 0;
    background: linear-gradient(180deg,
      rgba(0,0,0,.25) 0%,
      rgba(0,0,0,.45) 55%,
      rgba(0,0,0,.7) 90%);
    pointer-events: none;
  }

  /* === WORLD CLOCK BAR — opaque, sans transparence === */
  :root { --clock-speed: 120s; }
  .world-clock-bar {
    position: relative;
    overflow: hidden;
    background: #000;
    border-top: 1px solid #333;
    border-bottom: 1px solid #333;
    padding: 12px 0;
    margin-top: -6px;
    opacity: 1;
    z-index: 10;
    isolation: isolate;
    -webkit-user-select: none; user-select: none;
    touch-action: pan-x;
  }
  .world-clock-bar * { background: none !important; opacity: 1 !important; mix-blend-mode: normal !important; filter: none !important; }

  .ticker-wrapper {
    position: relative;
    z-index: 1;
    display: flex;
    width: max-content;
    white-space: nowrap;
    animation: tickerMove var(--clock-speed) linear infinite;
    will-change: transform;
  }
  @keyframes tickerMove { 0%{transform:translateX(0);} 100%{transform:translateX(-50%);} }
  .ticker-wrapper.reverse { animation-name: tickerMoveReverse; }
  @keyframes tickerMoveReverse { 0%{transform:translateX(-50%);} 100%{transform:translateX(0);} }
  .ticker-wrapper.dragging { animation-play-state: paused; cursor: grabbing; }

  .clock { display:flex; flex-direction:column; align-items:center; justify-content:center; min-width:150px; margin:0 35px; text-align:center; }
  .clock .city {
    font-weight:900; color:#7fb3ff; text-transform:uppercase; font-size:.92rem; letter-spacing:.05em;
    text-shadow:0 0 6px rgba(0,0,0,.85);
    animation: clockPulseCity 3.6s ease-in-out infinite; animation-delay:.6s;
  }
  .clock .time {
    font-weight:900; font-size:1.28rem; color:#fff; margin-top:2px;
    text-shadow:0 0 0 #000, 0 0 8px rgba(0,0,0,1), 0 0 1px #000;
    animation: clockPulse 1.8s ease-in-out infinite;
    will-change: transform, text-shadow, opacity; transform: translateZ(0);
  }
  @keyframes clockPulse {
    0%,100% { transform: scale(1); text-shadow: 0 0 0 #000, 0 0 8px rgba(0,0,0,1), 0 0 1px #000; }
    50%     { transform: scale(1.03); text-shadow: 0 0 10px rgba(44,140,255,.9), 0 0 22px rgba(44,140,255,.6), 0 0 2px #000; }
  }
  @keyframes clockPulseCity {
    0%,100% { text-shadow: 0 0 6px rgba(0,0,0,.8); }
    50%     { text-shadow: 0 0 10px rgba(44,140,255,.7), 0 0 18px rgba(44,140,255,.35); }
  }

  /* === MARKET STATUS (sous les horloges) === */
  .market-status{
    background:#0a0a0a;
    border-top:1px solid #222;
    color:#2c8cff;
    text-align:center;
    font-weight:800;
    letter-spacing:.08em;
    padding:8px 12px;
    position: relative;
    z-index: 50;
  }
  .market-status .badge{
    display:inline-block;
    margin:0 .35rem;
    padding:.25rem .5rem;
    border-radius:.6rem;
    border:1px solid #1f3b66;
    background:#0c1220;
    color:#9ec8ff;
    font-weight:800;
  }
  .market-status .closed{ opacity:.7; color:#9aa3b2; border-color:#333; background:#0f0f0f; }
  .market-status a.badge{ text-decoration:none; cursor:pointer; pointer-events:auto; }
  .market-status a.badge:hover{ border-color:#2c8cff99; box-shadow:0 0 0 2px rgba(44,140,255,.12) inset; }

  /* ===== Bande "Latest Updates" ===== */
  .news-band{
    background:#050505;
    border-top:1px solid #111;
    border-bottom:1px solid #111;
    padding:28px 20px;
  }
  .news-wrap{
    max-width:1100px;
    margin:0 auto;
    display:grid;
    grid-template-columns: 1fr 1fr;
    gap:18px;
  }
  .update-card{
    position:relative; background:#0d0d0d; border:1px solid #222; border-radius:14px;
    padding:18px 18px 16px; box-shadow:0 10px 30px rgba(0,0,0,.25);
    transition:transform .18s ease, box-shadow .18s ease, border-color .18s ease;
  }
  .update-card::after{
    content:""; position:absolute; inset:-1px; border-radius:14px; pointer-events:none;
    background:radial-gradient(600px 200px at 20% -20%, rgba(44,140,255,.15), transparent 70%); opacity:.7;
  }
  .update-card:hover{ transform:translateY(-2px); box-shadow:0 14px 36px rgba(0,0,0,.35); border-color:#2c8cff55; }
  .update-badge{
    display:inline-block; font-size:.72rem; letter-spacing:.08em; color:#9ec8ff;
    background:#0c1220; border:1px solid #1f3b66; border-radius:999px; padding:4px 8px; margin-bottom:10px; font-weight:800;
  }
  .update-title{ margin:0 0 6px; font-size:clamp(1.05rem,2.2vw,1.2rem); font-weight:800; }
  .update-meta{ color:#9aa3b2; font-size:.9rem; margin:0 0 10px; }
  .update-desc{ color:#c9cbd1; margin:0 0 12px; line-height:1.55; }
  .update-link{ display:inline-flex; align-items:center; gap:8px; padding:8px 10px; border:1px solid rgba(255,255,255,.16); border-radius:10px; background:#0f0f0f; color:#fff; font-weight:700; text-decoration:none; }
  .update-link:hover{ border-color:#4da0ff; background:#141414; }
  @media (max-width:820px){ .news-wrap{ grid-template-columns: 1fr; } }

  /* === SECTION ACTIVITIES (petit bloc sous les updates) === */
  .activities-section{
    background:#050505; color:#ccc; text-align:center;
    padding:40px 20px 50px; border-top:1px solid #111; border-bottom:1px solid #111;
  }
  .activities-section h2,
  .activities-section .activities-title{
    color:#9ec8ff !important;
    -webkit-text-fill-color:#9ec8ff !important;
    filter:none !important; text-shadow:0 0 6px rgba(44,140,255,.25);
    font-size:clamp(1.5rem,3vw,2.2rem); font-weight:800; margin-bottom:.6rem;
  }
  .activities-section p{ font-size:1rem; color:#aaa; max-width:800px; margin:0 auto; line-height:1.6; }

  /* === SECTION HUB (remplace "Latest Insights & Quantitative Research") === */
  .after-market{
    background:#050505; color:#ccc; padding:60px 20px 120px; border-top:1px solid #111;
  }
  .hub-inner{
    max-width:1100px; margin:0 auto;
  }
  .hub-eyebrow{
    color:#9aa3b2; font-weight:800; letter-spacing:.08em; text-transform:uppercase;
    margin:0 0 10px; text-align:left;
  }
  .hub-title{
    color:#fff; font-size:clamp(1.8rem,4vw,2.8rem); font-weight:900; line-height:1.1;
    margin:0 0 16px; text-align:left; text-shadow:0 0 10px rgba(0,0,0,.35);
  }
  .hub-sub{
    color:#9aa3b2; margin:0 0 20px; text-align:left; font-weight:700;
  }

  .hub-tabs{
    display:flex; gap:22px; flex-wrap:wrap;
    align-items:center; justify-content:flex-start;
    padding:8px 0 10px; border-bottom:1px solid #1a1a1a; margin-bottom:14px;
  }
  .hub-tab{
    position:relative; display:inline-block; cursor:pointer;
    font-weight:800; letter-spacing:.02em; text-decoration:none;
    color:#cfd6e4; padding:4px 2px;
  }
  .hub-tab:hover{ color:#ffffff; }
  .hub-tab.is-active{ color:#ffffff; }
  .hub-tab.is-active::after{
    content:""; position:absolute; left:0; right:0; bottom:-10px; height:3px;
    background:#2c8cff; border-radius:3px; box-shadow:0 0 12px rgba(44,140,255,.55);
  }

  /* === Titre dynamique sous le liseré bleu === */
  .hub-selected-title{
    margin:14px 0 6px;
    color:#fff;
    font-weight:900;
    letter-spacing:.06em;
    text-transform:uppercase;
    text-align:left;
    font-size:clamp(1.1rem,3vw,1.75rem);
  }

  .hub-panel{
    margin-top:8px;
    color:#c9cbd1; line-height:1.65; max-width:850px; text-align:justify;
  }

  /* === SURCHARGES: étendre la largeur de la section "Activities" === */
  .after-market .hub-inner{
    max-width: none;
    width: 100%;
    margin: 0;
  }
  .after-market .hub-panel{
    max-width: none;
  }
  .after-market{
    padding-left: 24px;
    padding-right: 24px;
  }

  /* === GALLERY PLEIN ÉCRAN (1 image, tilt + overlay) === */
  .hub-gallery{
    position: relative;
    width: min(88vw, 1200px);
    margin: 0 auto;   /* centre la galerie horizontalement */
    left: auto;
    right: auto;
    display: grid;
    grid-template-columns: 1fr;
    gap: 0;
    perspective: 900px;
    margin-top: 12px;
    margin-bottom: 36px;
  }
  .hub-gallery figure{
    position:relative;
    width:100%;
    aspect-ratio: 21/9;           /* paysage cinématique */
    overflow:hidden;
    border-radius:14px;
    background:#0a0a0a;
    border:1px solid #1f2333;
    box-shadow:0 10px 30px rgba(0,0,0,.35);
    transform-style: preserve-3d;
    transition: transform .25s ease, box-shadow .25s ease, border-color .25s ease;
  }
  .hub-gallery img{
    width:100%; height:100%; object-fit:cover;
    transition:transform .6s ease, filter .6s ease;
    filter:brightness(.95) contrast(1.08) saturate(1.05);
    display:block;
    transform: translateZ(0);
  }
  .hub-gallery figcaption{
    position:absolute; inset:0;
    display:flex; align-items:flex-end;
    padding:22px;
    background: linear-gradient(to top, rgba(10,18,36,.85) 0%, rgba(10,18,36,.35) 40%, transparent 70%);
    color:#e7f1ff;
    font-weight:800;
    letter-spacing:.04em;
    text-transform:uppercase;
    opacity:0; transform: translateY(8px);
    transition: opacity .35s ease, transform .35s ease;
    pointer-events:none;
  }
  .hub-gallery figcaption .caption-inner{
    backdrop-filter: blur(3px);
    padding:10px 12px;
    border-radius:10px;
    border:1px solid rgba(76,139,255,.35);
    background: rgba(15,22,40,.45);
    box-shadow:0 0 28px rgba(44,140,255,.25) inset;
  }
  .hub-gallery figure::after{
    content:"";
    position:absolute; inset:-1px; border-radius:14px; pointer-events:none;
    background: radial-gradient(900px 260px at 20% -20%, rgba(44,140,255,.18), transparent 70%);
    opacity:.0; transition: opacity .35s ease;
  }
  .hub-gallery figure:hover{
    box-shadow:0 16px 42px rgba(0,0,0,.45);
    border-color:#2c8cff55;
  }
  .hub-gallery figure:hover img{
    transform: scale(1.04);
    filter:brightness(1.05) contrast(1.08) saturate(1.1);
  }
  .hub-gallery figure:hover figcaption{
    opacity:1; transform: translateY(0);
  }
  .hub-gallery figure:hover::after{ opacity:.9; }

  @media (max-width:900px){
    .hub-gallery figure{ aspect-ratio: 16/9; }
  }

  /* au-dessus du footer */
  .news-band, .activities-section, .after-market { position: relative; z-index: 3; }
</style>

<section class="hero-video">
  <video class="hero-bg" autoplay muted loop playsinline preload="auto"
         poster="{{ '/assets/images/hero-poster.jpg' | relative_url }}">
    <source src="{{ '/assets/videos/trading-hero.mp4' | relative_url }}" type="video/mp4">
  </video>
  <div class="hero-overlay"></div>

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

<!-- ===== World Clocks ===== -->
<div class="world-clock-bar" id="clockBar">
  <div class="ticker-wrapper" id="clockTicker">
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

    <!-- Copie pour défilement infini -->
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

<!-- ===== Market Status ===== -->
<div class="market-status" id="marketStatus">Loading market status…</div>

<!-- ===== Latest Updates ===== -->
<section class="news-band">
  <div class="news-wrap">
    <article class="update-card">
      <span class="update-badge">INFO</span>
      <h3 class="update-title">Website under construction 🚧</h3>
      <p class="update-meta">Oct 2025 · Ongoing</p>
      <p class="update-desc">
        This website is currently being enhanced — new pages, animations, and live data integrations are coming soon.
        Stay tuned for the full Quantitative Finance & Trading experience.
      </p>
      <a class="update-link" href="{{ '/' | relative_url }}">Learn more →</a>
    </article>

    <article class="update-card">
      <span class="update-badge">UPDATE</span>
      <h3 class="update-title">What I do — Quant Engineering</h3>
      <p class="update-meta">Oct 2025 · Labs</p>
      <p class="update-desc">
        New “What I do” page: pricing engines, risk aggregation, intraday analytics and
        research notes. Coming next: CVA dashboard & volatility surface explorer.
      </p>
      <a class="update-link" href="{{ '/what-i-do' | relative_url }}">Open page →</a>
    </article>
  </div>
</section>

<!-- ===== Activities (petit bloc) ===== -->
<section class="activities-section">
  <div class="wrapper">
    <h2 class="activities-title" style="color:#9ec8ff !important; text-shadow:0 0 6px rgba(44,140,255,.4), 0 0 12px rgba(44,140,255,.25)">About my WebSite</h2>
    <p>On this website, you will find a wide range of content related to quantitative finance: courses, projects, analyses, interactive tools, and personal insights. The goal is to share diverse resources covering financial modeling, risk theory, portfolio optimization, and machine learning, offering a comprehensive exploration of modern finance from a quantitative and applied perspective.</p>
  </div>
</section>

<!-- ===== SECTION HUB (tabs) ===== -->
<section class="after-market">
  <div class="hub-inner">
    <p class="hub-eyebrow">The different sections</p>
    <h2 class="hub-title">Activities</h2>

    <nav class="hub-tabs" id="hubTabs" aria-label="Sections">
      <a class="hub-tab is-active" data-tab="what" href="#what" role="tab" aria-selected="true">What I do</a>
      <a class="hub-tab" data-tab="courses" href="#courses" role="tab" aria-selected="false">Courses</a>
      <a class="hub-tab" data-tab="projects" href="#projects" role="tab" aria-selected="false">Projects</a>
      <a class="hub-tab" data-tab="reading" href="#reading" role="tab" aria-selected="false">Reading</a>
    </nav>

    <!-- Titre dynamique sous les onglets -->
    <h3 class="hub-selected-title" id="hubSelectedTitle">WHAT I DO</h3>

    <!-- === GALLERY FULL-WIDTH (1 image paysage) === -->
    <div class="hub-gallery" id="hubGallery">
      <figure class="figure-tilt">
        <img src="/assets/images/image5.png" alt="New York at night — market activity overlay">
        <figcaption>
          <div class="caption-inner">Background</div>
        </figcaption>
      </figure>
    </div>

    <!-- Contenu initial long (WHAT I DO) -->
    <div class="hub-panel" id="hubPanel" role="region" aria-live="polite">
      <p>
        My quantitative journey began with a fascination for how mathematical models could explain and anticipate financial behavior. Over the years, I have progressively refined this passion, evolving from building valuation spreadsheets and market indicators to designing full-fledged pricing and risk-management systems.
      </p>

      <p>
        During my early experience at <strong>Société Générale Corporate & Investment Banking</strong>, I worked within the portfolio valuation team on the automation of fund and derivative pricing processes. I developed <em>Monte Carlo valuation tools</em> for structured funds and improved daily PnL explainability through dynamic volatility adjustments and systematic stress testing. This exposure to large-scale data and front-to-risk integration taught me the fundamentals of financial modeling reliability and auditability, critical pillars of any risk engine.
      </p>

      <p>
        I then joined <strong>Spread Research</strong> as a <em>Quantitative Analyst Intern</em>, where I focused on <strong>equity derivatives</strong> and market microstructure. My work involved building analytical tools for <em>volatility surface calibration</em>, pricing exotic options using <em>Monte Carlo</em> and <em>finite-difference methods</em>, and exploring hedging strategies such as gamma scalping and delta-neutral positioning. I also studied the dynamics of volatility smiles and skews across maturities, enhancing my understanding of option sensitivities and implied risk premia. This phase solidified my link between mathematical models and their behavior under real market stress.
      </p>

      <p>
        Today, I work at <strong>Natixis Corporate & Investment Banking</strong> within the <em>Market & Counterparty Risk Modelling (MCRM)</em> team. My mission is to develop and optimize CVA and XVA models under the <em>Linear Gaussian Model (LGM-1F)</em> framework. I designed a full <strong>CVA engine</strong> integrating zero-coupon bootstrapping, exposure simulation, and analytical estimation of sensitivities. I implemented <em>Gaussian Process Regression (GPR)</em> and <em>Bayesian Quadrature (BQ)</em> methods to approximate Delta, Gamma, Vega, Theta, and Cega, achieving highly stable results with strong computational efficiency. Beyond model development, I also work on <strong>multi-currency frameworks</strong>, curve construction for swap and cross-currency portfolios, and advanced analytics dashboards for traders and risk officers.
      </p>

      <p>
        My academic background bridges <strong>engineering and applied mathematics</strong>. I graduated from <strong>CY Tech (formerly EISTI)</strong> with a master’s degree in <em>Financial Mathematics and Quantitative Engineering</em>. My coursework covered <em>stochastic processes, Ito calculus, Monte Carlo methods, machine learning, and portfolio optimization</em>. I also conducted research on <em>portfolio selection under incomplete markets</em> using log-utility maximization, and on <em>volatility surface reconstruction</em> through Heston and SABR calibration. These studies strengthened both my mathematical intuition and my ability to design robust numerical schemes.
      </p>

      <p>
        In parallel, I continuously enhance my professional toolkit through certification and self-directed learning. I am a <strong>CFA Level I Holder</strong>, actively pursuing Level II, and I frequently explore academic research in <em>stochastic modeling</em>, <em>Bayesian inference</em>, and <em>deep learning for derivatives pricing</em>. I write Python libraries that implement curve bootstrapping, exposure computation, and neural approximations of pricing functions, bridging quantitative theory and market execution.
      </p>

      <p>
        My overarching goal is simple: to turn quantitative elegance into practical trading impact. Every model, dataset, or codebase I build serves one purpose, enabling better, faster, and more transparent decisions in modern financial markets.
      </p>
    </div>
  </div>
</section>

<script>
/* === Horloges === */
function updateClocks(){
  document.querySelectorAll('.clock').forEach(el=>{
    const city = el.dataset.city;
    const tz = el.dataset.tz;
    const now = new Date().toLocaleTimeString('en-GB', {
      timeZone: tz, hour:'2-digit', minute:'2-digit', hour12:false
    });
    el.innerHTML = `<span class="city">${city}</span><span class="time">${now}</span>`;
  });
}
updateClocks(); setInterval(updateClocks, 1000);

/* === Drag ticker === */
(function(){
  const bar  = document.getElementById('clockBar');
  const wrap = document.getElementById('clockTicker');
  let isDown=false, startX=0;
  const speedFromDx = dx => (Math.max(12, Math.min(120, 120 - (Math.min(Math.abs(dx),600)/600)*108)).toFixed(0)+'s');
  function onPointerDown(e){ isDown=true; wrap.classList.add('dragging'); startX=(e.touches?e.touches[0].clientX:e.clientX); }
  function onPointerMove(e){
    if(!isDown) return;
    const x=(e.touches?e.touches[0].clientX:e.clientX);
    const dx=x-startX;
    wrap.classList.toggle('reverse', dx>0);
    document.documentElement.style.setProperty('--clock-speed', speedFromDx(dx));
    e.preventDefault();
  }
  function onPointerUp(){ if(!isDown) return; isDown=false; wrap.classList.remove('dragging','reverse'); document.documentElement.style.setProperty('--clock-speed','120s'); }
  bar.addEventListener('mousedown', onPointerDown);
  window.addEventListener('mousemove', onPointerMove, { passive:false });
  window.addEventListener('mouseup', onPointerUp);
  bar.addEventListener('touchstart', onPointerDown, { passive:true });
  window.addEventListener('touchmove', onPointerMove, { passive:false });
  window.addEventListener('touchend', onPointerUp);
})();

/* === Market Status (Tokyo / London / Paris / New York) === */
(function(){
  const el = document.getElementById('marketStatus');
  if(!el) return;

  function isWeekday(tz){
    const day = new Intl.DateTimeFormat('en-US', { weekday:'short', timeZone:tz }).format(new Date());
    return day !== 'Sat' && day !== 'Sun';
  }
  function hmInTZ(tz){
    const parts = new Intl.DateTimeFormat('en-GB', { hour:'2-digit', minute:'2-digit', hour12:false, timeZone:tz }).formatToParts(new Date());
    const h = parseInt(parts.find(p=>p.type==='hour').value,10);
    const m = parseInt(parts.find(p=>p.type==='minute').value,10);
    return { h, m, t: h*60+m };
  }
  function isOpenTokyo(){ if(!isWeekday('Asia/Tokyo')) return false; const {t}=hmInTZ('Asia/Tokyo'); return t>=540 && t<900; }
  function isOpenLondon(){ if(!isWeekday('Europe/London')) return false; const {t}=hmInTZ('Europe/London'); return t>=480 && t<960; }
  function isOpenParis(){ if(!isWeekday('Europe/Paris')) return false; const {t}=hmInTZ('Europe/Paris'); return t>=540 && t<1020; }
  function isOpenNewYork(){ if(!isWeekday('America/New_York')) return false; const {t}=hmInTZ('America/New_York'); return t>=(9*60+30) && t<960; }

  function refresh(){
    const tokyo=isOpenTokyo(), london=isOpenLondon(), paris=isOpenParis(), ny=isOpenNewYork();
    const urls={ tokyo:"https://www.jpx.co.jp/english/markets/", london:"https://www.londonstockexchange.com/", paris:"https://live.euronext.com/en/markets/paris", ny:"https://www.nyse.com/" };
    const badge=(isOpen,label,url)=> isOpen ? `<a class="badge" href="${url}" target="_blank" rel="noopener noreferrer">${label} LIVE</a>` : `<span class="badge closed">${label} CLOSED</span>`;
    el.innerHTML = `${badge(tokyo,'TOKYO',urls.tokyo)} ${badge(london,'LONDON',urls.london)} ${badge(paris,'PARIS',urls.paris)} ${badge(ny,'NEW YORK',urls.ny)}`;
  }
  refresh(); setInterval(refresh, 60_000);
})();

/* === Tabs: Our Activities + galerie visible pour "what" === */
(function(){
  const tabs = document.querySelectorAll('.hub-tab');
  const panel = document.getElementById('hubPanel');
  const titleEl = document.getElementById('hubSelectedTitle');
  const gallery = document.getElementById('hubGallery');
  if(!tabs.length || !panel || !titleEl) return;

  const copy = {
    what: `
      <p>
        My quantitative journey began with a fascination for how mathematical models could explain and anticipate financial behavior. Over the years, I have progressively refined this passion — evolving from building valuation spreadsheets and market indicators to designing full-fledged pricing and risk-management systems.
      </p>
      <p>
        During my early experience at <strong>Société Générale Corporate & Investment Banking</strong>, I worked within the portfolio valuation team on the automation of fund and derivative pricing processes. I developed <em>Monte Carlo valuation tools</em> for structured funds and improved daily PnL explainability through dynamic volatility adjustments and systematic stress testing. This exposure to large-scale data and front-to-risk integration taught me the fundamentals of financial modeling reliability and auditability — critical pillars of any risk engine.
      </p>
      <p>
        I then joined <strong>Spread Research</strong> as a <em>Quantitative Analyst Intern</em>, where I focused on <strong>equity derivatives</strong> and market microstructure. My work involved building analytical tools for <em>volatility surface calibration</em>, pricing exotic options using <em>Monte Carlo</em> and <em>finite-difference methods</em>, and exploring hedging strategies such as gamma scalping and delta-neutral positioning. I also studied the dynamics of volatility smiles and skews across maturities, enhancing my understanding of option sensitivities and implied risk premia. This phase solidified my link between mathematical models and their behavior under real market stress.
      </p>
      <p>
        Today, I work at <strong>Natixis Corporate & Investment Banking</strong> within the <em>Market & Counterparty Risk Modelling (MCRM)</em> team. My mission is to develop and optimize CVA and XVA models under the <em>Linear Gaussian Model (LGM-1F)</em> framework. I designed a full <strong>CVA engine</strong> integrating zero-coupon bootstrapping, exposure simulation, and analytical estimation of sensitivities. I implemented <em>Gaussian Process Regression (GPR)</em> and <em>Bayesian Quadrature (BQ)</em> methods to approximate Delta, Gamma, Vega, Theta, and Cega — achieving highly stable results with strong computational efficiency. Beyond model development, I also work on <strong>multi-currency frameworks</strong>, curve construction for swap and cross-currency portfolios, and advanced analytics dashboards for traders and risk officers.
      </p>
      <p>
        My academic background bridges <strong>engineering and applied mathematics</strong>. I graduated from <strong>CY Tech (formerly EISTI)</strong> with a master’s degree in <em>Financial Mathematics and Quantitative Engineering</em>. My coursework covered <em>stochastic processes, Ito calculus, Monte Carlo methods, machine learning, and portfolio optimization</em>. I also conducted research on <em>portfolio selection under incomplete markets</em> using log-utility maximization, and on <em>volatility surface reconstruction</em> through Heston and SABR calibration. These studies strengthened both my mathematical intuition and my ability to design robust numerical schemes.
      </p>
      <p>
        In parallel, I continuously enhance my professional toolkit through certification and self-directed learning. I am a <strong>CFA Level I Holder</strong>, actively pursuing Level II, and I frequently explore academic research in <em>stochastic modeling</em>, <em>Bayesian inference</em>, and <em>deep learning for derivatives pricing</em>. I write Python libraries that implement curve bootstrapping, exposure computation, and neural approximations of pricing functions — bridging quantitative theory and market execution.
      </p>
      <p>
        My overarching goal is simple: to turn quantitative elegance into practical trading impact. Every model, dataset, or codebase I build serves one purpose — enabling better, faster, and more transparent decisions in modern financial markets.
      </p>
    `,
    courses: `Courses and notes that structure the core of my quantitative toolkit: probability, stochastic processes, optimization, numerical methods, derivatives, and machine learning — with short summaries and exercises.`,
    projects: `Hands-on projects that combine data, models and code: pricing prototypes, risk analytics, portfolio research and microstructure experiments. Each project highlights the problem, approach and results.`,
    reading: `Curated reading lists and annotations across papers, textbooks and articles that influenced my thinking on modeling, risk, markets and systems design.`
  };

  function activate(key, labelUpper){
    tabs.forEach(t=>{
      const isActive = t.dataset.tab === key;
      t.classList.toggle('is-active', isActive);
      t.setAttribute('aria-selected', isActive ? 'true' : 'false');
    });
    titleEl.textContent = labelUpper;
    panel.innerHTML = copy[key] || '';
    if (gallery){ gallery.style.display = (key === 'what') ? 'grid' : 'none'; }
  }

  /* Init */
  activate('what', 'WHAT I DO');
  tabs.forEach(t => t.addEventListener('click', (e)=>{
    e.preventDefault();
    activate(t.dataset.tab, t.textContent.trim().toUpperCase());
  }));
})();

/* === Effet tilt 3D léger sur l'image === */
(function(){
  const cards = document.querySelectorAll('.figure-tilt');
  const clamp = (v,min,max)=>Math.max(min,Math.min(max,v));
  cards.forEach(card=>{
    let rAF;
    function onMove(e){
      const rect = card.getBoundingClientRect();
      const clientX = (e.clientX ?? (e.touches&&e.touches[0].clientX));
      const clientY = (e.clientY ?? (e.touches&&e.touches[0].clientY));
      if (clientX==null || clientY==null) return;
      const x = clientX - rect.left;
      const y = clientY - rect.top;
      const rx = clamp(((y/rect.height)-0.5)*6,-6,6);
      const ry = clamp(((x/rect.width)-0.5)*-9,-9,9);
      cancelAnimationFrame(rAF);
      rAF = requestAnimationFrame(()=>{
        card.style.transform = `rotateX(${rx}deg) rotateY(${ry}deg)`;
      });
    }
    function reset(){ card.style.transform = 'rotateX(0deg) rotateY(0deg)'; }
    card.addEventListener('mousemove', onMove, {passive:true});
    card.addEventListener('mouseleave', reset);
    card.addEventListener('touchmove', onMove, {passive:true});
    card.addEventListener('touchend', reset);
  });
})();
</script>
