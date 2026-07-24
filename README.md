# elfcrafter.github.io
Popitka dva
<!DOCTYPE html>
<html lang="ru">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=yes, viewport-fit=cover">
  <meta name="theme-color" content="#1a1410">
  <meta name="apple-mobile-web-app-capable" content="yes">
  <title>🌸 Мастерская Эльфа</title>

  <link rel="manifest" href="data:application/json;base64,ewogICJuYW1lIjogItCc0LDRgdGC0LXRgNGB0LrQsNGPINCt0LvRjNGE0LAiLAogICJzaG9ydF9uYW1lIjogItCt0LvRjNGEIiwKICAic3RhcnRfdXJsIjogIi4iLAogICJkaXNwbGF5IjogInN0YW5kYWxvbmUiLAogICJiYWNrZ3JvdW5kX2NvbG9yIjogIiMxYTE0MTAiLAogICJ0aGVtZV9jb2xvciI6ICIjZDQ4YzViIiwKICAiaWNvbnMiOiBbCiAgICB7CiAgICAgICJzcmMiOiAiZGF0YTppbWFnZS9zdmcreG1sLCUzQ3N2ZyUyMHhtbG5zPSdodHRwOi8vd3d3LnczLm9yZy8yMDAwL3N2ZyclMjB2aWV3Qm94PScwIDAgMTAwIDEwMCclM0UlM0NjaXJjbGUlMjBjeD0nNTAnMjBjeT0nNTAnMjByPSc0OCclMjBmaWxsPSclMjMxYTE0MTAnMjBzdHJva2U9JyUyM2Q0OGM1YiclMjBzdHJva2Utd2lkdGg9JzQnLyUzRSUzQ3BhdGglMjBkPSdNMzAlMjA3MGwxMC0yMGgxMGwxMCUyMDIwSDQ1TTMwJTIwNDhsMTAtMjhoMTVsMTAlMjAyOGgtMTVsLTUtMTVINDBsLTUlMjAxNUgzMHonJTIwZmlsbD0nJTIzZDQ4YzViJyUyMHN0cm9rZT0nJTIzZDQ4YzViJyUyMHN0cm9rZS13aWR0aD0nMicvJTNFJTNDY2lyY2xlJTIwY3g9JzY1JTIwY3k9JzM1JTIwcj0nMTAnMjBmaWxsPSclMjNmZjMzMzMnLyUzRSUzQy9zdmclM0UiLAogICAgICAic2l6ZXMiOiAiMTkyeDE5MiIsCiAgICAgICJ0eXBlIjogImltYWdlL3N2Zy94bWwiCiAgICB9CiAgXQp9">

  <script>
    if ('serviceWorker' in navigator) {
      window.addEventListener('load', () => {
        navigator.serviceWorker.register('data:application/javascript,' + encodeURIComponent(
          `self.addEventListener('install', e => self.skipWaiting());
           self.addEventListener('activate', e => clients.claim());
           self.addEventListener('fetch', e => e.respondWith(fetch(e.request)));`
        ));
      });
    }
  </script>

  <style>
    * { margin:0; padding:0; box-sizing:border-box; }
    body {
      background: #1a1410;
      color: #e6d7c2;
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
      background: #231e18;
      border-radius: 36px;
      padding: 20px 16px;
      box-shadow: 0 20px 40px rgba(0,0,0,0.7);
      border: 1px solid #4a3b2f;
      position: relative;
      overflow: hidden;
    }
    .screen { display: none; flex-direction: column; }
    .screen.active { display: flex; }
    h2 {
      font-size: 1.6rem;
      color: #f0dbb0;
      margin-bottom: 16px;
      font-weight: 700;
      text-align: center;
    }
    .btn {
      background: #d48c5b;
      color: #1a1410;
      border: none;
      padding: 14px 20px;
      border-radius: 40px;
      font-weight: 700;
      font-size: 1rem;
      cursor: pointer;
      width: 100%;
      margin-top: 12px;
      transition: 0.2s;
    }
    .btn:hover { background: #f0b77c; }
    .btn-outline {
      background: transparent;
      border: 2px solid #5a4a38;
      color: #f0dbb0;
    }
    input, textarea {
      background: #1f1912;
      border: 1px solid #4a3b2f;
      border-radius: 16px;
      padding: 12px;
      color: #e6d7c2;
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
      color: #f0b77c;
      text-align: center;
      margin: 32px 0;
      animation: fadeIn 1s ease;
    }
    @keyframes fadeIn { from { opacity:0; transform: translateY(10px); } to { opacity:1; transform: translateY(0); } }

    /* Мандала */
    .mandala-grid {
      display: grid;
      grid-template-columns: 1fr 1.4fr 1fr;
      grid-template-rows: 1.2fr 1.4fr 1.2fr;
      gap: 12px;
      aspect-ratio: 1 / 1;
      max-width: 340px;
      margin: 20px auto;
    }
    .mandala-petal {
      background: #2a2119;
      border-radius: 30px;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      text-align: center;
      font-weight: 600;
      color: #f0dbb0;
      border: 1px solid #4a3b2f;
      transition: 0.2s;
      padding: 8px;
      font-size: 0.85rem;
      cursor: pointer;
      position: relative;
    }
    .mandala-petal:active { transform: scale(0.96); background: #3a2f22; }
    .mandala-petal .icon { font-size: 2rem; margin-bottom: 4px; }
    .mandala-petal.small { font-size: 0.7rem; border-radius: 22px; }
    .mandala-center {
      grid-column: 2; grid-row: 2;
      background: #d48c5b;
      border-radius: 50%;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 2.8rem;
      color: #1a1410;
      font-weight: 800;
      box-shadow: 0 0 25px #d48c5b60;
      cursor: pointer;
      transition: 0.2s;
      border: none;
    }
    .mandala-center:active { transform: scale(0.94); box-shadow: 0 0 35px #d48c5b; }

    .photo-preview { display: flex; gap: 8px; flex-wrap: wrap; margin: 8px 0; }
    .photo-preview img { width: 64px; height: 64px; object-fit: cover; border-radius: 12px; border: 2px solid #5a4a38; }
    .progress { background: #2a2119; border-radius: 20px; padding: 16px; margin: 16px 0; }
    .platform-list label { display: flex; align-items: center; gap: 8px; margin-bottom: 8px; }
    .calendar-day { display: inline-block; width: 32px; height: 32px; text-align: center; line-height: 32px; margin: 2px; border-radius: 8px; cursor: pointer; }
    .calendar-day.past { color: #5a4a38; text-decoration: line-through; }
    .calendar-day.today { background: #d48c5b; color: #1a1410; font-weight: bold; }
    .calendar-day.event { background: #3a4a3a; color: #b1e6b1; }
    .notes-list textarea { height: 60px; }
    .social-card { background: #2a2119; border-radius: 20px; padding: 12px; margin-bottom: 10px; display: flex; justify-content: space-between; align-items: center; }
  </style>
</head>
<body>
<div class="app" id="app">
  <!-- Аутентификация -->
  <div id="authScreen" class="screen active">
    <h2>🌸 Мастерская Эльфа</h2>
    <input type="password" id="pinInput" class="pin-input" maxlength="4" placeholder="····">
    <button class="btn" id="loginBtn">Войти</button>
    <button class="btn btn-outline" id="resetPinBtn">Сменить пин</button>
    <p style="color:#9c8a78; text-align:center; margin-top:12px;">Пин по умолчанию 1234</p>
  </div>

  <!-- Приветствие -->
  <div id="greetingScreen" class="screen">
    <div class="greeting" id="greetingText"></div>
  </div>

  <!-- Мандала (главный экран) -->
  <div id="mainScreen" class="screen">
    <div class="mandala-grid">
      <div class="mandala-petal" id="goCalendar" style="grid-column:2; grid-row:1;">
        <span class="icon">📅</span> Календарь
      </div>
      <div class="mandala-petal" id="goNotes" style="grid-column:1; grid-row:2;">
        <span class="icon">📝</span> Заметки
      </div>
      <div class="mandala-center" id="goPublish">＋</div>
      <div class="mandala-petal" id="goSettings" style="grid-column:3; grid-row:2;">
        <span class="icon">⚙️</span> Настройки
      </div>
      <div class="mandala-petal" id="goSocial" style="grid-column:2; grid-row:3;">
        <span class="icon">💬</span> Соцсети
      </div>
    </div>
  </div>

  <!-- Публикация -->
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

  <!-- Календарь -->
  <div id="calendarScreen" class="screen">
    <button class="btn btn-outline" id="backFromCalendar" style="width:auto; margin-bottom:12px;">← Назад</button>
    <h2>📅 Календарь событий</h2>
    <div style="display:flex; justify-content:space-between; margin-bottom:10px;">
      <button class="btn btn-outline" id="prevMonth" style="width:auto;">◀</button>
      <span id="monthLabel" style="font-weight:700;"></span>
      <button class="btn btn-outline" id="nextMonth" style="width:auto;">▶</button>
    </div>
    <div id="calendarDays" style="text-align:center;"></div>
    <div style="margin-top:12px;">
      <input type="text" id="eventTitle" placeholder="Название события">
      <input type="date" id="eventDate">
      <button class="btn" id="addEventBtn">Добавить</button>
    </div>
    <div id="upcomingEvents" style="margin-top:12px; color:#b8a68b;"></div>
  </div>

  <!-- Заметки -->
  <div id="notesScreen" class="screen">
    <button class="btn btn-outline" id="backFromNotes" style="width:auto; margin-bottom:12px;">← Назад</button>
    <h2>📝 Планы на неделю</h2>
    <div class="notes-list" id="notesContainer"></div>
  </div>

  <!-- Соцсети (агрегатор) -->
  <div id="socialScreen" class="screen">
    <button class="btn btn-outline" id="backFromSocial" style="width:auto; margin-bottom:12px;">← Назад</button>
    <h2>💬 Мои соцсети</h2>
    <div id="socialList"></div>
  </div>

  <!-- Настройки -->
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
    const STORAGE = 'craftsister_data';
    let state = {
      pin: '1234',
      platforms: [
        { id: 'vk', name: 'ВКонтакте', url: 'https://m.vk.com/write' },
        { id: 'avito', name: 'Авито', url: 'https://www.avito.ru/additem' },
        { id: 'youla', name: 'Юла', url: 'https://youla.ru/create' },
        { id: 'livemaster', name: 'Ярмарка Мастеров', url: 'https://www.livemaster.ru/add' },
        { id: 'meshok', name: 'Мешок', url: 'https://meshok.net/new_item' },
        { id: 'pikabu', name: 'Пикабу', url: 'https://pikabu.ru/add-post' },
        { id: 'instagram', name: 'Instagram', url: 'https://www.instagram.com/create/' }
      ],
      events: [],
      notes: { mon:'', tue:'', wed:'', thu:'', fri:'', sat:'', sun:'' },
      socialCounts: {},
      currentMonth: new Date().getMonth(),
      currentYear: new Date().getFullYear()
    };

    function load() {
      const saved = localStorage.getItem(STORAGE);
      if (saved) try { Object.assign(state, JSON.parse(saved)); } catch(e){}
      state.platforms.forEach(p => { if (!state.socialCounts[p.id]) state.socialCounts[p.id] = 0; });
    }
    function save() { localStorage.setItem(STORAGE, JSON.stringify(state)); }

    const screens = {
      auth: document.getElementById('authScreen'),
      greeting: document.getElementById('greetingScreen'),
      main: document.getElementById('mainScreen'),
      publish: document.getElementById('publishScreen'),
      calendar: document.getElementById('calendarScreen'),
      notes: document.getElementById('notesScreen'),
      social: document.getElementById('socialScreen'),
      settings: document.getElementById('settingsScreen')
    };
    function show(id) {
      Object.values(screens).forEach(s => s.classList.remove('active'));
      screens[id].classList.add('active');
    }

    // Пин-код
    document.getElementById('loginBtn').addEventListener('click', () => {
      if (document.getElementById('pinInput').value === state.pin) {
        const phrases = [
          'Привет! Что нового ты придумала?',
          'О, новые красивые штуки!',
          'Не волнуйся, мы найдём тебе заказы.',
          'Не бойся, я с тобой.',
          'Рисуй чаще, и чаща нарисует тебе.',
          'С возвращением, мастер Эльфа!',
          'Улыбнись, твои работы этого достойны.'
        ];
        document.getElementById('greetingText').textContent = phrases[Math.floor(Math.random() * phrases.length)];
        show('greeting');
        setTimeout(() => show('main'), 2500);
      } else alert('Неверный пин');
    });
    document.getElementById('resetPinBtn').addEventListener('click', () => {
      const p = prompt('Новый 4-значный пин:');
      if (p && /^\d{4}$/.test(p)) { state.pin = p; save(); alert('Готово!'); }
    });

    // Навигация с мандалы
    document.getElementById('goPublish').addEventListener('click', () => { renderPlatforms(); show('publish'); });
    document.getElementById('goCalendar').addEventListener('click', () => { renderCalendar(); show('calendar'); });
    document.getElementById('goNotes').addEventListener('click', () => { renderNotes(); show('notes'); });
    document.getElementById('goSocial').addEventListener('click', () => { renderSocial(); show('social'); });
    document.getElementById('goSettings').addEventListener('click', () => { renderSettings(); show('settings'); });

    // Кнопки назад
    document.getElementById('backFromPublish').addEventListener('click', () => show('main'));
    document.getElementById('backFromCalendar').addEventListener('click', () => show('main'));
    document.getElementById('backFromNotes').addEventListener('click', () => show('main'));
    document.getElementById('backFromSocial').addEventListener('click', () => show('main'));
    document.getElementById('backFromSettings').addEventListener('click', () => show('main'));

    // Публикация
    function renderPlatforms() {
      const div = document.getElementById('platformCheckboxes');
      div.innerHTML = state.platforms.map(p => `<label><input type="checkbox" value="${p.id}"> ${p.name}</label>`).join('');
    }
    let selectedPhotos = [];
    document.getElementById('photoInput').addEventListener('change', function() {
      selectedPhotos = [];
      document.getElementById('photoPreview').innerHTML = '';
      Array.from(this.files).slice(0,8).forEach(f => {
        const r = new FileReader();
        r.onload = e => { selectedPhotos.push(e.target.result); const img = document.createElement('img'); img.src = e.target.result; document.getElementById('photoPreview').appendChild(img); };
        r.readAsDataURL(f);
      });
    });
    document.getElementById('startPublishBtn').addEventListener('click', async () => {
      const title = document.getElementById('postTitle').value.trim();
      const desc = document.getElementById('postDesc').value.trim();
      const price = document.getElementById('postPrice').value;
      const tags = document.getElementById('postTags').value;
      if (!title) return alert('Введи название');
      const selected = [...document.querySelectorAll('#platformCheckboxes input:checked')].map(cb => cb.value);
      if (!selected.length) return alert('Выбери площадки');
      const progress = document.getElementById('publishProgress');
      progress.style.display = 'block';
      for (let i=0; i<selected.length; i++) {
        const plat = state.platforms.find(p => p.id === selected[i]);
        progress.innerHTML = `<p>📤 ${plat.name} (${i+1}/${selected.length})</p>`;
        const tagsStr = tags.split(',').map(t => t.trim()).filter(t => t).map(t => t.startsWith('#') ? t : '#'+t).join(' ');
        const text = `${title}\n${desc}\nЦена: ${price}₽\n${tagsStr}`;
        await navigator.clipboard.writeText(text);
        if (selectedPhotos.length) {
          try {
            const blob = await (await fetch(selectedPhotos[0])).blob();
            await navigator.clipboard.write([new ClipboardItem({[blob.type]: blob})]);
          } catch(e){}
        }
        window.open(plat.url, '_blank');
        await new Promise(r => {
          const btn = document.createElement('button');
          btn.textContent = '✅ Готово, дальше';
          btn.className = 'btn';
          btn.onclick = () => { progress.removeChild(btn); r(); };
          progress.appendChild(btn);
        });
      }
      progress.innerHTML = '<p style="color:#b1e6b1;">✅ Всё опубликовано!</p>';
    });

    // Календарь
    function renderCalendar() {
      const monthLabel = document.getElementById('monthLabel');
      const daysDiv = document.getElementById('calendarDays');
      const upcoming = document.getElementById('upcomingEvents');
      monthLabel.textContent = new Date(state.currentYear, state.currentMonth).toLocaleDateString('ru', {month:'long', year:'numeric'});
      const firstDay = new Date(state.currentYear, state.currentMonth, 1).getDay() || 7;
      const daysInMonth = new Date(state.currentYear, state.currentMonth+1, 0).getDate();
      let html = '';
      for (let i=1; i<firstDay; i++) html += '<span class="calendar-day"></span>';
      for (let d=1; d<=daysInMonth; d++) {
        const dateStr = `${state.currentYear}-${String(state.currentMonth+1).padStart(2,'0')}-${String(d).padStart(2,'0')}`;
        const isPast = new Date(dateStr) < new Date(new Date().toDateString());
        const isToday = dateStr === new Date().toISOString().slice(0,10);
        const event = state.events.find(e => e.date === dateStr);
        html += `<span class="calendar-day${isPast?' past':''}${isToday?' today':''}${event?' event':''}" title="${event?.title||''}">${d}</span>`;
      }
      daysDiv.innerHTML = html;
      upcoming.innerHTML = state.events.filter(e => new Date(e.date) >= new Date().toDateString()).map(e => {
        const diff = Math.ceil((new Date(e.date) - new Date()) / 86400000);
        return `<div>📌 ${e.title} — через ${diff} дн.</div>`;
      }).join('');
    }
    document.getElementById('prevMonth').addEventListener('click', () => {
      state.currentMonth--; if (state.currentMonth<0) { state.currentMonth=11; state.currentYear--; } renderCalendar();
    });
    document.getElementById('nextMonth').addEventListener('click', () => {
      state.currentMonth++; if (state.currentMonth>11) { state.currentMonth=0; state.currentYear++; } renderCalendar();
    });
    document.getElementById('addEventBtn').addEventListener('click', () => {
      const title = document.getElementById('eventTitle').value.trim();
      const date = document.getElementById('eventDate').value;
      if (title && date) { state.events.push({title, date}); save(); renderCalendar(); }
    });

    // Заметки
    function renderNotes() {
      const days = ['пн','вт','ср','чт','пт','сб','вс'];
      document.getElementById('notesContainer').innerHTML = days.map(d => `
        <label>${d.toUpperCase()}: <textarea id="note_${d}">${state.notes[d]||''}</textarea></label>
      `).join('');
    }
    document.getElementById('notesContainer').addEventListener('change', () => {
      ['mon','tue','wed','thu','fri','sat','sun'].forEach(d => {
        state.notes[d] = document.getElementById('note_'+d)?.value || '';
      });
      save();
    });

    // Соцсети
    function renderSocial() {
      document.getElementById('socialList').innerHTML = state.platforms.map(p => `
        <div class="social-card">
          <span>${p.name}</span>
          <span>Заказов: ${state.socialCounts[p.id]||0}</span>
          <button class="btn btn-outline" style="width:auto;" onclick="window.incSocial('${p.id}')">+1</button>
        </div>
      `).join('');
    }
    window.incSocial = function(id) {
      state.socialCounts[id] = (state.socialCounts[id]||0) + 1;
      save(); renderSocial();
    };

    // Настройки
    function renderSettings() {
      document.getElementById('customPlatforms').innerHTML = state.platforms.map(p => `<div>${p.name} (${p.url})</div>`).join('');
    }
    document.getElementById('addPlatformBtn').addEventListener('click', () => {
      const name = document.getElementById('newPlatformName').value.trim();
      const url = document.getElementById('newPlatformUrl').value.trim();
      if (name && url) { state.platforms.push({id:Date.now().toString(), name, url}); save(); renderSettings(); }
    });
    document.getElementById('changePinBtn').addEventListener('click', () => {
      const p = prompt('Новый пин:');
      if (p && /^\d{4}$/.test(p)) { state.pin = p; save(); alert('Сменён!'); }
    });

    load();
    show('auth');
  })();
</script>
</body>
</html>
