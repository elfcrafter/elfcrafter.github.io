# elfcrafter.github.io
Popitka dva
<!DOCTYPE html>
<html lang="ru">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=yes, viewport-fit=cover">
  <meta name="theme-color" content="#1a1410">
  <meta name="apple-mobile-web-app-capable" content="yes">
  <title>🎨 CraftSister</title>

  <link rel="manifest" href="data:application/json;base64,ewogICJuYW1lIjogIkNyYWZ0U2lzdGVyIiwKICAic2hvcnRfbmFtZSI6ICJDcmFmdFNpc3RlciIsCiAgInN0YXJ0X3VybCI6ICIuIiwKICAiZGlzcGxheSI6ICJzdGFuZGFsb25lIiwKICAiYmFja2dyb3VuZF9jb2xvciI6ICIjMWExNDEwIiwKICAidGhlbWVfY29sb3IiOiAiI2Q0OGM1YiIsCiAgImljb25zIjogWwogICAgewogICAgICAic3JjIjogImRhdGE6aW1hZ2Uvc3ZnK3htbCwlM0NzdmclMjB4bWxucz0naHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmcnJTIwdmlld0JveD0nMCAwIDEwMCAxMDAnJTNFJTNDY2lyY2xlJTIwY3g9JzUwJyUyMGN5PSc1MCclMjByPSc0OCclMjBmaWxsPSclMjMxYTE0MTAnJTIwc3Ryb2tlPSclMjNkNDhjNWInJTIwc3Ryb2tlLXdpZHRoPSc0Jy8lM0UlM0NwYXRoJTIwZD0nTTMwJTIwNzBsMTAtMjBoMTBsMTAlMjAyMEg0NU0zMCUyMDQ4bDEwLTI4aDE1bDEwJTIwMjhoLTE1bC01LTE1SDQwbC01JTIwMTVIMzB6JyUyMGZpbGw9JyUyM2Q0OGM1YiclMjBzdHJva2U9JyUyM2Q0OGM1YiclMjBzdHJva2Utd2lkdGg9JzInLyUzRSUzQ2NpcmNsZSUyMGN4PSc2NScyMGN5PSczNSUyMHI9JzEwJyUyMGZpbGw9JyUyM2ZmMzMzMycvJTNFJTNDL3N2ZyUzRSIsCiAgICAgICJzaXplcyI6ICIxOTJ4MTkyIiwKICAgICAgInR5cGUiOiAiaW1hZ2Uvc3ZnK3htbCIKICAgIH0KICBdCn0=">

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
      padding: 16px;
    }
    .app {
      max-width: 420px;
      width: 100%;
      background: #231e18;
      border-radius: 32px;
      padding: 24px 20px;
      box-shadow: 0 20px 40px rgba(0,0,0,0.7);
      border: 1px solid #4a3b2f;
    }
    .screen { display: none; }
    .screen.active { display: block; }
    h2 {
      font-size: 1.8rem;
      color: #f0dbb0;
      margin-bottom: 16px;
      font-weight: 700;
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
    input, textarea, select {
      background: #1f1912;
      border: 1px solid #4a3b2f;
      border-radius: 16px;
      padding: 12px;
      color: #e6d7c2;
      font-size: 1rem;
      width: 100%;
      margin-bottom: 12px;
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
    .photo-preview { display: flex; gap: 8px; flex-wrap: wrap; margin: 8px 0; }
    .photo-preview img { width: 70px; height: 70px; object-fit: cover; border-radius: 12px; border: 2px solid #5a4a38; }
    .platform-list { margin: 12px 0; }
    .progress { background: #2a2119; border-radius: 20px; padding: 16px; margin: 16px 0; }
    .step { display: flex; justify-content: space-between; align-items: center; padding: 8px 0; }
    .add-platform { display: flex; gap: 8px; margin-top: 8px; }
  </style>
</head>
<body>
<div class="app" id="app">
  <!-- Экран пина / приветствия -->
  <div id="authScreen" class="screen active">
    <h2>🔐 Вход в мастерскую</h2>
    <input type="password" id="pinInput" class="pin-input" maxlength="4" placeholder="····">
    <button class="btn" id="loginBtn">Войти</button>
    <button class="btn btn-outline" id="resetPinBtn" style="margin-top:8px;">Сменить пин</button>
    <p style="color:#9c8a78; text-align:center; margin-top:16px;">Подсказка: пин по умолчанию 1234</p>
  </div>

  <!-- Экран заботливого приветствия -->
  <div id="greetingScreen" class="screen">
    <div class="greeting" id="greetingText"></div>
  </div>

  <!-- Основной экран: чеклист и рассылка -->
  <div id="mainScreen" class="screen">
    <h2>📢 Новая публикация</h2>
    <input type="text" id="postTitle" placeholder="Название изделия">
    <textarea id="postDesc" placeholder="Описание, материалы, вдохновение..." rows="3"></textarea>
    <input type="number" id="postPrice" placeholder="Цена (₽)">
    <input type="text" id="postTags" placeholder="Хештеги через запятую (без #)">
    <div style="margin:8px 0;">
      <label>📎 Фото (до 8):</label>
      <input type="file" id="photoInput" accept="image/*" multiple style="display:none;">
      <button class="btn btn-outline" onclick="document.getElementById('photoInput').click()" style="margin-top:4px;">Выбрать фото</button>
      <div class="photo-preview" id="photoPreview"></div>
    </div>
    <div class="platform-list">
      <p style="color:#b8a68b;">Выбери площадки:</p>
      <div id="platformCheckboxes"></div>
      <div class="add-platform">
        <input type="text" id="newPlatformName" placeholder="Название">
        <input type="text" id="newPlatformUrl" placeholder="Ссылка">
        <button class="btn" id="addPlatformBtn" style="width:auto; margin-top:0;">+</button>
      </div>
    </div>
    <button class="btn" id="startPublishBtn">🚀 Начать рассылку</button>
    <div id="publishProgress" class="progress" style="display:none;"></div>
  </div>
</div>

<script>
  (function() {
    const STORAGE_KEY = 'craftsister';
    let state = {
      pin: null,
      post: { title: '', desc: '', price: '', tags: '', photos: [] },
      selectedPlatforms: [],
      currentStep: 0,
      platforms: [
        { id: 'vk', name: 'ВКонтакте', url: 'https://m.vk.com/write' },
        { id: 'avito', name: 'Авито', url: 'https://www.avito.ru/additem' },
        { id: 'youla', name: 'Юла', url: 'https://youla.ru/create' },
        { id: 'livemaster', name: 'Ярмарка Мастеров', url: 'https://www.livemaster.ru/add' },
        { id: 'artallery', name: 'Арт-площадка', url: 'https://artallery.ru' },
        { id: 'meshok', name: 'Мешок', url: 'https://meshok.net/new_item' },
        { id: 'pikabu', name: 'Пикабу', url: 'https://pikabu.ru/add-post' }
      ]
    };

    function loadState() {
      const saved = localStorage.getItem(STORAGE_KEY);
      if (saved) {
        try { const parsed = JSON.parse(saved); state.pin = parsed.pin; } catch(e){}
      }
      if (!state.pin) state.pin = '1234';
    }
    function saveState() {
      localStorage.setItem(STORAGE_KEY, JSON.stringify({ pin: state.pin }));
    }

    const authScreen = document.getElementById('authScreen');
    const greetingScreen = document.getElementById('greetingScreen');
    const mainScreen = document.getElementById('mainScreen');

    function showScreen(screen) {
      [authScreen, greetingScreen, mainScreen].forEach(s => s.classList.remove('active'));
      screen.classList.add('active');
    }

    const pinInput = document.getElementById('pinInput');
    document.getElementById('loginBtn').addEventListener('click', () => {
      if (pinInput.value.trim() === state.pin) showGreeting();
      else alert('Неверный пин, попробуй ещё раз');
    });

    document.getElementById('resetPinBtn').addEventListener('click', () => {
      const newPin = prompt('Введи новый 4-значный пин:');
      if (newPin && /^\d{4}$/.test(newPin)) {
        state.pin = newPin;
        saveState();
        alert('Пин обновлён!');
      } else {
        alert('Пин должен быть из 4 цифр.');
      }
    });

    const greetings = [
      'Привет! Что нового ты придумала?',
      'О, новые красивые штуки!',
      'Не волнуйся, мы найдём тебе заказы.',
      'Не бойся, я с тобой.',
      'С возвращением, мастер! Готова творить?',
      'Ты сегодня прекрасна, как свежая эпоксидка.',
      'Улыбнись, твои работы этого достойны.'
    ];

    function showGreeting() {
      document.getElementById('greetingText').textContent = greetings[Math.floor(Math.random() * greetings.length)];
      showScreen(greetingScreen);
      setTimeout(() => {
        showScreen(mainScreen);
        renderPlatforms();
      }, 2500);
    }

    function renderPlatforms() {
      const container = document.getElementById('platformCheckboxes');
      container.innerHTML = state.platforms.map(p => `
        <label style="display:flex; align-items:center; gap:8px; margin-bottom:8px;">
          <input type="checkbox" value="${p.id}" ${state.selectedPlatforms.includes(p.id) ? 'checked' : ''}>
          ${p.name}
        </label>
      `).join('');
      container.querySelectorAll('input').forEach(cb => {
        cb.addEventListener('change', () => {
          state.selectedPlatforms = [...container.querySelectorAll('input:checked')].map(cb => cb.value);
        });
      });
      state.selectedPlatforms = [...container.querySelectorAll('input:checked')].map(cb => cb.value);
    }

    document.getElementById('addPlatformBtn').addEventListener('click', () => {
      const name = document.getElementById('newPlatformName').value.trim();
      const url = document.getElementById('newPlatformUrl').value.trim();
      if (name && url) {
        state.platforms.push({ id: Date.now().toString(), name, url });
        renderPlatforms();
        document.getElementById('newPlatformName').value = '';
        document.getElementById('newPlatformUrl').value = '';
      }
    });

    const photoInput = document.getElementById('photoInput');
    const photoPreview = document.getElementById('photoPreview');
    photoInput.addEventListener('change', () => {
      const files = Array.from(photoInput.files).slice(0, 8);
      state.post.photos = [];
      photoPreview.innerHTML = '';
      files.forEach(file => {
        const reader = new FileReader();
        reader.onload = (e) => {
          state.post.photos.push(e.target.result);
          const img = document.createElement('img');
          img.src = e.target.result;
          photoPreview.appendChild(img);
        };
        reader.readAsDataURL(file);
      });
    });

    document.getElementById('startPublishBtn').addEventListener('click', () => {
      state.post.title = document.getElementById('postTitle').value.trim();
      state.post.desc = document.getElementById('postDesc').value.trim();
      state.post.price = document.getElementById('postPrice').value.trim();
      state.post.tags = document.getElementById('postTags').value.trim();

      if (!state.post.title) return alert('Введи название изделия');
      if (state.selectedPlatforms.length === 0) return alert('Выбери хотя бы одну площадку');

      state.currentStep = 0;
      document.getElementById('publishProgress').style.display = 'block';
      showNextPlatform();
    });

    function showNextPlatform() {
      const progressDiv = document.getElementById('publishProgress');
      if (state.currentStep >= state.selectedPlatforms.length) {
        progressDiv.innerHTML = '<p style="color:#b1e6b1;">✅ Все площадки обработаны! Ты умница.</p>';
        return;
      }
      const platformId = state.selectedPlatforms[state.currentStep];
      const platform = state.platforms.find(p => p.id === platformId);
      progressDiv.innerHTML = `<div class="step"><span>📤 ${platform.name}</span><span>${state.currentStep+1}/${state.selectedPlatforms.length}</span></div>`;
      copyToClipboard(platform).then(() => {
        window.open(platform.url, '_blank');
        progressDiv.innerHTML += `<button class="btn" id="nextStepBtn">✅ Готово, следующая</button>`;
        document.getElementById('nextStepBtn').addEventListener('click', () => {
          state.currentStep++;
          showNextPlatform();
        });
      });
    }

    async function copyToClipboard(platform) {
      const tagsFormatted = state.post.tags.split(',').map(t => t.trim()).filter(t => t).map(t => t.startsWith('#') ? t : '#' + t).join(' ');
      const text = `${state.post.title}\n${state.post.desc}\nЦена: ${state.post.price}₽\n${tagsFormatted}`;
      try {
        await navigator.clipboard.writeText(text);
        if (state.post.photos.length > 0) {
          const imgBlob = await (await fetch(state.post.photos[0])).blob();
          await navigator.clipboard.write([new ClipboardItem({ [imgBlob.type]: imgBlob })]);
        }
      } catch (err) {}
    }

    loadState();
    showScreen(authScreen);
    pinInput.focus();
    const observer = new MutationObserver(() => {
      if (mainScreen.classList.contains('active')) renderPlatforms();
    });
    observer.observe(mainScreen, { attributes: true, attributeFilter: ['class'] });
  })();
</script>
</body>
</html>
