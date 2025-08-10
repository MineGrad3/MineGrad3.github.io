<!doctype html>
<html lang="ru">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>MineGrad — Город возможностей</title>
  <meta name="description" content="MineGrad — роллплей сервер Minecraft. Подай заявку в вайтлист и начни свою историю. Дальше = больше." />
  <link rel="icon" href="data:;base64,iVBORw0KGgo=" />
  <style>
    /* Google-font-like fallback */
    @import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600;800&display=swap');

    :root{
      --bg1:#07021a;
      --bg2:#1a0830;
      --accent1:#7c3aed; /* purple */
      --accent2:#5b21b6; /* deep purple */
      --muted:rgba(255,255,255,0.78);
      --card: rgba(255,255,255,0.04);
      --glass: rgba(255,255,255,0.04);
      --glass-2: rgba(255,255,255,0.03);
    }

    *{box-sizing:border-box}
    html,body{height:100%}
    body{
      margin:0;
      font-family: 'Inter', system-ui, -apple-system, 'Segoe UI', Roboto, 'Helvetica Neue', Arial;
      color:var(--muted);
      background: radial-gradient(1200px 600px at 10% 10%, rgba(124,58,237,0.12), transparent), linear-gradient(180deg,var(--bg1),var(--bg2));
      -webkit-font-smoothing:antialiased;
      -moz-osx-font-smoothing:grayscale;
    }

    .container{max-width:1100px;margin:40px auto;padding:28px}

    header{display:flex;align-items:center;justify-content:space-between;gap:16px}
    .brand{display:flex;align-items:center;gap:12px}
    .logo{width:64px;height:64px;border-radius:14px;background:linear-gradient(135deg,var(--accent1),var(--accent2));display:flex;align-items:center;justify-content:center;font-weight:800;color:white;font-size:20px;box-shadow:0 10px 30px rgba(91,33,182,0.18)}
    h1{margin:0;font-size:22px}
    .tag{font-size:13px;color:rgba(255,255,255,0.65)}

    nav{display:flex;gap:10px}
    .btn{background:linear-gradient(90deg,var(--accent1),var(--accent2));padding:10px 16px;border-radius:10px;color:white;font-weight:600;text-decoration:none;display:inline-block}
    .btn.ghost{background:transparent;border:1px solid rgba(255,255,255,0.06);color:var(--muted)}

    main{margin-top:26px}
    .hero{display:grid;grid-template-columns:1fr 540px;gap:28px;align-items:center}
    .eyebrow{display:inline-block;background:linear-gradient(90deg,#2d1366,#6b3bd1);padding:6px 10px;border-radius:999px;font-size:13px;color:white;font-weight:700}
    .big{font-size:44px;line-height:1.02;margin:12px 0;font-weight:800}
    .lead{color:rgba(255,255,255,0.85);font-size:16px}

    .features{display:grid;grid-template-columns:repeat(2,1fr);gap:12px;margin-top:18px}
    .pill{background:var(--card);padding:12px;border-radius:10px;font-weight:600}

    /* gallery */
    .card{border-radius:16px;overflow:hidden;background:linear-gradient(180deg, rgba(255,255,255,0.02), rgba(255,255,255,0.01));box-shadow:0 10px 30px rgba(2,6,23,0.6);}
    .gallery{height:360px;background:#000;position:relative;display:flex;align-items:center;justify-content:center}
    .gallery img{width:100%;height:100%;object-fit:cover;display:block}
    .gallery .overlay{position:absolute;inset:0;background:linear-gradient(180deg,transparent,rgba(2,6,23,0.6) 65%)}
    .gallery .meta{position:absolute;left:18px;bottom:18px;background:rgba(0,0,0,0.35);backdrop-filter:blur(6px);padding:10px;border-radius:10px}
    .controls{display:flex;align-items:center;justify-content:space-between;padding:10px}
    .small-btn{background:rgba(255,255,255,0.03);border:1px solid rgba(255,255,255,0.04);padding:8px 10px;border-radius:8px;color:var(--muted);cursor:pointer}

    /* sections */
    section{margin-top:22px}
    .grid3{display:grid;grid-template-columns:repeat(3,1fr);gap:12px}
    .card-blur{padding:18px;border-radius:12px;background:linear-gradient(180deg, rgba(255,255,255,0.02), rgba(255,255,255,0.01));border:1px solid rgba(255,255,255,0.03)}

    /* rules */
    .rules{display:grid;grid-template-columns:repeat(2,1fr);gap:18px}
    .rules h3{margin-top:0}
    ul.rules-list{padding-left:18px;margin:8px 0}

    /* socials */
    .socials{display:flex;gap:10px;flex-wrap:wrap}
    .socials a{padding:8px 12px;border-radius:10px;text-decoration:none;font-weight:700}
    .yt{background:#ff3b3b;color:white}
    .tt{background:#111;color:white}
    .vk{background:#4a76a8;color:white}
    .tg{background:linear-gradient(90deg,#6b3bd1,#2a64d6);color:white}
    .donate{background:linear-gradient(90deg,#10b981,#059669);color:white}

    footer{margin-top:38px;text-align:center;color:rgba(255,255,255,0.44);font-size:13px;padding-bottom:30px}

    /* responsive */
    @media (max-width:1000px){
      .hero{grid-template-columns:1fr}
      .gallery{height:260px}
      .grid3{grid-template-columns:1fr}
      .rules{grid-template-columns:1fr}
    }

    @media (max-width:420px){.big{font-size:28px}}
  </style>
</head>
<body>
  <div class="container">
    <header>
      <div class="brand">
        <div class="logo">MG</div>
        <div>
          <h1>MineGrad</h1>
          <div class="tag">Город возможностей. Играй. РП. Живи.</div>
        </div>
      </div>

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

          <div style="margin-top:16px">
            <a class="btn" href="#apply">Подать заявку в вайтлист</a>
            <a class="btn ghost" href="#discord" style="margin-left:10px">Вступить в Discord</a>
          </div>

          <p style="margin-top:12px;color:rgba(255,255,255,0.6);font-size:13px">Важно: для захода на сервер обязательно подать заявку и дождаться добавления в вайтлист через Discord.</p>
        </div>

        <div class="card">
          <div class="gallery" id="gallery">
            <img id="gimg" src="https://images.unsplash.com/photo-1517248135467-4c7edcad34c4?auto=format&fit=crop&w=1600&q=80" alt="MineGrad screenshot">
            <div class="overlay"></div>
            <div class="meta">
              <div style="font-weight:800">MineGrad — вид города</div>
              <div style="font-size:12px;color:rgba(255,255,255,0.7)">Скриншоты сервера — позже сюда можно загрузить свои фото.</div>
            </div>
          </div>
          <div class="controls">
            <button class="small-btn" onclick="prev()">⟨</button>
            <div style="font-size:13px;color:rgba(255,255,255,0.7)" id="gmeta">Скрин 1 из 4</div>
            <button class="small-btn" onclick="next()">⟩</button>
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
          <div style="display:grid;grid-template-columns:repeat(3,1fr);gap:12px;margin-top:12px">
            <div class="pill" style="background:var(--glass)">Купить квартиру и открыть бизнес</div>
            <div class="pill" style="background:var(--glass)">Устроиться на работу: водитель, доставщик, полицейский</div>
            <div class="pill" style="background:var(--glass)">Участвовать в ивентах и влиять на сюжет</div>
          </div>
        </div>
      </section>

      <section class="card-blur" id="rules" style="margin-top:18px">
        <h3>📜 Официальные правила MineGrad</h3>
        <div class="rules" style="margin-top:12px">
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

          <div style="grid-column:1 / -1">
            <h4>5️⃣ Законы города MineGrad</h4>
            <p style="font-weight:700;margin:6px 0">🔴 Уголовные преступления:</p>
            <ul class="rules-list">
              <li>Убийство без причины — 30 минут тюрьмы.</li>
              <li>Ограбление (при поимке) — 20 минут тюрьмы + штраф.</li>
              <li>Нападение на полицейского/военного — 40 минут тюрьмы.</li>
              <li>Попытка госпереворота — пожизненное заключение.</li>
            </ul>

            <p style="font-weight:700;margin:6px 0">🟡 Административные нарушения:</p>
            <ul class="rules-list">
              <li>Оскорбления/провокации — штраф или 10 минут КПЗ.</li>
              <li>Незаконное проникновение — 15 минут тюрьмы.</li>
              <li>Вандализм (грифинг) — бан от 3 дней до перманента.</li>
            </ul>
          </div>
        </div>
      </section>

      <section style="margin-top:18px;display:flex;gap:18px;align-items:flex-start;flex-wrap:wrap">
        <div style="flex:1;min-width:260px" class="card-blur">
          <h4>Соцсети MineGrad</h4>
          <p style="margin-top:6px;color:rgba(255,255,255,0.75);font-size:14px">Подписывайся, подавай заявку и следи за ивентами.</p>
          <div style="margin-top:12px" class="socials">
            <a class="yt" href="https://www.youtube.com/@MineGradOfficial">YouTube</a>
            <a class="tt" href="https://www.tiktok.com/@minegrad">TikTok</a>
            <a class="vk" href="https://vk.com/club217846754">ВКонтакте</a>
            <a class="tg" href="https://t.me/minegradofficial">Telegram</a>
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
    // simple gallery logic — images are placeholders, replace with server screenshots later
    const gallery = [
      'https://images.unsplash.com/photo-1517248135467-4c7edcad34c4?auto=format&fit=crop&w=1600&q=80',
      'https://images.unsplash.com/photo-1500530855697-b586d89ba3ee?auto=format&fit=crop&w=1600&q=80',
      'https://images.unsplash.com/photo-1509395176047-4a66953fd231?auto=format&fit=crop&w=1600&q=80',
      'https://images.unsplash.com/photo-1502450802614-7df7a7b2b0a4?auto=format&fit=crop&w=1600&q=80',
    ];
    let idx = 0;
    const img = document.getElementById('gimg');
    const meta = document.getElementById('gmeta');

    function update(){
      img.src = gallery[idx];
      meta.innerText = `Скрин ${idx+1} из ${gallery.length}`;
    }
    function next(){ idx = (idx + 1) % gallery.length; update(); }
    function prev(){ idx = (idx - 1 + gallery.length) % gallery.length; update(); }
    // auto-rotate
    setInterval(()=>{ idx = (idx+1)%gallery.length; update(); },6000);
  </script>
</body>
</html>
