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

  /* === SECONDARY VIDEO === */
  .promo-video {
    position: relative;
    z-index: 0;
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
    background: linear-gradient(180deg, rgba(0,0,0,.35) 0%, rgba(0,0,0,.55) 65%, rgba(0,0,0,.7) 100%);
    pointer-events: none;
  }

  /* === WORLD CLOCK BAR === */
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
  .world-clock-bar * {
    background: none !important;
    opacity: 1 !important;
    mix-blend-mode: normal !important;
    filter: none !important;
  }

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

  .clock {
    display: flex; flex-direction: column; align-items: center; justify-content: center;
    min-width: 150px; margin: 0 35px; text-align: center;
  }
  .clock .city {
    font-weight: 900; color: #7fb3ff; text-transform: uppercase;
    font-size: .92rem; letter-spacing: .05em;
    text-shadow: 0 0 6px rgba(0,0,0,.85);
    animation: clockPulseCity 3.6s ease-in-out infinite; animation-delay: .6s;
  }
  .clock .time {
    font-weight: 900; font-size: 1.28rem; color: #fff; margin-top: 2px;
    text-shadow: 0 0 0 #000, 0 0 8px rgba(0,0,0,1), 0 0 1px #000;
    animation: clockPulse 1.8s ease-in-out infinite;
  }
  @keyframes clockPulse {
    0%, 100% { transform: scale(1); text-shadow: 0 0 0 #000, 0 0 8px rgba(0,0,0,1), 0 0 1px #000; }
    50%      { transform: scale(1.03); text-shadow: 0 0 10px rgba(44,140,255,.9), 0 0 22px rgba(44,140,255,.6), 0 0 2px #000; }
  }
  @keyframes clockPulseCity {
    0%, 100% { text-shadow: 0 0 6px rgba(0,0,0,.8); }
    50%      { text-shadow: 0 0 10px rgba(44,140,255,.7), 0 0 18px rgba(44,140,255,.35); }
  }

  /* === MARKET STATUS === */
  .market-status{
    background:#0a0a0a;
    border-top:1px solid #222;
    border-bottom:1px solid #222;
    color:#2c8cff;
    text-align:center;
    font-weight:800;
    letter-spacing:.08em;
    padding:8px 12px;
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

  /* === SECTION SCROLLABLE === */
  .after-market{
    background:#050505;
    color:#ccc;
    padding:100px 20px 180px;
    border-top:1px solid #111;
    text-align:center;
  }
  .after-market h2{
    color:#2c8cff;
    font-size:clamp(1.6rem,3vw,2.4rem);
    font-weight:800;
    margin-bottom:1rem;
  }
  .after-market p{
    max-width:850px;
    margin:0 auto 1rem;
    line-height:1.7;
    font-size:1rem;
    color:#aaa;
  }
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

<section class="promo-video">
  <div class="promo-video-frame">
    <video class="promo-video-el" autoplay muted loop playsinline preload="auto"
           poster="/assets/images/trading-broll-poster.jpg">
      <source src="/assets/videos/trading-broll.mp4" type="video/mp4">
    </video>
    <div class="promo-scrim"></div>
  </div>
</section>

<div class="world-clock-bar" id="clockBar">
  <div class="ticker-wrapper" id="clockTicker">
    <div class="clock" data-city="New York" data-tz="America/New_York"></div>
    <div class="clock" data-city="London" data-tz="Europe/London"></div>
    <div class="clock" data-city="Paris" data-tz="Europe/Paris"></div>
    <div class="clock" data-city="Tokyo" data-tz="Asia/Tokyo"></div>
    <div class="clock" data-city="Hong Kong" data-tz="Asia/Hong_Kong"></div>
    <div class="clock" data-city="Sydney" data-tz="Australia/Sydney"></div>
    <div class="clock" data-city="New York" data-tz="America/New_York"></div>
    <div class="clock" data-city="London" data-tz="Europe/London"></div>
    <div class="clock" data-city="Paris" data-tz="Europe/Paris"></div>
    <div class="clock" data-city="Tokyo" data-tz="Asia/Tokyo"></div>
  </div>
</div>

<div class="market-status" id="marketStatus">Loading market status…</div>

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
updateClocks(); setInterval(updateClocks,1000);

/* === Drag horloge === */
(function(){
  const root=document.documentElement,bar=document.getElementById('clockBar'),wrap=document.getElementById('clockTicker');
  let down=false,startX=0;
  function speed(dx){const a=Math.min(Math.abs(dx),600);return(Math.max(12,120-(a/600)*108)).toFixed(0)+'s';}
  function downFn(e){down=true;wrap.classList.add('dragging');startX=(e.touches?e.touches[0].clientX:e.clientX);}
  function moveFn(e){if(!down)return;const x=(e.touches?e.touches[0].clientX:e.clientX),dx=x-startX;wrap.classList.toggle('reverse',dx>0);root.style.setProperty('--clock-speed',speed(dx));e.preventDefault();}
  function upFn(){if(!down)return;down=false;wrap.classList.remove('dragging','reverse');root.style.setProperty('--clock-speed','120s');}
  bar.addEventListener('mousedown',downFn);window.addEventListener('mousemove',moveFn,{passive:false});window.addEventListener('mouseup',upFn);
  bar.addEventListener('touchstart',downFn,{passive:true});window.addEventListener('touchmove',moveFn,{passive:false});window.addEventListener('touchend',upFn);
})();

/* === Market Status === */
(function(){
  const el=document.getElementById('marketStatus');if(!el)return;
  function isWeekday(tz){const d=new Intl.DateTimeFormat('en-US',{weekday:'short',timeZone:tz}).format(new Date());return d!=='Sat'&&d!=='Sun';}
  function hm(tz){const p=new Intl.DateTimeFormat('en-GB',{hour:'2-digit',minute:'2-digit',hour12:false,timeZone:tz}).formatToParts(new Date());const h=parseInt(p.find(x=>x.type==='hour').value),m=parseInt(p.find(x=>x.type==='minute').value);return{t:h*60+m};}
  function tokyo(){if(!isWeekday('Asia/Tokyo'))return false;const{t}=hm('Asia/Tokyo');return t>=9*60&&t<15*60;}
  function london(){if(!isWeekday('Europe/London'))return false;const{t}=hm('Europe/London');return t>=8*60&&t<16*60;}
  function ny(){if(!isWeekday('America/New_York'))return false;const{t}=hm('America/New_York');return t>=(9*60+30)&&t<16*60;}
  function refresh(){el.innerHTML=`
    <span class="badge ${tokyo()?'':'closed'}">TOKYO ${tokyo()?'LIVE':'CLOSED'}</span>
    <span class="badge ${london()?'':'closed'}">LONDON ${london()?'LIVE':'CLOSED'}</span>
    <span class="badge ${ny()?'':'closed'}">NEW YORK ${ny()?'LIVE':'CLOSED'}</span>`;}
  refresh();setInterval(refresh,60000);
})();
</script>
