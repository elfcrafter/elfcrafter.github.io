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
      width: 70px; height: 70px; border-radius: 6px;
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
      gap: 10px;
      max-width: 400px;
      margin: 0 auto;
    }
    .mandala-item {
      aspect-ratio: 1 / 1;
      background: rgba(20,45,80,0.4);
      border-radius: 6px;
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

    /* SCREEN HEADER */
    .screen-header {
      display: flex;
      align-items: center;
      gap: 12px;
      margin-bottom: 16px;
      border-bottom: 1px solid rgba(40,70,120,0.25);
      padding-bottom: 12px;
    }
    .screen-header .back-btn {
      background: none; border: none; color: #6a8aaa;
      font-size: 24px; cursor: pointer;
    }
    .screen-header .title { font-size: 18px; font-weight: 600; color: #c8dcee; }

    /* FORMS */
    .form-group { margin-bottom: 16px; }
    .form-group label { display: block; font-size: 12px; color: #6a8aaa; margin-bottom: 4px; }
    .form-group input, .form-group textarea {
      width: 100%; padding: 12px;
      background: rgba(15,30,55,0.7);
      border: 1px solid rgba(50,90,140,0.2);
      border-radius: 6px;
      color: #d0d9e6; font-size: 15px; outline: none;
      font-family: inherit;
    }
    .form-group textarea { resize: vertical; min-height: 70px; }
    .checkbox-grid { display: flex; flex-wrap: wrap; gap: 8px; }
    .checkbox-item {
      display: flex; align-items: center; gap: 6px;
      background: rgba(20,45,80,0.3); padding: 6px 12px;
      border-radius: 20px; border: 1px solid rgba(50,90,140,0.15);
      font-size: 13px; color: #8aabca; cursor: pointer;
    }
    .checkbox-item.active { background: rgba(40,100,180,0.25); border-color: rgba(80,160,240,0.4); color: #b0d0ee; }
    .checkbox-item .check {
      width: 16px; height: 16px; border-radius: 4px;
      border: 2px solid #4a6a8a; display: flex; align-items: center; justify-content: center;
      font-size: 10px;
    }
    .checkbox-item.active .check { background: #4a8ac8; border-color: #4a8ac8; }
    .checkbox-item.active .check::after { content: '✓'; color: #fff; }
    .photo-upload-btn {
      display: inline-flex; align-items: center; gap: 8px;
      padding: 8px 16px; background: rgba(30,60,110,0.3);
      border: 1px dashed rgba(60,120,200,0.3); border-radius: 6px;
      color: #6a8aaa; cursor: pointer; font-size: 13px;
    }
    .photo-preview-grid { display: flex; flex-wrap: wrap; gap: 8px; margin-top: 8px; }
    .photo-preview { width: 60px; height: 60px; border-radius: 6px; object-fit: cover; }

    .btn-primary {
      width: 100%; padding: 14px;
      background: linear-gradient(135deg, #1a4a7a, #0f2a4a);
      border: 1px solid rgba(60,140,220,0.2); border-radius: 6px;
      color: #c8dcee; font-size: 16px; font-weight: 500;
      cursor: pointer; margin-top: 8px; transition: background 0.2s;
    }
    .btn-primary:active { background: linear-gradient(135deg, #1a5a8a, #0f2a5a); }

    /* FINANCE */
    .finance-container { display: flex; flex-direction: column; gap: 12px; }
    .finance-tree {
      background: rgba(10,25,50,0.5); border-radius: 6px;
      padding: 12px; max-height: 200px; overflow-y: auto;
      border: 1px solid rgba(40,80,130,0.15);
    }
    .finance-tree .folder {
      padding: 6px 8px; cursor: pointer; border-radius: 6px;
      font-size: 14px; display: flex; align-items: center; gap: 8px;
    }
    .finance-tree .folder:active { background: rgba(40,80,160,0.2); }
    .finance-tree .folder.selected { background: rgba(40,80,160,0.25); color: #b0d0ee; }
    .finance-tree .folder .arrow { font-size: 10px; transition: transform 0.2s; color: #4a6a8a; }
    .finance-tree .folder .arrow.open { transform: rotate(90deg); }
    .finance-tree .children { padding-left: 20px; }
    .finance-items {
      background: rgba(10,25,50,0.3); border-radius: 6px;
      padding: 12px; overflow-y: auto; border: 1px solid rgba(40,80,130,0.1);
      min-height: 80px;
    }
    .finance-items .item-row {
      display: grid; grid-template-columns: 1fr 60px 60px 50px 40px; gap: 4px;
      padding: 6px 4px; font-size: 12px;
      border-bottom: 1px solid rgba(40,80,130,0.08); align-items: center;
    }
    .finance-items .item-row .name { color: #b0cce6; white-space: nowrap; overflow: hidden; text-overflow: ellipsis; }
    .finance-items .item-row .profit { color: #6ac88a; }
    .finance-items .item-row .loss { color: #c87070; }
    .finance-items .empty { color: #4a5a7a; text-align: center; padding: 20px; font-size: 13px; }
    .finance-add { display: grid; grid-template-columns: 1fr 60px 60px; gap: 8px; margin-top: 8px; }
    .finance-add input {
      padding: 8px 10px; background: rgba(15,30,55,0.7);
      border: 1px solid rgba(50,90,140,0.2); border-radius: 6px;
      color: #d0d9e6; font-size: 13px; outline: none;
    }
    .finance-add .add-btn {
      grid-column: 1 / -1; padding: 10px;
      background: rgba(30,80,150,0.3); border: 1px solid rgba(60,120,200,0.2);
      border-radius: 6px; color: #8ab4d6; font-size: 14px; cursor: pointer; text-align: center;
    }

    /* FESTIVALS */
    .festival-card {
      background: rgba(15,30,55,0.5); border-radius: 6px;
      padding: 12px 14px; margin-bottom: 10px;
      border: 1px solid rgba(40,80,130,0.12);
      display: flex; justify-content: space-between; align-items: center; gap: 8px;
    }
    .festival-card .info { flex: 1; min-width: 0; }
    .festival-card .info .name { font-size: 15px; color: #c8dcee; font-weight: 500; }
    .festival-card .info .date { font-size: 12px; color: #5a7a9a; }
    .festival-card .status {
      font-size: 11px; padding: 4px 10px; border-radius: 20px;
      background: rgba(40,80,130,0.2); color: #8aabca; white-space: nowrap; cursor: pointer;
    }
    .festival-card .delete-fest { background: none; border: none; color: #5a4a4a; font-size: 18px; cursor: pointer; }

    /* CALENDAR */
    .cal-grid { display: grid; grid-template-columns: repeat(7, 1fr); gap: 4px; margin-bottom: 12px; }
    .cal-grid .cal-header { text-align: center; font-size: 10px; color: #4a6a8a; padding: 4px 0; font-weight: 600; }
    .cal-grid .cal-day {
      aspect-ratio: 1; display: flex; align-items: center; justify-content: center;
      border-radius: 50%; font-size: 14px; color: #8aabca; cursor: pointer;
      background: transparent; border: none; font-family: inherit; position: relative;
    }
    .cal-grid .cal-day:active { background: rgba(40,80,160,0.2); }
    .cal-grid .cal-day.has-event { color: #b0d0ee; font-weight: 500; }
    .cal-grid .cal-day.has-event::after {
      content: ''; position: absolute; bottom: 2px; width: 4px; height: 4px;
      border-radius: 50%; background: #4a8ac8;
    }
    .cal-grid .cal-day.other-month { color: #2a3a5a; }
    .cal-grid .cal-day.today { border: 1px solid rgba(80,160,240,0.3); }
    .cal-events-list { max-height: 150px; overflow-y: auto; }
    .cal-event-item {
      display: flex; align-items: center; gap: 10px;
      padding: 8px 10px; background: rgba(15,30,55,0.4);
      border-radius: 6px; margin-bottom: 6px; font-size: 13px;
    }
    .cal-event-item .event-text { flex: 1; color: #b0cce6; }
    .cal-event-item .event-check {
      width: 20px; height: 20px; border-radius: 4px;
      border: 2px solid #3a5a7a; display: flex; align-items: center; justify-content: center;
      cursor: pointer; font-size: 12px;
    }
    .cal-event-item .event-check.done { background: #4a8ac8; border-color: #4a8ac8; }
    .cal-event-item .event-check.done::after { content: '✓'; color: #fff; }
    .cal-event-item .event-del { background: none; border: none; color: #5a4a4a; font-size: 16px; cursor: pointer; }

    /* NOTES */
    .notes-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 10px; }
    .notes-grid .note-card {
      background: rgba(15,30,55,0.5); border-radius: 6px;
      padding: 12px; border: 1px solid rgba(40,80,130,0.1); min-height: 80px;
    }
    .notes-grid .note-card .note-label { font-size: 11px; color: #4a6a8a; margin-bottom: 6px; font-weight: 600; }
    .notes-grid .note-card textarea {
      width: 100%; background: transparent; border: none;
      color: #b0cce6; font-size: 13px; outline: none; resize: none;
      min-height: 50px; font-family: inherit; padding: 0;
    }

    /* SOCIAL */
    .social-item {
      display: flex; justify-content: space-between; align-items: center;
      padding: 12px 14px; background: rgba(15,30,55,0.4);
      border-radius: 6px; margin-bottom: 8px; border: 1px solid rgba(40,80,130,0.1);
    }
    .social-item .name { font-size: 15px; color: #b0cce6; }
    .social-item .check-btn {
      padding: 6px 16px; background: rgba(30,80,150,0.3);
      border: 1px solid rgba(60,120,200,0.2); border-radius: 20px;
      color: #8ab4d6; font-size: 12px; cursor: pointer;
    }

    /* GALLERY */
    .gallery-grid { display: grid; grid-template-columns: repeat(3, 1fr); gap: 6px; }
    .gallery-grid .gallery-item {
      aspect-ratio: 1; border-radius: 6px; overflow: hidden;
      background: rgba(20,45,80,0.3); border: 1px solid rgba(40,80,130,0.1);
      position: relative;
    }
    .gallery-grid .gallery-item img { width: 100%; height: 100%; object-fit: cover; }
    .gallery-grid .gallery-item .del-gallery {
      position: absolute; top: 2px; right: 2px;
      background: rgba(0,0,0,0.5); border: none; color: #c87070;
      border-radius: 50%; width: 20px; height: 20px; font-size: 12px; cursor: pointer;
    }

    /* SETTINGS */
    .settings-item {
      display: flex; justify-content: space-between; align-items: center;
      padding: 14px 0; border-bottom: 1px solid rgba(40,80,130,0.08);
    }
    .settings-item .label { color: #8aabca; font-size: 14px; }
    .settings-item .value { color: #5a7a9a; font-size: 14px; }
    .settings-item input {
      background: rgba(15,30,55,0.7); border: 1px solid rgba(50,90,140,0.2);
      border-radius: 6px; padding: 6px 12px; color: #d0d9e6;
      font-size: 14px; width: 100px; text-align: center; outline: none;
    }
    .settings-item .save-btn {
      padding: 6px 16px; background: rgba(30,80,150,0.3);
      border: 1px solid rgba(60,120,200,0.2); border-radius: 6px;
      color: #8ab4d6; font-size: 12px; cursor: pointer;
    }

    .text-muted { color: #4a5a7a; font-size: 13px; }
    .text-center { text-align: center; }
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
      <div class="mandala-item" data-screen="calendarScreen"><span class="icon">📅</span><span class="label">Календарь</span></div>
      <div class="mandala-item" data-screen="festivalScreen"><span class="icon">🎪</span><span class="label">Фестивали</span></div>
      <div class="mandala-item" data-screen="notesScreen"><span class="icon">📝</span><span class="label">Заметки</span></div>
      <div class="mandala-item" data-screen="settingsScreen"><span class="icon">⚙️</span><span class="label">Настройки</span></div>
      <div class="mandala-center" id="goPublish">＋</div>
      <div class="mandala-item" data-screen="financeScreen"><span class="icon">💰</span><span class="label">Финансы</span></div>
      <div class="mandala-item" data-screen="socialScreen"><span class="icon">🌐</span><span class="label">Мои соцсети</span></div>
      <div class="mandala-item" data-screen="galleryScreen"><span class="icon">🖼️</span><span class="label">Галерея</span></div>
    </div>
  </div>

  <!-- PUBLISH SCREEN -->
  <div class="screen" id="publishScreen">
    <div class="screen-header">
      <button class="back-btn" data-back="mandalaScreen">‹</button>
      <div class="title">Новая публикация</div>
    </div>
    <div class="form-group"><label>Название изделия</label><input type="text" id="pubTitle" placeholder="Например: Бабочка-резная"></div>
    <div class="form-group"><label>Описание</label><textarea id="pubDesc" placeholder="Расскажите о работе..."></textarea></div>
    <div class="form-group"><label>Цена (₽)</label><input type="number" id="pubPrice" placeholder="1500"></div>
    <div class="form-group"><label>Хештеги (через запятую)</label><input type="text" id="pubTags" placeholder="ручнаяработа, бабочка, кожа"></div>
    <div class="form-group">
      <label>Фотографии (до 8)</label>
      <div class="photo-upload-btn" id="photoUploadBtn">📷 Выбрать фото</div>
      <input type="file" id="photoInput" accept="image/*" multiple style="display:none">
      <div class="photo-preview-grid" id="photoPreviewGrid"></div>
    </div>
    <div class="form-group">
      <label>Площадки</label>
      <div class="checkbox-grid" id="platformGrid">
        <label class="checkbox-item active" data-platform="vk"><span class="check"></span> ВК</label>
        <label class="checkbox-item active" data-platform="avito"><span class="check"></span> Авито</label>
        <label class="checkbox-item active" data-platform="yula"><span class="check"></span> Юла</label>
        <label class="checkbox-item active" data-platform="ym"><span class="check"></span> Ярмарка</label>
        <label class="checkbox-item active" data-platform="meshok"><span class="check"></span> Мешок</label>
        <label class="checkbox-item active" data-platform="pikabu"><span class="check"></span> Пикабу</label>
        <label class="checkbox-item active" data-platform="ig"><span class="check"></span> Instagram</label>
        <label class="checkbox-item active" data-platform="tg"><span class="check"></span> Telegram</label>
      </div>
    </div>
    <button class="btn-primary" id="startPublishBtn">🚀 Начать рассылку</button>
  </div>

  <!-- FINANCE SCREEN -->
  <div class="screen" id="financeScreen">
    <div class="screen-header">
      <button class="back-btn" data-back="mandalaScreen">‹</button>
      <div class="title">Финансы</div>
    </div>
    <div class="finance-container">
      <div class="finance-tree" id="financeTree"></div>
      <div class="finance-items" id="financeItems"><div class="empty">Выберите категорию слева</div></div>
      <div class="finance-add">
        <input type="text" id="financeItemName" placeholder="Название">
        <input type="number" id="financeItemCost" placeholder="Затраты">
        <input type="number" id="financeItemProfit" placeholder="Прибыль">
        <div class="add-btn" id="financeAddBtn">➕ Добавить изделие</div>
      </div>
    </div>
  </div>

  <!-- SOCIAL SCREEN -->
  <div class="screen" id="socialScreen">
    <div class="screen-header">
      <button class="back-btn" data-back="mandalaScreen">‹</button>
      <div class="title">Мои соцсети</div>
    </div>
    <div id="socialList"></div>
  </div>

  <!-- FESTIVAL SCREEN -->
  <div class="screen" id="festivalScreen">
    <div class="screen-header">
      <button class="back-btn" data-back="mandalaScreen">‹</button>
      <div class="title">Фестивали</div>
    </div>
    <div class="form-group">
      <label>Добавить фестиваль</label>
      <div style="display:flex;gap:8px;flex-wrap:wrap;">
        <input type="text" id="festName" placeholder="Название" style="flex:1;min-width:100px;">
        <input type="date" id="festDate" style="flex:0 0 130px;">
        <button class="btn-primary" id="festAddBtn" style="width:auto;padding:10px 20px;margin:0;">➕</button>
      </div>
    </div>
    <div id="festivalList"></div>
  </div>

  <!-- CALENDAR SCREEN -->
  <div class="screen" id="calendarScreen">
    <div class="screen-header">
      <button class="back-btn" data-back="mandalaScreen">‹</button>
      <div class="title">Календарь</div>
    </div>
    <div style="display:flex;justify-content:space-between;align-items:center;margin-bottom:8px;">
      <button class="back-btn" id="calPrev" style="font-size:20px;">‹</button>
      <span id="calMonthYear" style="font-size:16px;color:#8ab4d6;"></span>
      <button class="back-btn" id="calNext" style="font-size:20px;">›</button>
    </div>
    <div class="cal-grid" id="calGrid"></div>
    <div style="display:flex;gap:8px;margin-bottom:8px;">
      <input type="text" id="calEventInput" placeholder="Добавить событие..." style="flex:1;padding:8px 12px;background:rgba(15,30,55,0.7);border:1px solid rgba(50,90,140,0.2);border-radius:6px;color:#d0d9e6;outline:none;">
      <button class="btn-primary" id="calEventAdd" style="width:auto;padding:8px 16px;margin:0;">➕</button>
    </div>
    <div class="cal-events-list" id="calEventsList"></div>
  </div>

  <!-- NOTES SCREEN -->
  <div class="screen" id="notesScreen">
    <div class="screen-header">
      <button class="back-btn" data-back="mandalaScreen">‹</button>
      <div class="title">Заметки</div>
    </div>
    <div class="notes-grid" id="notesGrid">
      <div class="note-card"><div class="note-label">Пн / Вт</div><textarea placeholder="Планы..." data-note="mon-tue"></textarea></div>
      <div class="note-card"><div class="note-label">Ср / Чт</div><textarea placeholder="Планы..." data-note="wed-thu"></textarea></div>
      <div class="note-card"><div class="note-label">Пт / Сб</div><textarea placeholder="Планы..." data-note="fri-sat"></textarea></div>
      <div class="note-card"><div class="note-label">Вс</div><textarea placeholder="Планы..." data-note="sun"></textarea></div>
    </div>
  </div>

  <!-- GALLERY SCREEN -->
  <div class="screen" id="galleryScreen">
    <div class="screen-header">
      <button class="back-btn" data-back="mandalaScreen">‹</button>
      <div class="title">Галерея</div>
    </div>
    <div class="gallery-grid" id="galleryGrid"></div>
  </div>

  <!-- SETTINGS SCREEN -->
  <div class="screen" id="settingsScreen">
    <div class="screen-header">
      <button class="back-btn" data-back="mandalaScreen">‹</button>
      <div class="title">Настройки</div>
    </div>
    <div class="settings-item">
      <span class="label">Пин-код</span>
      <div style="display:flex;gap:8px;align-items:center;">
        <input type="password" id="settingsPin" maxlength="4" placeholder="****" style="width:80px;">
        <button class="save-btn" id="settingsPinSave">Сохранить</button>
      </div>
    </div>
    <div class="settings-item"><span class="label">Версия</span><span class="value">2.0 — Чеклисты живы</span></div>
    <div class="settings-item" style="border-bottom:none;"><span class="label">Данные</span><span class="value" id="dataSize">0 КБ</span></div>
  </div>
</div>

<script>
  // ==================== DATA ====================
  const DATA = {
    pin: '1234',
    posts: [],
    finance: {
      tree: {
        'Кожа': {
          'Блокноты': { items: [] },
          'Браслеты': { items: [] },
          'Бабочки': { items: [] },
          'Брелки': { items: [] },
          'Подвески': { items: [] },
          items: []
        },
        'Ресуначбки))0)': {
          'Холстi': { items: [] },
          'Ткани': { items: [] },
          'Разновие))': { items: [] },
          items: []
        },
        'Пластинки': { items: [] },
        'Шкатулки': { items: [] },
        'Этнические штуки': { items: [] },
        'Несортируемое': { items: [] }
      }
    },
    festivals: [],
    calendar: {},
    notes: { 'mon-tue':'', 'wed-thu':'', 'fri-sat':'', 'sun':'' },
    socialPlatforms: [
      { id:'vk', name:'ВКонтакте', url:'https://vk.com' },
      { id:'avito', name:'Авито', url:'https://www.avito.ru' },
      { id:'yula', name:'Юла', url:'https://youla.ru' },
      { id:'ym', name:'Ярмарка Мастеров', url:'https://livemaster.ru' },
      { id:'meshok', name:'Мешок', url:'https://meshok.net' },
      { id:'pikabu', name:'Пикабу', url:'https://pikabu.ru' },
      { id:'ig', name:'Instagram', url:'https://instagram.com' },
      { id:'tg', name:'Telegram', url:'https://t.me' }
    ],
    gallery: []
  };

  // ==================== STORAGE ====================
  function saveData() { localStorage.setItem('elfData', JSON.stringify(DATA)); updateDataSize(); }
  function loadData() {
    try {
      const raw = localStorage.getItem('elfData');
      if (raw) Object.assign(DATA, JSON.parse(raw));
    } catch(e) {}
  }
  function updateDataSize() {
    const size = new Blob([localStorage.getItem('elfData')||'']).size;
    const el = document.getElementById('dataSize');
    if (el) el.textContent = (size/1024).toFixed(1) + ' КБ';
  }

  // ==================== NAVIGATION ====================
  let currentScreen = 'pinScreen';
  function showScreen(id) {
    document.querySelectorAll('.screen').forEach(s => s.classList.remove('active'));
    const target = document.getElementById(id);
    if (target) { target.classList.add('active'); currentScreen = id; }
    // refresh content on show
    if (id === 'financeScreen') renderFinance();
    if (id === 'socialScreen') renderSocial();
    if (id === 'festivalScreen') renderFestivals();
    if (id === 'calendarScreen') renderCalendar();
    if (id === 'galleryScreen') renderGallery();
    if (id === 'notesScreen') renderNotes();
    if (id === 'settingsScreen') updateDataSize();
  }
  document.querySelectorAll('[data-back]').forEach(btn => {
    btn.addEventListener('click', () => showScreen(btn.dataset.back));
  });
  document.querySelectorAll('.mandala-item').forEach(item => {
    item.addEventListener('click', () => showScreen(item.dataset.screen));
  });
  document.getElementById('goPublish').addEventListener('click', () => showScreen('publishScreen'));

  // ==================== PIN ====================
  let pinBuffer = '';
  const dots = document.querySelectorAll('.pin-dot');
  const pinScreen = document.getElementById('pinScreen');
  function updateDots() { dots.forEach((d,i) => d.classList.toggle('filled', i < pinBuffer.length)); }
  function handlePinInput(val) {
    if (val === 'del') { pinBuffer = pinBuffer.slice(0,-1); updateDots(); return; }
    if (pinBuffer.length >= 4) return;
    pinBuffer += val; updateDots();
    if (pinBuffer.length === 4) {
      if (pinBuffer === DATA.pin) {
        pinBuffer = ''; updateDots();
        showScreen('mandalaScreen');
      } else {
        alert('Неверный пин');
        pinBuffer = ''; updateDots();
      }
    }
  }
  document.querySelectorAll('.pin-key[data-value]').forEach(b => {
    b.addEventListener('click', () => handlePinInput(b.dataset.value));
  });

  // ==================== PUBLISH ====================
  let selectedPhotos = [];
  document.getElementById('photoUploadBtn').addEventListener('click', () => document.getElementById('photoInput').click());
  document.getElementById('photoInput').addEventListener('change', function(e) {
    const files = Array.from(e.target.files);
    for (const file of files) {
      if (selectedPhotos.length >= 8) break;
      const reader = new FileReader();
      reader.onload = ev => {
        selectedPhotos.push(ev.target.result);
        renderPhotoPreviews();
      };
      reader.readAsDataURL(file);
    }
    e.target.value = '';
  });
  function renderPhotoPreviews() {
    const grid = document.getElementById('photoPreviewGrid');
    grid.innerHTML = '';
    selectedPhotos.forEach((src,i) => {
      const img = document.createElement('img');
      img.className = 'photo-preview'; img.src = src;
      img.addEventListener('click', () => { selectedPhotos.splice(i,1); renderPhotoPreviews(); });
      grid.appendChild(img);
    });
  }
  document.querySelectorAll('#platformGrid .checkbox-item').forEach(el => {
    el.addEventListener('click', () => el.classList.toggle('active'));
  });

  document.getElementById('startPublishBtn').addEventListener('click', async () => {
    const title = document.getElementById('pubTitle').value.trim() || 'Без названия';
    const desc = document.getElementById('pubDesc').value.trim();
    const price = document.getElementById('pubPrice').value || '0';
    const tags = document.getElementById('pubTags').value.trim();
    const platforms = [...document.querySelectorAll('#platformGrid .checkbox-item.active')].map(e => e.dataset.platform);
    if (selectedPhotos.length === 0) return alert('Добавьте фото');
    DATA.posts.push({ id:Date.now(), title, desc, price, tags, photos:[...selectedPhotos], platforms, date:new Date().toISOString() });
    DATA.gallery.push(...selectedPhotos);
    saveData();
    const text = `${title}\n${desc}\nЦена: ${price}₽\n#${tags.replace(/,/g, ' #')}`;
    try { await navigator.clipboard.writeText(text); } catch(e) {
      const ta = document.createElement('textarea'); ta.value=text; document.body.appendChild(ta); ta.select(); document.execCommand('copy'); ta.remove();
    }
    for (const p of platforms) {
      const plat = DATA.socialPlatforms.find(s => s.id === p);
      if (plat) { window.open(plat.url, '_blank'); await new Promise(r => setTimeout(r, 300)); }
    }
    alert('✅ Текст скопирован! Площадки открыты.');
    document.getElementById('pubTitle').value = ''; document.getElementById('pubDesc').value = '';
    document.getElementById('pubPrice').value = ''; document.getElementById('pubTags').value = '';
    selectedPhotos = []; renderPhotoPreviews();
  });

  // ==================== FINANCE ====================
  let selectedFinancePath = [];
  function getNode(path) { let n = DATA.finance.tree; for (const k of path) { if (n[k]) n = n[k]; else return null; } return n; }
  function renderFinance() {
    const tree = document.getElementById('financeTree');
    tree.innerHTML = '';
    function renderNode(node, path) {
      const keys = Object.keys(node).filter(k => k !== 'items');
      keys.forEach(key => {
        const isSel = path.concat(key).join('/') === selectedFinancePath.join('/');
        const folder = document.createElement('div');
        folder.className = 'folder' + (isSel ? ' selected' : '');
        folder.innerHTML = `<span class="arrow ${isSel?'open':''}">▶</span> ${key}`;
        folder.addEventListener('click', (e) => { e.stopPropagation(); selectedFinancePath = [...path, key]; renderFinance(); });
        tree.appendChild(folder);
        if (isSel) {
          const children = document.createElement('div'); children.className='children';
          const subNode = getNode([...path, key]);
          if (subNode) renderNode(subNode, [...path, key]);
          tree.appendChild(children);
        }
      });
    }
    renderNode(DATA.finance.tree, []);
    renderFinanceItems();
  }
  function renderFinanceItems() {
    const node = getNode(selectedFinancePath);
    const container = document.getElementById('financeItems');
    if (!node) { container.innerHTML = '<div class="empty">Выберите категорию</div>'; return; }
    let items = [...(node.items||[])];
    Object.keys(node).forEach(k => { if (k !== 'items' && node[k].items) items = items.concat(node[k].items); });
    if (!items.length) { container.innerHTML = '<div class="empty">Нет изделий</div>'; return; }
    container.innerHTML = `<div class="item-row"><span class="name">Название</span><span>Затраты</span><span>Прибыль</span><span>%</span><span></span></div>`
      + items.map(i => {
        const pct = i.cost ? Math.round(i.profit/i.cost*100) : 0;
        return `<div class="item-row"><span class="name">${i.name}</span><span>${i.cost}₽</span><span class="${i.profit>0?'profit':'loss'}">${i.profit}₽</span><span>${pct}%</span><span style="cursor:pointer;color:#5a4a4a;" data-del="${i.name}">✕</span></div>`;
      }).join('');
    container.querySelectorAll('[data-del]').forEach(el => el.addEventListener('click', () => {
      const name = el.dataset.del;
      const node2 = getNode(selectedFinancePath);
      if (node2 && node2.items) {
        const idx = node2.items.findIndex(i => i.name === name);
        if (idx > -1) { node2.items.splice(idx,1); saveData(); renderFinanceItems(); }
      }
    }));
  }
  document.getElementById('financeAddBtn').addEventListener('click', () => {
    const name = document.getElementById('financeItemName').value.trim();
    const cost = parseInt(document.getElementById('financeItemCost').value) || 0;
    const profit = parseInt(document.getElementById('financeItemProfit').value) || 0;
    if (!name) return alert('Введите название');
    const node = getNode(selectedFinancePath);
    if (!node) return alert('Выберите категорию');
    if (!node.items) node.items = [];
    node.items.push({ name, cost, profit });
    document.getElementById('financeItemName').value = '';
    document.getElementById('financeItemCost').value = '';
    document.getElementById('financeItemProfit').value = '';
    saveData(); renderFinanceItems();
  });

  // ==================== SOCIAL ====================
  function renderSocial() {
    const list = document.getElementById('socialList');
    list.innerHTML = DATA.socialPlatforms.map(p => `
      <div class="social-item">
        <span class="name">${p.name}</span>
        <button class="check-btn" data-url="${p.url}">Проверить</button>
      </div>`).join('');
    list.querySelectorAll('.check-btn').forEach(b => b.addEventListener('click', () => window.open(b.dataset.url, '_blank')));
  }

  // ==================== FESTIVALS ====================
  const FEST_STATUSES = ['Планирую','Заявка отправлена','Участвую','Отказ'];
  function renderFestivals() {
    const list = document.getElementById('festivalList');
    if (!DATA.festivals.length) { list.innerHTML = '<div class="text-muted text-center" style="padding:20px;">Нет фестивалей</div>'; return; }
    list.innerHTML = DATA.festivals.map((f,i) => `
      <div class="festival-card">
        <div class="info"><div class="name">${f.name}</div><div class="date">${f.date||'—'}</div></div>
        <span class="status" data-idx="${i}">${f.status}</span>
        <button class="delete-fest" data-idx="${i}">✕</button>
      </div>`).join('');
    list.querySelectorAll('.status').forEach(el => el.addEventListener('click', () => {
      const i = +el.dataset.idx;
      DATA.festivals[i].status = FEST_STATUSES[(FEST_STATUSES.indexOf(DATA.festivals[i].status)+1)%FEST_STATUSES.length];
      saveData(); renderFestivals();
    }));
    list.querySelectorAll('.delete-fest').forEach(el => el.addEventListener('click', () => {
      DATA.festivals.splice(+el.dataset.idx,1); saveData(); renderFestivals();
    }));
  }
  document.getElementById('festAddBtn').addEventListener('click', () => {
    const name = document.getElementById('festName').value.trim();
    const date = document.getElementById('festDate').value;
    if (!name) return alert('Введите название');
    DATA.festivals.push({ id:Date.now(), name, date: date||'—', status:'Планирую' });
    document.getElementById('festName').value = ''; document.getElementById('festDate').value = '';
    saveData(); renderFestivals();
  });

  // ==================== CALENDAR ====================
  let calYear = new Date().getFullYear(), calMonth = new Date().getMonth(), calSelectedDate = null;
  function renderCalendar() {
    const grid = document.getElementById('calGrid');
    document.getElementById('calMonthYear').textContent = new Date(calYear, calMonth).toLocaleDateString('ru',{month:'long',year:'numeric'});
    grid.innerHTML = '';
    ['Пн','Вт','Ср','Чт','Пт','Сб','Вс'].forEach(d => {
      const div = document.createElement('div'); div.className='cal-header'; div.textContent=d; grid.appendChild(div);
    });
    const firstDay = new Date(calYear, calMonth, 1).getDay();
    const startOffset = firstDay === 0 ? 6 : firstDay - 1;
    const daysInPrev = new Date(calYear, calMonth, 0).getDate();
    for (let i=startOffset; i>0; i--) {
      const div = document.createElement('div'); div.className='cal-day other-month'; div.textContent = daysInPrev - i + 1; grid.appendChild(div);
    }
    const daysInMonth = new Date(calYear, calMonth+1, 0).getDate();
    const today = new Date();
    const todayStr = `${today.getFullYear()}-${String(today.getMonth()+1).padStart(2,'0')}-${String(today.getDate()).padStart(2,'0')}`;
    if (!calSelectedDate) calSelectedDate = todayStr;
    for (let d=1; d<=daysInMonth; d++) {
      const dateStr = `${calYear}-${String(calMonth+1).padStart(2,'0')}-${String(d).padStart(2,'0')}`;
      const btn = document.createElement('button'); btn.className='cal-day';
      if (dateStr === todayStr) btn.classList.add('today');
      if (DATA.calendar[dateStr]?.length) btn.classList.add('has-event');
      btn.textContent = d; btn.dataset.date = dateStr;
      btn.addEventListener('click', () => { calSelectedDate = dateStr; renderCalendarEvents(); });
      grid.appendChild(btn);
    }
    const total = grid.children.length;
    for (let i=1; i<=42-total; i++) {
      const div = document.createElement('div'); div.className='cal-day other-month'; div.textContent = i; grid.appendChild(div);
    }
    renderCalendarEvents();
  }
  function renderCalendarEvents() {
    const list = document.getElementById('calEventsList');
    if (!calSelectedDate || !DATA.calendar[calSelectedDate]?.length) {
      list.innerHTML = '<div class="text-muted text-center" style="padding:8px;">Нет событий на этот день</div>'; return;
    }
    list.innerHTML = DATA.calendar[calSelectedDate].map((ev,i) => `
      <div class="cal-event-item">
        <span class="event-check ${ev.checked?'done':''}" data-idx="${i}"></span>
        <span class="event-text">${ev.text}</span>
        <button class="event-del" data-idx="${i}">✕</button>
      </div>`).join('');
    list.querySelectorAll('.event-check').forEach(el => el.addEventListener('click', () => {
      const i = +el.dataset.idx;
      DATA.calendar[calSelectedDate][i].checked = !DATA.calendar[calSelectedDate][i].checked;
      saveData(); renderCalendarEvents(); renderCalendar();
    }));
    list.querySelectorAll('.event-del').forEach(el => el.addEventListener('click', () => {
      DATA.calendar[calSelectedDate].splice(+el.dataset.idx,1);
      if (!DATA.calendar[calSelectedDate].length) delete DATA.calendar[calSelectedDate];
      saveData(); renderCalendarEvents(); renderCalendar();
    }));
  }
  document.getElementById('calEventAdd').addEventListener('click', () => {
    const text = document.getElementById('calEventInput').value.trim();
    if (!text) return;
    if (!calSelectedDate) {
      const today = new Date();
      calSelectedDate = `${today.getFullYear()}-${String(today.getMonth()+1).padStart(2,'0')}-${String(today.getDate()).padStart(2,'0')}`;
    }
    if (!DATA.calendar[calSelectedDate]) DATA.calendar[calSelectedDate] = [];
    DATA.calendar[calSelectedDate].push({ text, checked: false });
    document.getElementById('calEventInput').value = '';
    saveData(); renderCalendarEvents(); renderCalendar();
  });
  document.getElementById('calPrev').addEventListener('click', () => { calMonth--; if(calMonth<0){calMonth=11;calYear--;} renderCalendar(); });
  document.getElementById('calNext').addEventListener('click', () => { calMonth++; if(calMonth>11){calMonth=0;calYear++;} renderCalendar(); });

  // ==================== NOTES ====================
  function renderNotes() {
    document.querySelectorAll('#notesGrid textarea').forEach(ta => {
      ta.value = DATA.notes[ta.dataset.note] || '';
    });
  }
  document.getElementById('notesGrid').addEventListener('input', (e) => {
    if (e.target.tagName === 'TEXTAREA') {
      DATA.notes[e.target.dataset.note] = e.target.value;
      saveData();
    }
  });

  // ==================== GALLERY ====================
  function renderGallery() {
    const grid = document.getElementById('galleryGrid');
    if (!DATA.gallery.length) { grid.innerHTML = '<div class="text-muted text-center" style="grid-column:1/-1;padding:30px;">Галерея пуста</div>'; return; }
    grid.innerHTML = DATA.gallery.map((src,i) => `
      <div class="gallery-item">
        <img src="${src}" alt="Работа">
        <button class="del-gallery" data-idx="${i}">✕</button>
      </div>`).join('');
    grid.querySelectorAll('.del-gallery').forEach(el => el.addEventListener('click', () => {
      DATA.gallery.splice(+el.dataset.idx,1); saveData(); renderGallery();
    }));
  }

  // ==================== SETTINGS ====================
  document.getElementById('settingsPinSave').addEventListener('click', () => {
    const val = document.getElementById('settingsPin').value.trim();
    if (val.length===4 && /^\d{4}$/.test(val)) { DATA.pin = val; saveData(); alert('Пин-код обновлён!'); document.getElementById('settingsPin').value = ''; }
    else alert('Пин должен быть 4 цифры');
  });

  // ==================== INIT ====================
  loadData();
  updateDataSize();
  showScreen('pinScreen');
  document.addEventListener('keydown', (e) => {
    if (currentScreen !== 'pinScreen') return;
    if (e.key>='0' && e.key<='9') handlePinInput(e.key);
    else if (e.key==='Backspace'||e.key==='Delete') handlePinInput('del');
  });
</script>
</body>
</html>
