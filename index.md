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
    --promo-overlap: clamp(850px, 110vh, 1500px);
  }

  /* === Fade-in global === */
  @keyframes fadeInUp { from{opacity:0; transform:translateY(25px);} to{opacity:1; transform:translateY(0);} }

  /* === Hero titles fade-in === */
  .eyebrow.shifted{
    margin-top:-25px;
    opacity:0;
    transform:translateY(10px);
    animation:fadeInUp 1.4s ease-out .3s forwards;

    /* Style responsive propre */
    font-size:clamp(1.6rem, 3vw, 3rem);
    font-weight:300;                 /* lettres fines */
    letter-spacing:0.1em;
    text-transform:uppercase;
    color:#bcd9ff;
    text-shadow:0 0 6px rgba(44,140,255,.35);
    font-family:'Helvetica Neue','Segoe UI',Roboto,sans-serif;
  }
  
  .hero-content h1{ opacity:0; transform:translateY(20px); animation:fadeInUp 1.4s ease-out .8s forwards; }
  .hero-content .subtitle{ opacity:0; transform:translateY(20px); animation:fadeInUp 1.4s ease-out 1.3s forwards; }

  /* === HERO LAYERS === */
  .hero-video{
    position:relative;
    padding:var(--hero-spacing) 24px calc(var(--hero-spacing) * 1.2);
    display:flex;
    align-items:flex-start;
    justify-content:center;
    min-height:clamp(420px, 78vh, 720px);
    color:#fff;
    overflow:hidden;
    background:#050814;
  }
  .hero-video::after{
    content:"";
    position:absolute;
    left:0; right:0; bottom:-1px;
    height:100px;
    background:linear-gradient(to bottom,
      rgba(5,8,16,0) 0%,
      rgba(5,8,16,0.4) 60%,
      rgba(5,8,16,0.8) 100%);
    pointer-events:none;
  }
  .hero-content{
    position: relative;
    top: -80px;  
    margin-left: -400px;
    z-index: 2;
    max-width: 1100px;
    width: 100%;
    text-align: left;
  }
  .hero-video::before{
    content:"";
    position:absolute;
    inset:0;
    background: radial-gradient(60% 60% at 20% 10%, rgba(44,140,255,.15), transparent 70%),
                radial-gradient(80% 80% at 80% 90%, rgba(159,122,255,.12), transparent 65%);
    opacity:.35;
    pointer-events:none;
  }

  /* === LOGO IMAGE + halo pulsé === */
  .hero-logo-img{
    position:absolute;
    right:-50px;
    top:60px;
    transform:translateY(-34%);
    width:clamp(90px,14vw,220px);
    height:auto;
    z-index:3;
    opacity:0;
    animation: fadeInLogo 1s ease-out .5s forwards, logoPulse 4s ease-in-out infinite;
    pointer-events:none;
  }
  @keyframes fadeInLogo{ from{opacity:0; transform: translateY(-34%) translateX(40px);} to{opacity:1; transform: translateY(-34%) translateX(0);} }
  @keyframes logoPulse{ 0%,100%{filter: drop-shadow(0 0 6px rgba(44,140,255,.6));} 50%{filter: drop-shadow(0 0 14px rgba(44,140,255,.95));} }
  @media (max-width:880px){ .hero-logo-img{ right:-1.2vw; top:42%; transform:translateY(-42%); width:min(22vw,34vh); } }

  /* === SECONDARY VIDEO — FULL OVERLAY BEHIND HERO (FINAL ADJUSTMENTS) === */
  .promo-video{
    position: relative;
    z-index: 0;
    width: 100%;
    margin-top: calc(var(--promo-overlap) * -1);
  }

  @keyframes tipParticlesFadeOut{
  from{ opacity:1; }
  to{ opacity:0; }
  }
  
  .timeline-graph-wrapper.about-graph-visible .axis-tip-particles{
    animation: tipParticlesFadeOut .8s ease forwards;
    animation-delay: 2.6s; /* durée totale de drawAxisX */
  }
  
  .promo-video-frame{
    position: relative;
    width: 100%;
    aspect-ratio: 16/9;
    overflow: hidden;
    background: #000;
    border: 0;
  }
  
  @supports not (aspect-ratio:16/9){
    .promo-video-frame{ padding-top:56.25%; }
    .promo-video-el{ position:absolute; left:0; top:0; width:100%; height:100%; }
  }
  
  .promo-video-el{
    position: absolute;
    inset: 0;
    width: 100%;
    height: 100%;
    object-fit: cover;
    object-position: center 25%;
    filter: brightness(.82) contrast(1.05) saturate(1.05);
  }
  
  .promo-scrim{
    position: absolute;
    inset: 0;
    background: linear-gradient(
      180deg,
      rgba(0,0,0,.05) 0%,
      rgba(0,0,0,.2) 20%,
      rgba(0,0,0,.4) 50%,
      rgba(0,0,0,.7) 90%
    );
    pointer-events: none;
  }

  /* === Bouton play / pause pour la vidéo promo (dans la barre social-actions) === */
  .promo-video-toggle{
    margin-left:auto;
    width:46px;
    height:46px;
    border-radius:50%;
    border:1px solid rgba(255,255,255,.35);
    background: radial-gradient(120% 120% at 30% 10%, rgba(44,140,255,.35), rgba(5,8,16,.92));
    box-shadow:0 8px 20px rgba(0,0,0,.6), inset 0 0 0 1px rgba(0,0,0,.4);
    display:grid;
    place-items:center;
    cursor:pointer;
    color:#e7efff;
    font-size:1rem;
    font-weight:800;
    transition:transform .15s ease, box-shadow .2s ease, border-color .2s ease, background .2s ease;
  }
  .promo-video-toggle:hover{
    transform:translateY(-1px);
    border-color:#6bb0ff;
    box-shadow:0 12px 30px rgba(0,0,0,.7), 0 0 18px rgba(44,140,255,.35) inset;
    background: radial-gradient(120% 120% at 30% 10%, rgba(44,140,255,.5), rgba(8,12,24,.98));
  }
  .promo-video-toggle:focus-visible{
    outline:none;
    box-shadow:0 0 0 3px rgba(76,139,255,.7);
  }
  .promo-video-toggle-icon{
    line-height:1;
    transform:translateY(1px); /* pour centrer visuellement les icônes ❚❚ / ▶ */
  }

  @media (max-width:600px){
    .promo-video-toggle{
      width:40px;
      height:40px;
      font-size:.9rem;
    }
  }
  
  /* === Écrans à faible hauteur === */
  @media (max-height: 720px){
    :root{
      --promo-overlap: clamp(1200px, 130vh, 2200px);
    }
    .hero-video{
      min-height: clamp(320px, 54svh, 640px);
    }
  }
    
  /* === WORLD CLOCK BAR === */
  .world-clock-bar{
    position:relative;
    overflow:hidden;
    background:#000;
    border-top:1px solid #333;
    border-bottom:1px solid #333;
    padding:12px 0;
  
    /* on remonte la barre d’horloges sous la vidéo */
    margin-top: clamp(0px, 0vh, 0px);
  
    opacity:1;
    z-index:10;
    isolation:isolate;
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

  /* ====== UPDATES CAROUSEL (remplace l'ancien "news-band") ====== */
  .news-band{ background:#050505; border-top:1px solid #111; border-bottom:1px solid #111; padding:28px 0 40px; }
  .updates-wrap{ max-width:1100px; margin:0 auto; padding:0 20px; }
  .updates-head{
    display:flex;
    align-items:center;
    justify-content:space-between;
    gap:12px;
    margin-bottom:14px;
  }
  /* Conteneur du label + badge */
  .updates-label{
    position:relative;
    display:inline-block;
  }
  /* Texte "LATEST UPDATES" (tu peux adapter si tu veux plus gros) */
  .updates-title{
    color:#e7efff;
    font-weight:900;
    letter-spacing:.08em;
    text-transform:uppercase;
    font-size:.9rem;
  }
  /* Badge type notification iPhone */
  .updates-counter{
    position:absolute;
    top:-10px;
    right:-14px;
    min-width:22px;
    height:22px;
    padding:0 6px;
    border-radius:999px;
    background:#ff3b30; /* rouge notif */
    color:#fff;
    font-size:.75rem;
    font-weight:800;
    display:flex;
    align-items:center;
    justify-content:center;
    box-shadow:
      0 0 0 2px #050505,      /* anneau foncé autour */
      0 4px 10px rgba(0,0,0,.7);
  }
  .updates-ctrls{ display:flex; gap:8px; }
  .updates-btn{
    width:42px; height:42px; border-radius:50%; display:grid; place-items:center;
    border:1px solid rgba(255,255,255,.15); background:#0f0f0f; color:#cfe3ff; font-weight:900; cursor:pointer;
    box-shadow:0 8px 20px rgba(0,0,0,.35);
  }
  .updates-btn:hover{ border-color:#4da0ff; }
  .updates-stage{
    position:relative; overflow:visible;
  }
  
  .updates-fade{ display:none; }
  .updates-track{
    display:flex; gap:18px; align-items:stretch;
    will-change:transform; transform:translate3d(0,0,0);
    transition: transform .35s cubic-bezier(.2,.75,.2,1);
    padding:8px 0;
  }
  /* État par défaut (déjà présent, tu peux juste vérifier que tu as bien ça) */
  .update-card{
    position:relative;
    background:#0d0d0d;
    border:1px solid #222;
    border-radius:14px;
    padding:18px 18px 16px;
    box-shadow:0 10px 30px rgba(0,0,0,.25);
    width:min(540px, 86vw);
    flex:0 0 auto;
    transition:
      transform .25s ease,
      box-shadow .25s ease,
      border-color .25s ease,
      filter .25s ease,
      opacity .25s ease;
    transform-origin:center center;
    opacity:.78;
    filter:saturate(.95) brightness(.95);
    transform:scale(.985);
  }
  
  /* Carte au centre (déjà présent, on garde) */
  .update-card.is-center{
    transform:scale(1.02);
    border-color:#2c8cff55;
    box-shadow:0 18px 46px rgba(0,0,0,.45);
    opacity:1;
    filter:none;
  }

  /* Toutes les cartes NON sélectionnées (gauche, droite, hors écran) */
  .update-card:not(.is-center){
    opacity:0.38;
    filter:blur(2.5px) saturate(.85) brightness(.72);
    box-shadow:0 12px 50px rgba(0,0,0,.6);
  }
  
  /* Dégradé sur les bords pour toutes les cartes floutées */
  .update-card:not(.is-center)::before{
    content:"";
    position:absolute;
    inset:0;
    border-radius:inherit;
    pointer-events:none;
    background:linear-gradient(
      to right,
      rgba(0,0,0,.65),
      transparent 40%,
      transparent 60%,
      rgba(0,0,0,.45)
    );
    opacity:.9;
  }
  /* On garde la carte centrale parfaitement nette et “au-dessus” visuellement */
  .update-card.is-center::before{
    content:"";
    position:absolute;
    inset:-1px;
    border-radius:inherit;
    pointer-events:none;
    background:radial-gradient(80% 120% at 50% -10%, rgba(44,140,255,.16), transparent 70%);
    opacity:.9;
  }
 
  /* Halo global déjà présent, on laisse tel quel */
  .update-card::after{
    content:"";
    position:absolute;
    inset:-1px;
    border-radius:14px;
    pointer-events:none;
    background:radial-gradient(600px 200px at 20% -20%, rgba(44,140,255,.15), transparent 70%);
    opacity:.7;
  }

  /* === Teaser vidéo dans la carte "My first book" === */
  .update-teaser-wrapper{
    position:relative;
    width:100%;
    border-radius:14px;
    overflow:hidden;
    background:#000;
    margin:0;
    max-height:0;
    opacity:0;
    transform:translateY(8px);
    transition:
      max-height .6s ease,
      opacity .6s ease,
      transform .6s ease;
  }

  .update-teaser-video{
    display:block;
    width:100%;
    height:100%;
    object-fit:cover;
  }

  /* Transitions texte & lien */
  .update-card .update-badge,
  .update-card .update-title,
  .update-card .update-meta,
  .update-card .update-desc,
  .update-card .update-link{
    transition:opacity .45s ease, transform .45s ease;
  }

  /* Avant la vidéo : on cache juste le texte long + lien (pour le reveal final) */
  .update-card.teaser-armed .update-desc,
  .update-card.teaser-armed .update-link{
    opacity:0;
    transform:translateY(6px);
  }

  /* Pendant la lecture :
     - on garde le même padding pour que la hauteur de la carte
       reste EXACTEMENT la même
     - on colle la vidéo en absolu sur les bords de la carte
  */
  .update-card.teaser-playing{
    padding:18px 18px 16px; /* même padding que l'état normal */
  }
  
  .update-card.teaser-playing .update-teaser-wrapper{
    position:absolute;
    inset:0;                /* colle le wrapper aux bords de la carte */
    max-height:none;
    height:100%;
    opacity:1;
    transform:none;
    border-radius:inherit;  /* même arrondi que la carte */
  }

  .update-card.teaser-playing .update-badge,
  .update-card.teaser-playing .update-title,
  .update-card.teaser-playing .update-meta,
  .update-card.teaser-playing .update-desc,
  .update-card.teaser-playing .update-link{
    opacity:0;
    transform:translateY(6px);
    pointer-events:none;
  }

  /* Après la vidéo :
     - on remet la padding par défaut
     - on cache la vidéo
     - on affiche TOUT le texte (badge + titre + meta + desc + lien)
  */
  .update-card.teaser-done{
    padding:18px 18px 16px;
  }

  .update-card.teaser-done .update-teaser-wrapper{
    max-height:0;
    opacity:0;
    pointer-events:none;
  }

  .update-card.teaser-done .update-badge,
  .update-card.teaser-done .update-title,
  .update-card.teaser-done .update-meta,
  .update-card.teaser-done .update-desc,
  .update-card.teaser-done .update-link{
    opacity:1;
    transform:translateY(0);
    pointer-events:auto;
  }

  /* === OUTRO après la fin de la vidéo (0.7s) === */
  .update-card.teaser-outro .update-teaser-wrapper{
    animation: teaserCurtain 0.7s ease forwards;
  }

  /* Pendant l’outro, on garde le texte caché */
  .update-card.teaser-outro .update-badge,
  .update-card.teaser-outro .update-title,
  .update-card.teaser-outro .update-meta,
  .update-card.teaser-outro .update-desc,
  .update-card.teaser-outro .update-link{
    opacity:0;
    transform:translateY(8px);
  }

  /* Animation de sortie de la vidéo : léger zoom + montée + blur */
  @keyframes teaserCurtain{
    0%{
      opacity:1;
      transform:scale(1) translateY(0);
      filter:blur(0);
    }
    40%{
      opacity:1;
      transform:scale(1.02) translateY(-4px);
      filter:blur(1px);
    }
    100%{
      opacity:0;
      transform:scale(1.06) translateY(-28px);
      filter:blur(4px);
    }
  }

  /* Cascade de retour du texte quand on passe en .teaser-done */
  .update-card.teaser-done .update-badge{ transition-delay:0.05s; }
  .update-card.teaser-done .update-title{ transition-delay:0.12s; }
  .update-card.teaser-done .update-meta{  transition-delay:0.18s; }
  .update-card.teaser-done .update-desc{  transition-delay:0.26s; }
  .update-card.teaser-done .update-link{  transition-delay:0.34s; }

  .update-badge{ display:inline-block; font-size:.72rem; letter-spacing:.08em; color:#9ec8ff; background:#0c1220; border:1px solid #1f3b66; border-radius:999px; padding:4px 8px; margin-bottom:10px; font-weight:800; }
  .update-title{ margin:0 0 6px; font-size:clamp(1.05rem,2.2vw,1.2rem); font-weight:800; }
  .update-meta{ color:#9aa3b2; font-size:.9rem; margin:0 0 10px; }
  .update-desc{ color:#c9cbd1; margin:0 0 12px; line-height:1.55; }
  .update-link{ display:inline-flex; align-items:center; gap:8px; padding:8px 10px; border:1px solid rgba(255,255,255,.16); border-radius:10px; background:#0f0f0f; color:#fff; font-weight:700; text-decoration:none; }
  .update-link:hover{ border-color:#4da0ff; background:#141414; }
  .update-link,
  .update-link:visited{
    color:#fff;
  }

  .update-link:hover,
  .update-link:focus{
    color:#fff;
  }

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

  /* Particles inside boards disabled */
  .particles,
  .particles .dot{
    display:none !important;
  }

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

  /* ===== HERO SOCIAL ICON BUTTONS + Play/Pause à droite ===== */
  .social-actions{
    margin-top:14px;
    display:flex;
    align-items:center;
    gap:12px;
  }
  .social-actions-left{
    display:flex;
    gap:12px;
  }
  .icon-btn{
    width:46px; height:46px; display:grid; place-items:center;
    border-radius:50%;
    background: radial-gradient(120% 120% at 30% 10%, rgba(44,140,255,.18), rgba(8,12,24,.9));
    border:1px solid rgba(76,139,255,.45);
    box-shadow: 0 8px 20px rgba(0,0,0,.35), inset 0 0 0 1px rgba(255,255,255,.04);
    transition: transform .15s ease, box-shadow .2s ease, border-color .2s ease, background .2s ease;
    text-decoration:none; outline:none;
  }
  .icon-btn:hover{
    transform: translateY(-1px);
    border-color:#6bb0ff;
    box-shadow: 0 12px 30px rgba(0,0,0,.45), 0 0 18px rgba(44,140,255,.25) inset;
    background: radial-gradient(120% 120% at 30% 10%, rgba(44,140,255,.28), rgba(10,14,28,.95));
  }
  .icon-btn:focus-visible{ box-shadow: 0 0 0 3px rgba(76,139,255,.35); }
  .icon-btn svg{ width:22px; height:22px; fill:#9ec8ff; }
  .icon-btn:hover svg{ fill:#ffffff; }
  .sr-only{ position:absolute; width:1px; height:1px; padding:0; margin:-1px; overflow:hidden; clip:rect(0,0,0,0); border:0; }
 
  /* Accent color for "Haagerton" */
  .brand-accent{
    color:#55aaff;            /* bleu lumineux cohérent avec ton thème */
    font-weight:800;          /* un peu plus affirmé */
    letter-spacing:0.5px;     /* léger effet premium */
  }

  /* === ABOUT ME — TIMELINE GRAPH (2020–2026) === */
  .hub-split .about-graph-card{
    grid-column:1 / -1;          /* la carte prend toute la largeur du grid */
  }

  .about-graph-card{
    margin-top:12px;
  }

  .about-graph-header{
    display:flex;
    align-items:flex-start;
    justify-content:space-between;
    gap:12px;
    position:relative;
    z-index:1;
  }

  .about-graph-header .card-sub{
    margin-top:2px;
    font-size:.9rem;
    color:#9aa3b2;
  }

  .timeline-graph-wrapper{
    position:relative;
    margin-top:12px;
    padding:22px 22px 18px;
    border-radius:18px;
    background: radial-gradient(120% 160% at 0% 0%, rgba(44,140,255,.08), transparent 60%),
                radial-gradient(120% 180% at 100% 100%, rgba(159,122,255,.08), transparent 60%),
                #050712;
    border:1px solid rgba(76,139,255,.35);
    box-shadow: 0 16px 38px rgba(0,0,0,.55), inset 0 0 0 1px rgba(255,255,255,.03);
    overflow:hidden;
  }

  .timeline-graph{
    display:block;
    width:100%;
    max-width:1100px; 
    margin:0 auto;
  }

  /* Axes + grille */
  .timeline-axis-line{
    stroke:#3f4e6d;
    stroke-width:1.6;
    stroke-linecap:round;
  }
  
  /* Y légèrement plus épais */
  .timeline-axis-y{
    stroke-width:1.8;
  }
  
  /* Nécessaire pour animer le scale proprement dans le repère SVG */
  .timeline-axis-y,
  .timeline-axis-x{
    transform-box: fill-box;
  }
  
  /* On veut que l’axe Y “pousse” depuis le bas, et l’axe X depuis la gauche */
  .timeline-axis-y{
    transform-origin: center bottom;
  }
  .timeline-axis-x{
    transform-origin: left center;
  }

  /* === PARTICULES AU NIVEAU DES FLÈCHES (nuages lumineux) === */
  
  .axis-tip-particles{
    pointer-events:none;
    transform-box:fill-box;
  }
  
  .axis-tip-particle{
    fill:#9ec8ff;
    opacity:0;
    filter:drop-shadow(0 0 8px rgba(44,140,255,.95));
    transform-origin:center center;
  }
  
  /* Flèche Y (en haut) : nuage qui pulse + légère respiration */
  .timeline-graph-wrapper.about-graph-visible .axis-tip-y .axis-tip-particle{
      animation: tipParticlesY 2.6s ease-out;
  }
  
  .timeline-graph-wrapper.about-graph-visible .axis-tip-x .axis-tip-particle{
      animation: tipParticlesX 2.9s ease-out;
  }
  
  /* Nuage au bout de la flèche Y : grosse respiration lumineuse */
  @keyframes tipParticlesY{
    0%{
      opacity:0;
      transform:scale(.3);
    }
    20%{
      opacity:1;
      transform:scale(1.0);
    }
    60%{
      opacity:1;
      transform:scale(1.15);
    }
    100%{
      opacity:0;
      transform:scale(1.35);
    }
  }
  
  /* Nuage au bout de la flèche X : léger drift horizontal + glow */
  @keyframes tipParticlesX{
    0%{
      opacity:0;
      transform:translateX(0) scale(.35);
    }
    20%{
      opacity:1;
      transform:translateX(-2px) scale(1.0);
    }
    60%{
      opacity:1;
      transform:translateX(4px) scale(1.15);
    }
    100%{
      opacity:0;
      transform:translateX(6px) scale(1.35);
    }
  }
 
  .timeline-grid-line{
    stroke:rgba(255,255,255,.04);
    stroke-width:1;
    stroke-dasharray:4 4;
  }

  .timeline-label-year{
    fill:#9aa3b2;
    font-size:13px;          /* au lieu de 11px */
    font-weight:500;         /* un peu plus lisible */
    font-family:-apple-system,BlinkMacSystemFont,"Segoe UI",Roboto,Helvetica,Arial,sans-serif;
  }

  .timeline-label-event{
    fill:#9ec8ff;
    font-size:11px;
    font-family:-apple-system,BlinkMacSystemFont,"Segoe UI",Roboto,Helvetica,Arial,sans-serif;
  }

  .timeline-label-axis{
    fill:#cfe3ff;
    font-size:13px;          /* au lieu de 12px */
    font-weight:700;         /* plus affirmé */
    letter-spacing:.08em;
    text-transform:uppercase;
    font-family:-apple-system,BlinkMacSystemFont,"Segoe UI",Roboto,Helvetica,Arial,sans-serif;
  }

  .timeline-path{
    fill:none;
    stroke-width:2.6;
    stroke-linecap:round;
    stroke-linejoin:round;
    stroke-dasharray:620;
    stroke-dashoffset:620;
    opacity:0;
  }

  .timeline-point{
    stroke-width:1.8;
  }

  .timeline-point-core{
    fill:#e7f1ff;
    opacity:0;
  }

  .timeline-point-glow{
    fill:url(#pointGlow);
    opacity:0;
  }

  .timeline-tag{
    fill:#e7efff;
    font-size:11px;
    font-family:-apple-system,BlinkMacSystemFont,"Segoe UI",Roboto,Helvetica,Arial,sans-serif;
  }
  
  .timeline-graph-wrapper.about-graph-visible .timeline-path{
    animation: drawPath 2.4s cubic-bezier(.23,.83,.32,1) 1.1s forwards;
  }
  .timeline-graph-wrapper.about-graph-visible .timeline-point-core,
  .timeline-graph-wrapper.about-graph-visible .timeline-point-glow{
    animation:fadePoint 0.6s ease-out forwards;
  }
  .timeline-graph-wrapper.about-graph-visible .timeline-point-core:nth-of-type(1),
  .timeline-graph-wrapper.about-graph-visible .timeline-point-glow:nth-of-type(1){
    animation-delay:0.85s;
  }
  .timeline-graph-wrapper.about-graph-visible .timeline-point-core:nth-of-type(2),
  .timeline-graph-wrapper.about-graph-visible .timeline-point-glow:nth-of-type(2){
    animation-delay:1.0s;
  }
  .timeline-graph-wrapper.about-graph-visible .timeline-point-core:nth-of-type(3),
  .timeline-graph-wrapper.about-graph-visible .timeline-point-glow:nth-of-type(3){
    animation-delay:1.15s;
  }
  .timeline-graph-wrapper.about-graph-visible .timeline-point-core:nth-of-type(4),
  .timeline-graph-wrapper.about-graph-visible .timeline-point-glow:nth-of-type(4){
    animation-delay:1.3s;
  }
  .timeline-graph-wrapper.about-graph-visible .timeline-point-core:nth-of-type(5),
  .timeline-graph-wrapper.about-graph-visible .timeline-point-glow:nth-of-type(5){
    animation-delay:1.45s;
  }
  .timeline-graph-wrapper.about-graph-visible .timeline-point-core:nth-of-type(6),
  .timeline-graph-wrapper.about-graph-visible .timeline-point-glow:nth-of-type(6){
    animation-delay:1.6s;
  }
  .timeline-graph-wrapper.about-graph-visible .timeline-point-core:nth-of-type(7),
  .timeline-graph-wrapper.about-graph-visible .timeline-point-glow:nth-of-type(7){
    animation-delay:1.75s;
  }

  .timeline-point,
  .timeline-point-core,
  .timeline-point-glow{
    display: none;
  }
 
  .timeline-graph-wrapper.about-graph-visible .timeline-point-core{
    animation-name:fadePoint,pulsePoint;
    animation-duration:0.6s,2.2s;
    animation-timing-function:ease-out,ease-in-out;
    animation-iteration-count:1,infinite;
  }
  .timeline-graph-wrapper.about-graph-visible .timeline-point-glow{
    animation-name:fadePoint,softGlow;
    animation-duration:0.6s,3.4s;
    animation-timing-function:ease-out,ease-in-out;
    animation-iteration-count:1,infinite;
  }

  @keyframes drawAxisY{
    0%{
      stroke-dashoffset:520;
      opacity:0;
      transform:scaleY(0.4);
    }
    35%{
      opacity:1;
    }
    70%{
      stroke-dashoffset:60;
      transform:scaleY(1.05);
    }
    100%{
      stroke-dashoffset:0;
      opacity:1;
      transform:scaleY(1);
    }
  }
  
  @keyframes drawAxisX{
    0%{
      stroke-dashoffset:520;
      opacity:0;
      transform:scaleX(0.4);
    }
    35%{
      opacity:1;
    }
    70%{
      stroke-dashoffset:60;
      transform:scaleX(1.04);
    }
    100%{
      stroke-dashoffset:0;
      opacity:1;
      transform:scaleX(1);
    }
  }

  @keyframes drawPath{
    0%{ stroke-dashoffset:620; opacity:1; }
    100%{ stroke-dashoffset:0; opacity:1; }
  }

  @keyframes fadePoint{
    from{ opacity:0; transform:scale(.4); }
    to  { opacity:1; transform:scale(1); }
  }

  @keyframes pulsePoint{
    0%,100%{ transform:scale(1); }
    50%{ transform:scale(1.3); }
  }

  @keyframes softGlow{
    0%,100%{ opacity:.45; }
    50%{ opacity:.9; }
  }

  /* Légende en haut à droite du graphe */
  .timeline-legend{
    fill:#9aa3b2;
    font-size:10px;
    font-family:-apple-system,BlinkMacSystemFont,"Segoe UI",Roboto,Helvetica,Arial,sans-serif;
  }
 
</style>

<section class="hero-video">
  <div class="hero-content">
    <p class="eyebrow shifted">Quantitative Finance & Trading</p>
    <h1>Turning Models into Market Impact</h1>
    <p class="subtitle" style="text-align: justify;">
      Welcome to <span class="brand-accent">Haagerton</span>, my quantitative finance and trading lab.  
      I explore the mechanics of modern markets through stochastic calculus and SDEs, 
      term-structure and volatility-surface models, Monte Carlo engines and PDE solvers, 
      as well as high-frequency order book dynamics and optimal execution.  
      On this site, I will publish books, long-form, highly technical volumes in quantitative finance.
    </p>

    <!-- ==== Social / Contact + Play/Pause vidéo ==== -->
    <div class="social-actions" aria-label="Contact links and video controls">
      <div class="social-actions-left">
        <!-- LinkedIn -->
        <a class="icon-btn" href="https://www.linkedin.com/in/s%C3%A9bastien-haag/" target="_blank" rel="noopener noreferrer" aria-label="Open LinkedIn profile" title="LinkedIn">
          <span class="sr-only">LinkedIn</span>
          <!-- LinkedIn SVG -->
          <svg viewBox="0 0 24 24" role="img" aria-hidden="true">
            <path d="M4.98 3.5C4.98 4.88 3.86 6 2.5 6S0 4.88 0 3.5 1.12 1 2.5 1s2.48 1.12 2.48 2.5zM0 8h5v16H0V8zm7.5 0H12v2.2h.06c.63-1.2 2.16-2.46 4.45-2.46 4.76 0 5.64 3.13 5.64 7.2V24h-5v-6.9c0-1.65-.03-3.77-2.3-3.77-2.3 0-2.65 1.8-2.65 3.65V24h-5V8z"/>
          </svg>
        </a>
        <!-- Email -->
        <a class="icon-btn" href="mailto:sbthaag@gmail.com" aria-label="Send me an email" title="Email">
          <span class="sr-only">Email</span>
          <!-- Envelope SVG -->
          <svg viewBox="0 0 24 24" role="img" aria-hidden="true">
            <path d="M20 4H4c-1.1 0-2 .9-2 2v12a2 2 0 0 0 2 2h16a2 2 0 0 0 2-2V6c0-1.1-.9-2-2-2zm0 4-8 5-8-5V6l8 5 8-5v2z"/>
          </svg>
        </a>
      </div>

      <!-- Bouton play / pause (contrôle la vidéo promo) -->
      <button
        class="promo-video-toggle"
        id="promoVideoToggle"
        type="button"
        aria-label="Pause background video"
        title="Pause background video">
        <span class="sr-only">Toggle background video</span>
        <span class="promo-video-toggle-icon">❚❚</span>
      </button>
    </div>
  </div>

  <img class="hero-logo-img" src="/assets/images/sh-logo.png" alt="SH monogram">
</section>

<!-- ===== Full-width secondary video ===== -->
<section class="promo-video">
  <div class="promo-video-frame">
    <video
      id="promoVideo"
      class="promo-video-el"
      autoplay
      muted
      loop
      playsinline
      preload="auto"
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

<!-- ===== Latest Updates — CAROUSEL ===== -->
<section class="news-band">
  <div class="updates-wrap">
    <div class="updates-head">
      <div class="updates-label">
        <span class="updates-title">LATEST UPDATES</span>
        <span class="updates-counter" id="updatesCounter">3</span>
      </div>
    
      <div class="updates-ctrls" role="group" aria-label="Carousel controls">
        <button class="updates-btn" id="updPrev" aria-label="Previous update" title="Previous" type="button">‹</button>
        <button class="updates-btn" id="updNext" aria-label="Next update" title="Next" type="button">›</button>
      </div>
    </div>

    <div class="updates-stage" id="updatesStage" aria-live="polite">
      <div class="updates-fade" aria-hidden="true"></div>
      <div class="updates-track" id="updatesTrack">
        <!-- Card 1 (ex-INFO) -->
        <article class="update-card" data-card="0" tabindex="0">
          <span class="update-badge">INFO</span>
          <h3 class="update-title">Website under construction</h3>
          <p class="update-meta">Dec 2025 · Ongoing</p>
          <p class="update-desc">
            This website is currently being enhanced, new pages, animations, and live data integrations are coming soon.
            Stay tuned for the full Quantitative Finance & Trading experience.
          </p>
        </article>

        <!-- Card 2 (ex-UPDATE) -->
        <article class="update-card" data-card="1" tabindex="0">
          <span class="update-badge">NOTE</span>
          <h3 class="update-title">About Me - Quant Engineering</h3>
          <p class="update-meta">Oct 2025 · My professional background</p>
          <p class="update-desc">
            You will find below all the information about my background and my past professional experiences.
          </p>
        </article>

        <!-- Card 3 (Book teaser) -->
        <article class="update-card teaser-armed" data-card="2" tabindex="0">
          <span class="update-badge">COMING SOON</span>
          <h3 class="update-title">My first book - Preview</h3>
          <p class="update-meta">March 2026 · Teaser</p>
        
          <!-- Teaser vidéo : même taille que le texte (hauteur limitée) -->
          <div class="update-teaser-wrapper">
            <video
              class="update-teaser-video"
              muted
              playsinline
              preload="none"
              poster="{{ '/assets/images/book-teaser-poster.jpg' | relative_url }}">
              <source src="{{ '/assets/videos/f5150d5a-7fc4-4fa8-862c-555e8c402526.mp4' | relative_url }}" type="video/mp4">
              Your browser does not support the video tag.
            </video>
          </div>
        
          <!-- Texte qui apparaît après la vidéo -->
          <p class="update-desc">
            The core foundations of quantitative finance, distilled into one comprehensive volume.
          </p>
          <a class="update-link" href="#" id="bookTeaserReplay">Watch the teaser →</a>
        </article>
      </div>
    </div>
  </div>
</section>

<!-- ===== SECTION HUB (tabs) ===== -->
<section class="after-market">
  <div class="hub-inner">
    <p class="hub-eyebrow">Activities</p>
    <h2 class="hub-title">The different sections</h2>

    <nav class="hub-tabs" id="hubTabs" aria-label="Sections">
      <a class="hub-tab is-active" data-tab="what" href="#what" role="tab" aria-selected="true">About Me</a>
      <a class="hub-tab" data-tab="reading" href="#reading" role="tab" aria-selected="false">Books</a>
    </nav>

    <h3 class="hub-selected-title" id="hubSelectedTitle">ABOUT ME</h3>

    <!-- ===== SPLIT (ABOUT ME = timeline graph) ===== -->
    <div class="hub-split" id="hubSplit">
      <div class="about-graph-card card-glass">
        <div class="about-graph-header">
          <div>
            <h4 class="card-title">Quant Timeline 2020–2027</h4>
            <p class="card-sub">Orthogonal view of my journey in quantitative finance.</p>
          </div>
        </div>

        <div class="timeline-graph-wrapper" id="aboutTimeline">
          <svg class="timeline-graph" viewBox="0 0 600 400" preserveAspectRatio="xMidYMid meet" role="img" aria-label="Timeline 2020–2027">
            <defs>
              <!-- Dégradé pour les axes -->
              <linearGradient id="axisGradient" x1="0%" y1="0%" x2="100%" y2="0%">
                <stop offset="0%" stop-color="#2c8cff" stop-opacity="0.3"/>
                <stop offset="50%" stop-color="#9ec8ff" stop-opacity="0.9"/>
                <stop offset="100%" stop-color="#9f7aff" stop-opacity="0.6"/>
              </linearGradient>

              <!-- Dégradé pour la courbe -->
              <linearGradient id="pathGradient" x1="0%" y1="0%" x2="100%" y2="0%">
                <stop offset="0%" stop-color="#2c8cff"/>
                <stop offset="40%" stop-color="#7ad2ff"/>
                <stop offset="100%" stop-color="#9f7aff"/>
              </linearGradient>

              <!-- Glow des points -->
              <radialGradient id="pointGlow" cx="50%" cy="50%" r="50%">
                <stop offset="0%" stop-color="#cfe3ff" stop-opacity="0.9"/>
                <stop offset="40%" stop-color="#2c8cff" stop-opacity="0.4"/>
                <stop offset="100%" stop-color="#2c8cff" stop-opacity="0"/>
              </radialGradient>

              <!-- Flèche des axes -->
              <marker id="axisArrow"
                      viewBox="0 0 12 12"
                      refX="12" refY="6"
                      markerWidth="12" markerHeight="12"
                      orient="auto"
                      markerUnits="strokeWidth">
              
                <!-- Flèche un peu plus grande -->
                <path d="M 0 0 L 12 6 L 0 12 z" fill="#9ec8ff"/>
              
              </marker>  
            </defs>

            <!-- Grille horizontale (événements / niveaux) -->
            <g></g>

            <!-- Axes -->
            <g>
              <!-- Axe Y (événements) -->
              <line x1="70" y1="340" x2="70" y2="340"
                    class="timeline-axis-line timeline-axis-y"
                    stroke="url(#axisGradient)"
                    marker-end="url(#axisArrow)"/>
                    
              <!-- Axe X (temps) -->
              <line x1="70" y1="340" x2="70" y2="340"
                    class="timeline-axis-line timeline-axis-x"
                    stroke="url(#axisGradient)"
                    marker-end="url(#axisArrow)"/>
            </g>

            <!-- Nuage de particules au bout de la flèche de l’axe Y (en haut) -->
            <g class="axis-tip-particles axis-tip-y" transform="translate(70,40)">
              <circle class="axis-tip-particle" cx="0"   cy="0"   r="2.4" />
              <circle class="axis-tip-particle" cx="-4"  cy="-3"  r="2.1" />
              <circle class="axis-tip-particle" cx="3"   cy="-4"  r="1.9" />
              <circle class="axis-tip-particle" cx="-2"  cy="4"   r="1.7" />
              <circle class="axis-tip-particle" cx="5"   cy="2"   r="1.6" />
              <circle class="axis-tip-particle" cx="-6"  cy="1"   r="1.5" />
              <circle class="axis-tip-particle" cx="1.5" cy="6"   r="1.4" />
              <circle class="axis-tip-particle" cx="7"   cy="-1"  r="1.3" />
            </g>
            
            <!-- Nuage de particules au bout de la flèche de l’axe X (à droite) -->
            <g class="axis-tip-particles axis-tip-x" transform="translate(580,340)">
              <circle class="axis-tip-particle" cx="0"   cy="0"   r="2.4" />
              <circle class="axis-tip-particle" cx="-3"  cy="-3"  r="2.1" />
              <circle class="axis-tip-particle" cx="-4"  cy="2"   r="1.9" />
              <circle class="axis-tip-particle" cx="3"   cy="-4"  r="1.8" />
              <circle class="axis-tip-particle" cx="5.5" cy="1"   r="1.6" />
              <circle class="axis-tip-particle" cx="2"   cy="4.5" r="1.5" />
              <circle class="axis-tip-particle" cx="-6"  cy="0"   r="1.4" />
              <circle class="axis-tip-particle" cx="7"   cy="-1"  r="1.3" />
            </g>

            <!-- Labels axe Y (événements abstraits, on pourra raffiner) -->
            <g></g>

            <!-- Labels axe X (années) -->
            <g>
              <text x="70"  y="356" class="timeline-label-year">2020</text>
              <text x="150" y="356" class="timeline-label-year">2021</text>
              <text x="230" y="356" class="timeline-label-year">2022</text>
              <text x="310" y="356" class="timeline-label-year">2023</text>
              <text x="390" y="356" class="timeline-label-year">2024</text>
              <text x="470" y="356" class="timeline-label-year">2025</text>
              <text x="550" y="356" class="timeline-label-year">2026</text>
            </g>

            <!-- Courbe des événements (forme en cloche / loi normale) -->
            <g>
              <path
                class="timeline-path"
                stroke="url(#pathGradient)"
                d="
                  M 70 260
                  C 150 260, 220 180, 310 120
                  C 400 60,  470 180, 550 260
                "
              />
            </g>

            <!-- Points marquants (alignés sur la courbe) -->
            <g>
            </g>

            <!-- Légende en haut à droite -->
            <g id="particleLayer"></g>
          </svg>
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

    <!-- ===== READING PANEL ===== -->
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
              <span class="btn-chip" aria-disabled="true" title="Bientôt">All readings</span>
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

<!-- ===== BANDEAU LECTURES ===== -->
<section class="reading-band">
  <div class="reading-inner">
    <p class="reading-eyebrow">READINGS — ON MY DESK</p>
    <div class="reading-track" aria-label="Lectures en cours">
      <div class="reading-chip"><span class="reading-badge">BOOK</span> Paul Wilmott on Quantitative Finance — Stochastic calculus, volatility, pricing, risk</div>
      <div class="reading-chip"><span class="reading-badge">GUIDE</span> Ultimate Bloomberg Guide — Terminal navigation, market functions, Fixed Income analytics</div>
      <div class="reading-chip"><span class="reading-badge">BOOK</span> Options, Futures & Other Derivatives (Hull) — BSM, exotics, VaR, credit risk</div>

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
    const urls={
      tokyo:"https://www.jpx.co.jp/english/markets/",
      london:"https://www.londonstockexchange.com/",
      paris:"https://live.euronext.com/en/markets/paris",
      ny:"https://www.nyse.com/"
    };
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
    reading:  'Curated reading lists and annotations across papers, textbooks and articles that influenced my thinking on modeling, risk, markets and systems design.',
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

  activate('what', 'ABOUT ME');
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
    const n = 0;

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

/* === Updates Carousel logic === */
(function(){
  const track = document.getElementById('updatesTrack');
  const stage = document.getElementById('updatesStage');
  const btnPrev = document.getElementById('updPrev');
  const btnNext = document.getElementById('updNext');
  const cards = Array.from(track.querySelectorAll('.update-card'));
  const counterEl = document.getElementById('updatesCounter');

  // === Teaser vidéo "My first book" ===
  const bookCard  = cards.find(c => c.dataset.card === '2');
  const bookIndex = bookCard ? cards.indexOf(bookCard) : -1;
  const bookVideo = bookCard ? bookCard.querySelector('.update-teaser-video') : null;
  const bookReplayLink = bookCard ? bookCard.querySelector('#bookTeaserReplay') : null;
  let bookTeaserPlayed = false;
  let bookCardInitialHeight = null;

  if (bookVideo && bookCard){
    // Quand la vidéo se termine naturellement → outro vidéo stylée puis texte
    bookVideo.addEventListener('ended', () => {
      bookTeaserPlayed = true;

      // 1) on sort de l'état "playing" et on lance l'OUTRO
      bookCard.classList.remove('teaser-playing', 'teaser-armed');
      bookCard.classList.add('teaser-outro');

      // 2) après l'outro (0.7s), on bascule sur le texte normal
      setTimeout(() => {
        bookCard.classList.remove('teaser-outro');
        bookCard.classList.add('teaser-done');
        // on rend la hauteur auto à la fin
        bookCard.style.height = '';
      }, 700);
    });
  }

  // Option : clic sur "Watch the teaser →" pour rejouer
  if (bookVideo && bookCard && bookReplayLink){
    bookReplayLink.addEventListener('click', (e)=>{
      e.preventDefault();
      bookTeaserPlayed = false;
      bookCard.classList.remove('teaser-done', 'teaser-outro');
      bookCard.classList.add('teaser-armed', 'teaser-playing');
      bookVideo.currentTime = 0;
      bookVideo.play().catch(()=>{});
    });
  }

  function playBookTeaserIfNeeded(centerIndex){
    if (!bookCard || !bookVideo) return;
    if (centerIndex !== bookIndex) return;
    if (bookTeaserPlayed) return; // déjà vue → on laisse le texte

    // On mémorise la hauteur initiale de la carte (une seule fois)
    if (bookCardInitialHeight === null){
      bookCardInitialHeight = bookCard.offsetHeight;
    }
    // On fige la hauteur pour éviter que l'étiquette grandisse
    bookCard.style.height = bookCardInitialHeight + 'px';

    // Première fois qu'on arrive au centre sur la carte "book"
    bookCard.classList.add('teaser-armed', 'teaser-playing');
    bookVideo.currentTime = 0;
    const p = bookVideo.play();
    if (p && typeof p.then === 'function'){
      p.catch(()=> {
        // Autoplay bloqué → on montre directement le texte
        bookTeaserPlayed = true;
        bookCard.classList.remove('teaser-playing', 'teaser-armed');
        bookCard.classList.add('teaser-done');
        bookCard.style.height = '';
      });
    }
  }

  // --- Nouveau : suivi des cartes vues ---
  const seen = new Set();
  let unseenCount = cards.length;

  function updateCounter(){
    if (!counterEl) return;
    if (unseenCount > 0){
      counterEl.textContent = String(unseenCount);
      counterEl.style.display = '';
    } else {
      counterEl.style.display = 'none';
    }
  }
  updateCounter(); // initialisation

  function markSeen(i){
    if (seen.has(i)) return;      // déjà vue → on ne fait rien
    seen.add(i);
    unseenCount = Math.max(0, unseenCount - 1);
    updateCounter();
  }
  // ----------------------------------------

  let idx = 1; // démarre sur la carte du milieu (0,1,2)
  let lastRect = null;

  function getCurrentTranslateX(el){
    const tr = getComputedStyle(el).transform;
    if (!tr || tr === 'none') return 0;

    try{
      if (typeof DOMMatrixReadOnly !== 'undefined'){
        const m = new DOMMatrixReadOnly(tr);
        return m.m41;
      }
      if (typeof DOMMatrix !== 'undefined'){
        const m = new DOMMatrix(tr);
        return m.m41;
      }
      if (typeof WebKitCSSMatrix !== 'undefined'){
        const m = new WebKitCSSMatrix(tr);
        return m.m41;
      }
      const match = tr.match(/matrix\(([^)]+)\)/);
      if (match){
        const parts = match[1].split(',');
        return parseFloat(parts[4] || '0');
      }
    }catch(e){
      console.warn('getCurrentTranslateX fallback', e);
    }
    return 0;
  }

  function centerOn(i, withAnim=true){
    idx = (i + cards.length) % cards.length;
    const target = cards[idx];
    const stageRect = stage.getBoundingClientRect();
    const cardRect  = target.getBoundingClientRect();
    const offset = (stageRect.left + stageRect.right)/2 - (cardRect.left + cardRect.right)/2;

    const trackX = getCurrentTranslateX(track);
    const nextX = trackX + offset;

    if(!withAnim){ track.style.transition = 'none'; }
    track.style.transform = `translate3d(${nextX}px,0,0)`;
    if(!withAnim){
      requestAnimationFrame(()=>{ track.style.transition='transform .35s cubic-bezier(.2,.75,.2,1)'; });
    }

    cards.forEach(c => c.classList.remove('is-center'));
    target.classList.add('is-center');
    target.focus({preventScroll:true});

    // Marque la carte comme "vue" (compteur LATEST UPDATES)
    markSeen(idx);

    // Si c'est la carte "My first book", on lance le teaser vidéo une fois
    playBookTeaserIfNeeded(idx);
  }

  function recalc(){
    track.style.transition = 'none';
    track.style.transform = 'translate3d(0,0,0)';
    requestAnimationFrame(()=> centerOn(idx, false));
  }

  btnPrev.addEventListener('click', ()=> centerOn(idx-1));
  btnNext.addEventListener('click', ()=> centerOn(idx+1));

  // Keyboard (flèches)
  stage.addEventListener('keydown', (e)=>{
    if(e.key === 'ArrowLeft'){ e.preventDefault(); centerOn(idx-1); }
    else if(e.key === 'ArrowRight'){ e.preventDefault(); centerOn(idx+1); }
  });

  // Swipe
  let startX=0, dragging=false;
  function onDown(e){
    dragging=true;
    startX = (e.touches?e.touches[0].clientX:e.clientX);
    track.style.transition='none';
  }
  function onMove(e){
    if(!dragging) return;
    const x = (e.touches?e.touches[0].clientX:e.clientX);
    const dx = x - startX;
    const base = getCurrentTranslateX(track);
    track.style.transform = `translate3d(${base + dx}px,0,0)`;
    startX = x;
  }
  function onUp(){
    if(!dragging) return;
    dragging=false;
    const center = (stage.getBoundingClientRect().left + stage.getBoundingClientRect().right)/2;
    let best = 0, bestDist = Infinity;
    cards.forEach((c,i)=>{
      const r = c.getBoundingClientRect();
      const mid = (r.left + r.right)/2;
      const d = Math.abs(mid - center);
      if(d < bestDist){ bestDist=d; best=i; }
    });
    track.style.transition='transform .35s cubic-bezier(.2,.75,.2,1)';
    centerOn(best);
  }

  stage.addEventListener('mousedown', onDown);
  window.addEventListener('mousemove', onMove, {passive:false});
  window.addEventListener('mouseup', onUp);
  stage.addEventListener('touchstart', onDown, {passive:true});
  window.addEventListener('touchmove', onMove, {passive:false});
  window.addEventListener('touchend', onUp);

  // Reflow on resize/orientation change
  window.addEventListener('resize', ()=>{
    const r = stage.getBoundingClientRect().width;
    if(!lastRect || Math.abs(r - lastRect) > 2){
      lastRect = r;
      recalc();
    }
  });

  // Initial center (sur la 2e carte) → compte comme "vue"
  requestAnimationFrame(()=> centerOn(idx, false));
})();

/* === Play / Pause de la vidéo promo === */
(function(){
  const video = document.getElementById('promoVideo');
  const btn   = document.getElementById('promoVideoToggle');
  if (!video || !btn) return;

  const iconSpan = btn.querySelector('.promo-video-toggle-icon');

  function syncLabel(){
    if (video.paused){
      if (iconSpan) iconSpan.textContent = '▶';
      btn.setAttribute('aria-label','Play background video');
      btn.title = 'Play background video';
    } else {
      if (iconSpan) iconSpan.textContent = '❚❚';
      btn.setAttribute('aria-label','Pause background video');
      btn.title = 'Pause background video';
    }
  }

  btn.addEventListener('click', ()=>{
    if (video.paused){
      // certains navigateurs peuvent bloquer le play, on ignore juste l’erreur
      video.play().catch(()=>{});
    } else {
      video.pause();
    }
    syncLabel();
  });

})();
</script>

<script>
  // === ABOUT ME TIMELINE — Activation à l'apparition ===
  (function(){
    const wrapper = document.getElementById('aboutTimeline');
    if (!wrapper) return;

    function activate(){
      wrapper.classList.add('about-graph-visible');
    }

    // Si IntersectionObserver n'est pas dispo, on active directement
    if (!('IntersectionObserver' in window)){
      activate();
      return;
    }

    const io = new IntersectionObserver((entries)=>{
      entries.forEach(entry=>{
        if (entry.isIntersecting){
          activate();
          io.disconnect();
        }
      });
    }, {
      threshold:0.35
    });

    io.observe(wrapper);
  })();
</script>

<script>
(function(){
  const svg = document.querySelector('.timeline-graph');
  if (!svg) return;

  const axisX = svg.querySelector('.timeline-axis-x');
  const axisY = svg.querySelector('.timeline-axis-y');
  if (!axisX || !axisY) return;

  const duration = 3800; // même durée qu'avant

  // Coordonnées de départ / arrivée des axes
  const xStart = { x: 70,  y: 340 };
  const xEnd   = { x: 601, y: 340 }; // comme dans ton code actuel

  const yStart = { x: 70,  y: 340 };
  const yEnd   = { x: 70,  y: 40  };

  let start = null;
  let running = false;

  function animateAxes(timestamp){
    if (!start) start = timestamp;
    const t = (timestamp - start) / duration;
    const progress = Math.min(1, t);

    // interpolation linéaire
    const px = xStart.x + (xEnd.x - xStart.x) * progress;
    const py = xStart.y + (xEnd.y - xStart.y) * progress;

    const qx = yStart.x + (yEnd.x - yStart.x) * progress;
    const qy = yStart.y + (yEnd.y - yStart.y) * progress;

    // mise à jour des axes
    axisX.setAttribute("x2", px);
    axisX.setAttribute("y2", py);

    axisY.setAttribute("x2", qx);
    axisY.setAttribute("y2", qy);

    // plus AUCUNE particule JS
    if (progress < 1){
      requestAnimationFrame(animateAxes);
    }
  }

  const wrapper = document.getElementById("aboutTimeline");
  if (!wrapper){
    // fallback : on anime quand même si le wrapper n'existe pas
    requestAnimationFrame(animateAxes);
    return;
  }

  // On démarre l'animation quand la section devient visible
  const io = new IntersectionObserver((entries)=>{
    entries.forEach(entry=>{
      if (entry.isIntersecting && !running){
        running = true;
        requestAnimationFrame(animateAxes);
        io.disconnect();
      }
    });
  }, { threshold: 0.4 });

  io.observe(wrapper);
})();
</script>
