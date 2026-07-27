<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>U.C.L — Официальные Правила Боёв</title>
    <link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@400;500;600;700;800;900&family=Teko:wght@500;600;700&display=swap" rel="stylesheet">
    <style>
        :root {
            --bg-primary: #0a0c14;
            --bg-secondary: #121624;
            --bg-card: #181d2e;
            --bg-card-hover: #1f253d;
            --accent: #f39c12;
            --accent-glow: rgba(243, 156, 18, 0.3);
            --danger: #e74c3c;
            --danger-glow: rgba(231, 76, 60, 0.3);
            --success: #2ecc71;
            --info: #3498db;
            --text-main: #f0f3f8;
            --text-muted: #94a3b8;
            --border-color: #2a3450;
            --transition: all 0.3s ease;
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
            line-height: 1.6;
            overflow-x: hidden;
        }

        /* Header & Hero Section */
        header {
            position: relative;
            background: linear-gradient(135deg, rgba(18, 22, 36, 0.95), rgba(10, 12, 20, 0.98)), url('https://images.unsplash.com/photo-1542751371-adc38448a05e?auto=format&fit=crop&w=1920&q=80') center/cover no-repeat;
            border-bottom: 2px solid var(--accent);
            padding: 60px 20px 40px;
            text-align: center;
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
            font-size: 1.5rem;
            font-weight: 700;
            padding: 2px 20px;
            border-radius: 4px;
            margin-bottom: 15px;
            letter-spacing: 2px;
            text-transform: uppercase;
            box-shadow: 0 0 15px var(--accent-glow);
        }

        h1 {
            font-family: 'Teko', sans-serif;
            font-size: 4.5rem;
            text-transform: uppercase;
            letter-spacing: 3px;
            color: #fff;
            margin-bottom: 10px;
            line-height: 1;
            text-shadow: 0 5px 15px rgba(0,0,0,0.5);
        }

        h1 span {
            color: var(--accent);
        }

        .subtitle {
            font-size: 1.1rem;
            color: var(--text-muted);
            max-width: 700px;
            margin: 0 auto 30px;
        }

        /* Quick Navigation Tabs */
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
            border-radius: 6px;
            cursor: pointer;
            font-weight: 600;
            font-size: 0.95rem;
            transition: var(--transition);
            text-decoration: none;
        }

        .nav-tab:hover, .nav-tab.active {
            background: var(--accent);
            color: #000;
            border-color: var(--accent);
            box-shadow: 0 0 10px var(--accent-glow);
        }

        /* Main Container */
        .container {
            max-width: 1200px;
            margin: 40px auto;
            padding: 0 20px;
        }

        section {
            margin-bottom: 50px;
        }

        .section-header {
            display: flex;
            align-items: center;
            gap: 15px;
            margin-bottom: 25px;
            border-bottom: 2px solid var(--border-color);
            padding-bottom: 12px;
        }

        .section-header h2 {
            font-family: 'Teko', sans-serif;
            font-size: 2.5rem;
            letter-spacing: 2px;
            color: #fff;
            text-transform: uppercase;
        }

        .section-header .icon {
            font-size: 2rem;
        }

        /* Grid Layout for Rules */
        .rules-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(360px, 1fr));
            gap: 25px;
        }

        .rule-card {
            background: var(--bg-card);
            border: 1px solid var(--border-color);
            border-radius: 12px;
            padding: 25px;
            transition: var(--transition);
            position: relative;
            overflow: hidden;
            display: flex;
            flex-direction: column;
            justify-content: space-between;
        }

        .rule-card:hover {
            border-color: var(--accent);
            transform: translateY(-4px);
            box-shadow: 0 10px 25px rgba(0,0,0,0.4);
            background: var(--bg-card-hover);
        }

        .rule-card.danger-border {
            border-left: 4px solid var(--danger);
        }

        .rule-card.warning-border {
            border-left: 4px solid var(--accent);
        }

        .rule-card.info-border {
            border-left: 4px solid var(--info);
        }

        .rule-title {
            font-size: 1.35rem;
            font-weight: 700;
            color: #fff;
            margin-bottom: 12px;
            display: flex;
            align-items: center;
            justify-content: space-between;
            gap: 10px;
        }

        .penalty-badge {
            font-size: 0.75rem;
            padding: 3px 8px;
            border-radius: 4px;
            font-weight: 700;
            text-transform: uppercase;
            white-space: nowrap;
        }

        .penalty-badge.warning {
            background: rgba(243, 156, 18, 0.2);
            color: var(--accent);
            border: 1px solid var(--accent);
        }

        .penalty-badge.danger {
            background: rgba(231, 76, 60, 0.2);
            color: var(--danger);
            border: 1px solid var(--danger);
        }

        .rule-desc {
            font-size: 0.98rem;
            color: var(--text-muted);
            line-height: 1.65;
        }

        .rule-desc strong {
            color: var(--text-main);
        }

        /* Ban Styles List */
        .bans-container {
            background: var(--bg-card);
            border: 1px solid var(--border-color);
            border-radius: 12px;
            padding: 30px;
        }

        .bans-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(220px, 1fr));
            gap: 15px;
            margin-top: 20px;
        }

        .ban-item {
            background: rgba(231, 76, 60, 0.1);
            border: 1px solid rgba(231, 76, 60, 0.3);
            border-radius: 8px;
            padding: 12px 16px;
            font-weight: 600;
            color: #ff8080;
            display: flex;
            align-items: center;
            gap: 10px;
            transition: var(--transition);
        }

        .ban-item:hover {
            background: rgba(231, 76, 60, 0.2);
            border-color: var(--danger);
        }

        /* Tournament Combat Rules Cards */
        .combat-rules-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(340px, 1fr));
            gap: 25px;
        }

        /* Footer */
        footer {
            background: var(--bg-secondary);
            border-top: 1px solid var(--border-color);
            text-align: center;
            padding: 30px 20px;
            color: var(--text-muted);
            font-size: 0.9rem;
            margin-top: 60px;
        }

        footer span {
            color: var(--accent);
            font-weight: 700;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .rule-card {
            animation: fadeIn 0.5s ease forwards;
        }
    </style>
</head>
<body>

    <header>
        <div class="hero-container">
            <div class="logo-badge">Official Rules & Regulations</div>
            <h1>Правила боёв <span>U.C.L</span></h1>
            <p class="subtitle">Полный официальный свод соревновательного регламента лиги. Четкие требования, стандарты и наказания.</p>
            
            <div class="nav-tabs">
                <a href="#pd" class="nav-tab">ПД Фишинг</a>
                <a href="#bugs" class="nav-tab">Багоюз</a>
                <a href="#combos" class="nav-tab">Медленные M1</a>
                <a href="#skating" class="nav-tab">С-кейтинг & Бекдеши</a>
                <a href="#audio" class="nav-tab">Звуки / Эффекты</a>
                <a href="#combat" class="nav-tab">Проведение боёв</a>
                <a href="#bans" class="nav-tab">Бан-стили</a>
            </div>
        </div>
    </header>

    <main class="container">

        <!-- СЕКЦИЯ 1: ПД ФИШИНГ -->
        <section id="pd">
            <div class="section-header">
                <span class="icon">⏱️</span>
                <h2>1. ПД Фишинг (Пассивное уклонение)</h2>
            </div>
            <div class="rules-grid">
                <div class="rule-card warning-border">
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

                <div class="rule-card warning-border">
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

                <div class="rule-card warning-border">
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
        <section id="bugs">
            <div class="section-header">
                <span class="icon">🚫</span>
                <h2>2. Запрещенный багоюз</h2>
            </div>
            <div class="rules-grid">
                <div class="rule-card danger-border">
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

                <div class="rule-card danger-border">
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

                <div class="rule-card danger-border">
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
        <section id="combos">
            <div class="section-header">
                <span class="icon">🐢</span>
                <h2>3. Медленные комбо М1 (Слоу клики)</h2>
            </div>
            <div class="rules-grid">
                <div class="rule-card warning-border">
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

                <div class="rule-card info-border">
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
        <section id="skating">
            <div class="section-header">
                <span class="icon">⛸️</span>
                <h2>4. С-кейтинг, Бекдеши и ДД</h2>
            </div>
            <div class="rules-grid">
                <div class="rule-card warning-border">
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

                <div class="rule-card warning-border">
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
        <section id="audio">
            <div class="section-header">
                <span class="icon">🎨</span>
                <h2>5. Кастомные звуки и изображения</h2>
            </div>
            <div class="rules-grid">
                <div class="rule-card warning-border">
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

                <div class="rule-card danger-border">
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
        <section id="combat">
            <div class="section-header">
                <span class="icon">🏟️</span>
                <h2>6. Регламент проведения боёв U.C.L</h2>
            </div>
            <div class="combat-rules-grid">
                <div class="rule-card info-border">
                    <div>
                        <div class="rule-title">🌐 Проблемы со связью и вылеты</div>
                        <div class="rule-desc">
                            При обрыве соединения или вылете игры посреди матча включается таймер: у бойца есть ровно <strong>5 минут</strong> на возвращение. Если дедлайн нарушен — поединок аннулируется либо присуждается технический нокаут (ТКО) по решению рефери.
                        </div>
                    </div>
                </div>

                <div class="rule-card info-border">
                    <div>
                        <div class="rule-title">⚖️ Авторитет рефери</div>
                        <div class="rule-desc">
                            Вердикт судьи на ринге непререкаем и не обсуждается по ходу боя. Однако зафиксированные явные и грубые судейские ошибки после проверки будут строго караться администрацией лиги.
                        </div>
                    </div>
                </div>

                <div class="rule-card info-border">
                    <div>
                        <div class="rule-title">📅 Суточный лимит на поединки</div>
                        <div class="rule-desc">
                            Во избежание выгорания бойцов действует жесткий соревновательный лимит: один спортсмен имеет право провести <strong>не более 3 боёв за календарные сутки</strong>.
                        </div>
                    </div>
                </div>

                <div class="rule-card info-border">
                    <div>
                        <div class="rule-title">📈 Дивизионы и переходы</div>
                        <div class="rule-desc">
                            При аномальном доминировании администрация может принудительно поднять бойца выше. В стандартном порядке для легального перехода в другую лигу необходимо завоевать пояс и провести минимум 1 успешную защиту.
                        </div>
                    </div>
                </div>

                <div class="rule-card info-border">
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
        <section id="bans">
            <div class="section-header">
                <span class="icon">❌</span>
                <h2>7. Список бан-стилей</h2>
            </div>
            <div class="bans-container">
                <p style="color: var(--text-muted); margin-bottom: 15px;">К использованию на официальных боях U.C.L категорически запрещены следующие стили (включая все их шайни/блестящие вариации и эксклюзивные версии):</p>
                <div class="bans-grid">
                    <div class="ban-item">🥊 Слаггер (Slugger)</div>
                    <div class="ban-item">🦅 Хоук (Hawk)</div>
                    <div class="ban-item">🔄 Свитч Хит (Switch Hit)</div>
                    <div class="ban-item">🔨 Хаммер (Hammer)</div>
                    <div class="ban-item">🐟 Драгонфиш (Dragonfish)</div>
                    <div class="ban-item">⚡ Вайт Эш (White Ash)</div>
                    <div class="ban-item">🐺 Вульф (Wolf)</div>
                    <div class="ban-item">🌀 Крюк (без слоу кликов)</div>
                    <div class="ban-item">🎯 Буллет (Bullet)</div>
                    <div class="ban-item">⏳ Хронос (без эмоций)</div>
                </div>
            </div>
        </section>

    </main>

    <footer>
        <p>Официальный регламент лиги <span>U.C.L Combat Rules</span>. Разработано для турниров и матчей.</p>
    </footer>

</body>
</html>
