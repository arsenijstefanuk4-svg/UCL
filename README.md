<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>U.C.L — Официальный Регламент Боёв</title>
    <link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@400;500;600;700;800;900&family=Teko:wght@600;700&display=swap" rel="stylesheet">
    <style>
        :root {
            --bg-primary: #070913;
            --bg-secondary: #0f1322;
            --bg-card: rgba(21, 26, 46, 0.7);
            --accent: #f39c12;
            --accent-glow: rgba(243, 156, 18, 0.4);
            --danger: #ff4757;
            --danger-glow: rgba(255, 71, 87, 0.4);
            --success: #2ed573;
            --info: #1e90ff;
            --text-main: #f1f5f9;
            --text-muted: #8b9bb4;
            --border-color: rgba(35, 45, 74, 0.8);
        }

        * { box-sizing: border-box; margin: 0; padding: 0; }
        html, body { width: 100%; overflow-x: hidden; scroll-behavior: smooth; }
        body {
            font-family: 'Montserrat', sans-serif;
            background-color: var(--bg-primary);
            color: var(--text-main);
            line-height: 1.6;
            background-image: 
                radial-gradient(circle at 10% 20%, rgba(243, 156, 18, 0.05) 0%, transparent 40%),
                radial-gradient(circle at 90% 80%, rgba(30, 144, 255, 0.05) 0%, transparent 40%);
        }

        /* Preloader */
        #loader {
            position: fixed;
            inset: 0;
            background: var(--bg-primary);
            z-index: 99999;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            transition: opacity 0.5s ease, visibility 0.5s;
        }
        .spinner {
            width: 70px;
            height: 70px;
            border: 5px solid rgba(243, 156, 18, 0.2);
            border-top: 5px solid var(--accent);
            border-radius: 50%;
            animation: spin 1s infinite linear;
            margin-bottom: 15px;
        }
        @keyframes spin { 0% { transform: rotate(0deg); } 100% { transform: rotate(360deg); } }

        /* Progress & Floating UI */
        #progress-bar {
            position: fixed; top: 0; left: 0; height: 4px;
            background: var(--accent); width: 0%; z-index: 1000;
            box-shadow: 0 0 12px var(--accent);
        }
        
        /* Status Radar Banner */
        .status-radar {
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 10px;
            background: rgba(15, 19, 34, 0.9);
            border: 1px solid var(--border-color);
            padding: 8px 16px;
            border-radius: 30px;
            margin: 0 auto 15px;
            width: fit-content;
            backdrop-filter: blur(8px);
        }
        .radar-dot {
            width: 12px; height: 12px; border-radius: 50%;
            position: relative;
        }
        .radar-dot.open { background: var(--success); box-shadow: 0 0 10px var(--success); }
        .radar-dot.closed { background: var(--danger); box-shadow: 0 0 10px var(--danger); }
        .radar-dot::after {
            content: ''; position: absolute; inset: -3px; border-radius: 50%;
            border: 2px solid cubic-bezier(0, 0.2, 0.8, 1);
            animation: pulse 1.5s infinite;
        }
        @keyframes pulse { 0% { transform: scale(0.8); opacity: 1; } 100% { transform: scale(1.8); opacity: 0; } }

        /* Header & Hero */
        header {
            background: linear-gradient(135deg, rgba(15, 19, 34, 0.95), rgba(7, 9, 19, 0.98)), url('https://images.unsplash.com/photo-1542751371-adc38448a05e?auto=format&fit=crop&w=1920&q=80') center/cover no-repeat;
            border-bottom: 3px solid var(--accent);
            padding: 40px 16px 30px;
            text-align: center;
        }
        .hero-container { max-width: 900px; margin: 0 auto; }
        .logo-badge {
            display: inline-block; background: var(--accent); color: #000;
            font-family: 'Teko', sans-serif; font-size: 1.3rem; font-weight: 700;
            padding: 2px 14px; border-radius: 6px; letter-spacing: 2px;
            text-transform: uppercase; margin-bottom: 10px;
        }
        h1 {
            font-family: 'Teko', sans-serif; font-size: 3.5rem; text-transform: uppercase;
            letter-spacing: 2px; line-height: 1; margin-bottom: 6px;
        }
        h1 span { color: var(--accent); }
        
        /* Search */
        .search-wrapper { position: relative; max-width: 600px; margin: 20px auto 10px; }
        .search-input {
            width: 100%; background: var(--bg-secondary); border: 2px solid var(--border-color);
            padding: 14px 18px; border-radius: 12px; color: #fff; font-size: 1rem;
            outline: none; transition: var(--transition);
        }
        .search-input:focus { border-color: var(--accent); box-shadow: 0 0 15px var(--accent-glow); }

        /* Navigation */
        .nav-tabs { display: flex; justify-content: center; gap: 8px; flex-wrap: wrap; margin-top: 15px; }
        .nav-tab {
            background: var(--bg-secondary); border: 1px solid var(--border-color);
            color: var(--text-main); padding: 8px 14px; border-radius: 8px;
            font-weight: 600; font-size: 0.85rem; text-decoration: none; transition: 0.2s;
        }
        .nav-tab:hover { background: var(--accent); color: #000; }

        /* Container & Cards */
        .container { max-width: 1200px; margin: 30px auto; padding: 0 16px; }
        section { margin-bottom: 40px; }
        .section-header {
            display: flex; align-items: center; gap: 10px; margin-bottom: 18px;
            border-bottom: 2px solid var(--border-color); padding-bottom: 10px;
        }
        .section-header h2 { font-family: 'Teko', sans-serif; font-size: 2.2rem; text-transform: uppercase; }

        .rules-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(320px, 1fr)); gap: 20px; }
        .rule-card {
            background: var(--bg-card); border: 1px solid var(--border-color);
            border-radius: 14px; padding: 22px; backdrop-filter: blur(10px);
            transition: transform 0.3s ease, box-shadow 0.3s ease;
            display: flex; flex-direction: column; justify-content: space-between;
        }
        .rule-card:hover { transform: translateY(-5px); box-shadow: 0 8px 25px rgba(0,0,0,0.5); }
        .rule-card.danger-border { border-left: 5px solid var(--danger); }
        .rule-card.warning-border { border-left: 5px solid var(--accent); }
        .rule-card.info-border { border-left: 5px solid var(--info); }

        .rule-title { font-size: 1.2rem; font-weight: 700; margin-bottom: 10px; display: flex; justify-content: space-between; align-items: center; }
        .penalty-badge { font-size: 0.7rem; padding: 3px 8px; border-radius: 6px; font-weight: 700; text-transform: uppercase; }
        .penalty-badge.warning { background: rgba(243, 156, 18, 0.15); color: var(--accent); border: 1px solid var(--accent); }
        .penalty-badge.danger { background: rgba(255, 71, 87, 0.15); color: var(--danger); border: 1px solid var(--danger); }

        /* Bans */
        .bans-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(180px, 1fr)); gap: 12px; margin-top: 15px; }
        .ban-item {
            background: rgba(255, 71, 87, 0.08); border: 1px solid rgba(255, 71, 87, 0.25);
            border-radius: 8px; padding: 10px; font-weight: 600; color: #ff8080; font-size: 0.85rem; text-align: center;
        }

        #scrollTopBtn {
            position: fixed; bottom: 20px; right: 20px; background: var(--accent);
            color: #000; border: none; width: 45px; height: 45px; border-radius: 50%;
            cursor: pointer; display: none; align-items: center; justify-content: center;
            font-weight: 900; z-index: 999; box-shadow: 0 4px 15px var(--accent-glow);
        }

        footer { text-align: center; padding: 25px; border-top: 1px solid var(--border-color); color: var(--text-muted); font-size: 0.85rem; }
    </style>
