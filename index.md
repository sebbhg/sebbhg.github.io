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
    top: 34%;
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
    margin: -1950px 0 0;
  }
  @media (max-width: 1400px) { .promo-video { margin: -1150px 0 0; } }
  @media (max-width: 1200px) { .promo-video { margin: -1050px 0 0; } }
  @media (max-width: 1024px) { .promo-video { margin: -900px  0 0; } }
  @media (max-width: 768px)  { .promo-video { margin: -640px  0 0; } }
  @media (max-width: 560px)  { .promo-video { margin: -520px  0 0; } }

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

  /* === SECTION ACTIVITIES === */
  .activities-section{
    background:#050505; color:#ccc; text-align:center;
    padding:40px 20px 50px; border-top:1px solid #111; border-bottom:1px solid #111;
  }
  .activities-section h2,
  .activities-section .activities-title{
    color:#9ec8ff !important;                /* bleu des badges */
    -webkit-text-fill-color:#9ec8ff !important;
    filter:none !important; text-shadow:0 0 6px rgba(44,140,255,.25);
    font-size:clamp(1.5rem,3vw,2.2rem); font-weight:800; margin-bottom:.6rem;
  }
  .activities-section p{ font-size:1rem; color:#aaa; max-width:800px; margin:0 auto; line-height:1.6; }

  /* === SECTION SCROLLABLE (contenu) === */
  .after-market{
    background:#050505; color:#ccc; padding:60px 20px 180px; border-top:1px solid #111; text-align:center;
  }
  .after-market h2{ color:#2c8cff; font-size:clamp(1.6rem,3vw,2.4rem); font-weight:800; margin-bottom:1rem; }
  .after-market p{ max-width:850px; margin:0 auto 1rem; line-height:1.7; font-size:1rem; color:#aaa; }

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

<!-- ===== Activities ===== -->
<section class="activities-section">
  <div class="wrapper">
    <h2 class="activities-title" style="color:#9ec8ff !important; text-shadow:0 0 6px rgba(44,140,255,.4), 0 0 12px rgba(44,140,255,.25)">Activities</h2>
    <p>Explore the different sections of this website to discover projects, courses, theses, and readings.</p>
  </div>
</section>

<!-- ===== SECTION SCROLLABLE ===== -->
<section class="after-market">
  <div class="wrapper">
    <h2>Latest Insights & Quantitative Research</h2>
    <p>
      Explore upcoming features such as volatility surfaces, CVA dashboards, and market analytics.
      This section scrolls, so you can showcase dynamic data, visuals, and updates.
    </p>
    <p>
      Ideal for adding trading dashboards, portfolio analytics, or model visualizations.
    </p>
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
</script>
