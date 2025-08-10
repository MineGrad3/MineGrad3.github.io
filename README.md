<!doctype html>
<html lang="ru">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>MineGrad — Город возможностей</title>
  <meta name="description" content="MineGrad — роллплей сервер Minecraft. Подай заявку в вайтлист и начни свою историю. Дальше = больше." />
  <link rel="icon" href="data:;base64,iVBORw0KGgo=" />
  <link rel="apple-touch-icon" sizes="180x180" href="/apple-touch-icon.png">
  <link rel="icon" type="image/png" sizes="32x32" href="/favicon-32x32.png">
  <link rel="icon" type="image/png" sizes="16x16" href="/favicon-16x16.png">
  <link rel="manifest" href="/site.webmanifest">

  <!-- font (kept) -->
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600;800&display=swap" rel="stylesheet">

  <style>
    :root{
      --bg1:#07021a;
      --bg2:#1a0830;
      --accent1:#7c3aed; /* purple */
      --accent2:#5b21b6; /* deep purple */
      --muted:rgba(255,255,255,0.88);
      --muted-2:rgba(255,255,255,0.74);
      --card: rgba(255,255,255,0.04);
      --glass: rgba(255,255,255,0.04);
      --glass-2: rgba(255,255,255,0.03);
      --glass-strong: rgba(255,255,255,0.06);
    }

    *{box-sizing:border-box}
    html,body{height:100%}
    body{
      margin:0;
      font-family: 'Inter', system-ui, -apple-system, 'Segoe UI', Roboto, 'Helvetica Neue', Arial;
      color:var(--muted);
      background:
        radial-gradient(1200px 600px at 10% 10%, rgba(124,58,237,0.12), transparent),
        linear-gradient(180deg,var(--bg1),var(--bg2));
      -webkit-font-smoothing:antialiased;
      -moz-osx-font-smoothing:grayscale;
      -webkit-tap-highlight-color: transparent;
    }

    /* container responsive padding */
    .container{max-width:1100px;margin:40px auto;padding:28px}

    header{display:flex;align-items:center;justify-content:space-between;gap:16px}
    .brand{display:flex;align-items:center;gap:12px}

    /* logo with subtle animation */
    .logo{width:64px;height:64px;border-radius:14px;background:linear-gradient(135deg,var(--accent1),var(--accent2));display:flex;align-items:center;justify-content:center;font-weight:800;color:white;font-size:20px;box-shadow:0 10px 30px rgba(91,33,182,0.18);overflow:hidden;position:relative}
    .logo img{width:70px;height:70px;object-fit:cover;border-radius:10px;transform-origin:center;transition:transform .5s cubic-bezier(.2,.9,.2,1);} 
    .logo:hover img{transform:scale(1.03) rotate(-3deg)}

    h1{margin:0;font-size:22px}
    .tag{font-size:13px;color:var(--muted-2)}

    nav{display:flex;gap:10px}
    .btn{background:linear-gradient(90deg,var(--accent1),var(--accent2));padding:10px 16px;border-radius:10px;color:white;font-weight:600;text-decoration:none;display:inline-block;position:relative;overflow:hidden}
    .btn::after{content:'';position:absolute;inset:0;background:linear-gradient(90deg,rgba(255,255,255,0.06),transparent);mix-blend-mode:overlay;opacity:.6}
    .btn:hover{transform:translateY(-3px);box-shadow:0 12px 30px rgba(91,33,182,0.18);}
    .btn.ghost{background:transparent;border:1px solid rgba(255,255,255,0.06);color:var(--muted)}

    main{margin-top:26px}
    .hero{display:grid;grid-template-columns:1fr 540px;gap:28px;align-items:center}
    .eyebrow{display:inline-block;background:linear-gradient(90deg,#2d1366,#6b3bd1);padding:6px 10px;border-radius:999px;font-size:13px;color:white;font-weight:700}

    /* animated gradient text for headline */
    .big{font-size:44px;line-height:1.02;margin:12px 0;font-weight:800;background:linear-gradient(90deg,#fff,#bdb0ff,#fff);-webkit-background-clip:text;background-clip:text;color:transparent;position:relative}
    @keyframes hueShift{from{background-position:0% 50%}to{background-position:100% 50%}}
    .big{background-size:200% 200%;animation:hueShift 6s linear infinite}

    .lead{color:var(--muted-2);font-size:16px}

    .features{display:grid;grid-template-columns:repeat(2,1fr);gap:12px;margin-top:18px}
    .pill{background:var(--card);padding:12px;border-radius:10px;font-weight:600;transition:transform .28s ease, box-shadow .28s ease;min-width:0;white-space:normal;word-break:break-word}
    .pill:hover{transform:translateY(-6px);box-shadow:0 18px 40px rgba(2,6,23,0.6)}

    /* card base + glassy hover */
    .card{border-radius:16px;overflow:hidden;background:linear-gradient(180deg, rgba(255,255,255,0.02), rgba(255,255,255,0.01));box-shadow:0 10px 30px rgba(2,6,23,0.6);border:1px solid rgba(255,255,255,0.03)}

    /* gallery: responsive aspect ratio */
    .gallery{background:#000;position:relative;display:flex;align-items:center;justify-content:center;overflow:hidden;border-radius:12px}
    .gallery img{width:100%;height:100%;object-fit:cover;display:block;transition:opacity .7s ease, transform .7s cubic-bezier(.2,.9,.2,1);opacity:1}
    .gallery img.fade-out{opacity:0;transform:scale(1.02) translateY(-6px)}
    .gallery .overlay{position:absolute;inset:0;background:linear-gradient(180deg,transparent,rgba(2,6,23,0.6) 65%)}
    .gallery .meta{position:absolute;left:18px;bottom:18px;background:rgba(0,0,0,0.35);backdrop-filter:blur(6px);padding:10px;border-radius:10px}

    .controls{display:flex;align-items:center;justify-content:space-between;padding:10px}
    .small-btn{background:rgba(255,255,255,0.03);border:1px solid rgba(255,255,255,0.04);padding:8px 10px;border-radius:8px;color:var(--muted);cursor:pointer}

    /* progress bar under gallery */
    .progress-wrap{height:4px;background:transparent;border-radius:999px;overflow:hidden;margin-top:6px}
    .progress{height:100%;width:0%;background:linear-gradient(90deg,var(--accent1),var(--accent2));transition:width .25s linear}

    /* dots */
    .dots{display:flex;gap:8px;align-items:center}
    .dot{width:9px;height:9px;border-radius:50%;background:rgba(255,255,255,0.06);cursor:pointer}
    .dot.active{background:linear-gradient(90deg,var(--accent1),var(--accent2));box-shadow:0 6px 18px rgba(91,33,182,0.16)}

    /* sections */
    section{margin-top:22px}
    .grid3{display:grid;grid-template-columns:repeat(3,1fr);gap:12px}
    .card-blur{padding:18px;border-radius:12px;background:linear-gradient(180deg, rgba(255,255,255,0.02), rgba(255,255,255,0.01));border:1px solid rgba(255,255,255,0.03);transition:transform .28s ease,box-shadow .28s ease}
    .card-blur:hover{transform:translateY(-6px);box-shadow:0 18px 40px rgba(2,6,23,0.45)}

    /* rules */
    .rules{display:grid;grid-template-columns:repeat(2,1fr);gap:18px}
    .rules h3{margin-top:0}
    ul.rules-list{padding-left:18px;margin:8px 0}

    /* law tabs */
    .law-tabs{display:flex;gap:10px;margin-bottom:12px}
    .law-btn{padding:8px 12px;border-radius:10px;background:rgba(255,255,255,0.03);border:1px solid rgba(255,255,255,0.04);cursor:pointer;font-weight:700;display:inline-flex;align-items:center;gap:10px}
    .law-btn.active{background:linear-gradient(90deg,var(--accent1),var(--accent2));color:white;box-shadow:0 12px 30px rgba(91,33,182,0.12)}
    .law-panel{display:none;animation:fadeIn .28s ease both}
    .law-panel.active{display:block}
    @keyframes fadeIn{from{opacity:0;transform:translateY(6px)}to{opacity:1;transform:translateY(0)}}

    /* accordion (mobile) */
    @media (max-width:1000px){
      .law-tabs{display:block}
      .law-btn{width:100%;justify-content:space-between}
      .law-btn .chev{display:inline-block;transition:transform .18s ease}
      .law-btn[aria-expanded="true"] .chev{transform:rotate(180deg)}
      .law-panel{display:none;padding:12px 0;border-top:1px solid rgba(255,255,255,0.03)}
      .law-panel.active{display:block}
    }

    /* actions grid (section 'Что делать') */
    .actions-grid{display:grid;grid-template-columns:repeat(3,1fr);gap:12px;margin-top:12px}

    /* socials */
    .socials{display:flex;gap:10px;flex-wrap:wrap}
    .socials a{display:inline-flex;align-items:center;gap:8px;padding:8px 12px;border-radius:10px;text-decoration:none;font-weight:700;transition:transform .18s ease, box-shadow .18s ease}
    .socials a svg{width:16px;height:16px;opacity:0.95}
    .socials a:hover{transform:translateY(-4px);box-shadow:0 14px 36px rgba(2,6,23,0.5)}
    .yt{background:#ff3b3b;color:white}
    .tt{background:#111;color:white}
    .vk{background:#4a76a8;color:white}
    .tg{background:linear-gradient(90deg,#6b3bd1,#2a64d6);color:white}
    .donate{background:linear-gradient(90deg,#10b981,#059669);color:white}

    footer{margin-top:38px;text-align:center;color:rgba(255,255,255,0.44);font-size:13px;padding-bottom:30px}

    /* responsive tweaks for phones */
    @media (max-width:1000px){
      .hero{grid-template-columns:1fr}
      /* gallery becomes responsive using aspect-ratio and max-height on phones */
      .gallery{aspect-ratio:16/9;height:auto;max-height:48vh}
      .gallery img{height:100%}
      .grid3{grid-template-columns:1fr}
      .rules{grid-template-columns:1fr}
      .law-tabs{flex-wrap:wrap}
      .actions-grid{grid-template-columns:1fr}
      .card{border-radius:12px}
      .card-blur{padding:14px}
      .container{padding:18px;margin:18px auto}
    }

    /* even smaller phones */
    @media (max-width:420px){
      .big{font-size:28px}
      .logo{width:52px;height:52px}
      .logo img{width:54px;height:54px}
      header{flex-direction:column;align-items:flex-start;gap:8px}
      nav{width:100%;display:flex;gap:8px}
      .btn{flex:1;padding:10px;font-size:14px}
      .tag{font-size:12px}
      .pill{font-size:14px;padding:10px}
      .socials a{flex:1 1 auto;justify-content:center}
      .gallery{max-height:38vh}
    }

    /* reduce motion */
    @media (prefers-reduced-motion: reduce){
      .big, .logo img, .pill, .card-blur, .btn, .gallery img{animation:none;transition:none}
    }
  </style>
</head>
<body>
  <div class="container">
    <header>
      <div class="brand">
        <div class="logo" title="MineGrad logo">
         <img src="android-chrome-512x512.png" alt="MineGrad logo" width="70" height="70">
        </div>
        <div>
          <h1>MineGrad</h1>
          <div class="tag">Город возможностей. Играй. РП. Живи.</div>
        </div>
      </div>

      <nav aria-label="main">
        <a class="btn" href="#apply">Подать заявку</a>
        <a class="btn ghost" href="#discord">Discord</a>
      </nav>
    </header>

    <main>
      <section class="hero">
        <div>
          <div class="eyebrow">MineGrad</div>
          <h2 class="big">MineGrad — город возможностей.</h2>
          <p class="lead">Представь мир, где каждое утро начинается на оживлённой остановке — с гидом рядом и навигатором в телефоне. Здесь у тебя есть работа, дом, друзья и враги — и всё это влияет на судьбу города. Заходи сейчас — и помни: <strong>дальше = больше</strong>.</p>

          <div class="features">
            <div class="pill">Реалистичный городской спавн и вводный гид</div>
            <div class="pill">Фракции: полиция, военные, медики, СМИ</div>
            <div class="pill">Уникальная рыбалка и экономика без Pay-to-Win</div>
            <div class="pill">Покупка жилья через NPC и карьерные профессии</div>
          </div>

          <div style="margin-top:16px;display:flex;gap:10px;flex-wrap:wrap">
            <a class="btn" href="#apply">Подать заявку в вайтлист</a>
            <a class="btn ghost" href="#discord" style="margin-left:0">Вступить в Discord</a>
          </div>

          <p style="margin-top:12px;color:rgba(255,255,255,0.6);font-size:13px">Важно: для захода на сервер обязательно подать заявку и дождаться добавления в вайтлист через Discord.</p>
        </div>

        <div class="card">
          <div class="gallery" id="gallery" aria-live="polite">
            <!-- single-image approach with crossfade on change (keeps repo paths intact) -->
            <img id="gimg" src="https://images.unsplash.com/photo-1517248135467-4c7edcad34c4?auto=format&fit=crop&w=1600&q=80" alt="MineGrad screenshot" loading="lazy">
            <div class="overlay"></div>
            <div class="meta">
              <div style="font-weight:800">MineGrad — вид города</div>
              <div style="font-size:12px;color:rgba(255,255,255,0.7)">Скриншоты сервера.</div>
            </div>
          </div>

          <div class="controls">
            <div style="display:flex;gap:8px;align-items:center">
              <button class="small-btn" id="prevBtn" aria-label="Previous">⟨</button>
              <div class="dots" id="dots"></div>
              <button class="small-btn" id="nextBtn" aria-label="Next">⟩</button>
            </div>
            <div style="text-align:right">
              <div style="font-size:13px;color:rgba(255,255,255,0.7)" id="gmeta">Скрин 1 из 4</div>
              <div class="progress-wrap"><div class="progress" id="gprogress"></div></div>
            </div>
          </div>
        </div>
      </section>

      <section class="grid3">
        <div class="card-blur">
          <h4>Игровая экономика</h4>
          <p style="margin-top:8px;color:rgba(255,255,255,0.75);font-size:14px">Стабильная модель: донат — косметика, а не преимущества. Профессии и торговля влияют на развитие персонажа.</p>
        </div>
        <div class="card-blur">
          <h4>Фракции и сюжет</h4>
          <p style="margin-top:8px;color:rgba(255,255,255,0.75);font-size:14px">Фракции развиваются силами игроков — ваша активность формирует политическую и криминальную карту города.</p>
        </div>
        <div class="card-blur">
          <h4>Механики и плагины</h4>
          <p style="margin-top:8px;color:rgba(255,255,255,0.75);font-size:14px">BetonQuests, NPC-покупки, паспортная система — всё уже работает, а в будущем будет ещё глубже.</p>
        </div>
      </section>

      <section>
        <div class="card-blur">
          <h3>Что делать на сервере</h3>
          <div class="actions-grid">
            <div class="pill" style="background:var(--glass)">Купить квартиру и открыть бизнес</div>
            <div class="pill" style="background:var(--glass)">Устроиться на работу: водитель, доставщик, полицейский</div>
            <div class="pill" style="background:var(--glass)">Участвовать в ивентах и влиять на сюжет</div>
          </div>
        </div>
      </section>

      <section class="card-blur" id="rules" style="margin-top:18px">
        <h3>📜 Официальные правила MineGrad</h3>
        <div class="rules" style="margin-top:12px">
          <!-- rules content unchanged -->
          <div>
            <h4>1️⃣ Общие правила</h4>
            <ul class="rules-list">
              <li>Уважай других игроков — без оскорблений, угроз и провокаций.</li>
              <li>Запрещены любые читы, баги, дюпы и сторонние программы.</li>
              <li>Без мата, спама, чрезмерного капса и рекламы других серверов.</li>
              <li>РП-игра обязательна — соблюдай атмосферу города.</li>
              <li>Незнание правил не освобождает от ответственности. Обход наказаний запрещён.</li>
            </ul>
          </div>

          <div>
            <h4>2️⃣ Игровые имена и скины</h4>
            <ul class="rules-list">
              <li>Ник не должен содержать оскорблений, рекламы или мата.</li>
              <li>RP-имена — реалистичные: <strong>Имя Фамилия</strong>.</li>
              <li>Скины должны соответствовать сеттингу, запрещена экстремистская символика.</li>
              <li>При работе во фракции — форма обязательна.</li>
            </ul>
          </div>

          <div>
            <h4>3️⃣ Взаимодействие с миром</h4>
            <ul class="rules-list">
              <li>Гриферство запрещено — не ломай чужое и не порти город.</li>
              <li>Чат — для общения по игре, без оффтопа и спама.</li>
              <li>Запрещено злоупотреблять игровыми механиками (баги экономики, PvP и т.д.).</li>
            </ul>
          </div>

          <div>
            <h4>4️⃣ Фракции и конфликты</h4>
            <ul class="rules-list">
              <li>Конфликты только в рамках РП — без атак без причины.</li>
              <li>Каждая фракция выполняет свою роль, смена — только через РП.</li>
              <li>Нейтральные игроки не вмешиваются в разборки.</li>
              <li>Полиция и военные проводят аресты по закону.</li>
            </ul>
          </div>

          <!-- responsive accordion/tabs -->
          <div style="grid-column:1 / -1">
            <h4>5️⃣ Законы города MineGrad</h4>

            <div class="law-tabs" role="tablist" aria-label="Законы города">
              <button class="law-btn active" data-target="criminal" role="tab" aria-selected="true" aria-expanded="false">🔴 Уголовные преступления <span class="chev">▾</span></button>
              <button class="law-btn" data-target="administrative" role="tab" aria-selected="false" aria-expanded="false">🟡 Административные нарушения <span class="chev">▾</span></button>
            </div>

            <div id="criminal" class="law-panel active" role="tabpanel">
              <p style="font-weight:700;margin:6px 0">🔴 Уголовные преступления:</p>
              <ul class="rules-list">
                <li>Убийство без причины — 30 минут тюрьмы.</li>
                <li>Ограбление (при поимке) — 20 минут тюрьмы + штраф.</li>
                <li>Нападение на полицейского/военного — 40 минут тюрьмы.</li>
                <li>Попытка госпереворота — пожизненное заключение.</li>
              </ul>
            </div>

            <div id="administrative" class="law-panel" role="tabpanel" aria-hidden="true">
              <p style="font-weight:700;margin:6px 0">🟡 Административные нарушения:</p>
              <ul class="rules-list">
                <li>Оскорбления/провокации — штраф или 10 минут КПЗ.</li>
                <li>Незаконное проникновение — 15 минут тюрьмы.</li>
                <li>Вандализм (грифинг) — бан от 3 дней до перманента.</li>
              </ul>
            </div>

          </div>
        </div>
      </section>

      <section style="margin-top:18px;display:flex;gap:18px;align-items:flex-start;flex-wrap:wrap">
        <div style="flex:1;min-width:260px" class="card-blur">
          <h4>Соцсети MineGrad</h4>
          <p style="margin-top:6px;color:rgba(255,255,255,0.75);font-size:14px">Подписывайся, подавай заявку и следи за ивентами.</p>
          <div style="margin-top:12px" class="socials">
            <a class="yt" href="https://www.youtube.com/@MineGradOfficial" target="_blank" rel="noopener"> <!-- YouTube -->
              <svg viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" aria-hidden="true"><path d="M23 7a3 3 0 0 0-2.1-2.15C19.4 4.5 12 4.5 12 4.5s-7.4 0-8.9.35A3 3 0 0 0 1 7v10a3 3 0 0 0 2.1 2.15C4.6 19.5 12 19.5 12 19.5s7.4 0 8.9-.35A3 3 0 0 0 23 17V7z" fill="white" opacity="0.12"/><path d="M10 15V9l5 3-5 3z" fill="white"/></svg>
              YouTube
            </a>
            <a class="tt" href="https://www.tiktok.com/@minegrad" target="_blank" rel="noopener"> <!-- TikTok -->
              <svg viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" aria-hidden="true"><path d="M9 3v7.5A4.5 4.5 0 1 0 13.5 15H15a6 6 0 1 1 0 12v-5.25A9 9 0 1 1 9 3z" fill="white" opacity="0.12"/></svg>
              TikTok
            </a>
            <a class="vk" href="https://vk.com/club217846754" target="_blank" rel="noopener"> <!-- VK -->
              <svg viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" aria-hidden="true"><path d="M2 2h20v20H2z" fill="white" opacity="0.06"/></svg>
              ВКонтакте
            </a>
            <a class="tg" href="https://t.me/minegradofficial" target="_blank" rel="noopener"> <!-- Telegram -->
              <svg viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" aria-hidden="true"><path d="M2 12l8-4 6 5-9 5-5-6z" fill="white" opacity="0.12"/></svg>
              Telegram
            </a>
            <a class="donate" href="#donate">Поддержать проект</a>
          </div>
        </div>

        <div style="flex:1;min-width:260px" class="card-blur">
          <h4>Как зайти на сервер</h4>
          <ol style="margin-top:8px;color:rgba(255,255,255,0.78);font-size:14px">
            <li>Вступи в наш Discord.</li>
            <li>Подай заявку на вайтлист в специальном канале.</li>
            <li>Дождись подтверждения — тебя добавят и пришлют IP сервера.</li>
          </ol>
          <p style="margin-top:8px;color:rgba(255,255,255,0.62);font-size:13px">Важно: вход на сервер доступен только после подтверждения в вайтлисте.</p>
        </div>
      </section>

      <footer>
        © MineGrad — проект развивается. Помни: <strong>дальше = больше</strong>.
      </footer>

    </main>
  </div>

  <script>
    // gallery logic with crossfade, progress and controls (unchanged)
    const gallery = [
      'images/screen1.png',
      'images/screen3.png',
      'images/screen4.png',
      'images/screen5.png',
      'images/screen6.png',
    ];

    let idx = 0;
    const img = document.getElementById('gimg');
    const meta = document.getElementById('gmeta');
    const progress = document.getElementById('gprogress');
    const dotsWrap = document.getElementById('dots');
    const nextBtn = document.getElementById('nextBtn');
    const prevBtn = document.getElementById('prevBtn');

    // build dots
    for(let i=0;i<gallery.length;i++){
      const d = document.createElement('div');
      d.className='dot'+(i===0?' active':'');
      d.dataset.i = i;
      d.addEventListener('click', ()=>{ goTo(parseInt(d.dataset.i)); resetTimer(); });
      dotsWrap.appendChild(d);
    }

    function setActiveDot(i){
      const dots = dotsWrap.children;
      for(let j=0;j<dots.length;j++) dots[j].classList.toggle('active', j===i);
    }

    function update(){
      // crossfade: fade out -> change src -> fade in
      img.classList.add('fade-out');
      setTimeout(()=>{
        img.src = gallery[idx];
        img.onload = ()=>{
          img.classList.remove('fade-out');
        };
        meta.innerText = `Скрин ${idx+1} из ${gallery.length}`;
        setActiveDot(idx);
        progress.style.width = '0%';
      },220);
    }

    function next(){ idx = (idx + 1) % gallery.length; update(); }
    function prev(){ idx = (idx - 1 + gallery.length) % gallery.length; update(); }
    function goTo(i){ idx = ((i % gallery.length)+gallery.length)%gallery.length; update(); }

    nextBtn.addEventListener('click', ()=>{ next(); resetTimer(); });
    prevBtn.addEventListener('click', ()=>{ prev(); resetTimer(); });

    // keyboard support
    document.addEventListener('keydown', (e)=>{
      if(e.key === 'ArrowRight') { next(); resetTimer(); }
      if(e.key === 'ArrowLeft') { prev(); resetTimer(); }
    });

    // pause on hover/touch
    let hovering = false;
    const galleryEl = document.getElementById('gallery');
    galleryEl.addEventListener('mouseenter', ()=>{ hovering = true; });
    galleryEl.addEventListener('mouseleave', ()=>{ hovering = false; });
    galleryEl.addEventListener('touchstart', ()=>{ hovering = true; }, {passive:true});
    galleryEl.addEventListener('touchend', ()=>{ hovering = false; }, {passive:true});

    // auto-rotate with visual progress
    const ROTATE_MS = 6000;
    let autoTimer = null;
    function startTimer(){
      let start = Date.now();
      progress.style.transition = 'width 100ms linear';
      autoTimer = setInterval(()=>{
        if(hovering) { start = Date.now(); progress.style.width='0%'; return; }
        const elapsed = Date.now() - start;
        const pct = Math.min(100, (elapsed / ROTATE_MS) * 100);
        progress.style.width = pct + '%';
        if(elapsed >= ROTATE_MS){ next(); start = Date.now(); progress.style.width='0%'; }
      }, 120);
    }
    function resetTimer(){ clearInterval(autoTimer); startTimer(); }

    // init
    update();
    startTimer();

    // accessibility: ensure reduced-motion honored
    const mediaQuery = window.matchMedia('(prefers-reduced-motion: reduce)');
    if(mediaQuery.matches){ clearInterval(autoTimer); progress.style.display='none'; }

    // prefetch other images to make transitions smoother (non-blocking)
    gallery.forEach((s,i)=>{ if(i===0) return; const im = new Image(); im.src = s; });

    // small UX: when user clicks links to anchors, smooth scroll
    document.querySelectorAll('a[href^="#"]').forEach(a=>{
      a.addEventListener('click', (e)=>{
        const target = a.getAttribute('href');
        if(target.length>1){
          e.preventDefault();
          const el = document.querySelector(target);
          if(el) el.scrollIntoView({behavior:'smooth', block:'start'});
        }
      });
    });

    // LAW TABS / ACCORDION logic
    function setupLawControls(){
      const buttons = Array.from(document.querySelectorAll('.law-btn'));
      const panels = Array.from(document.querySelectorAll('.law-panel'));

      function activateTab(btn){
        buttons.forEach(b=>{ b.classList.toggle('active', b===btn); b.setAttribute('aria-selected', b===btn); b.setAttribute('aria-expanded', 'false'); });
        panels.forEach(p=>{ p.classList.toggle('active', p.id===btn.dataset.target); p.setAttribute('aria-hidden', p.id===btn.dataset.target? 'false':'true'); });
        // mark expanded only for mobile (handled later)
      }

      // initial state: desktop tab active for criminal
      activateTab(buttons[0]);

      buttons.forEach(btn=>{
        btn.addEventListener('click', ()=>{
          const isMobile = window.matchMedia('(max-width:1000px)').matches;
          const targetId = btn.dataset.target;
          const panel = document.getElementById(targetId);

          if(isMobile){
            // accordion behavior: toggle clicked panel; close others
            const wasOpen = panel.classList.contains('active');
            panels.forEach(p=>{ p.classList.remove('active'); p.setAttribute('aria-hidden','true'); });
            buttons.forEach(b=>{ b.classList.remove('active'); b.setAttribute('aria-expanded','false'); b.setAttribute('aria-selected','false'); });
            if(!wasOpen){
              panel.classList.add('active');
              panel.setAttribute('aria-hidden','false');
              btn.classList.add('active');
              btn.setAttribute('aria-expanded','true');
              btn.setAttribute('aria-selected','true');
            }
          } else {
            // tab behavior
            activateTab(btn);
          }
        });
      });

      // on resize: if switching modes, ensure sensible default
      let lastMobile = window.matchMedia('(max-width:1000px)').matches;
      window.addEventListener('resize', ()=>{
        const nowMobile = window.matchMedia('(max-width:1000px)').matches;
        if(nowMobile !== lastMobile){
          lastMobile = nowMobile;
          if(nowMobile){
            // collapse all by default on mobile
            panels.forEach(p=>{ p.classList.remove('active'); p.setAttribute('aria-hidden','true'); });
            buttons.forEach(b=>{ b.classList.remove('active'); b.setAttribute('aria-expanded','false'); b.setAttribute('aria-selected','false'); });
          } else {
            // go back to default tab view (first active)
            activateTab(buttons[0]);
          }
        }
      });
    }

    // run after DOM ready (script is at bottom so it's fine)
    setupLawControls();

    // small accessibility for social links: open external in new tab and announce
    document.querySelectorAll('.socials a[target="_blank"]').forEach(a=>{
      a.addEventListener('click', ()=>{ /* noop for now, reserved for tracking if needed */ });
    });

  </script>
</body>
</html>
