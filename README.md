<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>U.C.L — Официальные Правила Боёв</title>
    <link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@400;500;600;700;800;900&family=Teko:wght@500;600;700&display=swap" rel="stylesheet">
    <style>
        :root {
            --bg-primary: #070913;
            --bg-secondary: #0f1322;
            --bg-card: #151a2e;
            --bg-card-hover: #1c233d;
            --accent: #f39c12;
            --accent-glow: rgba(243, 156, 18, 0.4);
            --danger: #ff4757;
            --danger-glow: rgba(255, 71, 87, 0.4);
            --success: #2ed573;
            --info: #1e90ff;
            --text-main: #f1f5f9;
            --text-muted: #8b9bb4;
            --border-color: #232d4a;
            --transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }

        body {
            font-family: 'Montserrat', sans-serif;
            background-color: var(--bg-primary);
            color: var(--text-main);
            line-height: 1.7;
            overflow-x: hidden;
            background-image: 
                radial-gradient(circle at 10% 20%, rgba(243, 156, 18, 0.05) 0%, transparent 40%),
                radial-gradient(circle at 90% 80%, rgba(30, 144, 255, 0.05) 0%, transparent 40%);
        }

        /* Scroll Progress Bar */
        #progress-bar {
            position: fixed;
            top: 0;
            left: 0;
            height: 4px;
            background: var(--accent);
            width: 0%;
            z-index: 1000;
            box-shadow: 0 0 12px var(--accent);
            transition: width 0.1s ease-out;
        }

        /* Header & Hero */
        header {
            position: relative;
            background: linear-gradient(135deg, rgba(15, 19, 34, 0.95), rgba(7, 9, 19, 0.98)), url('https://images.unsplash.com/photo-1542751371-adc38448a05e?auto=format&fit=crop&w=1920&q=80') center/cover no-repeat;
            border-bottom: 3px solid var(--accent);
            padding: 80px 20px 60px;
            text-align: center;
            box-shadow: 0 10px 40px rgba(0,0,0,0.6);
        }

        .hero-container {
            max-width: 1000px;
            margin: 0 auto;
        }

        .logo-badge {
            display: inline-block;
            background: var(--accent);
            color: #000;
            font-family: 'Teko', sans-serif;
            font-size: 1.7rem;
            font-weight: 700;
            padding: 2px 24px;
            border-radius: 6px;
            margin-bottom: 15px;
            letter-spacing: 2px;
            text-transform: uppercase;
            box-shadow: 0 0 25px var(--accent-glow);
        }

        h1 {
            font-family: 'Teko', sans-serif;
            font-size: 5rem;
            text-transform: uppercase;
            letter-spacing: 3px;
            color: #fff;
            margin-bottom: 10px;
            line-height: 1;
            text-shadow: 0 5px 25px rgba(0,0,0,0.7);
        }

        h1 span {
            color: var(--accent);
            text-shadow: 0 0 30px var(--accent-glow);
        }

        .subtitle {
            font-size: 1.2rem;
            color: var(--text-muted);
            max-width: 750px;
            margin: 0 auto 40px;
        }

        /* Search Bar & Advanced Autocomplete */
        .search-wrapper {
            max-width: 540px;
            margin: 0 auto 25px;
            position: relative;
        }

        .search-input-container {
            position: relative;
            display: flex;
            align-items: center;
        }

        .search-icon {
            position: absolute;
            left: 20px;
            font-size: 1.2rem;
            color: var(--text-muted);
            pointer-events: none;
            z-index: 3;
            transition: var(--transition);
        }

        .search-input {
            width: 100%;
            background: var(--bg-secondary);
            border: 2px solid var(--border-color);
            padding: 16px 20px 16px 52px;
            border-radius: 12px;
            color: #fff;
            font-size: 1.05rem;
            font-family: 'Montserrat', sans-serif;
            transition: var(--transition);
            outline: none;
            box-shadow: inset 0 2px 5px rgba(0,0,0,0.3);
        }

        .search-input:focus {
            border-color: var(--accent);
            box-shadow: 0 0 20px var(--accent-glow), inset 0 2px 5px rgba(0,0,0,0.3);
        }

        .search-input:focus + .search-icon {
            color: var(--accent);
        }

        /* Suggestions dropdown list */
        .autocomplete-items {
            position: absolute;
            border: 1px solid var(--border-color);
            border-top: none;
            z-index: 99;
            top: 100%;
            left: 0;
            right: 0;
            background: var(--bg-secondary);
            border-radius: 0 0 12px 12px;
            max-height: 250px;
            overflow-y: auto;
            text-align: left;
            box-shadow: 0 15px 30px rgba(0,0,0,0.6);
            backdrop-filter: blur(10px);
        }

        .autocomplete-items div {
            padding: 13px 22px;
            cursor: pointer;
            color: var(--text-main);
            border-bottom: 1px solid var(--border-color);
            font-size: 0.95rem;
            transition: var(--transition);
            display: flex;
            align-items: center;
            justify-content: space-between;
        }

        .autocomplete-items div span {
            color: var(--text-muted);
            font-size: 0.8rem;
            background: rgba(255,255,255,0.05);
            padding: 2px 8px;
            border-radius: 4px;
        }

        .autocomplete-items div:last-child {
            border-bottom: none;
        }

        .autocomplete-items div:hover, .autocomplete-items div.autocomplete-active {
            background: var(--bg-card-hover);
            color: var(--accent);
            padding-left: 26px;
        }

        /* Navigation Tabs */
        .nav-tabs {
            display: flex;
            justify-content: center;
            gap: 12px;
            flex-wrap: wrap;
            margin-top: 25px;
        }

        .nav-tab {
            background: var(--bg-secondary);
            border: 1px solid var(--border-color);
            color: var(--text-main);
            padding: 10px 20px;
            border-radius: 10px;
            cursor: pointer;
            font-weight: 600;
            font-size: 0.92rem;
            transition: var(--transition);
            text-decoration: none;
            box-shadow: 0 4px 10px rgba(0,0,0,0.2);
        }

        .nav-tab:hover, .nav-tab.active {
            background: var(--accent);
            color: #000;
            border-color: var(--accent);
            box-shadow: 0 0 20px var(--accent-glow);
            transform: translateY(-3px);
        }

        /* Container */
        .container {
            max-width: 1200px;
            margin: 60px auto;
            padding: 0 20px;
        }

        section {
            margin-bottom: 65px;
            transition: all 0.4s ease;
        }

        .section-header {
            display: flex;
            align-items: center;
            gap: 15px;
            margin-bottom: 30px;
            border-bottom: 2px solid var(--border-color);
            padding-bottom: 15px;
        }

        .section-header h2 {
            font-family: 'Teko', sans-serif;
            font-size: 2.8rem;
            letter-spacing: 2px;
            color: #fff;
            text-transform: uppercase;
        }

        .section-header .icon {
            font-size: 2.3rem;
        }

        /* Grid Cards */
        .rules-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(360px, 1fr));
            gap: 28px;
        }

        .rule-card {
            background: var(--bg-card);
            border: 1px solid var(--border-color);
            border-radius: 16px;
            padding: 30px;
            transition: var(--transition);
            position: relative;
            overflow: hidden;
            display: flex;
            flex-direction: column;
            justify-content: space-between;
            box-shadow: 0 6px 25px rgba(0,0,0,0.35);
        }

        .rule-card:hover {
            border-color: var(--accent);
            transform: translateY(-8px);
            box-shadow: 0 15px 35px rgba(0,0,0,0.55), 0 0 15px rgba(243, 156, 18, 0.1);
            background: var(--bg-card-hover);
        }

        .rule-card.danger-border {
            border-left: 6px solid var(--danger);
        }

        .rule-card.warning-border {
            border-left: 6px solid var(--accent);
        }

        .rule-card.info-border {
            border-left: 6px solid var(--info);
        }

        .rule-title {
            font-size: 1.45rem;
            font-weight: 700;
            color: #fff;
            margin-bottom: 15px;
            display: flex;
            align-items: center;
            justify-content: space-between;
            gap: 12px;
        }

        .penalty-badge {
            font-size: 0.75rem;
            padding: 5px 12px;
            border-radius: 6px;
            font-weight: 700;
            text-transform: uppercase;
            white-space: nowrap;
            letter-spacing: 0.5px;
        }

        .penalty-badge.warning {
            background: rgba(243, 156, 18, 0.15);
            color: var(--accent);
            border: 1px solid rgba(243, 156, 18, 0.4);
        }

        .penalty-badge.danger {
            background: rgba(255, 71, 87, 0.15);
            color: var(--danger);
            border: 1px solid rgba(255, 71, 87, 0.4);
        }

        .rule-desc {
            font-size: 1rem;
            color: var(--text-muted);
            line-height: 1.75;
        }

        .rule-desc strong {
            color: var(--text-main);
            font-weight: 600;
        }

        /* Ban Styles Grid */
        .bans-container {
            background: var(--bg-card);
            border: 1px solid var(--border-color);
            border-radius: 16px;
            padding: 40px;
            box-shadow: 0 6px 25px rgba(0,0,0,0.35);
        }

        .bans-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(240px, 1fr));
            gap: 18px;
            margin-top: 20px;
        }

        .ban-item {
            background: rgba(255, 71, 87, 0.08);
            border: 1px solid rgba(255, 71, 87, 0.25);
            border-radius: 12px;
            padding: 16px 20px;
            font-weight: 600;
            color: #ff8080;
            display: flex;
            align-items: center;
            gap: 12px;
            transition: var(--transition);
        }

        .ban-item:hover {
            background: rgba(255, 71, 87, 0.18);
            border-color: var(--danger);
            transform: translateX(6px);
            box-shadow: 0 0 15px var(--danger-glow);
        }

        .combat-rules-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(340px, 1fr));
            gap: 28px;
        }

        /* No Results Message */
        #noResults {
            display: none;
            text-align: center;
            color: var(--text-muted);
            font-size: 1.3rem;
            padding: 50px;
            background: var(--bg-card);
            border-radius: 16px;
            border: 1px solid var(--border-color);
            margin-top: 20px;
        }

        /* Scroll to Top Button */
        #scrollTopBtn {
            position: fixed;
            bottom: 35px;
            right: 35px;
            background: var(--accent);
            color: #000;
            border: none;
            width: 50px;
            height: 50px;
            border-radius: 50%;
            font-size: 1.3rem;
            cursor: pointer;
            display: none;
            align-items: center;
            justify-content: center;
            box-shadow: 0 6px 20px var(--accent-glow);
            transition: var(--transition);
            z-index: 999;
            font-weight: 900;
        }

        #scrollTopBtn:hover {
            transform: scale(1.15) translateY(-3px);
            background: #ffa502;
            box-shadow: 0 10px 25px var(--accent-glow);
        }

        /* Footer */
        footer {
            background: var(--bg-secondary);
            border-top: 1px solid var(--border-color);
            text-align: center;
            padding: 40px 20px;
            color: var(--text-muted);
            font-size: 0.98rem;
            margin-top: 80px;
        }

        footer span {
            color: var(--accent);
            font-weight: 700;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .rule-card {
            animation: fadeIn 0.5s ease forwards;
        }
    </style>
</head>
<body>

    <div id="progress-bar"></div>

    <header>
        <div class="hero-container">
            <div class="logo-badge">Official Rules & Regulations</div>
            <h1>Правила боёв <span>U.C.L</span></h1>
            <p class="subtitle">Единый официальный свод соревновательного регламента лиги. Четкие требования, стандарты и система наказаний.</p>
            
            <div class="search-wrapper" autocomplete="off">
                <div class="search-input-container">
                    <span class="search-icon">🔍</span>
                    <input type="text" id="searchInput" class="search-input" placeholder="Поиск по правилам (например: фишинг, ульта, деш)..." oninput="handleSearchInput()" onkeydown="handleSearchKeydown(event)">
                </div>
                <div id="autocompleteList" class="autocomplete-items"></div>
            </div>

            <div class="nav-tabs">
                <a href="#pd" class="nav-tab">ПД Фишинг</a>
                <a href="#bugs" class="nav-tab">Багоюз</a>
                <a href="#combos" class="nav-tab">Медленные M1</a>
                <a href="#skating" class="nav-tab">С-кейтинг</a>
                <a href="#audio" class="nav-tab">Звуки</a>
                <a href="#combat" class="nav-tab">Бои</a>
                <a href="#bans" class="nav-tab">Бан-стили</a>
            </div>
        </div>
    </header>

    <main class="container">

        <div id="noResults">Ничего не найдено по вашему запросу 😕 Попробуйте изменить ключевые слова.</div>

        <!-- СЕКЦИЯ 1: ПД ФИШИНГ -->
        <section id="pd" class="rule-section">
            <div class="section-header">
                <span class="icon">⏱️</span>
                <h2>1. ПД Фишинг (Пассивное уклонение)</h2>
            </div>
            <div class="rules-grid">
                <div class="rule-card warning-border searchable" data-keywords="пд фишинг уклонение пассивное удары таймер">
                    <div>
                        <div class="rule-title">
                            Суть ПД Фишинга
                            <span class="penalty-badge warning">Фол / Предупреждение</span>
                        </div>
                        <div class="rule-desc">
                            Это когда игрок намеренно перестает бить или взаимодействовать, чтобы спровоцировать идеальное уклонение. Разрешено сделать два уклона подряд только в том случае, если вас поймали на стагеринге или вы находитесь в безвыходном положении под градом спамящих комбо (особенно актуально против медленных стилей).
                        </div>
                    </div>
                </div>

                <div class="rule-card warning-border searchable" data-keywords="таймер порог 2.5 секунды демпси ролл фол эмоции">
                    <div>
                        <div class="rule-title">
                            Таймер порога (2.5 секунды)
                            <span class="penalty-badge warning">Злоупотребление = Фол</span>
                        </div>
                        <div class="rule-desc">
                            Ожидать удара разрешено максимум <strong>2.5 секунды</strong>. Незначительный выход за рамки карается предупреждением, а систематическое злоупотребление — фолом. Аналогичное правило действует и на демпси ролл. Таймер сбрасывается попыткой удара с получением контрудара, атакой или способностями возврата в нейтраль. Использование эмоций (кроме старта раунда) приравнивается к попытке ПД.
                        </div>
                    </div>
                </div>

                <div class="rule-card warning-border searchable" data-keywords="контроль дистанции фол обоим демпси с-кейтинг бекдеш шотган">
                    <div>
                        <div class="rule-title">
                            Контроль дистанции
                            <span class="penalty-badge warning">Фол обоим</span>
                        </div>
                        <div class="rule-desc">
                            Если после завершения таймера ПД-порога оба игрока намеренно продолжают держаться на дистанции, включается дополнительный 3-секундный счёт. Если никто из бойцов не начинает сближение за это время, фол присуждается обоим участникам матча. Против демпси разрешено фишить, но запрещено уходить назад (с-кейтить). Против шотгана можно использовать бекдеш на способность, если перед этим был совершен обычный бекдеш.
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <!-- СЕКЦИЯ 2: БАГОЮЗ -->
        <section id="bugs" class="rule-section">
            <div class="section-header">
                <span class="icon">🚫</span>
                <h2>2. Запрещенный багоюз</h2>
            </div>
            <div class="rules-grid">
                <div class="rule-card danger-border searchable" data-keywords="парирование ультимейта ульта блок баг дисквалификация">
                    <div>
                        <div class="rule-title">
                            Парирование ультимейта
                            <span class="penalty-badge danger">Дисквалификация</span>
                        </div>
                        <div class="rule-desc">
                            Ситуация, когда в вас летит ульта и по идее должна нанести урон, но игрок прожимает блок в специфический тайминг, из-за чего ультимейт «сжирается» без последствий. Намеренное использование карается вылетом из реальной жизни / жестким баном.
                        </div>
                    </div>
                </div>

                <div class="rule-card danger-border searchable" data-keywords="нелегальный стаггеринг удар m1 серия предупреждение фол">
                    <div>
                        <div class="rule-title">
                            Нелегальный стаггеринг
                            <span class="penalty-badge warning">Предупреждение ➔ Фол</span>
                        </div>
                        <div class="rule-desc">
                            Нарушением считается момент, когда удар M1 фиксируется в серии, но искусственно задерживается, становится неуклоняемым и притягивает оппонента обратно вопреки кадрам уклонения. <em>Примечание:</em> обычный тактический стаггеринг (тычки M1 для перебивания атаки, смены темпа или миксапов) полностью разрешен. Первое нарушение нелегального стаггеринга — устное предупреждение, далее — фолы.
                        </div>
                    </div>
                </div>

                <div class="rule-card danger-border searchable" data-keywords="залипающие комбо смеши m2 m1+m2 баги">
                    <div>
                        <div class="rule-title">
                            Залипающие комбо (Смеши)
                            <span class="penalty-badge danger">Запрещено</span>
                        </div>
                        <div class="rule-desc">
                            Использование багов с залипанием атак, от которых физически нельзя увернуться (по типу смешей M2, M1+M2). Данные уязвимости движка уже официально устранены разработчиками игры, но попытки их симуляции или поиска обходов караются регламентом.
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <!-- СЕКЦИЯ 3: МЕДЛЕННЫЕ КОМБО М1 -->
        <section id="combos" class="rule-section">
            <div class="section-header">
                <span class="icon">🐢</span>
                <h2>3. Медленные комбо М1 (Слоу клики)</h2>
            </div>
            <div class="rules-grid">
                <div class="rule-card warning-border searchable" data-keywords="слоу клики медленные m1 ультимейт фол серия">
                    <div>
                        <div class="rule-title">
                            Регламент слоу кликов
                            <span class="penalty-badge warning">Лимит: 1 серия</span>
                        </div>
                        <div class="rule-desc">
                            Медленные удары M1 разрешены <strong>только после того, как игрок попал под вражеский ультимейт</strong>. Их категорически запрещено использовать после использования способностей (Focus, Stampede и т.д.). Кроме того, слоу клики разрешено применять ровно для <strong>ОДНОЙ СЕРИИ УДАРОВ</strong> — большее количество расценивается как нарушение и ведет к фолу.
                        </div>
                    </div>
                </div>

                <div class="rule-card info-border searchable" data-keywords="исключения стили крюк айрон фист слоу клики комбо">
                    <div>
                        <div class="rule-title">
                            Исключения для стилей
                            <span class="penalty-badge warning">Баланс стилей</span>
                        </div>
                        <div class="rule-desc">
                            Существуют индивидуальные ограничения по стилям: бойцам со стилем «Крюк» запрещено использовать слоу клики даже после ультимейта соперника. В то же время, после ультимейта стиля «Айрон Фист» бойцу разрешено выполнить ровно <strong>ДВА КОМБО</strong> слоу кликов.
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <!-- СЕКЦИЯ 4: С-КЕЙТИНГ И БЕКДЕШИ -->
        <section id="skating" class="rule-section">
            <div class="section-header">
                <span class="icon">⛸️</span>
                <h2>4. С-кейтинг, Бекдеши и ДД</h2>
            </div>
            <div class="rules-grid">
                <div class="rule-card warning-border searchable" data-keywords="с-кейтинг пассивный отход назад клавиша s фол бекдеши">
                    <div>
                        <div class="rule-title">
                            С-кейтинг и пассивный отход
                            <span class="penalty-badge warning">Фол</span>
                        </div>
                        <div class="rule-desc">
                            С-кейтинг — это отход назад от противника с зажатой клавишей S (направление джойстика назад). Допускается сразу после успешного попадания удара или комбо по сопернику. Однако, если вы идете назад и пассивно ничего не делаете, пропуская два действия оппонента подряд — вы получаете фол. Аналогичное правило применяется к бекдешам.
                        </div>
                    </div>
                </div>

                <div class="rule-card warning-border searchable" data-keywords="дабл-деши дд спидстеры финты трипл деш">
                    <div>
                        <div class="rule-title">
                            Правила Дабл-дешей (ДД)
                            <span class="penalty-badge warning">Строгие лимиты</span>
                        </div>
                        <div class="rule-desc">
                            Понятие делится на две категории: <strong>1)</strong> Два деша подряд для спидстеров, используемые для уклонения от финтов — строго запрещены, дается фол. <strong>2)</strong> Два деша после двух совершенных атак — разрешены. Тройной деш (трипл деш) запрещен полностью в любых ситуациях.
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <!-- СЕКЦИЯ 5: ПОЛЬЗОВАТЕЛЬСКИЕ ЗВУКИ И ИЗОБРАЖЕНИЯ -->
        <section id="audio" class="rule-section">
            <div class="section-header">
                <span class="icon">🎨</span>
                <h2>5. Кастомные звуки и изображения</h2>
            </div>
            <div class="rules-grid">
                <div class="rule-card warning-border searchable" data-keywords="звуки пд отвлекающие эффекты судья кастомные">
                    <div>
                        <div class="rule-title">
                            Звуки ПД и отвлекающие эффекты
                            <span class="penalty-badge warning">На усмотрение судьи</span>
                        </div>
                        <div class="rule-desc">
                            Использование кастомных звуковых эффектов идеального уклонения (ПД) остается на усмотрение самих игроков. Тем не менее, рефери может в любой момент запросить их удаление, если сочтет, что они создают нечестное преимущество за счет сильного отвлечения внимания оппонента.
                        </div>
                    </div>
                </div>

                <div class="rule-card danger-border searchable" data-keywords="каунтеры картинки звуки изображения ультимативные способности ульты">
                    <div>
                        <div class="rule-title">
                            Каунтеры и картинки
                            <span class="penalty-badge danger">Запрещено</span>
                        </div>
                        <div class="rule-desc">
                            Пользовательские звуковые эффекты контрударов (каунтер), а также любые кастомные изображения строго запрещены регламентом и подлежат обязательному удалению перед началом официальных матчей. <em>Исключение:</em> кастомные звуки и изображения для ультимативных способностей (ульт) полностью разрешены.
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <!-- СЕКЦИЯ 6: ПРАВИЛА ПРОВЕДЕНИЯ БОЕВ U.C.L -->
        <section id="combat" class="rule-section">
            <div class="section-header">
                <span class="icon">🏟️</span>
                <h2>6. Регламент проведения боёв U.C.L</h2>
            </div>
            <div class="combat-rules-grid">
                <div class="rule-card info-border searchable" data-keywords="проблемы со связью вылеты 5 минут тко нокаут">
                    <div>
                        <div class="rule-title">🌐 Проблемы со связью и вылеты</div>
                        <div class="rule-desc">
                            При обрыве соединения или вылете игры посреди матча включается таймер: у бойца есть ровно <strong>5 минут</strong> на возвращение. Если дедлайн нарушен — поединок аннулируется либо присуждается технический нокаут (ТКО) по решению рефери.
                        </div>
                    </div>
                </div>

                <div class="rule-card info-border searchable" data-keywords="авторитет рефери судья вердикт ошибки">
                    <div>
                        <div class="rule-title">⚖️ Авторитет рефери</div>
                        <div class="rule-desc">
                            Вердикт судьи на ринге непререкаем и не обсуждается по ходу боя. Однако зафиксированные явные и грубые судейские ошибки после проверки будут строго караться администрацией лиги.
                        </div>
                    </div>
                </div>

                <div class="rule-card info-border searchable" data-keywords="суточный лимит поединки 3 боя календарные сутки">
                    <div>
                        <div class="rule-title">📅 Суточный лимит на поединки</div>
                        <div class="rule-desc">
                            Во избежание выгорания бойцов действует жесткий соревновательный лимит: один спортсмен имеет право провести <strong>не более 3 боёв за календарные сутки</strong>.
                        </div>
                    </div>
                </div>

                <div class="rule-card info-border searchable" data-keywords="дивизионы переходы пояс защита">
                    <div>
                        <div class="rule-title">📈 Дивизионы и переходы</div>
                        <div class="rule-desc">
                            При аномальном доминировании администрация может принудительно поднять бойца выше. В стандартном порядке для легального перехода в другую лигу необходимо завоевать пояс и провести минимум 1 успешную защиту.
                        </div>
                    </div>
                </div>

                <div class="rule-card info-border searchable" data-keywords="право вызов чемпион топ-5 топ-1 рейтинг">
                    <div>
                        <div class="rule-title">👑 Право на вызов чемпиона</div>
                        <div class="rule-desc">
                            Бросить вызов действующему чемпиону разрешено только бойцам из первой пятерки (Топ-5) рейтинга. Лидер таблицы (Топ-1) обладает эксклюзивным правом: чемпион обязан принять его вызов безоговорочно.
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <!-- СЕКЦИЯ 7: БАН СТИЛИ -->
        <section id="bans" class="rule-section">
            <div class="section-header">
                <span class="icon">❌</span>
                <h2>7. Список бан-стилей</h2>
            </div>
            <div class="bans-container">
                <p style="color: var(--text-muted); margin-bottom: 15px;">К использованию на официальных боях U.C.L категорически запрещены следующие стили (включая все их шайни/блестящие вариации и эксклюзивные версии):</p>
                <div class="bans-grid">
                    <div class="ban-item searchable" data-keywords="слаггер slugger бан-стиль">🥊 Слаггер (Slugger)</div>
                    <div class="ban-item searchable" data-keywords="хоук hawk бан-стиль">🦅 Хоук (Hawk)</div>
                    <div class="ban-item searchable" data-keywords="свитч хит switch hit бан-стиль">🔄 Свитч Хит (Switch Hit)</div>
                    <div class="ban-item searchable" data-keywords="хаммер hammer бан-стиль">🔨 Хаммер (Hammer)</div>
                    <div class="ban-item searchable" data-keywords="драгонфиш dragonfish бан-стиль">🐟 Драгонфиш (Dragonfish)</div>
                    <div class="ban-item searchable" data-keywords="вайт эш white ash бан-стиль">⚡ Вайт Эш (White Ash)</div>
                    <div class="ban-item searchable" data-keywords="вульф wolf бан-стиль">🐺 Вульф (Wolf)</div>
                    <div class="ban-item searchable" data-keywords="крюк слоу клики бан-стиль">🌀 Крюк (без слоу кликов)</div>
                    <div class="ban-item searchable" data-keywords="буллет bullet бан-стиль">🎯 Буллет (Bullet)</div>
                    <div class="ban-item searchable" data-keywords="хронос эмоции бан-стиль">⏳ Хронос (без эмоций)</div>
                </div>
            </div>
        </section>

    </main>

    <button id="scrollTopBtn" onclick="scrollToTop()">↑</button>

    <footer>
        <p>Официальный регламент лиги <span>U.C.L Combat Rules</span>. Разработано для турниров и матчей.</p>
    </footer>

    <script>
        const suggestionsData = [
            { title: "ПД Фишинг", category: "Пассивное уклонение" },
            { title: "Таймер порога", category: "Пассивное уклонение" },
            { title: "Контроль дистанции", category: "Пассивное уклонение" },
            { title: "Парирование ультимейта", category: "Багоюз" },
            { title: "Нелегальный стаггеринг", category: "Багоюз" },
            { title: "Залипающие комбо (Смеши)", category: "Багоюз" },
            { title: "Слоу клики", category: "Медленные M1" },
            { title: "Исключения для стилей", category: "Медленные M1" },
            { title: "С-кейтинг", category: "С-кейтинг" },
            { title: "Дабл-деши (ДД)", category: "С-кейтинг" },
            { title: "Звуки ПД", category: "Кастомные звуки" },
            { title: "Каунтеры и картинки", category: "Кастомные звуки" },
            { title: "Проблемы со связью", category: "Регламент боёв" },
            { title: "Авторитет рефери", category: "Регламент боёв" },
            { title: "Суточный лимит", category: "Регламент боёв" },
            { title: "Дивизионы и переходы", category: "Регламент боёв" },
            { title: "Вызов чемпиона", category: "Регламент боёв" },
            { title: "Слаггер", category: "Бан-стили" },
            { title: "Хоук", category: "Бан-стили" },
            { title: "Свитч Хит", category: "Бан-стили" },
            { title: "Хаммер", category: "Бан-стили" },
            { title: "Драгонфиш", category: "Бан-стили" },
            { title: "Вайт Эш", category: "Бан-стили" },
            { title: "Вульф", category: "Бан-стили" },
            { title: "Крюк", category: "Бан-стили" },
            { title: "Буллет", category: "Бан-стили" },
            { title: "Хронос", category: "Бан-стили" }
        ];

        let currentFocus = -1;

        function handleSearchInput() {
            let inputField = document.getElementById('searchInput');
            let inputVal = inputField.value.trim().toLowerCase();
            let listContainer = document.getElementById('autocompleteList');
            listContainer.innerHTML = "";
            currentFocus = -1;

            let cards = document.querySelectorAll('.searchable');
            let sections = document.querySelectorAll('.rule-section');
            let noResults = document.getElementById('noResults');
            let visibleCount = 0;

            cards.forEach(card => {
                let text = card.innerText.toLowerCase();
                let keywords = card.getAttribute('data-keywords') || "";
                if (inputVal === "" || text.includes(inputVal) || keywords.includes(inputVal)) {
                    card.style.display = "";
                    visibleCount++;
                } else {
                    card.style.display = "none";
                }
            });

            sections.forEach(section => {
                let visibleCardsInSec = section.querySelectorAll('.searchable:not([style*="display: none"])');
                if (visibleCardsInSec.length === 0) {
                    section.style.display = "none";
                } else {
                    section.style.display = "";
                }
            });

            if (visibleCount === 0 && inputVal !== "") {
                noResults.style.display = "block";
            } else {
                noResults.style.display = "none";
            }

            if (inputVal.length > 0) {
                let matches = suggestionsData.filter(item => 
                    item.title.toLowerCase().includes(inputVal) || item.category.toLowerCase().includes(inputVal)
                );

                matches.slice(0, 6).forEach((match, index) => {
                    let div = document.createElement('div');
                    div.innerHTML = `<span>${match.title}</span> <small>${match.category}</small>`;
                    div.onclick = function() {
                        inputField.value = match.title;
                        listContainer.innerHTML = "";
                        handleSearchInput();
                    };
                    listContainer.appendChild(div);
                });
            }
        }

        // Управление клавиатурой в выпадающем списке (стрелочки вверх/вниз и Enter)
        function handleSearchKeydown(e) {
            let listContainer = document.getElementById('autocompleteList');
            let items = listContainer ? listContainer.getElementsByTagName('div') : [];

            if (e.keyCode === 40) { // Стрелка вниз
                currentFocus++;
                addActive(items);
            } else if (e.keyCode === 38) { // Стрелка вверх
                currentFocus--;
                addActive(items);
            } else if (e.keyCode === 13) { // Enter
                e.preventDefault();
                if (currentFocus > -1 && items[currentFocus]) {
                    items[currentFocus].click();
                }
            }
        }

        function addActive(items) {
            if (!items) return false;
            removeActive(items);
            if (currentFocus >= items.length) currentFocus = 0;
            if (currentFocus < 0) currentFocus = (items.length - 1);
            items[currentFocus].classList.add("autocomplete-active");
            items[currentFocus].scrollIntoView({ block: 'nearest' });
        }

        function removeActive(items) {
            for (let i = 0; i < items.length; i++) {
                items[i].classList.remove("autocomplete-active");
            }
        }

        document.addEventListener('click', function(e) {
            if (!e.target.closest('.search-wrapper')) {
                document.getElementById('autocompleteList').innerHTML = "";
            }
        });

        window.onscroll = function() {
            let winScroll = document.body.scrollTop || document.documentElement.scrollTop;
            let height = document.documentElement.scrollHeight - document.documentElement.clientHeight;
            let scrolled = (winScroll / height) * 100;
            document.getElementById("progress-bar").style.width = scrolled + "%";

            let btn = document.getElementById("scrollTopBtn");
            if (winScroll > 300) {
                btn.style.display = "flex";
            } else {
                btn.style.display = "none";
            }
        };

        function scrollToTop() {
            window.scrollTo({top: 0, behavior: 'smooth'});
        }
    </script>

</body>
</html>
