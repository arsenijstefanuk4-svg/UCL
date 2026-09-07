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

        * { box-sizing: border-box; margin: 0; padding: 0; }
        html { scroll-behavior: smooth; }
        
        body {
            font-family: 'Montserrat', sans-serif;
            background-color: var(--bg-dark);
            color: var(--text-main);
            line-height: 1.5;
            overflow-x: hidden;
            background-image: 
                radial-gradient(circle at 50% 0%, rgba(255, 183, 3, 0.15) 0%, transparent 50%),
                radial-gradient(circle at 100% 100%, rgba(255, 42, 75, 0.1) 0%, transparent 40%),
                linear-gradient(to right, rgba(255, 255, 255, 0.02) 1px, transparent 1px),
                linear-gradient(to bottom, rgba(255, 255, 255, 0.02) 1px, transparent 1px);
            background-size: 100% 100%, 100% 100%, 40px 40px, 40px 40px;
        }

        #progress-bar {
            position: fixed; top: 0; left: 0; height: 3px;
            background: linear-gradient(90deg, var(--red), var(--gold), var(--cyan));
            width: 0%; z-index: 10000;
            box-shadow: 0 0 12px var(--gold);
        }

        /* 5-секундный прелоадер */
        #loader {
            position: fixed; inset: 0; background: #020203;
            z-index: 99999; display: flex; flex-direction: column;
            align-items: center; justify-content: center;
            transition: opacity 0.5s ease, visibility 0.5s;
        }

        .punch-stage {
            position: relative; width: 220px; height: 160px;
            display: flex; align-items: center; justify-content: center;
        }

        .heavy-bag {
            font-size: 4.5rem; position: relative; z-index: 1;
            transform-origin: top center; animation: bagSwing 0.6s ease-in-out infinite alternate;
        }

        .glove-left, .glove-right {
            position: absolute; font-size: 3rem; z-index: 2; top: 35px;
        }

        .glove-left {
            left: 0; animation: punchLeft 0.6s ease-in-out infinite;
        }

        .glove-right {
            right: 0; transform: scaleX(-1); animation: punchRight 0.6s ease-in-out infinite 0.3s;
        }

        .impact-spark {
            position: absolute; width: 30px; height: 30px;
            border-radius: 50%; background: var(--gold);
            box-shadow: 0 0 25px var(--gold), 0 0 40px var(--red);
            opacity: 0; z-index: 3; animation: sparkFlash 0.6s infinite;
        }

        @keyframes bagSwing {
            0% { transform: rotate(-8deg); }
            100% { transform: rotate(8deg); }
        }

        @keyframes punchLeft {
            0%, 100% { transform: translateX(0) rotate(-10deg); }
            50% { transform: translateX(55px) rotate(15deg); }
        }

        @keyframes punchRight {
            0%, 100% { transform: scaleX(-1) translateX(0) rotate(-10deg); }
            50% { transform: scaleX(-1) translateX(55px) rotate(15deg); }
        }

        @keyframes sparkFlash {
            0%, 40%, 60%, 100% { opacity: 0; transform: scale(0.5); }
            50% { opacity: 1; transform: scale(1.4); }
        }

        .loader-text {
            font-family: 'Teko', sans-serif; font-size: 2.2rem;
            letter-spacing: 3px; color: var(--gold); margin-top: 20px;
            text-shadow: 0 0 15px var(--gold-glow);
        }

        .loader-timer {
            font-size: 0.9rem; color: var(--text-sub); margin-top: 5px; font-weight: 700;
        }

        /* Полноширинная зацикленная бегущая строка по центру */
        .marquee-wrapper {
            background: linear-gradient(90deg, #100003, var(--red), var(--gold), #100003);
            color: #ffffff;
            font-weight: 900;
            font-size: 0.95rem;
            text-transform: uppercase;
            letter-spacing: 2px;
            padding: 12px 0;
            overflow: hidden;
            white-space: nowrap;
            width: 100vw;
            position: relative;
            left: 50%;
            transform: translateX(-50%);
            display: flex;
            border-bottom: 1px solid var(--gold);
            box-shadow: 0 4px 20px rgba(0,0,0,0.9);
        }

        .marquee-content { 
            display: flex;
            flex-shrink: 0;
            white-space: nowrap;
            animation: marquee 14s linear infinite;
            text-shadow: 0 2px 4px rgba(0, 0, 0, 0.8);
        }

        .marquee-item {
            padding-right: 50px;
        }

        @keyframes marquee { 
            0% { transform: translateX(0%); } 
            100% { transform: translateX(-50%); } 
        }

        .status-container { display: flex; justify-content: center; margin-top: 25px; }
        .status-badge {
            display: flex; align-items: center; gap: 10px;
            background: rgba(15, 18, 32, 0.85); border: 1px solid var(--gold);
            padding: 8px 18px; border-radius: 50px;
            box-shadow: 0 0 20px var(--gold-glow); backdrop-filter: blur(12px);
        }
        .radar-dot { width: 10px; height: 10px; border-radius: 50%; }
        .radar-dot.open { background: #00e676; box-shadow: 0 0 12px #00e676; }
        .radar-dot.closed { background: var(--red); box-shadow: 0 0 12px var(--red); }

        header { text-align: center; padding: 20px 15px; }
        .main-badge {
            display: inline-block; background: linear-gradient(45deg, var(--red), #ff5252); color: #fff;
            font-family: 'Teko', sans-serif; font-size: 1.3rem; font-weight: 700;
            padding: 2px 16px; border-radius: 4px; text-transform: uppercase;
            letter-spacing: 2px; box-shadow: 0 0 15px var(--red-glow);
            transform: skewX(-8deg); margin-bottom: 12px;
        }
        h1 {
            font-family: 'Teko', sans-serif; font-size: 3.5rem;
            line-height: 0.95; text-transform: uppercase; letter-spacing: 2px;
        }
        h1 span { color: var(--gold); text-shadow: 0 0 20px var(--gold-glow); }

        .search-wrapper { width: 100%; max-width: 650px; margin: 20px auto 0; padding: 0 10px; }
        .search-input {
            width: 100%; background: rgba(15, 18, 32, 0.9);
            border: 2px solid var(--border-grid);
            padding: 14px 20px; border-radius: 14px;
            color: #fff; font-size: 1rem; font-weight: 600;
            outline: none; transition: 0.3s ease; backdrop-filter: blur(10px);
        }
        .search-input:focus { border-color: var(--gold); box-shadow: 0 0 25px var(--gold-glow); }

        .nav-scroller {
            display: flex; gap: 10px; overflow-x: auto;
            padding: 20px 10px 10px; scrollbar-width: none;
            justify-content: center; flex-wrap: wrap;
        }
        .nav-scroller::-webkit-scrollbar { display: none; }
        .nav-link {
            background: rgba(20, 25, 45, 0.7); border: 1px solid var(--border-grid);
            color: var(--text-sub); padding: 8px 16px; border-radius: 8px;
            font-weight: 700; font-size: 0.8rem; text-decoration: none;
            text-transform: uppercase; transition: 0.2s ease;
        }
        .nav-link:hover { border-color: var(--gold); color: #fff; transform: translateY(-2deg); }

        .container { width: 100%; max-width: 1250px; margin: 30px auto; padding: 0 15px; }
        section { margin-bottom: 45px; }

        .section-header {
            display: flex; align-items: center; gap: 12px;
            margin-bottom: 22px; border-bottom: 2px solid var(--border-grid);
            padding-bottom: 8px;
        }
        .section-header h2 {
            font-family: 'Teko', sans-serif; font-size: 2.3rem;
            text-transform: uppercase; letter-spacing: 1px;
        }
        .header-line {
            height: 5px; width: 25px; background: var(--gold);
            box-shadow: 0 0 12px var(--gold-glow); border-radius: 2px;
        }

        .rules-grid {
            display: grid; grid-template-columns: repeat(auto-fit, minmax(320px, 1fr));
            gap: 20px;
        }
        .rule-card {
            background: var(--bg-card); border: 1px solid var(--border-grid);
            border-radius: 16px; padding: 22px; backdrop-filter: blur(16px);
            display: flex; flex-direction: column; justify-content: space-between;
            transition: all 0.3s ease; cursor: pointer; position: relative;
        }
        .rule-card:hover {
            transform: translateY(-4deg);
            border-color: var(--gold);
            box-shadow: 0 8px 25px rgba(255, 183, 3, 0.15);
        }
        .rule-card.danger-card { border-color: rgba(255, 42, 75, 0.3); }
        .rule-card.danger-card:hover {
            border-color: var(--red);
            box-shadow: 0 8px 25px rgba(255, 42, 75, 0.2);
        }

        .card-top {
            display: flex; justify-content: space-between; align-items: flex-start;
            margin-bottom: 14px; gap: 10px;
        }
        .card-title { font-size: 1.1rem; font-weight: 800; line-height: 1.3; }

        .badge-penalty {
            font-size: 0.7rem; font-weight: 900; padding: 4px 10px;
            border-radius: 6px; text-transform: uppercase; white-space: nowrap;
        }
        .badge-penalty.warn { background: rgba(255, 183, 3, 0.15); color: var(--gold); border: 1px solid var(--gold); }
        .badge-penalty.danger { background: rgba(255, 42, 75, 0.15); color: var(--red); border: 1px solid var(--red); }
        .badge-penalty.info { background: rgba(0, 242, 254, 0.15); color: var(--cyan); border: 1px solid var(--cyan); }

        .card-desc { color: var(--text-sub); font-size: 0.92rem; }
        .card-desc strong { color: #fff; }

        .bans-flex {
            display: grid; grid-template-columns: repeat(auto-fill, minmax(140px, 1fr)); gap: 12px;
        }
        .ban-box {
            background: rgba(255, 42, 75, 0.06); border: 1px solid rgba(255, 42, 75, 0.25);
            border-radius: 10px; padding: 14px 8px; text-align: center;
            font-weight: 800; color: #ff6b81; font-size: 0.85rem; transition: 0.2s;
        }
        .ban-box:hover { background: rgba(255, 42, 75, 0.2); transform: scale(1.03); }

        #toast {
            position: fixed; bottom: 30px; left: 50%; transform: translateX(-50%) translateY(100px);
            background: var(--gold); color: #000; padding: 10px 24px; border-radius: 30px;
            font-weight: 800; font-size: 0.85rem; box-shadow: 0 0 20px var(--gold-glow);
            opacity: 0; transition: all 0.3s ease; z-index: 10000; pointer-events: none;
        }
        #toast.show { transform: translateX(-50%) translateY(0); opacity: 1; }

        #scrollTop {
            position: fixed; bottom: 25px; right: 25px;
            width: 48px; height: 48px; background: var(--gold);
            color: #000; border: none; border-radius: 50%; cursor: pointer;
            display: none; align-items: center; justify-content: center;
            font-weight: 900; font-size: 1.3rem; z-index: 999;
            box-shadow: 0 0 20px var(--gold-glow); transition: 0.2s;
        }
        #scrollTop:hover { transform: scale(1.1); }

        footer {
            text-align: center; padding: 30px 15px;
            border-top: 1px solid var(--border-grid); color: var(--text-sub); font-size: 0.85rem;
        }
        footer span { color: var(--gold); font-weight: 800; }
    </style>
</head>
<body>

    <div id="loader">
        <div class="punch-stage">
            <div class="glove-left">🥊</div>
            <div class="heavy-bag">🥊</div>
            <div class="glove-right">🥊</div>
            <div class="impact-spark"></div>
        </div>
        <div class="loader-text">ПОДГОТОВКА АРЕНЫ U.C.L...</div>
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
                        <span class="badge-penalty warn">Предупреждение / Фол</span>
                    </div>
                    <div class="card-desc">
                        Ждать удара можно максимум <strong>2 секунды</strong>, вы можете случайно выйти за рамки времени и будет только предупреждение, но если вы злоупотребляете этим то получите фол. Это касается и демпси ролла - вы не можете злоупотреблять им больше чем <strong>2 секунды</strong>.<br><br>
                        Если вы первым ждёте удар и пдфишите, больше двух раз, даже если делаете это в таймер пдфиша (2 секунды) то даётся фол.
                    </div>
                </div>

                <div class="rule-card danger-card searchable" onclick="copyCardText(this)">
                    <div class="card-top">
                        <div class="card-title">Сброс таймера, Эмоции и Стамина</div>
                        <span class="badge-penalty danger">2 Фола</span>
                    </div>
                    <div class="card-desc">
                        Попытка удара и получение контрудара сбрасывают таймер порога ПД фиша (таймер 2 секунды). Также атака и способности которые возвращают бойцов на нейтральное положение тоже сбрасывает таймер.<br><br>
                        Использование эмоций будет приравниваться к бездействию. ( кроме начала раунда ).<br><br>
                        Если вы пассивите или пдфишите в конце боя чтобы нанести ульту это приравнивается как <strong>два фола</strong>.<br><br>
                        Пдфишить можно когда у бойца закончилась стамина <strong>ПОЛНОСТЬЮ</strong>.
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
                        Когда в вас летит ульта и вас должны пробить и вы в тайминг прожимаете блок и ульта сжирается (если сделаете это намеренно будет вылет из реальной жизни).
                    </div>
                </div>

                <div class="rule-card searchable" onclick="copyCardText(this)">
                    <div class="card-top">
                        <div class="card-title">Нелегальный стаггеринг</div>
                        <span class="badge-penalty warn">Предупреждение ➔ Фол</span>
                    </div>
                    <div class="card-desc">
                        Это когда удар M1 все еще регистрируется в серии, но задерживается и становится неуклоняемым, а также притягивает игрока обратно, несмотря на уклонение и срабатывание кадров, будет считаться нарушением.<br><br>
                        Первое нарушение за нелегальный стаггеринг влечет за собой устное предупреждение. Последующие нарушения приведут к фолу.
                    </div>
                </div>

                <div class="rule-card searchable" onclick="copyCardText(this)">
                    <div class="card-top">
                        <div class="card-title">Разрешенный стаггеринг</div>
                        <span class="badge-penalty info">Разрешено</span>
                    </div>
                    <div class="card-desc">
                        Стаггеринг (тыкать М1 когда хочешь перебить атаку противника) с целью смены темпа или миксапов разрешен .
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
                        Медленные удары M1 разрешены только после того, как игрок попал под ультимейт. Медленные M1 нельзя использовать после способностей (например, Focus, Stampede и т. д.). Игрокам разрешено использовать медленные M1 только для <strong>ОДНОЙ СЕРИИ УДАРОВ</strong> большее количество приведет к фолу.
                    </div>
                </div>

                <div class="rule-card searchable" onclick="copyCardText(this)">
                    <div class="card-top">
                        <div class="card-title">Исключения для стилей</div>
                        <span class="badge-penalty info">Исключения</span>
                    </div>
                    <div class="card-desc">
                        <strong>ИСКЛЮЧЕНИЕ:</strong> нельзя использовать стилю крюк слоу клики после ультимейта.<br><br>
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
                        С-кейтинг - уход назад от противника зажатие кнопки S ( направление джойстика назад ). Можно использовать после попадания удара или комбо по сопернику, если вы идёте назад и ничего не делаете пропуская два действия противника - фол. Также и с бекдешом.
                    </div>
                </div>

                <div class="rule-card searchable" onclick="copyCardText(this)">
                    <div class="card-top">
                        <div class="card-title">Обоюдный кайтанг</div>
                        <span class="badge-penalty warn">Фол обоим</span>
                    </div>
                    <div class="card-desc">
                        Если оба игрока намеренно держатся на расстоянии, включается 3 секундный счёт после 2 секундного счёта порога ПД, ЕСЛИ никто из игроков не приближается обоим - фол.
                    </div>
                </div>

                <div class="rule-card searchable" onclick="copyCardText(this)">
                    <div class="card-top">
                        <div class="card-title">Против Демпси и Шотгана</div>
                        <span class="badge-penalty info">Особые условия</span>
                    </div>
                    <div class="card-desc">
                        Против демпси можно фишить но нельзя уходить назад ( С-кейтить ).<br><br>
                        Против шотгана можно использовать бекдеш на способность если вы до этого сделали бекдеш.
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
                <div class="rule-card danger-card searchable" onclick="copyCardText(this)">
                    <div class="card-top">
                        <div class="card-title">Дабл деш подряд (спидстеры)</div>
                        <span class="badge-penalty danger">Запрещено (Фол)</span>
                    </div>
                    <div class="card-desc">
                        Дабл деш подряд (для спидстеров) - который используется для уклона от финтов, он запрещён даётся фол за него.
                    </div>
                </div>

                <div class="rule-card searchable" onclick="copyCardText(this)">
                    <div class="card-top">
                        <div class="card-title">Правила Дешей</div>
                        <span class="badge-penalty info">Разрешено / Запрещено</span>
                    </div>
                    <div class="card-desc">
                        Второе понятие: два деша после двух атак разрешён.<br><br>
                        Трипл деш запрещён.
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
                        Использование неприятных или раздражающих звуковых эффектов и изображений может отвлекать игроков во время игры. Ниже приведены правила, касающиеся пользовательских звуковых эффектов и изображений; несоблюдение этих правил приведет к предупреждению.
                    </div>
                </div>

                <div class="rule-card searchable" onclick="copyCardText(this)">
                    <div class="card-top">
                        <div class="card-title">Звуки ПД (Идеальное уклонение)</div>
                        <span class="badge-penalty info">На усмотрение</span>
                    </div>
                    <div class="card-desc">
                        Пользовательские звуковые эффекты идеального уклонения (ПД) остаются на усмотрение игроков, но может быть запрошено их удаление, чтобы избежать несправедливого преимущества из-за отвлечения внимания.
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
                        Проводятся в формате бо3 ( 3 боя ). Игрок может сменить стиль только после поражения; победитель должен сохранять текущий стиль до проигрыша. Правила такие же как и в обычных боях.<br><br>
                        За боем будут наблюдать рефери высшей категории которые будут давать оценки за бой.<br><br>
                        Максимальный балл 10 очков по системе оценивания рефери, если вы играли пассивно и выиграли с небольшим отрывом, но набрали очков меньше чем противник, то рефери могут отдать победу ему.
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
                        Если прямо посреди матча у вас оборвалось соединение или вылетела игра, включается счетчик: у вас есть ровно 5 минут на немедленное возвращение. Если не уложитесь в этот дедлайн - поединок либо полностью аннулируется, либо вам присуждается технический нокаут (ТКО) по решению рефери.
                    </div>
                </div>

                <div class="rule-card searchable" onclick="copyCardText(this)">
                    <div class="card-top">
                        <div class="card-title">Неоспоримый авторитет рефери</div>
                        <span class="badge-penalty info">Закон на ринге</span>
                    </div>
                    <div class="card-desc">
                        Вердикт судьи на ринге - это закон, который не обсуждается во время боя. Однако, если рефери допустил явную и грубую ошибку, это не сойдет ему с рук - после проверки такое судейство будет жестко караться.
                    </div>
                </div>

                <div class="rule-card searchable" onclick="copyCardText(this)">
                    <div class="card-top">
                        <div class="card-title">Суточный лимит на поединки</div>
                        <span class="badge-penalty warn">Макс 3 боя</span>
                    </div>
                    <div class="card-desc">
                        Не стоит перегорать на ринге. Введено строгое ограничение: один боец имеет право провести не более 3 боев за одни сутки.
                    </div>
                </div>

                <div class="rule-card searchable" onclick="copyCardText(this)">
                    <div class="card-top">
                        <div class="card-title">Смена дивизионов и путевка наверх</div>
                        <span class="badge-penalty info">Продвижение</span>
                    </div>
                    <div class="card-desc">
                        Если вы буквально аннигилируете своих соперников без шансов, администрация может принудительно перевести вас в более высокий рейтинг за слишком явное доминирование. В обычном же порядке, чтобы легально перейти в другую лигу, вам необходимо сначала завоевать чемпионский пояс текущего рейтинга и провести как минимум одну успешную защиту.
                    </div>
                </div>

                <div class="rule-card searchable" onclick="copyCardText(this)">
                    <div class="card-top">
                        <div class="card-title">Право на вызов чемпиона</div>
                        <span class="badge-penalty info">Топ-5 / Топ-1</span>
                    </div>
                    <div class="card-desc">
                        Покушаться на пояс короля имеют право далеко не все - бросить вызов действующему чемпиону могут только бойцы из первой пятерки (Топ-5) рейтинга. При этом первый номер таблицы (Топ-1) обладает эксклюзивной привилегией: чемпион обязан принять его вызов безоговорочно!
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
                <div class="ban-box searchable">dragonfish</div>
                <div class="ban-box searchable">white ash</div>
                <div class="ban-box searchable">wolf</div>
                <div class="ban-box searchable">hitman</div>
                <div class="ban-box searchable">shotgun</div>
                <div class="ban-box searchable">corkscrew</div>
                <div class="ban-box searchable">bullet</div>
                <div class="ban-box searchable">chronos</div>
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
        let timeLeft = 5;
        const timerElement = document.getElementById('loadTimer');
        
        const countdown = setInterval(() => {
            timeLeft--;
            if (timeLeft > 0) {
                timerElement.textContent = `Загрузка: ${timeLeft} сек`;
            } else {
                clearInterval(countdown);
                timerElement.textContent = `Готово!`;
                const loader = document.getElementById('loader');
                loader.style.opacity = '0';
                setTimeout(() => loader.style.visibility = 'hidden', 500);
            }
        }, 1000);

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

        function searchRules() {
            const query = document.getElementById('searchInput').value.toLowerCase().trim();
            const items = document.querySelectorAll('.searchable');

            items.forEach(item => {
                const text = item.textContent.toLowerCase();
                if (text.includes(query)) {
                    item.style.display = "";
                } else {
                    item.style.display = "none";
                }
            });
        }

        function copyCardText(card) {
            const title = card.querySelector('.card-title') ? card.querySelector('.card-title').innerText : 'Бан стиль';
            const desc = card.querySelector('.card-desc') ? card.querySelector('.card-desc').innerText : card.innerText;
            const textToCopy = `📌 [U.C.L Rule] ${title}: ${desc}`;
            
            navigator.clipboard.writeText(textToCopy).then(() => {
                const toast = document.getElementById('toast');
                toast.classList.add('show');
                setTimeout(() => toast.classList.remove('show'), 2000);
            });
        }

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
