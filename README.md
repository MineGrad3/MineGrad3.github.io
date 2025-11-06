<!doctype html>
<html lang="ru">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>PurplePay - прототип агрегатора покупок + кошелёк</title>
  <!-- README: Сокращённая информация для интеграции - все инструкции и предупреждения сохранены в исходном файле. (Подробности скрыты в UI). -->

  <style>
    :root{
      --purple-500: #6B46C1;
      --purple-400: #8B5CF6;
      --purple-700: #4C1D95;
      --bg: #EDE9FE;
      --muted: #6B7280;
      --glass: rgba(255,255,255,0.06);
      --radius: 12px;
      --font-family: system-ui, -apple-system, "Segoe UI", Roboto, "Helvetica Neue", Arial;
      --max-width: 1200px;
    }

    /* Mobile-first reset */
    *{box-sizing:border-box}
    html,body{height:100%}
    body{
      margin:0;
      font-family:var(--font-family);
      background:linear-gradient(180deg,var(--bg),#F7F3FF 80%);
      color:#0f172a;
      -webkit-font-smoothing:antialiased;
      -moz-osx-font-smoothing:grayscale;
      line-height:1.45;
      padding:16px;
      display:flex;justify-content:center;
    }
    .container{width:100%;max-width:var(--max-width)}

    /* Header */
    header.site-header{display:flex;align-items:center;justify-content:space-between;gap:12px;margin-bottom:12px}
    .brand{display:flex;align-items:center;gap:12px}
    .logo{width:64px;height:64px;border-radius:10px;background:linear-gradient(135deg,var(--purple-500),var(--purple-400));display:flex;align-items:center;justify-content:center;color:white;font-weight:700;font-size:20px;box-shadow:0 6px 18px rgba(107,70,193,0.18)}
    .brand h1{font-size:20px;margin:0}
    .profile{display:flex;align-items:center;gap:10px}
    .profile .name{font-weight:600}
    .avatar{width:48px;height:48px;border-radius:999px;background:linear-gradient(0deg,#fff8,transparent);display:flex;align-items:center;justify-content:center;border:2px solid rgba(255,255,255,0.2)}

    /* Nav */
    nav.main-nav{display:flex;gap:8px;overflow:auto;margin-bottom:16px}
    nav.main-nav a{padding:8px 12px;border-radius:10px;text-decoration:none;color:var(--purple-700);font-weight:600;background:transparent}
    nav.main-nav a.active{background:linear-gradient(90deg,var(--purple-400),var(--purple-500));color:white}

    /* Layout */
    .layout{display:grid;grid-template-columns:1fr;gap:16px}

    /* Sidebar */
    .sidebar{background:linear-gradient(180deg,rgba(255,255,255,0.6),rgba(255,255,255,0.4));padding:12px;border-radius:12px;box-shadow:0 6px 20px rgba(76,29,149,0.08);position:relative}
    .balance{display:flex;flex-direction:column;gap:8px}
    .balance .amount{font-size:20px;font-weight:700;color:var(--purple-700)}
    .sidebar .btn{display:block;width:100%;padding:10px;border-radius:10px;border:0;background:var(--purple-500);color:white;font-weight:700}

    /* Search + Filters */
    .controls{display:flex;gap:8px;flex-wrap:wrap;margin-bottom:12px}
    .search{flex:1;display:flex;gap:8px}
    .search input{flex:1;padding:10px;border-radius:10px;border:1px solid rgba(15,23,42,0.06)}
    .filters{display:flex;gap:8px;overflow:auto}
    .chip{padding:8px 10px;border-radius:999px;border:1px solid rgba(15,23,42,0.04);background:white;font-weight:600}

    /* Grid */
    .grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(300px,1fr));gap:16px}

    /* Card layout: ensure readable line length */
    .card{
      background:white;padding:14px;border-radius:12px;display:flex;gap:12px;align-items:flex-start;box-shadow:0 2px 8px rgba(16,24,40,0.03);transition:transform .18s ease,box-shadow .18s ease;position:relative;overflow:hidden;flex-direction:row;
    }
    .card:hover{transform:translateY(-6px);box-shadow:0 16px 40px rgba(16,24,40,0.08)}

    /* fixed image area */
    .card .img-wrap{width:140px;height:100px;border-radius:8px;flex:0 0 140px;overflow:hidden;background:linear-gradient(90deg,var(--purple-400),var(--purple-500));display:flex;align-items:center;justify-content:center;color:white}
    .card img{width:100%;height:100%;object-fit:cover;display:block}

    /* content area: limit width in characters (ch) so lines ~10-20 chars */
    .card .content{flex:1;min-width:0;max-width:28ch;}
    .card h3{margin:0;font-size:16px}
    .card p{margin:6px 0 0;color:var(--muted);font-size:13px;line-height:1.4;word-break:break-word;overflow-wrap:break-word}

    /* price area stays fixed so it doesn't push content */
    .price{margin-left:auto;text-align:right;display:flex;flex-direction:column;gap:6px;flex:0 0 110px;min-width:110px}
    .price .L{font-weight:800;font-size:18px}

    .badge{position:absolute;left:12px;top:12px;background:linear-gradient(90deg,var(--purple-400),var(--purple-500));color:white;padding:6px 8px;border-radius:999px;font-weight:700;font-size:12px}
    .card .meta{display:flex;gap:6px;align-items:center;margin-top:8px}
    .meta .icon{width:18px;height:18px;display:inline-flex;align-items:center;justify-content:center}
    .cta{padding:8px 12px;border-radius:10px;border:0;background:var(--purple-500);color:white;font-weight:700}

    /* Footer */
    footer{margin-top:18px;padding:12px;border-radius:12px;background:linear-gradient(180deg,rgba(107,70,193,0.06),rgba(139,92,246,0.03));color:var(--muted);display:flex;justify-content:space-between;align-items:center}
    footer a{color:var(--purple-700);text-decoration:none;font-weight:700}

    /* Modals & Toasts */
    .modal-backdrop{position:fixed;inset:0;background:rgba(2,6,23,0.6);display:none;align-items:center;justify-content:center;padding:16px;z-index:80}
    .modal{background:white;border-radius:12px;padding:18px;max-width:520px;width:100%;box-shadow:0 30px 80px rgba(2,6,23,0.6)}
    .modal header{display:flex;justify-content:space-between;align-items:center}
    .toast{position:fixed;right:20px;bottom:20px;background:var(--purple-700);color:white;padding:10px 14px;border-radius:10px;box-shadow:0 10px 30px rgba(76,29,149,0.3);display:none;z-index:90}

    /* History table */
    table{width:100%;border-collapse:collapse}
    td,th{padding:8px;text-align:left;border-bottom:1px solid #f3f4f6}

    /* Responsive behavior */
    @media(max-width:699px){
      .grid{grid-template-columns:1fr}
      .card{flex-direction:column}
      .card .img-wrap{width:100%;height:160px;flex:0 0 auto}
      .card .content{max-width:100%}
      .price{flex:0 0 auto;min-width:0;text-align:left}
    }

    @media(min-width:700px){
      .layout{grid-template-columns:320px 1fr}
      .container{padding:20px}
    }

    /* Accessibility focus */
    a:focus,button:focus,input:focus{outline:3px solid rgba(139,92,246,0.25);outline-offset:3px}

    /* Visual adjustments */
    body{font-size:16px;padding:20px}
    .logo{width:64px;height:64px;font-size:20px}
    .avatar{width:48px;height:48px}
    .card h3{font-size:18px}
    .price .L{font-size:20px}

  </style>
</head>
<body>
  <div class="container" role="main">
    <header class="site-header" aria-label="Шапка сайта">
      <div class="brand">
        <div class="logo" aria-hidden="true">SW</div>
        <div>
          <h1 style="text-transform:none">SaveWallet.md</h1>
          <div style="font-size:13px;color:var(--muted)">SaveWallet.md - ваш надежный помощник для онлайн переводов.</div>
        </div>
      </div>

      <div class="profile" aria-label="Пользователь">
        <div style="text-align:right">
          <div class="name">Ксения Татарчук</div>
          <div style="font-size:12px;color:var(--muted)">online</div>
        </div>
        <button id="open-profile" class="avatar" aria-label="Открыть профиль" title="Открыть профиль">
          <!-- Avatar SVG -->
          <svg width="24" height="24" viewBox="0 0 24 24" fill="none" aria-hidden="true"><circle cx="12" cy="8" r="3.2" stroke="white" stroke-width="1.2"/><path d="M3 20c1.8-4 6-6 9-6s7.2 2 9 6" stroke="white" stroke-width="1.2" stroke-linecap="round"/></svg>
        </button>
      </div>
    </header>

    <nav class="main-nav" role="navigation" aria-label="Главная навигация">
      <a href="#" class="active">Home</a>
      <a href="#">Магазин</a>
      <a href="#">Профиль</a>
      <a href="#">Баланс</a>
    </nav>

    <div class="layout">
      <aside class="sidebar" aria-labelledby="wallet-label">
        <div id="wallet-label" style="font-size:13px;color:var(--muted)">Кошелёк</div>
        <div class="balance" aria-live="polite" style="margin-top:8px">
          <div style="font-size:12px;color:var(--muted)">Баланс</div>
          <div class="amount" id="balance-amount">350 L</div>
        </div>
        <div style="display:flex;gap:8px;margin-top:10px">
          <button id="btn-topup" class="btn" aria-haspopup="dialog">Пополнить</button>
          <button id="btn-send" class="btn" style="background:transparent;border:1px solid var(--purple-500);color:var(--purple-700)">Отправить</button>
        </div>
        <button id="btn-history" class="btn" style="margin-top:10px;background:transparent;border:1px dashed rgba(107,70,193,0.12);color:var(--purple-700)">История</button>

        <div style="margin-top:12px;font-size:13px;color:var(--muted)">
          <strong>Ссылки</strong>
          <div style="margin-top:6px"><a href="#">Terms</a> • <a href="#">Privacy</a></div>
        </div>
      </aside>

      <section>
        <div class="controls" role="region" aria-label="Поиск и фильтры">
          <div class="search">
            <input id="search" type="search" placeholder="Поиск товаров, сервисов..." aria-label="Поиск" />
            </div>
          <div class="filters" role="tablist" aria-label="Категории">
            <button class="chip" data-cat="all">Все</button>
            <button class="chip" data-cat="games">Игры</button>
            <button class="chip" data-cat="subscriptions">Подписки</button>
            <button class="chip" data-cat="food">Доставка</button>
            <button class="chip" data-cat="electronics">Электроника</button>
            <button class="chip" data-cat="services">Услуги</button>
            <button class="chip" data-cat="giftcards">Подарочные карты</button>
          </div>
        </div>

        <div class="grid" id="products" aria-live="polite">
          <!-- Примеры карточек -->

          <!-- CARD -->
          <article class="card" data-cat="games" data-title="Cyber Quest" tabindex="0">
            <div class="img-wrap" aria-hidden="true">
              <img class="product-image" src="https://images.unsplash.com/photo-1511512578047-dfb367046420?ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=800&q=60" alt="Игра: Cyber Quest"/>
            </div>
            <div class="content">
              <h3>Cyber Quest</h3>
              <p>Приключенческая RPG - ключ Steam. Моментальная доставка.</p>
              <div class="meta">
                <span class="icon" aria-hidden="true"><!-- ICON: gamepad -->
                  <svg width="16" height="16" viewBox="0 0 24 24" fill="none"><path d="M6 14v-4" stroke="#6B46C1" stroke-width="1.6" stroke-linecap="round"/><path d="M18 14v-4" stroke="#6B46C1" stroke-width="1.6" stroke-linecap="round"/></svg>
                </span>
              </div>
            </div>

            <div class="price">
              <div class="L" data-price="50">50 L</div>
              <button class="cta buy-btn" data-id="p1">Купить</button>
            </div>
            <div class="badge">Гарантия безопасности</div>
          </article>

          <!-- CARD -->
          <article class="card" data-cat="subscriptions" data-title="StreamPlus" tabindex="0">
            <div class="img-wrap" aria-hidden="true">
              <img class="product-image" src="https://images.unsplash.com/photo-1729860648897-270eddd9026b?ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=800&q=60" alt="Подписка: StreamPlus"/>
            </div>
            <div class="content">
              <h3>StreamPlus - 1 мес</h3>
              <p>Новый стриминг с HD на популярных платформах. Авто-активация.</p>
              <div class="meta">
                <span class="icon" aria-hidden="true"><!-- ICON: play -->
                  <svg width="16" height="16" viewBox="0 0 24 24" fill="none"><path d="M5 3v18l15-9L5 3z" stroke="#6B46C1" stroke-width="0.6" fill="#8B5CF6"/></svg>
                </span>
              </div>
            </div>

            <div class="price">
              <div class="L" data-price="30">30 L</div>
              <button class="cta buy-btn" data-id="p2">Купить</button>
            </div>
            <div class="badge">Гарантия безопасности</div>
          </article>

          <!-- CARD -->
          <article class="card" data-cat="food" data-title="SushiBox" tabindex="0">
            <div class="img-wrap" aria-hidden="true">
              <img class="product-image" src="https://images.unsplash.com/photo-1599513333212-30a0f705b179?ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=800&q=60" alt="Доставка: SushiBox"/>
            </div>
            <div class="content">
              <h3>SushiBox - набор</h3>
              <p>Премиум сеты. Доставка за 40-60 мин.</p>
              <div class="meta">
                <span class="icon" aria-hidden="true"><!-- ICON: food -->
                  <svg width="16" height="16" viewBox="0 0 24 24" fill="none"><path d="M12 3v18" stroke="#6B46C1" stroke-width="1.4"/><path d="M4 7h16" stroke="#6B46C1" stroke-width="1.4"/></svg>
                </span>
              </div>
            </div>

            <div class="price">
              <div class="L" data-price="120">120 L</div>
              <button class="cta buy-btn" data-id="p3">Купить</button>
            </div>
            <div class="badge">Гарантия безопасности</div>
          </article>

          <!-- CARD -->
          <article class="card" data-cat="electronics" data-title="EarPods X" tabindex="0">
            <div class="img-wrap" aria-hidden="true">
              <img class="product-image" src="https://plus.unsplash.com/premium_photo-1679056944603-3a1e03fe68d7?ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=800&q=60" alt="Наушники EarPods X"/>
            </div>
            <div class="content">
              <h3>EarPods X</h3>
              <p>Беспроводные наушники с шумоподавлением.</p>
              <div class="meta">
                <span class="icon" aria-hidden="true">
                  <svg width="16" height="16" viewBox="0 0 24 24" fill="none"><circle cx="12" cy="12" r="8" stroke="#6B46C1"/></svg>
                </span>
              </div>
            </div>

            <div class="price">
              <div class="L" data-price="900">900 L</div>
              <button class="cta buy-btn" data-id="p4">Купить</button>
            </div>
            <div class="badge">Гарантия безопасности</div>
          </article>

          <!-- CARD -->
          <article class="card" data-cat="services" data-title="SafeVPN - 1 год" tabindex="0">
            <div class="img-wrap" aria-hidden="true">
              <img class="product-image" src="https://images.unsplash.com/photo-1603985529862-9e12198c9a60?ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=800&q=60" alt="VPN: SafeVPN"/>
            </div>
            <div class="content">
              <h3>SafeVPN - 1 год</h3>
              <p>VPN для безопасности и приватности.</p>
              <div class="meta">
                <span class="icon" aria-hidden="true">
                  <svg width="16" height="16" viewBox="0 0 24 24" fill="none"><path d="M12 2v4" stroke="#6B46C1" stroke-width="1.4"/></svg>
                </span>
              </div>
            </div>

            <div class="price">
              <div class="L" data-price="180">180 L</div>
              <button class="cta buy-btn" data-id="p5">Купить</button>
            </div>
            <div class="badge">Гарантия безопасности</div>
          </article>

          <!-- CARD -->
          <article class="card" data-cat="giftcards" data-title="Gift Card 200L" tabindex="0">
            <div class="img-wrap" aria-hidden="true">
              <img class="product-image" src="https://images.unsplash.com/photo-1512436991641-6745cdb1723f?auto=format&fit=crop&w=800&q=60" alt="Подарочная карта 200 лей"/>
            </div>
            <div class="content">
              <h3>Gift Card - 200 L</h3>
              <p>Подарочная карта для популярных сервисов.</p>
              <div class="meta">
                <span class="icon" aria-hidden="true">
                  <svg width="16" height="16" viewBox="0 0 24 24" fill="none"><rect x="3" y="7" width="18" height="12" rx="2" stroke="#6B46C1"/></svg>
                </span>
              </div>
            </div>

            <div class="price">
              <div class="L" data-price="200">200 L</div>
              <button class="cta buy-btn" data-id="p6">Купить</button>
            </div>
            <div class="badge">Гарантия безопасности</div>
          </article>

        </div>

        <footer>
          <div>
            <strong>SaveWallet.md</strong> - мы обеспечиваем безопасность покупок и простоту управления балансом.
          </div>
          <div>
            <a href="#">Terms</a> • <a href="#">Privacy</a>
          </div>
        </footer>
      </section>
    </div>
  </div>

  <!-- Modals -->
  <div class="modal-backdrop" id="modal-backdrop" role="dialog" aria-modal="true" aria-hidden="true">
    <div class="modal" role="document" aria-labelledby="modal-title">
      <header>
        <h2 id="modal-title">Модальное окно</h2>
        <button id="modal-close" aria-label="Закрыть">✕</button>
      </header>
      <div id="modal-body" style="margin-top:12px"></div>
    </div>
  </div>

  <div class="toast" id="toast" role="status" aria-live="polite"></div>

  <script>
    // === Demo data & helpers ===
    const COMMISSION = 0.10; // 10% commission
    const products = [
      {id:'p1',title:'Cyber Quest',price:50,cat:'games'},
      {id:'p2',title:'StreamPlus - 1 мес',price:30,cat:'subscriptions'},
      {id:'p3',title:'SushiBox - набор',price:120,cat:'food'},
      {id:'p4',title:'EarPods X',price:900,cat:'electronics'},
      {id:'p5',title:'SafeVPN - 1 год',price:180,cat:'services'},
      {id:'p6',title:'Gift Card - 200 L',price:200,cat:'giftcards'}
    ];

    // Local balance (demo) - stored in memory; optionally persist to localStorage
    const STATE = {
      balance: (localStorage.getItem('pp_balance') ? Number(localStorage.getItem('pp_balance')) : 350),
      history: (localStorage.getItem('pp_history') ? JSON.parse(localStorage.getItem('pp_history')) : [])
    };

    function formatL(sum){return `${sum} L`}
    function showToast(msg, timeout=2500){const t=document.getElementById('toast');t.textContent=msg;t.style.display='block';setTimeout(()=>{t.style.display='none'},timeout)}

    function updateBalanceUI(){document.getElementById('balance-amount').textContent = formatL(STATE.balance);localStorage.setItem('pp_balance',STATE.balance)}

    updateBalanceUI();

    // === Modal helpers ===
    const backdrop=document.getElementById('modal-backdrop');
    function openModal(title, html){document.getElementById('modal-title').textContent=title;document.getElementById('modal-body').innerHTML=html;backdrop.style.display='flex';backdrop.setAttribute('aria-hidden','false')}
    function closeModal(){backdrop.style.display='none';backdrop.setAttribute('aria-hidden','true')}
    document.getElementById('modal-close').addEventListener('click',closeModal);
    backdrop.addEventListener('click',(e)=>{if(e.target===backdrop)closeModal()});

    // === Purchase flow ===
    document.querySelectorAll('.buy-btn').forEach(btn=>btn.addEventListener('click',handleBuy));

    function calcTotal(price){return Math.round((price*(1+COMMISSION))*100)/100}

    function handleBuy(e){
      const id=e.currentTarget.dataset.id;const p=products.find(x=>x.id===id);
      if(!p)return;
      const total=calcTotal(p.price);
      openModal('Подтверждение покупки',`\n        <p>Вы собираетесь купить <strong>${p.title}</strong> за <strong>${p.price} L</strong>.</p>\n        <p>Комиссия ${COMMISSION*100}% - итог: <strong>${total} L</strong>.</p>\n        <div style="display:flex;gap:8px;margin-top:12px">\n          <button id="confirm-buy" class="cta">Подтвердить - ${total} L</button>\n          <button id="cancel-buy" style="padding:10px;border-radius:10px;border:0;background:#f3f4f6">Отмена</button>\n        </div>\n        <p style="margin-top:12px;font-size:13px;color:var(--muted)">Функция демонстрационная - требует бэкенд.</p>\n      `);

      document.getElementById('confirm-buy').addEventListener('click',()=>{
        if(STATE.balance < total){showToast('Недостаточно средств');return}
        // Demo: update balance and history
        STATE.balance = Math.round((STATE.balance - total)*100)/100;
        const tx={id:Date.now(),type:'purchase',title:p.title,amount:-total,date:new Date().toLocaleString()};
        STATE.history.unshift(tx);if(STATE.history.length>50)STATE.history.pop();localStorage.setItem('pp_history',JSON.stringify(STATE.history));
        updateBalanceUI();showToast('Покупка подтверждена');closeModal();
      });
      document.getElementById('cancel-buy').addEventListener('click',closeModal);
    }

    // === Topup / Transfer / History UI ===
    document.getElementById('open-profile').addEventListener('click',openWallet);
    document.getElementById('btn-topup').addEventListener('click',()=>openTopup());
    document.getElementById('btn-send').addEventListener('click',()=>openSend());
    document.getElementById('btn-history').addEventListener('click',()=>openHistory());

    function openWallet(){
      openModal('Профиль / Кошелёк',`\n        <p><strong>Баланс:</strong> <span id="modal-balance">${formatL(STATE.balance)}</span></p>\n        <hr />\n        <h3>Получить перевод</h3>\n        <p>Адрес кошелька: <code>user_pp_Xenia</code></p>\n        <h3 style="margin-top:12px">Отправить перевод</h3>\n        <form id="send-form">\n          <label><br/><input name="to" required placeholder="например: user_pp_ivan"/></label>\n          <label>Получатель (адрес)<br/><input name="amount" type="number" step="0.01" min="0.01" required/></label>\n          <label>Сумма (L)<br/><input name="note" placeholder="За подарок"/></label></label>\nПримечание<label>\n          <div style="display:flex;gap:8px;margin-top:8px">\n            <button class="cta" type="submit">Отправить</button>\n            <button id="send-cancel" type="button" style="padding:10px;border-radius:10px;border:0;background:#f3f4f6">Отмена</button>\n          </div>\n        </form>\n        <p style="margin-top:12px;color:var(--muted)">Функция демонстрационная - требуется бэкенд для реальных переводов.</p>\n      `);

      document.getElementById('send-cancel').addEventListener('click',closeModal);
      document.getElementById('send-form').addEventListener('submit',function(ev){
        ev.preventDefault();const f=new FormData(ev.target);const to=f.get('to');const amount=Number(f.get('amount'));
        if(!to||amount<=0){showToast('Ошибка: заполните корректные данные');return}
        if(amount>STATE.balance){showToast('Ошибка: недостаточно средств');return}
        // Demo transfer: deduct balance & add history
        STATE.balance = Math.round((STATE.balance-amount)*100)/100;
        STATE.history.unshift({id:Date.now(),type:'transfer',title:`Перевод ${to}`,amount:-amount,date:new Date().toLocaleString()});
        localStorage.setItem('pp_history',JSON.stringify(STATE.history));updateBalanceUI();showToast('Перевод отправлен (демо)');closeModal();
      });
    }

    function openTopup(){
      openModal('Пополнение',`\n        <form id="topup-form">\n          <label>Сумма (L)<br/><input name="amount" type="number" step="0.01" min="1" required/></label>\n          <div style="display:flex;gap:8px;margin-top:8px">\n            <button class="cta" type="submit">Пополнить</button>\n            <button id="topup-cancel" type="button" style="padding:10px;border-radius:10px;border:0;background:#f3f4f6">Отмена</button>\n          </div>\n        </form>\n        <p style="margin-top:12px;color:var(--muted)">Демонстрация: реальная оплата требует сервера и платёжного провайдера.</p>\n      `);
      document.getElementById('topup-cancel').addEventListener('click',closeModal);
      document.getElementById('topup-form').addEventListener('submit',function(ev){
        ev.preventDefault();const f=new FormData(ev.target);const amount=Number(f.get('amount'));
        if(amount<=0){showToast('Введите корректную сумму');return}
        // Demo: add to balance
        STATE.balance = Math.round((STATE.balance + amount)*100)/100;
        STATE.history.unshift({id:Date.now(),type:'topup',title:'Пополнение',amount:amount,date:new Date().toLocaleString()});localStorage.setItem('pp_history',JSON.stringify(STATE.history));updateBalanceUI();showToast('Счёт пополнен (демо)');closeModal();
      });
    }

    function openHistory(){
      const rows = STATE.history.slice(0,5).map(tx=>`<tr><td>${tx.date}</td><td>${tx.title}</td><td style="text-align:right">${tx.amount>0?'+':''}${tx.amount} L</td></tr>`).join('')||'<tr><td colspan="3" style="color:var(--muted)">История пуста</td></tr>';
      openModal('История транзакций',`<table><thead><tr><th>Дата</th><th>Операция</th><th>Сумма</th></tr></thead><tbody>${rows}</tbody></table><div style="margin-top:8px"><button class="cta" onclick="downloadHistory()">Скачать CSV</button></div>`);
    }

    function downloadHistory(){
      const csv = ['date,title,amount',...STATE.history.map(h=>`"${h.date}","${h.title}","${h.amount}"`)].join('\n');
      const blob=new Blob([csv],{type:'text/csv'});const url=URL.createObjectURL(blob);const a=document.createElement('a');a.href=url;a.download='history.csv';a.click();URL.revokeObjectURL(url);
      showToast('CSV скачан (демо)');
    }

    // === Search & Filters ===
    document.getElementById('search').addEventListener('input',(e)=>{
      const q=e.target.value.toLowerCase();filterProducts(q,selectedCat);
    });
    const clearBtn = document.getElementById('clear-search'); if(clearBtn){clearBtn.addEventListener('click', ()=>{document.getElementById('search').value='';filterProducts('',selectedCat);});}

    let selectedCat='all';
    document.querySelectorAll('.filters .chip').forEach(ch=>ch.addEventListener('click',function(){
      document.querySelectorAll('.filters .chip').forEach(x=>x.classList.remove('active'));
      this.classList.add('active');selectedCat=this.dataset.cat||'all';filterProducts(document.getElementById('search').value.toLowerCase(),selectedCat);
    }));

    function filterProducts(q,cat){
      document.querySelectorAll('#products .card').forEach(card=>{
        const title = card.dataset.title.toLowerCase();const c = card.dataset.cat;
        const matchQ = !q || title.includes(q);
        const matchCat = (cat==='all' || !cat) ? true : (c===cat);
        card.style.display = (matchQ && matchCat) ? 'flex' : 'none';
      });
    }

    // Accessibility: enter on card -> open quick buy modal
    document.querySelectorAll('.card').forEach(card=>card.addEventListener('keydown',function(e){if(e.key==='Enter'){const btn=this.querySelector('.buy-btn');btn && btn.click()}}));

    // === Where server logic needed (developer note shown in console) ===
    console.warn('WARNING: Demo frontend. Do NOT use for real payments. Implement server-side endpoints: /api/pay, /api/wallet/* with authentication, validation and audit logs.');

    // Extra: show commission on hover by updating CTA text
    document.querySelectorAll('.card').forEach(card=>{
      const priceEl = card.querySelector('.L');const base = Number(priceEl.dataset.price);
      const btn = card.querySelector('.buy-btn');
      function updateBtn(){btn.textContent = `Купить - ${calcTotal(base)} L`} 
      card.addEventListener('mouseenter',updateBtn);card.addEventListener('focusin',updateBtn);
      card.addEventListener('mouseleave',()=>{btn.textContent='Купить'});
    });

  </script>
</body>
</html>
