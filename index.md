---
layout: default
title: Home
permalink: /
nav_order: 1
full_bleed: true
---

<style>
  /* ===== Root vars (incl. adjustable spacing) ===== */
  :root{
    --hero-spacing: 60px; /* valeur par défaut, ajustable via la poignée */
    --clock-speed: 120s;
  }

  /* === Fade-in global === */
  @keyframes fadeInUp { from{opacity:0; transform:translateY(25px);} to{opacity:1; transform:translateY(0);} }

  /* === Hero titles fade-in === */
  .eyebrow.shifted{ margin-top:-25px; opacity:0; transform:translateY(10px); animation:fadeInUp 1.4s ease-out .3s forwards; }
  .hero-content h1{ opacity:0; transform:translateY(20px); animation:fadeInUp 1.4s ease-out .8s forwards; }
  .hero-content .subtitle{ opacity:0; transform:translateY(20px); animation:fadeInUp 1.4s ease-out 1.3s forwards; }

  /* === HERO LAYERS === */
  .hero-video{ position:relative; z-index:2; overflow:hidden; }
  .hero-overlay{ position:absolute; inset:0; z-index:1; }
  .hero-content{ position:relative; z-index:2; }
  .hero-bg{ position:absolute; inset:0; width:100%; height:100%; object-fit:cover; }

  /* === LOGO IMAGE + halo pulsé === */
  .hero-logo-img{
    position:absolute; right:-4.0vw; top:20%; transform:translateY(-34%); z-index:3;
    width:min(13vw,40vh); height:auto; opacity:0;
    animation: fadeInLogo 1.2s ease-out 1.0s forwards, logoPulse 4s ease-in-out infinite;
    pointer-events:none; user-select:none; filter: drop-shadow(0 0 6px rgba(44,140,255,.6));
  }
  @keyframes fadeInLogo{ from{opacity:0; transform: translateY(-34%) translateX(40px);} to{opacity:1; transform: translateY(-34%) translateX(0);} }
  @keyframes logoPulse{ 0%,100%{filter: drop-shadow(0 0 6px rgba(44,140,255,.6));} 50%{filter: drop-shadow(0 0 14px rgba(44,140,255,.95));} }
  @media (max-width:880px){ .hero-logo-img{ right:-1.2vw; top:42%; transform:translateY(-42%); width:min(22vw,34vh); } }

  /* === SECONDARY VIDEO === */
  .promo-video{ position:relative; z-index:0; width:100%; margin:-1250px 0 0; }
  @media (max-width:1400px){ .promo-video{ margin:-1450px 0 0; } }
  @media (max-width:1200px){ .promo-video{ margin:-1350px 0 0; } }
  @media (max-width:1024px){ .promo-video{ margin:-1250px 0 0; } }
  @media (max-width:768px){ .promo-video{ margin:-1150px 0 0; } }
  @media (max-width:560px){ .promo-video{ margin:-1050px 0 0; } }
  .promo-video-frame{ position:relative; width:100%; aspect-ratio:16/9; overflow:hidden; background:#000; border-top:1px solid #222; border-bottom:1px solid #222; }
  @supports not (aspect-ratio:16/9){ .promo-video-frame{ padding-top:56.25%; } .promo-video-el{ position:absolute; left:0; top:0; width:100%; height:100%; } }
  .promo-video-el{ position:absolute; inset:0; width:100%; height:100%; object-fit:cover; filter:brightness(.8) contrast(1.05) saturate(1.05); }
  .promo-scrim{ position:absolute; inset:0; background:linear-gradient(180deg, rgba(0,0,0,.25) 0%, rgba(0,0,0,.45) 55%, rgba(0,0,0,.7) 90%); pointer-events:none; }

  /* === SPACING HANDLE (draggable) === */
  .clock-resizer{
    width:100%; height:16px;
    display:grid; place-items:center;
    cursor:row-resize; user-select:none;
    position:relative; z-index:11;
  }
  .clock-resizer::before{
    content:""; width:86px; height:6px; border-radius:6px;
    border:1px dashed rgba(158,200,255,.35); background:rgba(15,18,34,.6);
    box-shadow:0 4px 18px rgba(0,0,0,.35), inset 0 0 0 1px rgba(255,255,255,.04);
  }
  .clock-resizer.is-dragging::before{ border-color:#4da0ff; background:rgba(20,24,40,.8); }

  /* === WORLD CLOCK BAR === */
  .world-clock-bar{
    position:relative; overflow:hidden; background:#000;
    border-top:1px solid #333; border-bottom:1px solid #333;
    padding:12px 0; margin-top:var(--hero-spacing); opacity:1; z-index:10; isolation:isolate;
    -webkit-user-select:none; user-select:none; touch-action:pan-x;
  }
  .world-clock-bar *{ background:none !important; opacity:1 !important; mix-blend-mode:normal !important; filter:none !important; }
  .ticker-wrapper{ position:relative; z-index:1; display:flex; width:max-content; white-space:nowrap; animation:tickerMove var(--clock-speed) linear infinite; will-change:transform; }
  @keyframes tickerMove{ 0%{transform:translateX(0);} 100%{transform:translateX(-50%);} }
  .ticker-wrapper.reverse{ animation-name:tickerMoveReverse; }
  @keyframes tickerMoveReverse{ 0%{transform:translateX(-50%);} 100%{transform:translateX(0);} }
  .ticker-wrapper.dragging{ animation-play-state:paused; cursor:grabbing; }
  .clock{ display:flex; flex-direction:column; align-items:center; justify-content:center; min-width:150px; margin:0 35px; text-align:center; }
  .clock .city{ font-weight:900; color:#7fb3ff; text-transform:uppercase; font-size:.92rem; letter-spacing:.05em; text-shadow:0 0 6px rgba(0,0,0,.85); animation:clockPulseCity 3.6s ease-in-out infinite; animation-delay:.6s; }
  .clock .time{ font-weight:900; font-size:1.28rem; color:#fff; margin-top:2px; text-shadow:0 0 0 #000, 0 0 8px rgba(0,0,0,1), 0 0 1px #000; animation:clockPulse 1.8s ease-in-out infinite; will-change:transform, text-shadow, opacity; transform:translateZ(0); }
  @keyframes clockPulse{ 0%,100%{ transform:scale(1); text-shadow:0 0 0 #000, 0 0 8px rgba(0,0,0,1), 0 0 1px #000; } 50%{ transform:scale(1.03); text-shadow:0 0 10px rgba(44,140,255,.9), 0 0 22px rgba(44,140,255,.6), 0 0 2px #000; } }
  @keyframes clockPulseCity{ 0%,100%{ text-shadow:0 0 6px rgba(0,0,0,.8); } 50%{ text-shadow:0 0 10px rgba(44,140,255,.7), 0 0 18px rgba(44,140,255,.35); } }

  /* === MARKET STATUS === */
  .market-status{ background:#0a0a0a; border-top:1px solid #222; color:#2c8cff; text-align:center; font-weight:800; letter-spacing:.08em; padding:8px 12px; position:relative; z-index:50; }
  .market-status .badge{ display:inline-block; margin:0 .35rem; padding:.25rem .5rem; border-radius:.6rem; border:1px solid #1f3b66; background:#0c1220; color:#9ec8ff; font-weight:800; }
  .market-status .closed{ opacity:.7; color:#9aa3b2; border-color:#333; background:#0f0f0f; }
  .market-status a.badge{ text-decoration:none; cursor:pointer; pointer-events:auto; }
  .market-status a.badge:hover{ border-color:#2c8cff99; box-shadow:0 0 0 2px rgba(44,140,255,.12) inset; }

  /* ===== Bande "Latest Updates" ===== */
  .news-band{ background:#050505; border-top:1px solid #111; border-bottom:1px solid #111; padding:28px 20px; }
  .news-wrap{ max-width:1100px; margin:0 auto; display:grid; grid-template-columns: 1fr 1fr; gap:18px; }
  .update-card{
    position:relative; background:#0d0d0d; border:1px solid #222; border-radius:14px;
    padding:18px 18px 16px; box-shadow:0 10px 30px rgba(0,0,0,.25);
    transition:transform .18s ease, box-shadow .18s ease, border-color .18s ease;
  }
  .update-card::after{ content:""; position:absolute; inset:-1px; border-radius:14px; pointer-events:none; background:radial-gradient(600px 200px at 20% -20%, rgba(44,140,255,.15), transparent 70%); opacity:.7; }
  .update-card:hover{ transform:translateY(-2px); box-shadow:0 14px 36px rgba(0,0,0,.35); border-color:#2c8cff55; }
  .update-badge{ display:inline-block; font-size:.72rem; letter-spacing:.08em; color:#9ec8ff; background:#0c1220; border:1px solid #1f3b66; border-radius:999px; padding:4px 8px; margin-bottom:10px; font-weight:800; }
  .update-title{ margin:0 0 6px; font-size:clamp(1.05rem,2.2vw,1.2rem); font-weight:800; }
  .update-meta{ color:#9aa3b2; font-size:.9rem; margin:0 0 10px; }
  .update-desc{ color:#c9cbd1; margin:0 0 12px; line-height:1.55; }
  .update-link{ display:inline-flex; align-items:center; gap:8px; padding:8px 10px; border:1px solid rgba(255,255,255,.16); border-radius:10px; background:#0f0f0f; color:#fff; font-weight:700; text-decoration:none; }
  .update-link:hover{ border-color:#4da0ff; background:#141414; }
  @media (max-width:820px){ .news-wrap{ grid-template-columns: 1fr; } }

  /* === SECTION HUB === */
  .after-market{ position:relative; z-index:4; /* au-dessus du bandeau lectures */ background:#050505; color:#ccc; padding:60px 20px 120px; border-top:1px solid #111; }
  .hub-inner{ max-width:1100px; margin:0 auto; }
  .hub-eyebrow{ color:#9aa3b2; font-weight:800; letter-spacing:.08em; text-transform:uppercase; margin:0 0 10px; text-align:left; }
  .hub-title{ color:#fff; font-size:clamp(1.8rem,4vw,2.8rem); font-weight:900; line-height:1.1; margin:0 0 16px; text-align:left; text-shadow:0 0 10px rgba(0,0,0,.35); }

  .hub-tabs{ display:flex; gap:22px; flex-wrap:wrap; align-items:center; justify-content:flex-start; padding:8px 0 10px; border-bottom:1px solid #1a1a1a; margin-bottom:14px; }
  .hub-tab{ position:relative; display:inline-block; cursor:pointer; font-weight:800; letter-spacing:.02em; text-decoration:none; color:#cfd6e4; padding:4px 2px; }
  .hub-tab:hover{ color:#ffffff; }
  .hub-tab.is-active{ color:#ffffff; }
  .hub-tab.is-active::after{ content:""; position:absolute; left:0; right:0; bottom:-10px; height:3px; background:#2c8cff; border-radius:3px; box-shadow:0 0 12px rgba(44,140,255,.55); }

  .hub-selected-title{ margin:14px 0 6px; color:#fff; font-weight:900; letter-spacing:.06em; text-transform:uppercase; text-align:left; font-size:clamp(1.1rem,3vw,1.75rem); }
  .hub-panel{ margin-top:8px; color:#c9cbd1; line-height:1.65; text-align:justify; }

  /* === LAYOUT: split éducation / expériences === */
  .after-market .hub-inner{ max-width:none; width:100%; margin:0; padding:0 24px; }
  .hub-split{
    display:grid;
    grid-template-columns: minmax(320px, 42%) 1fr;
    gap:28px; align-items:start; margin-top:12px;
  }
  .hub-split.no-media{ grid-template-columns:1fr; }
  @media (max-width:1100px){ .hub-split{ grid-template-columns:1fr; } }

  /* ===== Stack gauche (Education + Certifications) ===== */
  .left-stack{ display:flex; flex-direction:column; gap:16px; }

  /* ===== CARTE GÉNÉRIQUE (verre + halo) ===== */
  .card-glass{
    position:relative; border-radius:18px; padding:16px 16px 18px;
    background: linear-gradient(180deg, rgba(14,18,34,.85), rgba(8,10,20,.9));
    border:1px solid rgba(76,139,255,.28);
    box-shadow: 0 10px 28px rgba(0,0,0,.35), inset 0 0 0 1px rgba(255,255,255,.04);
    overflow:hidden;
  }
  .card-glass::after{
    content:""; position:absolute; inset:-25% -25% -25% -25%;
    background: radial-gradient(50% 40% at 20% 0%, rgba(44,140,255,.18), transparent 60%),
                radial-gradient(60% 50% at 80% 100%, rgba(159,122,255,.12), transparent 65%);
    filter: blur(18px); opacity:.6; pointer-events:none;
  }
  .card-title{ margin:0 0 8px; font-size:1.05rem; font-weight:900; color:#e7efff; letter-spacing:.04em; text-transform:uppercase; position:relative; z-index:1; }
  .card-sub{ margin:.15rem 0 0; color:#9ec8ff; font-weight:700; font-size:.9rem; position:relative; z-index:1; }

  /* ===== EDUCATION ===== */
  .edu-header{ display:flex; align-items:center; gap:14px; position:relative; z-index:1; }
  .edu-body{ position:relative; z-index:1; margin-top:10px; color:#cfe3ff; line-height:1.6; font-size:.98rem; }

  /* BADGE CY Tech (rond + flip + halo) */
  .hub-gallery{ perspective:1200px; }
  .cy-holo.figure-tilt{
    --size: 90px; width:var(--size); height:var(--size); min-width:var(--size);
    border-radius:50%; position:relative; transform-style:preserve-3d;
    transition: transform .25s ease; cursor:pointer; flex:0 0 auto;
  }
  .cy-holo::before{
    content:""; position:absolute; inset:-5px; border-radius:50%;
    background: conic-gradient(from var(--a,0deg), #2c8cff, #7ad2ff, #9f7aff, #2c8cff);
    filter: blur(5px); opacity:.7; animation:ringSpin 8s linear infinite;
  }
  @keyframes ringSpin{ to{ --a:360deg; } }
  .cy-holo::after{
    content:""; position:absolute; inset:-14px; border-radius:50%;
    background: radial-gradient(60% 60% at 30% 10%, rgba(44,140,255,.22), transparent 55%),
                radial-gradient(80% 80% at 70% 90%, rgba(159,122,255,.14), transparent 60%);
    filter: blur(10px); opacity:.55; pointer-events:none;
  }
  .cy-holo .flip-inner{
    position:absolute; inset:0; border-radius:50%; overflow:hidden;
    transform-style:preserve-3d; transition: transform .7s cubic-bezier(.2,.65,.2,1);
    background: radial-gradient(120% 120% at 50% 10%, rgba(255,255,255,.08), rgba(13,16,30,.9));
    box-shadow: inset 0 0 0 2px rgba(76,139,255,.35), 0 6px 18px rgba(0,0,0,.35);
    backdrop-filter: blur(2px);
  }
  .cy-holo.is-flipped .flip-inner{ transform: rotateY(180deg); }
  .cy-holo .flip-face{ position:absolute; inset:0; backface-visibility:hidden; border-radius:50%; overflow:hidden; }
  .cy-holo .flip-front{ display:grid; place-items:center; }
  .cy-holo .flip-front .logo{
    width:100%; height:100%; border-radius:50%; overflow:hidden; display:flex; align-items:center; justify-content:center; background:transparent;
    box-shadow:0 0 0 1px rgba(255,255,255,.08) inset;
  }
  .cy-holo .flip-front .logo img{
    width:120%; height:120%; object-fit:cover; object-position:43% 35%;
    border-radius:50%; clip-path:circle(50% at 50% 50%);
    -webkit-mask-image: radial-gradient(closest-side, #000 99%, transparent 100%);
    mask-image: radial-gradient(closest-side, #000 99%, transparent 100%);
    filter:contrast(1.05) saturate(1.05) brightness(1.02); transform:scale(1.1);
  }
  .cy-holo .gloss{ position:absolute; inset:0; background: radial-gradient(60% 35% at 30% 10%, rgba(255,255,255,.18), transparent 60%), linear-gradient(180deg, rgba(255,255,255,.06), transparent 35%), radial-gradient(50% 60% at 70% 85%, rgba(44,140,255,.12), transparent 60%); mix-blend-mode:screen; pointer-events:none; }
  .cy-holo .flip-back{ transform: rotateY(180deg); display:flex; align-items:center; justify-content:center; padding:12px; background:#0b0f1a; color:#cfe3ff; text-align:center; }
  .cy-holo .flip-back .edu-text{ font-size:.78rem; line-height:1.25; }

  /* ===== EXPERIENCES ===== */
  .xp-section{ margin-top: 8px; }
  .xp-list{ display:flex; flex-direction:column; gap:12px; position:relative; z-index:1; }
  .xp-item{
    display:grid; grid-template-columns:52px 1fr auto; gap:14px; align-items:center;
    padding:12px 14px; border:1px solid #1f2333; border-radius:14px; background:#0b0f1a;
    transition:border-color .2s ease, box-shadow .2s ease, transform .2s ease;
  }
  .xp-item:hover{ border-color:#2c8cff55; box-shadow:0 10px 30px rgba(0,0,0,.35); transform: translateY(-1px); }
  .xp-logo{ width:52px; height:52px; border-radius:50%; overflow:hidden; position:relative; box-shadow: 0 0 0 1px rgba(76,139,255,.35) inset, 0 6px 18px rgba(0,0,0,.35); }
  .xp-logo img{ width:100%; height:100%; object-fit:cover; display:block; }
  .xp-logo::after{ content:""; position:absolute; inset:-8%; border-radius:50%; background: radial-gradient(120px 80px at 25% -10%, rgba(44,140,255,.22), transparent 60%); opacity:0; transition:opacity .25s ease; pointer-events:none; }
  .xp-item:hover .xp-logo::after{ opacity:.9; }
  .xp-role{ font-weight:800; color:#ffffff; line-height:1.25; }
  .xp-company{ color:#9ec8ff; font-weight:800; }
  .xp-desc{ color:#c9cbd1; margin-top:4px; }
  .xp-meta{ margin-left:auto; color:#9aa3b2; text-align:right; white-space:nowrap; }

  /* ===== CERTIFICATIONS ===== */
  .cert-list{ display:flex; flex-direction:column; gap:12px; margin-top:8px; }
  .cert-item{
    display:grid; grid-template-columns:52px 1fr; gap:14px; align-items:center;
    padding:12px 14px; border:1px solid #1f2333; border-radius:14px; background:#0b0f1a;
    transition:border-color .2s ease, box-shadow .2s ease, transform .2s ease;
  }
  .cert-item:hover{ border-color:#2c8cff55; box-shadow:0 10px 30px rgba(0,0,0,.35); transform: translateY(-1px); }
  .cert-logo{ width:52px; height:52px; border-radius:50%; overflow:hidden; position:relative; box-shadow: 0 0 0 1px rgba(76,139,255,.35) inset, 0 6px 18px rgba(0,0,0,.35); }
  .cert-logo img{ width:100%; height:100%; object-fit:cover; display:block; }
  .cert-title{ font-weight:800; color:#fff; line-height:1.25; }
  .cert-issuer{ color:#9ec8ff; font-weight:800; }
  .cert-desc{ color:#c9cbd1; margin-top:4px; font-size:.95rem; }

  /* === SHARED: Glass Board (Courses, Projects, Reading) === */
  .courses-panel, .projects-panel, .reading-panel{ display:none; }
  .courses-lede, .projects-lede, .reading-lede{ color:#cfe3ff; max-width:960px; line-height:1.65; margin:8px 0 16px; }
  .courses-stage, .projects-stage, .reading-stage{ perspective:1400px; margin-top:14px; display:grid; place-items:center; }
  .glass-board{
    position:relative; width:min(1100px, 96%); border-radius:22px;
    background: linear-gradient(180deg, rgba(13,16,30,.92), rgba(8,10,20,.96));
    border:1px solid rgba(76,139,255,.35);
    box-shadow: 0 18px 40px rgba(0,0,0,.45), inset 0 0 0 1px rgba(255,255,255,.04);
    transform-style:preserve-3d; transition: transform .18s ease, box-shadow .18s ease;
  }
  .glass-board:hover{ box-shadow: 0 20px 54px rgba(0,0,0,.55), inset 0 0 0 1px rgba(255,255,255,.04); }
  .board-halo{ content:""; position:absolute; inset:-20%; border-radius:26px; pointer-events:none;
    background:
      radial-gradient(60% 50% at 15% 0%, rgba(44,140,255,.18), transparent 60%),
      radial-gradient(70% 60% at 85% 100%, rgba(159,122,255,.12), transparent 65%);
    filter: blur(22px); opacity:.7; transform: translateZ(-40px);
  }
  .board-header{ display:flex; align-items:center; justify-content:space-between; gap:12px; padding:16px 18px; border-bottom:1px solid rgba(255,255,255,.06); }
  .board-title{ color:#e7efff; font-weight:900; letter-spacing:.06em; text-transform:uppercase; }
  .board-actions{ display:flex; gap:10px; }
  .btn-chip{ padding:8px 12px; border-radius:12px; border:1px solid rgba(255,255,255,.16); background:#0f1222; color:#cfe3ff; font-weight:800; text-decoration:none; }
  .btn-chip:hover{ border-color:#4da0ff; }

  .board-grid{ display:grid; grid-template-columns: 1.2fr 1.2fr 1.2fr; gap:12px; padding:14px; position:relative; }
  @media (max-width:980px){ .board-grid{ grid-template-columns:1fr; } }

  .board-col{ background:#0b0f1a; border:1px solid #1f2333; border-radius:16px; overflow:hidden; box-shadow: inset 0 0 0 1px rgba(255,255,255,.02); }
  .col-head{ display:flex; align-items:center; gap:10px; padding:12px 14px; border-bottom:1px solid #171a28; }
  .col-icon{ width:34px; height:34px; border-radius:50%; display:grid; place-items:center; background: radial-gradient(100% 100% at 30% 10%, rgba(44,140,255,.18), rgba(44,140,255,.05)); box-shadow: inset 0 0 0 1px rgba(76,139,255,.35); font-weight:900; color:#9ec8ff; }
  .col-title{ color:#ffffff; font-weight:900; letter-spacing:.02em; }
  .col-sub{ color:#9aa3b2; font-size:.92rem; }

  .row{ display:grid; grid-template-columns: 1fr auto; gap:10px; align-items:center; padding:12px 14px; border-top:1px solid #171a28; transition: background .18s ease, transform .18s ease, border-color .18s ease; }
  .row:first-child{ border-top:0; }
  .row:hover{ background:linear-gradient(180deg, rgba(32,42,72,.18), rgba(16,20,36,.18)); border-color:#2c8cff55; transform: translateY(-1px); }
  .row-title{ color:#e7efff; font-weight:800; }
  .row-desc{ color:#c9cbd1; font-size:.95rem; margin-top:2px; }
  .row-meta{ color:#9aa3b2; font-size:.9rem; margin-top:4px; }
  .row-cta{ color:#9ec8ff; font-weight:800; white-space:nowrap; }

  /* Désactivation des clics (pas de consultation / téléchargement) */
  .board-col .row{ cursor:default; }
  .board-col .row:hover{ transform:none; }

  /* Subtle floating particles inside the board */
  .particles{ position:absolute; inset:0; pointer-events:none; overflow:hidden; }
  .dot{ position:absolute; width:4px; height:4px; border-radius:50%; background: radial-gradient(circle, #9ec8ff 0%, rgba(158,200,255,.0) 70%); opacity:.45; animation: drift 12s linear infinite; }
  @keyframes drift{ 0%{ transform: translateY(0) translateX(0); opacity:.15;} 50%{ transform: translateY(-40px) translateX(20px); opacity:.5;} 100%{ transform: translateY(-80px) translateX(0); opacity:.15;} }

  /* ===== Bandeau Lectures ===== */
  .reading-band{
    position:relative;
    z-index:3; /* sous la section after-market */
    background:#050505;
    border-top:1px solid #111;
    border-bottom:1px solid #111;
    padding:18px 0 22px;
    overflow:hidden;
  }
  .reading-inner{ max-width:1100px; margin:0 auto; padding:0 24px; }
  .reading-eyebrow{ color:#9aa3b2; font-weight:800; letter-spacing:.08em; text-transform:uppercase; margin:0 0 10px; }
  .reading-track{
    display:flex; gap:16px; width:max-content; white-space:nowrap;
    animation: readingScroll 52s linear infinite;
  }
  @keyframes readingScroll{ 0%{ transform:translateX(0); } 100%{ transform:translateX(-50%); } }
  .reading-chip{
    display:flex; align-items:center; gap:10px;
    padding:10px 16px; border-radius:12px;
    background:#0b0f1a; border:1px solid #1f2333; color:#cfe3ff; font-weight:700;
    box-shadow:0 8px 18px rgba(0,0,0,.35);
  }
  .reading-badge{
    font-size:.75rem; background:#0c1220; border:1px solid #1f3b66;
    padding:4px 8px; border-radius:8px; color:#9ec8ff; font-weight:800;
  }

  /* au-dessus du footer */
  .news-band, .after-market{ position:relative; z-index:4; }
</style>

<section class="hero-video">
  <video class="hero-bg" autoplay muted loop playsinline preload="auto" poster="{{ '/assets/images/hero-poster.jpg' | relative_url }}">
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
    <video class="promo-video-el" autoplay muted loop playsinline preload="auto" poster="/assets/images/trading-broll-poster.jpg">
      <source src="/assets/videos/trading-broll.mp4" type="video/mp4">
    </video>
    <div class="promo-scrim"></div>
  </div>
</section>

<!-- ===== Spacing handle (drag to adjust, double-click to reset) ===== -->
<div class="clock-resizer" id="clockResizer" title="Drag to adjust spacing (double-click to reset)"></div>

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

    <h3 class="hub-selected-title" id="hubSelectedTitle">WHAT I DO</h3>

    <!-- ===== SPLIT (left = stack, right = experiences) ===== -->
    <div class="hub-split" id="hubSplit">
      <!-- LEFT STACK: Education + Certifications -->
      <div class="left-stack">
        <!-- Education card -->
        <div class="edu-card card-glass">
          <div class="edu-header">
            <figure class="cy-holo figure-tilt" id="eduBadge" role="button" aria-pressed="false" tabindex="0" title="Click to flip">
              <div class="flip-inner">
                <div class="flip-face flip-front" aria-hidden="false">
                  <div class="logo">
                    <img src="/assets/images/image13.png" alt="CY Tech logo">
                    <span class="gloss"></span>
                  </div>
                </div>
                <div class="flip-face flip-back" aria-hidden="true">
                  <div class="edu-text">
                    <strong>Education</strong>
                    Integrated preparatory program (Math/Physics/CS) → Engineering in Applied Mathematics for Finance + dual Master’s in Mathematics at CY Tech.
                  </div>
                </div>
              </div>
            </figure>

            <div class="edu-title-wrap">
              <h4 class="card-title">Education</h4>
              <p class="card-sub">CY Tech — Applied Mathematics for Finance</p>
            </div>
          </div>

          <div class="edu-body">
            I completed an integrated preparatory program specialized in mathematics, physics, and computer science, followed by an engineering degree in applied mathematics for finance and a dual master’s degree in mathematics at CY Tech.
          </div>
        </div>

        <!-- Certifications card -->
        <div class="cert-card card-glass">
          <h4 class="card-title">Certifications</h4>
          <p class="card-sub">Selected credentials</p>

          <div class="cert-list">
            <!-- Bloomberg -->
            <div class="cert-item">
              <div class="cert-logo"><img src="/assets/images/image20.png" alt="Bloomberg logo"></div>
              <div>
                <div class="cert-title">Bloomberg Market Concepts (BMC)</div>
                <div class="cert-issuer">Bloomberg</div>
                <div class="cert-desc">
                  Core modules across Economics, Equities, Fixed Income and FX with hands-on Terminal functions and market data navigation.
                </div>
              </div>
            </div>

            <!-- AMF -->
            <div class="cert-item">
              <div class="cert-logo"><img src="/assets/images/image21.png" alt="AMF logo"></div>
              <div>
                <div class="cert-title">AMF General Regulation Exam</div>
                <div class="cert-issuer">Autorité des Marchés Financiers (France)</div>
                <div class="cert-desc">
                  Knowledge requirements for French markets: financial instruments, conduct of business, client protection, market abuse and compliance.
                </div>
              </div>
            </div>

            <!-- CFA -->
            <div class="cert-item">
              <div class="cert-logo"><img src="/assets/images/image22.png" alt="CFA logo"></div>
              <div>
                <div class="cert-title">CFA® Program — Level I</div>
                <div class="cert-issuer">CFA Institute</div>
                <div class="cert-desc">
                  Ethics and professional standards, quantitative methods, economics, financial reporting & analysis, corporate finance, equity, fixed income and derivatives.
                </div>
              </div>
            </div>
          </div>
        </div>
      </div><!-- /left-stack -->

      <!-- RIGHT: Professional experiences -->
      <div class="xp-card card-glass">
        <h4 class="card-title">Professional Experiences</h4>
        <p class="card-sub">Recent roles & internships</p>

        <div class="xp-section">
          <div class="xp-list">
            <!-- Natixis -->
            <div class="xp-item">
              <div class="xp-logo"><img src="/assets/images/image10.png" alt="Natixis CIB logo"></div>
              <div>
                <div class="xp-role">Quantitative Trading Analyst</div>
                <div class="xp-company">Natixis Corporate &amp; Investment Banking</div>
                <div class="xp-desc">CVA/XVA development under LGM-1F, exposure simulation, sensitivities (Delta, Gamma, Vega, Theta, Cega) with GPR/BQ, multi-currency frameworks and analytics dashboards.</div>
              </div>
              <div class="xp-meta">Paris · 2025</div>
            </div>

            <!-- Spread Research -->
            <div class="xp-item">
              <div class="xp-logo"><img src="/assets/images/image12.png" alt="Spread Research logo"></div>
              <div>
                <div class="xp-role">Quantitative Analyst Intern (Equity Derivatives)</div>
                <div class="xp-company">Spread Research</div>
                <div class="xp-desc">Volatility surface calibration, Monte Carlo &amp; finite-difference pricing, hedging strategies (gamma scalping, delta-neutral), smile/skew dynamics.</div>
              </div>
              <div class="xp-meta">Paris · 2024</div>
            </div>

            <!-- Société Générale -->
            <div class="xp-item">
              <div class="xp-logo"><img src="/assets/images/image11.png" alt="Société Générale CIB logo"></div>
              <div>
                <div class="xp-role">Portfolio Valuation / Quant Intern</div>
                <div class="xp-company">Société Générale CIB</div>
                <div class="xp-desc">Automation of fund &amp; derivative pricing, Monte Carlo tools, daily PnL explainability, systematic stress testing, model reliability and auditability.</div>
              </div>
              <div class="xp-meta">La Défense · 2023</div>
            </div>
          </div>
        </div>
      </div>
    </div><!-- /hub-split -->

    <!-- ===== COURSES PANEL ===== -->
    <div class="courses-panel" id="coursesPanel" role="region" aria-live="polite">
      <p class="courses-lede">
        A collection of focused, practitioner-grade courses in Quantitative Finance, Machine Learning and Trading.
        Each course will come with concise notes, code notebooks, and applied exercises.
      </p>

      <div class="courses-stage">
        <div class="glass-board" id="glassBoard" aria-label="Courses board" tabindex="0">
          <div class="board-halo"></div>

          <div class="board-header">
            <div class="board-title">Courses — Live & On-site / Online</div>
            <div class="board-actions">
              <span class="btn-chip" aria-disabled="true" title="Coming soon">All courses</span>
            </div>
          </div>

          <div class="board-grid">
            <!-- Column 1: Quantitative Finance -->
            <div class="board-col">
              <div class="col-head">
                <div class="col-icon">𝛴</div>
                <div>
                  <div class="col-title">Quantitative Finance</div>
                  <div class="col-sub">Risk, rates, derivatives</div>
                </div>
              </div>

              <div class="row">
                <div>
                  <div class="row-title">Portfolio Theory & Risk Metrics</div>
                  <div class="row-desc">Mean–Variance, VaR/ES (MC), Cornish–Fisher, drawdowns, factor models.</div>
                </div>
              </div>

              <div class="row">
                <div>
                  <div class="row-title">Interest Rate Modelling (LGM-1F)</div>
                  <div class="row-desc">ZC bootstrapping, DF/forwards, swap pricing, exposures, sensitivities.</div>
                </div>
              </div>

              <div class="row">
                <div>
                  <div class="row-title">CVA & XVA Modelling</div>
                  <div class="row-desc">EE/EPE, default modeling, CSA, wrong-way risk, fast Greeks (GPR/BQ).</div>
                </div>
              </div>
            </div>

            <!-- Column 2: Machine Learning -->
            <div class="board-col">
              <div class="col-head">
                <div class="col-icon">ML</div>
                <div>
                  <div class="col-title">Machine Learning</div>
                  <div class="col-sub">For pricing & risk</div>
                </div>
              </div>

              <div class="row">
                <div>
                  <div class="row-title">Gaussian Process Regression</div>
                  <div class="row-desc">Kernels, training, uncertainty, surrogates for pricing, Greeks smoothing.</div>
                </div>
              </div>

              <div class="row">
                <div>
                  <div class="row-title">Bayesian Quadrature</div>
                  <div class="row-desc">Probabilistic integration for exposure & Greeks estimation, variance control.</div>
                </div>
              </div>

              <div class="row">
                <div>
                  <div class="row-title">Neural Nets for Derivatives</div>
                  <div class="row-desc">Calibration surrogates, PDE-to-NN, stability & monotonicity constraints.</div>
                </div>
              </div>
            </div>

            <!-- Column 3: Trading Strategies -->
            <div class="board-col">
              <div class="col-head">
                <div class="col-icon">α</div>
                <div>
                  <div class="col-title">Trading Strategies</div>
                  <div class="col-sub">Backtesting & microstructure</div>
                </div>
              </div>

              <div class="row">
                <div>
                  <div class="row-title">Options Hedging Simulation</div>
                  <div class="row-desc">Delta/Gamma/Theta management, transaction costs, P&L explainability.</div>
                </div>
              </div>

              <div class="row">
                <div>
                  <div class="row-title">Quant Backtesting with Python</div>
                  <div class="row-desc">Event-driven engine, slippage/latency models, robust metrics & pitfalls.</div>
                </div>
              </div>

              <div class="row">
                <div>
                  <div class="row-title">Volatility Surface Analysis</div>
                  <div class="row-desc">Smile/skew dynamics, arbitrage checks, interpolation & extrapolation.</div>
                </div>
              </div>
            </div>
          </div>

          <!-- floating particles -->
          <div class="particles" aria-hidden="true"></div>
        </div>
      </div>
    </div>

    <!-- ===== PROJECTS PANEL ===== -->
    <div class="projects-panel" id="projectsPanel" role="region" aria-live="polite">
      <p class="projects-lede">
        Selection of academic and applied research on credit risk, derivatives, extremes and market microstructure.
        Most projects include a write-up and reproducible code notebooks.
      </p>

      <div class="projects-stage">
        <div class="glass-board" id="projectsBoard" aria-label="Projects board" tabindex="0">
          <div class="board-halo"></div>

          <div class="board-header">
            <div class="board-title">Projects — Academic & Research</div>
            <div class="board-actions">
              <span class="btn-chip" aria-disabled="true" title="Coming soon">All projects</span>
            </div>
          </div>

          <div class="board-grid">
            <!-- Column 1: Credit Risk & XVA -->
            <div class="board-col">
              <div class="col-head">
                <div class="col-icon">X</div>
                <div>
                  <div class="col-title">Credit Risk & XVA</div>
                  <div class="col-sub">CVA · BQ · LGM-1F</div>
                </div>
              </div>

              <div class="row">
                <div>
                  <div class="row-title">Bayesian Quadrature for Efficient CVA Computation</div>
                  <div class="row-meta">May 2025</div>
                  <div class="row-desc">GPR surrogates + Bayesian Quadrature to accelerate CVA under LGM-1F; Monte Carlo + analytical hybrids; Basel/FRTB compliant.</div>
                </div>
              </div>

              <div class="row">
                <div>
                  <div class="row-title">Advanced Statistical & ML Techniques for Pricing & Risk</div>
                  <div class="row-meta">Mar–May 2025</div>
                  <div class="row-desc">GPR-accelerated VaR/ES with Monte Carlo; portfolio risk pipelines aligned with FRTB/Basel IV.</div>
                </div>
              </div>

              <div class="row">
                <div>
                  <div class="row-title">Calibration of the Heston Model</div>
                  <div class="row-meta">In progress</div>
                  <div class="row-desc">Levenberg–Marquardt calibration; fit implied vol surfaces; fast convergence on real market data.</div>
                </div>
              </div>
            </div>

            <!-- Column 2: Risk & Dependence -->
            <div class="board-col">
              <div class="col-head">
                <div class="col-icon">Σ</div>
                <div>
                  <div class="col-title">Risk & Dependence</div>
                  <div class="col-sub">EVT · Copulas · Networks</div>
                </div>
              </div>

              <div class="row">
                <div>
                  <div class="row-title">Risk Management & Extreme Values</div>
                  <div class="row-meta">Oct–Dec 2024</div>
                  <div class="row-desc">GEV/GPD tail modeling, Gaussian/t/Gumbel copulas for dependence; joint Sims for 200-year losses & aggregate exposure.</div>
                </div>
              </div>

              <div class="row">
                <div>
                  <div class="row-title">Systemic Risks & Contagion in Financial Networks</div>
                  <div class="row-meta">Jan–Apr 2024</div>
                  <div class="row-desc">Interbank Monte Carlo stress, cascade thresholds, contagion chains and critical nodes.</div>
                </div>
              </div>

              <div class="row">
                <div>
                  <div class="row-title">Climate Risk and Institutional Investors</div>
                  <div class="row-meta">Feb 2024</div>
                  <div class="row-desc">Physical vs transition risks; ESG policy adaptation, risk disclosure and capital allocation.</div>
                </div>
              </div>
            </div>

            <!-- Column 3: Derivatives & Methods -->
            <div class="board-col">
              <div class="col-head">
                <div class="col-icon">∂</div>
                <div>
                  <div class="col-title">Derivatives & Methods</div>
                  <div class="col-sub">Structured · LSMC</div>
                </div>
              </div>

              <div class="row">
                <div>
                  <div class="row-title">Autocallable Options: Mechanisms & Applications</div>
                  <div class="row-meta">Jan–May 2023</div>
                  <div class="row-desc">Pricing of autocallable structures; post-2008 design patterns; activation & payoff path modeling.</div>
                </div>
              </div>

              <div class="row">
                <div>
                  <div class="row-title">Pricing American Options (Longstaff–Schwartz)</div>
                  <div class="row-meta">In progress</div>
                  <div class="row-desc">LSMC for early exercise; optimal stopping in high-dimensional settings; equity & exotic Americans.</div>
                </div>
              </div>
            </div>
          </div>

          <!-- floating particles -->
          <div class="particles" aria-hidden="true"></div>
        </div>
      </div>
    </div>

    <!-- ===== READING PANEL (nouveau) ===== -->
    <div class="reading-panel" id="readingPanel" role="region" aria-live="polite">
      <p class="reading-lede">
        Technical readings in quantitative finance. For each book, I prepare a structured, application-oriented summary (pricing, risk, financial engineering). No public downloads available at the moment.
      </p>

      <div class="reading-stage">
        <div class="glass-board" id="readingBoard" aria-label="Reading board" tabindex="0">
          <div class="board-halo"></div>

          <div class="board-header">
            <div class="board-title">Reading — Selection in progress</div>
            <div class="board-actions">
              <span class="btn-chip" aria-disabled="true" title="Bientôt">View all</span>
            </div>
          </div>

          <div class="board-grid">
            <div class="board-col">
              <div class="col-head">
                <div class="col-icon">📘</div>
                <div><div class="col-title">Derivatives</div><div class="col-sub">Hull · Fundamentals</div></div>
              </div>
              <div class="row">
                <div>
                  <div class="row-title">Options, Futures and Other Derivatives — John C. Hull</div>
                  <div class="row-meta">Summary in progress</div>
                  <div class="row-desc">
                    Futures & options markets, Black–Scholes–Merton framework, hedging strategies (Greeks), exotic & structured products, Value-at-Risk and credit risk.
                  </div>
                </div>
              </div>
            </div>

            <div class="board-col">
              <div class="col-head">
                <div class="col-icon">📗</div>
                <div><div class="col-title">Quantitative Finance</div><div class="col-sub">Wilmott · Models</div></div>
              </div>
              <div class="row">
                <div>
                  <div class="row-title">Paul Wilmott on Quantitative Finance</div>
                  <div class="row-meta">Currently reading</div>
                  <div class="row-desc">
                    Stochastic calculus, volatility dynamics, calibration, pricing & risk management, robust methodologies for derivative products.
                  </div>
                </div>
              </div>
            </div>

            <div class="board-col">
              <div class="col-head">
                <div class="col-icon">🅑</div>
                <div><div class="col-title">Market & Data</div><div class="col-sub">Bloomberg</div></div>
              </div>
              <div class="row">
                <div>
                  <div class="row-title">Bloomberg Ultimate Guide (Terminal)</div>
                  <div class="row-meta">Personal notes</div>
                  <div class="row-desc">
                    Terminal navigation, key functions (Equities, FI, FX), data extraction, Fixed Income analytics, pricing & risk workflows.
                  </div>
                </div>
              </div>
            </div>
          </div>

          <div class="particles" aria-hidden="true"></div>
        </div>
      </div>
    </div>

    <!-- ===== Panneau générique (fallback) ===== -->
    <div class="hub-panel" id="hubPanelGeneric" style="display:none;" role="region" aria-live="polite"></div>
  </div>
</section>

<!-- ===== BANDEAU LECTURES (FR) ===== -->
<section class="reading-band">
  <div class="reading-inner">
    <p class="reading-eyebrow">LECTURES — SUR MON BUREAU</p>
    <div class="reading-track" aria-label="Lectures en cours">
      <div class="reading-chip"><span class="reading-badge">LIVRE</span> Paul Wilmott on Quantitative Finance — Calcul stochastique, volatilité, pricing, risque</div>
      <div class="reading-chip"><span class="reading-badge">GUIDE</span> Guide Ultime Bloomberg — Navigation terminal, fonctions marchés, Fixed Income analytics</div>
      <div class="reading-chip"><span class="reading-badge">LIVRE</span> Options, Futures & Other Derivatives (Hull) — BSM, exotiques, VaR, risque de crédit</div>

      <!-- duplication pour boucle fluide -->
      <div class="reading-chip"><span class="reading-badge">LIVRE</span> Paul Wilmott on Quantitative Finance — Calcul stochastique, volatilité, pricing, risque</div>
      <div class="reading-chip"><span class="reading-badge">GUIDE</span> Guide Ultime Bloomberg — Navigation terminal, fonctions marchés, Fixed Income analytics</div>
      <div class="reading-chip"><span class="reading-badge">LIVRE</span> Options, Futures & Other Derivatives (Hull) — BSM, exotiques, VaR, risque de crédit</div>
    </div>
  </div>
</section>

<script>
/* === Horloges === */
function updateClocks(){
  document.querySelectorAll('.clock').forEach(el=>{
    const city = el.dataset.city;
    const tz = el.dataset.tz;
    const now = new Date().toLocaleTimeString('en-GB', { timeZone: tz, hour:'2-digit', minute:'2-digit', hour12:false });
    el.innerHTML = `<span class="city">${city}</span><span class="time">${now}</span>`;
  });
}
updateClocks(); setInterval(updateClocks, 1000);

/* === Drag ticker (défilement horizontal) === */
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

/* === Spacing Resizer (hero <-> clocks) === */
(function(){
  const ROOT = document.documentElement;
  const HANDLE = document.getElementById('clockResizer');
  if(!HANDLE) return;

  const KEY = 'heroSpacingPx';
  const DEFAULT = parseInt(getComputedStyle(ROOT).getPropertyValue('--hero-spacing')) || 60;
  const MIN = 0;
  const MAX = 240;

  const saved = parseInt(localStorage.getItem(KEY));
  if(!Number.isNaN(saved)) ROOT.style.setProperty('--hero-spacing', saved + 'px');

  let startY = 0, startSpacing = 0, dragging = false;

  const getSpacing = () => {
    const v = getComputedStyle(ROOT).getPropertyValue('--hero-spacing').trim();
    return parseInt(v, 10) || 0;
  };

  function onDown(e){
    dragging = true;
    HANDLE.classList.add('is-dragging');
    startY = (e.touches ? e.touches[0].clientY : e.clientY);
    startSpacing = getSpacing();
    e.preventDefault();
  }

  function onMove(e){
    if(!dragging) return;
    const y = (e.touches ? e.touches[0].clientY : e.clientY);
    const dy = y - startY;
    const next = Math.min(MAX, Math.max(MIN, startSpacing + dy));
    ROOT.style.setProperty('--hero-spacing', next + 'px');
  }

  function onUp(){
    if(!dragging) return;
    dragging = false;
    HANDLE.classList.remove('is-dragging');
    const current = getSpacing();
    localStorage.setItem(KEY, String(current));
  }

  function onDblClick(){
    ROOT.style.setProperty('--hero-spacing', DEFAULT + 'px');
    localStorage.setItem(KEY, String(DEFAULT));
  }

  HANDLE.addEventListener('mousedown', onDown);
  window.addEventListener('mousemove', onMove, { passive:false });
  window.addEventListener('mouseup', onUp);

  HANDLE.addEventListener('touchstart', onDown, { passive:false });
  window.addEventListener('touchmove', onMove, { passive:false });
  window.addEventListener('touchend', onUp);

  HANDLE.addEventListener('dblclick', onDblClick);
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
  function isOpenTokyo(){ if(!isWeekday('Asia/Tokyo')) return false; const {t}=hmInTZ('Asia/Tokyo'); return t>=540 && t<900; }     // 09:00–15:00
  function isOpenLondon(){ if(!isWeekday('Europe/London')) return false; const {t}=hmInTZ('Europe/London'); return t>=480 && t<960; } // 08:00–16:00
  function isOpenParis(){ if(!isWeekday('Europe/Paris')) return false; const {t}=hmInTZ('Europe/Paris'); return t>=540 && t<1020; }   // 09:00–17:00
  function isOpenNewYork(){ if(!isWeekday('America/New_York')) return false; const {t}=hmInTZ('America/New_York'); return t>=(9*60+30) && t<960; } // 09:30–16:00

  function refresh(){
    const tokyo=isOpenTokyo(), london=isOpenLondon(), paris=isOpenParis(), ny=isOpenNewYork();
    const urls={ tokyo:"https://www.jpx.co.jp/english/markets/", london:"https://www.londonstockexchange.com/", paris:"https://live.euronext.com/en/markets/paris", ny:"https://www.nyse.com/" };
    const badge=(open,label,url)=> open
      ? `<a class="badge" href="${url}" target="_blank" rel="noopener noreferrer">${label} LIVE</a>`
      : `<span class="badge closed">${label} CLOSED</span>`;
    el.innerHTML = `${badge(tokyo,'TOKYO',urls.tokyo)} ${badge(london,'LONDON',urls.london)} ${badge(paris,'PARIS',urls.paris)} ${badge(ny,'NEW YORK',urls.ny)}`;
  }
  refresh(); setInterval(refresh, 60_000);
})();

/* === Tabs: WHAT / COURSES / PROJECTS / READING / others === */
(function(){
  const tabs = document.querySelectorAll('.hub-tab');
  const titleEl = document.getElementById('hubSelectedTitle');
  const split = document.getElementById('hubSplit');
  const panelGeneric = document.getElementById('hubPanelGeneric');
  const panelCourses = document.getElementById('coursesPanel');
  const panelProjects = document.getElementById('projectsPanel');
  const panelReading = document.getElementById('readingPanel');

  const copy = {
    reading:  `Curated reading lists and annotations across papers, textbooks and articles that influenced my thinking on modeling, risk, markets and systems design.`,
  };

  function showWhat(){
    split.style.display = '';
    panelGeneric.style.display = 'none';
    panelGeneric.innerHTML = '';
    panelCourses.style.display = 'none';
    panelProjects.style.display = 'none';
    panelReading.style.display = 'none';
  }
  function showCourses(){
    split.style.display = 'none';
    panelGeneric.style.display = 'none';
    panelProjects.style.display = 'none';
    panelReading.style.display = 'none';
    panelCourses.style.display = 'block';
  }
  function showProjects(){
    split.style.display = 'none';
    panelGeneric.style.display = 'none';
    panelCourses.style.display = 'none';
    panelReading.style.display = 'none';
    panelProjects.style.display = 'block';
  }
  function showReading(){
    split.style.display = 'none';
    panelGeneric.style.display = 'none';
    panelCourses.style.display = 'none';
    panelProjects.style.display = 'none';
    panelReading.style.display = 'block';
  }
  function showGeneric(key){
    split.style.display = 'none';
    panelCourses.style.display = 'none';
    panelProjects.style.display = 'none';
    panelReading.style.display = 'none';
    panelGeneric.style.display = '';
    panelGeneric.innerHTML = copy[key] || '';
  }

  function activate(key, labelUpper){
    tabs.forEach(t=>{
      const isActive = t.dataset.tab === key;
      t.classList.toggle('is-active', isActive);
      t.setAttribute('aria-selected', isActive ? 'true' : 'false');
    });
    titleEl.textContent = labelUpper;

    if (key === 'what')         showWhat();
    else if (key === 'courses') showCourses();
    else if (key === 'projects')showProjects();
    else if (key === 'reading') showReading();
    else                        showGeneric(key);
  }

  activate('what', 'WHAT I DO');
  tabs.forEach(t => t.addEventListener('click', (e)=>{
    e.preventDefault();
    activate(t.dataset.tab, t.textContent.trim().toUpperCase());
  }));
})();

/* === Tilt 3D + Flip sur le badge Education === */
(function(){
  const card = document.getElementById('eduBadge');
  if (!card) return;
  const clamp = (v,min,max)=>Math.max(min,Math.min(max,v));
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
    rAF = requestAnimationFrame(()=>{ card.style.transform = `rotateX(${rx}deg) rotateY(${ry}deg)`; });
  }
  function reset(){ card.style.transform = 'rotateX(0deg) rotateY(0deg)'; }
  function toggleFlip(){
    const flipped = card.classList.toggle('is-flipped');
    card.setAttribute('aria-pressed', flipped ? 'true' : 'false');
  }

  card.addEventListener('mousemove', onMove, {passive:true});
  card.addEventListener('mouseleave', reset);
  card.addEventListener('touchmove', onMove, {passive:true});
  card.addEventListener('touchend', reset);
  card.addEventListener('click', toggleFlip);
  card.addEventListener('keydown', (e)=>{ if (e.key==='Enter' || e.key===' '){ e.preventDefault(); toggleFlip(); }});
})();

/* === Tilt 3D sur les Glass Boards + Particles spawn === */
(function(){
  function enhanceBoard(boardId){
    const board = document.getElementById(boardId);
    const particles = board?.querySelector('.particles');
    if (!board) return;

    // spawn dots (courses / projects / reading)
    const p = particles || (()=>{ const el=document.createElement('div'); el.className='particles'; board.appendChild(el); return el; })();
    const n = 26;
    for(let i=0;i<n;i++){
      const d=document.createElement('div'); d.className='dot';
      d.style.left = (Math.random()*100)+'%';
      d.style.top  = (Math.random()*100)+'%';
      d.style.animationDelay = (Math.random()*10).toFixed(2)+'s';
      d.style.opacity = (0.15+Math.random()*0.45).toFixed(2);
      p.appendChild(d);
    }

    const clamp = (v,min,max)=>Math.max(min,Math.min(max,v));
    let rAF;
    function onMove(e){
      const rect = board.getBoundingClientRect();
      const clientX = (e.clientX ?? (e.touches&&e.touches[0].clientX));
      const clientY = (e.clientY ?? (e.touches&&e.touches[0].clientY));
      if (clientX==null || clientY==null) return;
      const x = clientX - rect.left;
      const y = clientY - rect.top;
      const rx = clamp(((y/rect.height)-0.5)*6,-6,6);
      const ry = clamp(((x/rect.width)-0.5)*-8,-8,8);
      cancelAnimationFrame(rAF);
      rAF = requestAnimationFrame(()=>{ board.style.transform = `rotateX(${rx}deg) rotateY(${ry}deg)`; });
    }
    function reset(){ board.style.transform = 'rotateX(0deg) rotateY(0deg)'; }

    board.addEventListener('mousemove', onMove, {passive:true});
    board.addEventListener('mouseleave', reset);
    board.addEventListener('touchmove', onMove, {passive:true});
    board.addEventListener('touchend', reset);
  }

  enhanceBoard('glassBoard');     // Courses
  enhanceBoard('projectsBoard');  // Projects
  enhanceBoard('readingBoard');   // Reading
})();
</script>
