<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
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

        html, body {
            width: 100%;
            overflow-x: hidden;
        }

        body {
            font-family: 'Montserrat', sans-serif;
            background-color: var(--bg-primary);
            color: var(--text-main);
            line-height: 1.6;
            background-image: 
                radial-gradient(circle at 10% 20%, rgba(243, 156, 18, 0.05) 0%, transparent 40%),
                radial-gradient(circle at 90% 80%, rgba(30, 144, 255, 0.05) 0%, transparent 40%);
        }

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

        header {
            position: relative;
            background: linear-gradient(135deg, rgba(15, 19, 34, 0.95), rgba(7, 9, 19, 0.98)), url('https://images.unsplash.com/photo-1542751371-adc38448a05e?auto=format&fit=crop&w=1920&q=80') center/cover no-repeat;
            border-bottom: 3px solid var(--accent);
            padding: 40px 16px 30px;
            text-align: center;
            box-shadow: 0 10px 40px rgba(0,0,0,0.6);
            width: 100%;
        }

        .hero-container {
            max-width: 900px;
            margin: 0 auto;
            width: 100%;
        }

        .logo-badge {
            display: inline-block;
            background: var(--accent);
            color: #000;
            font-family: 'Teko', sans-serif;
            font-size: 1.3rem;
            font-weight: 700;
            padding: 2px 14px;
            border-radius: 6px;
            margin-bottom: 8px;
            letter-spacing: 2px;
            text-transform: uppercase;
            box-shadow: 0 0 20px var(--accent-glow);
        }

        h1 {
            font-family: 'Teko', sans-serif;
            font-size: 3rem;
            text-transform: uppercase;
            letter-spacing: 2px;
            color: #fff;
            margin-bottom: 6px;
            line-height: 1;
            text-shadow: 0 5px 25px rgba(0,0,0,0.7);
        }

        @media (min-width: 768px) {
            h1 {
                font-size: 4.5rem;
            }
            header {
                padding: 70px 20px 50px;
            }
        }

        h1 span {
            color: var(--accent);
            text-shadow: 0 0 30px var(--accent-glow);
        }

        .subtitle {
            font-size: 0.9rem;
            color: var(--text-muted);
            max-width: 700px;
            margin: 0 auto 20px;
            padding: 0 10px;
        }

        @media (min-width: 768px) {
            .subtitle {
                font-size: 1.1rem;
                margin-bottom: 30px;
            }
        }

        .search-wrapper {
            width: 100%;
            max-width: 100%;
            margin: 0 auto 15px;
            position: relative;
        }

        .search-input-container {
            position: relative;
            display: flex;
            align-items: center;
            width: 100%;
        }

        .search-icon {
            position: absolute;
            left: 18px;
            font-size: 1rem;
            color: var(--text-muted);
            pointer-events: none;
            z-index: 3;
        }

        .search-input {
            width: 100%;
            background: var(--bg-secondary);
            border: 2px solid var(--border-color);
            padding: 14px 18px 14px 48px;
            border-radius: 12px;
            color: #fff;
            font-size: 1rem;
            font-family: 'Montserrat', sans-serif;
            outline: none;
            box-shadow: inset 0 2px 5px rgba(0,0,0,0.3);
        }

        .search-input:focus {
            border-color: var(--accent);
            box-shadow: 0 0 20px var(--accent-glow);
        }

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
            max-height: 220px;
            overflow-y: auto;
            text-align: left;
            box-shadow: 0 15px 30px rgba(0,0,0,0.6);
        }

        .autocomplete-items div {
            padding: 10px 15px;
            cursor: pointer;
            color: var(--text-main);
            border-bottom: 1px solid var(--border-color);
            font-size: 0.88rem;
            display: flex;
            align-items: center;
            justify-content: space-between;
        }

        .autocomplete-items div small {
            color: var(--text-muted);
            font-size: 0.7rem;
            background: rgba(255,255,255,0.05);
            padding: 2px 6px;
            border-radius: 4px;
        }

        .nav-tabs {
            display: flex;
            justify-content: center;
            gap: 6px;
            flex-wrap: wrap;
            margin-top: 12px;
        }

        .nav-tab {
            background: var(--bg-secondary);
            border: 1px solid var(--border-color);
            color: var(--text-main);
            padding: 6px 12px;
            border-radius: 8px;
            cursor: pointer;
            font-weight: 600;
            font-size: 0.78rem;
            text-decoration: none;
            box-shadow: 0 4px 10px rgba(0,0,0,0.2);
        }

        .nav-tab:hover, .nav-tab.active {
            background: var(--accent);
            color: #000;
            border-color: var(--accent);
        }

        .container {
            max-width: 1200px;
            margin: 25px auto;
            padding: 0 16px;
            width: 100%;
        }

        @media (min-width: 768px) {
            .container {
                margin: 50px auto;
                padding: 0 20px;
            }
        }

        section {
            margin-bottom: 40px;
            width: 100%;
        }

        .section-header {
            display: flex;
            align-items: center;
            gap: 10px;
            margin-bottom: 18px;
            border-bottom: 2px solid var(--border-color);
            padding-bottom: 10px;
        }

        .section-header h2 {
            font-family: 'Teko', sans-serif;
            font-size: 1.8rem;
            letter-spacing: 1.5px;
            color: #fff;
            text-transform: uppercase;
        }

        @media (min-width: 768px) {
            .section-header h2 {
                font-size: 2.5rem;
            }
        }

        .section-header .icon {
            font-size: 1.4rem;
        }

        @media (min-width: 768px) {
            .section-header .icon {
                font-size: 2rem;
            }
        }

        .rules-grid, .combat-rules-grid {
            display: grid;
            grid-template-columns: 100%;
            gap: 15px;
            width: 100%;
        }

        @media (min-width: 768px) {
            .rules-grid, .combat-rules-grid {
                grid-template-columns: repeat(auto-fit, minmax(320px, 1fr));
                gap: 25px;
            }
        }

        .rule-card {
            background: var(--bg-card);
            border: 1px solid var(--border-color);
            border-radius: 12px;
            padding: 18px;
            width: 100%;
            word-wrap: break-word;
            overflow-wrap: break-word;
            box-shadow: 0 4px 15px rgba(0,0,0,0.3);
            display: flex;
            flex-direction: column;
            justify-content: space-between;
        }

        @media (min-width: 768px) {
            .rule-card {
                padding: 25px;
                border-radius: 14px;
            }
        }

        .rule-card.danger-border { border-left: 5px solid var(--danger); }
        .rule-card.warning-border { border-left: 5px solid var(--accent); }
        .rule-card.info-border { border-left: 5px solid var(--info); }

        .rule-title {
            font-size: 1.15rem;
            font-weight: 700;
            color: #fff;
            margin-bottom: 10px;
            display: flex;
            align-items: center;
            justify-content: space-between;
            gap: 8px;
            flex-wrap: wrap;
        }

        @media (min-width: 768px) {
            .rule-title {
                font-size: 1.35rem;
            }
        }

        .penalty-badge {
            font-size: 0.65rem;
            padding: 3px 8px;
            border-radius: 6px;
            font-weight: 700;
            text-transform: uppercase;
            white-space: nowrap;
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
            font-size: 0.88rem;
            color: var(--text-muted);
            line-height: 1.55;
        }

        @media (min-width: 768px) {
            .rule-desc {
                font-size: 0.95rem;
                line-height: 1.7;
            }
        }

        .rule-desc strong {
            color: var(--text-main);
            font-weight: 600;
        }

        .bans-container {
            background: var(--bg-card);
            border: 1px solid var(--border-color);
            border-radius: 12px;
            padding: 18px;
            width: 100%;
            box-shadow: 0 4px 15px rgba(0,0,0,0.3);
        }

        @media (min-width: 768px) {
            .bans-container {
                padding: 30px;
                border-radius: 14px;
            }
        }

        .bans-grid {
            display: grid;
            grid-template-columns: 100%;
            gap: 10px;
            margin-top: 12px;
            width: 100%;
        }

        @media (min-width: 550px) {
            .bans-grid {
                grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
                gap: 12px;
            }
        }

        .ban-item {
            background: rgba(255, 71, 87, 0.08);
            border: 1px solid rgba(255, 71, 87, 0.25);
            border-radius: 8px;
            padding: 10px 14px;
            font-weight: 600;
            color: #ff8080;
            display: flex;
            align-items: center;
            gap: 8px;
            font-size: 0.85rem;
            width: 100%;
        }

        #noResults {
            display: none;
            text-align: center;
            color: var(--text-muted);
            font-size: 1rem;
            padding: 25px;
            background: var(--bg-card);
            border-radius: 12px;
            border: 1px solid var(--border-color);
            margin-top: 15px;
        }

        #scrollTopBtn {
            position: fixed;
            bottom: 20px;
            right: 20px;
            background: var(--accent);
            color: #000;
            border: none;
            width: 40px;
            height: 40px;
            border-radius: 50%;
            font-size: 1rem;
            cursor: pointer;
            display: none;
            align-items: center;
            justify-content: center;
            box-shadow: 0 4px 15px var(--accent-glow);
            z-index: 999;
            font-weight: 900;
        }

        footer {
            background: var(--bg-secondary);
            border-top: 1px solid var(--border-color);
            text-align: center;
            padding: 20px 16px;
            color: var(--text-muted);
            font-size: 0.85rem;
            margin-top: 40px;
            width: 100%;
        }

        footer span {
            color: var(--accent);
            font-weight: 700;
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
            
            <div class="search-wrapper">
                <div class="search-input-container">
                    <span class="search-icon">🔍</span>
                    <input type="text" id="searchInput" class="search-input" placeholder="Поиск по правилам..." oninput="handleSearchInput()" onkeydown="handleSearchKeydown(event)">
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
                            Это когда игрок намеренно перестает бить или взаимодействовать, чтобы спровоцировать идеальное уклонение. Разрешено сделать два уклона подряд только в том случае, если вас поймали на стагеринге или вы находитесь в безвыходном положении под градом спамящих комбо.
                        </div>
                    </div>
                </div>

                <div class="rule-card warning-border searchable" data-keywords="таймер порог 2.5 секунды демпси ролл фол эмоции">
                    <div>
                        <div class="rule-title">
                            Таймер порога (2.5 сек)
                            <span class="penalty-badge warning">Злоупотребление = Фол</span>
                        </div>
                        <div class="rule-desc">
                            Ожидать удара разрешено максимум <strong>2.5 секунды</strong>. Незначительный выход за рамки карается предупреждением, а систематическое злоупотребление — фолом. Аналогичное правило действует и на демпси ролл. Использование эмоций приравнивается к попытке ПД.
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
                            Если после завершения таймера ПД-порога оба игрока намеренно продолжают держаться на дистанции, включается дополнительный 3-секундный счёт. Если никто из бойцов не начинает сближение за это время, фол присуждается обоим участникам матча.
                        </div>
                    </div>
                </div>
            </div>
        </section>

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
                            Ситуация, когда в вас летит ульта и по идее должна нанести урон, но игрок прожимает блок в специфический тайминг, из-за чего ультимейт «сжирается» без последствий.
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
                            Нарушением считается момент, когда удар M1 фиксируется в серии, но искусственно задерживается, становится неуклоняемым и притягивает оппонента обратно. Обычный тактический стаггеринг полностью разрешен.
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
                            Использование багов с залипанием атак, от которых физически нельзя увернуться (по типу смешей M2, M1+M2). Попытки их симуляции или поиска обходов караются регламентом.
                        </div>
                    </div>
                </div>
            </div>
        </section>

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
                            Медленные удары M1 разрешены <strong>только после того, как игрок попал под вражеский ультимейт</strong>. Их запрещено использовать после способностей и применять более чем для <strong>ОДНОЙ СЕРИИ УДАРОВ</strong>.
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
                            Бойцам со стилем «Крюк» запрещено использовать слоу клики даже после ультимейта соперника. После ультимейта стиля «Айрон Фист» разрешено выполнить ровно <strong>ДВА КОМБО</strong> слоу кликов.
                        </div>
                    </div>
                </div>
            </div>
        </section>

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
                            С-кейтинг — это отход назад от противника с зажатой клавишей S. Допускается после успешного удара. Если вы идете назад и пассивно ничего не делаете, пропуская два действия оппонента — фол.
                        </div>
                    </div>
                </div>

                <div class="rule-card warning-border searchable" data-keywords="дабл-деши дд спидстеры финты трипл деш бекдеш шотган любые обстоятельства">
                    <div>
                        <div class="rule-title">
                            Правила Дабл-дешей и Бекдешей
                            <span class="penalty-badge warning">Строгие лимиты</span>
                        </div>
                        <div class="rule-desc">
                            Два деша подряд для спидстеров (для уклонения от финтов) строго запрещены. Два деша после двух совершенных атак — разрешены. Тройной деш запрещен полностью. При любых обстоятельствах можно делать бекдеш от способности шотгана, даже если игрок до этого его делал.
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <section id="audio" class="rule-section">
            <div class="section-header">
                <span class="icon">🎨</span>
                <h2>5. Кастомные звуки и изображения</h2>
            </div>
            <div class="rules-grid">
                <div class="rule-card warning-border searchable" data-keywords="звуки пд отвлекающие эффекты судья кастомные">
                    <div>
                        <div class="rule-title">
                            Звуки ПД и эффекты
                            <span class="penalty-badge warning">На усмотрение судьи</span>
                        </div>
                        <div class="rule-desc">
                            Использование кастомных звуков ПД разрешено, но рефери может запросить их удаление, если они сильно отвлекают оппонента.
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
                            Пользовательские звуки контрударов и любые кастомные изображения запрещены. <em>Исключение:</em> кастомные звуки и изображения для ультимативных способностей разрешены.
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <section id="combat" class="rule-section">
            <div class="section-header">
                <span class="icon">🏟️</span>
                <h2>6. Регламент проведения боёв U.C.L</h2>
            </div>
            <div class="combat-rules-grid">
                <div class="rule-card info-border searchable" data-keywords="проблемы со связью вылеты 5 минут тко нокаут">
                    <div>
                        <div class="rule-title">🌐 Проблемы со связью и вылеты</div>
                        <div class="rule-desc">При обрыве связи у бойца есть ровно <strong>5 минут</strong> на возвращение, иначе присуждается технический нокаут (ТКО).</div>
                    </div>
                </div>

                <div class="rule-card info-border searchable" data-keywords="авторитет рефери судья вердикт ошибки">
                    <div>
                        <div class="rule-title">⚖️ Авторитет рефери</div>
                        <div class="rule-desc">Вердикт судьи на ринге непререкаем. Грубые судейские ошибки наказываются администрацией лиги после проверок.</div>
                    </div>
                </div>

                <div class="rule-card info-border searchable" data-keywords="суточный лимит поединки 3 боя календарные сутки">
                    <div>
                        <div class="rule-title">📅 Суточный лимит на поединки</div>
                        <div class="rule-desc">Один спортсмен имеет право провести <strong>не более 3 боёв за календарные сутки</strong>.</div>
                    </div>
                </div>

                <div class="rule-card info-border searchable" data-keywords="дивизионы переходы пояс защита">
                    <div>
                        <div class="rule-title">📈 Дивизионы и переходы</div>
                        <div class="rule-desc">Для легального перехода в другую лигу необходимо завоевать пояс и провести минимум 1 успешную защиту.</div>
                    </div>
                </div>

                <div class="rule-card info-border searchable" data-keywords="право вызов чемпион топ-5 топ-1 рейтинг">
                    <div>
                        <div class="rule-title">👑 Право на вызов чемпиона</div>
                        <div class="rule-desc">Бросить вызов чемпиону могут бойцы из Топ-5. Лидер рейтинга (Топ-1) имеет гарантированное право на бой.</div>
                    </div>
                </div>
            </div>
        </section>

        <section id="bans" class="rule-section">
            <div class="section-header">
                <span class="icon">❌</span>
                <h2>7. Список бан-стилей</h2>
            </div>
            <div class="bans-container">
                <p style="color: var(--text-muted); margin-bottom: 12px; font-size: 0.85rem;">К использованию на официальных боях U.C.L категорически запрещены следующие стили (включая все их вариации):</p>
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
        <p>Официальный регламент лиги <span>U.C.L Combat Rules</span>.</p>
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

                matches.slice(0, 6).forEach((match) => {
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

        function handleSearchKeydown(e) {
            let listContainer = document.getElementById('autocompleteList');
            let items = listContainer ? listContainer.getElementsByTagName('div') : [];

            if (e.keyCode === 40) {
                currentFocus++;
                addActive(items);
            } else if (e.keyCode === 38) {
                currentFocus--;
                addActive(items);
            } else if (e.keyCode === 13) {
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
