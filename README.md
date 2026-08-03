<!DOCTYPE html>
<html lang="ru">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no, viewport-fit=cover">
  <meta name="apple-mobile-web-app-capable" content="yes">
  <meta name="theme-color" content="#0a0e1a">
  <title>Мастерская Эльфа</title>
  <style>
    * { margin:0; padding:0; box-sizing:border-box; -webkit-tap-highlight-color:transparent; }
    body {
      font-family: -apple-system, 'Segoe UI', Roboto, Helvetica, Arial, sans-serif;
      background: #0a0e1a;
      color: #d0d9e6;
      min-height: 100vh;
      /* больше не фиксируем высоту и не скрываем скролл */
    }
    .app-container {
      width: 100%;
      min-height: 100vh;
      background: radial-gradient(ellipse at 30% 20%, #0f1a2e, #080c18);
    }
    .screen {
      display: none;
      width: 100%;
      min-height: 100vh;
      padding: 20px 16px;
    }
    .screen.active {
      display: flex;
      flex-direction: column;
    }
    /* PIN */
    #pinScreen {
      justify-content: center;
      align-items: center;
      background: radial-gradient(ellipse at center, #0f1a2e, #050810);
    }
    .pin-logo { font-size: 42px; margin-bottom: 8px; }
    .pin-logo-text {
      font-size: 22px; font-weight: 300; color: #8ab4d6;
      letter-spacing: 4px; margin-bottom: 30px;
    }
    .pin-dots { display: flex; gap: 20px; margin-bottom: 32px; }
    .pin-dot {
      width: 16px; height: 16px; border-radius: 50%;
      border: 2px solid #3a5a7a; transition: 0.2s;
    }
    .pin-dot.filled { background: #6a9ac8; border-color: #6a9ac8; }
    .pin-keypad { display: grid; grid-template-columns: repeat(3, 70px); gap: 14px; margin-bottom: 20px; }
    .pin-key {
      width: 70px; height: 70px; border-radius: 6px; /* строгие углы */
      border: 1px solid rgba(60,100,150,0.3);
      background: rgba(20,40,70,0.5); color: #b0cce6;
      font-size: 26px; cursor: pointer;
      display: flex; align-items: center; justify-content: center;
    }
    .pin-key:active { background: rgba(60,120,200,0.3); }
    .pin-key.empty { background: transparent; border: none; pointer-events: none; }

    /* MANDALA – прямоугольные плитки */
    .mandala-grid {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      grid-auto-rows: auto;
      gap: 10px; /* меньше воздуха */
      max-width: 400px;
      margin: 0 auto;
    }
    .mandala-item {
      aspect-ratio: 1 / 1; /* квадратные */
      background: rgba(20,45,80,0.4);
      border-radius: 6px; /* строгий минимальный радиус */
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      border: 1px solid rgba(60,120,200,0.15);
      cursor: pointer;
      transition: background 0.2s;
      padding: 8px;
    }
    .mandala-item:active { background: rgba(40,80,140,0.3); }
    .mandala-item .icon { font-size: 28px; margin-bottom: 4px; }
    .mandala-item .label { font-size: 11px; color: #7a9aba; font-weight: 400; text-align: center; }
    .mandala-center {
      grid-column: 2; grid-row: 2;
      aspect-ratio: 1 / 1;
      background: radial-gradient(circle, #1a3a5a, #0f1a2e);
      border-radius: 6px;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 36px;
      color: #8ab4d6;
      border: 1px solid rgba(80,160,240,0.3);
      cursor: pointer;
    }
    .mandala-center:active { background: rgba(60,150,255,0.2); }
  </style>
</head>
<body>
<div class="app-container" id="appContainer">
  <!-- PIN SCREEN -->
  <div class="screen active" id="pinScreen">
    <div class="pin-logo">✧</div>
    <div class="pin-logo-text">Мастерская Эльфа</div>
    <div class="pin-dots" id="pinDots">
      <div class="pin-dot"></div><div class="pin-dot"></div><div class="pin-dot"></div><div class="pin-dot"></div>
    </div>
    <div class="pin-keypad" id="pinKeypad">
      <button class="pin-key" data-value="1">1</button>
      <button class="pin-key" data-value="2">2</button>
      <button class="pin-key" data-value="3">3</button>
      <button class="pin-key" data-value="4">4</button>
      <button class="pin-key" data-value="5">5</button>
      <button class="pin-key" data-value="6">6</button>
      <button class="pin-key" data-value="7">7</button>
      <button class="pin-key" data-value="8">8</button>
      <button class="pin-key" data-value="9">9</button>
      <button class="pin-key empty"></button>
      <button class="pin-key" data-value="0">0</button>
      <button class="pin-key" data-value="del">⌫</button>
    </div>
  </div>

  <!-- MANDALA SCREEN -->
  <div class="screen" id="mandalaScreen">
    <div class="mandala-grid">
      <div class="mandala-item"><span class="icon">📅</span><span class="label">Календарь</span></div>
      <div class="mandala-item"><span class="icon">🎪</span><span class="label">Фестивали</span></div>
      <div class="mandala-item"><span class="icon">📝</span><span class="label">Заметки</span></div>
      <div class="mandala-item"><span class="icon">⚙️</span><span class="label">Настройки</span></div>
      <div class="mandala-center" id="centerPlus">＋</div>
      <div class="mandala-item"><span class="icon">💰</span><span class="label">Финансы</span></div>
      <div class="mandala-item"><span class="icon">🌐</span><span class="label">Мои соцсети</span></div>
      <div class="mandala-item"><span class="icon">🖼️</span><span class="label">Галерея</span></div>
    </div>
  </div>
</div>

<script>
  const PIN = '1234';
  let buffer = '';
  const dots = document.querySelectorAll('.pin-dot');
  const pinScreen = document.getElementById('pinScreen');
  const mandalaScreen = document.getElementById('mandalaScreen');

  function updateDots() {
    dots.forEach((d, i) => d.classList.toggle('filled', i < buffer.length));
  }

  document.querySelectorAll('.pin-key[data-value]').forEach(btn => {
    btn.addEventListener('click', () => {
      const val = btn.dataset.value;
      if (val === 'del') { buffer = buffer.slice(0, -1); updateDots(); return; }
      if (buffer.length >= 4) return;
      buffer += val;
      updateDots();
      if (buffer.length === 4) {
        if (buffer === PIN) {
          pinScreen.classList.remove('active');
          mandalaScreen.classList.add('active');
        } else {
          alert('Неверный пин');
          buffer = '';
          updateDots();
        }
      }
    });
  });
</script>
</body>
</html>
