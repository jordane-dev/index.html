<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>TalentBridge — La Marketplace Mondiale des Talents Africains</title>
  <link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,700;0,900;1,700&family=DM+Sans:wght@300;400;500;600&display=swap" rel="stylesheet"/>
  <style>
    :root {
      --night:    #0A1628;
      --navy:     #0D1F3C;
      --gold:     #D4A843;
      --gold-lt:  #F0C96A;
      --terra:    #C4622D;
      --cream:    #F7EDD8;
      --cream-dk: #EDD9B0;
      --sage:     #3A7D6B;
      --white:    #FFFFFF;
      --muted:    rgba(247,237,216,0.55);
    }

    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

    html { scroll-behavior: smooth; }

    body {
      font-family: 'DM Sans', sans-serif;
      background: var(--night);
      color: var(--cream);
      overflow-x: hidden;
    }

    /* ── NOISE OVERLAY ── */
    body::before {
      content: '';
      position: fixed; inset: 0;
      background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noise'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noise)' opacity='0.04'/%3E%3C/svg%3E");
      pointer-events: none; z-index: 0; opacity: .5;
    }

    /* ── NAV ── */
    nav {
      position: fixed; top: 0; left: 0; right: 0;
      z-index: 100;
      display: flex; align-items: center; justify-content: space-between;
      padding: 1.25rem 5%;
      background: rgba(10,22,40,0.85);
      backdrop-filter: blur(14px);
      border-bottom: 1px solid rgba(212,168,67,0.12);
    }

    .nav-logo {
      font-family: 'Playfair Display', serif;
      font-size: 1.5rem; font-weight: 900;
      color: var(--gold);
      letter-spacing: -0.5px;
      text-decoration: none;
    }
    .nav-logo span { color: var(--cream); }

    .nav-links { display: flex; gap: 2rem; align-items: center; }
    .nav-links a {
      color: var(--muted); font-size: .9rem; font-weight: 500;
      text-decoration: none; transition: color .2s;
    }
    .nav-links a:hover { color: var(--gold); }

    .btn {
      display: inline-flex; align-items: center; justify-content: center;
      gap: .5rem; padding: .7rem 1.6rem;
      border-radius: 6px; font-family: 'DM Sans', sans-serif;
      font-weight: 600; font-size: .9rem;
      cursor: pointer; border: none; text-decoration: none;
      transition: transform .18s, box-shadow .18s, background .18s;
    }
    .btn:hover { transform: translateY(-2px); }

    .btn-gold {
      background: var(--gold);
      color: var(--night);
      box-shadow: 0 4px 22px rgba(212,168,67,.35);
    }
    .btn-gold:hover { background: var(--gold-lt); box-shadow: 0 6px 32px rgba(212,168,67,.5); }

    .btn-outline {
      background: transparent;
      border: 1.5px solid var(--gold);
      color: var(--gold);
    }
    .btn-outline:hover { background: rgba(212,168,67,.1); }

    .btn-terra {
      background: var(--terra);
      color: var(--white);
      box-shadow: 0 4px 22px rgba(196,98,45,.3);
    }
    .btn-terra:hover { background: #d96e35; box-shadow: 0 6px 32px rgba(196,98,45,.45); }

    .btn-lg { padding: 1rem 2.4rem; font-size: 1rem; border-radius: 8px; }

    /* ── HERO ── */
    #hero {
      position: relative;
      min-height: 100vh;
      display: flex; flex-direction: column; justify-content: center;
      padding: 10rem 5% 6rem;
      overflow: hidden;
    }

    .hero-orb {
      position: absolute;
      border-radius: 50%;
      filter: blur(90px);
      pointer-events: none;
    }
    .orb-1 {
      width: 600px; height: 600px;
      background: radial-gradient(circle, rgba(212,168,67,.18) 0%, transparent 70%);
      top: -150px; right: -100px;
      animation: drift 12s ease-in-out infinite alternate;
    }
    .orb-2 {
      width: 400px; height: 400px;
      background: radial-gradient(circle, rgba(196,98,45,.15) 0%, transparent 70%);
      bottom: 0; left: -80px;
      animation: drift 9s ease-in-out infinite alternate-reverse;
    }
    .orb-3 {
      width: 300px; height: 300px;
      background: radial-gradient(circle, rgba(58,125,107,.12) 0%, transparent 70%);
      top: 40%; left: 40%;
      animation: drift 15s ease-in-out infinite alternate;
    }

    @keyframes drift {
      from { transform: translate(0,0) scale(1); }
      to   { transform: translate(30px, 20px) scale(1.08); }
    }

    .hero-badge {
      display: inline-flex; align-items: center; gap: .5rem;
      background: rgba(212,168,67,.12);
      border: 1px solid rgba(212,168,67,.3);
      border-radius: 100px;
      padding: .4rem 1rem; font-size: .8rem; font-weight: 600;
      color: var(--gold); letter-spacing: .5px; text-transform: uppercase;
      margin-bottom: 2rem;
      animation: fadeUp .8s ease both;
    }
    .badge-dot {
      width: 7px; height: 7px; border-radius: 50%;
      background: var(--gold);
      animation: pulse 2s ease-in-out infinite;
    }
    @keyframes pulse {
      0%,100% { opacity: 1; transform: scale(1); }
      50%      { opacity: .4; transform: scale(1.4); }
    }

    .hero-title {
      font-family: 'Playfair Display', serif;
      font-size: clamp(2.8rem, 6vw, 5.5rem);
      font-weight: 900;
      line-height: 1.05;
      max-width: 780px;
      animation: fadeUp .9s .1s ease both;
    }
    .hero-title em {
      font-style: italic;
      background: linear-gradient(135deg, var(--gold), var(--terra));
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      background-clip: text;
    }

    .hero-sub {
      margin-top: 1.6rem;
      font-size: 1.15rem; font-weight: 300;
      color: var(--muted); max-width: 520px; line-height: 1.7;
      animation: fadeUp .9s .2s ease both;
    }

    .hero-ctas {
      display: flex; flex-wrap: wrap; gap: 1rem;
      margin-top: 2.6rem;
      animation: fadeUp .9s .3s ease both;
    }

    .hero-stats {
      display: flex; flex-wrap: wrap; gap: 2.5rem;
      margin-top: 4rem;
      padding-top: 2.5rem;
      border-top: 1px solid rgba(247,237,216,.08);
      animation: fadeUp .9s .4s ease both;
    }
    .stat-item { }
    .stat-num {
      font-family: 'Playfair Display', serif;
      font-size: 2.2rem; font-weight: 900;
      color: var(--gold); line-height: 1;
    }
    .stat-label {
      font-size: .8rem; font-weight: 500;
      color: var(--muted); margin-top: .3rem;
      text-transform: uppercase; letter-spacing: .6px;
    }

    .hero-scroll {
      position: absolute; bottom: 2.5rem; left: 50%;
      transform: translateX(-50%);
      display: flex; flex-direction: column; align-items: center; gap: .4rem;
      color: var(--muted); font-size: .75rem; letter-spacing: 1px;
      text-transform: uppercase; animation: bounce 2s ease-in-out infinite;
    }
    .hero-scroll-line {
      width: 1px; height: 40px;
      background: linear-gradient(to bottom, var(--gold), transparent);
    }
    @keyframes bounce {
      0%,100% { transform: translateX(-50%) translateY(0); }
      50%      { transform: translateX(-50%) translateY(6px); }
    }

    @keyframes fadeUp {
      from { opacity: 0; transform: translateY(24px); }
      to   { opacity: 1; transform: translateY(0); }
    }

    /* ── SECTION COMMONS ── */
    section { position: relative; z-index: 1; }

    .section-inner {
      max-width: 1200px;
      margin: 0 auto;
      padding: 7rem 5%;
    }

    .section-tag {
      display: inline-block;
      font-size: .75rem; font-weight: 700;
      letter-spacing: 2px; text-transform: uppercase;
      color: var(--gold); margin-bottom: 1rem;
    }

    .section-title {
      font-family: 'Playfair Display', serif;
      font-size: clamp(2rem, 4vw, 3.2rem);
      font-weight: 900; line-height: 1.1;
      max-width: 640px;
    }

    .section-title em {
      font-style: italic;
      color: var(--gold);
    }

    .section-sub {
      font-size: 1rem; font-weight: 300;
      color: var(--muted); max-width: 500px;
      line-height: 1.75; margin-top: 1rem;
    }

    /* ── PROBLEM ── */
    #problem { background: var(--navy); }

    .problem-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
      gap: 1.5rem;
      margin-top: 3.5rem;
    }

    .problem-card {
      background: rgba(247,237,216,.04);
      border: 1px solid rgba(247,237,216,.08);
      border-radius: 16px;
      padding: 2rem;
      transition: border-color .25s, transform .25s;
    }
    .problem-card:hover {
      border-color: rgba(212,168,67,.3);
      transform: translateY(-4px);
    }

    .problem-icon {
      font-size: 2rem; margin-bottom: 1rem;
    }

    .problem-card h3 {
      font-family: 'Playfair Display', serif;
      font-size: 1.2rem; font-weight: 700;
      margin-bottom: .6rem;
    }

    .problem-card p {
      font-size: .9rem; color: var(--muted); line-height: 1.65;
    }

    .problem-card .big-num {
      font-family: 'Playfair Display', serif;
      font-size: 3rem; font-weight: 900;
      color: var(--terra); line-height: 1;
      margin-bottom: .5rem;
    }

    /* ── HOW IT WORKS ── */
    #how { background: var(--night); }

    .how-grid {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 5rem;
      margin-top: 4rem;
      align-items: start;
    }

    .how-side-label {
      display: inline-flex; align-items: center; gap: .6rem;
      font-size: .8rem; font-weight: 700; letter-spacing: 1.5px;
      text-transform: uppercase; margin-bottom: 2rem;
      padding: .5rem 1.2rem;
      border-radius: 100px;
    }
    .label-talent {
      background: rgba(212,168,67,.12);
      color: var(--gold);
      border: 1px solid rgba(212,168,67,.25);
    }
    .label-company {
      background: rgba(196,98,45,.12);
      color: var(--terra);
      border: 1px solid rgba(196,98,45,.25);
    }

    .how-steps { display: flex; flex-direction: column; gap: 0; }

    .how-step {
      display: flex; gap: 1.5rem;
      padding-bottom: 2rem;
      position: relative;
    }
    .how-step:not(:last-child)::before {
      content: '';
      position: absolute;
      left: 19px; top: 42px;
      width: 1px; bottom: 0;
      background: linear-gradient(to bottom, rgba(212,168,67,.3), transparent);
    }

    .step-num {
      flex-shrink: 0;
      width: 40px; height: 40px;
      border-radius: 50%;
      background: rgba(212,168,67,.12);
      border: 1.5px solid rgba(212,168,67,.4);
      display: flex; align-items: center; justify-content: center;
      font-family: 'Playfair Display', serif;
      font-size: .9rem; font-weight: 900;
      color: var(--gold);
    }
    .how-step.terra .step-num {
      background: rgba(196,98,45,.12);
      border-color: rgba(196,98,45,.4);
      color: var(--terra);
    }

    .step-body h4 {
      font-family: 'Playfair Display', serif;
      font-size: 1.05rem; font-weight: 700;
      margin-bottom: .3rem;
    }
    .step-body p {
      font-size: .88rem; color: var(--muted); line-height: 1.6;
    }

    /* ── FEATURES ── */
    #features { background: var(--navy); }

    .features-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
      gap: 1.5rem;
      margin-top: 3.5rem;
    }

    .feat-card {
      background: rgba(10,22,40,.7);
      border: 1px solid rgba(247,237,216,.07);
      border-radius: 18px;
      padding: 2.2rem;
      transition: all .25s;
      position: relative;
      overflow: hidden;
    }
    .feat-card::before {
      content: '';
      position: absolute; top: 0; left: 0; right: 0;
      height: 2px;
      background: linear-gradient(90deg, transparent, var(--gold), transparent);
      opacity: 0;
      transition: opacity .25s;
    }
    .feat-card:hover::before { opacity: 1; }
    .feat-card:hover { border-color: rgba(212,168,67,.2); transform: translateY(-4px); }

    .feat-icon {
      width: 48px; height: 48px; border-radius: 12px;
      display: flex; align-items: center; justify-content: center;
      font-size: 1.4rem; margin-bottom: 1.4rem;
      background: rgba(212,168,67,.1);
    }

    .feat-card h3 {
      font-family: 'Playfair Display', serif;
      font-size: 1.15rem; font-weight: 700;
      margin-bottom: .5rem;
    }

    .feat-card p {
      font-size: .88rem; color: var(--muted); line-height: 1.65;
    }

    /* ── BRIDGE VISUAL ── */
    #bridge {
      background: linear-gradient(135deg, #0D1F3C 0%, #0A1628 50%, #1a1200 100%);
      overflow: hidden;
    }

    .bridge-inner {
      max-width: 1100px; margin: 0 auto;
      padding: 7rem 5%;
      text-align: center;
    }

    .bridge-diagram {
      display: flex; align-items: center; justify-content: center;
      gap: 0;
      margin: 4rem 0;
      flex-wrap: wrap;
    }

    .bridge-side {
      background: rgba(247,237,216,.05);
      border: 1px solid rgba(247,237,216,.1);
      border-radius: 16px;
      padding: 2rem 2.5rem;
      min-width: 220px;
    }

    .bridge-side h3 {
      font-family: 'Playfair Display', serif;
      font-size: 1.1rem; font-weight: 700;
      margin-bottom: 1rem;
      color: var(--gold);
    }

    .bridge-side ul {
      list-style: none;
      display: flex; flex-direction: column; gap: .5rem;
    }

    .bridge-side li {
      font-size: .85rem; color: var(--muted);
      display: flex; align-items: center; gap: .5rem;
    }
    .bridge-side li::before {
      content: '✓';
      color: var(--sage); font-weight: 700;
    }

    .bridge-center {
      flex: 1; min-width: 160px;
      display: flex; flex-direction: column;
      align-items: center; gap: 0; padding: 0 1rem;
    }

    .bridge-logo-big {
      font-family: 'Playfair Display', serif;
      font-size: 1.8rem; font-weight: 900;
      color: var(--gold);
      background: var(--night);
      border: 2px solid var(--gold);
      border-radius: 50%;
      width: 100px; height: 100px;
      display: flex; flex-direction: column;
      align-items: center; justify-content: center;
      line-height: 1;
      box-shadow: 0 0 50px rgba(212,168,67,.25);
      animation: glow 3s ease-in-out infinite;
    }
    .bridge-logo-big span { font-size: .6rem; letter-spacing: 1px; color: var(--cream-dk); }
    @keyframes glow {
      0%,100% { box-shadow: 0 0 30px rgba(212,168,67,.2); }
      50%      { box-shadow: 0 0 60px rgba(212,168,67,.45); }
    }

    .bridge-arrow {
      font-size: 1.5rem; color: var(--gold); opacity: .5;
    }

    .bridge-pillars {
      display: flex; gap: 1rem; flex-wrap: wrap;
      justify-content: center;
      margin: 3rem 0;
    }

    .pillar {
      background: rgba(247,237,216,.04);
      border: 1px solid rgba(247,237,216,.1);
      border-radius: 100px;
      padding: .6rem 1.4rem;
      font-size: .82rem; font-weight: 600;
      color: var(--cream-dk);
      display: flex; align-items: center; gap: .5rem;
    }
    .pillar-dot { width: 7px; height: 7px; border-radius: 50%; background: var(--gold); }

    /* ── MARKET ── */
    #market { background: var(--night); }

    .market-grid {
      display: grid;
      grid-template-columns: 1.2fr 1fr;
      gap: 5rem;
      margin-top: 4rem;
      align-items: center;
    }

    .tam-circles {
      display: flex; flex-direction: column; gap: 1rem;
    }

    .tam-row {
      display: flex; align-items: center; gap: 1.5rem;
    }

    .tam-bar-wrap {
      flex: 1; background: rgba(247,237,216,.06);
      border-radius: 100px; height: 14px; overflow: hidden;
    }
    .tam-bar {
      height: 100%; border-radius: 100px;
      animation: barGrow 1.5s ease both;
    }
    .tam-bar-1 { background: var(--gold); width: 100%; }
    .tam-bar-2 { background: var(--terra); width: 9.6%; animation-delay: .3s; }
    .tam-bar-3 { background: var(--sage); width: 0.048%; animation-delay: .6s; }

    @keyframes barGrow {
      from { transform: scaleX(0); transform-origin: left; }
      to   { transform: scaleX(1); }
    }

    .tam-info { min-width: 200px; }
    .tam-label { font-size: .75rem; text-transform: uppercase; letter-spacing: 1px; color: var(--muted); }
    .tam-value {
      font-family: 'Playfair Display', serif;
      font-size: 1.3rem; font-weight: 900; color: var(--cream);
    }

    .market-trends { display: flex; flex-direction: column; gap: 1.2rem; }

    .trend-item {
      display: flex; align-items: center; gap: 1.2rem;
      padding: 1.2rem;
      background: rgba(247,237,216,.04);
      border-radius: 12px;
      border: 1px solid rgba(247,237,216,.07);
    }

    .trend-num {
      font-family: 'Playfair Display', serif;
      font-size: 1.8rem; font-weight: 900;
      color: var(--gold); white-space: nowrap;
    }

    .trend-text {
      font-size: .85rem; color: var(--muted); line-height: 1.5;
    }
    .trend-text strong { color: var(--cream); display: block; font-weight: 600; }

    /* ── WAITLIST ── */
    #waitlist {
      background: linear-gradient(135deg, #0D1F3C, #0A1628);
      position: relative; overflow: hidden;
    }

    #waitlist::before {
      content: '';
      position: absolute;
      width: 700px; height: 700px;
      border-radius: 50%;
      background: radial-gradient(circle, rgba(212,168,67,.08) 0%, transparent 70%);
      top: 50%; left: 50%;
      transform: translate(-50%, -50%);
      pointer-events: none;
    }

    .waitlist-inner {
      max-width: 700px; margin: 0 auto;
      padding: 8rem 5%;
      text-align: center;
      position: relative; z-index: 1;
    }

    .waitlist-inner .section-title { max-width: 100%; margin: 0 auto; }

    .waitlist-tabs {
      display: flex; gap: .5rem;
      background: rgba(247,237,216,.06);
      border-radius: 12px;
      padding: .4rem;
      margin: 2.5rem auto 0;
      max-width: 380px;
    }

    .tab-btn {
      flex: 1; padding: .7rem 1rem;
      border-radius: 8px; border: none;
      font-family: 'DM Sans', sans-serif;
      font-size: .88rem; font-weight: 600;
      cursor: pointer; transition: all .2s;
      background: transparent; color: var(--muted);
    }
    .tab-btn.active {
      background: var(--gold);
      color: var(--night);
      box-shadow: 0 2px 12px rgba(212,168,67,.35);
    }

    .waitlist-form {
      display: flex; flex-direction: column; gap: 1rem;
      margin-top: 2rem;
    }

    .form-row { display: flex; gap: .75rem; }

    .form-input {
      flex: 1;
      background: rgba(247,237,216,.06);
      border: 1.5px solid rgba(247,237,216,.12);
      border-radius: 8px;
      padding: .85rem 1.2rem;
      font-family: 'DM Sans', sans-serif;
      font-size: .9rem; color: var(--cream);
      outline: none; transition: border-color .2s;
      width: 100%;
    }
    .form-input::placeholder { color: rgba(247,237,216,.35); }
    .form-input:focus { border-color: var(--gold); }

    .form-submit {
      padding: 1rem; font-size: 1rem;
      width: 100%; border-radius: 8px;
      background: var(--gold); color: var(--night);
      border: none; font-family: 'DM Sans', sans-serif;
      font-weight: 700; cursor: pointer;
      transition: all .2s;
      box-shadow: 0 4px 22px rgba(212,168,67,.35);
    }
    .form-submit:hover {
      background: var(--gold-lt);
      transform: translateY(-2px);
      box-shadow: 0 6px 32px rgba(212,168,67,.5);
    }

    .form-note {
      font-size: .78rem; color: var(--muted); margin-top: .5rem;
    }
    .form-note a { color: var(--gold); text-decoration: none; }

    .success-msg {
      display: none;
      background: rgba(58,125,107,.15);
      border: 1px solid rgba(58,125,107,.3);
      border-radius: 12px; padding: 1.5rem;
      color: #7ecbb8; font-size: .95rem; line-height: 1.6;
      margin-top: 1.5rem;
    }

    /* ── FOOTER ── */
    footer {
      background: #060E1C;
      padding: 3rem 5%;
      border-top: 1px solid rgba(247,237,216,.06);
    }

    .footer-inner {
     
