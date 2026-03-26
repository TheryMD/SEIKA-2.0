<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>CBA La Paz — Hub de Atención</title>
<link href="https://fonts.googleapis.com/css2?family=DM+Sans:wght@300;400;500;600&family=DM+Serif+Display:ital@0;1&display=swap" rel="stylesheet">
<style>
  :root {
    --navy: #0a2540;
    --blue: #1a56db;
    --blue-light: #e8f0fe;
    --blue-mid: #3b82f6;
    --accent: #f59e0b;
    --accent-light: #fef3c7;
    --green: #10b981;
    --green-light: #d1fae5;
    --red: #ef4444;
    --red-light: #fee2e2;
    --gray-50: #f8fafc;
    --gray-100: #f1f5f9;
    --gray-200: #e2e8f0;
    --gray-400: #94a3b8;
    --gray-600: #475569;
    --gray-700: #334155;
    --gray-800: #1e293b;
    --white: #ffffff;
    --sidebar-w: 220px;
    --radius: 10px;
    --shadow: 0 1px 3px rgba(0,0,0,0.08), 0 1px 2px rgba(0,0,0,0.04);
    --shadow-md: 0 4px 12px rgba(0,0,0,0.08);
  }
  * { box-sizing: border-box; margin: 0; padding: 0; }
  body {
    font-family: 'DM Sans', sans-serif;
    background: var(--gray-50);
    color: var(--gray-800);
    display: flex;
    min-height: 100vh;
    font-size: 14px;
  }

  /* SIDEBAR */
  .sidebar {
    width: var(--sidebar-w);
    background: var(--navy);
    min-height: 100vh;
    position: fixed;
    top: 0; left: 0;
    display: flex;
    flex-direction: column;
    padding: 0;
    z-index: 100;
  }
  .sidebar-logo {
    padding: 20px 20px 16px;
    border-bottom: 1px solid rgba(255,255,255,0.08);
  }
  .sidebar-logo .logo-title {
    font-family: 'DM Serif Display', serif;
    font-size: 18px;
    color: white;
    line-height: 1.2;
  }
  .sidebar-logo .logo-sub {
    font-size: 11px;
    color: rgba(255,255,255,0.45);
    margin-top: 2px;
    letter-spacing: 0.05em;
    text-transform: uppercase;
  }
  .sidebar-nav {
    flex: 1;
    padding: 12px 0;
  }
  .nav-label {
    font-size: 10px;
    font-weight: 600;
    color: rgba(255,255,255,0.3);
    text-transform: uppercase;
    letter-spacing: 0.1em;
    padding: 8px 20px 4px;
    margin-top: 8px;
  }
  .nav-item {
    display: flex;
    align-items: center;
    gap: 10px;
    padding: 9px 20px;
    color: rgba(255,255,255,0.65);
    cursor: pointer;
    border-radius: 0;
    font-size: 13.5px;
    font-weight: 400;
    transition: all 0.15s;
    border-left: 2px solid transparent;
  }
  .nav-item:hover { color: white; background: rgba(255,255,255,0.06); }
  .nav-item.active {
    color: white;
    background: rgba(255,255,255,0.1);
    border-left: 2px solid var(--accent);
    font-weight: 500;
  }
  .nav-item .nav-icon { font-size: 16px; width: 18px; text-align: center; }
  .sidebar-footer {
    padding: 16px 20px;
    border-top: 1px solid rgba(255,255,255,0.08);
  }
  .sidebar-footer .status-dot {
    display: inline-block;
    width: 7px; height: 7px;
    border-radius: 50%;
    background: var(--green);
    margin-right: 6px;
  }
  .sidebar-footer span {
    font-size: 12px;
    color: rgba(255,255,255,0.45);
  }
  .time-display {
    font-size: 11px;
    color: rgba(255,255,255,0.3);
    margin-top: 4px;
  }

  /* MAIN */
  .main {
    margin-left: var(--sidebar-w);
    flex: 1;
    display: flex;
    flex-direction: column;
  }
  .topbar {
    background: white;
    border-bottom: 1px solid var(--gray-200);
    padding: 0 28px;
    height: 56px;
    display: flex;
    align-items: center;
    justify-content: space-between;
    position: sticky;
    top: 0;
    z-index: 50;
  }
  .topbar-title {
    font-size: 16px;
    font-weight: 500;
    color: var(--gray-800);
  }
  .topbar-right {
    display: flex;
    align-items: center;
    gap: 12px;
  }
  .badge-alert {
    background: var(--red-light);
    color: #b91c1c;
    font-size: 11px;
    font-weight: 600;
    padding: 3px 10px;
    border-radius: 20px;
    animation: pulse-badge 2s infinite;
  }
  @keyframes pulse-badge {
    0%, 100% { opacity: 1; }
    50% { opacity: 0.7; }
  }
  .content {
    padding: 24px 28px;
    flex: 1;
  }

  /* SECTION VISIBILITY */
  .section { display: none; }
  .section.active { display: block; }

  /* CARDS */
  .card {
    background: white;
    border: 1px solid var(--gray-200);
    border-radius: var(--radius);
    padding: 20px;
    box-shadow: var(--shadow);
  }
  .card-title {
    font-size: 13px;
    font-weight: 600;
    color: var(--gray-600);
    text-transform: uppercase;
    letter-spacing: 0.06em;
    margin-bottom: 16px;
  }

  /* DASHBOARD */
  .alert-banner {
    background: linear-gradient(135deg, #1a56db 0%, #1e40af 100%);
    color: white;
    border-radius: var(--radius);
    padding: 16px 22px;
    margin-bottom: 20px;
    display: flex;
    align-items: center;
    justify-content: space-between;
  }
  .alert-banner .alert-text { font-size: 14px; font-weight: 500; }
  .alert-banner .alert-sub { font-size: 12px; opacity: 0.75; margin-top: 2px; }
  .alert-banner .alert-icon { font-size: 28px; opacity: 0.8; }

  .grid-4 { display: grid; grid-template-columns: repeat(4, 1fr); gap: 14px; margin-bottom: 20px; }
  .metric-card {
    background: white;
    border: 1px solid var(--gray-200);
    border-radius: var(--radius);
    padding: 16px 18px;
    box-shadow: var(--shadow);
  }
  .metric-card .m-label { font-size: 11px; color: var(--gray-400); font-weight: 500; text-transform: uppercase; letter-spacing: 0.05em; }
  .metric-card .m-value { font-size: 26px; font-weight: 600; color: var(--gray-800); margin: 4px 0 2px; line-height: 1; }
  .metric-card .m-sub { font-size: 12px; color: var(--gray-400); }
  .metric-card.blue { border-top: 3px solid var(--blue-mid); }
  .metric-card.amber { border-top: 3px solid var(--accent); }
  .metric-card.green { border-top: 3px solid var(--green); }
  .metric-card.red { border-top: 3px solid var(--red); }

  .grid-2 { display: grid; grid-template-columns: 1fr 1fr; gap: 14px; margin-bottom: 20px; }
  .grid-3 { display: grid; grid-template-columns: repeat(3, 1fr); gap: 14px; margin-bottom: 20px; }

  .dates-list { list-style: none; }
  .dates-list li {
    display: flex;
    align-items: center;
    gap: 12px;
    padding: 10px 0;
    border-bottom: 1px solid var(--gray-100);
  }
  .dates-list li:last-child { border-bottom: none; }
  .date-chip {
    background: var(--blue-light);
    color: var(--blue);
    font-size: 11px;
    font-weight: 600;
    padding: 4px 10px;
    border-radius: 20px;
    white-space: nowrap;
    min-width: 80px;
    text-align: center;
  }
  .date-chip.red { background: var(--red-light); color: var(--red); }
  .date-chip.green { background: var(--green-light); color: #065f46; }
  .date-chip.amber { background: var(--accent-light); color: #92400e; }
  .dates-list li .d-text { font-size: 13px; font-weight: 500; color: var(--gray-700); }
  .dates-list li .d-sub { font-size: 11px; color: var(--gray-400); }

  .contacts-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 10px;
  }
  .contact-card {
    background: var(--gray-50);
    border: 1px solid var(--gray-200);
    border-radius: 8px;
    padding: 12px 14px;
    display: flex;
    align-items: center;
    gap: 12px;
  }
  .contact-avatar {
    width: 36px; height: 36px;
    border-radius: 50%;
    background: var(--blue-light);
    color: var(--blue);
    display: flex;
    align-items: center;
    justify-content: center;
    font-weight: 600;
    font-size: 13px;
    flex-shrink: 0;
  }
  .contact-avatar.green { background: var(--green-light); color: #065f46; }
  .contact-name { font-size: 13px; font-weight: 500; }
  .contact-role { font-size: 11px; color: var(--gray-400); }
  .contact-num { font-size: 12px; color: var(--blue); font-weight: 500; cursor: pointer; }

  /* FAQ */
  .search-bar {
    display: flex;
    align-items: center;
    background: white;
    border: 1px solid var(--gray-200);
    border-radius: var(--radius);
    padding: 0 14px;
    margin-bottom: 16px;
    box-shadow: var(--shadow);
  }
  .search-bar input {
    border: none;
    outline: none;
    flex: 1;
    padding: 12px 8px;
    font-family: 'DM Sans', sans-serif;
    font-size: 14px;
    color: var(--gray-800);
    background: transparent;
  }
  .search-bar .search-icon { color: var(--gray-400); font-size: 16px; }
  .faq-filters {
    display: flex;
    gap: 8px;
    flex-wrap: wrap;
    margin-bottom: 16px;
  }
  .filter-btn {
    padding: 5px 14px;
    border-radius: 20px;
    border: 1px solid var(--gray-200);
    background: white;
    font-family: 'DM Sans', sans-serif;
    font-size: 12px;
    font-weight: 500;
    color: var(--gray-600);
    cursor: pointer;
    transition: all 0.15s;
  }
  .filter-btn:hover { border-color: var(--blue); color: var(--blue); }
  .filter-btn.active { background: var(--blue); color: white; border-color: var(--blue); }
  .faq-grid { display: flex; flex-direction: column; gap: 8px; }
  .faq-item {
    background: white;
    border: 1px solid var(--gray-200);
    border-radius: var(--radius);
    overflow: hidden;
    box-shadow: var(--shadow);
    transition: border-color 0.15s;
  }
  .faq-item:hover { border-color: var(--blue-mid); }
  .faq-q {
    padding: 14px 18px;
    font-weight: 500;
    font-size: 13.5px;
    cursor: pointer;
    display: flex;
    justify-content: space-between;
    align-items: center;
    color: var(--gray-800);
  }
  .faq-q .faq-category {
    font-size: 10px;
    font-weight: 600;
    text-transform: uppercase;
    letter-spacing: 0.06em;
    padding: 2px 8px;
    border-radius: 20px;
    white-space: nowrap;
    flex-shrink: 0;
    margin-left: 8px;
  }
  .cat-precios { background: var(--accent-light); color: #92400e; }
  .cat-horarios { background: var(--blue-light); color: #1e40af; }
  .cat-requisitos { background: var(--green-light); color: #065f46; }
  .cat-graduacion { background: #fce7f3; color: #9d174d; }
  .cat-convenios { background: #f3e8ff; color: #6b21a8; }
  .faq-toggle { font-size: 16px; color: var(--gray-400); transition: transform 0.2s; flex-shrink: 0; }
  .faq-a {
    padding: 0 18px;
    max-height: 0;
    overflow: hidden;
    transition: max-height 0.3s, padding 0.2s;
    font-size: 13px;
    color: var(--gray-600);
    line-height: 1.7;
    background: var(--gray-50);
  }
  .faq-item.open .faq-a {
    padding: 14px 18px;
    max-height: 300px;
  }
  .faq-item.open .faq-toggle { transform: rotate(45deg); }
  .copy-answer-btn {
    display: inline-flex;
    align-items: center;
    gap: 6px;
    margin-top: 10px;
    padding: 6px 12px;
    background: white;
    border: 1px solid var(--gray-200);
    border-radius: 6px;
    font-size: 12px;
    font-weight: 500;
    color: var(--gray-600);
    cursor: pointer;
    transition: all 0.15s;
  }
  .copy-answer-btn:hover { border-color: var(--blue); color: var(--blue); }
  .copy-answer-btn.copied { background: var(--green-light); color: #065f46; border-color: var(--green); }

  /* TEMPLATES */
  .template-grid { display: flex; flex-direction: column; gap: 12px; }
  .template-card {
    background: white;
    border: 1px solid var(--gray-200);
    border-radius: var(--radius);
    overflow: hidden;
    box-shadow: var(--shadow);
  }
  .template-header {
    padding: 12px 18px;
    border-bottom: 1px solid var(--gray-100);
    display: flex;
    align-items: center;
    justify-content: space-between;
    background: var(--gray-50);
  }
  .template-name { font-size: 13px; font-weight: 600; color: var(--gray-700); }
  .template-tag {
    font-size: 10px;
    font-weight: 600;
    text-transform: uppercase;
    letter-spacing: 0.06em;
    padding: 2px 8px;
    border-radius: 20px;
  }
  .tag-wa { background: #dcfce7; color: #166534; }
  .tag-fb { background: #dbeafe; color: #1e40af; }
  .tag-general { background: var(--gray-100); color: var(--gray-600); }
  .template-body {
    padding: 14px 18px;
    font-size: 13px;
    color: var(--gray-600);
    line-height: 1.75;
    font-family: monospace;
    white-space: pre-wrap;
    background: #fafbfc;
    border-bottom: 1px solid var(--gray-100);
  }
  .template-footer {
    padding: 10px 18px;
    display: flex;
    justify-content: flex-end;
    gap: 8px;
  }
  .btn {
    display: inline-flex;
    align-items: center;
    gap: 6px;
    padding: 7px 14px;
    border-radius: 7px;
    border: 1px solid var(--gray-200);
    font-family: 'DM Sans', sans-serif;
    font-size: 12px;
    font-weight: 500;
    cursor: pointer;
    transition: all 0.15s;
    background: white;
    color: var(--gray-700);
  }
  .btn:hover { border-color: var(--blue); color: var(--blue); }
  .btn-primary {
    background: var(--blue);
    color: white;
    border-color: var(--blue);
  }
  .btn-primary:hover { background: #1648c0; border-color: #1648c0; color: white; }
  .btn.copied { background: var(--green-light); color: #065f46; border-color: var(--green); }

  /* CRM */
  .crm-header {
    display: flex;
    align-items: center;
    justify-content: space-between;
    margin-bottom: 16px;
  }
  .crm-table-wrap {
    background: white;
    border: 1px solid var(--gray-200);
    border-radius: var(--radius);
    overflow: hidden;
    box-shadow: var(--shadow);
  }
  table { width: 100%; border-collapse: collapse; }
  thead { background: var(--gray-50); }
  th {
    text-align: left;
    padding: 10px 16px;
    font-size: 11px;
    font-weight: 600;
    text-transform: uppercase;
    letter-spacing: 0.06em;
    color: var(--gray-400);
    border-bottom: 1px solid var(--gray-200);
  }
  td {
    padding: 12px 16px;
    font-size: 13px;
    color: var(--gray-700);
    border-bottom: 1px solid var(--gray-100);
  }
  tr:last-child td { border-bottom: none; }
  tr:hover td { background: var(--gray-50); }
  .status-pill {
    display: inline-block;
    padding: 3px 10px;
    border-radius: 20px;
    font-size: 11px;
    font-weight: 600;
  }
  .s-pending { background: var(--accent-light); color: #92400e; }
  .s-resolved { background: var(--green-light); color: #065f46; }
  .s-escalated { background: var(--red-light); color: #b91c1c; }
  .channel-icon { display: inline-flex; align-items: center; gap: 5px; font-size: 12px; }

  /* MODAL */
  .modal-overlay {
    display: none;
    position: fixed;
    inset: 0;
    background: rgba(0,0,0,0.4);
    z-index: 200;
    align-items: center;
    justify-content: center;
  }
  .modal-overlay.open { display: flex; }
  .modal {
    background: white;
    border-radius: 14px;
    padding: 28px;
    width: 480px;
    max-width: 90vw;
    box-shadow: 0 20px 60px rgba(0,0,0,0.15);
  }
  .modal h3 { font-size: 16px; font-weight: 600; margin-bottom: 20px; color: var(--gray-800); }
  .form-group { margin-bottom: 14px; }
  .form-group label { display: block; font-size: 12px; font-weight: 600; color: var(--gray-600); margin-bottom: 5px; text-transform: uppercase; letter-spacing: 0.05em; }
  .form-group input, .form-group select, .form-group textarea {
    width: 100%;
    padding: 9px 12px;
    border: 1px solid var(--gray-200);
    border-radius: 7px;
    font-family: 'DM Sans', sans-serif;
    font-size: 13px;
    color: var(--gray-800);
    outline: none;
    transition: border-color 0.15s;
  }
  .form-group input:focus, .form-group select:focus, .form-group textarea:focus {
    border-color: var(--blue-mid);
  }
  .form-group textarea { resize: vertical; min-height: 80px; }
  .modal-footer { display: flex; justify-content: flex-end; gap: 8px; margin-top: 20px; }

  /* AI ASSISTANT */
  .ai-container {
    display: flex;
    flex-direction: column;
    height: calc(100vh - 150px);
    min-height: 400px;
  }
  .ai-chat-area {
    flex: 1;
    overflow-y: auto;
    display: flex;
    flex-direction: column;
    gap: 14px;
    padding: 20px;
    background: white;
    border: 1px solid var(--gray-200);
    border-radius: var(--radius) var(--radius) 0 0;
  }
  .msg {
    display: flex;
    gap: 10px;
    align-items: flex-start;
    max-width: 80%;
  }
  .msg.user { align-self: flex-end; flex-direction: row-reverse; }
  .msg-avatar {
    width: 30px; height: 30px;
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 13px;
    font-weight: 600;
    flex-shrink: 0;
  }
  .msg-avatar.bot { background: var(--navy); color: white; font-size: 14px; }
  .msg-avatar.user { background: var(--blue-light); color: var(--blue); }
  .msg-bubble {
    padding: 10px 14px;
    border-radius: 12px;
    font-size: 13.5px;
    line-height: 1.6;
  }
  .msg.bot .msg-bubble {
    background: var(--gray-50);
    border: 1px solid var(--gray-200);
    color: var(--gray-800);
    border-top-left-radius: 3px;
  }
  .msg.user .msg-bubble {
    background: var(--blue);
    color: white;
    border-top-right-radius: 3px;
  }
  .msg-time { font-size: 10px; color: var(--gray-400); margin-top: 3px; }
  .ai-input-area {
    background: white;
    border: 1px solid var(--gray-200);
    border-top: none;
    border-radius: 0 0 var(--radius) var(--radius);
    padding: 14px 16px;
    display: flex;
    gap: 10px;
    align-items: flex-end;
  }
  .ai-input-area textarea {
    flex: 1;
    border: 1px solid var(--gray-200);
    border-radius: 8px;
    padding: 9px 12px;
    font-family: 'DM Sans', sans-serif;
    font-size: 13.5px;
    resize: none;
    min-height: 42px;
    max-height: 100px;
    outline: none;
    transition: border-color 0.15s;
    color: var(--gray-800);
  }
  .ai-input-area textarea:focus { border-color: var(--blue-mid); }
  .send-btn {
    width: 40px; height: 40px;
    background: var(--blue);
    color: white;
    border: none;
    border-radius: 8px;
    cursor: pointer;
    font-size: 16px;
    display: flex;
    align-items: center;
    justify-content: center;
    flex-shrink: 0;
    transition: background 0.15s;
  }
  .send-btn:hover { background: #1648c0; }
  .send-btn:disabled { background: var(--gray-200); cursor: not-allowed; }
  .quick-prompts {
    display: flex;
    flex-wrap: wrap;
    gap: 6px;
    padding: 10px 0 0;
  }
  .quick-btn {
    padding: 5px 12px;
    border: 1px solid var(--gray-200);
    border-radius: 20px;
    background: white;
    font-family: 'DM Sans', sans-serif;
    font-size: 12px;
    color: var(--gray-600);
    cursor: pointer;
    transition: all 0.15s;
  }
  .quick-btn:hover { border-color: var(--blue); color: var(--blue); }
  .typing-indicator { display: flex; gap: 4px; align-items: center; padding: 8px 0; }
  .typing-dot {
    width: 7px; height: 7px;
    border-radius: 50%;
    background: var(--gray-400);
    animation: typing 1.2s infinite;
  }
  .typing-dot:nth-child(2) { animation-delay: 0.2s; }
  .typing-dot:nth-child(3) { animation-delay: 0.4s; }
  @keyframes typing { 0%, 60%, 100% { opacity: 0.3; transform: scale(1); } 30% { opacity: 1; transform: scale(1.2); } }

  /* SCROLLBAR */
  ::-webkit-scrollbar { width: 5px; }
  ::-webkit-scrollbar-track { background: transparent; }
  ::-webkit-scrollbar-thumb { background: var(--gray-200); border-radius: 10px; }
</style>
</head>
<body>

<aside class="sidebar">
  <div class="sidebar-logo">
    <div class="logo-title">CBA La Paz</div>
    <div class="logo-sub">Hub de Atención</div>
  </div>
  <nav class="sidebar-nav">
    <div class="nav-label">Principal</div>
    <div class="nav-item active" onclick="showSection('dashboard', this)">
      <span class="nav-icon">🏠</span> Dashboard
    </div>
    <div class="nav-item" onclick="showSection('ia', this)">
      <span class="nav-icon">🤖</span> Asistente IA
    </div>
    <div class="nav-label">Herramientas</div>
    <div class="nav-item" onclick="showSection('faq', this)">
      <span class="nav-icon">📚</span> Base FAQ
    </div>
    <div class="nav-item" onclick="showSection('templates', this)">
      <span class="nav-icon">💬</span> Plantillas
    </div>
    <div class="nav-item" onclick="showSection('crm', this)">
      <span class="nav-icon">📋</span> Consultas
    </div>
    <div class="nav-label">Recursos</div>
    <div class="nav-item" onclick="window.open('https://docs.google.com/forms/d/e/1FAIpQLSdEHeWCBCr4XmhIV8D853UACpynwIif5fuUvX_vBGT0tlpQZQ/viewform','_blank')">
      <span class="nav-icon">📝</span> Formulario
    </div>
    <div class="nav-item" onclick="window.open('https://tinyurl.com/39kdw67a','_blank')">
      <span class="nav-icon">🎓</span> Plataforma
    </div>
  </nav>
  <div class="sidebar-footer">
    <span class="status-dot"></span><span>Servicio activo</span>
    <div class="time-display" id="clock">–</div>
  </div>
</aside>

<main class="main">
  <div class="topbar">
    <div class="topbar-title" id="page-title">Dashboard</div>
    <div class="topbar-right">
      <span class="badge-alert" id="alert-badge">⚡ Hoy: inicio de clases</span>
    </div>
  </div>
  <div class="content">

    <!-- DASHBOARD -->
    <div class="section active" id="s-dashboard">
      <div class="alert-banner">
        <div>
          <div class="alert-text">📅 Inicio de clases: 16 de marzo — ¡Hoy!</div>
          <div class="alert-sub">Próximas inscripciones: 7 y 8 de mayo · Inicio: 11 de mayo</div>
        </div>
        <div class="alert-icon">🎓</div>
      </div>

      <div class="grid-4">
        <div class="metric-card blue">
          <div class="m-label">Módulo Básico</div>
          <div class="m-value">Bs. 815</div>
          <div class="m-sub">Regular / Acelerado</div>
        </div>
        <div class="metric-card amber">
          <div class="m-label">Módulo Avanzado</div>
          <div class="m-value">Bs. 865</div>
          <div class="m-sub">Regular / Acelerado</div>
        </div>
        <div class="metric-card green">
          <div class="m-label">El Alto (Básico)</div>
          <div class="m-value">Bs. 710</div>
          <div class="m-sub">Precio diferenciado</div>
        </div>
        <div class="metric-card red">
          <div class="m-label">Matrícula</div>
          <div class="m-value">Bs. 100</div>
          <div class="m-sub">Pago único</div>
        </div>
      </div>

      <div class="grid-2">
        <div class="card">
          <div class="card-title">📅 Fechas clave 2026</div>
          <ul class="dates-list">
            <li>
              <div><div class="date-chip green">16 Mar</div></div>
              <div><div class="d-text">Inicio de clases</div><div class="d-sub">Primer día — ciclo actual</div></div>
            </li>
            <li>
              <div><div class="date-chip red">23–24 Mar</div></div>
              <div><div class="d-text">Entrega de materiales</div><div class="d-sub">Libros Bs. 450 · válidos x3 módulos</div></div>
            </li>
            <li>
              <div><div class="date-chip amber">27 Mar</div></div>
              <div><div class="d-text">Graduación</div><div class="d-sub">A–J: 15:00 · L–Z: 19:00 · Bs. 390</div></div>
            </li>
            <li>
              <div><div class="date-chip">7–8 May</div></div>
              <div><div class="d-text">Próximas inscripciones</div><div class="d-sub">Inicio de clases: 11 de mayo</div></div>
            </li>
          </ul>
        </div>

        <div class="card">
          <div class="card-title">📞 Contactos rápidos</div>
          <div class="contacts-grid">
            <div class="contact-card">
              <div class="contact-avatar">AS</div>
              <div>
                <div class="contact-name">Arturo Saavedra</div>
                <div class="contact-role">Sistemas</div>
                <div class="contact-num" onclick="window.open('https://wa.me/59172578133','_blank')">📱 72578133</div>
              </div>
            </div>
            <div class="contact-card">
              <div class="contact-avatar green">JZ</div>
              <div>
                <div class="contact-name">Julieta Zuñagua</div>
                <div class="contact-role">Pagos en línea</div>
                <div class="contact-num" onclick="window.open('https://wa.me/59177201457','_blank')">📱 77201457</div>
              </div>
            </div>
          </div>
          <div style="margin-top: 14px; padding-top: 14px; border-top: 1px solid var(--gray-100);">
            <div class="card-title" style="margin-bottom: 10px;">🕐 Horarios de atención</div>
            <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 8px;">
              <div style="background: var(--blue-light); border-radius: 7px; padding: 10px 12px; font-size: 12px; color: #1e40af;">
                <strong>Oficina</strong><br>8:30–12:30<br>14:30–18:00
              </div>
              <div style="background: var(--green-light); border-radius: 7px; padding: 10px 12px; font-size: 12px; color: #065f46;">
                <strong>Línea</strong><br>10:00–12:00<br>15:00–18:00
              </div>
            </div>
          </div>
        </div>
      </div>

      <div class="card">
        <div class="card-title">🏫 Horarios por sede</div>
        <div style="display: grid; grid-template-columns: repeat(4, 1fr); gap: 12px; margin-top: 4px;">
          <div style="border: 1px solid var(--gray-200); border-radius: 8px; overflow: hidden;">
            <div style="background: var(--navy); color: white; padding: 9px 12px; font-size: 12px; font-weight: 600;">📍 Casa Central</div>
            <div style="padding: 10px 12px; font-size: 12px; color: var(--gray-600); line-height: 1.8;">
              <strong style="color: var(--gray-700);">Regular:</strong><br>
              07:15 · 14:45 · 16:25<br>18:05 · 19:45<br>
              <strong style="color: var(--gray-700);">Acelerado:</strong><br>
              08:55 – 12:05
            </div>
          </div>
          <div style="border: 1px solid var(--gray-200); border-radius: 8px; overflow: hidden;">
            <div style="background: #1e40af; color: white; padding: 9px 12px; font-size: 12px; font-weight: 600;">📍 Federico Zuazo</div>
            <div style="padding: 10px 12px; font-size: 12px; color: var(--gray-600); line-height: 1.8;">
              <strong style="color: var(--gray-700);">Regular:</strong><br>
              07:15 · 08:55 · 10:35<br>14:45 · 16:25 · 18:05 · 19:45<br>
              <strong style="color: var(--gray-700);">Acelerado:</strong><br>
              08:55 · 18:05
            </div>
          </div>
          <div style="border: 1px solid var(--gray-200); border-radius: 8px; overflow: hidden;">
            <div style="background: #065f46; color: white; padding: 9px 12px; font-size: 12px; font-weight: 600;">📍 El Alto</div>
            <div style="padding: 10px 12px; font-size: 12px; color: var(--gray-600); line-height: 1.8;">
              <strong style="color: var(--gray-700);">Regular:</strong><br>
              07:15 · 08:55 · 14:45<br>16:25 · 18:05 · 19:45<br>
              <strong style="color: var(--gray-700);">Acelerado:</strong><br>
              08:55 · 14:45 · 18:05
            </div>
          </div>
          <div style="border: 1px solid var(--gray-200); border-radius: 8px; overflow: hidden;">
            <div style="background: #6b21a8; color: white; padding: 9px 12px; font-size: 12px; font-weight: 600;">💻 Virtual</div>
            <div style="padding: 10px 12px; font-size: 12px; color: var(--gray-600); line-height: 1.8;">
              <strong style="color: var(--gray-700);">Regular:</strong><br>
              07:15 · 19:45<br>
              <strong style="color: var(--gray-700);">Acelerado:</strong><br>
              18:45 – 21:55<br>
              <strong style="color: var(--gray-700);">Sábados:</strong><br>
              08:00 – 14:30
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- IA ASSISTANT -->
    <div class="section" id="s-ia">
      <div class="ai-container">
        <div class="ai-chat-area" id="chat-area">
          <div class="msg bot">
            <div class="msg-avatar bot">🎓</div>
            <div>
              <div class="msg-bubble">¡Hola! Soy el asistente IA del CBA La Paz. Tengo toda la información del programa: precios, horarios, sedes, convenios, fechas y más. ¿En qué puedo ayudarte? 😊</div>
              <div class="msg-time">Ahora</div>
            </div>
          </div>
        </div>
        <div class="ai-input-area">
          <div style="flex: 1; display: flex; flex-direction: column; gap: 8px;">
            <textarea id="user-input" placeholder="Escribe tu consulta... (Ej: ¿Cuánto cuesta el módulo básico?)" rows="1" onkeydown="handleKey(event)"></textarea>
            <div class="quick-prompts">
              <button class="quick-btn" onclick="quickSend('¿Cuáles son los precios?')">Precios</button>
              <button class="quick-btn" onclick="quickSend('¿Cuáles son los requisitos de inscripción?')">Requisitos</button>
              <button class="quick-btn" onclick="quickSend('¿Qué horarios hay en Casa Central?')">Horarios</button>
              <button class="quick-btn" onclick="quickSend('¿Cómo es el programa acelerado?')">Acelerado</button>
              <button class="quick-btn" onclick="quickSend('¿Qué convenios tienen?')">Convenios</button>
              <button class="quick-btn" onclick="quickSend('¿Cuándo es la graduación?')">Graduación</button>
            </div>
          </div>
          <button class="send-btn" id="send-btn" onclick="sendMessage()">➤</button>
        </div>
      </div>
    </div>

    <!-- FAQ -->
    <div class="section" id="s-faq">
      <div class="search-bar">
        <span class="search-icon">🔍</span>
        <input type="text" id="faq-search" placeholder="Buscar pregunta..." oninput="filterFAQ()">
      </div>
      <div class="faq-filters">
        <button class="filter-btn active" onclick="setFilter('all', this)">Todas</button>
        <button class="filter-btn" onclick="setFilter('precios', this)">💰 Precios</button>
        <button class="filter-btn" onclick="setFilter('horarios', this)">🕐 Horarios</button>
        <button class="filter-btn" onclick="setFilter('requisitos', this)">📋 Requisitos</button>
        <button class="filter-btn" onclick="setFilter('graduacion', this)">🎓 Graduación</button>
        <button class="filter-btn" onclick="setFilter('convenios', this)">🤝 Convenios</button>
      </div>
      <div class="faq-grid" id="faq-grid"></div>
    </div>

    <!-- TEMPLATES -->
    <div class="section" id="s-templates">
      <div class="template-grid" id="templates-grid"></div>
    </div>

    <!-- CRM -->
    <div class="section" id="s-crm">
      <div class="crm-header">
        <div style="font-size: 14px; color: var(--gray-600);">Registro de consultas del día</div>
        <button class="btn btn-primary" onclick="openModal()">+ Nueva consulta</button>
      </div>
      <div class="crm-table-wrap">
        <table>
          <thead>
            <tr>
              <th>Nombre</th>
              <th>Consulta</th>
              <th>Canal</th>
              <th>Estado</th>
              <th>Hora</th>
              <th></th>
            </tr>
          </thead>
          <tbody id="crm-body"></tbody>
        </table>
      </div>
    </div>

  </div>
</main>

<!-- Modal nueva consulta -->
<div class="modal-overlay" id="modal">
  <div class="modal">
    <h3>Nueva consulta</h3>
    <div class="form-group">
      <label>Nombre</label>
      <input type="text" id="f-nombre" placeholder="Nombre del estudiante">
    </div>
    <div class="form-group">
      <label>Canal</label>
      <select id="f-canal">
        <option value="WhatsApp">📱 WhatsApp</option>
        <option value="Facebook">📘 Facebook</option>
        <option value="Teléfono">📞 Teléfono</option>
        <option value="Presencial">🏫 Presencial</option>
      </select>
    </div>
    <div class="form-group">
      <label>Consulta</label>
      <textarea id="f-consulta" placeholder="Describe la consulta..."></textarea>
    </div>
    <div class="form-group">
      <label>Estado</label>
      <select id="f-estado">
        <option value="pending">⏳ Pendiente</option>
        <option value="resolved">✅ Resuelta</option>
        <option value="escalated">🔴 Escalada</option>
      </select>
    </div>
    <div class="modal-footer">
      <button class="btn" onclick="closeModal()">Cancelar</button>
      <button class="btn btn-primary" onclick="saveConsulta()">Guardar</button>
    </div>
  </div>
</div>

<script>
// Clock
function updateClock() {
  const now = new Date();
  document.getElementById('clock').textContent = now.toLocaleTimeString('es-BO', { hour: '2-digit', minute: '2-digit' });
}
setInterval(updateClock, 1000);
updateClock();

// Nav
function showSection(id, el) {
  document.querySelectorAll('.section').forEach(s => s.classList.remove('active'));
  document.querySelectorAll('.nav-item').forEach(n => n.classList.remove('active'));
  document.getElementById('s-' + id).classList.add('active');
  el.classList.add('active');
  const titles = { dashboard: 'Dashboard', ia: 'Asistente IA', faq: 'Base de FAQ', templates: 'Plantillas WhatsApp', crm: 'Registro de Consultas' };
  document.getElementById('page-title').textContent = titles[id] || id;
}

// FAQ Data
const faqs = [
  { q: '¿Cuánto cuesta el módulo básico?', a: 'Bs. 815 en todas las sedes principales (Casa Central, Federico Zuazo, Virtual). En El Alto: Bs. 710 (precio diferenciado por responsabilidad social). Con convenio UMSA: Bs. 640. Matrícula única: Bs. 100.', cat: 'precios' },
  { q: '¿Cuáles son los precios por nivel?', a: 'Regular/Acelerado — Básico: Bs. 815 | Intermedio: Bs. 835 | Superior: Bs. 855 | Avanzado: Bs. 865. El Alto — Básico: Bs. 710 | Intermedio: Bs. 730 | Superior: Bs. 750 | Avanzado: Bs. 760. Matrícula única: Bs. 100.', cat: 'precios' },
  { q: '¿Cuánto cuestan los libros?', a: 'El material didáctico cuesta Bs. 450 y es válido para 3 módulos de aprendizaje. En modalidad Regular se paga aprox. cada 2 meses; en Acelerado cada 3 meses.', cat: 'precios' },
  { q: '¿Cuánto dura el programa Regular?', a: 'Cada módulo dura 34 días hábiles, con 1 hora y media de clase por día, de lunes a viernes. El programa completo consta de 18 módulos.', cat: 'horarios' },
  { q: '¿Cuánto dura el programa Acelerado?', a: 'Cada módulo dura 17 días hábiles, con 3 horas de clases intensivas por día, de lunes a viernes. Es la forma más rápida de avanzar.', cat: 'horarios' },
  { q: '¿Qué horarios hay en Casa Central?', a: 'Regular: 07:15, 14:45, 16:25, 18:05, 19:45. Acelerado: 08:55 – 12:05. Niños: 08:55 y 14:45. Adolescentes: 16:25. Sábados adultos: 08:00 – 14:30.', cat: 'horarios' },
  { q: '¿Qué horarios hay en Federico Zuazo?', a: 'Regular: 07:15, 08:55, 10:35, 14:45, 16:25, 18:05, 19:45. Acelerado: 08:55 y 18:05. Sábados: 08:00 – 14:30. Ideal para universitarios por cercanía a la UMSA.', cat: 'horarios' },
  { q: '¿Qué horarios hay en El Alto?', a: 'Regular: 07:15, 08:55, 14:45, 16:25, 18:05, 19:45. Acelerado: 08:55, 14:45, 18:05. Sábados adultos: 08:00 – 14:30. Niños sábados: 08:00 – 12:30.', cat: 'horarios' },
  { q: '¿Cuáles son los horarios virtuales?', a: 'Regular virtual: 07:15 y 19:45. Acelerado virtual: 18:45 – 21:55. Incluye clases en vivo con docentes certificados, Speaking Clubs y plataformas digitales.', cat: 'horarios' },
  { q: '¿Qué requisitos necesito para inscribirme?', a: 'Solo necesitas: 1) Fotocopia de tu Cédula de Identidad, 2) Un folder amarillo tamaño carta con fastener, y 3) Una cuenta de Gmail activa.', cat: 'requisitos' },
  { q: '¿Cómo me inscribo?', a: 'Puedes inscribirte presencialmente en cualquier sede o llenar el formulario en línea: https://forms.gle del CBA La Paz. Al finalizar envía captura, nombre completo y número de carnet.', cat: 'requisitos' },
  { q: '¿Cuándo son las inscripciones del ciclo actual?', a: 'Las inscripciones del ciclo actual fueron el 12 y 13 de marzo. El inicio de clases es el 16 de marzo. Las próximas inscripciones son el 7 y 8 de mayo, con inicio el 11 de mayo.', cat: 'requisitos' },
  { q: '¿Cuándo es la graduación?', a: 'La graduación es el 27 de marzo de 2026. Costo: Bs. 390 adultos / Bs. 260 niños. Turnos: Apellidos A–J: 15:00–17:00 | Apellidos L–Z: 19:00–21:00. Presentarse 45 min antes. Vestimenta: traje formal oscuro.', cat: 'graduacion' },
  { q: '¿Qué incluye el pago de graduación?', a: 'Incluye: birrete, banda y 3 invitaciones. El material se entrega los días 23 y 24 de marzo. Se recomienda pagar en esos días o antes. Costo: Bs. 390 adultos / Bs. 260 niños.', cat: 'graduacion' },
  { q: '¿Qué convenios tiene el CBA?', a: 'Convenios con precio diferenciado: UNIVALLE, UTB, EMI, SALESIANA, Cámara de Senadores, Col. Don Bosco, Col. Domingo Savio, Club The Strongest, BancoSol, ATB. En sucursal: La Salle, Los Pinos, Utasawa, American School, Vida y Verdad. Convenio UMSA: desde Bs. 640.', cat: 'convenios' },
  { q: '¿Cuáles son los precios con convenio UMSA?', a: 'Básico: Bs. 640 | Intermedio: Bs. 650 | Superior: Bs. 660 | Avanzado: Bs. 675. Requiere carnet universitario UMSA vigente.', cat: 'convenios' },
  { q: '¿Cómo funciona el examen de clasificación?', a: 'El examen de clasificación tiene un costo de Bs. 100. Al finalizar se comunica la nota para que el estudiante pueda inscribirse al nivel que le corresponde. Se realizó el 12 y 13 de marzo.', cat: 'requisitos' },
  { q: '¿Cómo puedo pagar en línea?', a: 'Para pagos en línea contactar a Julieta Zuñagua al número 77201457 (WhatsApp). También puede consultar al encargado de sistemas Arturo Saavedra al 72578133.', cat: 'requisitos' },
];

let currentFilter = 'all';

function renderFAQ(items) {
  const grid = document.getElementById('faq-grid');
  grid.innerHTML = items.map((f, i) => `
    <div class="faq-item" id="faq-${i}">
      <div class="faq-q" onclick="toggleFAQ(${i})">
        <span>${f.q}</span>
        <div style="display:flex;align-items:center;gap:8px;flex-shrink:0;">
          <span class="faq-category cat-${f.cat}">${catLabel(f.cat)}</span>
          <span class="faq-toggle">+</span>
        </div>
      </div>
      <div class="faq-a">
        ${f.a}
        <br>
        <button class="copy-answer-btn" onclick="copyAnswer(event, ${i})">📋 Copiar respuesta</button>
      </div>
    </div>
  `).join('');
}

function catLabel(c) {
  const m = { precios: 'Precios', horarios: 'Horarios', requisitos: 'Requisitos', graduacion: 'Graduación', convenios: 'Convenios' };
  return m[c] || c;
}

function toggleFAQ(i) {
  document.getElementById('faq-' + i).classList.toggle('open');
}

function copyAnswer(e, i) {
  e.stopPropagation();
  const btn = e.target;
  const visible = getVisibleFAQs();
  navigator.clipboard.writeText(visible[i].a).catch(() => {});
  btn.textContent = '✅ Copiado';
  btn.classList.add('copied');
  setTimeout(() => { btn.textContent = '📋 Copiar respuesta'; btn.classList.remove('copied'); }, 2000);
}

function getVisibleFAQs() {
  const q = document.getElementById('faq-search').value.toLowerCase();
  return faqs.filter(f => {
    const matchFilter = currentFilter === 'all' || f.cat === currentFilter;
    const matchSearch = !q || f.q.toLowerCase().includes(q) || f.a.toLowerCase().includes(q);
    return matchFilter && matchSearch;
  });
}

function filterFAQ() { renderFAQ(getVisibleFAQs()); }

function setFilter(cat, btn) {
  currentFilter = cat;
  document.querySelectorAll('.filter-btn').forEach(b => b.classList.remove('active'));
  btn.classList.add('active');
  filterFAQ();
}

renderFAQ(faqs);

// TEMPLATES
const templates = [
  {
    name: 'Saludo de bienvenida',
    tag: 'wa', tagLabel: 'WhatsApp',
    body: `👋 Buenas tardes, gracias por comunicarse con el CBA La Paz. ¿En qué puedo ayudarle hoy? 🤗`
  },
  {
    name: 'Información de precios',
    tag: 'wa', tagLabel: 'WhatsApp',
    body: `📚 Inversión por módulo — CBA La Paz:

💰 Precios generales:
• Básico: Bs. 815
• Intermedio: Bs. 835
• Superior: Bs. 855
• Avanzado: Bs. 865
💳 Matrícula única: Bs. 100
📖 Material (3 módulos): Bs. 450

🏙️ El Alto (precio social):
• Básico: Bs. 710 | Avanzado: Bs. 760

Si tiene convenio, puede haber un precio diferenciado.
¿Le gustaría más información sobre algún nivel o sede? 😊`
  },
  {
    name: 'Requisitos de inscripción',
    tag: 'wa', tagLabel: 'WhatsApp',
    body: `📋 Requisitos para inscribirse en el CBA La Paz:

🪪 Fotocopia de Cédula de Identidad
📁 Folder amarillo tamaño carta con fastener
📧 Cuenta de Gmail activa

📅 Inscripciones: 7 y 8 de mayo
📚 Inicio de clases: 11 de mayo

Si tiene más preguntas, no dude en consultar 🤗`
  },
  {
    name: 'Horarios disponibles',
    tag: 'wa', tagLabel: 'WhatsApp',
    body: `🕐 Horarios disponibles — CBA La Paz:

📍 Casa Central: 07:15 | 14:45 | 16:25 | 18:05 | 19:45
📍 Federico Zuazo: 07:15 | 08:55 | 10:35 | 14:45 | 16:25 | 18:05 | 19:45
📍 El Alto: 07:15 | 08:55 | 14:45 | 16:25 | 18:05 | 19:45
💻 Virtual: 07:15 | 19:45 (regular) | 18:45 (acelerado)

⚡ Programa Acelerado disponible en: 08:55 (CC, FZ, EA) y 18:45 (Virtual).

¿Qué sede o modalidad le queda más cómoda? 😊`
  },
  {
    name: 'Fuera de horario',
    tag: 'wa', tagLabel: 'WhatsApp',
    body: `Gracias por escribirnos 🤗

Nuestro horario de atención es:
🕣 Oficina: 8:30 – 12:30 y 14:30 – 18:00
🕙 Línea: 10:00 – 12:00 y 15:00 – 18:00

Déjanos tu consulta y te responderemos a la brevedad. ¡Que tengas un buen día! 😊`
  },
  {
    name: 'Información de graduación',
    tag: 'general', tagLabel: 'General',
    body: `🎓 Graduación CBA La Paz — 27 de marzo de 2026

💰 Costo: Bs. 390 (adultos) / Bs. 260 (niños)
✅ Incluye: birrete, banda y 3 invitaciones
👔 Vestimenta: traje formal oscuro

⏰ Turnos por apellido:
• A–J: 15:00 – 17:00
• L–Z: 19:00 – 21:00
⚠️ Presentarse 45 minutos antes del turno asignado.

📦 Entrega de materiales: 23 y 24 de marzo (se recomienda pagar esos días o antes).`
  },
  {
    name: 'Cierre profesional',
    tag: 'general', tagLabel: 'General',
    body: `✨ Ha sido un placer ayudarle. Si tiene más preguntas, no dude en consultarnos. ¡Éxito en sus estudios! 🤗`
  },
];

function renderTemplates() {
  document.getElementById('templates-grid').innerHTML = templates.map((t, i) => `
    <div class="template-card">
      <div class="template-header">
        <span class="template-name">${t.name}</span>
        <span class="template-tag tag-${t.tag}">${t.tagLabel}</span>
      </div>
      <div class="template-body">${t.body}</div>
      <div class="template-footer">
        <button class="btn" id="copy-tpl-${i}" onclick="copyTemplate(${i})">📋 Copiar</button>
      </div>
    </div>
  `).join('');
}

function copyTemplate(i) {
  const btn = document.getElementById('copy-tpl-' + i);
  navigator.clipboard.writeText(templates[i].body).catch(() => {});
  btn.textContent = '✅ Copiado';
  btn.classList.add('copied');
  setTimeout(() => { btn.textContent = '📋 Copiar'; btn.classList.remove('copied'); }, 2000);
}

renderTemplates();

// CRM
let consultas = [
  { nombre: 'María López', consulta: '¿Precio módulo básico?', canal: 'WhatsApp', estado: 'resolved', hora: '09:15' },
  { nombre: 'Carlos Mamani', consulta: 'Horarios tarde Federico Zuazo', canal: 'Facebook', estado: 'pending', hora: '10:32' },
  { nombre: 'Ana Quispe', consulta: 'Convenio UMSA precio', canal: 'Presencial', estado: 'resolved', hora: '11:05' },
  { nombre: 'José Flores', consulta: 'Fecha graduación y costo', canal: 'WhatsApp', estado: 'escalated', hora: '14:20' },
];

function renderCRM() {
  const statMap = { pending: '<span class="status-pill s-pending">⏳ Pendiente</span>', resolved: '<span class="status-pill s-resolved">✅ Resuelta</span>', escalated: '<span class="status-pill s-escalated">🔴 Escalada</span>' };
  const chanIcon = { WhatsApp: '📱', Facebook: '📘', Teléfono: '📞', Presencial: '🏫' };
  document.getElementById('crm-body').innerHTML = consultas.map((c, i) => `
    <tr>
      <td><strong>${c.nombre}</strong></td>
      <td style="max-width:220px;overflow:hidden;text-overflow:ellipsis;white-space:nowrap;">${c.consulta}</td>
      <td><span class="channel-icon">${chanIcon[c.canal] || '💬'} ${c.canal}</span></td>
      <td>${statMap[c.estado]}</td>
      <td style="color:var(--gray-400);">${c.hora}</td>
      <td>
        <select onchange="changeStatus(${i}, this.value)" style="border:1px solid var(--gray-200);border-radius:6px;padding:4px 8px;font-family:'DM Sans',sans-serif;font-size:12px;color:var(--gray-700);background:white;cursor:pointer;">
          <option value="pending" ${c.estado==='pending'?'selected':''}>⏳ Pendiente</option>
          <option value="resolved" ${c.estado==='resolved'?'selected':''}>✅ Resuelta</option>
          <option value="escalated" ${c.estado==='escalated'?'selected':''}>🔴 Escalada</option>
        </select>
      </td>
    </tr>
  `).join('');
}

function changeStatus(i, val) { consultas[i].estado = val; renderCRM(); }

function openModal() { document.getElementById('modal').classList.add('open'); }
function closeModal() {
  document.getElementById('modal').classList.remove('open');
  document.getElementById('f-nombre').value = '';
  document.getElementById('f-consulta').value = '';
}

function saveConsulta() {
  const n = document.getElementById('f-nombre').value.trim();
  const c = document.getElementById('f-consulta').value.trim();
  if (!n || !c) return;
  const now = new Date();
  consultas.unshift({
    nombre: n,
    consulta: c,
    canal: document.getElementById('f-canal').value,
    estado: document.getElementById('f-estado').value,
    hora: now.toLocaleTimeString('es-BO', { hour: '2-digit', minute: '2-digit' })
  });
  renderCRM();
  closeModal();
}

renderCRM();

// AI ASSISTANT
const CBA_CONTEXT = `Eres el asistente de atención al cliente del CBA La Paz (Centro Boliviano Americano La Paz), un centro de idiomas en Bolivia. Responde de forma amable, concisa y en español. Usa emojis moderadamente para hacer las respuestas más amigables.

INFORMACIÓN DEL CBA LA PAZ:

PRECIOS:
- Básico: Bs. 815 | Intermedio: Bs. 835 | Superior: Bs. 855 | Avanzado: Bs. 865
- El Alto (precio diferenciado): Básico Bs. 710 | Intermedio Bs. 730 | Superior Bs. 750 | Avanzado Bs. 760
- Matrícula: Bs. 100 (pago único) | Material/Libros: Bs. 450 (válido para 3 módulos)
- Convenio UMSA: Básico Bs. 640 | Intermedio Bs. 650 | Superior Bs. 660 | Avanzado Bs. 675
- Otros convenios (precio diferenciado): Básico Bs. 680 | Intermedio Bs. 690 | Superior Bs. 705 | Avanzado Bs. 715

PROGRAMAS:
- Regular: 34 días hábiles, 1.5 horas/día, lunes a viernes
- Acelerado: 17 días hábiles, 3 horas/día, lunes a viernes
- Programa completo: 18 módulos

FECHAS:
- Inscripciones ciclo actual: 12 y 13 de marzo
- Inicio de clases: 16 de marzo
- Entrega de materiales: 23 y 24 de marzo
- Graduación: 27 de marzo de 2026
- Próximas inscripciones: 7 y 8 de mayo
- Próximo inicio: 11 de mayo

GRADUACIÓN (27 marzo):
- Adultos: Bs. 390 | Niños: Bs. 260
- Incluye: birrete, banda, 3 invitaciones
- Turno A–J: 15:00–17:00 | Turno L–Z: 19:00–21:00
- Llegar 45 minutos antes
- Vestimenta: traje formal oscuro

REQUISITOS:
- Fotocopia de CI
- Folder amarillo tamaño carta con fastener
- Cuenta de Gmail activa

HORARIOS DE ATENCIÓN:
- Oficina: 8:30–12:30 y 14:30–18:00
- Línea: 10:00–12:00 y 15:00–18:00

SEDES Y HORARIOS:
Casa Central (Av. Arce): Regular 07:15, 14:45, 16:25, 18:05, 19:45 | Acelerado 08:55–12:05
Federico Zuazo (detrás UMSA): Regular 07:15, 08:55, 10:35, 14:45, 16:25, 18:05, 19:45 | Acelerado 08:55 y 18:05
El Alto (Av. 6 de Marzo): Regular 07:15, 08:55, 14:45, 16:25, 18:05, 19:45 | Acelerado 08:55, 14:45, 18:05
Virtual: Regular 07:15 y 19:45 | Acelerado 18:45–21:55

CONVENIOS:
UNIVALLE, UTB, EMI, SALESIANA, Cámara de Senadores, Col. Don Bosco, Col. Domingo Savio, Club The Strongest, BancoSol, ATB, Col. La Salle, Instituto Los Pinos, Col. Utasawa, American School, Col. Vida y Verdad, UMSA.

EXAMEN DE CLASIFICACIÓN: Bs. 100. Se realiza para determinar el nivel del estudiante.

CONTACTOS:
- Sistemas (Arturo Saavedra): 72578133
- Pagos en línea (Julieta Zuñagua): 77201457

FORMULARIO: https://docs.google.com/forms/d/e/1FAIpQLSdEHeWCBCr4XmhIV8D853UACpynwIif5fuUvX_vBGT0tlpQZQ/viewform
PLATAFORMA ESTUDIANTIL: https://tinyurl.com/39kdw67a`;

let chatHistory = [];

function getTime() {
  return new Date().toLocaleTimeString('es-BO', { hour: '2-digit', minute: '2-digit' });
}

function addMsg(role, text) {
  const area = document.getElementById('chat-area');
  const isUser = role === 'user';
  const div = document.createElement('div');
  div.className = `msg ${isUser ? 'user' : 'bot'}`;
  div.innerHTML = `
    <div class="msg-avatar ${isUser ? 'user' : 'bot'}">${isUser ? '👤' : '🎓'}</div>
    <div>
      <div class="msg-bubble">${text.replace(/\n/g, '<br>')}</div>
      <div class="msg-time">${getTime()}</div>
    </div>
  `;
  area.appendChild(div);
  area.scrollTop = area.scrollHeight;
}

function addTyping() {
  const area = document.getElementById('chat-area');
  const div = document.createElement('div');
  div.className = 'msg bot';
  div.id = 'typing-msg';
  div.innerHTML = `
    <div class="msg-avatar bot">🎓</div>
    <div>
      <div class="msg-bubble">
        <div class="typing-indicator">
          <div class="typing-dot"></div>
          <div class="typing-dot"></div>
          <div class="typing-dot"></div>
        </div>
      </div>
    </div>
  `;
  area.appendChild(div);
  area.scrollTop = area.scrollHeight;
}

async function sendMessage() {
  const input = document.getElementById('user-input');
  const text = input.value.trim();
  if (!text) return;

  input.value = '';
  input.style.height = '42px';
  document.getElementById('send-btn').disabled = true;

  addMsg('user', text);
  chatHistory.push({ role: 'user', content: text });
  addTyping();

  try {
    const res = await fetch('https://api.anthropic.com/v1/messages', {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({
        model: 'claude-sonnet-4-20250514',
        max_tokens: 1000,
        system: CBA_CONTEXT,
        messages: chatHistory
      })
    });

    const data = await res.json();
    const reply = data.content?.[0]?.text || 'Lo siento, no pude procesar tu consulta.';

    document.getElementById('typing-msg')?.remove();
    addMsg('bot', reply);
    chatHistory.push({ role: 'assistant', content: reply });
  } catch (e) {
    document.getElementById('typing-msg')?.remove();
    addMsg('bot', 'Ocurrió un error al conectar con el asistente. Verifica tu conexión e intenta nuevamente.');
  }

  document.getElementById('send-btn').disabled = false;
}

function quickSend(text) {
  document.getElementById('user-input').value = text;
  sendMessage();
}

function handleKey(e) {
  if (e.key === 'Enter' && !e.shiftKey) { e.preventDefault(); sendMessage(); }
}
</script>
</body>
</html>
