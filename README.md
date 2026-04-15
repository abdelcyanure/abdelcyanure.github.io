<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Librairie Mollat — La page que vous cherchez s'ouvre ici</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Gloock&family=Josefin+Sans:ital,wght@0,300;0,400;0,600;0,700;1,300&display=swap" rel="stylesheet">

  <style>
    /* ══════════════════════════════════════════
       DESIGN TOKENS
    ══════════════════════════════════════════ */
    :root {
      --burgundy:        oklch(40% 0.118 355);
      --burgundy-deep:   oklch(27% 0.098 355);
      --burgundy-mid:    oklch(52% 0.092 355);
      --ecru:            oklch(91.5% 0.024 76);
      --ecru-mid:        oklch(87%   0.030 74);
      --ecru-warm:       oklch(83%   0.038 72);
      --orange:          oklch(69%   0.188 52);
      --orange-dim:      oklch(62%   0.188 52);
      --coastal:         oklch(82%   0.064 196);
      --coastal-deep:    oklch(62%   0.092 196);
      --coastal-pale:    oklch(92%   0.036 197);

      --ink:             oklch(23%   0.054 358);
      --ink-mid:         oklch(46%   0.058 358);
      --ink-soft:        oklch(62%   0.042 75);
      --on-dark:         oklch(92%   0.022 76);
      --on-dark-muted:   oklch(72%   0.028 76);

      --font-serif:      'Gloock', Georgia, serif;
      --font-sans:       'Josefin Sans', system-ui, sans-serif;

      --s-2xs:  4px;
      --s-xs:   8px;
      --s-sm:   12px;
      --s-md:   16px;
      --s-lg:   24px;
      --s-xl:   32px;
      --s-2xl:  48px;
      --s-3xl:  64px;
      --s-4xl:  96px;

      --ease-out: cubic-bezier(0.25, 0.46, 0.45, 0.94);
    }

    /* ══════════════════════════════════════════
       RESET
    ══════════════════════════════════════════ */
    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
    html { scroll-behavior: smooth; }
    body {
      background: var(--ecru);
      color: var(--ink);
      font-family: var(--font-sans);
      font-weight: 400;
      line-height: 1.6;
      overflow-x: hidden;
    }
    ::selection { background: oklch(69% 0.188 52 / 0.22); }
    img, svg { display: block; }

    /* ══════════════════════════════════════════
       HEADER
    ══════════════════════════════════════════ */
    .site-header {
      position: fixed;
      inset: 0 0 auto;
      z-index: 200;
      height: 62px;
      background: var(--burgundy);
      display: grid;
      grid-template-columns: 1fr auto 1fr;
      align-items: center;
      padding: 0 var(--s-2xl);
    }

    .nav-main {
      display: flex;
      gap: var(--s-xl);
    }
    .nav-main a {
      font-size: 10px;
      font-weight: 600;
      letter-spacing: 0.18em;
      text-transform: uppercase;
      color: var(--on-dark-muted);
      text-decoration: none;
      transition: color 0.2s;
      position: relative;
      padding-bottom: 2px;
    }
    .nav-main a::after {
      content: '';
      position: absolute;
      bottom: -2px; left: 0; right: 0;
      height: 1px;
      background: var(--orange);
      transform: scaleX(0);
      transform-origin: left;
      transition: transform 0.3s var(--ease-out);
    }
    .nav-main a:hover { color: var(--on-dark); }
    .nav-main a:hover::after { transform: scaleX(1); }

    .header-logo {
      display: flex;
      flex-direction: column;
      align-items: center;
      gap: 1px;
      text-decoration: none;
      color: var(--on-dark);
    }
    .logo-mark {
      width: 36px;
      height: 24px;
      color: var(--ecru);
    }
    .logo-wordmark {
      font-family: var(--font-serif);
      font-size: 20px;
      letter-spacing: 0.1em;
      line-height: 1;
    }
    .logo-sub {
      font-size: 8px;
      font-weight: 600;
      letter-spacing: 0.28em;
      text-transform: uppercase;
      color: var(--on-dark-muted);
    }

    .header-actions {
      display: flex;
      gap: var(--s-xs);
      justify-content: flex-end;
      align-items: center;
    }
    .btn-ghost {
      width: 38px; height: 38px;
      border-radius: 50%;
      border: none;
      background: transparent;
      cursor: pointer;
      display: flex; align-items: center; justify-content: center;
      color: var(--on-dark-muted);
      transition: color 0.2s, background 0.2s;
    }
    .btn-ghost:hover {
      color: var(--on-dark);
      background: oklch(55% 0.09 355 / 0.35);
    }
    .btn-ghost svg { width: 18px; height: 18px; }

    .cart-wrap { position: relative; }
    .cart-badge {
      position: absolute;
      top: 5px; right: 5px;
      width: 14px; height: 14px;
      background: var(--orange);
      border-radius: 50%;
      font-size: 8px;
      font-weight: 700;
      color: #fff;
      display: flex; align-items: center; justify-content: center;
      transition: transform 0.18s;
    }

    /* Sound orb */
    .sound-btn { position: relative; }
    .sound-orb {
      position: absolute;
      inset: 5px;
      border-radius: 50%;
      border: 1px solid var(--orange);
      opacity: 0;
      pointer-events: none;
      transition: opacity 0.3s;
    }
    .sound-btn.is-on .sound-orb {
      opacity: 1;
      animation: orbPulse 2.2s ease-in-out infinite;
    }
    @keyframes orbPulse {
      0%, 100% { transform: scale(1);   opacity: 0.4; }
      50%       { transform: scale(1.5); opacity: 0.9; }
    }

    /* ══════════════════════════════════════════
       HERO
    ══════════════════════════════════════════ */
    .hero {
      position: relative;
      height: 100vh;
      min-height: 620px;
      display: flex;
      align-items: center;
      justify-content: center;
      overflow: hidden;
      padding-top: 62px;
    }

    /* Dark warm bookstore interior at golden hour */
    .hero-bg {
      position: absolute;
      inset: 0;
      background:
        radial-gradient(ellipse 70% 55% at 62% 38%, oklch(42% 0.14 60 / 0.55) 0%, transparent 60%),
        radial-gradient(ellipse 50% 70% at 20% 80%, oklch(30% 0.10 355 / 0.7) 0%, transparent 55%),
        oklch(19% 0.075 48);
    }

    /* Animated golden light shafts */
    .shaft {
      position: absolute;
      top: -10%;
      height: 130%;
      background: linear-gradient(to bottom,
        oklch(80% 0.16 66 / 0.13) 0%,
        oklch(78% 0.14 62 / 0.07) 40%,
        transparent 75%
      );
      transform-origin: top center;
      pointer-events: none;
    }
    .shaft-1 { left: 12%; width: 55px;  transform: rotate(7deg);  animation: drift 14s ease-in-out infinite; }
    .shaft-2 { left: 26%; width: 35px;  transform: rotate(11deg); animation: drift 17s ease-in-out infinite -4s; opacity: 0.6; }
    .shaft-3 { left: 48%; width: 90px;  transform: rotate(5deg);  animation: drift 20s ease-in-out infinite -8s; }
    .shaft-4 { left: 68%; width: 48px;  transform: rotate(9deg);  animation: drift 15s ease-in-out infinite -6s; opacity: 0.7; }
    .shaft-5 { left: 84%; width: 40px;  transform: rotate(6deg);  animation: drift 18s ease-in-out infinite -11s; opacity: 0.5; }

    @keyframes drift {
      0%, 100% { transform: rotate(var(--r, 7deg)) translateX(0px);   opacity: 0.7; }
      33%       { transform: rotate(var(--r, 7deg)) translateX(10px);  opacity: 1; }
      66%       { transform: rotate(var(--r, 7deg)) translateX(-6px);  opacity: 0.5; }
    }

    /* Book spine silhouettes at bottom */
    .hero-spines {
      position: absolute;
      bottom: 0; left: 0; right: 0;
      height: 150px;
      display: flex;
      align-items: flex-end;
      padding: 0 var(--s-xl);
      gap: 4px;
    }
    .h-spine {
      border-radius: 1px 1px 0 0;
      opacity: 0.35;
      flex-shrink: 0;
    }

    /* Gradient fade at bottom */
    .hero-fade {
      position: absolute;
      bottom: 0; left: 0; right: 0;
      height: 220px;
      background: linear-gradient(to top, var(--ecru) 0%, transparent 100%);
      pointer-events: none;
      z-index: 3;
    }

    /* Vignette */
    .hero-vignette {
      position: absolute;
      inset: 0;
      background: radial-gradient(ellipse at 50% 50%, transparent 38%, oklch(10% 0.04 355 / 0.65) 100%);
      pointer-events: none;
    }

    /* Hero content */
    .hero-inner {
      position: relative;
      z-index: 5;
      text-align: center;
      max-width: 820px;
      padding: 0 var(--s-xl);
    }
    .hero-kicker {
      font-size: 9px;
      font-weight: 600;
      letter-spacing: 0.32em;
      text-transform: uppercase;
      color: var(--orange);
      margin-bottom: var(--s-lg);
      display: flex;
      align-items: center;
      justify-content: center;
      gap: var(--s-md);
      animation: slideUp 0.8s var(--ease-out) 0.3s both;
    }
    .hero-kicker::before,
    .hero-kicker::after {
      content: '';
      width: 36px; height: 1px;
      background: var(--orange);
      opacity: 0.55;
    }
    .hero-heading {
      font-family: var(--font-serif);
      font-size: clamp(38px, 6.5vw, 76px);
      line-height: 1.1;
      letter-spacing: -0.01em;
      color: var(--on-dark);
      margin-bottom: var(--s-2xl);
      animation: slideUp 0.9s var(--ease-out) 0.5s both;
    }
    .hero-heading em {
      font-style: italic;
      color: oklch(84% 0.10 68);
    }
    .hero-cta {
      display: inline-flex;
      align-items: center;
      gap: var(--s-sm);
      background: var(--orange);
      color: #fff;
      font-size: 10px;
      font-weight: 700;
      letter-spacing: 0.2em;
      text-transform: uppercase;
      padding: 15px 34px;
      text-decoration: none;
      border-radius: 2px;
      transition: background 0.2s, transform 0.2s;
      animation: slideUp 0.8s var(--ease-out) 0.8s both;
    }
    .hero-cta:hover { background: var(--orange-dim); transform: translateY(-2px); }
    .hero-cta svg { width: 13px; height: 13px; transition: transform 0.2s; }
    .hero-cta:hover svg { transform: translateX(4px); }

    .hero-scroll {
      position: absolute;
      bottom: 38px; left: 50%;
      transform: translateX(-50%);
      z-index: 5;
      display: flex;
      flex-direction: column;
      align-items: center;
      gap: var(--s-xs);
      animation: bobDown 2s ease-in-out infinite;
    }
    .hero-scroll-line {
      width: 1px;
      height: 38px;
      background: linear-gradient(to bottom, transparent, oklch(91.5% 0.024 76 / 0.45));
    }
    .hero-scroll-dot {
      width: 4px; height: 4px;
      border-radius: 50%;
      background: oklch(91.5% 0.024 76 / 0.45);
    }

    @keyframes slideUp {
      from { opacity: 0; transform: translateY(22px); }
      to   { opacity: 1; transform: translateY(0); }
    }
    @keyframes bobDown {
      0%, 100% { transform: translateX(-50%) translateY(0);  opacity: 0.55; }
      50%       { transform: translateX(-50%) translateY(9px); opacity: 0.9; }
    }

    /* ══════════════════════════════════════════
       ORACLE SEARCH
    ══════════════════════════════════════════ */
    .oracle {
      padding: var(--s-4xl) var(--s-2xl);
      text-align: center;
      background: var(--ecru);
    }

    .section-eyebrow {
      font-size: 9px;
      font-weight: 700;
      letter-spacing: 0.3em;
      text-transform: uppercase;
      color: var(--ink-soft);
      margin-bottom: var(--s-sm);
    }
    .oracle-title {
      font-family: var(--font-serif);
      font-size: clamp(26px, 3.8vw, 42px);
      color: var(--ink);
      margin-bottom: var(--s-xs);
    }
    .oracle-sub {
      font-size: 13px;
      font-weight: 300;
      letter-spacing: 0.04em;
      color: var(--ink-mid);
      margin-bottom: var(--s-2xl);
      max-width: 520px;
      margin-left: auto;
      margin-right: auto;
    }

    .oracle-field {
      position: relative;
      max-width: 660px;
      margin: 0 auto var(--s-xl);
    }
    .oracle-input {
      width: 100%;
      padding: 18px 62px 18px 24px;
      background: #fff;
      border: 1.5px solid oklch(81% 0.038 76);
      border-radius: 3px;
      font-family: var(--font-serif);
      font-size: 16px;
      color: var(--ink);
      outline: none;
      transition: border-color 0.3s, box-shadow 0.3s;
    }
    .oracle-input::placeholder { color: var(--ink-soft); font-style: italic; }
    .oracle-input:focus {
      border-color: var(--burgundy);
      box-shadow: 0 0 0 3px oklch(40% 0.118 355 / 0.08);
    }
    .oracle-submit {
      position: absolute;
      right: 8px; top: 50%;
      transform: translateY(-50%);
      width: 44px; height: 44px;
      background: var(--burgundy);
      border: none;
      border-radius: 2px;
      display: flex; align-items: center; justify-content: center;
      cursor: pointer;
      transition: background 0.2s;
    }
    .oracle-submit:hover { background: var(--burgundy-deep); }
    .oracle-submit svg { width: 16px; height: 16px; color: var(--ecru); }

    .moods {
      display: flex;
      flex-wrap: wrap;
      gap: var(--s-xs);
      justify-content: center;
      max-width: 620px;
      margin: 0 auto;
    }
    .mood {
      display: inline-flex;
      align-items: center;
      gap: 5px;
      padding: 7px 17px;
      border-radius: 100px;
      border: 1px solid oklch(80% 0.038 76);
      background: transparent;
      font-family: var(--font-sans);
      font-size: 11px;
      font-weight: 400;
      letter-spacing: 0.07em;
      color: var(--ink-mid);
      cursor: pointer;
      transition: all 0.2s;
    }
    .mood:hover { border-color: var(--burgundy); color: var(--burgundy); }
    .mood.on {
      background: var(--burgundy);
      border-color: var(--burgundy);
      color: var(--ecru);
    }
    .mood-dot { font-size: 10px; }

    /* ══════════════════════════════════════════
       SHARED SECTION CHROME
    ══════════════════════════════════════════ */
    .sec-head {
      display: flex;
      align-items: baseline;
      justify-content: space-between;
      margin-bottom: var(--s-2xl);
    }
    .sec-title {
      font-family: var(--font-serif);
      font-size: clamp(28px, 4.2vw, 46px);
      color: var(--ink);
      line-height: 1.1;
    }
    .see-all {
      font-size: 10px;
      font-weight: 600;
      letter-spacing: 0.16em;
      text-transform: uppercase;
      color: var(--ink-mid);
      text-decoration: none;
      display: inline-flex;
      align-items: center;
      gap: 5px;
      white-space: nowrap;
      transition: color 0.2s;
    }
    .see-all svg { width: 12px; height: 12px; transition: transform 0.2s; }
    .see-all:hover { color: var(--burgundy); }
    .see-all:hover svg { transform: translateX(3px); }

    /* ══════════════════════════════════════════
       3-BOOK FEATURED GRID
    ══════════════════════════════════════════ */
    .featured {
      padding: var(--s-4xl) var(--s-2xl);
      max-width: 1300px;
      margin: 0 auto;
    }
    .books-trio {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      gap: var(--s-3xl);
    }
    @media (max-width: 840px) {
      .books-trio { grid-template-columns: 1fr; }
    }

    /* ── Book card ── */
    .book-card { display: flex; flex-direction: column; cursor: pointer; }

    .book-stage {
      position: relative;
      height: 290px;
      display: flex;
      align-items: flex-end;
      justify-content: center;
      margin-bottom: var(--s-xl);
    }

    /* 3-D book object */
    .book {
      position: relative;
      width: 168px;
      height: 242px;
      transform: perspective(580px) rotateY(-16deg);
      transform-origin: center center;
      transition:
        transform 0.5s var(--ease-out),
        filter   0.5s ease;
      filter: drop-shadow(6px 14px 22px rgba(0,0,0,0.18))
              drop-shadow(2px 4px 7px rgba(0,0,0,0.11));
    }
    .book:hover {
      transform: perspective(580px) rotateY(-5deg) translateY(-12px);
      filter: drop-shadow(10px 22px 30px rgba(0,0,0,0.23))
              drop-shadow(3px 6px 10px rgba(0,0,0,0.14));
    }
    .book:focus-visible {
      outline: 2px solid var(--orange);
      outline-offset: 6px;
    }

    .book-face {
      position: absolute;
      inset: 0;
      border-radius: 2px 5px 5px 2px;
      overflow: hidden;
      display: flex;
      flex-direction: column;
      padding: 22px 18px;
      justify-content: space-between;
    }
    /* Spine depth gradient */
    .book-face::before {
      content: '';
      position: absolute;
      left: 0; top: 0; bottom: 0;
      width: 32%;
      background: linear-gradient(to right,
        rgba(0,0,0,0.32) 0%,
        rgba(0,0,0,0.07) 55%,
        transparent 100%
      );
      pointer-events: none; z-index: 2;
    }
    /* Top-right highlight */
    .book-face::after {
      content: '';
      position: absolute;
      right: 0; top: 0;
      width: 45%; height: 45%;
      background: linear-gradient(135deg, rgba(255,255,255,0.09), transparent 55%);
      pointer-events: none; z-index: 2;
    }

    .book-pages {
      position: absolute;
      right: -7px; top: 4px; bottom: 4px;
      width: 8px;
      border-radius: 0 1px 1px 0;
      background: repeating-linear-gradient(
        to bottom,
        oklch(95% 0.01 80) 0px,
        oklch(88% 0.018 74) 1.5px,
        oklch(95% 0.01 80) 3px
      );
      z-index: -1;
    }

    .book-text {
      position: relative; z-index: 3;
      display: flex; flex-direction: column;
      height: 100%; justify-content: space-between;
    }
    .cover-tag {
      font-size: 8.5px;
      font-weight: 700;
      letter-spacing: 0.22em;
      text-transform: uppercase;
    }
    .cover-title {
      font-family: var(--font-serif);
      font-size: 20px;
      line-height: 1.18;
      flex: 1;
      display: flex;
      align-items: center;
      padding: 14px 0;
    }
    .cover-genre { font-size: 9.5px; letter-spacing: 0.1em; opacity: 0.75; }

    /* Book colour themes */
    .book-vuong .book-face {
      background:
        radial-gradient(ellipse at 72% 18%, oklch(50% 0.15 128 / 0.6), transparent 55%),
        oklch(24% 0.088 140);
    }
    .book-brocal .book-face {
      background:
        radial-gradient(ellipse at 28% 78%, oklch(36% 0.10 18 / 0.7), transparent 50%),
        oklch(18% 0.076 12);
    }
    .book-vuillard .book-face {
      background:
        radial-gradient(ellipse at 52% 28%, oklch(38% 0.072 242 / 0.55), transparent 58%),
        oklch(27% 0.068 248);
    }

    /* Cover ornamental SVGs */
    .cover-ornament {
      position: absolute;
      z-index: 2;
      pointer-events: none;
      opacity: 0.18;
    }

    /* Mollat seal */
    .m-seal {
      position: absolute;
      top: -14px; right: -14px;
      width: 54px; height: 54px;
      background: var(--orange);
      border-radius: 50%;
      display: flex; align-items: center; justify-content: center;
      z-index: 10;
      box-shadow: 0 3px 10px rgba(0,0,0,0.22);
      transition: transform 0.35s var(--ease-out);
    }
    .book-stage:hover .m-seal { transform: rotate(-10deg) scale(1.06); }
    .m-seal svg { width: 30px; height: 22px; color: #fff; }

    /* Book metadata */
    .book-meta { padding: 0 var(--s-xs); }
    .book-genre-tag {
      font-size: 9px;
      font-weight: 700;
      letter-spacing: 0.26em;
      text-transform: uppercase;
      color: var(--ink-soft);
      margin-bottom: var(--s-xs);
    }
    .book-title {
      font-family: var(--font-serif);
      font-size: 21px;
      line-height: 1.2;
      color: var(--ink);
      margin-bottom: 4px;
    }
    .book-author {
      font-size: 12px;
      font-weight: 300;
      letter-spacing: 0.06em;
      color: var(--ink-mid);
      margin-bottom: var(--s-md);
    }
    .book-foot {
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: var(--s-sm);
    }
    .price {
      font-size: 15px;
      font-weight: 700;
      color: var(--ink);
      letter-spacing: 0.03em;
    }
    .price small { font-size: 10px; font-weight: 400; color: var(--ink-soft); }

    .btn-cart {
      display: inline-flex;
      align-items: center;
      gap: 6px;
      background: var(--orange);
      color: #fff;
      border: none;
      padding: 10px 20px;
      font-family: var(--font-sans);
      font-size: 10px;
      font-weight: 700;
      letter-spacing: 0.16em;
      text-transform: uppercase;
      border-radius: 2px;
      cursor: pointer;
      transition: background 0.2s, transform 0.18s;
    }
    .btn-cart:hover { background: var(--orange-dim); transform: translateY(-1px); }
    .btn-cart svg { width: 11px; height: 11px; flex-shrink: 0; }

    /* ══════════════════════════════════════════
       RAYON VIRTUEL — horizontal scroll shelf
    ══════════════════════════════════════════ */
    .rayon {
      background: var(--ecru-mid);
      padding: var(--s-4xl) 0 0;
      overflow: hidden;
    }
    .rayon-head {
      padding: 0 var(--s-2xl) var(--s-2xl);
      display: flex;
      align-items: baseline;
      justify-content: space-between;
    }

    .shelf-track {
      display: flex;
      gap: 26px;
      padding: var(--s-lg) var(--s-2xl) var(--s-xl);
      overflow-x: auto;
      scroll-snap-type: x mandatory;
      scrollbar-width: none;
      cursor: grab;
      user-select: none;
    }
    .shelf-track::-webkit-scrollbar { display: none; }
    .shelf-track.dragging { cursor: grabbing; scroll-behavior: auto; }

    /* Individual spine-book on shelf */
    .s-book {
      flex-shrink: 0;
      width: 118px;
      height: 188px;
      position: relative;
      scroll-snap-align: start;
      transform: perspective(480px) rotateY(-13deg);
      transform-origin: center bottom;
      transition: transform 0.4s var(--ease-out), filter 0.4s ease;
      filter: drop-shadow(3px 8px 14px rgba(0,0,0,0.14));
      cursor: pointer;
      border-radius: 2px 4px 4px 2px;
    }
    .s-book:hover {
      transform: perspective(480px) rotateY(-3deg) translateY(-14px);
      filter: drop-shadow(5px 14px 22px rgba(0,0,0,0.22));
    }
    .s-book:focus-visible { outline: 2px solid var(--orange); }
    .s-book-face {
      position: absolute;
      inset: 0;
      border-radius: 2px 4px 4px 2px;
      overflow: hidden;
    }
    .s-book-face::before {
      content: '';
      position: absolute;
      left: 0; top: 0; bottom: 0;
      width: 30%;
      background: linear-gradient(to right, rgba(0,0,0,0.30), transparent);
      z-index: 2;
    }
    .s-book-pages {
      position: absolute;
      right: -5px; top: 3px; bottom: 3px;
      width: 6px;
      border-radius: 0 1px 1px 0;
      background: repeating-linear-gradient(
        to bottom,
        oklch(95% 0.01 80) 0px,
        oklch(88% 0.018 74) 1.5px,
        oklch(95% 0.01 80) 3px
      );
      z-index: -1;
    }
    .s-spine-label {
      position: absolute;
      left: 12px; top: 50%;
      transform: translateY(-50%) rotate(-90deg);
      transform-origin: center;
      white-space: nowrap;
      font-size: 8.5px;
      font-weight: 600;
      letter-spacing: 0.16em;
      text-transform: uppercase;
      z-index: 3;
      pointer-events: none;
    }

    /* Height variation */
    .s-book:nth-child(2n)   { height: 200px; }
    .s-book:nth-child(3n)   { height: 175px; }
    .s-book:nth-child(5n)   { height: 208px; }

    /* Colour palette for shelf books */
    .s-book:nth-child(1)  .s-book-face { background: oklch(36% 0.10 355); }
    .s-book:nth-child(2)  .s-book-face { background: oklch(55% 0.13 63); }
    .s-book:nth-child(3)  .s-book-face { background: oklch(29% 0.085 242); }
    .s-book:nth-child(4)  .s-book-face { background: oklch(48% 0.12 133); }
    .s-book:nth-child(5)  .s-book-face { background: oklch(40% 0.12 355); }
    .s-book:nth-child(6)  .s-book-face { background: oklch(62% 0.08 196); }
    .s-book:nth-child(7)  .s-book-face { background: oklch(50% 0.10 318); }
    .s-book:nth-child(8)  .s-book-face { background: oklch(40% 0.08 56); }
    .s-book:nth-child(9)  .s-book-face { background: oklch(63% 0.09 102); }
    .s-book:nth-child(10) .s-book-face { background: oklch(33% 0.07 204); }
    .s-book:nth-child(11) .s-book-face { background: oklch(52% 0.11 29); }
    .s-book:nth-child(12) .s-book-face { background: oklch(44% 0.09 162); }

    /* Wooden shelf plank */
    .shelf-plank {
      height: 18px;
      margin: 0 var(--s-2xl);
      background: linear-gradient(
        to bottom,
        oklch(63% 0.058 62) 0%,
        oklch(53% 0.068 58) 40%,
        oklch(46% 0.068 55) 100%
      );
      border-radius: 0 0 3px 3px;
      box-shadow: 0 5px 14px rgba(0,0,0,0.13);
      position: relative;
      overflow: hidden;
    }
    .shelf-plank::after {
      content: '';
      position: absolute;
      inset: 0;
      background: repeating-linear-gradient(
        90deg,
        transparent 0px,
        oklch(60% 0.06 62 / 0.28) 48px,
        transparent 95px,
        oklch(50% 0.07 57 / 0.18) 150px
      );
    }

    /* Shelf nav arrows */
    .shelf-nav {
      display: flex;
      gap: var(--s-xs);
      padding: var(--s-lg) var(--s-2xl) var(--s-2xl);
    }
    .shelf-arrow {
      width: 40px; height: 40px;
      border-radius: 50%;
      border: 1.5px solid oklch(74% 0.038 76);
      background: transparent;
      display: flex; align-items: center; justify-content: center;
      cursor: pointer;
      color: var(--ink-mid);
      transition: all 0.2s;
    }
    .shelf-arrow:hover {
      border-color: var(--burgundy);
      background: var(--burgundy);
      color: var(--ecru);
    }
    .shelf-arrow svg { width: 16px; height: 16px; }

    /* ══════════════════════════════════════════
       LIBRAIRE SELECTION
    ══════════════════════════════════════════ */
    .selection {
      padding: var(--s-4xl) var(--s-2xl);
      max-width: 1300px;
      margin: 0 auto;
    }
    .sel-grid {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: var(--s-xl);
    }
    @media (max-width: 720px) {
      .sel-grid { grid-template-columns: 1fr; }
    }

    .sel-card {
      background: var(--ecru-mid);
      padding: var(--s-2xl);
      border-radius: 4px;
      display: flex;
      gap: var(--s-xl);
      position: relative;
      overflow: hidden;
    }
    /* Coastal top accent using background, not border-left */
    .sel-card::before {
      content: '';
      position: absolute;
      top: 0; left: 0; right: 0;
      height: 3px;
      background: var(--coastal);
    }

    .sel-book-img {
      flex-shrink: 0;
      width: 96px; height: 140px;
      position: relative;
      filter: drop-shadow(3px 6px 12px rgba(0,0,0,0.15));
    }
    .sel-cover {
      position: absolute;
      inset: 0;
      border-radius: 2px 4px 4px 2px;
    }
    .sel-cover::before {
      content: '';
      position: absolute;
      left: 0; top: 0; bottom: 0;
      width: 26%;
      background: linear-gradient(to right, rgba(0,0,0,0.28), transparent);
      z-index: 1;
    }
    .sel-pages {
      position: absolute;
      right: -4px; top: 3px; bottom: 3px;
      width: 5px;
      border-radius: 0 1px 1px 0;
      background: repeating-linear-gradient(
        to bottom,
        oklch(95% 0.01 80) 0px,
        oklch(88% 0.018 74) 1.5px,
        oklch(95% 0.01 80) 3px
      );
      z-index: -1;
    }

    .sel-content { flex: 1; min-width: 0; }
    .sel-seal {
      position: absolute;
      top: var(--s-md); right: var(--s-md);
      width: 42px; height: 42px;
      flex-shrink: 0;
    }
    .libraire-note {
      font-family: var(--font-serif);
      font-style: italic;
      font-size: 13.5px;
      line-height: 1.75;
      color: var(--ink-mid);
      margin-bottom: var(--s-md);
      display: -webkit-box;
      -webkit-line-clamp: 3;
      -webkit-box-orient: vertical;
      overflow: hidden;
    }
    .libraire-sig {
      font-size: 9px;
      font-weight: 700;
      letter-spacing: 0.18em;
      text-transform: uppercase;
      color: var(--burgundy);
    }

    /* ══════════════════════════════════════════
       COASTAL INTERLUDE
    ══════════════════════════════════════════ */
    .coastal-band {
      background: var(--coastal-pale);
      padding: var(--s-3xl) var(--s-2xl);
      text-align: center;
    }
    .coastal-band p:first-child {
      font-family: var(--font-serif);
      font-size: clamp(18px, 2.8vw, 30px);
      color: var(--coastal-deep);
      margin-bottom: var(--s-xs);
    }
    .coastal-band p:last-child {
      font-size: 12px;
      font-weight: 300;
      letter-spacing: 0.09em;
      color: var(--coastal-deep);
      opacity: 0.75;
    }

    /* ══════════════════════════════════════════
       RENCONTRES & ÉVÉNEMENTS
    ══════════════════════════════════════════ */
    .rencontres {
      background: var(--burgundy);
      padding: var(--s-4xl) var(--s-2xl);
    }
    .rencontres-inner { max-width: 1300px; margin: 0 auto; }
    .rencontres .section-eyebrow { color: oklch(64% 0.055 358); }
    .rencontres .sec-title { color: var(--on-dark); }
    .rencontres .see-all { color: var(--on-dark-muted); }
    .rencontres .see-all:hover { color: var(--orange); }

    .events-row {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      gap: var(--s-xl);
    }
    @media (max-width: 840px) {
      .events-row { grid-template-columns: 1fr; }
    }

    .event-card {
      background: oklch(34% 0.096 358);
      border-radius: 4px;
      overflow: hidden;
      cursor: pointer;
      transition: transform 0.3s var(--ease-out);
    }
    .event-card:hover { transform: translateY(-5px); }

    .event-band {
      background: var(--orange);
      padding: var(--s-md) var(--s-lg);
      display: flex;
      align-items: baseline;
      gap: var(--s-xs);
    }
    .event-day {
      font-family: var(--font-serif);
      font-size: 30px;
      color: #fff;
      line-height: 1;
    }
    .event-month {
      font-size: 9px;
      font-weight: 700;
      letter-spacing: 0.22em;
      text-transform: uppercase;
      color: oklch(95% 0.03 65);
    }
    .event-body { padding: var(--s-lg); }
    .event-type {
      font-size: 8px;
      font-weight: 700;
      letter-spacing: 0.3em;
      text-transform: uppercase;
      color: var(--coastal);
      margin-bottom: var(--s-xs);
    }
    .event-title {
      font-family: var(--font-serif);
      font-size: 16px;
      color: var(--on-dark);
      line-height: 1.3;
      margin-bottom: 3px;
    }
    .event-author { font-size: 11px; color: var(--on-dark-muted); margin-bottom: var(--s-lg); }
    .event-link {
      display: inline-flex;
      align-items: center;
      gap: 5px;
      font-size: 9.5px;
      font-weight: 700;
      letter-spacing: 0.16em;
      text-transform: uppercase;
      color: var(--coastal);
      text-decoration: none;
      transition: gap 0.2s;
    }
    .event-link:hover { gap: 10px; }
    .event-link svg { width: 12px; height: 12px; }

    /* ══════════════════════════════════════════
       FOOTER
    ══════════════════════════════════════════ */
    .site-footer {
      background: var(--burgundy-deep);
      padding: var(--s-4xl) var(--s-2xl) var(--s-2xl);
    }
    .footer-inner { max-width: 1300px; margin: 0 auto; }

    .footer-top {
      display: grid;
      grid-template-columns: 2fr 1fr 1fr 1fr;
      gap: var(--s-3xl);
      padding-bottom: var(--s-3xl);
      margin-bottom: var(--s-xl);
      border-bottom: 1px solid oklch(36% 0.075 358);
    }
    @media (max-width: 840px) {
      .footer-top { grid-template-columns: 1fr 1fr; }
    }
    .footer-brand-name {
      font-family: var(--font-serif);
      font-size: 22px;
      color: var(--on-dark);
      display: block;
      margin-bottom: 3px;
    }
    .footer-brand-year {
      font-size: 8.5px;
      font-weight: 600;
      letter-spacing: 0.26em;
      text-transform: uppercase;
      color: var(--on-dark-muted);
      display: block;
      margin-bottom: var(--s-lg);
    }
    .footer-tagline {
      font-family: var(--font-serif);
      font-style: italic;
      font-size: 13px;
      line-height: 1.65;
      color: var(--on-dark-muted);
      max-width: 240px;
    }
    .footer-col h4 {
      font-size: 8.5px;
      font-weight: 700;
      letter-spacing: 0.26em;
      text-transform: uppercase;
      color: var(--on-dark);
      margin-bottom: var(--s-lg);
    }
    .footer-col ul { list-style: none; display: flex; flex-direction: column; gap: var(--s-sm); }
    .footer-col a {
      font-size: 12px;
      font-weight: 300;
      letter-spacing: 0.05em;
      color: var(--on-dark-muted);
      text-decoration: none;
      transition: color 0.2s;
    }
    .footer-col a:hover { color: var(--ecru); }

    .footer-bottom {
      display: flex;
      justify-content: space-between;
      align-items: center;
    }
    .footer-copy, .footer-address {
      font-size: 9.5px;
      font-weight: 300;
      letter-spacing: 0.1em;
      color: oklch(44% 0.055 358);
    }
    .footer-address { text-align: right; }

    /* ══════════════════════════════════════════
       SCROLL REVEAL
    ══════════════════════════════════════════ */
    .reveal {
      opacity: 0;
      transform: translateY(26px);
      transition: opacity 0.65s ease, transform 0.65s var(--ease-out);
    }
    .reveal.visible {
      opacity: 1;
      transform: translateY(0);
    }

    /* ══════════════════════════════════════════
       TOAST NOTIFICATION
    ══════════════════════════════════════════ */
    .toast {
      position: fixed;
      bottom: 28px; right: 28px;
      background: var(--burgundy);
      color: var(--ecru);
      padding: 14px 22px;
      border-radius: 3px;
      font-size: 12px;
      font-weight: 600;
      letter-spacing: 0.05em;
      z-index: 999;
      transform: translateY(80px);
      opacity: 0;
      transition: transform 0.4s var(--ease-out), opacity 0.4s ease;
      pointer-events: none;
      display: flex;
      align-items: center;
      gap: var(--s-sm);
      box-shadow: 0 8px 24px rgba(0,0,0,0.22);
    }
    .toast.show { transform: translateY(0); opacity: 1; }
    .toast svg { width: 14px; height: 14px; color: var(--orange); flex-shrink: 0; }

  </style>
</head>
<body>

  <!-- ════════════════════════════
       HEADER
  ════════════════════════════ -->
  <header class="site-header">

    <nav class="nav-main" aria-label="Navigation principale">
      <a href="#rayons">Rayons</a>
      <a href="#nouveautes">Nouveautés</a>
      <a href="#rencontres">Rencontres</a>
    </nav>

    <a class="header-logo" href="/" aria-label="Librairie Mollat — retour à l'accueil">
      <!-- M-on-horizon emblem -->
      <svg class="logo-mark" viewBox="0 0 42 28" fill="none" aria-hidden="true">
        <line x1="0" y1="22" x2="42" y2="22" stroke="currentColor" stroke-width="1.1" opacity="0.55"/>
        <text x="21" y="22" text-anchor="middle" dominant-baseline="alphabetic"
              font-family="Gloock,Georgia,serif" font-size="24" fill="currentColor">M</text>
      </svg>
      <span class="logo-wordmark">Mollat</span>
      <span class="logo-sub">Bordeaux — 1896</span>
    </a>

    <div class="header-actions">
      <button class="btn-ghost" aria-label="Rechercher"
              onclick="document.getElementById('oracle').scrollIntoView({behavior:'smooth'})">
        <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.6">
          <circle cx="11" cy="11" r="8"/>
          <path d="m21 21-4.35-4.35"/>
        </svg>
      </button>

      <button class="btn-ghost sound-btn" id="soundBtn"
              aria-label="Activer l'ambiance sonore"
              onclick="toggleSound(this)">
        <div class="sound-orb" aria-hidden="true"></div>
        <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.6">
          <path d="M9 18V5l12-2v13"/>
          <circle cx="6" cy="18" r="3"/>
          <circle cx="18" cy="16" r="3"/>
        </svg>
      </button>

      <div class="cart-wrap">
        <button class="btn-ghost" id="cartBtn" aria-label="Panier — 2 articles">
          <div class="cart-badge" id="cartCount">2</div>
          <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.6">
            <path d="M6 2 3 6v14a2 2 0 0 0 2 2h14a2 2 0 0 0 2-2V6l-3-4z"/>
            <line x1="3" y1="6" x2="21" y2="6"/>
            <path d="M16 10a4 4 0 0 1-8 0"/>
          </svg>
        </button>
      </div>
    </div>

  </header>


  <!-- ════════════════════════════
       HERO — Golden Hour
  ════════════════════════════ -->
  <section class="hero" aria-labelledby="hero-h1">
    <div class="hero-bg"        aria-hidden="true"></div>
    <div class="shaft shaft-1"  aria-hidden="true"></div>
    <div class="shaft shaft-2"  aria-hidden="true"></div>
    <div class="shaft shaft-3"  aria-hidden="true"></div>
    <div class="shaft shaft-4"  aria-hidden="true"></div>
    <div class="shaft shaft-5"  aria-hidden="true"></div>
    <div class="hero-vignette"  aria-hidden="true"></div>

    <!-- Book spine silhouettes (generated by JS) -->
    <div class="hero-spines" id="heroSpines" aria-hidden="true"></div>
    <div class="hero-fade"   aria-hidden="true"></div>

    <div class="hero-inner">
      <p class="hero-kicker">Librairie Mollat — Bordeaux</p>
      <h1 class="hero-heading" id="hero-h1">
        La page que vous cherchez<br>
        <em>s'ouvre ici.</em>
      </h1>
      <a href="#nouveautes" class="hero-cta">
        Entrer dans la librairie
        <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
          <path d="M5 12h14M12 5l7 7-7 7"/>
        </svg>
      </a>
    </div>

    <div class="hero-scroll" aria-hidden="true">
      <div class="hero-scroll-line"></div>
      <div class="hero-scroll-dot"></div>
    </div>
  </section>


  <!-- ════════════════════════════
       ORACLE SEARCH
  ════════════════════════════ -->
  <section class="oracle" id="oracle" aria-labelledby="oracle-h2">
    <p class="section-eyebrow">Recherche intuitive</p>
    <h2 class="oracle-title" id="oracle-h2">L'Oracle Mollat</h2>
    <p class="oracle-sub">Décrivez votre humeur, une émotion, un souvenir.<br>Nous trouvons le livre qui vous attend.</p>

    <div class="oracle-field">
      <input class="oracle-input" id="oracleInput" type="search"
             placeholder="Je cherche quelque chose de mélancolique et lumineux…"
             aria-label="Recherche par humeur ou sentiment"/>
      <button class="oracle-submit" aria-label="Lancer la recherche">
        <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
          <circle cx="11" cy="11" r="8"/>
          <path d="m21 21-4.35-4.35"/>
        </svg>
      </button>
    </div>

    <div class="moods" role="group" aria-label="Filtres par humeur">
      <button class="mood on"  onclick="toggleMood(this)"><span class="mood-dot">✦</span> Mélancolie douce</button>
      <button class="mood"     onclick="toggleMood(this)"><span class="mood-dot">✦</span> Aventure</button>
      <button class="mood"     onclick="toggleMood(this)"><span class="mood-dot">✦</span> Amour impossible</button>
      <button class="mood"     onclick="toggleMood(this)"><span class="mood-dot">✦</span> Mystère</button>
      <button class="mood"     onclick="toggleMood(this)"><span class="mood-dot">✦</span> Histoire &amp; Mémoire</button>
      <button class="mood"     onclick="toggleMood(this)"><span class="mood-dot">✦</span> Voyage intérieur</button>
      <button class="mood"     onclick="toggleMood(this)"><span class="mood-dot">✦</span> Humour &amp; Légèreté</button>
      <button class="mood"     onclick="toggleMood(this)"><span class="mood-dot">✦</span> Nature &amp; Silence</button>
    </div>
  </section>


  <!-- ════════════════════════════
       LES PÉPITES DU MOMENT
  ════════════════════════════ -->
  <section class="featured" id="nouveautes" aria-labelledby="feat-h2">
    <div class="sec-head">
      <div>
        <p class="section-eyebrow">Sélection du moment</p>
        <h2 class="sec-title" id="feat-h2">Les Pépites du Moment</h2>
      </div>
      <a href="#" class="see-all">
        Tout le catalogue
        <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
          <path d="M5 12h14M12 5l7 7-7 7"/>
        </svg>
      </a>
    </div>

    <div class="books-trio">

      <!-- ── Book 1 : L'Empereur de la Joie ── -->
      <article class="book-card reveal">
        <div class="book-stage">

          <div class="book book-vuong" tabindex="0"
               aria-label="L'Empereur de la Joie, Ocean Vuong">
            <!-- Decorative ring ornament on cover -->
            <svg class="cover-ornament" style="bottom:24px;right:14px;width:64px;height:76px"
                 viewBox="0 0 64 76" fill="none">
              <circle cx="32" cy="38" r="28" stroke="white" stroke-width="0.9" stroke-dasharray="5 3.5"/>
              <circle cx="32" cy="38" r="18" stroke="white" stroke-width="0.5"/>
              <line x1="32" y1="10" x2="32" y2="66" stroke="white" stroke-width="0.5"/>
              <line x1="4"  y1="38" x2="60" y2="38" stroke="white" stroke-width="0.5"/>
            </svg>
            <div class="book-face">
              <div class="book-text">
                <span class="cover-tag" style="color:oklch(84% 0.12 122)">Ocean Vuong</span>
                <p class="cover-title" style="color:oklch(95% 0.02 80)">L'Empereur<br>de la Joie</p>
                <span class="cover-genre" style="color:oklch(76% 0.09 122)">Roman</span>
              </div>
            </div>
            <div class="book-pages"></div>
          </div>

          <!-- Mollat seal — coup de cœur -->
          <div class="m-seal" aria-label="Coup de cœur libraire Mollat">
            <svg viewBox="0 0 42 28" fill="none" aria-hidden="true">
              <line x1="2" y1="22" x2="40" y2="22" stroke="white" stroke-width="1.4" opacity="0.85"/>
              <text x="21" y="22" text-anchor="middle" dominant-baseline="alphabetic"
                    font-family="Gloock,Georgia,serif" font-size="22" fill="white">M</text>
            </svg>
          </div>

        </div>
        <div class="book-meta">
          <p class="book-genre-tag">Roman contemporain</p>
          <h3 class="book-title">L'Empereur de la Joie</h3>
          <p class="book-author">Ocean Vuong</p>
          <div class="book-foot">
            <p class="price">22,00 € <small>broché</small></p>
            <button class="btn-cart" onclick="addToCart(this, 'L\'Empereur de la Joie')">
              <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                <path d="M6 2 3 6v14a2 2 0 0 0 2 2h14a2 2 0 0 0 2-2V6l-3-4z"/>
                <line x1="3" y1="6" x2="21" y2="6"/>
                <path d="M16 10a4 4 0 0 1-8 0"/>
              </svg>
              Ajouter
            </button>
          </div>
        </div>
      </article>

      <!-- ── Book 2 : La Langue des Vipères ── -->
      <article class="book-card reveal" style="transition-delay:0.12s">
        <div class="book-stage">

          <div class="book book-brocal" tabindex="0"
               aria-label="La Langue des Vipères, Juliette Brocal">
            <svg class="cover-ornament" style="top:18px;left:50%;transform:translateX(-50%);width:90px;height:60px"
                 viewBox="0 0 90 60" fill="none">
              <path d="M45 4 C28 18 10 26 45 34 C80 42 62 50 45 56"
                    stroke="white" stroke-width="1.1" fill="none"/>
              <path d="M30 4 C14 18 -4 26 30 34 C64 42 48 50 30 56"
                    stroke="white" stroke-width="0.5" fill="none" opacity="0.5"/>
            </svg>
            <div class="book-face">
              <div class="book-text">
                <span class="cover-tag" style="color:oklch(80% 0.07 28)">Juliette Brocal</span>
                <p class="cover-title" style="color:oklch(94% 0.015 40)">La Langue<br>des Vipères</p>
                <span class="cover-genre" style="color:oklch(70% 0.065 26)">Thriller littéraire</span>
              </div>
            </div>
            <div class="book-pages"></div>
          </div>

        </div>
        <div class="book-meta">
          <p class="book-genre-tag">Thriller littéraire</p>
          <h3 class="book-title">La Langue des Vipères</h3>
          <p class="book-author">Juliette Brocal</p>
          <div class="book-foot">
            <p class="price">20,00 € <small>broché</small></p>
            <button class="btn-cart" onclick="addToCart(this, 'La Langue des Vipères')">
              <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                <path d="M6 2 3 6v14a2 2 0 0 0 2 2h14a2 2 0 0 0 2-2V6l-3-4z"/>
                <line x1="3" y1="6" x2="21" y2="6"/>
                <path d="M16 10a4 4 0 0 1-8 0"/>
              </svg>
              Ajouter
            </button>
          </div>
        </div>
      </article>

      <!-- ── Book 3 : Les Orphelins ── -->
      <article class="book-card reveal" style="transition-delay:0.24s">
        <div class="book-stage">

          <div class="book book-vuillard" tabindex="0"
               aria-label="Les Orphelins, Éric Vuillard">
            <svg class="cover-ornament" style="top:50%;left:50%;transform:translate(-50%,-50%);width:80px;height:96px"
                 viewBox="0 0 80 96" fill="none">
              <rect x="8"  y="8"  width="64" height="80" rx="1" stroke="white" stroke-width="0.7" opacity="0.6"/>
              <rect x="16" y="16" width="48" height="64" rx="1" stroke="white" stroke-width="0.4" opacity="0.3"/>
              <line x1="8" y1="48" x2="72" y2="48" stroke="white" stroke-width="0.4" opacity="0.4"/>
              <line x1="40" y1="8" x2="40" y2="88" stroke="white" stroke-width="0.4" opacity="0.3"/>
            </svg>
            <div class="book-face">
              <div class="book-text">
                <span class="cover-tag" style="color:oklch(80% 0.05 248)">Éric Vuillard</span>
                <p class="cover-title" style="color:oklch(94% 0.018 76)">Les<br>Orphelins</p>
                <span class="cover-genre" style="color:oklch(72% 0.048 244)">Récit historique</span>
              </div>
            </div>
            <div class="book-pages"></div>
          </div>

          <div class="m-seal" aria-label="Coup de cœur libraire Mollat">
            <svg viewBox="0 0 42 28" fill="none" aria-hidden="true">
              <line x1="2" y1="22" x2="40" y2="22" stroke="white" stroke-width="1.4" opacity="0.85"/>
              <text x="21" y="22" text-anchor="middle" dominant-baseline="alphabetic"
                    font-family="Gloock,Georgia,serif" font-size="22" fill="white">M</text>
            </svg>
          </div>

        </div>
        <div class="book-meta">
          <p class="book-genre-tag">Récit historique</p>
          <h3 class="book-title">Les Orphelins</h3>
          <p class="book-author">Éric Vuillard</p>
          <div class="book-foot">
            <p class="price">18,50 € <small>broché</small></p>
            <button class="btn-cart" onclick="addToCart(this, 'Les Orphelins')">
              <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                <path d="M6 2 3 6v14a2 2 0 0 0 2 2h14a2 2 0 0 0 2-2V6l-3-4z"/>
                <line x1="3" y1="6" x2="21" y2="6"/>
                <path d="M16 10a4 4 0 0 1-8 0"/>
              </svg>
              Ajouter
            </button>
          </div>
        </div>
      </article>

    </div>
  </section>


  <!-- ════════════════════════════
       LE RAYON VIRTUEL
  ════════════════════════════ -->
  <section class="rayon" id="rayons" aria-labelledby="rayon-h2">
    <div class="rayon-head">
      <div>
        <p class="section-eyebrow">Navigation immersive</p>
        <h2 class="sec-title" id="rayon-h2">Déambuler dans les Rayons</h2>
      </div>
      <a href="#" class="see-all">
        Tous les rayons
        <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
          <path d="M5 12h14M12 5l7 7-7 7"/>
        </svg>
      </a>
    </div>

    <div class="shelf-track" id="shelfTrack"
         role="list" aria-label="Étagère de rayons — glisser pour explorer">

      <div class="s-book" role="listitem" tabindex="0" aria-label="Littérature française">
        <div class="s-book-face"></div>
        <div class="s-book-pages"></div>
        <span class="s-spine-label" style="color:oklch(90% 0.02 76)">Littérature française</span>
      </div>
      <div class="s-book" role="listitem" tabindex="0" aria-label="Poésie">
        <div class="s-book-face"></div>
        <div class="s-book-pages"></div>
        <span class="s-spine-label" style="color:oklch(90% 0.02 76)">Poésie</span>
      </div>
      <div class="s-book" role="listitem" tabindex="0" aria-label="Histoire">
        <div class="s-book-face"></div>
        <div class="s-book-pages"></div>
        <span class="s-spine-label" style="color:oklch(85% 0.05 200)">Histoire</span>
      </div>
      <div class="s-book" role="listitem" tabindex="0" aria-label="Nature &amp; Récits">
        <div class="s-book-face"></div>
        <div class="s-book-pages"></div>
        <span class="s-spine-label" style="color:oklch(88% 0.09 118)">Nature &amp; Récits</span>
      </div>
      <div class="s-book" role="listitem" tabindex="0" aria-label="Polars &amp; Noir">
        <div class="s-book-face"></div>
        <div class="s-book-pages"></div>
        <span class="s-spine-label" style="color:oklch(90% 0.02 76)">Polars &amp; Noir</span>
      </div>
      <div class="s-book" role="listitem" tabindex="0" aria-label="Voyages &amp; Mer">
        <div class="s-book-face"></div>
        <div class="s-book-pages"></div>
        <span class="s-spine-label" style="color:oklch(24% 0.06 196)">Voyages &amp; Mer</span>
      </div>
      <div class="s-book" role="listitem" tabindex="0" aria-label="Philosophie">
        <div class="s-book-face"></div>
        <div class="s-book-pages"></div>
        <span class="s-spine-label" style="color:oklch(90% 0.02 76)">Philosophie</span>
      </div>
      <div class="s-book" role="listitem" tabindex="0" aria-label="Cuisine &amp; Terroir">
        <div class="s-book-face"></div>
        <div class="s-book-pages"></div>
        <span class="s-spine-label" style="color:oklch(90% 0.02 76)">Cuisine &amp; Terroir</span>
      </div>
      <div class="s-book" role="listitem" tabindex="0" aria-label="Art &amp; Photographie">
        <div class="s-book-face"></div>
        <div class="s-book-pages"></div>
        <span class="s-spine-label" style="color:oklch(28% 0.07 102)">Art &amp; Photo</span>
      </div>
      <div class="s-book" role="listitem" tabindex="0" aria-label="Sciences">
        <div class="s-book-face"></div>
        <div class="s-book-pages"></div>
        <span class="s-spine-label" style="color:oklch(90% 0.02 76)">Sciences</span>
      </div>
      <div class="s-book" role="listitem" tabindex="0" aria-label="Jeunesse">
        <div class="s-book-face"></div>
        <div class="s-book-pages"></div>
        <span class="s-spine-label" style="color:oklch(90% 0.02 76)">Jeunesse</span>
      </div>
      <div class="s-book" role="listitem" tabindex="0" aria-label="Littérature étrangère">
        <div class="s-book-face"></div>
        <div class="s-book-pages"></div>
        <span class="s-spine-label" style="color:oklch(84% 0.07 157)">Littérature étrangère</span>
      </div>

    </div>

    <div class="shelf-plank" aria-hidden="true"></div>

    <div class="shelf-nav" aria-hidden="true">
      <button class="shelf-arrow" id="shelfPrev" aria-label="Défiler à gauche">
        <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
          <path d="M19 12H5M12 19l-7-7 7-7"/>
        </svg>
      </button>
      <button class="shelf-arrow" id="shelfNext" aria-label="Défiler à droite">
        <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
          <path d="M5 12h14M12 5l7 7-7 7"/>
        </svg>
      </button>
    </div>
  </section>


  <!-- ════════════════════════════
       LA SÉLECTION DES LIBRAIRES
  ════════════════════════════ -->
  <section class="selection" aria-labelledby="sel-h2">
    <div class="sec-head">
      <div>
        <p class="section-eyebrow">Cœur à cœur</p>
        <h2 class="sec-title" id="sel-h2">La Sélection des Libraires</h2>
      </div>
    </div>

    <div class="sel-grid">

      <article class="sel-card reveal">
        <div class="sel-book-img">
          <div class="sel-cover"
               style="background:linear-gradient(145deg,oklch(40% 0.09 72),oklch(29% 0.075 65))">
          </div>
          <div class="sel-pages"></div>
        </div>
        <div class="sel-content">
          <p class="book-genre-tag">Roman · 312 pages</p>
          <h3 class="book-title" style="font-size:18px;margin-bottom:3px">La Carte et le Territoire</h3>
          <p class="book-author">Michel Houellebecq</p>
          <p class="libraire-note">
            "Un livre qui parle de la création artistique avec une lucidité troublante.
             J'ai pensé à lui pendant des semaines après l'avoir refermé."
          </p>
          <p class="libraire-sig">— Sophie D., libraire rayon Romans</p>
        </div>
        <!-- Mollat seal inline -->
        <div class="sel-seal">
          <svg viewBox="0 0 44 44" fill="none" aria-label="Coup de cœur libraire">
            <circle cx="22" cy="22" r="20" fill="var(--orange)"
                    stroke="var(--ecru-warm)" stroke-width="1.3"/>
            <line x1="6" y1="28" x2="38" y2="28" stroke="white" stroke-width="1.2" opacity="0.85"/>
            <text x="22" y="28" text-anchor="middle" dominant-baseline="alphabetic"
                  font-family="Gloock,Georgia,serif" font-size="20" fill="white">M</text>
          </svg>
        </div>
      </article>

      <article class="sel-card reveal" style="transition-delay:0.14s">
        <div class="sel-book-img">
          <div class="sel-cover"
               style="background:linear-gradient(145deg,oklch(48% 0.088 200),oklch(34% 0.076 212))">
          </div>
          <div class="sel-pages"></div>
        </div>
        <div class="sel-content">
          <p class="book-genre-tag">Essai · 220 pages</p>
          <h3 class="book-title" style="font-size:18px;margin-bottom:3px">La Mer intérieure</h3>
          <p class="book-author">Donatien Grau</p>
          <p class="libraire-note">
            "Un essai rare sur le temps et la mémoire, écrit avec la précision d'un horloger
             et la sensibilité d'un poète. Absolument indispensable."
          </p>
          <p class="libraire-sig">— Marc T., libraire rayon Essais</p>
        </div>
      </article>

    </div>
  </section>


  <!-- ════════════════════════════
       COASTAL INTERLUDE
  ════════════════════════════ -->
  <div class="coastal-band" aria-hidden="true">
    <p>Voyages &amp; Mer · Le Bleu Côtier</p>
    <p>Une sélection pour les âmes qui cherchent l'horizon</p>
  </div>


  <!-- ════════════════════════════
       RENCONTRES & DÉDICACES
  ════════════════════════════ -->
  <section class="rencontres" id="rencontres" aria-labelledby="renc-h2">
    <div class="rencontres-inner">
      <div class="sec-head">
        <div>
          <p class="section-eyebrow">Agenda littéraire</p>
          <h2 class="sec-title" id="renc-h2">Rencontres &amp; Dédicaces</h2>
        </div>
        <a href="#" class="see-all">
          Tout l'agenda
          <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
            <path d="M5 12h14M12 5l7 7-7 7"/>
          </svg>
        </a>
      </div>

      <div class="events-row">

        <article class="event-card">
          <div class="event-band">
            <span class="event-day">22</span>
            <span class="event-month">Avril 2026</span>
          </div>
          <div class="event-body">
            <p class="event-type">Rencontre &amp; Signature</p>
            <h3 class="event-title">Ocean Vuong en conversation</h3>
            <p class="event-author">Autour de L'Empereur de la Joie</p>
            <a href="#" class="event-link">
              Réserver sa place
              <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                <path d="M5 12h14M12 5l7 7-7 7"/>
              </svg>
            </a>
          </div>
        </article>

        <article class="event-card">
          <div class="event-band">
            <span class="event-day">28</span>
            <span class="event-month">Avril 2026</span>
          </div>
          <div class="event-body">
            <p class="event-type">Lecture à voix haute</p>
            <h3 class="event-title">Nuit de la Poésie Bordelaise</h3>
            <p class="event-author">Collectif de poètes bordelais</p>
            <a href="#" class="event-link">
              En savoir plus
              <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                <path d="M5 12h14M12 5l7 7-7 7"/>
              </svg>
            </a>
          </div>
        </article>

        <article class="event-card">
          <div class="event-band">
            <span class="event-day">5</span>
            <span class="event-month">Mai 2026</span>
          </div>
          <div class="event-body">
            <p class="event-type">Dédicace</p>
            <h3 class="event-title">Éric Vuillard — Les Orphelins</h3>
            <p class="event-author">Dédicace en présence de l'auteur</p>
            <a href="#" class="event-link">
              Réserver
              <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                <path d="M5 12h14M12 5l7 7-7 7"/>
              </svg>
            </a>
          </div>
        </article>

      </div>
    </div>
  </section>


  <!-- ════════════════════════════
       FOOTER
  ════════════════════════════ -->
  <footer class="site-footer">
    <div class="footer-inner">
      <div class="footer-top">

        <div>
          <a href="/" style="text-decoration:none">
            <span class="footer-brand-name">Mollat</span>
            <span class="footer-brand-year">Bordeaux — 1896</span>
          </a>
          <p class="footer-tagline">
            "La librairie indépendante. Depuis 1896, au service des lecteurs de Bordeaux et du monde entier."
          </p>
        </div>

        <div class="footer-col">
          <h4>La Librairie</h4>
          <ul>
            <li><a href="#">Notre histoire</a></li>
            <li><a href="#">L'équipe</a></li>
            <li><a href="#">Nous trouver</a></li>
            <li><a href="#">Recrutement</a></li>
          </ul>
        </div>

        <div class="footer-col">
          <h4>Services</h4>
          <ul>
            <li><a href="#">Commande &amp; Livraison</a></li>
            <li><a href="#">Click &amp; Collect</a></li>
            <li><a href="#">Carte cadeau</a></li>
            <li><a href="#">Abonnement livre</a></li>
          </ul>
        </div>

        <div class="footer-col">
          <h4>Communauté</h4>
          <ul>
            <li><a href="#">Le blog Mollat</a></li>
            <li><a href="#">Newsletter</a></li>
            <li><a href="#">Instagram</a></li>
            <li><a href="#">Actualités</a></li>
          </ul>
        </div>

      </div>

      <div class="footer-bottom">
        <p class="footer-copy">© 2026 Librairie Mollat — Tous droits réservés</p>
        <p class="footer-address">15 rue Vital-Carles, 33000 Bordeaux</p>
      </div>
    </div>
  </footer>


  <!-- ════════════════════════════
       TOAST
  ════════════════════════════ -->
  <div class="toast" id="toast" role="status" aria-live="polite">
    <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" aria-hidden="true">
      <polyline points="20 6 9 17 4 12"/>
    </svg>
    <span id="toastMsg">Ajouté au panier</span>
  </div>


  <!-- ════════════════════════════
       SCRIPTS
  ════════════════════════════ -->
  <script>
    /* ── Hero spines ── */
    (function () {
      const wrap = document.getElementById('heroSpines');
      const palette = [
        'oklch(36% 0.10 355)','oklch(46% 0.09 58)','oklch(30% 0.08 242)',
        'oklch(40% 0.12 130)','oklch(50% 0.08 320)','oklch(38% 0.065 196)',
        'oklch(48% 0.10 28)','oklch(42% 0.09 102)','oklch(35% 0.07 162)',
        'oklch(54% 0.08 68)','oklch(32% 0.10 272)','oklch(60% 0.10 50)',
        'oklch(40% 0.08 202)','oklch(48% 0.12 14)','oklch(34% 0.09 148)',
        'oklch(52% 0.07 76)','oklch(38% 0.11 352)','oklch(44% 0.08 222)',
      ];
      const hs = [76,96,110,84,100,90,86,106,78,112,88,98,104,82,92,118,80,94];
      const ws = [18,22,15,26,20,16,24,19,21,17,23,18,20,22,16,28,19,21];
      for (let i = 0; i < 42; i++) {
        const d = document.createElement('div');
        d.className = 'h-spine';
        const ci = i % palette.length;
        d.style.cssText = `height:${hs[i % hs.length]}px;width:${ws[i % ws.length]}px;background:${palette[ci]};`;
        wrap.appendChild(d);
      }
    })();

    /* ── Oracle typewriter placeholder ── */
    (function () {
      const inp = document.getElementById('oracleInput');
      const phrases = [
        'Je cherche quelque chose de mélancolique et lumineux…',
        'Un roman qui se lit comme une nuit d\'été…',
        'Quelque chose qui parle de mémoire et de transmission…',
        'Un livre qui m\'emporte très loin, sans que je sache où…',
        'Une histoire qui donne envie de tout recommencer…',
        'Quelque chose de court mais qui dure longtemps…',
      ];
      let pi = 0, ci = 0, del = false, paused = false;

      function tick() {
        if (document.activeElement === inp) { setTimeout(tick, 200); return; }
        const text = phrases[pi];
        if (paused) { paused = false; setTimeout(() => { del = true; tick(); }, 2600); return; }
        if (!del) {
          inp.placeholder = text.slice(0, ++ci);
          if (ci === text.length) { paused = true; setTimeout(tick, 100); }
          else setTimeout(tick, 52);
        } else {
          inp.placeholder = text.slice(0, --ci);
          if (ci === 0) {
            del = false;
            pi = (pi + 1) % phrases.length;
            setTimeout(tick, 420);
          } else setTimeout(tick, 28);
        }
      }
      setTimeout(tick, 1400);
    })();

    /* ── Mood chips ── */
    function toggleMood(btn) { btn.classList.toggle('on'); }

    /* ── Sound toggle ── */
    function toggleSound(btn) {
      const on = btn.classList.toggle('is-on');
      btn.setAttribute('aria-label', on ? "Désactiver l'ambiance sonore" : "Activer l'ambiance sonore");
    }

    /* ── Shelf drag-to-scroll ── */
    (function () {
      const track = document.getElementById('shelfTrack');
      let down = false, sx = 0, sl = 0;

      track.addEventListener('mousedown', e => {
        down = true; sx = e.pageX - track.offsetLeft; sl = track.scrollLeft;
        track.classList.add('dragging');
      });
      document.addEventListener('mouseup', () => { down = false; track.classList.remove('dragging'); });
      document.addEventListener('mousemove', e => {
        if (!down) return;
        e.preventDefault();
        track.scrollLeft = sl - (e.pageX - track.offsetLeft - sx) * 1.7;
      });

      const STEP = 420;
      document.getElementById('shelfNext').onclick = () => track.scrollBy({ left: STEP, behavior: 'smooth' });
      document.getElementById('shelfPrev').onclick = () => track.scrollBy({ left: -STEP, behavior: 'smooth' });
    })();

    /* ── Cart ── */
    function addToCart(btn, title) {
      const orig = btn.innerHTML;
      btn.innerHTML = `
        <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"
             style="width:11px;height:11px"><polyline points="20 6 9 17 4 12"/></svg>
        Ajouté !`;
      btn.style.background = 'oklch(50% 0.14 148)';
      setTimeout(() => { btn.innerHTML = orig; btn.style.background = ''; }, 2200);

      /* badge bump */
      const badge = document.getElementById('cartCount');
      const n = (parseInt(badge.textContent) || 0) + 1;
      badge.textContent = n;
      badge.style.transform = 'scale(1.45)';
      setTimeout(() => badge.style.transform = '', 220);

      /* toast */
      const toast = document.getElementById('toast');
      document.getElementById('toastMsg').textContent = `"${title}" ajouté au panier`;
      toast.classList.add('show');
      clearTimeout(toast._t);
      toast._t = setTimeout(() => toast.classList.remove('show'), 3000);
    }

    /* ── Scroll reveal ── */
    (function () {
      const obs = new IntersectionObserver(entries => {
        entries.forEach(e => { if (e.isIntersecting) e.target.classList.add('visible'); });
      }, { threshold: 0.08, rootMargin: '0px 0px -30px 0px' });

      document.querySelectorAll('.reveal').forEach(el => obs.observe(el));
    })();

    /* ── Keyboard: shelf books ── */
    document.querySelectorAll('.s-book').forEach(b => {
      b.addEventListener('keydown', e => {
        if (e.key === 'Enter' || e.key === ' ') { e.preventDefault(); b.click(); }
      });
    });
  </script>

</body>
</html>
