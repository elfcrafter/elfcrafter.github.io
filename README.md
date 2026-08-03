<!DOCTYPE html>
<html lang="ru">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no, viewport-fit=cover">
  <title>Мастерская Эльфа</title>
  <style>
    * { margin:0; padding:0; box-sizing:border-box; }
    body { background:#0a0e1a; color:#d0d9e6; font-family:-apple-system,sans-serif; height:100vh; overflow:hidden; }
    .screen { position:absolute; top:0; left:0; width:100%; height:100%; padding:20px; display:none; }
    .screen.active { display:flex; flex-direction:column; }
    #pinScreen { display:flex; flex-direction:column; justify-content:center; align-items:center; background:radial-gradient(ellipse at center, #0f1a2e, #050810); }
    #pinScreen.hidden { display:none; }
    .pin-logo { font-size:42px; margin-bottom:8px; }
    .pin-logo-text { font-size:22px; font-weight:300; color:#8ab4d6; letter-spacing:4px; margin-bottom:30px; }
    .pin-dots { display:flex; gap:20px; margin-bottom:32px; }
    .pin-dot { width:16px; height:16px; border-radius:50%; border:2px solid #3a5a7a; }
    .pin-dot.filled { background:#6a9ac8; border-color:#6a9ac8; }
    .pin-keypad { display:grid; grid-template-columns:repeat(3, 70px); gap:14px; }
    .pin-key { width:70px; height:70px; border-radius:50%; border:1px solid rgba(60,100,150,0.3); background:rgba(20,40,70,0.5); color:#b0cce6; font-size:26px; cursor:pointer; display:flex; align-items:center; justify-content:center; }
    .pin-key.empty { background:transparent; border:none; pointer-events:none; }
    /* Мандала */
    .mandala-grid { display:grid; grid-template-columns:1fr 1fr 1fr; grid-template-rows:1fr 1.6fr 1fr; gap:12px; max-width:400px; margin:auto; }
    .mandala-item { aspect-ratio:1; background:rgba(20,45,80,0.4); border-radius:20px; display:flex; flex-direction:column; align-items:center; justify-content:center; border:1px solid rgba(60,120,200,0.15); cursor:pointer; }
    .mandala-center { grid-column:2; grid-row:2; border-radius:50%; background:radial-gradient(circle, #1a3a5a, #0f1a2e); display:flex; align-items:center; justify-content:center; font-size:36px; color:#8ab4d6; border:2px solid rgba(80,160,240,0.3); cursor:pointer; }
    .icon { font-size:28px; }
    .label { font-size:10px; color:#7a9aba; margin-top:4px; }
  </style>
</head>
<body>

<!-- ПИН-ЭКРАН -->
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

<!-- МАНДАЛА (статическая) -->
<div class="screen" id="mandalaScreen">
  <div class="mandala-grid">
    <div class="mandala-item"><span class="icon">📅</span><span class="label">Календарь</span></div>
    <div class="mandala-item"><span class="icon">🎪</span><span class="label">Фестивали</span></div>
    <div class="mandala-item"><span class="icon">📝</span><span class="label">Заметки</span></div>
    <div class="mandala-item"><span class="icon">⚙️</span><span class="label">Настройки</span></div>
    <div class="mandala-center">＋</div>
    <div class="mandala-item"><span class="icon">💰</span><span class="label">Финансы</span></div>
    <div class="mandala-item"><span class="icon">🌐</span><span class="label">Мои соцсети</span></div>
    <div class="mandala-item"><span class="icon">🖼️</span><span class="label">Галерея</span></div>
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
          pinScreen.classList.add('hidden');
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
