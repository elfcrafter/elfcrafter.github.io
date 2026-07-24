<!DOCTYPE html>
<html lang="ru">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=yes, viewport-fit=cover">
  <meta name="theme-color" content="#0a1a2e">
  <meta name="apple-mobile-web-app-capable" content="yes">
  <title>🌿 Мастерская Эльфа</title>
  <link rel="manifest" href="data:application/json;base64,ewogICJuYW1lIjogItCc0LDRgdGC0LXRgNGB0LrQsNGPINCt0LvRjNGE0LAiLAogICJzaG9ydF9uYW1lIjogItCt0LvRjNGEIiwKICAic3RhcnRfdXJsIjogIi4iLAogICJkaXNwbGF5IjogInN0YW5kYWxvbmUiLAogICJiYWNrZ3JvdW5kX2NvbG9yIjogIiMwYTFhMmUiLAogICJ0aGVtZV9jb2xvciI6ICIjMGExYTJlIiwKICAiaWNvbnMiOiBbCiAgICB7CiAgICAgICJzcmMiOiAiZGF0YTppbWFnZS9zdmcreG1sLCUzQ3N2ZyUyMHhtbG5zPSdodHRwOi8vd3d3LnczLm9yZy8yMDAwL3N2ZyclMjB2aWV3Qm94PScwIDAgMTAwIDEwMCclM0UlM0NjaXJjbGUlMjBjeD0nNTAnMjBjeT0nNTAnMjByPSc0OCclMjBmaWxsPSclMjMwYTFhMmUnMjBzdHJva2U9JyUyMzJkMmQ0NCclMjBzdHJva2Utd2lkdGg9JzQnLyUzRSUzQ3BhdGglMjBkPSdNMzAlMjA3MGwxMC0yMGgxMGwxMCUyMDIwSDQ1TTMwJTIwNDhsMTAtMjhoMTVsMTAlMjAyOGgtMTVsLTUtMTVINDBsLTUlMjAxNUgzMHonJTIwZmlsbD0nJTIzZDJhYjY3JyUyMHN0cm9rZT0nJTIzZDJhYjY3JyUyMHN0cm9rZS13aWR0aD0nMicvJTNFJTNDY2lyY2xlJTIwY3g9JzY1JTIwY3k9JzM1JTIwcj0nMTAnMjBmaWxsPSclMjNmZjU1MzMnLyUzRSUzQy9zdmclM0UiLAogICAgICAic2l6ZXMiOiAiMTkyeDE5MiIsCiAgICAgICJ0eXBlIjogImltYWdlL3N2Zy94bWwiCiAgICB9CiAgXQp9">
  <style>
    * { margin:0; padding:0; box-sizing:border-box; }
    body {
      background: linear-gradient(135deg, #0a1a2e 0%, #1a3a4e 100%);
      color: #d2d2d2;
      font-family: 'Nunito', 'Segoe UI', system-ui, sans-serif;
      min-height: 100vh;
      display: flex;
      justify-content: center;
      align-items: center;
      padding: 12px;
    }
    .app {
      max-width: 420px;
      width: 100%;
      background: #0f2235;
      border-radius: 32px;
      padding: 20px 16px;
      box-shadow: 0 20px 40px rgba(0,0,0,0.7);
      border: 1px solid #2d4a5a;
      position: relative;
      overflow: hidden;
    }
    .screen { display: none; flex-direction: column; }
    .screen.active { display: flex; }
    h2 { font-size: 1.5rem; color: #d2ab67; margin-bottom: 16px; font-weight: 700; text-align: center; }
    .btn {
      background: #1a3a4e;
      color: #d2d2d2;
      border: 1px solid #4a6a7a;
      padding: 14px 20px;
      border-radius: 40px;
      font-weight: 600;
      font-size: 0.95rem;
      cursor: pointer;
      width: 100%;
      margin-top: 12px;
    }
    .btn:hover { background: #2a4a5e; }
    .btn-outline {
      background: transparent;
      border: 2px solid #4a6a7a;
      color: #d2ab67;
    }
    input, textarea, select {
      background: #0a1a2e;
      border: 1px solid #4a6a7a;
      border-radius: 16px;
      padding: 12px;
      color: #d2d2d2;
      font-size: 0.95rem;
      width: 100%;
      margin-bottom: 10px;
      outline: none;
    }
    .pin-input {
      font-size: 2rem;
      letter-spacing: 12px;
      text-align: center;
    }
    .greeting {
      font-size: 1.4rem;
      color: #d2ab67;
      text-align: center;
      margin: 32px 0;
    }
    .mandala-grid {
      display: grid;
      grid-template-columns: 1fr 1fr 1fr;
      grid-template-rows: 1fr 1.2fr 1fr auto;
      gap: 8px;
      max-width: 360px;
      margin: 12px auto;
    }
    .mandala-petal {
      background: #162d40;
      border: 1px solid #4a6a7a;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      text-align: center;
      font-weight: 600;
      color: #d2d2d2;
      padding: 8px;
      font-size: 0.8rem;
      cursor: pointer;
    }
    #goCalendar { border-radius: 60% 40% 50% 50% / 60% 60% 40% 40%; }
    #goSocial { border-radius: 40% 60% 50% 50% / 40% 40% 60% 60%; }
    #goSettings { border-radius: 50% 50% 40% 60% / 60% 40% 50% 50%; }
    #goNotes { border-radius: 50% 50% 60% 40% / 40% 60% 50% 50%; }
    #goFinance { border-radius: 40% 60% 60% 40% / 50% 50% 40% 60%; }
    #goGallery { border-radius: 60% 40% 40% 60% / 40% 50% 60% 50%; }
    #goFestivals { border-radius: 30% 70% 50% 50% / 60% 40% 60% 40%; }
    .mandala-petal:active { transform: scale(0.96); background: #1e3a4e; }
    .mandala-petal .icon { font-size: 1.8rem; margin-bottom: 2px; }
    .mandala-center {
      grid-column: 2; grid-row: 2;
      width: 70px; height: 70px; border-radius: 50%;
      background: #1a3a4e;
      display: flex; align-items: center; justify-content: center;
      font-size: 2.8rem; color: #d2ab67; font-weight: 700;
      cursor: pointer; border: 2px solid #d2ab67;
      box-shadow: 0 0 20px #2a4a5e; margin: auto;
    }
    .mandala-center:active { transform: scale(0.94); background: #2a4a5e; }

    .photo-preview { display: flex; gap: 8px; flex-wrap: wrap; margin: 8px 0; }
    .photo-preview img { width: 64px; height: 64px; object-fit: cover; border-radius: 12px; border: 2px solid #4a6a7a; }
    .progress { background: #0a1a2e; border-radius: 20px; padding: 16px; margin: 16px 0; }

    .calendar-day { display: inline-block; width: 32px; height: 32px; text-align: center; line-height: 32px; margin: 2px; border-radius: 8px; cursor: pointer; }
    .calendar-day.past { color: #4a6a7a; text-decoration: line-through; }
    .calendar-day.today { background: #d2ab67; color: #0a1a2e; font-weight: bold; }
    .calendar-day.event { background: #2d5a2d; color: #a0d6a0; }
    .event-list { max-height: 250px; overflow-y: auto; margin-top: 12px; }
    .event-card { background: #0a1a2e; border: 1px solid #4a6a7a; border-radius: 16px; padding: 12px; margin-bottom: 8px; cursor: pointer; position: relative; }
    .event-card .tools { position: absolute; top: 8px; right: 12px; display: flex; gap: 6px; }
    .event-checklist { margin-top: 8px; display: none; }
    .event-checklist input[type="text"] { margin-top: 4px; }

    .notes-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 10px; }
    .notes-grid .note-widget { background: #0a1a2e; border-radius: 12px; padding: 12px; border: 1px solid #4a6a7a; display: flex; flex-direction: column; }
    .notes-grid .note-widget.wide { grid-column: span 2; }
    .note-widget label { font-size: 0.8rem; color: #d2ab67; margin-bottom: 4px; font-weight: 700; }
    .note-widget textarea { background: transparent; border: none; resize: none; padding: 4px 0; color: #d2d2d2; font-size: 0.85rem; height: 60px; }

    .finance-panel { display: flex; gap: 12px; height: 350px; }
    .category-tree { width: 35%; background: #0a1a2e; border-radius: 16px; padding: 12px; overflow-y: auto; font-size: 0.8rem; }
    .category-item { padding: 8px 6px; margin-bottom: 4px; cursor: pointer; border-radius: 12px; white-space: nowrap; }
    .category-item.active { background: #2a4a5e; color: #d2ab67; }
    .category-item.sub { padding-left: 16px; }
    .category-item.sub2 { padding-left: 32px; }
    .item-table { width: 65%; overflow-y: auto; background: #0a1a2e; border-radius: 16px; padding: 12px; }
    .item-row { display: flex; justify-content: space-between; align-items: center; padding: 6px 0; border-bottom: 1px solid #2d4a5a; font-size: 0.8rem; }
    .gallery-grid { display: flex; flex-wrap: wrap; gap: 8px; }
    .gallery-item { width: 80px; height: 80px; object-fit: cover; border-radius: 12px; border: 2px solid #4a6a7a; }

    .festival-card { background: #0a1a2e; border: 1px solid #4a6a7a; border-radius: 16px; padding: 12px; margin-bottom: 10px; }
    .festival-card select { width: auto; margin: 4px 0; }
    .social-card button { width: auto; padding: 6px 12px; }
  </style>
</head>
<body>
<div class="app" id="app">
  <div id="authScreen" class="screen active">
    <h2>📔 Мастерская 🪶<br>🌿 Эльфа 🍁</h2>
    <input type="password" id="pinInput" class="pin-input" maxlength="4" placeholder="····">
    <button class="btn" id="loginBtn">Войти</button>
    <button class="btn btn-outline" id="resetPinBtn">Сменить пин</button>
    <p style="color:#7a8a9a; text-align:center; margin-top:12px;">Пин по умолчанию 1234</p>
  </div>
  <div id="greetingScreen" class="screen"><div class="greeting" id="greetingText"></div></div>

  <div id="mainScreen" class="screen">
    <div class="mandala-grid">
      <div class="mandala-petal" id="goCalendar" style="grid-column:2; grid-row:1;"><span class="icon">📅</span> Календарь</div>
      <div class="mandala-petal" id="goSettings" style="grid-column:1; grid-row:2;"><span class="icon">⚙️</span> Настройки</div>
      <div class="mandala-center" id="goPublish">＋</div>
      <div class="mandala-petal" id="goNotes" style="grid-column:3; grid-row:2;"><span class="icon">📝</span> Заметки</div>
      <div class="mandala-petal" id="goFinance" style="grid-column:1; grid-row:3;"><span class="icon">💰</span> Финансы</div>
      <div class="mandala-petal" id="goSocial" style="grid-column:2; grid-row:3;"><span class="icon">💬</span> Соцсети</div>
      <div class="mandala-petal" id="goGallery" style="grid-column:3; grid-row:3;"><span class="icon">🖼️</span> Галерея</div>
      <div class="mandala-petal" id="goFestivals" style="grid-column:1 / span 3; grid-row:4;"><span class="icon">🎪</span> Фестивали</div>
    </div>
  </div>

  <div id="publishScreen" class="screen">
    <button class="btn btn-outline" id="backFromPublish" style="width:auto; margin-bottom:12px;">← Назад</button>
    <h2>📢 Новая публикация</h2>
    <input type="text" id="postTitle" placeholder="Название изделия">
    <textarea id="postDesc" placeholder="Описание..." rows="3"></textarea>
    <input type="number" id="postPrice" placeholder="Цена (₽)">
    <input type="text" id="postTags" placeholder="Хештеги через запятую (без #)">
    <label>📎 Фото (до 8):</label>
    <input type="file" id="photoInput" accept="image/*" multiple style="display:none;">
    <button class="btn btn-outline" onclick="document.getElementById('photoInput').click()" style="margin-top:4px;">Выбрать фото</button>
    <div class="photo-preview" id="photoPreview"></div>
    <div class="platform-list">
      <p style="color:#b8a68b;">Площадки:</p>
      <div id="platformCheckboxes"></div>
    </div>
    <button class="btn" id="startPublishBtn">🚀 Начать рассылку</button>
    <div id="publishProgress" class="progress" style="display:none;"></div>
  </div>

  <div id="calendarScreen" class="screen">
    <button class="btn btn-outline" id="backFromCalendar" style="width:auto; margin-bottom:12px;">← Назад</button>
    <h2>📅 Календарь</h2>
    <div style="display:flex; justify-content:space-between; margin-bottom:10px;">
      <button class="btn btn-outline" id="prevMonth" style="width:auto;">◀</button>
      <span id="monthLabel" style="font-weight:700;"></span>
      <button class="btn btn-outline" id="nextMonth" style="width:auto;">▶</button>
    </div>
    <div id="calendarDays" style="text-align:center;"></div>
    <div id="eventInput" style="display:none; margin-top:8px;">
      <input type="text" id="eventTitle" placeholder="Название события">
      <button class="btn" id="saveEventBtn">Сохранить</button>
    </div>
    <h3 style="margin-top:16px;">Ближайшие события</h3>
    <div class="event-list" id="eventList"></div>
  </div>

  <div id="notesScreen" class="screen">
    <button class="btn btn-outline" id="backFromNotes" style="width:auto; margin-bottom:12px;">← Назад</button>
    <h2>📝 Планы на неделю</h2>
    <div id="notesContainer"></div>
  </div>

  <div id="financeScreen" class="screen">
    <button class="btn btn-outline" id="backFromFinance" style="width:auto; margin-bottom:12px;">← Назад</button>
    <h2>💰 Финансы</h2>
    <div class="finance-panel">
      <div class="category-tree" id="categoryTree"></div>
      <div class="item-table" id="itemTable"></div>
    </div>
    <div style="margin-top:12px;">
      <input type="text" id="newItemName" placeholder="Название изделия">
      <input type="number" id="newItemCost" placeholder="Затраты (₽)">
      <input type="number" id="newItemPrice" placeholder="Прибыль (₽)">
      <input type="file" id="newItemPhoto" accept="image/*" style="display:none;">
      <button class="btn btn-outline" onclick="document.getElementById('newItemPhoto').click()">Фото</button>
      <button class="btn" id="addItemBtn">Добавить в категорию</button>
    </div>
  </div>

  <div id="socialScreen" class="screen">
    <button class="btn btn-outline" id="backFromSocial" style="width:auto; margin-bottom:12px;">← Назад</button>
    <h2>💬 Мои соцсети</h2>
    <div id="socialList"></div>
  </div>

  <div id="galleryScreen" class="screen">
    <button class="btn btn-outline" id="backFromGallery" style="width:auto; margin-bottom:12px;">← Назад</button>
    <h2>🖼️ Галерея</h2>
    <div class="gallery-grid" id="galleryGrid"></div>
  </div>

  <div id="festivalsScreen" class="screen">
    <button class="btn btn-outline" id="backFromFestivals" style="width:auto; margin-bottom:12px;">← Назад</button>
    <h2>🎪 Фестивали</h2>
    <div style="margin-bottom:12px;">
      <input type="text" id="newFestName" placeholder="Название фестиваля">
      <input type="text" id="newFestUrl" placeholder="Ссылка">
      <input type="date" id="newFestDate">
      <button class="btn" id="addFestBtn">Добавить</button>
    </div>
    <div id="festivalList"></div>
  </div>

  <div id="settingsScreen" class="screen">
    <button class="btn btn-outline" id="backFromSettings" style="width:auto; margin-bottom:12px;">← Назад</button>
    <h2>⚙️ Настройки</h2>
    <button class="btn btn-outline" id="changePinBtn">Сменить пин-код</button>
    <p style="color:#9c8a78; margin-top:12px;">Добавление площадок:</p>
    <div style="display:flex; gap:8px;">
      <input type="text" id="newPlatformName" placeholder="Название">
      <input type="text" id="newPlatformUrl" placeholder="Ссылка">
      <button class="btn" id="addPlatformBtn" style="width:auto;">+</button>
    </div>
    <div id="customPlatforms" style="margin-top:12px;"></div>
  </div>
</div>

<script>
  (function() {
    const STORAGE = 'craftsister_v5';
    let state = {
      pin: '1234',
      platforms: [
        { id: 'vk', name: 'ВКонтакте', url: 'https://m.vk.com/write' },
        { id: 'avito', name: 'Авито', url: 'https://www.avito.ru/additem' },
        { id: 'youla', name: 'Юла', url: 'https://youla.ru/create' },
        { id: 'livemaster', name: 'Ярмарка Мастеров', url: 'https://www.livemaster.ru/add' },
        { id: 'meshok', name: 'Мешок', url: 'https://meshok.net/new_item' },
        { id: 'pikabu', name: 'Пикабу', url: 'https://pikabu.ru/add-post' },
        { id: 'instagram', name: 'Instagram', url: 'https://www.instagram.com/create/' },
        { id: 'telegram', name: 'Telegram', url: 'https://t.me/' }
      ],
      events: [],
      notes: { mon:'', tue:'', wed:'', thu:'', fri:'', sat:'', sun:'' },
      socialCounts: {},
      currentMonth: new Date().getMonth(),
      currentYear: new Date().getFullYear(),
      selectedDate: null,
      financeItems: [],
      activeCategory: null,
      categories: [
        { name: 'Кожа', sub: [
          { name: 'Блокноты', sub: ['А4','А5','А6','А7','А8'] },
          { name: 'Браслеты', sub: ['контурами','красками','выжигатель','горелка'] },
          { name: 'Бабочки', sub: ['одинарные','двойные','тройные'] },
          { name: 'Брелки', sub: [] },
          { name: 'Броши', sub: [] },
          { name: 'Подвески', sub: [] }
        ]},
        { name: 'Ресуначбки))0)', sub: [
          { name: 'Холстi', sub: ['Болбшие','Маненькие','Ащщье жьест маненькие','Мемі))))))'] },
          { name: 'Ткани', sub: [] },
          { name: 'Разновие))', sub: [] }
        ]},
        { name: 'Пластинки', sub: [] },
        { name: 'Шкатулки', sub: [] },
        { name: 'Этнические штуки', sub: [] },
        { name: 'Несортируемое', sub: [] }
      ],
      festivals: [],
      festivalStatuses: ['Планирую', 'Заявка отправлена', 'Участвую', 'Отказ']
    };

    function load() {
      const saved = localStorage.getItem(STORAGE);
      if (saved) try { Object.assign(state, JSON.parse(saved)); } catch(e){}
      state.platforms.forEach(p => { if (!state.socialCounts[p.id]) state.socialCounts[p.id] = 0; });
    }
    function save() { localStorage.setItem(STORAGE, JSON.stringify(state)); }

    const screens = {
      auth: document.getElementById('authScreen'), greeting: document.getElementById('greetingScreen'), main: document.getElementById('mainScreen'),
      publish: document.getElementById('publishScreen'), calendar: document.getElementById('calendarScreen'), notes: document.getElementById('notesScreen'),
      finance: document.getElementById('financeScreen'), social: document.getElementById('socialScreen'), gallery: document.getElementById('galleryScreen'),
      festivals: document.getElementById('festivalsScreen'), settings: document.getElementById('settingsScreen')
    };
    function show(id) {
      Object.values(screens).forEach(s => s.classList.remove('active'));
      screens[id].classList.add('active');
    }

    document.getElementById('loginBtn').addEventListener('click', () => {
      if (document.getElementById('pinInput').value === state.pin) {
        const phrases = ['Привет! Что нового ты придумал?','О, новые красивые штуки!','Не волнуйся, мы найдём тебе заказы.','Не бойся, я с тобой.','Рисуй чаще, и чаща нарисует тебе.','С возвращением, мастер Эльфа!','Улыбнись, твои работы этого достойны.'];
        document.getElementById('greetingText').textContent = phrases[Math.floor(Math.random()*phrases.length)];
        show('greeting'); setTimeout(() => show('main'), 2000);
      } else alert('Неверный пин');
    });
    document.getElementById('resetPinBtn').addEventListener('click', () => {
      const p = prompt('Новый 4-значный пин:'); if (p && /^\d{4}$/.test(p)) { state.pin = p; save(); alert('Готово!'); }
    });

    document.getElementById('goPublish').addEventListener('click', () => { renderPlatforms(); show('publish'); });
    document.getElementById('goCalendar').addEventListener('click', () => { renderCalendar(); show('calendar'); });
    document.getElementById('goNotes').addEventListener('click', () => { renderNotes(); show('notes'); });
    document.getElementById('goFinance').addEventListener('click', () => { renderFinance(); show('finance'); });
    document.getElementById('goSocial').addEventListener('click', () => { renderSocial(); show('social'); });
    document.getElementById('goGallery').addEventListener('click', () => { renderGallery(); show('gallery'); });
    document.getElementById('goFestivals').addEventListener('click', () => { renderFestivals(); show('festivals'); });
    document.getElementById('goSettings').addEventListener('click', () => { renderSettings(); show('settings'); });
    document.getElementById('backFromPublish').addEventListener('click', () => show('main'));
    document.getElementById('backFromCalendar').addEventListener('click', () => show('main'));
    document.getElementById('backFromNotes').addEventListener('click', () => show('main'));
    document.getElementById('backFromFinance').addEventListener('click', () => show('main'));
    document.getElementById('backFromSocial').addEventListener('click', () => show('main'));
    document.getElementById('backFromGallery').addEventListener('click', () => show('main'));
    document.getElementById('backFromFestivals').addEventListener('click', () => show('main'));
    document.getElementById('backFromSettings').addEventListener('click', () => show('main'));

    function renderPlatforms() {
      document.getElementById('platformCheckboxes').innerHTML = state.platforms.map(p => `<label><input type="checkbox" value="${p.id}"> ${p.name}</label>`).join('');
    }
    let selectedPhotos = [];
    document.getElementById('photoInput').addEventListener('change', function() {
      selectedPhotos = []; document.getElementById('photoPreview').innerHTML = '';
      Array.from(this.files).slice(0,8).forEach(f => {
        const r = new FileReader();
        r.onload = e => { selectedPhotos.push(e.target.result); const img = document.createElement('img'); img.src = e.target.result; document.getElementById('photoPreview').appendChild(img); };
        r.readAsDataURL(f);
      });
    });
    document.getElementById('startPublishBtn').addEventListener('click', async () => {
      const title = document.getElementById('postTitle').value.trim();
      if (!title) return alert('Введи название');
      const selected = [...document.querySelectorAll('#platformCheckboxes input:checked')].map(cb => cb.value);
      if (!selected.length) return alert('Выбери площадки');
      const progress = document.getElementById('publishProgress');
      progress.style.display = 'block';
      for (let i=0; i<selected.length; i++) {
        const plat = state.platforms.find(p => p.id === selected[i]);
        progress.innerHTML = `<p>📤 ${plat.name} (${i+1}/${selected.length})</p>`;
        const tagsStr = (document.getElementById('postTags').value||'').split(',').map(t => t.trim()).filter(t => t).map(t => t.startsWith('#') ? t : '#'+t).join(' ');
        const text = `${title}\n${document.getElementById('postDesc').value}\nЦена: ${document.getElementById('postPrice').value}₽\n${tagsStr}`;
        await navigator.clipboard.writeText(text);
        if (selectedPhotos.length) {
          try { const blob = await (await fetch(selectedPhotos[0])).blob(); await navigator.clipboard.write([new ClipboardItem({[blob.type]: blob})]); } catch(e){}
        }
        window.open(plat.url, '_blank');
        await new Promise(r => {
          const btn = document.createElement('button'); btn.textContent = '✅ Готово, дальше'; btn.className = 'btn';
          btn.onclick = () => { progress.removeChild(btn); r(); }; progress.appendChild(btn);
        });
      }
      progress.innerHTML = '<p style="color:#a0d6a0;">✅ Всё опубликовано!</p>';
    });

    function renderCalendar() {
      document.getElementById('monthLabel').textContent = new Date(state.currentYear, state.currentMonth).toLocaleDateString('ru', {month:'long', year:'numeric'});
      const firstDay = new Date(state.currentYear, state.currentMonth, 1).getDay() || 7;
      const daysInMonth = new Date(state.currentYear, state.currentMonth+1, 0).getDate();
      let html = ''; for (let i=1; i<firstDay; i++) html += '<span class="calendar-day"></span>';
      for (let d=1; d<=daysInMonth; d++) {
        const dateStr = `${state.currentYear}-${String(state.currentMonth+1).padStart(2,'0')}-${String(d).padStart(2,'0')}`;
        const isPast = new Date(dateStr) < new Date(new Date().toDateString());
        const isToday = dateStr === new Date().toISOString().slice(0,10);
        const hasEvent = state.events.some(e => e.date === dateStr);
        html += `<span class="calendar-day${isPast?' past':''}${isToday?' today':''}${hasEvent?' event':''}" data-date="${dateStr}">${d}</span>`;
      }
      document.getElementById('calendarDays').innerHTML = html;
      document.querySelectorAll('.calendar-day[data-date]').forEach(el => {
        el.addEventListener('click', function() {
          state.selectedDate = this.dataset.date;
          document.getElementById('eventInput').style.display = 'block';
        });
      });
      renderEventList();
    }
    function renderEventList() {
      const list = document.getElementById('eventList');
      const upcoming = state.events.filter(e => new Date(e.date) >= new Date().toDateString());
      upcoming.sort((a,b) => new Date(a.date) - new Date(b.date));
      list.innerHTML = upcoming.map((e, idx) => {
        const diff = Math.ceil((new Date(e.date) - new Date()) / 86400000);
        return `<div class="event-card" data-date="${e.date}" data-index="${idx}">
          <strong>Через ${diff} дн.: ${e.title}</strong>
          <div class="tools">
            <span style="cursor:pointer;" onclick="window.editEvent('${e.date}', ${idx})">✏️</span>
            <span style="cursor:pointer;" onclick="window.deleteEvent('${e.date}', ${idx})">🗑️</span>
          </div>
          <div class="event-checklist">
            ${(e.checklist||[]).map((item,i) => `<label><input type="checkbox" ${item.done?'checked':''} data-checkidx="${i}"> ${item.text}</label><br>`).join('')}
            <input type="text" class="new-checklist-item" placeholder="Новый пункт">
          </div>
        </div>`;
      }).join('');
      list.querySelectorAll('.event-card').forEach(card => {
        card.addEventListener('click', function(e) {
          if (e.target.tagName === 'INPUT' || e.target.tagName === 'LABEL' || e.target.closest('.tools')) return;
          const checklistDiv = this.querySelector('.event-checklist');
          checklistDiv.style.display = checklistDiv.style.display === 'block' ? 'none' : 'block';
        });
        card.querySelector('.new-checklist-item')?.addEventListener('keypress', function(e) {
          if (e.key === 'Enter') {
            const date = card.dataset.date;
            const idx = parseInt(card.dataset.index);
            const event = state.events.find((ev,i) => ev.date === date && i === idx);
            if (event) { event.checklist = event.checklist || []; event.checklist.push({text: this.value, done: false}); save(); renderEventList(); }
          }
        });
        card.querySelectorAll('input[type="checkbox"]').forEach(cb => {
          cb.addEventListener('change', function() {
            const date = card.dataset.date;
            const idx = parseInt(card.dataset.index);
            const event = state.events.find((ev,i) => ev.date === date && i === idx);
            if (event) { const checkIdx = parseInt(this.dataset.checkidx); event.checklist[checkIdx].done = this.checked; save(); }
          });
        });
      });
    }
    window.editEvent = function(date, idx) {
      const event = state.events.find((e,i) => e.date === date && i === idx);
      if (!event) return;
      const newTitle = prompt('Изменить название:', event.title);
      if (newTitle) { event.title = newTitle; const newDate = prompt('Изменить дату (гггг-мм-дд):', event.date); if (newDate && /^\d{4}-\d{2}-\d{2}$/.test(newDate)) event.date = newDate; save(); renderCalendar(); }
    };
    window.deleteEvent = function(date, idx) {
      state.events = state.events.filter((e,i) => !(e.date === date && i === idx)); save(); renderCalendar();
    };
    document.getElementById('saveEventBtn').addEventListener('click', () => {
      const title = document.getElementById('eventTitle').value.trim();
      if (title && state.selectedDate) { state.events.push({date: state.selectedDate, title, checklist: []}); save(); renderCalendar(); document.getElementById('eventInput').style.display='none'; document.getElementById('eventTitle').value=''; }
    });
    document.getElementById('prevMonth').addEventListener('click', () => {
      state.currentMonth--; if (state.currentMonth<0) { state.currentMonth=11; state.currentYear--; } renderCalendar();
    });
    document.getElementById('nextMonth').addEventListener('click', () => {
      state.currentMonth++; if (state.currentMonth>11) { state.currentMonth=0; state.currentYear++; } renderCalendar();
    });

    function renderNotes() {
      const days = [{ id:'mon', label:'Пн' }, { id:'tue', label:'Вт' }, { id:'wed', label:'Ср' }, { id:'thu', label:'Чт' }, { id:'fri', label:'Пт' }, { id:'sat', label:'Сб' }, { id:'sun', label:'Вс' }];
      const container = document.getElementById('notesContainer');
      container.innerHTML = '<div class="notes-grid"></div>';
      const grid = container.querySelector('.notes-grid');
      days.forEach(day => {
        const widget = document.createElement('div');
        widget.className = `note-widget${day.id==='sun'?' wide':''}`;
        widget.innerHTML = `<label>${day.label}</label><textarea id="note_${day.id}">${state.notes[day.id]||''}</textarea>`;
        grid.appendChild(widget);
      });
      grid.addEventListener('input', () => {
        days.forEach(d => { state.notes[d.id] = document.getElementById('note_'+d.id)?.value || ''; }); save();
      });
    }

    function getItemsForCategory(catName) {
      let results = [];
      function search(cat) {
        if (cat.name === catName || cat === catName) {
          results.push(...state.financeItems.filter(i => i.category === catName));
        }
        if (cat.sub) {
          cat.sub.forEach(sub => {
            if (typeof sub === 'string') {
              if (sub === catName) results.push(...state.financeItems.filter(i => i.category === sub));
            } else {
              search(sub);
              if (sub.name === catName) results.push(...state.financeItems.filter(i => i.category === sub.name));
            }
          });
        }
      }
      state.categories.forEach(c => search(c));
      return results;
    }

    function renderFinance() {
      const tree = document.getElementById('categoryTree');
      tree.innerHTML = '';
      function addCategory(cat, level = 0) {
        const div = document.createElement('div');
        div.className = `category-item${level===0 ? '' : (level===1 ? ' sub' : ' sub2')}${state.activeCategory === cat.name ? ' active' : ''}`;
        div.textContent = cat.name;
        div.dataset.cat = cat.name;
        div.addEventListener('click', (e) => { e.stopPropagation(); state.activeCategory = cat.name; renderFinance(); });
        tree.appendChild(div);
        if (cat.sub) {
          cat.sub.forEach(sub => {
            if (typeof sub === 'string') {
              const subDiv = document.createElement('div');
              subDiv.className = `category-item sub${level===0 ? '' : '2'}${state.activeCategory === sub ? ' active' : ''}`;
              subDiv.textContent = sub;
              subDiv.dataset.cat = sub;
              subDiv.addEventListener('click', (e) => { e.stopPropagation(); state.activeCategory = sub; renderFinance(); });
              tree.appendChild(subDiv);
            } else {
              addCategory(sub, level+1);
            }
          });
        }
      }
      state.categories.forEach(cat => addCategory(cat, 0));
      const items = state.activeCategory ? getItemsForCategory(state.activeCategory) : [];
      document.getElementById('itemTable').innerHTML = items.map(i => `
        <div class="item-row"><span>${i.name}</span><span>${i.cost}₽ / ${i.price}₽ (${Math.round(i.price/i.cost*100)||0}%)</span>${i.photo?`<img src="${i.photo}" style="width:40px;height:40px;border-radius:8px;">`:''}</div>
      `).join('');
    }
    document.getElementById('addItemBtn').addEventListener('click', () => {
      const name = document.getElementById('newItemName').value.trim();
      const cost = parseFloat(document.getElementById('newItemCost').value);
      const price = parseFloat(document.getElementById('newItemPrice').value);
      const photoInput = document.getElementById('newItemPhoto');
      if (name && !isNaN(cost) && !isNaN(price) && state.activeCategory) {
        const reader = new FileReader();
        const item = { name, cost, price, category: state.activeCategory, photo: null };
        if (photoInput.files.length) {
          reader.onload = e => { item.photo = e.target.result; state.financeItems.push(item); save(); renderFinance(); };
          reader.readAsDataURL(photoInput.files[0]);
        } else { state.financeItems.push(item); save(); renderFinance(); }
      }
    });

    function renderSocial() {
      document.getElementById('socialList').innerHTML = state.platforms.map(p => `
        <div class="social-card">
          <span>${p.name}</span>
          <button class="btn btn-outline" onclick="window.open('${p.url}')">Проверить</button>
        </div>
      `).join('');
    }

    function renderGallery() {
      const grid = document.getElementById('galleryGrid');
      let photos = state.financeItems.filter(i => i.photo).map(i => i.photo);
      grid.innerHTML = photos.length ? photos.map(p => `<img src="${p}" class="gallery-item">`).join('') : '<p>Галерея пуста. Добавь фото в финансы.</p>';
    }

    function renderFestivals() {
      const list = document.getElementById('festivalList');
      list.innerHTML = state.festivals.map((f, idx) => `
        <div class="festival-card">
          <strong>${f.name}</strong> (${f.date || 'дата не указана'})
          <div>Ссылка: <a href="${f.url}" target="_blank">${f.url}</a></div>
          <select onchange="window.updateFestStatus(${idx}, this.value)">
            ${state.festivalStatuses.map(s => `<option value="${s}" ${f.status===s?'selected':''}>${s}</option>`).join('')}
          </select>
          <button class="btn btn-outline" onclick="window.deleteFest(${idx})">Удалить</button>
        </div>
      `).join('');
    }
    window.updateFestStatus = function(idx, status) {
      state.festivals[idx].status = status; save(); renderFestivals();
    };
    window.deleteFest = function(idx) {
      state.festivals.splice(idx, 1); save(); renderFestivals();
    };
    document.getElementById('addFestBtn').addEventListener('click', () => {
      const name = document.getElementById('newFestName').value.trim();
      const url = document.getElementById('newFestUrl').value.trim();
      const date = document.getElementById('newFestDate').value;
      if (name && url) { state.festivals.push({ name, url, date, status: 'Планирую' }); save(); renderFestivals(); }
    });

    function renderSettings() {
      document.getElementById('customPlatforms').innerHTML = state.platforms.map(p => `<div>${p.name} (${p.url})</div>`).join('');
    }
    document.getElementById('addPlatformBtn').addEventListener('click', () => {
      const name = document.getElementById('newPlatformName').value.trim();
      const url = document.getElementById('newPlatformUrl').value.trim();
      if (name && url) { state.platforms.push({id:Date.now().toString(), name, url}); save(); renderSettings(); }
    });
    document.getElementById('changePinBtn').addEventListener('click', () => {
      const p = prompt('Новый пин:'); if (p && /^\d{4}$/.test(p)) { state.pin = p; save(); alert('Сменён!'); }
    });

    load(); show('auth');
  })();
</script>
</body>
</html>