</head>
<body>

    <!-- Прелоадер на 3 секунды -->
    <div id="loader">
        <div class="spinner"></div>
        <h2 style="font-family:'Teko'; letter-spacing:2px; color:var(--accent);">U.C.L RULES LOADING...</h2>
    </div>

    <div id="progress-bar"></div>

    <header>
        <div class="hero-container">
            <div class="status-radar">
                <div id="radarDot" class="radar-dot"></div>
                <span id="radarStatusText" style="font-size:0.85rem; font-weight:700;">Проверка лиги...</span>
            </div>

            <div class="logo-badge">Official Regulations</div>
            <h1>Правила боёв <span>U.C.L</span></h1>
            
            <div class="search-wrapper">
                <input type="text" id="searchInput" class="search-input" placeholder="Поиск по регламенту (багоюз, ПД, слоу клики...)" oninput="handleSearch()">
            </div>

            <div class="nav-tabs">
                <a href="#pd" class="nav-tab">1. Пассив / ПД</a>
                <a href="#bugs" class="nav-tab">2. Багоюз</a>
                <a href="#combos" class="nav-tab">3. Медленные M1</a>
                <a href="#skating" class="nav-tab">4. С-кейтинг</a>
                <a href="#dd" class="nav-tab">5. Дабл деш</a>
                <a href="#audio" class="nav-tab">6. Звуки / Картинки</a>
                <a href="#title" class="nav-tab">7. Титульные бои</a>
                <a href="#combat" class="nav-tab">8. Регламент</a>
                <a href="#bans" class="nav-tab">9. Бан стили</a>
            </div>
        </div>
    </header>

    <main class="container">

        <section id="pd">
            <div class="section-header"><h2>1. Пассив и ПД Фишинг</h2></div>
            <div class="rules-grid">
                <div class="rule-card warning-border searchable">
                    <div class="rule-title">Суть ПД Фишинга <span class="penalty-badge warning">Ограничение</span></div>
                    <div class="rule-desc">Игрок намеренно прекращает бить/взаимодействовать для идеального уклонения. Разрешено сделать два уклона подряд только при стагеринге или под спам-комбо (особенно против медленных стилей). ПД-фиш разрешен, только если стамина бойца **ПОЛНОСТЬЮ на нуле**.</div>
                </div>
                <div class="rule-card warning-border searchable">
                    <div class="rule-title">Таймер порога (2.5 сек) <span class="penalty-badge warning">Фол за абуз</span></div>
                    <div class="rule-desc">Ждать удара можно максимум **2.5 секунды**. Незначительный выход — устное предупреждение, систематический злоупотребление — фол. Правило действует и на Демпси ролл. Использование эмоций = бездействие (кроме начала раунда). ПД-фиш 3+ раз первым дает фол даже внутри 2.5 сек.</div>
                </div>
                <div class="rule-card warning-border searchable">
                    <div class="rule-title">Сброс таймера и ульта <span class="penalty-badge danger">2 Фола</span></div>
                    <div class="rule-desc">Попытка удара, контрудар, атаки и способности, возвращающие бойцов в нейтрал, **сбрасывают 2.5-сек таймер**. Пассив или ПД-фиш в конце боя ради нанесения ультимейта караются **2 фолами**.</div>
                </div>
            </div>
        </section>

        <section id="bugs">
            <div class="section-header"><h2>2. Багоюз</h2></div>
            <div class="rules-grid">
                <div class="rule-card danger-border searchable">
                    <div class="rule-title">Парирование ульты <span class="penalty-badge danger">Дисквалификация</span></div>
                    <div class="rule-desc">Намеренный блок в тайминг при полете ультимейта, из-за чего ульта «сжирается» без урона. Намеренное использование влечет вылет из лиги.</div>
                </div>
                <div class="rule-card warning-border searchable">
                    <div class="rule-title">Нелегальный стаггеринг <span class="penalty-badge warning">Предупреждение ➔ Фол</span></div>
                    <div class="rule-desc">Удар M1 задерживается в серии, становится неуклоняемым и притягивает игрока обратно. Обычный стаггеринг (M1 для смены темпа/миксапов) полностью разрешен. Первое нарушение — устное предупреждение, далее — фол.</div>
                </div>
            </div>
        </section>

        <section id="combos">
            <div class="section-header"><h2>3. Медленные комбо М1 (Слоу клики)</h2></div>
            <div class="rules-grid">
                <div class="rule-card warning-border searchable">
                    <div class="rule-title">Лимит использования <span class="penalty-badge warning">Макс 1 серия</span></div>
                    <div class="rule-desc">Слоу клики разрешены **только после попадания под вражеский ультимейт**. Запрещено использовать после способностей (Focus, Stampede и др.). Разрешено использовать только для **ОДНОЙ СЕРИИ УДАРОВ**.</div>
                </div>
                <div class="rule-card info-border searchable">
                    <div class="rule-title">Исключения стилей <span class="penalty-badge warning">Особые правила</span></div>
                    <div class="rule-desc">Стилю **Крюк** запрещено делать слоу клики даже после ульты. После ультимейта **Айрон Фиста** разрешено делать **ДВА КОМБО** слоу клика.</div>
                </div>
            </div>
        </section>

        <section id="skating">
            <div class="section-header"><h2>4. С-кейтинг и бекдеши</h2></div>
            <div class="rules-grid">
                <div class="rule-card warning-border searchable">
                    <div class="rule-title">Правила ухода назад <span class="penalty-badge warning">Фол</span></div>
                    <div class="rule-desc">С-кейтинг (уход назад на S / джойстик назад) разрешен только после попадания удара/комбо по сопернику. Если идете назад, ничего не делая и пропуская 2 действия врага — **фол** (аналогично для бекдеша). Против Демпси фишить можно, а С-кейтить нельзя. Против Шотгана бекдеш на способность разрешен всегда.</div>
                </div>
                <div class="rule-card warning-border searchable">
                    <div class="rule-title">Дополнительный 3-сек счет <span class="penalty-badge warning">Фол обоим</span></div>
                    <div class="rule-desc">Если оба игрока намеренно держатся на дистанции, после порога 2.5 сек включается **3-секундный отсчет**. Если никто не сблизится — фол получают оба.</div>
                </div>
            </div>
        </section>

        <section id="dd">
            <div class="section-header"><h2>5. Дабл деш (ДД)</h2></div>
            <div class="rules-grid">
                <div class="rule-card danger-border searchable">
                    <div class="rule-title">ДД для спидстеров <span class="penalty-badge danger">Запрещено (Фол)</span></div>
                    <div class="rule-desc">Дабл деш подряд для уклона от финтов спидстерами строго запрещен — дается фол. Трипл деш запрещен полностью.</div>
                </div>
                <div class="rule-card info-border searchable">
                    <div class="rule-title">Разрешенный Дабл Деш <span class="penalty-badge warning">После 2 атак</span></div>
                    <div class="rule-desc">Два деша подряд официально разрешены исключительно **после совершения двух атак**.</div>
                </div>
            </div>
        </section>

        <section id="audio">
            <div class="section-header"><h2>6. Пользовательские звуки / изображения</h2></div>
            <div class="rules-grid">
                <div class="rule-card warning-border searchable">
                    <div class="rule-title">Звуки ПД <span class="penalty-badge warning">На усмотрение</span></div>
                    <div class="rule-desc">Кастомные звуки ПД разрешены, но судья может запросить их удаление, если они отвлекают соперника.</div>
                </div>
                <div class="rule-card danger-border searchable">
                    <div class="rule-title">Каунтеры и картинки <span class="penalty-badge danger">Строгий Бан</span></div>
                    <div class="rule-desc">Звуки контрударов (каунтер) и картинки **строго запрещены**. *Исключение:* звуки и картинки для ультимативных способностей (ульты) **разрешены**.</div>
                </div>
            </div>
        </section>

        <section id="title">
            <div class="section-header"><h2>7. Титульные бои</h2></div>
            <div class="rules-grid">
                <div class="rule-card info-border searchable">
                    <div class="rule-title">Формат и Рефери <span class="penalty-badge warning">Bo3</span></div>
                    <div class="rule-desc">Проводятся в формате **Bo3 (3 боя)**. Смена стиля возможна только после поражения. За боем наблюдают 3 рефери высшей категории (макс. 10 очков). Пассивный победитель с меньшим числом очков может проиграть по решению судей.</div>
                </div>
                <div class="rule-card info-border searchable">
                    <div class="rule-title">Сроки защиты титулов <span class="penalty-badge warning">Регламент</span></div>
                    <div class="rule-desc">
                        • **UNF:** Каждую неделю<br>
                        • **UNC:** Каждые 2 недели<br>
                        • **UCL:** Каждые 2.5 недели
                    </div>
                </div>
            </div>
        </section>

        <section id="combat">
            <div class="section-header"><h2>8. Общий регламент боёв</h2></div>
            <div class="rules-grid">
                <div class="rule-card info-border searchable">
                    <div class="rule-title">Вылеты и Судейство <span class="penalty-badge warning">5 минут</span></div>
                    <div class="rule-desc">При вылете дается **5 минут** на возврат (иначе ТКО/аннулирование). Вердикт судьи на ринге не обсуждается, но предвзятое судейство жестко карается после проверки.</div>
                </div>
                <div class="rule-card info-border searchable">
                    <div class="rule-title">Лимиты и Ранги <span class="penalty-badge warning">Топ-5</span></div>
                    <div class="rule-desc">Лимит: **не более 3 боев в сутки**. Для перехода в лигу выше нужен пояс и минимум 1 защита. Вызов чемпиону бросает **Топ-5**, а **Топ-1** имеет гарантированное право на бой.</div>
                </div>
            </div>
        </section>

        <section id="bans">
            <div class="section-header"><h2>9. Бан стили (Запрещены)</h2></div>
            <div class="bans-grid">
                <div class="ban-item searchable">Slugger</div>
                <div class="ban-item searchable">Hawk</div>
                <div class="ban-item searchable">Hammer</div>
                <div class="ban-item searchable">Dragonfish</div>
                <div class="ban-item searchable">White Ash</div>
                <div class="ban-item searchable">Wolf</div>
                <div class="ban-item searchable">Hitman</div>
                <div class="ban-item searchable">Shotgun</div>
                <div class="ban-item searchable">Corkscrew</div>
                <div class="ban-item searchable">Bullet</div>
                <div class="ban-item searchable">Chronos</div>
                <div class="ban-item searchable">All Shinies + Exclusive Styles</div>
            </div>
        </section>

    </main>

    <button id="scrollTopBtn" onclick="window.scrollTo({top:0, behavior:'smooth'})">↑</button>

    <footer>
        <p>Официальный регламент соревновательной лиги <span>U.C.L</span></p>
    </footer>

    <script>
        // Прелоадер ровно 3 секунды
        window.addEventListener('load', () => {
            setTimeout(() => {
                const loader = document.getElementById('loader');
                loader.style.opacity = '0';
                loader.style.visibility = 'hidden';
            }, 3000);
        });

        // Радар работы лиги (12:00 - 22:00 МСК)
        function checkLeagueStatus() {
            const now = new Date();
            // Перевод в UTC, затем в МСК (UTC+3)
            const utc = now.getTime() + (now.getTimezoneOffset() * 60000);
            const mskTime = new Date(utc + (3600000 * 3));
            
            const hours = mskTime.getHours();
            const dot = document.getElementById('radarDot');
            const text = document.getElementById('radarStatusText');

            if (hours >= 12 && hours < 22) {
                dot.className = 'radar-dot open';
                text.innerHTML = 'ЛИГА ОТКРЫТА (12:00 - 22:00 МСК)';
                text.style.color = 'var(--success)';
            } else {
                dot.className = 'radar-dot closed';
                text.innerHTML = 'ЛИГА ЗАКРЫТА (Открытие в 12:00 МСК)';
                text.style.color = 'var(--danger)';
            }
        }
        checkLeagueStatus();
        setInterval(checkLeagueStatus, 30000);

        // Поиск по сайту
        function handleSearch() {
            let val = document.getElementById('searchInput').value.toLowerCase();
            let cards = document.querySelectorAll('.searchable');
            cards.forEach(card => {
                let text = card.innerText.toLowerCase();
                card.style.display = text.includes(val) ? "" : "none";
            });
        }

        // Прогресс бар и кнопка наверх
        window.onscroll = function() {
            let winScroll = document.documentElement.scrollTop;
            let height = document.documentElement.scrollHeight - document.documentElement.clientHeight;
            document.getElementById("progress-bar").style.width = (winScroll / height) * 100 + "%";
            document.getElementById("scrollTopBtn").style.display = winScroll > 300 ? "flex" : "none";
        };
    </script>
</body>
</html>
