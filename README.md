<!DOCTYPE html>
<html lang="ru">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no, viewport-fit=cover">
  <meta name="apple-mobile-web-app-capable" content="yes">
  <meta name="theme-color" content="#0a0e1a">
  <title>Мастерская Эльфа</title>
  <style>
    * { margin:0; padding:0; box-sizing:border-box; -webkit-tap-highlight-color:transparent; user-select:none; }
    body { font-family:-apple-system,'Segoe UI',Roboto,Helvetica,Arial,sans-serif; background:#0a0e1a; color:#d0d9e6; height:100vh; width:100vw; overflow:hidden; position:fixed; }
    .app-container { width:100%; height:100%; position:relative; overflow:hidden; background:radial-gradient(ellipse at 30% 20%, #0f1a2e, #080c18); }
    .screen { position:absolute; top:0; left:0; width:100%; height:100%; padding:20px 16px 80px 16px; overflow-y:auto; opacity:0; pointer-events:none; transition:opacity 0.3s; background:transparent; }
    .screen.active { opacity:1; pointer-events:auto; }
    .screen-header { display:flex; align-items:center; gap:12px; padding:8px 0 16px 0; border-bottom:1px solid rgba(40,70,120,0.25); margin-bottom:16px; }
    .screen-header .back-btn { background:none; border:none; color:#6a8aaa; font-size:24px; cursor:pointer; }
    .screen-header .title { font-size:18px; font-weight:600; color:#c8dcee; }
    /* PIN */
    #pinScreen { display:flex; flex-direction:column; justify-content:center; align-items:center; background:radial-gradient(ellipse at center, #0f1a2e, #050810); opacity:1!important; pointer-events:auto!important; }
    #pinScreen.hidden { opacity:0!important; pointer-events:none!important; }
    .pin-logo { font-size:42px; margin-bottom:8px; }
    .pin-logo-text { font-size:22px; font-weight:300; color:#8ab4d6; letter-spacing:4px; margin-bottom:30px; }
    .pin-dots { display:flex; gap:20px; margin-bottom:32px; }
    .pin-dot { width:16px; height:16px; border-radius:50%; border:2px solid #3a5a7a; transition:0.2s; }
    .pin-dot.filled { background:#6a9ac8; border-color:#6a9ac8; }
    .pin-keypad { display:grid; grid-template-columns:repeat(3, 70px); gap:14px; margin-bottom:20px; }
    .pin-key { width:70px; height:70px; border-radius:50%; border:1px solid rgba(60,100,150,0.3); background:rgba(20,40,70,0.5); color:#b0cce6; font-size:26px; cursor:pointer; display:flex; align-items:center; justify-content:center; }
    .pin-key:active { background:rgba(60,120,200,0.3); }
    .pin-key.empty { background:transparent; border:none; pointer-events:none; }
    /* MANDALA */
    .mandala-grid { display:grid; grid-template-columns:1fr 1fr 1fr; grid-template-rows:1fr 1.6fr 1fr; gap:12px; max-width:400px; margin:20px auto; }
    .mandala-item { aspect-ratio:1; background:rgba(20,45,80,0.4); border-radius:20px; display:flex; flex-direction:column; align-items:center; justify-content:center; border:1px solid rgba(60,120,200,0.15); cursor:pointer; }
    .mandala-item .icon { font-size:28px; }
    .mandala-item .label { font-size:10px; color:#7a9aba; }
    .mandala-center { grid-column:2; grid-row:2; border-radius:50%; background:radial-gradient(circle, #1a3a5a, #0f1a2e); display:flex; align-items:center; justify-content:center; font-size:36px; color:#8ab4d6; border:2px solid rgba(80,160,240,0.3); cursor:pointer; }
    /* GREETING */
    .greeting-overlay { position:fixed; top:0; left:0; width:100%; height:100%; background:radial-gradient(ellipse at center, #0f1a2e, #050810); display:flex; align-items:center; justify-content:center; z-index:1000; opacity:0; pointer-events:none; transition:opacity 0.5s; }
    .greeting-overlay.show { opacity:1; pointer-events:auto; }
    .greeting-text { font-size:22px; color:#8ab4d6; text-align:center; padding:30px; font-weight:300; }
    /* UTILITY */
    .btn-primary { width:100%; padding:14px; background:linear-gradient(135deg, #1a4a7a, #0f2a4a); border:1px solid rgba(60,140,220,0.2); border-radius:14px; color:#c8dcee; font-size:16px; cursor:pointer; margin-top:8px; }
    .form-group { margin-bottom:16px; }
    .form-group label { display:block; font-size:12px; color:#6a8aaa; margin-bottom:4px; }
    .form-group input, .form-group textarea { width:100%; padding:12px; background:rgba(15,30,55,0.7); border:1px solid rgba(50,90,140,0.2); border-radius:12px; color:#d0d9e6; font-size:15px; outline:none; }
    .checkbox-grid { display:flex; flex-wrap:wrap; gap:8px; }
    .checkbox-item { display:flex; align-items:center; gap:6px; background:rgba(20,45,80,0.3); padding:6px 12px; border-radius:20px; border:1px solid rgba(50,90,140,0.15); font-size:13px; color:#8aabca; cursor:pointer; }
    .checkbox-item.active { background:rgba(40,100,180,0.25); border-color:rgba(80,160,240,0.4); color:#b0d0ee; }
    .checkbox-item .check { width:16px; height:16px; border-radius:4px; border:2px solid #4a6a8a; display:flex; align-items:center; justify-content:center; font-size:10px; }
    .checkbox-item.active .check { background:#4a8ac8; border-color:#4a8ac8; }
    .checkbox-item.active .check::after { content:'✓'; color:#fff; }
    .photo-upload-btn { display:inline-flex; align-items:center; gap:8px; padding:8px 16px; background:rgba(30,60,110,0.3); border:1px dashed rgba(60,120,200,0.3); border-radius:12px; color:#6a8aaa; cursor:pointer; font-size:13px; }
    .photo-preview-grid { display:flex; flex-wrap:wrap; gap:8px; margin-top:8px; }
    .photo-preview { width:60px; height:60px; border-radius:10px; object-fit:cover; }
    .text-muted { color:#4a5a7a; font-size:13px; }
    .text-center { text-align:center; }
  </style>
</head>
<body>
<div class="greeting-overlay" id="greetingOverlay">
  <div class="greeting-text" id="greetingText">Рисуй чаще, и чаща нарисует тебе</div>
</div>

<div class="app-container" id="appContainer">
  <!-- PIN -->
  <div class="screen" id="pinScreen">
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

  <!-- MANDALA (остальные экраны для краткости опущены, но они будут добавлены через JS) -->
  <div class="screen" id="mandalaScreen">
    <div class="screen-header"><div class="title">Мастерская Эльфа</div></div>
    <div class="mandala-grid" id="mandalaGrid"></div>
  </div>
</div>

<script>
  // Базовая инициализация, которая точно сработает
  alert('Скрипт запущен! Если вы это видите, код работает.');
  
  // Строим мандалу
  const mandalaGrid = document.getElementById('mandalaGrid');
  const items = [
    { icon:'📅', label:'Календарь' },
    { icon:'🎪', label:'Фестивали' },
    { icon:'📝', label:'Заметки' },
    { icon:'⚙️', label:'Настройки' },
    { icon:'＋', label:'', isCenter:true },
    { icon:'💰', label:'Финансы' },
    { icon:'🌐', label:'Соцсети' },
    { icon:'🖼️', label:'Галерея' }
  ];
  
  items.forEach(item => {
    const div = document.createElement('div');
    if (item.isCenter) {
      div.className = 'mandala-center';
      div.textContent = item.icon;
    } else {
      div.className = 'mandala-item';
      div.innerHTML = `<span class="icon">${item.icon}</span><span class="label">${item.label}</span>`;
    }
    mandalaGrid.appendChild(div);
  });

  // Пин-код
  const PIN = '1234';
  let buffer = '';
  const dots = document.querySelectorAll('.pin-dot');
  
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
          document.getElementById('pinScreen').classList.add('hidden');
          document.getElementById('mandalaScreen').classList.add('active');
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
