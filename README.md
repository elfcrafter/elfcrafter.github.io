<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no, viewport-fit=cover">
    <meta name="apple-mobile-web-app-capable" content="yes">
    <meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
    <meta name="theme-color" content="#0a0e1a">
    <title>Мастерская Эльфа</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            -webkit-tap-highlight-color: transparent;
            user-select: none;
        }
        body {
            font-family: -apple-system, 'Segoe UI', Roboto, Helvetica, Arial, sans-serif;
            background: #0a0e1a;
            color: #d0d9e6;
            overflow: hidden;
            height: 100vh;
            width: 100vw;
            position: fixed;
        }
        ::-webkit-scrollbar {
            width: 3px;
        }
        ::-webkit-scrollbar-track {
            background: transparent;
        }
        ::-webkit-scrollbar-thumb {
            background: #2a3a5a;
            border-radius: 10px;
        }
        .app-container {
            width: 100%;
            height: 100%;
            position: relative;
            overflow: hidden;
            background: radial-gradient(ellipse at 30% 20%, #0f1a2e, #080c18);
        }
        .screen {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            padding: 20px 16px 80px 16px;
            overflow-y: auto;
            opacity: 0;
            pointer-events: none;
            transition: opacity 0.3s ease, transform 0.3s ease;
            transform: scale(0.97);
            background: transparent;
            will-change: transform, opacity;
        }
        .screen.active {
            opacity: 1;
            pointer-events: auto;
            transform: scale(1);
        }
        .screen-header {
            display: flex;
            align-items: center;
            gap: 12px;
            padding: 8px 0 16px 0;
            border-bottom: 1px solid rgba(40, 70, 120, 0.25);
            margin-bottom: 16px;
            flex-shrink: 0;
        }
        .screen-header .back-btn {
            background: none;
            border: none;
            color: #6a8aaa;
            font-size: 24px;
            cursor: pointer;
            padding: 4px 8px;
            transition: color 0.2s;
            line-height: 1;
        }
        .screen-header .back-btn:hover {
            color: #aac8ee;
        }
        .screen-header .title {
            font-size: 18px;
            font-weight: 600;
            color: #c8dcee;
            letter-spacing: 0.5px;
            flex: 1;
        }
        .screen-header .title span {
            color: #5a8aaa;
            font-weight: 300;
        }

        /* PIN SCREEN */
        #pinScreen {
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            padding: 40px 20px;
            background: radial-gradient(ellipse at center, #0f1a2e, #050810);
            opacity: 1 !important;
            pointer-events: auto !important;
            transform: none !important;
        }
        #pinScreen.hidden {
            opacity: 0 !important;
            pointer-events: none !important;
        }
        .pin-logo {
            font-size: 42px;
            margin-bottom: 8px;
            letter-spacing: 2px;
        }
        .pin-logo-text {
            font-size: 22px;
            font-weight: 300;
            color: #8ab4d6;
            letter-spacing: 4px;
            margin-bottom: 30px;
        }
        .pin-dots {
            display: flex;
            gap: 20px;
            margin-bottom: 32px;
        }
        .pin-dot {
            width: 16px;
            height: 16px;
            border-radius: 50%;
            border: 2px solid #3a5a7a;
            background: transparent;
            transition: background 0.15s ease, border-color 0.15s ease;
        }
        .pin-dot.filled {
            background: #6a9ac8;
            border-color: #6a9ac8;
            box-shadow: 0 0 12px rgba(80, 140, 220, 0.3);
        }
        .pin-keypad {
            display: grid;
            grid-template-columns: repeat(3, 70px);
            gap: 14px;
            margin-bottom: 20px;
        }
        .pin-key {
            width: 70px;
            height: 70px;
            border-radius: 50%;
            border: 1px solid rgba(60, 100, 150, 0.3);
            background: rgba(20, 40, 70, 0.5);
            color: #b0cce6;
            font-size: 26px;
            font-weight: 300;
            cursor: pointer;
            transition: background 0.15s, transform 0.1s;
            display: flex;
            align-items: center;
            justify-content: center;
            backdrop-filter: blur(4px);
        }
        .pin-key:active {
            background: rgba(60, 120, 200, 0.3);
            transform: scale(0.92);
        }
        .pin-key.empty {
            background: transparent !important;
            border: none !important;
            pointer-events: none;
        }
        .pin-error {
            color: #c87070;
            font-size: 14px;
            min-height: 24px;
            margin-bottom: 8px;
            opacity: 0;
            transition: opacity 0.3s;
        }
        .pin-error.show {
            opacity: 1;
        }

        /* GREETING */
        .greeting-overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: radial-gradient(ellipse at center, #0f1a2e, #050810);
            display: flex;
            align-items: center;
            justify-content: center;
            z-index: 1000;
            opacity: 0;
            pointer-events: none;
            transition: opacity 0.5s ease;
        }
        .greeting-overlay.show {
            opacity: 1;
            pointer-events: auto;
        }
        .greeting-text {
            font-size: 22px;
            color: #8ab4d6;
            text-align: center;
            padding: 30px;
            font-weight: 300;
            letter-spacing: 1px;
            line-height: 1.6;
            max-width: 320px;
        }

        /* MANDALA */
        .mandala-grid {
            display: grid;
            grid-template-columns: 1fr 1fr 1fr;
            gap: 12px;
            max-width: 400px;
            margin: 20px auto 0 auto;
            position: relative;
            padding: 10px;
        }
        .mandala-item {
            aspect-ratio: 1;
            background: rgba(20, 45, 80, 0.4);
            border-radius: 20px;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            gap: 4px;
            border: 1px solid rgba(60, 120, 200, 0.15);
            cursor: pointer;
            transition: background 0.2s, transform 0.15s, border-color 0.2s;
            backdrop-filter: blur(2px);
            padding: 8px;
            text-align: center;
        }
        .mandala-item:active {
            transform: scale(0.94);
            background: rgba(40, 80, 140, 0.3);
            border-color: rgba(80, 160, 240, 0.3);
        }
        .mandala-item .icon {
            font-size: 28px;
            margin-bottom: 2px;
        }
        .mandala-item .label {
            font-size: 10px;
            color: #7a9aba;
            font-weight: 400;
            letter-spacing: 0.3px;
            line-height: 1.2;
        }
        .mandala-center {
            grid-column: 2;
            grid-row: 2;
            aspect-ratio: 1;
            background: radial-gradient(circle, #1a3a5a, #0f1a2e);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            border: 2px solid rgba(80, 160, 240, 0.3);
            cursor: pointer;
            transition: transform 0.2s, border-color 0.2s, box-shadow 0.2s;
            box-shadow: 0 0 30px rgba(40, 100, 200, 0.1);
            font-size: 32px;
            color: #8ab4d6;
        }
        .mandala-center:active {
            transform: scale(0.92);
            border-color: rgba(80, 200, 255, 0.6);
            box-shadow: 0 0 50px rgba(60, 150, 255, 0.2);
        }

        /* FORM ELEMENTS */
        .form-group {
            margin-bottom: 16px;
        }
        .form-group label {
            display: block;
            font-size: 12px;
            color: #6a8aaa;
            margin-bottom: 4px;
            letter-spacing: 0.5px;
            font-weight: 500;
        }
        .form-group input, .form-group textarea {
            width: 100%;
            padding: 12px 14px;
            background: rgba(15, 30, 55, 0.7);
            border: 1px solid rgba(50, 90, 140, 0.2);
            border-radius: 12px;
            color: #d0d9e6;
            font-size: 15px;
            outline: none;
            transition: border-color 0.2s;
            font-family: inherit;
        }
        .form-group input:focus, .form-group textarea:focus {
            border-color: rgba(80, 160, 240, 0.4);
        }
        .form-group textarea {
            resize: vertical;
            min-height: 70px;
        }
        .form-group input::placeholder, .form-group textarea::placeholder {
            color: #4a5a7a;
        }

        .checkbox-grid {
            display: flex;
            flex-wrap: wrap;
            gap: 8px;
            margin-top: 4px;
        }
        .checkbox-item {
            display: flex;
            align-items: center;
            gap: 6px;
            background: rgba(20, 45, 80, 0.3);
            padding: 6px 12px;
            border-radius: 20px;
            border: 1px solid rgba(50, 90, 140, 0.15);
            font-size: 13px;
            color: #8aabca;
            cursor: pointer;
            transition: background 0.2s, border-color 0.2s;
        }
        .checkbox-item.active {
            background: rgba(40, 100, 180, 0.25);
            border-color: rgba(80, 160, 240, 0.4);
            color: #b0d0ee;
        }
        .checkbox-item input {
            display: none;
        }
        .checkbox-item .check {
            width: 16px;
            height: 16px;
            border-radius: 4px;
            border: 2px solid #4a6a8a;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 10px;
            transition: background 0.2s, border-color 0.2s;
            flex-shrink: 0;
        }
        .checkbox-item.active .check {
            background: #4a8ac8;
            border-color: #4a8ac8;
        }
        .checkbox-item.active .check::after {
            content: '✓';
            color: #fff;
        }

        .photo-preview-grid {
            display: flex;
            flex-wrap: wrap;
            gap: 8px;
            margin-top: 8px;
        }
        .photo-preview {
            width: 60px;
            height: 60px;
            border-radius: 10px;
            object-fit: cover;
            border: 1px solid rgba(60, 120, 200, 0.2);
        }
        .photo-upload-btn {
            display: inline-flex;
            align-items: center;
            gap: 8px;
            padding: 8px 16px;
            background: rgba(30, 60, 110, 0.3);
            border: 1px dashed rgba(60, 120, 200, 0.3);
            border-radius: 12px;
            color: #6a8aaa;
            cursor: pointer;
            font-size: 13px;
            transition: background 0.2s;
        }
        .photo-upload-btn:active {
            background: rgba(40, 80, 160, 0.2);
        }

        .btn-primary {
            width: 100%;
            padding: 14px;
            background: linear-gradient(135deg, #1a4a7a, #0f2a4a);
            border: 1px solid rgba(60, 140, 220, 0.2);
            border-radius: 14px;
            color: #c8dcee;
            font-size: 16px;
            font-weight: 500;
            cursor: pointer;
            transition: background 0.2s, transform 0.1s;
            letter-spacing: 0.5px;
            margin-top: 8px;
        }
        .btn-primary:active {
            transform: scale(0.97);
            background: linear-gradient(135deg, #1a5a8a, #0f2a5a);
        }

        /* FINANCE */
        .finance-container {
            display: flex;
            flex-direction: column;
            gap: 12px;
            height: 100%;
        }
        .finance-tree {
            background: rgba(10, 25, 50, 0.5);
            border-radius: 14px;
            padding: 12px;
            max-height: 200px;
            overflow-y: auto;
            border: 1px solid rgba(40, 80, 130, 0.15);
        }
        .finance-tree .folder {
            padding: 6px 8px;
            cursor: pointer;
            border-radius: 8px;
            transition: background 0.15s;
            font-size: 14px;
            display: flex;
            align-items: center;
            gap: 8px;
        }
        .finance-tree .folder:active {
            background: rgba(40, 80, 160, 0.2);
        }
        .finance-tree .folder.selected {
            background: rgba(40, 80, 160, 0.25);
            color: #b0d0ee;
        }
        .finance-tree .folder .arrow {
            font-size: 10px;
            transition: transform 0.2s;
            color: #4a6a8a;
        }
        .finance-tree .folder .arrow.open {
            transform: rotate(90deg);
        }
        .finance-tree .children {
            padding-left: 20px;
        }
        .finance-items {
            flex: 1;
            background: rgba(10, 25, 50, 0.3);
            border-radius: 14px;
            padding: 12px;
            overflow-y: auto;
            border: 1px solid rgba(40, 80, 130, 0.1);
            min-height: 80px;
        }
        .finance-items .item-row {
            display: grid;
            grid-template-columns: 1fr 60px 60px 50px 40px;
            gap: 4px;
            padding: 6px 4px;
            font-size: 12px;
            border-bottom: 1px solid rgba(40, 80, 130, 0.08);
            align-items: center;
        }
        .finance-items .item-row .name {
            color: #b0cce6;
            white-space: nowrap;
            overflow: hidden;
            text-overflow: ellipsis;
        }
        .finance-items .item-row .profit {
            color: #6ac88a;
        }
        .finance-items .item-row .loss {
            color: #c87070;
        }
        .finance-items .empty {
            color: #4a5a7a;
            text-align: center;
            padding: 20px;
            font-size: 13px;
        }
        .finance-add {
            display: grid;
            grid-template-columns: 1fr 60px 60px;
            gap: 8px;
            margin-top: 8px;
        }
        .finance-add input {
            padding: 8px 10px;
            background: rgba(15, 30, 55, 0.7);
            border: 1px solid rgba(50, 90, 140, 0.2);
            border-radius: 10px;
            color: #d0d9e6;
            font-size: 13px;
            outline: none;
            width: 100%;
        }
        .finance-add input:focus {
            border-color: rgba(80, 160, 240, 0.4);
        }
        .finance-add .add-btn {
            grid-column: 1 / -1;
            padding: 10px;
            background: rgba(30, 80, 150, 0.3);
            border: 1px solid rgba(60, 120, 200, 0.2);
            border-radius: 10px;
            color: #8ab4d6;
            font-size: 14px;
            cursor: pointer;
            transition: background 0.2s;
            text-align: center;
        }
        .finance-add .add-btn:active {
            background: rgba(40, 100, 180, 0.3);
        }

        /* FESTIVALS */
        .festival-card {
            background: rgba(15, 30, 55, 0.5);
            border-radius: 12px;
            padding: 12px 14px;
            margin-bottom: 10px;
            border: 1px solid rgba(40, 80, 130, 0.12);
            display: flex;
            justify-content: space-between;
            align-items: center;
            gap: 8px;
        }
        .festival-card .info {
            flex: 1;
            min-width: 0;
        }
        .festival-card .info .name {
            font-size: 15px;
            color: #c8dcee;
            font-weight: 500;
        }
        .festival-card .info .date {
            font-size: 12px;
            color: #5a7a9a;
        }
        .festival-card .status {
            font-size: 11px;
            padding: 4px 10px;
            border-radius: 20px;
            background: rgba(40, 80, 130, 0.2);
            color: #8aabca;
            white-space: nowrap;
            cursor: pointer;
            transition: background 0.2s;
        }
        .festival-card .status:active {
            background: rgba(60, 120, 200, 0.2);
        }
        .festival-card .delete-fest {
            background: none;
            border: none;
            color: #5a4a4a;
            font-size: 18px;
            cursor: pointer;
            padding: 0 4px;
        }

        /* CALENDAR */
        .cal-grid {
            display: grid;
            grid-template-columns: repeat(7, 1fr);
            gap: 4px;
            margin-bottom: 12px;
        }
        .cal-grid .cal-header {
            text-align: center;
            font-size: 10px;
            color: #4a6a8a;
            padding: 4px 0;
            font-weight: 600;
            letter-spacing: 0.5px;
        }
        .cal-grid .cal-day {
            aspect-ratio: 1;
            display: flex;
            align-items: center;
            justify-content: center;
            border-radius: 50%;
            font-size: 14px;
            color: #8aabca;
            cursor: pointer;
            transition: background 0.15s;
            background: transparent;
            border: none;
            font-family: inherit;
            position: relative;
        }
        .cal-grid .cal-day:active {
            background: rgba(40, 80, 160, 0.2);
        }
        .cal-grid .cal-day.has-event {
            color: #b0d0ee;
            font-weight: 500;
        }
        .cal-grid .cal-day.has-event::after {
            content: '';
            position: absolute;
            bottom: 2px;
            width: 4px;
            height: 4px;
            border-radius: 50%;
            background: #4a8ac8;
        }
        .cal-grid .cal-day.other-month {
            color: #2a3a5a;
        }
        .cal-grid .cal-day.today {
            border: 1px solid rgba(80, 160, 240, 0.3);
        }
        .cal-events-list {
            max-height: 150px;
            overflow-y: auto;
        }
        .cal-event-item {
            display: flex;
            align-items: center;
            gap: 10px;
            padding: 8px 10px;
            background: rgba(15, 30, 55, 0.4);
            border-radius: 10px;
            margin-bottom: 6px;
            font-size: 13px;
        }
        .cal-event-item .event-text {
            flex: 1;
            color: #b0cce6;
        }
        .cal-event-item .event-check {
            width: 20px;
            height: 20px;
            border-radius: 6px;
            border: 2px solid #3a5a7a;
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            font-size: 12px;
            transition: background 0.2s, border-color 0.2s;
            flex-shrink: 0;
        }
        .cal-event-item .event-check.done {
            background: #4a8ac8;
            border-color: #4a8ac8;
        }
        .cal-event-item .event-check.done::after {
            content: '✓';
            color: #fff;
        }
        .cal-event-item .event-del {
            background: none;
            border: none;
            color: #5a4a4a;
            font-size: 16px;
            cursor: pointer;
        }

        /* NOTES */
        .notes-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 10px;
        }
        .notes-grid .note-card {
            background: rgba(15, 30, 55, 0.5);
            border-radius: 14px;
            padding: 12px;
            border: 1px solid rgba(40, 80, 130, 0.1);
            min-height: 80px;
        }
        .notes-grid .note-card .note-label {
            font-size: 11px;
            color: #4a6a8a;
            margin-bottom: 6px;
            font-weight: 600;
            letter-spacing: 0.5px;
        }
        .notes-grid .note-card textarea {
            width: 100%;
            background: transparent;
            border: none;
            color: #b0cce6;
            font-size: 13px;
            outline: none;
            resize: none;
            min-height: 50px;
            font-family: inherit;
            padding: 0;
        }
        .notes-grid .note-card textarea::placeholder {
            color: #3a4a6a;
        }

        /* SOCIAL */
        .social-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 12px 14px;
            background: rgba(15, 30, 55, 0.4);
            border-radius: 12px;
            margin-bottom: 8px;
            border: 1px solid rgba(40, 80, 130, 0.1);
        }
        .social-item .name {
            font-size: 15px;
            color: #b0cce6;
        }
        .social-item .check-btn {
            padding: 6px 16px;
            background: rgba(30, 80, 150, 0.3);
            border: 1px solid rgba(60, 120, 200, 0.2);
            border-radius: 20px;
            color: #8ab4d6;
            font-size: 12px;
            cursor: pointer;
            transition: background 0.2s;
        }
        .social-item .check-btn:active {
            background: rgba(40, 100, 180, 0.3);
        }

        /* SETTINGS */
        .settings-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 14px 0;
            border-bottom: 1px solid rgba(40, 80, 130, 0.08);
        }
        .settings-item .label {
            color: #8aabca;
            font-size: 14px;
        }
        .settings-item .value {
            color: #5a7a9a;
            font-size: 14px;
        }
        .settings-item input {
            background: rgba(15, 30, 55, 0.7);
            border: 1px solid rgba(50, 90, 140, 0.2);
            border-radius: 8px;
            padding: 6px 12px;
            color: #d0d9e6;
            font-size: 14px;
            width: 100px;
            text-align: center;
            outline: none;
        }
        .settings-item input:focus {
            border-color: rgba(80, 160, 240, 0.4);
        }
        .settings-item .save-btn {
            padding: 6px 16px;
            background: rgba(30, 80, 150, 0.3);
            border: 1px solid rgba(60, 120, 200, 0.2);
            border-radius: 8px;
            color: #8ab4d6;
            font-size: 12px;
            cursor: pointer;
            transition: background 0.2s;
        }
        .settings-item .save-btn:active {
            background: rgba(40, 100, 180, 0.3);
        }

        /* GALLERY */
        .gallery-grid {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 6px;
        }
        .gallery-grid .gallery-item {
            aspect-ratio: 1;
            border-radius: 10px;
            overflow: hidden;
            background: rgba(20, 45, 80, 0.3);
            border: 1px solid rgba(40, 80, 130, 0.1);
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 24px;
            color: #3a5a7a;
            position: relative;
        }
        .gallery-grid .gallery-item img {
            width: 100%;
            height: 100%;
            object-fit: cover;
        }
        .gallery-grid .gallery-item .del-gallery {
            position: absolute;
            top: 2px;
            right: 2px;
            background: rgba(0,0,0,0.5);
            border: none;
            color: #c87070;
            border-radius: 50%;
            width: 20px;
            height: 20px;
            font-size: 12px;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
        }

        /* PUBLISH */
        .publish-form {
            padding-bottom: 20px;
        }

        /* UTILITY */
        .mt-8 { margin-top: 8px; }
        .mb-8 { margin-bottom: 8px; }
        .flex { display: flex; gap: 8px; align-items: center; }
        .flex-wrap { flex-wrap: wrap; }
        .gap-4 { gap: 4px; }
        .text-center { text-align: center; }
        .text-muted { color: #4a5a7a; font-size: 13px; }
        .w-full { width: 100%; }
    </style>
</head>
<body>

<!-- GREETING OVERLAY -->
<div class="greeting-overlay" id="greetingOverlay">
    <div class="greeting-text" id="greetingText">Рисуй чаще, и чаща нарисует тебе</div>
</div>

<!-- PIN SCREEN -->
<div class="app-container" id="appContainer">
    <div class="screen" id="pinScreen">
        <div class="pin-logo">✧</div>
        <div class="pin-logo-text">Мастерская Эльфа</div>
        <div class="pin-dots" id="pinDots">
            <div class="pin-dot" data-index="0"></div>
            <div class="pin-dot" data-index="1"></div>
            <div class="pin-dot" data-index="2"></div>
            <div class="pin-dot" data-index="3"></div>
        </div>
        <div class="pin-error" id="pinError">Неверный пин-код</div>
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

    <!-- MAIN SCREENS (all hidden by default) -->
    <!-- MANDALA -->
    <div class="screen" id="mandalaScreen">
        <div class="screen-header">
            <div class="title">Мастерская <span>Эльфа</span></div>
        </div>
        <div class="mandala-grid">
            <div class="mandala-item" data-screen="calendarScreen">
                <div class="icon">📅</div>
                <div class="label">Календарь</div>
            </div>
            <div class="mandala-item" data-screen="settingsScreen">
                <div class="icon">⚙️</div>
                <div class="label">Настройки</div>
            </div>
            <div class="mandala-item" data-screen="notesScreen">
                <div class="icon">📝</div>
                <div class="label">Заметки</div>
            </div>
            <div class="mandala-item" data-screen="financeScreen">
                <div class="icon">💰</div>
                <div class="label">Финансы</div>
            </div>
            <div class="mandala-center" id="centerPlus">＋</div>
            <div class="mandala-item" data-screen="socialScreen">
                <div class="icon">🌐</div>
                <div class="label">Мои соцсети</div>
            </div>
            <div class="mandala-item" data-screen="galleryScreen">
                <div class="icon">🖼️</div>
                <div class="label">Галерея</div>
            </div>
            <div class="mandala-item" data-screen="festivalScreen">
                <div class="icon">🎪</div>
                <div class="label">Фестивали</div>
            </div>
        </div>
    </div>

    <!-- PUBLISH -->
    <div class="screen" id="publishScreen">
        <div class="screen-header">
            <button class="back-btn" data-back="mandalaScreen">‹</button>
            <div class="title">Новая публикация</div>
        </div>
        <div class="publish-form">
            <div class="form-group">
                <label>Название изделия</label>
                <input type="text" id="pubTitle" placeholder="Например: Бабочка-резная">
            </div>
            <div class="form-group">
                <label>Описание</label>
                <textarea id="pubDesc" placeholder="Расскажите о работе..."></textarea>
            </div>
            <div class="form-group">
                <label>Цена (₽)</label>
                <input type="number" id="pubPrice" placeholder="1500">
            </div>
            <div class="form-group">
                <label>Хештеги (через запятую)</label>
                <input type="text" id="pubTags" placeholder="ручнаяработа, бабочка, кожа">
            </div>
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
            <button class="btn-primary" id="publishBtn">🚀 Начать рассылку</button>
        </div>
    </div>

    <!-- FINANCE -->
    <div class="screen" id="financeScreen">
        <div class="screen-header">
            <button class="back-btn" data-back="mandalaScreen">‹</button>
            <div class="title">Финансы</div>
        </div>
        <div class="finance-container">
            <div class="finance-tree" id="financeTree"></div>
            <div class="finance-items" id="financeItems">
                <div class="empty">Выберите категорию слева</div>
            </div>
            <div class="finance-add">
                <input type="text" id="financeItemName" placeholder="Название">
                <input type="number" id="financeItemCost" placeholder="Затраты">
                <input type="number" id="financeItemProfit" placeholder="Прибыль">
                <div class="add-btn" id="financeAddBtn">➕ Добавить изделие</div>
            </div>
        </div>
    </div>

    <!-- SOCIAL -->
    <div class="screen" id="socialScreen">
        <div class="screen-header">
            <button class="back-btn" data-back="mandalaScreen">‹</button>
            <div class="title">Мои соцсети</div>
        </div>
        <div id="socialList"></div>
    </div>

    <!-- FESTIVALS -->
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

    <!-- CALENDAR -->
    <div class="screen" id="calendarScreen">
        <div class="screen-header">
            <button class="back-btn" data-back="mandalaScreen">‹</button>
            <div class="title">Календарь</div>
        </div>
        <div style="display:flex;justify-content:space-between;align-items:center;margin-bottom:8px;">
            <button class="back-btn" id="calPrev" style="font-size:20px;">‹</button>
            <span id="calMonthYear" style="font-size:16px;color:#8ab4d6;">Январь 2025</span>
            <button class="back-btn" id="calNext" style="font-size:20px;">›</button>
        </div>
        <div class="cal-grid" id="calGrid"></div>
        <div style="display:flex;gap:8px;margin-bottom:8px;">
            <input type="text" id="calEventInput" placeholder="Добавить событие..." style="flex:1;padding:8px 12px;background:rgba(15,30,55,0.7);border:1px solid rgba(50,90,140,0.2);border-radius:10px;color:#d0d9e6;outline:none;">
            <button class="btn-primary" id="calEventAdd" style="width:auto;padding:8px 16px;margin:0;">➕</button>
        </div>
        <div class="cal-events-list" id="calEventsList"></div>
    </div>

    <!-- NOTES -->
    <div class="screen" id="notesScreen">
        <div class="screen-header">
            <button class="back-btn" data-back="mandalaScreen">‹</button>
            <div class="title">Заметки</div>
        </div>
        <div class="notes-grid" id="notesGrid">
            <div class="note-card"><div class="note-label">Пн / Вт</div><textarea placeholder="Планы на понедельник и вторник..." data-note="mon-tue"></textarea></div>
            <div class="note-card"><div class="note-label">Ср / Чт</div><textarea placeholder="Планы на среду и четверг..." data-note="wed-thu"></textarea></div>
            <div class="note-card"><div class="note-label">Пт / Сб</div><textarea placeholder="Планы на пятницу и субботу..." data-note="fri-sat"></textarea></div>
            <div class="note-card"><div class="note-label">Вс</div><textarea placeholder="Планы на воскресенье..." data-note="sun"></textarea></div>
        </div>
    </div>

    <!-- GALLERY -->
    <div class="screen" id="galleryScreen">
        <div class="screen-header">
            <button class="back-btn" data-back="mandalaScreen">‹</button>
            <div class="title">Галерея</div>
        </div>
        <div class="gallery-grid" id="galleryGrid"></div>
    </div>

    <!-- SETTINGS -->
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
        <div class="settings-item">
            <span class="label">Версия</span>
            <span class="value">1.0.0 (прототип)</span>
        </div>
        <div class="settings-item" style="border-bottom:none;">
            <span class="label">Данные</span>
            <span class="value" id="dataSize">0 КБ</span>
        </div>
    </div>
</div>

<script>
    // ============================================================
    // DATA LAYER
    // ============================================================
    const DATA = {
        pin: '1234',
        posts: [],          // { id, title, desc, price, tags, photos: ['data:image/png...'], platforms: ['vk','avito'], date }
        finance: {          // tree: { 'Кожа': { 'Бабочки': { items: [{name,cost,profit}] }, items: [] } }
            tree: {
                'Кожа': {
                    'Бабочки': { items: [
                        { name: 'Бабочка-одинарная', cost: 200, profit: 800 },
                        { name: 'Бабочка-двойная', cost: 350, profit: 1200 }
                    ] },
                    items: []
                },
                'Дерево': { items: [] }
            },
            flatItems: []   // for quick display
        },
        festivals: [],      // { id, name, date, status: 'Планирую'|'Заявка отправлена'|'Участвую'|'Отказ' }
        calendar: {},       // '2025-01-15': [{ text: 'дедлайн', checked: false }]
        notes: {            // 'mon-tue': 'текст', 'wed-thu': 'текст', 'fri-sat': 'текст', 'sun': 'текст' }
            'mon-tue': '',
            'wed-thu': '',
            'fri-sat': '',
            'sun': ''
        },
        socialPlatforms: [
            { id: 'vk', name: 'ВКонтакте', url: 'https://vk.com' },
            { id: 'avito', name: 'Авито', url: 'https://www.avito.ru' },
            { id: 'yula', name: 'Юла', url: 'https://youla.ru' },
            { id: 'ym', name: 'Ярмарка Мастеров', url: 'https://livemaster.ru' },
            { id: 'meshok', name: 'Мешок', url: 'https://meshok.net' },
            { id: 'pikabu', name: 'Пикабу', url: 'https://pikabu.ru' },
            { id: 'ig', name: 'Instagram', url: 'https://instagram.com' },
            { id: 'tg', name: 'Telegram', url: 'https://t.me' }
        ],
        gallery: []         // ['data:image/png...']
    };

    // ============================================================
    // STORAGE
    // ============================================================
    function saveData() {
        try {
            const serialized = JSON.stringify(DATA);
            localStorage.setItem('elfData', serialized);
            updateDataSize();
        } catch(e) { console.warn('Save error:', e); }
    }

    function loadData() {
        try {
            const raw = localStorage.getItem('elfData');
            if (raw) {
                const parsed = JSON.parse(raw);
                Object.assign(DATA, parsed);
                // ensure nested structures exist
                if (!DATA.finance.tree) DATA.finance.tree = {};
                if (!DATA.calendar) DATA.calendar = {};
                if (!DATA.notes) DATA.notes = { 'mon-tue': '', 'wed-thu': '', 'fri-sat': '', 'sun': '' };
                if (!DATA.gallery) DATA.gallery = [];
                if (!DATA.posts) DATA.posts = [];
                if (!DATA.festivals) DATA.festivals = [];
            }
        } catch(e) { console.warn('Load error:', e); }
    }

    function updateDataSize() {
        const size = new Blob([localStorage.getItem('elfData') || '']).size;
        const el = document.getElementById('dataSize');
        if (el) el.textContent = (size / 1024).toFixed(1) + ' КБ';
    }

    // ============================================================
    // PIN
    // ============================================================
    let pinBuffer = '';
    const pinDots = document.querySelectorAll('.pin-dot');
    const pinError = document.getElementById('pinError');

    function updatePinDots() {
        pinDots.forEach((dot, i) => {
            dot.classList.toggle('filled', i < pinBuffer.length);
        });
    }

    function handlePinInput(value) {
        if (value === 'del') {
            pinBuffer = pinBuffer.slice(0, -1);
            updatePinDots();
            pinError.classList.remove('show');
            return;
        }
        if (pinBuffer.length >= 4) return;
        pinBuffer += value;
        updatePinDots();
        if (pinBuffer.length === 4) {
            if (pinBuffer === DATA.pin) {
                pinBuffer = '';
                updatePinDots();
                showGreeting();
            } else {
                pinError.classList.add('show');
                pinBuffer = '';
                updatePinDots();
            }
        }
    }

    document.querySelectorAll('.pin-key[data-value]').forEach(btn => {
        btn.addEventListener('click', () => {
            handlePinInput(btn.dataset.value);
        });
    });

    // ============================================================
    // GREETING
    // ============================================================
    const GREETINGS = [
        'Рисуй чаще, и чаща нарисует тебе',
        'Не бойся, я с тобой',
        'С возвращением, мастер Эльфа!',
        'Творчество начинается здесь',
        'Вдохновение уже рядом'
    ];

    function showGreeting() {
        const overlay = document.getElementById('greetingOverlay');
        const text = document.getElementById('greetingText');
        text.textContent = GREETINGS[Math.floor(Math.random() * GREETINGS.length)];
        overlay.classList.add('show');
        setTimeout(() => {
            overlay.classList.remove('show');
            document.getElementById('pinScreen').classList.add('hidden');
            showScreen('mandalaScreen');
        }, 2200);
    }

    // ============================================================
    // NAVIGATION
    // ============================================================
    let currentScreen = '';

    function showScreen(id) {
        if (currentScreen === id && id === 'mandalaScreen') return;
        document.querySelectorAll('.screen').forEach(s => s.classList.remove('active'));
        const target = document.getElementById(id);
        if (target) {
            target.classList.add('active');
            currentScreen = id;
            // refresh content on screen change
            if (id === 'financeScreen') renderFinance();
            if (id === 'socialScreen') renderSocial();
            if (id === 'festivalScreen') renderFestivals();
            if (id === 'calendarScreen') renderCalendar();
            if (id === 'galleryScreen') renderGallery();
            if (id === 'settingsScreen') updateDataSize();
        }
    }

    // Back buttons
    document.querySelectorAll('[data-back]').forEach(btn => {
        btn.addEventListener('click', () => {
            showScreen(btn.dataset.back);
        });
    });

    // Mandala items
    document.querySelectorAll('.mandala-item').forEach(item => {
        item.addEventListener('click', () => {
            showScreen(item.dataset.screen);
        });
    });

    // Center plus
    document.getElementById('centerPlus').addEventListener('click', () => {
        showScreen('publishScreen');
    });

    // ============================================================
    // PUBLISH
    // ============================================================
    let selectedPhotos = [];

    document.getElementById('photoUploadBtn').addEventListener('click', () => {
        document.getElementById('photoInput').click();
    });

    document.getElementById('photoInput').addEventListener('change', async function(e) {
        const files = Array.from(e.target.files);
        if (selectedPhotos.length + files.length > 8) {
            alert('Можно выбрать не более 8 фото');
            return;
        }
        for (const file of files) {
            try {
                const dataUrl = await compressImage(file, 300);
                selectedPhotos.push(dataUrl);
            } catch(err) {
                console.warn('Photo error:', err);
            }
        }
        renderPhotoPreviews();
        e.target.value = '';
        saveData();
    });

    function compressImage(file, maxSize) {
        return new Promise((resolve) => {
            const img = new Image();
            img.onload = function() {
                const canvas = document.createElement('canvas');
                const ctx = canvas.getContext('2d');
                const ratio = Math.min(maxSize / img.width, maxSize / img.height);
                canvas.width = img.width * ratio;
                canvas.height = img.height * ratio;
                ctx.imageSmoothingEnabled = false; // CRITICAL for marker art!
                ctx.drawImage(img, 0, 0, canvas.width, canvas.height);
                resolve(canvas.toDataURL('image/png'));
            };
            img.src = URL.createObjectURL(file);
        });
    }

    function renderPhotoPreviews() {
        const grid = document.getElementById('photoPreviewGrid');
        grid.innerHTML = '';
        selectedPhotos.forEach((src, i) => {
            const img = document.createElement('img');
            img.className = 'photo-preview';
            img.src = src;
            img.style.cursor = 'pointer';
            img.addEventListener('click', () => {
                selectedPhotos.splice(i, 1);
                renderPhotoPreviews();
                saveData();
            });
            grid.appendChild(img);
        });
    }

    // Platform toggles
    document.querySelectorAll('.checkbox-item').forEach(item => {
        item.addEventListener('click', () => {
            item.classList.toggle('active');
        });
    });

    // Publish
    document.getElementById('publishBtn').addEventListener('click', async () => {
        const title = document.getElementById('pubTitle').value.trim() || 'Без названия';
        const desc = document.getElementById('pubDesc').value.trim() || '';
        const price = document.getElementById('pubPrice').value || '0';
        const tags = document.getElementById('pubTags').value.trim() || '';
        const platforms = [];
        document.querySelectorAll('.checkbox-item.active').forEach(el => {
            platforms.push(el.dataset.platform);
        });

        if (selectedPhotos.length === 0) {
            alert('Добавьте хотя бы одно фото');
            return;
        }

        // Save post
        DATA.posts.push({
            id: Date.now(),
            title,
            desc,
            price: parseInt(price),
            tags,
            photos: selectedPhotos.slice(0, 8),
            platforms,
            date: new Date().toISOString()
        });
        saveData();

        // Also save to gallery
        DATA.gallery.push(...selectedPhotos.slice(0, 8));
        saveData();

        // Start "magic" - copy text and open platforms
        const text = `${title}\n${desc}\nЦена: ${price}₽\n#${tags.replace(/,/g, ' #')}`;

        try {
            await navigator.clipboard.writeText(text);
        } catch(e) {
            // fallback
            const ta = document.createElement('textarea');
            ta.value = text;
            document.body.appendChild(ta);
            ta.select();
            document.execCommand('copy');
            ta.remove();
        }

        // Open platforms (except VK which needs manual)
        for (const p of platforms) {
            const platform = DATA.socialPlatforms.find(s => s.id === p);
            if (platform && p !== 'vk') {
                window.open(platform.url, '_blank');
                await sleep(300);
            }
        }

        alert('✅ Текст скопирован в буфер!\nПлощадки открыты. Вставьте текст и опубликуйте.');

        // Clear form
        document.getElementById('pubTitle').value = '';
        document.getElementById('pubDesc').value = '';
        document.getElementById('pubPrice').value = '';
        document.getElementById('pubTags').value = '';
        selectedPhotos = [];
        renderPhotoPreviews();
        saveData();
    });

    function sleep(ms) { return new Promise(r => setTimeout(r, ms)); }

    // ============================================================
    // FINANCE
    // ============================================================
    let selectedFinancePath = [];

    function renderFinance() {
        const tree = DATA.finance.tree;
        const container = document.getElementById('financeTree');
        container.innerHTML = '';
        renderTreeNodes(container, tree, []);
        renderFinanceItems();
    }

    function renderTreeNodes(container, node, path) {
        const keys = Object.keys(node).filter(k => k !== 'items');
        for (const key of keys) {
            const isSelected = path.join('/') + '/' + key === selectedFinancePath.join('/');
            const folder = document.createElement('div');
            folder.className = 'folder' + (isSelected ? ' selected' : '');
            folder.innerHTML = `<span class="arrow ${isSelected ? 'open' : ''}">▶</span> ${key}`;
            folder.addEventListener('click', (e) => {
                e.stopPropagation();
                selectedFinancePath = [...path, key];
                renderFinance();
            });
            container.appendChild(folder);
            if (isSelected) {
                const children = document.createElement('div');
                children.className = 'children';
                const subNode = getNodeByPath([...path, key]);
                if (subNode) {
                    renderTreeNodes(children, subNode, [...path, key]);
                }
                container.appendChild(children);
                // render items
                renderFinanceItems();
            }
        }
    }

    function getNodeByPath(path) {
        let node = DATA.finance.tree;
        for (const key of path) {
            if (node[key]) node = node[key];
            else return null;
        }
        return node;
    }

    function renderFinanceItems() {
        const container = document.getElementById('financeItems');
        const node = getNodeByPath(selectedFinancePath);
        if (!node) {
            container.innerHTML = '<div class="empty">Выберите категорию</div>';
            return;
        }
        let items = node.items || [];
        // flatten: include items from subfolders
        for (const key of Object.keys(node)) {
            if (key !== 'items' && node[key] && node[key].items) {
                items = items.concat(node[key].items);
            }
        }
        if (items.length === 0) {
            container.innerHTML = '<div class="empty">Нет изделий в этой категории</div>';
            return;
        }
        let html = '<div class="item-row"><span class="name">Название</span><span>Затраты</span><span>Прибыль</span><span>%</span><span></span></div>';
        for (const item of items) {
            const profit = item.profit || 0;
            const cost = item.cost || 0;
            const pct = cost > 0 ? Math.round((profit / cost) * 100) : 0;
            html += `<div class="item-row">
                <span class="name">${item.name}</span>
                <span>${cost}₽</span>
                <span class="${profit > 0 ? 'profit' : 'loss'}">${profit}₽</span>
                <span>${pct}%</span>
                <span style="cursor:pointer;color:#5a4a4a;" data-del-item="${item.name}">✕</span>
            </div>`;
        }
        container.innerHTML = html;
        // delete handlers
        container.querySelectorAll('[data-del-item]').forEach(el => {
            el.addEventListener('click', () => {
                const name = el.dataset.delItem;
                const node2 = getNodeByPath(selectedFinancePath);
                if (node2 && node2.items) {
                    const idx = node2.items.findIndex(i => i.name === name);
                    if (idx > -1) {
                        node2.items.splice(idx, 1);
                        saveData();
                        renderFinanceItems();
                    }
                }
            });
        });
    }

    document.getElementById('financeAddBtn').addEventListener('click', () => {
        const name = document.getElementById('financeItemName').value.trim();
        const cost = parseInt(document.getElementById('financeItemCost').value) || 0;
        const profit = parseInt(document.getElementById('financeItemProfit').value) || 0;
        if (!name) { alert('Введите название'); return; }
        const node = getNodeByPath(selectedFinancePath);
        if (!node) { alert('Выберите категорию'); return; }
        if (!node.items) node.items = [];
        node.items.push({ name, cost, profit });
        document.getElementById('financeItemName').value = '';
        document.getElementById('financeItemCost').value = '';
        document.getElementById('financeItemProfit').value = '';
        saveData();
        renderFinanceItems();
    });

    // ============================================================
    // SOCIAL
    // ============================================================
    function renderSocial() {
        const container = document.getElementById('socialList');
        container.innerHTML = '';
        DATA.socialPlatforms.forEach(p => {
            const div = document.createElement('div');
            div.className = 'social-item';
            div.innerHTML = `
                <span class="name">${p.name}</span>
                <button class="check-btn" data-url="${p.url}">Проверить</button>
            `;
            container.appendChild(div);
        });
        container.querySelectorAll('.check-btn').forEach(btn => {
            btn.addEventListener('click', () => {
                window.open(btn.dataset.url, '_blank');
            });
        });
    }

    // ============================================================
    // FESTIVALS
    // ============================================================
    const FEST_STATUSES = ['Планирую', 'Заявка отправлена', 'Участвую', 'Отказ'];

    function renderFestivals() {
        const container = document.getElementById('festivalList');
        if (DATA.festivals.length === 0) {
            container.innerHTML = '<div class="text-muted text-center" style="padding:20px;">Нет фестивалей</div>';
            return;
        }
        container.innerHTML = '';
        DATA.festivals.forEach((f, idx) => {
            const div = document.createElement('div');
            div.className = 'festival-card';
            div.innerHTML = `
                <div class="info">
                    <div class="name">${f.name}</div>
                    <div class="date">${f.date || 'Дата не указана'}</div>
                </div>
                <span class="status" data-idx="${idx}">${f.status}</span>
                <button class="delete-fest" data-idx="${idx}">✕</button>
            `;
            container.appendChild(div);
        });
        container.querySelectorAll('.status').forEach(el => {
            el.addEventListener('click', () => {
                const idx = parseInt(el.dataset.idx);
                const current = DATA.festivals[idx].status;
                const nextIdx = (FEST_STATUSES.indexOf(current) + 1) % FEST_STATUSES.length;
                DATA.festivals[idx].status = FEST_STATUSES[nextIdx];
                saveData();
                renderFestivals();
            });
        });
        container.querySelectorAll('.delete-fest').forEach(el => {
            el.addEventListener('click', () => {
                const idx = parseInt(el.dataset.idx);
                DATA.festivals.splice(idx, 1);
                saveData();
                renderFestivals();
            });
        });
    }

    document.getElementById('festAddBtn').addEventListener('click', () => {
        const name = document.getElementById('festName').value.trim();
        const date = document.getElementById('festDate').value;
        if (!name) { alert('Введите название фестиваля'); return; }
        DATA.festivals.push({
            id: Date.now(),
            name,
            date: date || 'Дата не указана',
            status: 'Планирую'
        });
        document.getElementById('festName').value = '';
        document.getElementById('festDate').value = '';
        saveData();
        renderFestivals();
    });

    // ============================================================
    // CALENDAR
    // ============================================================
    let calYear = new Date().getFullYear();
    let calMonth = new Date().getMonth();
    let calSelectedDate = null;

    function renderCalendar() {
        const grid = document.getElementById('calGrid');
        const monthYear = document.getElementById('calMonthYear');
        const monthNames = ['Январь','Февраль','Март','Апрель','Май','Июнь','Июль','Август','Сентябрь','Октябрь','Ноябрь','Декабрь'];
        monthYear.textContent = `${monthNames[calMonth]} ${calYear}`;

        grid.innerHTML = '';
        ['Пн','Вт','Ср','Чт','Пт','Сб','Вс'].forEach(d => {
            const div = document.createElement('div');
            div.className = 'cal-header';
            div.textContent = d;
            grid.appendChild(div);
        });

        const firstDay = new Date(calYear, calMonth, 1).getDay();
        const daysInMonth = new Date(calYear, calMonth + 1, 0).getDate();
        const daysInPrev = new Date(calYear, calMonth, 0).getDate();

        // adjust for Monday start
        let startOffset = (firstDay === 0) ? 6 : firstDay - 1;

        const today = new Date();
        const todayStr = `${today.getFullYear()}-${String(today.getMonth()+1).padStart(2,'0')}-${String(today.getDate()).padStart(2,'0')}`;

        for (let i = startOffset; i > 0; i--) {
            const day = daysInPrev - i + 1;
            const div = document.createElement('div');
            div.className = 'cal-day other-month';
            div.textContent = day;
            grid.appendChild(div);
        }

        for (let d = 1; d <= daysInMonth; d++) {
            const dateStr = `${calYear}-${String(calMonth+1).padStart(2,'0')}-${String(d).padStart(2,'0')}`;
            const div = document.createElement('button');
            div.className = 'cal-day';
            if (dateStr === todayStr) div.classList.add('today');
            if (DATA.calendar[dateStr] && DATA.calendar[dateStr].length > 0) {
                div.classList.add('has-event');
            }
            div.textContent = d;
            div.dataset.date = dateStr;
            div.addEventListener('click', () => {
                calSelectedDate = dateStr;
                renderCalendarEvents();
            });
            grid.appendChild(div);
        }

        const totalCells = grid.children.length;
        const remaining = 42 - totalCells;
        for (let i = 1; i <= remaining; i++) {
            const div = document.createElement('div');
            div.className = 'cal-day other-month';
            div.textContent = i;
            grid.appendChild(div);
        }

        renderCalendarEvents();
    }

    function renderCalendarEvents() {
        const container = document.getElementById('calEventsList');
        if (!calSelectedDate || !DATA.calendar[calSelectedDate] || DATA.calendar[calSelectedDate].length === 0) {
            container.innerHTML = '<div class="text-muted text-center" style="padding:8px;">Нет событий на этот день</div>';
            return;
        }
        container.innerHTML = '';
        DATA.calendar[calSelectedDate].forEach((ev, idx) => {
            const div = document.createElement('div');
            div.className = 'cal-event-item';
            div.innerHTML = `
                <span class="event-check ${ev.checked ? 'done' : ''}" data-idx="${idx}"></span>
                <span class="event-text">${ev.text}</span>
                <button class="event-del" data-idx="${idx}">✕</button>
            `;
            container.appendChild(div);
        });
        container.querySelectorAll('.event-check').forEach(el => {
            el.addEventListener('click', () => {
                const idx = parseInt(el.dataset.idx);
                DATA.calendar[calSelectedDate][idx].checked = !DATA.calendar[calSelectedDate][idx].checked;
                saveData();
                renderCalendarEvents();
                renderCalendar();
            });
        });
        container.querySelectorAll('.event-del').forEach(el => {
            el.addEventListener('click', () => {
                const idx = parseInt(el.dataset.idx);
                DATA.calendar[calSelectedDate].splice(idx, 1);
                if (DATA.calendar[calSelectedDate].length === 0) delete DATA.calendar[calSelectedDate];
                saveData();
                renderCalendarEvents();
                renderCalendar();
            });
        });
    }

    document.getElementById('calEventAdd').addEventListener('click', () => {
        const input = document.getElementById('calEventInput');
        const text = input.value.trim();
        if (!text) return;
        if (!calSelectedDate) {
            const today = new Date();
            calSelectedDate = `${today.getFullYear()}-${String(today.getMonth()+1).padStart(2,'0')}-${String(today.getDate()).padStart(2,'0')}`;
        }
        if (!DATA.calendar[calSelectedDate]) DATA.calendar[calSelectedDate] = [];
        DATA.calendar[calSelectedDate].push({ text, checked: false });
        input.value = '';
        saveData();
        renderCalendarEvents();
        renderCalendar();
    });

    document.getElementById('calPrev').addEventListener('click', () => {
        calMonth--;
        if (calMonth < 0) { calMonth = 11; calYear--; }
        renderCalendar();
    });
    document.getElementById('calNext').addEventListener('click', () => {
        calMonth++;
        if (calMonth > 11) { calMonth = 0; calYear++; }
        renderCalendar();
    });

    // ============================================================
    // NOTES
    // ============================================================
    document.querySelectorAll('.notes-grid textarea').forEach(ta => {
        ta.value = DATA.notes[ta.dataset.note] || '';
        ta.addEventListener('input', () => {
            DATA.notes[ta.dataset.note] = ta.value;
            saveData();
        });
    });

    // ============================================================
    // GALLERY
    // ============================================================
    function renderGallery() {
        const grid = document.getElementById('galleryGrid');
        if (DATA.gallery.length === 0) {
            grid.innerHTML = '<div class="text-muted text-center" style="grid-column:1/-1;padding:30px;">Галерея пуста</div>';
            return;
        }
        grid.innerHTML = '';
        DATA.gallery.forEach((src, i) => {
            const div = document.createElement('div');
            div.className = 'gallery-item';
            div.innerHTML = `
                <img src="${src}" alt="Работа ${i+1}">
                <button class="del-gallery" data-idx="${i}">✕</button>
            `;
            grid.appendChild(div);
        });
        grid.querySelectorAll('.del-gallery').forEach(el => {
            el.addEventListener('click', () => {
                const idx = parseInt(el.dataset.idx);
                DATA.gallery.splice(idx, 1);
                saveData();
                renderGallery();
            });
        });
    }

    // ============================================================
    // SETTINGS
    // ============================================================
    document.getElementById('settingsPinSave').addEventListener('click', () => {
        const val = document.getElementById('settingsPin').value.trim();
        if (val.length === 4 && /^\d{4}$/.test(val)) {
            DATA.pin = val;
            saveData();
            alert('Пин-код обновлён!');
            document.getElementById('settingsPin').value = '';
        } else {
            alert('Пин-код должен быть ровно 4 цифры');
        }
    });

    // ============================================================
    // INIT
    // ============================================================
    loadData();
    updateDataSize();

    // Show pin screen first
    document.getElementById('pinScreen').classList.remove('hidden');
    document.getElementById('pinScreen').classList.add('active');

    // Pre-fill calendar with today selected
    const today = new Date();
    calSelectedDate = `${today.getFullYear()}-${String(today.getMonth()+1).padStart(2,'0')}-${String(today.getDate()).padStart(2,'0')}`;

    // Auto-save on page unload
    window.addEventListener('beforeunload', saveData);

    // Keyboard support for PIN (for desktop testing)
    document.addEventListener('keydown', (e) => {
        if (document.getElementById('pinScreen').classList.contains('hidden')) return;
        if (e.key >= '0' && e.key <= '9') {
            handlePinInput(e.key);
        } else if (e.key === 'Backspace' || e.key === 'Delete') {
            handlePinInput('del');
        }
    });

    console.log('🦉 Мастерская Эльфа загружена!');
    console.log('📦 Данные в localStorage:', Object.keys(localStorage));
</script>

</body>
</html>
