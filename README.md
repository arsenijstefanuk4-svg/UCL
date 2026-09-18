
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>U.C.L — Untitled CIS league Arena</title>
    <link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@400;700;900&family=Teko:wght@600;700&display=swap" rel="stylesheet">
    <style>
        :root {
            --bg-dark: #030407;
            --bg-card: rgba(13, 16, 28, 0.75);
            --gold: #ffb703;
            --gold-glow: rgba(255, 183, 3, 0.5);
            --red: #ff2a4b;
            --red-glow: rgba(255, 42, 75, 0.5);
            --cyan: #00f2fe;
            --text-main: #f0f4f8;
            --text-sub: #94a3b8;
            --border-grid: rgba(255, 183, 3, 0.15);
        }

        /* Динамические темы подсветки */
        body.theme-gold   { --gold: #ffb703; --gold-glow: rgba(255, 183, 3, 0.5);  --border-grid: rgba(255, 183, 3, 0.15); }
        body.theme-cyan    { --gold: #00f2fe; --gold-glow: rgba(0, 242, 254, 0.5);  --border-grid: rgba(0, 242, 254, 0.15); }
        body.theme-red      { --gold: #ff2a4b; --gold-glow: rgba(255, 42, 75, 0.5);  --border-grid: rgba(255, 42, 75, 0.15); }
        body.theme-purple  { --gold: #b5179e; --gold-glow: rgba(181, 23, 158, 0.5); --border-grid: rgba(181, 23, 158, 0.15); }
        body.theme-green   { --gold: #00e676; --gold-glow: rgba(0, 230, 118, 0.5);  --border-grid: rgba(0, 230, 118, 0.15); }
        body.theme-orange  { --gold: #ff6d00; --gold-glow: rgba(255, 109, 0, 0.5);  --border-grid: rgba(255, 109, 0, 0.15); }
        body.theme-blue    { --gold: #2979ff; --gold-glow: rgba(41, 121, 255, 0.5); --border-grid: rgba(41, 121, 255, 0.15); }
        body.theme-pink    { --gold: #ff4dab; --gold-glow: rgba(255, 77, 171, 0.5); --border-grid: rgba(255, 77, 171, 0.15); }

        * { box-sizing: border-box; margin: 0; padding: 0; }
        html { scroll-behavior: smooth; }

        body {
            font-family: 'Montserrat', sans-serif;
            background-color: var(--bg-dark);
            color: var(--text-main);
            line-height: 1.5;
            overflow-x: hidden;
            position: relative;
            background-image:
                radial-gradient(circle at 50% 0%, var(--gold-glow) 0%, transparent 50%),
                radial-gradient(circle at 100% 100%, rgba(255, 42, 75, 0.1) 0%, transparent 40%),
                linear-gradient(to right, rgba(255, 255, 255, 0.02) 1px, transparent 1px),
                linear-gradient(to bottom, rgba(255, 255, 255, 0.02) 1px, transparent 1px);
            background-size: 100% 100%, 100% 100%, 40px 40px, 40px 40px;
            transition: background-image 0.4s ease;
        }

        /* Глобальное отключение анимаций */
        body.no-motion *,
        body.no-motion *::before,
        body.no-motion *::after {
            animation: none !important;
            transition: none !important;
            scroll-behavior: auto !important;
        }
        @media (prefers-reduced-motion: reduce) {
            body:not(.motion-forced) *,
            body:not(.motion-forced) *::before,
            body:not(.motion-forced) *::after {
                animation-duration: 0.001s !important;
                transition-duration: 0.001s !important;
            }
        }

        #progress-bar {
            position: fixed; top: 0; left: 0; height: 3px;
            background: linear-gradient(90deg, var(--red), var(--gold), var(--cyan));
            width: 0%; z-index: 10000;
            box-shadow: 0 0 12px var(--gold);
        }

        /* ===== Фоновая ринг-декорация в стиле бокса ===== */
        .ring-decor { position: fixed; inset: 0; z-index: 0; pointer-events: none; overflow: hidden; }

        .ring-ropes-top, .ring-ropes-bottom {
            position: fixed; left: 0; width: 100%; height: 18px; z-index: 1;
            display: flex; flex-direction: column; justify-content: space-between;
            opacity: 0.55;
        }
        .ring-ropes-top { top: 0; }
        .ring-ropes-bottom { bottom: 0; transform: rotate(180deg); }
        .rope-line { height: 3px; width: 100%; border-radius: 3px; }
        .rope-line.r1 { background: linear-gradient(90deg, var(--red), transparent, var(--red)); box-shadow: 0 0 8px var(--red-glow); }
        .rope-line.r2 { background: linear-gradient(90deg, var(--text-main), transparent, var(--text-main)); opacity: 0.35; }
        .rope-line.r3 { background: linear-gradient(90deg, var(--gold), transparent, var(--gold)); box-shadow: 0 0 8px var(--gold-glow); }

        .spotlight-sweep {
            position: fixed; top: -30%; left: -20%; width: 60%; height: 160%; z-index: 0;
            background: radial-gradient(ellipse at center, var(--gold-glow) 0%, transparent 65%);
            opacity: 0.18; filter: blur(10px);
            animation: sweepLight 16s ease-in-out infinite;
        }
        @keyframes sweepLight {
            0%, 100% { transform: translateX(0) rotate(-8deg); }
            50% { transform: translateX(160vw) rotate(8deg); }
        }

        .corner-glow { position: fixed; width: 260px; height: 260px; border-radius: 50%; z-index: 0; filter: blur(60px); opacity: 0.25; animation: cornerPulse 6s ease-in-out infinite; }
        .corner-glow.cg-tl { top: -80px; left: -80px; background: var(--red); }
        .corner-glow.cg-br { bottom: -80px; right: -80px; background: var(--gold); animation-delay: 3s; }
        @keyframes cornerPulse { 0%, 100% { opacity: 0.15; transform: scale(1); } 50% { opacity: 0.32; transform: scale(1.15); } }

        .floating-particles { position: fixed; inset: 0; z-index: 0; }
        .p-ember {
            position: absolute; bottom: -5%; font-size: 1.1rem; opacity: 0;
            animation: emberRise linear infinite; color: var(--gold); filter: drop-shadow(0 0 6px var(--gold-glow));
        }
        @keyframes emberRise {
            0% { transform: translateY(0) rotate(0deg); opacity: 0; }
            10% { opacity: 0.5; }
            90% { opacity: 0.35; }
            100% { transform: translateY(-105vh) rotate(360deg); opacity: 0; }
        }

        /* Панель настроек кастомизации */
        .customizer-panel {
            position: fixed; top: 15px; right: 15px; z-index: 9999;
        }
        .settings-toggle-btn {
            width: 42px; height: 42px; border-radius: 50%;
            background: rgba(13, 16, 28, 0.92); border: 1px solid var(--border-grid);
            color: var(--gold); font-size: 1.2rem; cursor: pointer;
            display: flex; align-items: center; justify-content: center;
            box-shadow: 0 4px 20px rgba(0,0,0,0.5), 0 0 14px var(--gold-glow);
            transition: 0.3s ease;
        }
        .settings-toggle-btn:hover { transform: rotate(90deg) scale(1.08); border-color: var(--gold); }

        .settings-dropdown {
            position: absolute; top: 52px; right: 0; min-width: 230px;
            background: rgba(13, 16, 28, 0.95); border: 1px solid var(--border-grid);
            padding: 16px; border-radius: 14px; backdrop-filter: blur(14px);
            box-shadow: 0 10px 30px rgba(0,0,0,0.6);
            opacity: 0; visibility: hidden; transform: translateY(-8px);
            transition: 0.25s ease;
        }
        .settings-dropdown.open { opacity: 1; visibility: visible; transform: translateY(0); }

        .settings-row { display: flex; flex-direction: column; gap: 8px; margin-bottom: 14px; }
        .settings-row:last-child { margin-bottom: 0; }
        .settings-row span.label { font-size: 0.72rem; font-weight: 800; text-transform: uppercase; color: var(--text-sub); letter-spacing: 1px; }

        .color-dots { display: flex; gap: 8px; flex-wrap: wrap; }
        .dot-btn {
            width: 22px; height: 22px; border-radius: 50%; border: 2px solid transparent;
            cursor: pointer; transition: 0.2s; position: relative;
        }
        .dot-btn:hover { transform: scale(1.2); }
        .dot-btn.active { border-color: #fff; transform: scale(1.12); box-shadow: 0 0 10px currentColor; }
        .dot-gold   { background: #ffb703; }
        .dot-cyan   { background: #00f2fe; }
        .dot-red    { background: #ff2a4b; }
        .dot-purple { background: #b5179e; }
        .dot-green  { background: #00e676; }
        .dot-orange { background: #ff6d00; }
        .dot-blue   { background: #2979ff; }
        .dot-pink   { background: #ff4dab; }

        .toggle-row { display: flex; align-items: center; justify-content: space-between; }
        .switch { position: relative; width: 44px; height: 24px; flex-shrink: 0; }
        .switch input { opacity: 0; width: 0; height: 0; }
        .slider-track {
            position: absolute; cursor: pointer; inset: 0; background: rgba(148,163,184,0.25);
            border-radius: 24px; transition: 0.3s;
        }
        .slider-track::before {
            content: ""; position: absolute; height: 18px; width: 18px; left: 3px; bottom: 3px;
            background: #fff; border-radius: 50%; transition: 0.3s;
        }
        .switch input:checked + .slider-track { background: var(--gold); box-shadow: 0 0 10px var(--gold-glow); }
        .switch input:checked + .slider-track::before { transform: translateX(20px); }

        /* 5-секундный прелоадер в стиле бокса */
        #loader {
            position: fixed; inset: 0; background: #020203;
            z-index: 99999; display: flex; flex-direction: column;
            align-items: center; justify-content: center;
            transition: opacity 0.5s ease, visibility 0.5s;
            overflow: hidden;
        }
        .loader-ropes { position: absolute; left: 0; width: 100%; height: 14px; opacity: 0.7; }
        .loader-ropes.top { top: 0; } .loader-ropes.bottom { bottom: 0; }
        .loader-ropes .rope-line { height: 3px; }

        .loader-bg-glow {
            position: absolute; width: 480px; height: 480px; border-radius: 50%;
            background: radial-gradient(circle, var(--gold-glow) 0%, transparent 70%);
            filter: blur(20px); animation: cornerPulse 3s ease-in-out infinite;
        }

        .loader-round {
            font-family: 'Teko', sans-serif; font-size: 1.1rem; letter-spacing: 4px;
            color: var(--red); text-transform: uppercase; margin-bottom: 6px;
            text-shadow: 0 0 10px var(--red-glow);
        }

        .punch-stage {
            position: relative; width: 220px; height: 160px;
            display: flex; align-items: center; justify-content: center;
        }
        .heavy-bag { font-size: 4.5rem; position: relative; z-index: 1; transform-origin: top center; animation: bagSwing 0.6s ease-in-out infinite alternate; }
        .glove-left, .glove-right { position: absolute; font-size: 3rem; z-index: 2; top: 35px; }
        .glove-left { left: 0; animation: punchLeft 0.6s ease-in-out infinite; }
        .glove-right { right: 0; transform: scaleX(-1); animation: punchRight 0.6s ease-in-out infinite 0.3s; }
        .impact-spark {
            position: absolute; width: 30px; height: 30px; border-radius: 50%; background: var(--gold);
            box-shadow: 0 0 25px var(--gold), 0 0 40px var(--red); opacity: 0; z-index: 3; animation: sparkFlash 0.6s infinite;
        }
        @keyframes bagSwing { 0% { transform: rotate(-8deg); } 100% { transform: rotate(8deg); } }
        @keyframes punchLeft { 0%, 100% { transform: translateX(0) rotate(-10deg); } 50% { transform: translateX(55px) rotate(15deg); } }
        @keyframes punchRight { 0%, 100% { transform: scaleX(-1) translateX(0) rotate(-10deg); } 50% { transform: scaleX(-1) translateX(55px) rotate(15deg); } }
        @keyframes sparkFlash { 0%, 40%, 60%, 100% { opacity: 0; transform: scale(0.5); } 50% { opacity: 1; transform: scale(1.4); } }

        .loader-bell { font-size: 1.6rem; margin-top: 6px; animation: bellIdle 1.4s ease-in-out infinite; }
        @keyframes bellIdle { 0%, 100% { transform: rotate(-6deg); } 50% { transform: rotate(6deg); } }
        .loader-bell.ding { animation: bellDing 0.5s ease; }
        @keyframes bellDing { 0%, 100% { transform: rotate(0); } 20% { transform: rotate(-25deg); } 40% { transform: rotate(20deg); } 60% { transform: rotate(-12deg); } 80% { transform: rotate(8deg); } }

        .loader-text {
            font-family: 'Teko', sans-serif; font-size: 2.2rem;
            letter-spacing: 3px; color: var(--gold); margin-top: 14px;
            text-shadow: 0 0 15px var(--gold-glow); text-align: center; padding: 0 20px;
        }
        .loader-fight {
            font-family: 'Teko', sans-serif; font-size: 4rem; letter-spacing: 6px; color: var(--red);
            text-shadow: 0 0 30px var(--red-glow); opacity: 0; transform: scale(0.6);
        }
        .loader-fight.show { animation: fightFlash 0.6s ease forwards; }
        @keyframes fightFlash { 0% { opacity: 0; transform: scale(0.4) rotate(-5deg); } 60% { opacity: 1; transform: scale(1.15) rotate(2deg); } 100% { opacity: 1; transform: scale(1) rotate(0); } }

        .loader-timer { font-size: 0.9rem; color: var(--text-sub); margin-top: 6px; font-weight: 700; letter-spacing: 1px; }

        /* Полноширинная зацикленная бегущая строка по центру */
        .marquee-wrapper {
            background: linear-gradient(90deg, #100003, var(--red), var(--gold), #100003);
            color: #ffffff; font-weight: 900; font-size: 0.95rem; text-transform: uppercase;
            letter-spacing: 2px; padding: 12px 0; overflow: hidden; white-space: nowrap;
            width: 100vw; position: relative; left: 50%; transform: translateX(-50%);
            display: flex; border-bottom: 1px solid var(--gold); box-shadow: 0 4px 20px rgba(0,0,0,0.9);
            z-index: 2;
        }
        .marquee-content { display: flex; flex-shrink: 0; white-space: nowrap; animation: marquee 14s linear infinite; text-shadow: 0 2px 4px rgba(0,0,0,0.8); }
        .marquee-item { padding-right: 50px; }
        @keyframes marquee { 0% { transform: translateX(0%); } 100% { transform: translateX(-50%); } }

        .status-container { display: flex; justify-content: center; margin-top: 25px; position: relative; z-index: 2; }
        .status-badge {
            display: flex; align-items: center; gap: 10px;
            background: rgba(15, 18, 32, 0.85); border: 1px solid var(--gold);
            padding: 8px 18px; border-radius: 50px; box-shadow: 0 0 20px var(--gold-glow); backdrop-filter: blur(12px);
        }
        .radar-dot { width: 10px; height: 10px; border-radius: 50%; animation: dotPulse 1.6s ease-in-out infinite; }
        @keyframes dotPulse { 0%, 100% { box-shadow: 0 0 6px currentColor; } 50% { box-shadow: 0 0 16px currentColor; } }
        .radar-dot.open { background: #00e676; color: #00e676; box-shadow: 0 0 12px #00e676; }
        .radar-dot.closed { background: var(--red); color: var(--red); box-shadow: 0 0 12px var(--red); }

        header { text-align: center; padding: 20px 15px; position: relative; z-index: 2; }
        .main-badge {
            display: inline-block; background: linear-gradient(45deg, var(--red), #ff5252); color: #fff;
            font-family: 'Teko', sans-serif; font-size: 1.3rem; font-weight: 700;
            padding: 2px 16px; border-radius: 4px; text-transform: uppercase; letter-spacing: 2px;
            box-shadow: 0 0 15px var(--red-glow); transform: skewX(-8deg); margin-bottom: 12px;
            animation: floatBadge 3s ease-in-out infinite;
        }
        @keyframes floatBadge { 0%, 100% { transform: skewX(-8deg) translateY(0); } 50% { transform: skewX(-8deg) translateY(-5px); } }

        h1 { font-family: 'Teko', sans-serif; font-size: 3.5rem; line-height: 0.95; text-transform: uppercase; letter-spacing: 2px; }
        h1 span { color: var(--gold); text-shadow: 0 0 20px var(--gold-glow); transition: 0.3s; animation: titleGlow 2.4s ease-in-out infinite; }
        @keyframes titleGlow { 0%, 100% { text-shadow: 0 0 20px var(--gold-glow); } 50% { text-shadow: 0 0 34px var(--gold-glow), 0 0 8px #fff; } }

        .search-wrapper { width: 100%; max-width: 650px; margin: 20px auto 0; padding: 0 10px; }
        .search-input {
            width: 100%; background: rgba(15, 18, 32, 0.9); border: 2px solid var(--border-grid);
            padding: 14px 20px; border-radius: 14px; color: #fff; font-size: 1rem; font-weight: 600;
            outline: none; transition: 0.3s ease; backdrop-filter: blur(10px);
        }
        .search-input:focus { border-color: var(--gold); box-shadow: 0 0 25px var(--gold-glow); }

        .nav-scroller { display: flex; gap: 10px; overflow-x: auto; padding: 20px 10px 10px; scrollbar-width: none; justify-content: center; flex-wrap: wrap; }
        .nav-scroller::-webkit-scrollbar { display: none; }
        .nav-link {
            background: rgba(20, 25, 45, 0.7); border: 1px solid var(--border-grid); color: var(--text-sub);
            padding: 8px 16px; border-radius: 8px; font-weight: 700; font-size: 0.8rem; text-decoration: none;
            text-transform: uppercase; transition: 0.2s ease;
        }
        .nav-link:hover { border-color: var(--gold); color: #fff; transform: translateY(-3px) scale(1.02); box-shadow: 0 6px 16px var(--gold-glow); }

        .container { width: 100%; max-width: 1250px; margin: 30px auto; padding: 0 15px; position: relative; z-index: 2; }
        section { margin-bottom: 45px; }

        .section-header { display: flex; align-items: center; gap: 12px; margin-bottom: 22px; border-bottom: 2px solid var(--border-grid); padding-bottom: 8px; transition: 0.3s; }
        .section-header h2 { font-family: 'Teko', sans-serif; font-size: 2.3rem; text-transform: uppercase; letter-spacing: 1px; }
        .header-line { height: 5px; width: 25px; background: var(--gold); box-shadow: 0 0 12px var(--gold-glow); border-radius: 2px; transition: 0.3s; animation: lineGrow 2.8s ease-in-out infinite; }
        @keyframes lineGrow { 0%, 100% { width: 25px; } 50% { width: 42px; } }

        .rules-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(320px, 1fr)); gap: 20px; }
        .rule-card {
            background: var(--bg-card); border: 1px solid var(--border-grid); border-radius: 16px; padding: 22px;
            backdrop-filter: blur(16px); display: flex; flex-direction: column; justify-content: space-between;
            transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1); cursor: pointer; position: relative;
            animation: cardAppear 0.5s ease backwards;
        }
        @keyframes cardAppear { from { opacity: 0; transform: translateY(16px); } to { opacity: 1; transform: translateY(0); } }
        .rule-card:hover { transform: translateY(-6px) scale(1.01); border-color: var(--gold); box-shadow: 0 10px 30px var(--gold-glow); }
        .rule-card.punch { animation: cardPunch 0.35s ease; }
        @keyframes cardPunch { 0% { transform: scale(1); } 35% { transform: scale(0.96) rotate(-0.6deg); } 60% { transform: scale(1.03) rotate(0.6deg); box-shadow: 0 0 30px var(--gold-glow); } 100% { transform: scale(1); } }
        .rule-card.danger-card { border-color: rgba(255, 42, 75, 0.3); }
        .rule-card.danger-card:hover { border-color: var(--red); box-shadow: 0 10px 30px rgba(255, 42, 75, 0.3); }

        .card-top { display: flex; justify-content: space-between; align-items: flex-start; margin-bottom: 14px; gap: 10px; }
        .card-title { font-size: 1.1rem; font-weight: 800; line-height: 1.3; }

        .badge-penalty { font-size: 0.7rem; font-weight: 900; padding: 4px 10px; border-radius: 6px; text-transform: uppercase; white-space: nowrap; }
        .badge-penalty.warn { background: rgba(255, 183, 3, 0.15); color: var(--gold); border: 1px solid var(--gold); }
        .badge-penalty.danger { background: rgba(255, 42, 75, 0.15); color: var(--red); border: 1px solid var(--red); animation: dangerPulse 1.6s ease-in-out infinite; }
        @keyframes dangerPulse { 0%, 100% { box-shadow: 0 0 0 rgba(255,42,75,0); } 50% { box-shadow: 0 0 10px var(--red-glow); } }
        .badge-penalty.info { background: rgba(0, 242, 254, 0.15); color: var(--cyan); border: 1px solid var(--cyan); }

        .card-desc { color: var(--text-sub); font-size: 0.92rem; }
        .card-desc strong { color: #fff; }

        .bans-flex { display: grid; grid-template-columns: repeat(auto-fill, minmax(140px, 1fr)); gap: 12px; }
        .ban-box {
            background: rgba(255, 42, 75, 0.06); border: 1px solid rgba(255, 42, 75, 0.25); border-radius: 10px;
            padding: 14px 8px; text-align: center; font-weight: 800; color: #ff6b81; font-size: 0.85rem; transition: 0.3s;
        }
        .ban-box:hover { background: rgba(255, 42, 75, 0.2); transform: translateY(-4px) scale(1.05); box-shadow: 0 5px 15px rgba(255,42,75,0.3); }

        #toast {
            position: fixed; bottom: 30px; left: 50%; transform: translateX(-50%) translateY(100px);
            background: var(--gold); color: #000; padding: 10px 24px; border-radius: 30px; font-weight: 800;
            font-size: 0.85rem; box-shadow: 0 0 20px var(--gold-glow); opacity: 0; transition: all 0.3s ease;
            z-index: 10000; pointer-events: none;
        }
        #toast.show { transform: translateX(-50%) translateY(0); opacity: 1; }

        #scrollTop {
            position: fixed; bottom: 25px; right: 25px; width: 48px; height: 48px; background: var(--gold);
            color: #000; border: none; border-radius: 50%; cursor: pointer; display: none; align-items: center;
            justify-content: center; font-weight: 900; font-size: 1.3rem; z-index: 999; box-shadow: 0 0 20px var(--gold-glow); transition: 0.2s;
        }
        #scrollTop:hover { transform: scale(1.15) rotate(15deg); }

        footer { text-align: center; padding: 30px 15px; border-top: 1px solid var(--border-grid); color: var(--text-sub); font-size: 0.85rem; position: relative; z-index: 2; }
        footer span { color: var(--gold); font-weight: 800; }

        @media (max-width: 480px) {
            h1 { font-size: 2.6rem; }
            .loader-text { font-size: 1.6rem; }
        }
    </style>
</head>
<body class="theme-gold">

    <!-- Фоновая декорация в стиле боксёрского ринга -->
    <div class="ring-decor" aria-hidden="true">
        <div class="ring-ropes-top"><div class="rope-line r1"></div><div class="rope-line r2"></div><div class="rope-line r3"></div></div>
        <div class="ring-ropes-bottom"><div class="rope-line r1"></div><div class="rope-line r2"></div><div class="rope-line r3"></div></div>
        <div class="spotlight-sweep"></div>
        <div class="corner-glow cg-tl"></div>
        <div class="corner-glow cg-br"></div>
        <div class="floating-particles" id="particles"></div>
    </div>

    <!-- Панель настроек -->
    <div class="customizer-panel">
        <button class="settings-toggle-btn" id="settingsBtn" onclick="toggleSettings()" title="Настройки">⚙</button>
        <div class="settings-dropdown" id="settingsDropdown">
            <div class="settings-row">
                <span class="label">Подсветка</span>
                <div class="color-dots">
                    <div class="dot-btn dot-gold active" onclick="setTheme('theme-gold', this)" title="Золотой неон"></div>
                    <div class="dot-btn dot-cyan" onclick="setTheme('theme-cyan', this)" title="Киберпанк синий"></div>
                    <div class="dot-btn dot-red" onclick="setTheme('theme-red', this)" title="Кровавый красный"></div>
                    <div class="dot-btn dot-purple" onclick="setTheme('theme-purple', this)" title="Неоновый фиолетовый"></div>
                    <div class="dot-btn dot-green" onclick="setTheme('theme-green', this)" title="Ринг зелёный"></div>
                    <div class="dot-btn dot-orange" onclick="setTheme('theme-orange', this)" title="Нокаут оранжевый"></div>
                    <div class="dot-btn dot-blue" onclick="setTheme('theme-blue', this)" title="Ледяной синий"></div>
                    <div class="dot-btn dot-pink" onclick="setTheme('theme-pink', this)" title="Неоновый розовый"></div>
                </div>
            </div>
            <div class="settings-row toggle-row">
                <span class="label">Анимации</span>
                <label class="switch">
                    <input type="checkbox" id="motionToggle" checked onchange="toggleMotion(this.checked)">
                    <span class="slider-track"></span>
                </label>
            </div>
        </div>
    </div>

    <div id="loader">
        <div class="loader-ropes top"><div class="rope-line r1"></div><div class="rope-line r3"></div></div>
        <div class="loader-ropes bottom"><div class="rope-line r1"></div><div class="rope-line r3"></div></div>
        <div class="loader-bg-glow"></div>
        <div class="loader-round">Выход на ринг</div>
        <div class="punch-stage">
            <div class="glove-left">🥊</div>
            <div class="heavy-bag">🥊</div>
            <div class="glove-right">🥊</div>
            <div class="impact-spark"></div>
        </div>
        <div class="loader-bell" id="loaderBell">🔔</div>
        <div class="loader-text" id="loaderText">ПОДГОТОВКА АРЕНЫ U.C.L...</div>
        <div class="loader-fight" id="loaderFight">БОЙ!</div>
        <div class="loader-timer" id="loadTimer">Загрузка: 5 сек</div>
    </div>

    <div id="progress-bar"></div>
    <div id="toast">Правило скопировано в буфер!</div>

    <div class="marquee-wrapper">
        <div class="marquee-content">
            <span class="marquee-item">⚡ ПРАВИЛА БОЁВ U.C.L • ОФИЦИАЛЬНЫЙ РЕГЛАМЕНТ • СОБЛЮДАЙТЕ ПРАВИЛА ЛИГИ • ⚡</span>
            <span class="marquee-item">⚡ ПРАВИЛА БОЁВ U.C.L • ОФИЦИАЛЬНЫЙ РЕГЛАМЕНТ • СОБЛЮДАЙТЕ ПРАВИЛА ЛИГИ • ⚡</span>
        </div>
    </div>

    <header>
        <div class="status-container">
            <div class="status-badge">
                <div id="radarDot" class="radar-dot"></div>
                <span id="radarText" style="font-weight:800; font-size:0.8rem; text-transform:uppercase;">Проверка арены...</span>
            </div>
        </div>

        <div style="margin-top:20px;">
            <div class="main-badge">Untitled CIS league</div>
            <h1>Правила боёв <span>U.C.L</span></h1>
        </div>

        <div class="search-wrapper">
            <input type="text" id="searchInput" class="search-input" placeholder="⚡ Поиск правил (пассив, демпси, багоюз, бекдеш...)" oninput="searchRules()">
        </div>

        <div class="nav-scroller">
            <a href="#pd" class="nav-link">1. Пассив</a>
            <a href="#bugs" class="nav-link">2. Багоюз</a>
            <a href="#combos" class="nav-link">3. Медленные комбо М1</a>
            <a href="#skating" class="nav-link">4. С-кейтинг и бекдеши</a>
            <a href="#dd" class="nav-link">5. ДД (дабл деш)</a>
            <a href="#audio" class="nav-link">6. Звуки / Изображения</a>
            <a href="#title" class="nav-link">7. Титульные бои</a>
            <a href="#combat" class="nav-link">8. Регламент боев</a>
            <a href="#bans" class="nav-link">9. Бан стили</a>
        </div>
    </header>

    <main class="container">

        <section id="pd">
            <div class="section-header">
                <div class="header-line"></div>
                <h2>1. Пассив</h2>
            </div>
            <div class="rules-grid">
                <div class="rule-card searchable" onclick="copyCardText(this)">
                    <div class="card-top">
                        <div class="card-title">ПД Фишинг</div>
                        <span class="badge-penalty info">Определение</span>
                    </div>
                    <div class="card-desc">
                        ПД Фишинг— это когда игрок намеренно перестает бить/взаимодействовать, чтобы сделать идеальное уклонение.<br><br>
                        Если вас ловят на стагеринге или вы ничего не можете сделать кроме уклона то можете выждать момент и сделать два уклона если по вам делают спамящие комбо (особенно касается медленных стилей).
                    </div>
                </div>

                <div class="rule-card searchable" onclick="copyCardText(this)">
                    <div class="card-top">
                        <div class="card-title">Таймеры и Ограничения</div>
                        <span class="badge-penalty warn">ТКО за 2 фола</span>
                    </div>
                    <div class="card-desc">
                        ТКО даётся за 2 фола.<br><br>
                        Ждать удара можно максимум <strong>3 секунды</strong>, вы можете выйти за рамки времени и будет предупреждение, но при злоупотреблении — фол.
                    </div>
                </div>

                <div class="rule-card danger-card searchable" onclick="copyCardText(this)">
                    <div class="card-top">
                        <div class="card-title">Сброс таймера, Эмоции и Стамина</div>
                        <span class="badge-penalty danger">Важно</span>
                    </div>
                    <div class="card-desc">
                        Попытка удара и получение контрудара сбрасывают таймер порога ПД фиша (таймер 3 секунды). Также атака и способности, возвращающие бойцов в нейтральное положение, сбрасывают таймер.<br><br>
                        Использование эмоций приравнивается к бездействию (кроме начала раунда).<br><br>
                        Пдфишить можно, когда у бойца <strong>полностью</strong> закончилась стамина.
                    </div>
                </div>
            </div>
        </section>

        <section id="bugs">
            <div class="section-header">
                <div class="header-line"></div>
                <h2>2. Багоюз</h2>
            </div>
            <div class="rules-grid">
                <div class="rule-card danger-card searchable" onclick="copyCardText(this)">
                    <div class="card-top">
                        <div class="card-title">Парирование ульты</div>
                        <span class="badge-penalty danger">Вылет из реальной жизни</span>
                    </div>
                    <div class="card-desc">
                        Когда в вас летит ульта и вас должны пробить, а вы в тайминг прожимаете блок и ульта сжирается (при намеренном использовании будет вылет из реальной жизни).
                    </div>
                </div>

                <div class="rule-card searchable" onclick="copyCardText(this)">
                    <div class="card-top">
                        <div class="card-title">Нелегальный стаггеринг</div>
                        <span class="badge-penalty warn">Предупреждение ➔ Фол</span>
                    </div>
                    <div class="card-desc">
                        Это когда удар M1 все еще регистрируется в серии, но задерживается и становится неуклоняемым, притягивая игрока обратно вопреки уклонению и кадрам — нарушение.<br><br>
                        Первое нарушение влечет устное предупреждение, последующие — фол.
                    </div>
                </div>

                <div class="rule-card searchable" onclick="copyCardText(this)">
                    <div class="card-top">
                        <div class="card-title">Разрешенный стаггеринг</div>
                        <span class="badge-penalty info">Разрешено</span>
                    </div>
                    <div class="card-desc">
                        Стаггеринг (тыкать М1 при попытке перебить атаку противника) с целью смены темпа или миксапов разрешен.
                    </div>
                </div>
            </div>
        </section>

        <section id="combos">
            <div class="section-header">
                <div class="header-line"></div>
                <h2>3. Медленные комбо М1 (слоу клики)</h2>
            </div>
            <div class="rules-grid">
                <div class="rule-card searchable" onclick="copyCardText(this)">
                    <div class="card-top">
                        <div class="card-title">Правила применения</div>
                        <span class="badge-penalty warn">Фол при нарушении</span>
                    </div>
                    <div class="card-desc">
                        Медленные удары M1 разрешены только после того, как игрок попал под ультимейт. Их нельзя использовать после способностей (Focus, Stampede и т. д.). Игрокам разрешено использовать медленные M1 только для <strong>ОДНОЙ СЕРИИ УДАРОВ</strong>, большее количество приведет к фолу.
                    </div>
                </div>

                <div class="rule-card searchable" onclick="copyCardText(this)">
                    <div class="card-top">
                        <div class="card-title">Исключения для стилей</div>
                        <span class="badge-penalty info">Исключения</span>
                    </div>
                    <div class="card-desc">
                        <strong>ИСКЛЮЧЕНИЕ:</strong> нельзя использовать стиль крюк (corkscrew) слоу клики после ультимейта.<br><br>
                        После ультимейта айрон фиста можно делать <strong>ДВА КОМБО СЛОУ КЛИКА</strong>.
                    </div>
                </div>
            </div>
        </section>

        <section id="skating">
            <div class="section-header">
                <div class="header-line"></div>
                <h2>4. С-кейтинг и бекдеши</h2>
            </div>
            <div class="rules-grid">
                <div class="rule-card searchable" onclick="copyCardText(this)">
                    <div class="card-top">
                        <div class="card-title">С-кейтинг</div>
                        <span class="badge-penalty warn">Фол</span>
                    </div>
                    <div class="card-desc">
                        С-кейтинг — уход назад от противника зажатием кнопки S (направление джойстика назад). Можно использовать после попадания удара или комбо по сопернику. Если вы идете назад и ничего не делаете, пропуская два действия противника — фол. Аналогично с бекдешом.
                    </div>
                </div>

                <div class="rule-card searchable" onclick="copyCardText(this)">
                    <div class="card-top">
                        <div class="card-title">Обоюдный кайтанг</div>
                        <span class="badge-penalty warn">Фол обоим</span>
                    </div>
                    <div class="card-desc">
                        Если оба игрока намеренно держатся на расстоянии, включается 3-секундный счёт после 3-секундного счёта порога ПД. Если никто не приближается — фол обоим.
                    </div>
                </div>

                <div class="rule-card searchable" onclick="copyCardText(this)">
                    <div class="card-top">
                        <div class="card-title">Против Демпси и Шотгана</div>
                        <span class="badge-penalty info">Особые условия</span>
                    </div>
                    <div class="card-desc">
                        Против демпси можно фишить, но нельзя уходить назад (С-кейтить).<br><br>
                        Против шотгана можно использовать бекдеш на способность, если вы до этого сделали бекдеш.
                    </div>
                </div>
            </div>
        </section>

        <section id="dd">
            <div class="section-header">
                <div class="header-line"></div>
                <h2>5. ДД (дабл деш)</h2>
            </div>
            <div class="rules-grid">
                <div class="rule-card searchable" onclick="copyCardText(this)">
                    <div class="card-top">
                        <div class="card-title">Правила дешей</div>
                        <span class="badge-penalty info">Свободно / Трипл деш</span>
                    </div>
                    <div class="card-desc">
                        Используйте как хотите.<br><br>
                        Трипл деш карается <strong>1 фолом</strong>.
                    </div>
                </div>
            </div>
        </section>

        <section id="audio">
            <div class="section-header">
                <div class="header-line"></div>
                <h2>6. Пользовательские звуки / изображения</h2>
            </div>
            <div class="rules-grid">
                <div class="rule-card searchable" onclick="copyCardText(this)">
                    <div class="card-top">
                        <div class="card-title">Общие правила</div>
                        <span class="badge-penalty warn">Предупреждение</span>
                    </div>
                    <div class="card-desc">
                        Использование неприятных или раздражающих звуковых эффектов и изображений может отвлекать игроков во время игры; несоблюдение приведет к предупреждению.
                    </div>
                </div>

                <div class="rule-card searchable" onclick="copyCardText(this)">
                    <div class="card-top">
                        <div class="card-title">Звуки ПД (Идеальное уклонение)</div>
                        <span class="badge-penalty info">На усмотрение</span>
                    </div>
                    <div class="card-desc">
                        Пользовательские звуковые эффекты идеального уклонения (ПД) остаются на усмотрение игроков, но может быть запрошено их удаление во избежание отвлечения внимания.
                    </div>
                </div>

                <div class="rule-card danger-card searchable" onclick="copyCardText(this)">
                    <div class="card-top">
                        <div class="card-title">Контрудары и Ульта</div>
                        <span class="badge-penalty danger">Строго запрещено / Разрешено</span>
                    </div>
                    <div class="card-desc">
                        Пользовательские звуковые эффекты контрударов (каунтер), а также изображения строго запрещены и должны быть удалены для официальных матчей.<br><br>
                        Пользовательские звуковые эффекты и изображения ультимативных способностей (ульта) разрешены.
                    </div>
                </div>
            </div>
        </section>

        <section id="title">
            <div class="section-header">
                <div class="header-line"></div>
                <h2>7. Титульные бои</h2>
            </div>
            <div class="rules-grid">
                <div class="rule-card searchable" onclick="copyCardText(this)">
                    <div class="card-top">
                        <div class="card-title">Формат боев и оценивание</div>
                        <span class="badge-penalty info">Формат bo3</span>
                    </div>
                    <div class="card-desc">
                        Проводятся в формате bo3 (3 боя). Игрок может сменить стиль только после поражения; победитель должен сохранять текущий стиль до проигрыша. Правила такие же, как в обычных боях.<br><br>
                        За боем будет наблюдать <strong>один рефери высшей категории</strong>, который будет следить за поединком.<br><br>
                        Каждый бой (не раунд) счётчик фолов будет аннулироваться. В зависимости от количества фолов рефери может поменять итог боя.
                    </div>
                </div>

                <div class="rule-card searchable" onclick="copyCardText(this)">
                    <div class="card-top">
                        <div class="card-title">Защита титулов</div>
                        <span class="badge-penalty info">Сроки защиты</span>
                    </div>
                    <div class="card-desc">
                        • <strong>ЗАЩИТА ТИТУЛА ЧЕМПИОНА В UNF:</strong> КАЖДАЯ НЕДЕЛЯ<br><br>
                        • <strong>ЗАЩИТА ТИТУЛА ЧЕМПИОНА UNC:</strong> КАЖДЫЕ 2 НЕДЕЛИ<br><br>
                        • <strong>ЗАЩИТА ТИТУЛА ЧЕМПИОНА UCL:</strong> КАЖДЫЕ 2.5 НЕДЕЛИ
                    </div>
                </div>
            </div>
        </section>

        <section id="combat">
            <div class="section-header">
                <div class="header-line"></div>
                <h2>8. Правила проведения боев U.C.L</h2>
            </div>
            <div class="rules-grid">
                <div class="rule-card searchable" onclick="copyCardText(this)">
                    <div class="card-top">
                        <div class="card-title">Проблемы со связью и вылеты</div>
                        <span class="badge-penalty warn">5 минут дедлайн</span>
                    </div>
                    <div class="card-desc">
                        Если прямо посреди матча у вас оборвалось соединение или вылетела игра, включается счетчик: у вас есть ровно 5 минут на немедленное возвращение. Если не уложитесь — поединок аннулируется либо присуждается технический нокаут (ТКО) по решению рефери.
                    </div>
                </div>

                <div class="rule-card searchable" onclick="copyCardText(this)">
                    <div class="card-top">
                        <div class="card-title">Неоспоримый авторитет рефери</div>
                        <span class="badge-penalty info">Закон на ринге</span>
                    </div>
                    <div class="card-desc">
                        Вердикт судьи на ринге — закон, который не обсуждается во время боя. Если рефери допустил явную и грубую ошибку, после проверки такое судейство будет жестко караться.
                    </div>
                </div>

                <div class="rule-card searchable" onclick="copyCardText(this)">
                    <div class="card-top">
                        <div class="card-title">Суточный лимит на поединки</div>
                        <span class="badge-penalty warn">Макс 3 боя</span>
                    </div>
                    <div class="card-desc">
                        Один боец имеет право провести не более 3 боев за одни сутки.
                    </div>
                </div>

                <div class="rule-card searchable" onclick="copyCardText(this)">
                    <div class="card-top">
                        <div class="card-title">Смена дивизионов и путевка наверх</div>
                        <span class="badge-penalty info">Продвижение</span>
                    </div>
                    <div class="card-desc">
                        При сильном доминировании администрация может принудительно перевести вас в более высокий рейтинг. В обычном порядке для перехода нужно завоевать чемпионский пояс текущего рейтинга и провести минимум одну успешную защиту.
                    </div>
                </div>

                <div class="rule-card searchable" onclick="copyCardText(this)">
                    <div class="card-top">
                        <div class="card-title">Право на вызов чемпиона</div>
                        <span class="badge-penalty info">Топ-5 / Топ-1</span>
                    </div>
                    <div class="card-desc">
                        Бросить вызов чемпиону могут только бойцы из Топ-5 рейтинга. Первый номер таблицы (Топ-1) имеет эксклюзивную привилегию: чемпион обязан принять его вызов безоговорочно!
                    </div>
                </div>
            </div>
        </section>

        <section id="bans">
            <div class="section-header">
                <div class="header-line"></div>
                <h2>9. Бан стили</h2>
            </div>
            <div class="bans-flex">
                <div class="ban-box searchable">slugger</div>
                <div class="ban-box searchable">hawk</div>
                <div class="ban-box searchable">hammer</div>
                <div class="ban-box searchable">switch hit (не может отменять ульту)</div>
                <div class="ban-box searchable">white ash</div>
                <div class="ban-box searchable">wolf</div>
                <div class="ban-box searchable">shotgun</div>
                <div class="ban-box searchable">corkscrew</div>
                <div class="ban-box searchable">bullet</div>
                <div class="ban-box searchable">chronos</div>
                <div class="ban-box searchable">deimos</div>
                <div class="ban-box searchable">all shinies</div>
                <div class="ban-box searchable">exclusive styles</div>
            </div>
        </section>

    </main>

    <button id="scrollTop" onclick="window.scrollTo({top:0, behavior:'smooth'})">↑</button>

    <footer>
        <p>Официальный регламент соревновательной лиги <span>U.C.L</span> &copy; 2026</p>
    </footer>

    <script>
        /* ===== Загрузочный экран ===== */
        let timeLeft = 5;
        const timerElement = document.getElementById('loadTimer');
        const loaderText = document.getElementById('loaderText');
        const loaderBell = document.getElementById('loaderBell');
        const loaderFight = document.getElementById('loaderFight');
        const loaderStages = ["ПОДГОТОВКА АРЕНЫ U.C.L...", "СЕКУНДАНТЫ ГОТОВЯТ УГЛЫ РИНГА...", "СУДЬЯ ПРОВЕРЯЕТ ПЕРЧАТКИ...", "ПОСЛЕДНИЕ ИНСТРУКЦИИ БОЙЦАМ..."];

        const countdown = setInterval(() => {
            timeLeft--;
            if (timeLeft > 0) {
                timerElement.textContent = `Загрузка: ${timeLeft} сек`;
                loaderText.textContent = loaderStages[(5 - timeLeft) % loaderStages.length];
            } else {
                clearInterval(countdown);
                timerElement.textContent = `Гонг!`;
                loaderBell.classList.add('ding');
                loaderText.textContent = "РИНГ ГОТОВ";
                loaderFight.classList.add('show');
                setTimeout(() => {
                    const loader = document.getElementById('loader');
                    loader.style.opacity = '0';
                    setTimeout(() => loader.style.visibility = 'hidden', 500);
                }, 450);
            }
        }, 1000);

        /* ===== Статус арены (МСК) ===== */
        function checkArenaStatus() {
            const now = new Date();
            const utc = now.getTime() + (now.getTimezoneOffset() * 60000);
            const msk = new Date(utc + (3600000 * 3));
            const hours = msk.getHours();

            const dot = document.getElementById('radarDot');
            const text = document.getElementById('radarText');

            if (hours >= 12 && hours < 22) {
                dot.className = 'radar-dot open';
                text.textContent = 'Арена открыта (12:00 - 22:00 МСК)';
                text.style.color = '#00e676';
            } else {
                dot.className = 'radar-dot closed';
                text.textContent = 'Арена закрыта (Открытие в 12:00 МСК)';
                text.style.color = 'var(--red)';
            }
        }
        checkArenaStatus();
        setInterval(checkArenaStatus, 30000);

        /* ===== Поиск ===== */
        function searchRules() {
            const query = document.getElementById('searchInput').value.toLowerCase().trim();
            const items = document.querySelectorAll('.searchable');
            items.forEach(item => {
                const text = item.textContent.toLowerCase();
                item.style.display = text.includes(query) ? "" : "none";
            });
        }

        /* ===== Копирование правила с "ударным" эффектом ===== */
        function copyCardText(card) {
            const title = card.querySelector('.card-title') ? card.querySelector('.card-title').innerText : 'Бан стиль';
            const desc = card.querySelector('.card-desc') ? card.querySelector('.card-desc').innerText : card.innerText;
            const textToCopy = `📌 [U.C.L Rule] ${title}: ${desc}`;

            card.classList.remove('punch');
            void card.offsetWidth;
            card.classList.add('punch');

            navigator.clipboard.writeText(textToCopy).then(() => {
                const toast = document.getElementById('toast');
                toast.classList.add('show');
                setTimeout(() => toast.classList.remove('show'), 2000);
            });
        }

        /* ===== Фоновые "искры" ===== */
        function spawnParticles() {
            const wrap = document.getElementById('particles');
            const symbols = ['🥊', '⭐', '💥'];
            for (let i = 0; i < 6; i++) {
                const el = document.createElement('div');
                el.className = 'p-ember';
                el.textContent = symbols[i % symbols.length];
                el.style.left = (Math.random() * 96 + 2) + '%';
                el.style.animationDuration = (14 + Math.random() * 10) + 's';
                el.style.animationDelay = (Math.random() * 12) + 's';
                el.style.fontSize = (0.8 + Math.random() * 0.8) + 'rem';
                wrap.appendChild(el);
            }
        }
        spawnParticles();

        /* ===== Настройки: подсветка ===== */
        const themeClasses = ['theme-gold', 'theme-cyan', 'theme-red', 'theme-purple', 'theme-green', 'theme-orange', 'theme-blue', 'theme-pink'];

        function setTheme(themeName, element) {
            themeClasses.forEach(t => document.body.classList.remove(t));
            document.body.classList.add(themeName);
            document.querySelectorAll('.dot-btn').forEach(btn => btn.classList.remove('active'));
            if (element) element.classList.add('active');
            localStorage.setItem('ucl_theme', themeName);
        }

        /* ===== Настройки: панель ===== */
        function toggleSettings() {
            document.getElementById('settingsDropdown').classList.toggle('open');
        }
        document.addEventListener('click', (e) => {
            const panel = document.querySelector('.customizer-panel');
            const dropdown = document.getElementById('settingsDropdown');
            if (dropdown.classList.contains('open') && !panel.contains(e.target)) {
                dropdown.classList.remove('open');
            }
        });

        /* ===== Настройки: отключение анимаций ===== */
        function toggleMotion(enabled) {
            document.body.classList.toggle('no-motion', !enabled);
            document.body.classList.add('motion-forced');
            localStorage.setItem('ucl_motion', enabled ? 'on' : 'off');
        }

        window.addEventListener('DOMContentLoaded', () => {
            const savedTheme = localStorage.getItem('ucl_theme');
            if (savedTheme && themeClasses.includes(savedTheme)) {
                themeClasses.forEach(t => document.body.classList.remove(t));
                document.body.classList.add(savedTheme);
                document.querySelectorAll('.dot-btn').forEach(btn => btn.classList.remove('active'));
                const activeDot = document.querySelector(`[onclick*="'${savedTheme}'"]`);
                if (activeDot) activeDot.classList.add('active');
            }

            const savedMotion = localStorage.getItem('ucl_motion');
            const prefersReduced = window.matchMedia && window.matchMedia('(prefers-reduced-motion: reduce)').matches;
            const motionOn = savedMotion ? savedMotion === 'on' : !prefersReduced;
            document.getElementById('motionToggle').checked = motionOn;
            document.body.classList.toggle('no-motion', !motionOn);
            document.body.classList.add('motion-forced');
        });

        /* ===== Скролл ===== */
        window.onscroll = () => {
            const winScroll = document.documentElement.scrollTop;
            const height = document.documentElement.scrollHeight - document.documentElement.clientHeight;
            const scrolled = (winScroll / height) * 100;
            document.getElementById("progress-bar").style.width = scrolled + "%";
            document.getElementById("scrollTop").style.display = winScroll > 300 ? "flex" : "none";
        };
    </script>
</body>
</html>
