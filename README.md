<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>U.C.L — Ultimate Championship League</title>
    <link href="https://fonts.googleapis.com/css2?family=Montserrat:ital,wght@0,400;0,600;0,800;0,900;1,900&family=Teko:wght@600;700&display=swap" rel="stylesheet">
    <style>
        :root {
            --bg-main: #06070c;
            --bg-card: rgba(18, 22, 41, 0.75);
            --bg-card-hover: rgba(26, 32, 59, 0.9);
            --accent-gold: #ffb703;
            --accent-gold-glow: rgba(255, 183, 3, 0.35);
            --danger: #ff4757;
            --danger-glow: rgba(255, 71, 87, 0.4);
            --success: #00e676;
            --info: #00f2fe;
            --text-primary: #ffffff;
            --text-secondary: #94a3b8;
            --border: rgba(255, 255, 255, 0.08);
            --border-accent: rgba(255, 183, 3, 0.3);
        }

        * { box-sizing: border-box; margin: 0; padding: 0; }
        html { scroll-behavior: smooth; }
        body {
            font-family: 'Montserrat', sans-serif;
            background-color: var(--bg-main);
            color: var(--text-primary);
            line-height: 1.6;
            overflow-x: hidden;
            background-image: 
                radial-gradient(circle at 15% 15%, rgba(255, 183, 3, 0.04) 0%, transparent 45%),
                radial-gradient(circle at 85% 85%, rgba(0, 242, 254, 0.04) 0%, transparent 45%);
        }

        /* Loading Screen */
        #loader {
            position: fixed; inset: 0;
            background: #030407;
            z-index: 99999;
            display: flex; flex-direction: column;
            align-items: center; justify-content: center;
            transition: opacity 0.6s ease, visibility 0.6s;
        }
        .loader-ring {
            width: 80px; height: 80px;
            border: 4px solid rgba(255, 183, 3, 0.1);
            border-top: 4px solid var(--accent-gold);
            border-radius: 50%;
            animation: spin 0.9s infinite linear;
            box-shadow: 0 0 20px var(--accent-gold-glow);
        }
        .loader-title {
            font-family: 'Teko', sans-serif;
            font-size: 2rem; letter-spacing: 3px;
            color: var(--accent-gold); margin-top: 20px;
            text-shadow: 0 0 10px var(--accent-gold-glow);
        }
        @keyframes spin { 0% { transform: rotate(0deg); } 100% { transform: rotate(360deg); } }

        /* Progress Line */
        #progress-bar {
            position: fixed; top: 0; left: 0; height: 3px;
            background: linear-gradient(90deg, var(--accent-gold), var(--info));
            width: 0%; z-index: 10000;
            box-shadow: 0 0 10px var(--accent-gold);
        }

        /* Top Bar / Status Radar */
        .status-bar-wrapper {
            display: flex; justify-content: center; padding: 15px 10px 0;
        }
        .status-radar {
            display: flex; align-items: center; gap: 10px;
            background: rgba(18, 22, 41, 0.8);
            border: 1px solid var(--border-accent);
            padding: 6px 18px; border-radius: 50px;
            backdrop-filter: blur(12px);
            box-shadow: 0 4px 20px rgba(0, 0, 0, 0.4);
        }
        .radar-dot {
            width: 10px; height: 10px; border-radius: 50%;
            position: relative;
        }
        .radar-dot.open { background: var(--success); box-shadow: 0 0 12px var(--success); }
        .radar-dot.closed { background: var(--danger); box-shadow: 0 0 12px var(--danger); }
        .radar-dot::after {
            content: ''; position: absolute; inset: -4px; border-radius: 50%;
            border: 2px solid currentColor; opacity: 0.7;
            animation: pulse 1.6s infinite ease-out;
        }
        @keyframes pulse { 0% { transform: scale(0.6); opacity: 1; } 100% { transform: scale(2.2); opacity: 0; } }
        .radar-text { font-size: 0.8rem; font-weight: 800; letter-spacing: 1px; text-transform: uppercase; }

        /* Hero Header */
        header {
            position: relative; padding: 30px 20px 40px; text-align: center;
            border-bottom: 1px solid var(--border);
            background: linear-gradient(180deg, rgba(6, 7, 12, 0.4) 0%, var(--bg-main) 100%);
        }
        .badge-main {
            display: inline-block;
            background: linear-gradient(135deg, var(--accent-gold), #d48806);
            color: #000; font-family: 'Teko', sans-serif;
            font-size: 1.4rem; font-weight: 700; padding: 2px 16px;
            border-radius: 4px; letter-spacing: 2px; text-transform: uppercase;
            box-shadow: 0 0 15px var(--accent-gold-glow); margin-bottom: 12px;
        }
        h1 {
            font-family: 'Teko', sans-serif; font-size: 4rem;
            line-height: 0.95; letter-spacing: 2px; text-transform: uppercase;
            margin-bottom: 15px;
        }
        h1 span {
            background: linear-gradient(135deg, var(--accent-gold), #ffffff);
            -webkit-background-clip: text; -webkit-text-fill-color: transparent;
        }

        /* Search input */
        .search-box {
            position: relative; max-width: 650px; margin: 25px auto 10px;
        }
        .search-box input {
            width: 100%; background: rgba(18, 22, 41, 0.9);
            border: 1px solid var(--border-accent);
            padding: 16px 22px; border-radius: 14px;
            color: #fff; font-size: 0.95rem; font-weight: 600;
            outline: none; transition: 0.3s ease;
            box-shadow: 0 8px 30px rgba(0, 0, 0, 0.3);
        }
        .search-box input:focus {
            border-color: var(--accent-gold);
            box-shadow: 0 0 25px var(--accent-gold-glow);
        }

        /* Nav Pills */
        .nav-scroller {
            display: flex; justify-content: center; gap: 8px; flex-wrap: wrap;
            max-width: 1000px; margin: 25px auto 0;
        }
        .nav-btn {
            background: var(--bg-card); border: 1px solid var(--border);
            color: var(--text-secondary); padding: 8px 16px; border-radius: 8px;
            font-weight: 700; font-size: 0.8rem; text-decoration: none;
            transition: 0.25s ease; text-transform: uppercase; letter-spacing: 0.5px;
        }
        .nav-btn:hover {
            background: var(--accent-gold); color: #000;
            border-color: var(--accent-gold); box-shadow: 0 4px 15px var(--accent-gold-glow);
        }

        /* Main Content Structure */
        .container { max-width: 1250px; margin: 40px auto; padding: 0 20px; }
        section { margin-bottom: 50px; }
        
        .section-title {
            display: flex; align-items: center; gap: 12px;
            margin-bottom: 25px; border-bottom: 1px solid var(--border);
            padding-bottom: 12px;
        }
        .section-title h2 {
            font-family: 'Teko', sans-serif; font-size: 2.5rem;
            letter-spacing: 1.5px; text-transform: uppercase;
        }
        .section-title .icon-box {
            width: 8px; height: 28px; background: var(--accent-gold);
            border-radius: 2px; box-shadow: 0 0 10px var(--accent-gold-glow);
        }

        /* Cards Layout */
        .grid-cards {
            display: grid; grid-template-columns: repeat(auto-fit, minmax(340px, 1fr)); gap: 20px;
        }
        .card {
            background: var(--bg-card); border: 1px solid var(--border);
            border-radius: 16px; padding: 24px; backdrop-filter: blur(10px);
            transition: all 0.3s cubic-bezier(0.25, 0.8, 0.25, 1);
            display: flex; flex-direction: column; justify-content: space-between;
            position: relative; overflow: hidden;
        }
        .card::before {
            content: ''; position: absolute; top: 0; left: 0; width: 4px; height: 100%;
            background: var(--accent-gold); opacity: 0.4; transition: 0.3s;
        }
        .card.danger::before { background: var(--danger); opacity: 0.8; }
        .card.info::before { background: var(--info); opacity: 0.8; }
        
        .card:hover {
            transform: translateY(-6px); background: var(--bg-card-hover);
            border-color: rgba(255, 255, 255, 0.2);
            box-shadow: 0 12px 30px rgba(0, 0, 0, 0.5);
        }
        .card:hover::before { opacity: 1; }

        .card-header {
            display: flex; justify-content: space-between; align-items: flex-start;
            margin-bottom: 12px; gap: 10px;
        }
        .card-title { font-size: 1.15rem; font-weight: 800; line-height: 1.3; }
        
        .tag {
            font-size: 0.68rem; font-weight: 800; padding: 4px 10px;
            border-radius: 6px; text-transform: uppercase; letter-spacing: 0.5px;
            white-space: nowrap;
        }
        .tag.warning { background: rgba(255, 183, 3, 0.12); color: var(--accent-gold); border: 1px solid var(--accent-gold); }
        .tag.danger { background: rgba(255, 71, 87, 0.12); color: var(--danger); border: 1px solid var(--danger); }
        .tag.info { background: rgba(0, 242, 254, 0.12); color: var(--info); border: 1px solid var(--info); }

        .card-body { color: var(--text-secondary); font-size: 0.92rem; }
        .card-body strong { color: #fff; font-weight: 700; }

        /* Ban Grid */
        .bans-container {
            display: grid; grid-template-columns: repeat(auto-fill, minmax(190px, 1fr)); gap: 14px;
        }
        .ban-card {
            background: rgba(255, 71, 87, 0.05); border: 1px solid rgba(255, 71, 87, 0.2);
            border-radius: 12px; padding: 14px; text-align: center;
            font-weight: 800; color: #ff6b81; font-size: 0.9rem;
            transition: 0.25s ease;
        }
        .ban-card:hover {
            background: rgba(255, 71, 87, 0.15); border-color: var(--danger);
            transform: scale(1.03); box-shadow: 0 0 15px var(--danger-glow);
        }

        /* Scroll Top Button */
        #scrollTop {
            position: fixed; bottom: 30px; right: 30px;
            width: 50px; height: 50px; background: var(--accent-gold);
            color: #000; border: none; border-radius: 14px; cursor: pointer;
            display: none; align-items: center; justify-content: center;
            font-weight: 900; font-size: 1.2rem; z-index: 999;
            box-shadow: 0 6px 20px var(--accent-gold-glow); transition: 0.3s;
        }
        #scrollTop:hover { transform: scale(1.1); }

        footer {
            text-align: center; padding: 35px 20px;
            border-top: 1px solid var(--border); color: var(--text-secondary);
            font-size: 0.85rem; font-weight: 600;
        }
        footer span { color: var(--accent-gold); }
    </style>
</head>
<body>

    <!-- 3-Second Loading Screen -->
    <div id="loader">
        <div class="loader-ring"></div>
        <div class="loader-title">U.C.L ARENA LOADING...</div>
    </div>

    <!-- Scroll Progress -->
    <div id="progress-bar"></div>

    <!-- Header Section -->
    <header>
        <div class="status-bar-wrapper">
            <div class="status-radar">
                <div id="radarDot" class="radar-dot"></div>
                <span id="radarText" class="radar-text">Синхронизация МСК...</span>
            </div>
        </div>

        <div class="badge-main">Official Regulations 2026</div>
        <h1>Регламент боёв <span>U.C.L</span></h1>

        <div class="search-box">
            <input type="text" id="searchInput" placeholder="Поиск по регламенту (ПД, слоу клик, баги, деш...)" oninput="filterRules()">
        </div>

        <div class="nav-scroller">
            <a href="#pd" class="nav-btn">1. Пассив / ПД</a>
            <a href="#bugs" class="nav-btn">2. Багоюз</a>
            <a href="#combos" class="nav-btn">3. Медленные M1</a>
            <a href="#skating" class="nav-btn">4. С-кейтинг</a>
            <a href="#dd" class="nav-btn">5. Дабл деш</a>
            <a href="#audio" class="nav-btn">6. Звуки / Картинки</a>
            <a href="#title" class="nav-btn">7. Титульные бои</a>
            <a href="#combat" class="nav-btn">8. Общий регламент</a>
            <a href="#bans" class="nav-btn">9. Бан стили</a>
        </div>
    </header>

    <main class="container">

        <!-- 1. PASSIVE & PD -->
        <section id="pd">
            <div class="section-title">
                <div class="icon-box"></div>
                <h2>1. Пассив и ПД Фишинг</h2>
            </div>
            <div class="grid-cards">
                <div class="card searchable">
                    <div class="card-header">
                        <div class="card-title">Суть ПД Фишинга</div>
                        <span class="tag warning">Ограничение</span>
                    </div>
                    <div class="card-body">
                        Намеренный отказ от действий ради уклонения. Разрешено делать <strong>2 уклона подряд</strong> только при стаггеринге или под спам-комбо. ПД-фиш разрешен только при <strong>нулевой стамине</strong>.
                    </div>
                </div>
                <div class="card searchable">
                    <div class="card-header">
                        <div class="card-title">Порог ожидания (2.5 сек)</div>
                        <span class="tag warning">Фол за абуз</span>
                    </div>
                    <div class="card-body">
                        Максимум ожидания — <strong>2.5 секунды</strong>. Незначительный выход — предупреждение, системность — фол. Распространяется на Dempsey Roll. Эмоции во время боя запрещены. ПД-фиш 3+ раз первым — фол.
                    </div>
                </div>
                <div class="card danger searchable">
                    <div class="card-header">
                        <div class="card-title">Сброс таймера и ультимейт</div>
                        <span class="tag danger">2 Фола</span>
                    </div>
                    <div class="card-body">
                        Удары и способности в нейтрале <strong>сбрасывают таймер 2.5 сек</strong>. Пассив или ПД-фиш ради нанесения ульта в конце боя караются <strong>2 фолами</strong>.
                    </div>
                </div>
            </div>
        </section>

        <!-- 2. BUGS -->
        <section id="bugs">
            <div class="section-title">
                <div class="icon-box"></div>
                <h2>2. Запрещенный багоюз</h2>
            </div>
            <div class="grid-cards">
                <div class="card danger searchable">
                    <div class="card-header">
                        <div class="card-title">Парирование ульты</div>
                        <span class="tag danger">Дисквалификация</span>
                    </div>
                    <div class="card-body">
                        Намеренный блок в тайминг при полете ультимейта с целью его «сжигания» без урона. Карается <strong>немедленным исключение из лиги</strong>.
                    </div>
                </div>
                <div class="card searchable">
                    <div class="card-header">
                        <div class="card-title">Нелегальный стаггеринг</div>
                        <span class="tag warning">Предупреждение ➔ Фол</span>
                    </div>
                    <div class="card-body">
                        Задержка M1 в серии, сделающая удар неуклоняемым и притягивающая соперника. Обычный стаггеринг для смены темпа разрешен.
                    </div>
                </div>
            </div>
        </section>

        <!-- 3. SLOW CLICKS -->
        <section id="combos">
            <div class="section-title">
                <div class="icon-box"></div>
                <h2>3. Медленные комбо M1 (Слоу клики)</h2>
            </div>
            <div class="grid-cards">
                <div class="card searchable">
                    <div class="card-header">
                        <div class="card-title">Условия использования</div>
                        <span class="tag warning">Макс 1 серия</span>
                    </div>
                    <div class="card-body">
                        Слоу клики разрешены <strong>только после попадания под ульт врага</strong>. Запрещены после обычных способностей. Разрешено проводить строго <strong>1 серию</strong>.
                    </div>
                </div>
                <div class="card info searchable">
                    <div class="card-header">
                        <div class="card-title">Исключения стилей</div>
                        <span class="tag info">Спец-правила</span>
                    </div>
                    <div class="card-body">
                        Стилю <strong>Крюк</strong> слоу клики запрещены полностью. После ультимейта <strong>Айрон Фиста</strong> разрешено делать <strong>2 комбо</strong> подряд.
                    </div>
                </div>
            </div>
        </section>

        <!-- 4. S-KATING -->
        <section id="skating">
            <div class="section-title">
                <div class="icon-box"></div>
                <h2>4. С-кейтинг и бекдеши</h2>
            </div>
            <div class="grid-cards">
                <div class="card searchable">
                    <div class="card-header">
                        <div class="card-title">Правила отхода назад</div>
                        <span class="tag warning">Фол</span>
                    </div>
                    <div class="card-body">
                        С-кейтинг (уход назад на S) разрешен только после собственного успешного удара/комбо. Пропуск 2 действий соперника при отступлении — <strong>фол</strong>.
                    </div>
                </div>
                <div class="card searchable">
                    <div class="card-header">
                        <div class="card-title">Таймер дистанции</div>
                        <span class="tag warning">Фол обоим</span>
                    </div>
                    <div class="card-body">
                        Если оба игрока удерживают дистанцию сверх 2.5 сек, включается <strong>3-секундный отсчет</strong>. Отсутствие сближения — фол обоим бойцам.
                    </div>
                </div>
            </div>
        </section>

        <!-- 5. DOUBLE DASH -->
        <section id="dd">
            <div class="section-title">
                <div class="icon-box"></div>
                <h2>5. Дабл деш (ДД)</h2>
            </div>
            <div class="grid-cards">
                <div class="card danger searchable">
                    <div class="card-header">
                        <div class="card-title">ДД для спидстеров</div>
                        <span class="tag danger">Строго запрещено</span>
                    </div>
                    <div class="card-body">
                        Двойной деш подряд для уклонения от финтов на скоростных стилях карается фолом. <strong>Трипл деш запрещен полностью</strong>.
                    </div>
                </div>
                <div class="card info searchable">
                    <div class="card-header">
                        <div class="card-title">Разрешенный Дабл Деш</div>
                        <span class="tag info">Условие</span>
                    </div>
                    <div class="card-body">
                        Два деша подряд разрешено выполнять исключительно <strong>после совершения двух атак</strong>.
                    </div>
                </div>
            </div>
        </section>

        <!-- 6. AUDIO & MEDIA -->
        <section id="audio">
            <div class="section-title">
                <div class="icon-box"></div>
                <h2>6. Звуки и Изображения</h2>
            </div>
            <div class="grid-cards">
                <div class="card searchable">
                    <div class="card-header">
                        <div class="card-title">Звуки Perfect Dodge</div>
                        <span class="tag warning">По запросу</span>
                    </div>
                    <div class="card-body">
                        Кастомные звуки ПД разрешены. Рефери имеет право потребовать их отключение при создании помех сопернику.
                    </div>
                </div>
                <div class="card danger searchable">
                    <div class="card-header">
                        <div class="card-title">Каунтеры и Картинки</div>
                        <span class="tag danger">Бан</span>
                    </div>
                    <div class="card-body">
                        Звуки контрударов и визуальные картинки запрещены. <strong>Исключение:</strong> аудио и визуал для ультимативных способностей разрешены.
                    </div>
                </div>
            </div>
        </section>

        <!-- 7. TITLE FIGHTS -->
        <section id="title">
            <div class="section-title">
                <div class="icon-box"></div>
                <h2>7. Титульные Бои</h2>
            </div>
            <div class="grid-cards">
                <div class="card info searchable">
                    <div class="card-header">
                        <div class="card-title">Регламент Bo3 и Судейство</div>
                        <span class="tag info">Формат Bo3</span>
                    </div>
                    <div class="card-body">
                        Бои проходят до 2 побед (Bo3). Смена стиля допускается только после поражения. Поединок оценивают 3 рефери высшей категории.
                    </div>
                </div>
                <div class="card info searchable">
                    <div class="card-header">
                        <div class="card-title">Сроки защиты поясов</div>
                        <span class="tag info">График</span>
                    </div>
                    <div class="card-body">
                        • <strong>UNF:</strong> Защита раз в неделю<br>
                        • <strong>UNC:</strong> Защита каждые 2 недели<br>
                        • <strong>UCL:</strong> Защита каждые 2.5 недели
                    </div>
                </div>
            </div>
        </section>

        <!-- 8. COMBAT RULES -->
        <section id="combat">
            <div class="section-title">
                <div class="icon-box"></div>
                <h2>8. Общие Правила Лиги</h2>
            </div>
            <div class="grid-cards">
                <div class="card searchable">
                    <div class="card-header">
                        <div class="card-title">Технические проблемы</div>
                        <span class="tag warning">5 минут</span>
                    </div>
                    <div class="card-body">
                        При вылете бойцу дается ровно <strong>5 минут</strong> на перезаход. Превышение лимита — техническое поражение.
                    </div>
                </div>
                <div class="card searchable">
                    <div class="card-header">
                        <div class="card-title">Ограничения боев</div>
                        <span class="tag warning">Макс 3 в день</span>
                    </div>
                    <div class="card-body">
                        Лимит: не более 3 официальных боев в сутки. Для претендентского боя необходим входящий в <strong>Топ-5</strong> рейтинг.
                    </div>
                </div>
            </div>
        </section>

        <!-- 9. BANNED STYLES -->
        <section id="bans">
            <div class="section-title">
                <div class="icon-box"></div>
                <h2>9. Запрещенные Стили (Banned)</h2>
            </div>
            <div class="bans-container">
                <div class="ban-card searchable">Slugger</div>
                <div class="ban-card searchable">Hawk</div>
                <div class="ban-card searchable">Hammer</div>
                <div class="ban-card searchable">Dragonfish</div>
                <div class="ban-card searchable">White Ash</div>
                <div class="ban-card searchable">Wolf</div>
                <div class="ban-card searchable">Hitman</div>
                <div class="ban-card searchable">Shotgun</div>
                <div class="ban-card searchable">Corkscrew</div>
                <div class="ban-card searchable">Bullet</div>
                <div class="ban-card searchable">Chronos</div>
                <div class="ban-card searchable">All Shiny Versions</div>
                <div class="ban-card searchable">Exclusive Styles</div>
            </div>
        </section>

    </main>

    <button id="scrollTop" onclick="window.scrollTo({top: 0, behavior: 'smooth'})">↑</button>

    <footer>
        <p>Ultimate Championship League &copy; 2026. Все права защищены. <span>U.C.L Arena</span></p>
    </footer>

    <script>
        // Preloader 3s
        window.addEventListener('load', () => {
            setTimeout(() => {
                const loader = document.getElementById('loader');
                loader.style.opacity = '0';
                loader.style.visibility = 'hidden';
            }, 3000);
        });

        // MSK Time status radar
        function updateLeagueRadar() {
            const now = new Date();
            const utc = now.getTime() + (now.getTimezoneOffset() * 60000);
            const msk = new Date(utc + (3600000 * 3));
            const hours = msk.getHours();

            const dot = document.getElementById('radarDot');
            const text = document.getElementById('radarText');

            if (hours >= 12 && hours < 22) {
                dot.className = 'radar-dot open';
                text.textContent = 'Лига открыта (12:00 - 22:00 МСК)';
                text.style.color = 'var(--success)';
            } else {
                dot.className = 'radar-dot closed';
                text.textContent = 'Лига закрыта (Открытие в 12:00 МСК)';
                text.style.color = 'var(--danger)';
            }
        }
        updateLeagueRadar();
        setInterval(updateLeagueRadar, 30000);

        // Search Filter
        function filterRules() {
            const query = document.getElementById('searchInput').value.toLowerCase();
            const cards = document.querySelectorAll('.searchable');
            cards.forEach(card => {
                const content = card.textContent.toLowerCase();
                card.style.display = content.includes(query) ? 'flex' : 'none';
            });
        }

        // Scroll events
        window.onscroll = () => {
            const scrollTop = document.documentElement.scrollTop;
            const scrollHeight = document.documentElement.scrollHeight - document.documentElement.clientHeight;
            const progress = (scrollTop / scrollHeight) * 100;
            document.getElementById('progress-bar').style.width = progress + '%';
            
            const btn = document.getElementById('scrollTop');
            btn.style.display = scrollTop > 400 ? 'flex' : 'none';
        };
    </script>
</body>
</html>
