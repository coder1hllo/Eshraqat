<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover">
  <title>serene · space for teens</title>
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    :root {
      --bg-gradient: linear-gradient(145deg, #f9f3ee 0%, #e9f0f5 100%);
      --card-bg: rgba(250, 247, 252, 0.7);
      --text-primary: #2e3b4e;
      --text-secondary: #6a5e7c;
      --text-tertiary: #4e4b5c;
      --accent: #b8a3cc;
      --accent-light: #efe2f7;
      --accent-dark: #7c6b8f;
      --border: rgba(255, 255, 255, 0.8);
      --input-bg: rgba(255, 255, 250, 0.75);
      --input-border: #d9cfdf;
      --button-bg: #efe2f7;
      --button-border: #cfbedb;
      --button-hover: #e1cef0;
      --mood-selected: #e3d4f0;
      --mood-selected-border: #a58db8;
      --tool-bg: rgba(252, 250, 255, 0.7);
      --tool-hover: rgba(255, 251, 250, 0.8);
      --affirmation-bg: rgba(255, 250, 245, 0.75);
      --breathing-bg: rgba(234, 225, 245, 0.55);
      --greeting-bg: rgba(239, 232, 245, 0.7);
      --shadow: rgba(148, 126, 158, 0.15);
      --orb-1: rgba(203, 182, 219, 0.25);
      --orb-2: rgba(167, 196, 188, 0.3);
      --orb-3: rgba(251, 225, 198, 0.4);
      --tab-active-bg: rgba(255, 255, 255, 0.9);
      --tab-hover-bg: rgba(255, 255, 255, 0.6);
      --toggle-bg: #ccc;
      --footer-color: #8b7f94;
    }

    /* Dark mode variables */
    body.dark-mode {
      --bg-gradient: linear-gradient(145deg, #1a1a2e 0%, #16213e 100%);
      --card-bg: rgba(30, 30, 50, 0.8);
      --text-primary: #e0dce8;
      --text-secondary: #b8b0c8;
      --text-tertiary: #c8c0d8;
      --accent: #9b8ec4;
      --accent-light: rgba(155, 142, 196, 0.3);
      --accent-dark: #b8a8d8;
      --border: rgba(255, 255, 255, 0.1);
      --input-bg: rgba(40, 40, 60, 0.8);
      --input-border: #4a4a6a;
      --button-bg: rgba(155, 142, 196, 0.3);
      --button-border: #6a5a8a;
      --button-hover: rgba(155, 142, 196, 0.5);
      --mood-selected: rgba(155, 142, 196, 0.4);
      --mood-selected-border: #9b8ec4;
      --tool-bg: rgba(35, 35, 55, 0.8);
      --tool-hover: rgba(45, 45, 65, 0.9);
      --affirmation-bg: rgba(35, 35, 55, 0.8);
      --breathing-bg: rgba(40, 35, 60, 0.7);
      --greeting-bg: rgba(40, 35, 60, 0.7);
      --shadow: rgba(0, 0, 0, 0.3);
      --orb-1: rgba(100, 80, 140, 0.2);
      --orb-2: rgba(80, 100, 130, 0.2);
      --orb-3: rgba(120, 90, 110, 0.2);
      --tab-active-bg: rgba(50, 50, 70, 0.9);
      --tab-hover-bg: rgba(50, 50, 70, 0.5);
      --toggle-bg: #4a4a6a;
      --footer-color: #8b8ba8;
    }

    body {
      background: var(--bg-gradient);
      font-family: 'Segoe UI', 'Inter', system-ui, -apple-system, BlinkMacSystemFont, sans-serif;
      min-height: 100vh;
      display: flex;
      align-items: center;
      justify-content: center;
      padding: 1.5rem;
      margin: 0;
      color: var(--text-primary);
      position: relative;
      transition: all 0.5s ease;
    }

    body::before {
      content: "";
      position: fixed;
      inset: 0;
      background: radial-gradient(circle at 20% 30%, var(--orb-1) 0%, transparent 45%),
                  radial-gradient(circle at 80% 70%, var(--orb-2) 0%, transparent 50%),
                  radial-gradient(circle at 40% 80%, var(--orb-3) 0%, transparent 55%);
      pointer-events: none;
      z-index: 0;
      transition: all 0.5s ease;
    }

    /* Notification toast */
    .notification-toast {
      position: fixed;
      top: 20px;
      right: 20px;
      background: var(--card-bg);
      backdrop-filter: blur(20px);
      border: 1px solid var(--border);
      border-radius: 2rem;
      padding: 1rem 1.5rem;
      box-shadow: 0 10px 30px var(--shadow);
      z-index: 1000;
      font-size: 0.95rem;
      color: var(--text-primary);
      display: flex;
      align-items: center;
      gap: 0.5rem;
      animation: slideIn 0.4s ease, slideOut 0.4s ease 3.5s forwards;
      max-width: 350px;
    }

    @keyframes slideIn {
      from { transform: translateX(120%); opacity: 0; }
      to { transform: translateX(0); opacity: 1; }
    }

    @keyframes slideOut {
      from { transform: translateX(0); opacity: 1; }
      to { transform: translateX(120%); opacity: 0; }
    }

    .app-container {
      position: relative;
      z-index: 2;
      max-width: 800px;
      width: 100%;
      display: flex;
      flex-direction: column;
      gap: 1rem;
    }

    /* Tab Navigation */
    .tab-navigation {
      display: flex;
      flex-wrap: wrap;
      gap: 0.5rem;
      justify-content: center;
      background: var(--card-bg);
      backdrop-filter: blur(22px);
      -webkit-backdrop-filter: blur(22px);
      border-radius: 3rem;
      padding: 0.8rem;
      box-shadow: 0 15px 30px var(--shadow);
      border: 1px solid var(--border);
      transition: all 0.5s ease;
    }

    .tab-btn {
      background: transparent;
      border: none;
      padding: 0.7rem 1.2rem;
      border-radius: 2.5rem;
      cursor: pointer;
      font-size: 0.9rem;
      font-weight: 500;
      color: var(--text-secondary);
      transition: all 0.3s ease;
      white-space: nowrap;
      font-family: inherit;
      display: flex;
      align-items: center;
      gap: 0.4rem;
    }

    .tab-btn:hover {
      background: var(--tab-hover-bg);
      color: var(--text-primary);
    }

    .tab-btn.active {
      background: var(--tab-active-bg);
      color: var(--accent-dark);
      box-shadow: 0 4px 12px var(--shadow);
      font-weight: 600;
    }

    .tab-emoji {
      font-size: 1.2rem;
    }

    /* Tab Content */
    .tab-content {
      display: none;
      animation: fadeIn 0.4s ease;
    }

    .tab-content.active {
      display: block;
    }

    @keyframes fadeIn {
      from { opacity: 0; transform: translateY(10px); }
      to { opacity: 1; transform: translateY(0); }
    }

    /* ---------- ONBOARDING CARD ---------- */
    .onboarding-card {
      background: var(--card-bg);
      backdrop-filter: blur(22px);
      -webkit-backdrop-filter: blur(22px);
      border-radius: 3.5rem;
      padding: 2.8rem 2.5rem;
      box-shadow: 0 30px 55px var(--shadow),
                  0 10px 25px rgba(110, 130, 140, 0.1),
                  inset 0 1px 1px var(--border);
      border: 1px solid var(--border);
      display: flex;
      flex-direction: column;
      gap: 2rem;
      transition: all 0.5s ease;
    }

    .header {
      display: flex;
      align-items: center;
      gap: 0.7rem;
      justify-content: center;
      flex-wrap: wrap;
    }

    .moon-leaf {
      font-size: 2.8rem;
      filter: drop-shadow(0 6px 8px var(--shadow));
      background: rgba(255, 255, 255, 0.2);
      border-radius: 50%;
      padding: 0.3rem;
      line-height: 1;
    }

    h1 {
      font-weight: 500;
      font-size: 2.3rem;
      letter-spacing: -0.5px;
      background: linear-gradient(135deg, #5f6b7a, #4a5668);
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      background-clip: text;
    }

    body.dark-mode h1 {
      background: linear-gradient(135deg, #c8c0d8, #a898c8);
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      background-clip: text;
    }

    h2 {
      font-weight: 500;
      font-size: 1.8rem;
      color: var(--text-tertiary);
      text-align: center;
    }

    .subtitle {
      text-align: center;
      font-size: 1.2rem;
      font-weight: 400;
      color: var(--text-secondary);
      margin-top: -0.8rem;
      letter-spacing: 0.3px;
    }

    .form-group {
      display: flex;
      flex-direction: column;
      gap: 0.5rem;
    }

    label {
      font-weight: 500;
      color: var(--text-tertiary);
      font-size: 1rem;
      margin-left: 0.5rem;
      display: flex;
      align-items: center;
      gap: 0.4rem;
    }

    input, select, textarea {
      background: var(--input-bg);
      border: 1px solid var(--input-border);
      border-radius: 2rem;
      padding: 0.9rem 1.3rem;
      font-size: 1rem;
      outline: none;
      font-family: inherit;
      color: var(--text-primary);
      backdrop-filter: blur(10px);
      transition: 0.2s;
      width: 100%;
    }

    input:focus, select:focus, textarea:focus {
      border-color: var(--accent);
      box-shadow: 0 0 0 3px rgba(195, 167, 218, 0.3);
    }

    textarea {
      border-radius: 1.8rem;
      resize: vertical;
      min-height: 70px;
    }

    .row {
      display: flex;
      gap: 1rem;
      flex-wrap: wrap;
    }

    .row .form-group {
      flex: 1 1 120px;
    }

    .mood-selector {
      display: flex;
      flex-wrap: wrap;
      gap: 0.7rem;
      justify-content: flex-start;
    }

    .mood-option {
      background: var(--input-bg);
      border: 1.5px solid var(--input-border);
      border-radius: 2.5rem;
      padding: 0.5rem 1.2rem;
      font-size: 0.95rem;
      cursor: pointer;
      transition: all 0.2s;
      backdrop-filter: blur(8px);
      color: var(--text-tertiary);
      font-weight: 500;
      display: flex;
      align-items: center;
      gap: 0.3rem;
      user-select: none;
    }

    .mood-option:hover {
      background: var(--accent-light);
      border-color: var(--accent-dark);
    }

    .mood-option.selected {
      background: var(--mood-selected);
      border-color: var(--mood-selected-border);
      box-shadow: 0 4px 12px rgba(159, 130, 185, 0.3);
      color: var(--text-primary);
    }

    .submit-btn {
      background: var(--button-bg);
      border: 1px solid var(--button-border);
      border-radius: 3rem;
      padding: 1rem 2rem;
      font-weight: 550;
      font-size: 1.2rem;
      color: var(--text-tertiary);
      cursor: pointer;
      transition: 0.25s;
      backdrop-filter: blur(12px);
      letter-spacing: 0.5px;
      margin-top: 0.5rem;
      width: fit-content;
      align-self: center;
    }

    .submit-btn:hover {
      background: var(--button-hover);
      box-shadow: 0 10px 22px rgba(156, 132, 179, 0.25);
    }

    .error-message {
      color: #e08090;
      font-size: 0.85rem;
      margin-left: 0.8rem;
      min-height: 1.2rem;
    }

    /* ---------- MAIN CALMING PAGE ---------- */
    .main-card {
      background: var(--card-bg);
      backdrop-filter: blur(22px);
      -webkit-backdrop-filter: blur(22px);
      border-radius: 3.5rem;
      padding: 2.8rem 2.5rem;
      box-shadow: 0 30px 55px var(--shadow),
                  0 10px 25px rgba(110, 130, 140, 0.1),
                  inset 0 1px 1px var(--border);
      border: 1px solid var(--border);
      display: flex;
      flex-direction: column;
      gap: 2.2rem;
      transition: all 0.5s ease;
    }

    .greeting {
      text-align: center;
      font-size: 1.3rem;
      font-weight: 400;
      color: var(--text-secondary);
      margin-top: -0.6rem;
      letter-spacing: 0.3px;
      background: var(--greeting-bg);
      padding: 0.4rem 1.8rem;
      border-radius: 2rem;
      display: inline-block;
      margin-left: auto;
      margin-right: auto;
      transition: all 0.5s ease;
    }

    .affirmation-box {
      background: var(--affirmation-bg);
      backdrop-filter: blur(12px);
      -webkit-backdrop-filter: blur(12px);
      border-radius: 2.5rem;
      padding: 1.8rem 1.5rem;
      border: 1px solid rgba(255, 245, 235, 0.2);
      box-shadow: 0 12px 28px var(--shadow);
      text-align: center;
      transition: all 0.5s ease;
    }

    .quote-text {
      font-size: 1.6rem;
      font-weight: 450;
      line-height: 1.5;
      color: var(--text-tertiary);
      font-style: italic;
      word-break: break-word;
      transition: opacity 0.3s ease, color 0.5s ease;
    }

    .refresh-btn {
      background: transparent;
      border: 1.5px solid var(--input-border);
      color: var(--text-secondary);
      padding: 0.5rem 1.5rem;
      border-radius: 3rem;
      margin-top: 1rem;
      font-size: 0.95rem;
      font-weight: 500;
      cursor: pointer;
      background: rgba(255, 255, 255, 0.1);
      backdrop-filter: blur(8px);
      transition: all 0.25s;
      display: inline-flex;
      align-items: center;
      gap: 0.3rem;
      letter-spacing: 0.3px;
    }

    .refresh-btn:hover {
      background: var(--accent-light);
      border-color: var(--accent-dark);
      color: var(--text-primary);
      box-shadow: 0 5px 15px rgba(169, 143, 192, 0.25);
    }

    .tools-grid {
      display: flex;
      flex-wrap: wrap;
      gap: 1.2rem;
      justify-content: center;
    }

    .tool-card {
      flex: 1 1 130px;
      min-width: 110px;
      background: var(--tool-bg);
      backdrop-filter: blur(14px);
      -webkit-backdrop-filter: blur(14px);
      border-radius: 2.2rem;
      padding: 1.5rem 0.8rem;
      display: flex;
      flex-direction: column;
      align-items: center;
      gap: 0.7rem;
      border: 1px solid var(--border);
      box-shadow: 0 10px 20px rgba(128, 118, 148, 0.08);
      transition: transform 0.2s ease, background 0.3s;
      cursor: pointer;
      text-align: center;
    }

    .tool-card:hover {
      transform: translateY(-4px);
      background: var(--tool-hover);
      box-shadow: 0 20px 28px rgba(137, 120, 160, 0.15);
    }

    .tool-card.active-tool {
      background: var(--mood-selected);
      border-color: var(--mood-selected-border);
      box-shadow: 0 8px 20px rgba(159, 130, 185, 0.25);
    }

    .tool-emoji {
      font-size: 2.4rem;
      filter: drop-shadow(0 4px 5px rgba(137, 122, 162, 0.25));
    }

    .tool-label {
      font-weight: 500;
      font-size: 0.95rem;
      color: var(--text-tertiary);
      background: rgba(255, 255, 250, 0.1);
      padding: 0.3rem 0.8rem;
      border-radius: 1.5rem;
    }

    .breathing-section {
      background: var(--breathing-bg);
      backdrop-filter: blur(16px);
      -webkit-backdrop-filter: blur(16px);
      border-radius: 2.8rem;
      padding: 1.8rem;
      margin-top: 0.3rem;
      display: flex;
      flex-direction: column;
      align-items: center;
      gap: 1.2rem;
      border: 1px solid var(--border);
      transition: all 0.5s ease;
    }

    .circle-breath {
      width: 95px;
      height: 95px;
      border-radius: 50%;
      background: radial-gradient(circle at 30% 30%, #f7e9fb, #dac7e8);
      box-shadow: 0 0 30px rgba(189, 157, 215, 0.5);
      transition: transform 0.1s linear, background 0.2s;
      margin: 0.5rem 0;
    }

    .breath-instruction {
      font-size: 1.3rem;
      font-weight: 480;
      color: #4b405a;
      background: rgba(255, 250, 250, 0.3);
      padding: 0.4rem 1.8rem;
      border-radius: 3rem;
    }

    body.dark-mode .breath-instruction {
      color: #d8d0e8;
    }

    .stop-breath-btn {
      background: none;
      border: 1px solid #baafc9;
      color: #4e465c;
      padding: 0.5rem 1.5rem;
      border-radius: 2rem;
      font-weight: 500;
      cursor: pointer;
      transition: 0.2s;
      background: rgba(255, 255, 255, 0.2);
    }

    body.dark-mode .stop-breath-btn {
      color: #d8d0e8;
      border-color: #8a7aaa;
    }

    .stop-breath-btn:hover {
      background: var(--accent-light);
    }

    .note-area {
      display: flex;
      flex-direction: column;
      gap: 0.6rem;
      margin-top: 0.2rem;
    }

    .gratitude-input {
      background: var(--input-bg);
      border: 1px solid var(--input-border);
      border-radius: 2rem;
      padding: 0.9rem 1.3rem;
      font-size: 0.95rem;
      outline: none;
      resize: vertical;
      font-family: inherit;
      color: var(--text-primary);
      backdrop-filter: blur(10px);
      transition: 0.2s;
    }

    .gratitude-input:focus {
      border-color: var(--accent);
      box-shadow: 0 0 0 3px rgba(195, 167, 218, 0.3);
    }

    .tiny-btn {
      background: var(--button-bg);
      border: 1px solid var(--button-border);
      border-radius: 2rem;
      padding: 0.5rem;
      font-weight: 500;
      color: var(--text-tertiary);
      cursor: pointer;
      transition: 0.2s;
      align-self: center;
      width: fit-content;
      padding-left: 1.5rem;
      padding-right: 1.5rem;
    }

    .tiny-btn:hover {
      background: var(--button-hover);
    }

    /* Empty tab placeholder */
    .empty-tab {
      background: var(--card-bg);
      backdrop-filter: blur(22px);
      -webkit-backdrop-filter: blur(22px);
      border-radius: 3.5rem;
      padding: 3rem 2.5rem;
      box-shadow: 0 30px 55px var(--shadow);
      border: 1px solid var(--border);
      text-align: center;
      transition: all 0.5s ease;
    }

    .empty-tab-content {
      display: flex;
      flex-direction: column;
      align-items: center;
      gap: 1.5rem;
    }

    .empty-tab-emoji {
      font-size: 4rem;
      opacity: 0.6;
    }

    .empty-tab-text {
      font-size: 1.2rem;
      color: var(--text-secondary);
      font-style: italic;
    }

    /* Settings tab */
    .settings-card {
      background: var(--card-bg);
      backdrop-filter: blur(22px);
      -webkit-backdrop-filter: blur(22px);
      border-radius: 3.5rem;
      padding: 2.5rem;
      box-shadow: 0 30px 55px var(--shadow);
      border: 1px solid var(--border);
      display: flex;
      flex-direction: column;
      gap: 1.8rem;
      transition: all 0.5s ease;
    }

    .setting-item {
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding: 1rem 0;
      border-bottom: 1px solid var(--border);
    }

    .setting-label {
      font-weight: 500;
      color: var(--text-tertiary);
    }

    .setting-description {
      font-size: 0.85rem;
      color: var(--text-secondary);
      margin-top: 0.2rem;
    }

    .toggle-switch {
      position: relative;
      width: 50px;
      height: 26px;
      flex-shrink: 0;
    }

    .toggle-switch input {
      opacity: 0;
      width: 0;
      height: 0;
    }

    .toggle-slider {
      position: absolute;
      cursor: pointer;
      top: 0;
      left: 0;
      right: 0;
      bottom: 0;
      background-color: var(--toggle-bg);
      transition: 0.4s;
      border-radius: 34px;
    }

    .toggle-slider:before {
      position: absolute;
      content: "";
      height: 20px;
      width: 20px;
      left: 3px;
      bottom: 3px;
      background-color: white;
      transition: 0.4s;
      border-radius: 50%;
    }

    input:checked + .toggle-slider {
      background-color: var(--accent);
    }

    input:checked + .toggle-slider:before {
      transform: translateX(24px);
    }

    .settings-btn {
      background: var(--button-bg);
      border: 1px solid var(--button-border);
      border-radius: 2rem;
      padding: 0.8rem 1.5rem;
      font-weight: 500;
      color: var(--text-tertiary);
      cursor: pointer;
      transition: 0.2s;
      font-family: inherit;
    }

    .settings-btn:hover {
      background: var(--button-hover);
    }

    .settings-btn.danger {
      background: rgba(220, 100, 100, 0.2);
      border-color: rgba(220, 100, 100, 0.4);
      color: #d08080;
    }

    .settings-btn.danger:hover {
      background: rgba(220, 100, 100, 0.35);
    }

    footer {
      text-align: center;
      font-size: 0.8rem;
      color: var(--footer-color);
      margin-top: 0.5rem;
    }

    .hidden {
      display: none !important;
    }

    #soundStatus {
      text-align: center;
      font-size: 0.85rem;
      color: var(--text-secondary);
      margin-top: 0.3rem;
      transition: all 0.3s ease;
      min-height: 1.5rem;
    }

    .sound-active-indicator {
      display: inline-block;
      width: 8px;
      height: 8px;
      background: var(--accent-dark);
      border-radius: 50%;
      margin-right: 0.4rem;
      animation: pulse 1.5s infinite;
    }

    @keyframes pulse {
      0%, 100% { opacity: 0.4; transform: scale(0.8); }
      50% { opacity: 1; transform: scale(1.2); }
    }

    @media (max-width: 600px) {
      .tab-btn {
        padding: 0.5rem 0.8rem;
        font-size: 0.8rem;
      }
    }

    @media (max-width: 500px) {
      .onboarding-card, .main-card, .empty-tab, .settings-card {
        padding: 2rem 1.5rem;
      }
      .quote-text {
        font-size: 1.3rem;
      }
    }
  </style>
</head>
<body>

  <div class="app-container" id="appContainer">
    
    <!-- ========== TAB NAVIGATION ========== -->
    <div class="tab-navigation" id="tabNav">
      <button class="tab-btn active" data-tab="home">🏠 Home</button>
      <button class="tab-btn" data-tab="tab1">📸 Gallery</button>
      <button class="tab-btn" data-tab="tab2">🎵 Music</button>
      <button class="tab-btn" data-tab="tab3">📖 Journal</button>
      <button class="tab-btn" data-tab="tab4">🎮 Fun</button>
      <button class="tab-btn" data-tab="tab5">💭 Thoughts</button>
      <button class="tab-btn" data-tab="settings">⚙️ Settings</button>
    </div>

    <!-- ========== ONBOARDING FORM ========== -->
    <div class="tab-content active" id="onboardingTab">
      <div class="onboarding-card" id="onboardingForm">
        <div class="header">
          <span class="moon-leaf">🌿🌙</span>
          <h1>welcome</h1>
        </div>
        <div class="subtitle">let's create your calm space ✦ a few things first</div>

        <div class="form-group">
          <label>🧸 your name / nickname</label>
          <input type="text" id="nameInput" placeholder="what should we call you?" autocomplete="off">
          <div class="error-message" id="nameError"></div>
        </div>

        <div class="row">
          <div class="form-group">
            <label>🌸 age</label>
            <input type="number" id="ageInput" placeholder="13-19" min="10" max="20">
            <div class="error-message" id="ageError"></div>
          </div>
          <div class="form-group">
            <label>🌈 gender</label>
            <select id="genderSelect">
              <option value="" disabled selected>select</option>
              <option value="female">female</option>
              <option value="male">male</option>
              <option value="non-binary">non-binary</option>
              <option value="prefer not to say">prefer not to say</option>
              <option value="other">other</option>
            </select>
            <div class="error-message" id="genderError"></div>
          </div>
        </div>

        <div class="form-group">
          <label>✨ your hobbies / interests</label>
          <textarea id="hobbiesInput" placeholder="gaming, music, art, reading, sports... anything you enjoy"></textarea>
        </div>

        <div class="form-group">
          <label>🌤️ how are you feeling right now?</label>
          <div class="mood-selector" id="moodSelector">
            <span class="mood-option" data-mood="calm">😌 calm</span>
            <span class="mood-option" data-mood="anxious">😟 anxious</span>
            <span class="mood-option" data-mood="tired">😴 tired</span>
            <span class="mood-option" data-mood="okay">🙂 okay</span>
            <span class="mood-option" data-mood="sad">🥺 sad</span>
            <span class="mood-option" data-mood="hopeful">🌟 hopeful</span>
          </div>
          <div class="error-message" id="moodError"></div>
        </div>

        <button class="submit-btn" id="enterBtn">enter your serene space ↺</button>
      </div>
    </div>

    <!-- ========== HOME TAB ========== -->
    <div class="tab-content" id="homeTab">
      <div class="main-card">
        <div class="header">
          <span class="moon-leaf">🌿🌙</span>
          <h1>soft reset</h1>
        </div>
        <div class="greeting" id="personalGreeting">welcome, friend</div>

        <div class="affirmation-box" id="affirmationContainer">
          <div class="quote-text" id="affirmationDisplay">you are exactly where you need to be.</div>
          <button class="refresh-btn" id="newAffirmationBtn">
            <span>↺</span> new thought
          </button>
        </div>

        <div class="tools-grid">
          <div class="tool-card" id="breathingTool">
            <span class="tool-emoji">🧘‍♀️</span>
            <span class="tool-label">breathe</span>
          </div>
          <div class="tool-card" id="gratitudeTool">
            <span class="tool-emoji">📝</span>
            <span class="tool-label">gratitude</span>
          </div>
          <div class="tool-card" id="calmSoundsTool">
            <span class="tool-emoji">🎵</span>
            <span class="tool-label">soft sounds</span>
          </div>
          <div class="tool-card" id="colorMoodTool">
            <span class="tool-emoji">🎨</span>
            <span class="tool-label">mood palette</span>
          </div>
        </div>

        <div id="breathingBox" class="breathing-section hidden">
          <div class="circle-breath" id="breathCircle"></div>
          <div class="breath-instruction" id="breathText">inhale</div>
          <button class="stop-breath-btn" id="stopBreathBtn">✧ finish breathing</button>
        </div>

        <div id="gratitudeNoteBox" class="note-area hidden">
          <textarea class="gratitude-input" id="gratitudeInput" placeholder="write something kind to yourself... or one good thing today." rows="2"></textarea>
          <button class="tiny-btn" id="saveGratitudeBtn">✨ save gentle note</button>
          <p style="font-size:0.8rem; color:var(--text-secondary); text-align:center; margin-top:0.2rem;" id="gratitudeFeedback"></p>
        </div>

        <div id="soundStatus"></div>

        <footer>
          <span>you're safe here ✦ take your time</span>
        </footer>
      </div>
    </div>

    <!-- ========== TAB 1-5: Empty Tabs ========== -->
    <div class="tab-content" id="tab1Content">
      <div class="empty-tab">
        <div class="empty-tab-content">
          <span class="empty-tab-emoji">📸</span>
          <h2>Gallery</h2>
          <p class="empty-tab-text">Add your favorite pictures and videos here</p>
          <p style="color: var(--text-secondary); font-size: 0.9rem;">✨ Coming soon - customize this space!</p>
        </div>
      </div>
    </div>

    <div class="tab-content" id="tab2Content">
      <div class="empty-tab">
        <div class="empty-tab-content">
          <span class="empty-tab-emoji">🎵</span>
          <h2>Music</h2>
          <p class="empty-tab-text">Your calming playlist and favorite tunes</p>
          <p style="color: var(--text-secondary); font-size: 0.9rem;">🎶 Ready for your music collection!</p>
        </div>
      </div>
    </div>

    <div class="tab-content" id="tab3Content">
      <div class="empty-tab">
        <div class="empty-tab-content">
          <span class="empty-tab-emoji">📖</span>
          <h2>Journal</h2>
          <p class="empty-tab-text">Write down your thoughts and feelings</p>
          <p style="color: var(--text-secondary); font-size: 0.9rem;">📝 A safe space for your words</p>
        </div>
      </div>
    </div>

    <div class="tab-content" id="tab4Content">
      <div class="empty-tab">
        <div class="empty-tab-content">
          <span class="empty-tab-emoji">🎮</span>
          <h2>Fun Zone</h2>
          <p class="empty-tab-text">Games, activities, and relaxing distractions</p>
          <p style="color: var(--text-secondary); font-size: 0.9rem;">🎲 Fun stuff loading soon!</p>
        </div>
      </div>
    </div>

    <div class="tab-content" id="tab5Content">
      <div class="empty-tab">
        <div class="empty-tab-content">
          <span class="empty-tab-emoji">💭</span>
          <h2>Thoughts</h2>
          <p class="empty-tab-text">Positive quotes, memes, and good vibes</p>
          <p style="color: var(--text-secondary); font-size: 0.9rem;">🌈 Fill with things that make you smile</p>
        </div>
      </div>
    </div>

    <!-- ========== SETTINGS TAB ========== -->
    <div class="tab-content" id="settingsContent">
      <div class="settings-card">
        <div class="header">
          <span class="moon-leaf">⚙️</span>
          <h1>settings</h1>
        </div>
        
        <div class="setting-item">
          <div>
            <div class="setting-label">🌙 Dark Mode</div>
            <div class="setting-description">Easier on the eyes at night</div>
          </div>
          <label class="toggle-switch">
            <input type="checkbox" id="darkModeToggle">
            <span class="toggle-slider"></span>
          </label>
        </div>

        <div class="setting-item">
          <div>
            <div class="setting-label">🔔 Gentle Reminders</div>
            <div class="setting-description">Occasional calming notifications</div>
          </div>
          <label class="toggle-switch">
            <input type="checkbox" id="notificationsToggle" checked>
            <span class="toggle-slider"></span>
          </label>
        </div>

        <div class="setting-item">
          <div>
            <div class="setting-label">🎵 Auto-play Sounds</div>
            <div class="setting-description">Play calming sounds when opening Home</div>
          </div>
          <label class="toggle-switch">
            <input type="checkbox" id="autoSoundToggle">
            <span class="toggle-slider"></span>
          </label>
        </div>

        <div class="setting-item">
          <div>
            <div class="setting-label">📊 Mood Tracking</div>
            <div class="setting-description">Save your mood history over time</div>
          </div>
          <label class="toggle-switch">
            <input type="checkbox" id="moodTrackingToggle" checked>
            <span class="toggle-slider"></span>
          </label>
        </div>

        <div class="setting-item">
          <div>
            <div class="setting-label">📋 View Mood History</div>
            <div class="setting-description">See your past moods and patterns</div>
          </div>
          <button class="settings-btn" id="viewMoodHistoryBtn">View History</button>
        </div>

        <div class="setting-item">
          <div>
            <div class="setting-label">🔄 Reset Profile</div>
            <div class="setting-description">Clear all data and start fresh</div>
          </div>
          <button class="settings-btn danger" id="resetProfileBtn">Reset All Data</button>
        </div>

        <div style="text-align: center; color: var(--text-secondary); font-size: 0.85rem; margin-top: 1rem;">
          <p>serene v1.0 · made with care 🌿</p>
          <p style="margin-top: 0.3rem;">your privacy matters · all data stays local</p>
        </div>
      </div>
    </div>

  </div>

  <!-- Notification toast container -->
  <div id="notificationContainer"></div>

  <script>
    (function() {
      // ========== GLOBAL STATE ==========
      let userProfile = null;
      let onboardingComplete = false;
      let soundPlaying = false;
      let audioCtx = null;
      let soundNodes = [];
      let notificationInterval = null;
      let moodHistory = [];

      // ========== LOAD SAVED DATA ==========
      function loadAllData() {
        // Load profile
        const savedProfile = localStorage.getItem('sereneUserProfile');
        if (savedProfile) {
          try {
            userProfile = JSON.parse(savedProfile);
            onboardingComplete = true;
          } catch (e) {
            userProfile = null;
            onboardingComplete = false;
          }
        }

        // Load settings
        const savedSettings = localStorage.getItem('sereneSettings');
        if (savedSettings) {
          try {
            return JSON.parse(savedSettings);
          } catch (e) {
            return {};
          }
        }
        return {};
      }

      function saveSettings(settings) {
        localStorage.setItem('sereneSettings', JSON.stringify(settings));
      }

      function loadMoodHistory() {
        const saved = localStorage.getItem('sereneMoodHistory');
        if (saved) {
          try {
            moodHistory = JSON.parse(saved);
          } catch (e) {
            moodHistory = [];
          }
        }
      }

      function saveMoodHistory() {
        localStorage.setItem('sereneMoodHistory', JSON.stringify(moodHistory));
      }

      // Initialize data
      const settings = loadAllData();
      loadMoodHistory();

      // ========== DOM ELEMENTS ==========
      const onboardingTab = document.getElementById('onboardingTab');
      const homeTab = document.getElementById('homeTab');
      const tabBtns = document.querySelectorAll('.tab-btn');
      const tabContents = {
        'home': homeTab,
        'tab1': document.getElementById('tab1Content'),
        'tab2': document.getElementById('tab2Content'),
        'tab3': document.getElementById('tab3Content'),
        'tab4': document.getElementById('tab4Content'),
        'tab5': document.getElementById('tab5Content'),
        'settings': document.getElementById('settingsContent')
      };

      // Settings elements
      const darkModeToggle = document.getElementById('darkModeToggle');
      const notificationsToggle = document.getElementById('notificationsToggle');
      const autoSoundToggle = document.getElementById('autoSoundToggle');
      const moodTrackingToggle = document.getElementById('moodTrackingToggle');
      const viewMoodHistoryBtn = document.getElementById('viewMoodHistoryBtn');
      const resetProfileBtn = document.getElementById('resetProfileBtn');

      // Apply loaded settings
      if (settings.darkMode) {
        darkModeToggle.checked = true;
        document.body.classList.add('dark-mode');
      }
      if (settings.notifications !== undefined) {
        notificationsToggle.checked = settings.notifications;
      }
      if (settings.autoSound) {
        autoSoundToggle.checked = true;
      }
      if (settings.moodTracking !== undefined) {
        moodTrackingToggle.checked = settings.moodTracking;
      }

      // ========== NOTIFICATION SYSTEM ==========
      function showNotification(message, emoji = '🔔', duration = 4000) {
        const container = document.getElementById('notificationContainer');
        const toast = document.createElement('div');
        toast.className = 'notification-toast';
        toast.innerHTML = `<span>${emoji}</span> ${message}`;
        container.appendChild(toast);
        
        setTimeout(() => {
          if (toast.parentNode) {
            toast.remove();
          }
        }, duration + 400);
      }

      function startNotifications() {
        stopNotifications();
        if (!settings.notifications && !notificationsToggle.checked) return;
        
        const reminders = [
          { msg: 'Take a deep breath 🌿', emoji: '🧘' },
          { msg: 'You\'re doing great today!', emoji: '✨' },
          { msg: 'Remember to drink water 💧', emoji: '💙' },
          { msg: 'Stretch your body gently', emoji: '🤸' },
          { msg: 'You are enough, just as you are', emoji: '💫' },
          { msg: 'Take a moment to look outside', emoji: '🌤️' },
          { msg: 'Your feelings are valid', emoji: '🤍' },
          { msg: 'Small progress is still progress', emoji: '🌱' }
        ];

        notificationInterval = setInterval(() => {
          if (notificationsToggle.checked) {
            const random = reminders[Math.floor(Math.random() * reminders.length)];
            showNotification(random.msg, random.emoji);
          }
        }, 300000); // Every 5 minutes
      }

      function stopNotifications() {
        if (notificationInterval) {
          clearInterval(notificationInterval);
          notificationInterval = null;
        }
      }

      // Start notifications if enabled
      if (notificationsToggle.checked) {
        startNotifications();
      }

      // ========== DARK MODE ==========
      darkModeToggle.addEventListener('change', function() {
        if (this.checked) {
          document.body.classList.add('dark-mode');
          showNotification('Dark mode activated 🌙', '🌙', 2000);
        } else {
          document.body.classList.remove('dark-mode');
          showNotification('Light mode activated ☀️', '☀️', 2000);
        }
        saveCurrentSettings();
      });

      // ========== NOTIFICATIONS TOGGLE ==========
      notificationsToggle.addEventListener('change', function() {
        if (this.checked) {
          startNotifications();
          showNotification('Gentle reminders enabled 🔔', '🔔', 2000);
        } else {
          stopNotifications();
          showNotification('Reminders paused', '🔕', 2000);
        }
        saveCurrentSettings();
      });

      // ========== AUTO SOUND ==========
      autoSoundToggle.addEventListener('change', function() {
        saveCurrentSettings();
        if (this.checked) {
          showNotification('Sounds will auto-play on Home tab 🎵', '🎵', 2000);
        }
      });

      // ========== MOOD TRACKING ==========
      moodTrackingToggle.addEventListener('change', function() {
        saveCurrentSettings();
        if (this.checked) {
          showNotification('Mood tracking enabled 📊', '📊', 2000);
        }
      });

      // ========== VIEW MOOD HISTORY ==========
      viewMoodHistoryBtn.addEventListener('click', function() {
        loadMoodHistory();
        if (moodHistory.length === 0) {
          showNotification('No mood history yet! Complete the welcome form first 📝', '📋', 3000);
          return;
        }

        // Create a modal-like display
        let historyText = 'Your Mood History:\n\n';
        moodHistory.forEach((entry, index) => {
          historyText += `${entry.date} - ${entry.mood} ${entry.emoji || ''}\n`;
        });
        
        alert(historyText);
      });

      // ========== RESET PROFILE ==========
      resetProfileBtn.addEventListener('click', function() {
        if (confirm('Are you sure you want to reset everything? This will clear your profile, notes, mood history, and settings. This cannot be undone.')) {
          // Clear all data
          localStorage.removeItem('sereneUserProfile');
          localStorage.removeItem('sereneGratitudeNotes');
          localStorage.removeItem('sereneMoodHistory');
          localStorage.removeItem('sereneSettings');
          
          // Stop sounds
          stopAllSounds();
          stopNotifications();
          
          // Reset state
          onboardingComplete = false;
          userProfile = null;
          moodHistory = [];
          
          // Reset settings toggles
          darkModeToggle.checked = false;
          notificationsToggle.checked = true;
          autoSoundToggle.checked = false;
          moodTrackingToggle.checked = true;
          document.body.classList.remove('dark-mode');
          
          // Reset form
          document.getElementById('nameInput').value = '';
          document.getElementById('ageInput').value = '';
          document.getElementById('genderSelect').value = '';
          document.getElementById('hobbiesInput').value = '';
          document.querySelectorAll('.mood-option').forEach(opt => opt.classList.remove('selected'));
          document.getElementById('nameError').textContent = '';
          document.getElementById('ageError').textContent = '';
          document.getElementById('genderError').textContent = '';
          document.getElementById('moodError').textContent = '';
          
          // Show onboarding
          Object.values(tabContents).forEach(c => c.classList.remove('active'));
          onboardingTab.classList.add('active');
          onboardingTab.style.display = 'block';
          
          // Reset tab buttons
          tabBtns.forEach(b => b.classList.remove('active'));
          document.querySelector('[data-tab="home"]').classList.add('active');
          
          // Reset greeting
          document.getElementById('personalGreeting').textContent = 'welcome, friend';
          
          showNotification('Profile reset complete. Welcome! 🌱', '🔄', 3000);
          
          // Restart notifications with default settings
          saveCurrentSettings();
          startNotifications();
        }
      });

      function saveCurrentSettings() {
        const currentSettings = {
          darkMode: darkModeToggle.checked,
          notifications: notificationsToggle.checked,
          autoSound: autoSoundToggle.checked,
          moodTracking: moodTrackingToggle.checked
        };
        saveSettings(currentSettings);
        
        // Update local reference
        Object.assign(settings, currentSettings);
      }

      // ========== TAB SWITCHING ==========
      function switchTab(tabName) {
        // Hide all tabs
        Object.values(tabContents).forEach(content => {
          content.classList.remove('active');
        });
        if (!onboardingComplete) {
          onboardingTab.classList.remove('active');
          onboardingTab.style.display = 'none';
        }

        // Show selected tab
        if (tabName === 'home' && onboardingComplete) {
          homeTab.classList.add('active');
          // Auto-play sounds if enabled and not already playing
          if (autoSoundToggle.checked && !soundPlaying) {
            setTimeout(() => startCalmSoundscape(), 500);
          }
        } else if (tabContents[tabName]) {
          tabContents[tabName].classList.add('active');
        }

        // Update active button
        tabBtns.forEach(btn => {
          btn.classList.remove('active');
          if (btn.getAttribute('data-tab') === tabName) {
            btn.classList.add('active');
          }
        });

        // Stop sounds when leaving home tab
        if (tabName !== 'home' && soundPlaying) {
          stopAllSounds();
        }
      }

      tabBtns.forEach(btn => {
        btn.addEventListener('click', function() {
          const tabName = this.getAttribute('data-tab');
          
          if (!onboardingComplete && tabName !== 'home') {
            showNotification('Please complete the welcome form first! 🌱', '🌸', 3000);
            return;
          }
          
          if (tabName === 'home' && !onboardingComplete) {
            onboardingTab.classList.add('active');
            onboardingTab.style.display = 'block';
            homeTab.classList.remove('active');
            tabBtns.forEach(b => b.classList.remove('active'));
            this.classList.add('active');
            return;
          }

          switchTab(tabName);
        });
      });

      // ========== ONBOARDING LOGIC ==========
      const enterBtn = document.getElementById('enterBtn');
      const nameInput = document.getElementById('nameInput');
      const ageInput = document.getElementById('ageInput');
      const genderSelect = document.getElementById('genderSelect');
      const hobbiesInput = document.getElementById('hobbiesInput');
      const nameError = document.getElementById('nameError');
      const ageError = document.getElementById('ageError');
      const genderError = document.getElementById('genderError');
      const moodError = document.getElementById('moodError');
      const moodOptions = document.querySelectorAll('.mood-option');
      let selectedMood = null;

      moodOptions.forEach(option => {
        option.addEventListener('click', function() {
          moodOptions.forEach(opt => opt.classList.remove('selected'));
          this.classList.add('selected');
          selectedMood = this.getAttribute('data-mood');
          moodError.textContent = '';
        });
      });

      function clearErrors() {
        nameError.textContent = '';
        ageError.textContent = '';
        genderError.textContent = '';
        moodError.textContent = '';
      }

      enterBtn.addEventListener('click', function() {
        clearErrors();
        let valid = true;

        const name = nameInput.value.trim();
        if (name === '') {
          nameError.textContent = 'please tell us your name or nickname 🌱';
          valid = false;
        } else if (name.length < 2) {
          nameError.textContent = 'a little longer? (at least 2 characters)';
          valid = false;
        }

        const age = parseInt(ageInput.value, 10);
        if (isNaN(age)) {
          ageError.textContent = 'enter your age';
          valid = false;
        } else if (age < 10 || age > 20) {
          ageError.textContent = 'this space is designed for ages 13-19';
          valid = false;
        }

        if (genderSelect.value === '' || genderSelect.value === null) {
          genderError.textContent = 'select one or prefer not to say';
          valid = false;
        }

        if (!selectedMood) {
          moodError.textContent = 'tap a feeling above';
          valid = false;
        }

        if (!valid) return;

        userProfile = {
          name: name,
          age: age,
          gender: genderSelect.value,
          hobbies: hobbiesInput.value.trim() || 'various interests',
          mood: selectedMood,
          timestamp: new Date().toISOString()
        };
        localStorage.setItem('sereneUserProfile', JSON.stringify(userProfile));

        // Track mood if enabled
        if (moodTrackingToggle.checked) {
          const moodEmojis = {
            'calm': '😌', 'anxious': '😟', 'tired': '😴',
            'okay': '🙂', 'sad': '🥺', 'hopeful': '🌟'
          };
          moodHistory.push({
            mood: selectedMood,
            emoji: moodEmojis[selectedMood] || '',
            date: new Date().toLocaleDateString(),
            time: new Date().toLocaleTimeString()
          });
          saveMoodHistory();
        }

        onboardingComplete = true;
        onboardingTab.classList.remove('active');
        onboardingTab.style.display = 'none';
        
        document.getElementById('personalGreeting').textContent = 
          'hey ' + userProfile.name + ' ✦ feeling ' + userProfile.mood + ' · we got you';
        
        initMainApp(userProfile);
        switchTab('home');
        
        showNotification('Welcome to your serene space, ' + userProfile.name + '! 🌿', '✨', 3000);
      });

      // ========== MAIN APP INITIALIZATION ==========
      function initMainApp(profile) {
        // Affirmations
        const affirmations = [
          "you are enough, exactly as you are.",
          "this moment is gentle; let it hold you.",
          "your feelings are valid and temporary.",
          "breathe in calm, breathe out worry.",
          "you belong here, right now.",
          "it's okay to rest. you're not behind.",
          "small steps still move you forward.",
          "kindness towards yourself is powerful.",
          "you are not alone in this.",
          "let the world be soft for a moment.",
          "peace begins with a single breath.",
          "you are worthy of good things.",
          "anxiety does not define you.",
          "stillness is a form of strength."
        ];

        const affirmationDisplay = document.getElementById('affirmationDisplay');
        const newAffirmationBtn = document.getElementById('newAffirmationBtn');

        function setRandomAffirmation() {
          const randomIndex = Math.floor(Math.random() * affirmations.length);
          affirmationDisplay.style.opacity = '0.6';
          setTimeout(() => {
            affirmationDisplay.textContent = affirmations[randomIndex];
            affirmationDisplay.style.opacity = '1';
          }, 120);
        }

        newAffirmationBtn.addEventListener('click', setRandomAffirmation);
        setRandomAffirmation();

        // Breathing
        const breathingTool = document.getElementById('breathingTool');
        const breathingBox = document.getElementById('breathingBox');
        const breathCircle = document.getElementById('breathCircle');
        const breathText = document.getElementById('breathText');
        const stopBreathBtn = document.getElementById('stopBreathBtn');
        const gratitudeNoteBox = document.getElementById('gratitudeNoteBox');
        let breathInterval = null;
        let breathActive = false;

        function resetBreathingUI() {
          if (breathInterval) {
            clearInterval(breathInterval);
            breathInterval = null;
          }
          breathActive = false;
          breathCircle.style.transform = 'scale(1)';
          breathText.textContent = 'inhale';
          breathingBox.classList.add('hidden');
          breathingTool.classList.remove('active-tool');
        }

        function startBreathingCycle() {
          if (breathActive) return;
          breathActive = true;
          breathingBox.classList.remove('hidden');
          breathingTool.classList.add('active-tool');
          
          let phase = 'inhale';
          breathText.textContent = 'inhale';
          breathCircle.style.transform = 'scale(0.85)';
          let counter = 0;
          
          breathInterval = setInterval(() => {
            if (!breathActive) return;
            
            if (phase === 'inhale') {
              let scale = parseFloat(breathCircle.style.transform.replace('scale(', '').replace(')', '')) || 0.85;
              if (scale < 1.25) {
                scale += 0.008;
                breathCircle.style.transform = `scale(${Math.min(scale, 1.25)})`;
              }
              counter++;
              if (counter >= 40) { phase = 'hold'; breathText.textContent = 'hold gently'; counter = 0; }
            } else if (phase === 'hold') {
              counter++;
              if (counter >= 20) { phase = 'exhale'; breathText.textContent = 'exhale slowly'; counter = 0; }
            } else if (phase === 'exhale') {
              let scale = parseFloat(breathCircle.style.transform.replace('scale(', '').replace(')', '')) || 1.25;
              if (scale > 0.8) {
                scale -= 0.007;
                breathCircle.style.transform = `scale(${Math.max(scale, 0.8)})`;
              }
              counter++;
              if (counter >= 50) { phase = 'inhale'; breathText.textContent = 'inhale'; counter = 0; }
            }
          }, 100);
        }

        breathingTool.addEventListener('click', () => {
          gratitudeNoteBox.classList.add('hidden');
          document.getElementById('gratitudeTool').classList.remove('active-tool');
          if (breathActive) {
            clearInterval(breathInterval);
            breathInterval = null;
            breathActive = false;
          }
          startBreathingCycle();
        });

        stopBreathBtn.addEventListener('click', resetBreathingUI);

        // Gratitude
        const gratitudeTool = document.getElementById('gratitudeTool');
        const gratitudeInput = document.getElementById('gratitudeInput');
        const saveGratitudeBtn = document.getElementById('saveGratitudeBtn');
        const gratitudeFeedback = document.getElementById('gratitudeFeedback');

        gratitudeTool.addEventListener('click', () => {
          if (breathActive) resetBreathingUI();
          gratitudeNoteBox.classList.toggle('hidden');
          if (!gratitudeNoteBox.classList.contains('hidden')) {
            gratitudeInput.focus();
            gratitudeTool.classList.add('active-tool');
          } else {
            gratitudeTool.classList.remove('active-tool');
          }
          gratitudeFeedback.textContent = '';
        });

        saveGratitudeBtn.addEventListener('click', () => {
          const note = gratitudeInput.value.trim();
          if (note === '') {
            gratitudeFeedback.textContent = 'write a little something 🌱';
            return;
          }
          try {
            const savedNotes = JSON.parse(localStorage.getItem('sereneGratitudeNotes') || '[]');
            savedNotes.push({ text: note, date: new Date().toLocaleDateString() });
            localStorage.setItem('sereneGratitudeNotes', JSON.stringify(savedNotes));
            gratitudeFeedback.textContent = 'saved with care 🤍';
            gratitudeInput.value = '';
            setTimeout(() => { gratitudeFeedback.textContent = ''; }, 2500);
            showNotification('Note saved! 🤍', '📝', 2000);
          } catch (e) {
            gratitudeFeedback.textContent = 'saved in this moment.';
          }
        });

        // Sounds
        const calmSoundsTool = document.getElementById('calmSoundsTool');
        const soundStatus = document.getElementById('soundStatus');

        function createNoiseBuffer(duration = 2, sampleRate = 44100) {
          const bufferSize = duration * sampleRate;
          const buffer = audioCtx.createBuffer(1, bufferSize, sampleRate);
          const data = buffer.getChannelData(0);
          let b0 = 0, b1 = 0, b2 = 0, b3 = 0, b4 = 0, b5 = 0, b6 = 0;
          for (let i = 0; i < bufferSize; i++) {
            const white = Math.random() * 2 - 1;
            b0 = 0.99886 * b0 + white * 0.0555179;
            b1 = 0.99332 * b1 + white * 0.0750759;
            b2 = 0.96900 * b2 + white * 0.1538520;
            b3 = 0.86650 * b3 + white * 0.3104856;
            b4 = 0.55000 * b4 + white * 0.5329522;
            b5 = -0.7616 * b5 - white * 0.0168980;
            data[i] = (b0 + b1 + b2 + b3 + b4 + b5 + b6 + white * 0.5362) * 0.11;
            b6 = white * 0.115926;
          }
          return buffer;
        }

        window.stopAllSounds = function() {
          soundNodes.forEach(node => {
            try {
              if (node.stop) node.stop();
              if (node.disconnect) node.disconnect();
            } catch (e) {}
          });
          soundNodes = [];
          soundPlaying = false;
          calmSoundsTool.classList.remove('active-tool');
          soundStatus.innerHTML = '';
        };

        function startCalmSoundscape() {
          if (soundPlaying) return;
          try {
            if (!audioCtx) {
              audioCtx = new (window.AudioContext || window.webkitAudioContext)();
            }
            const noiseBuffer = createNoiseBuffer(3);
            const noiseSource = audioCtx.createBufferSource();
            noiseSource.buffer = noiseBuffer;
            noiseSource.loop = true;
            const noiseFilter = audioCtx.createBiquadFilter();
            noiseFilter.type = 'lowpass';
            noiseFilter.frequency.setValueAtTime(800, audioCtx.currentTime);
            const noiseGain = audioCtx.createGain();
            noiseGain.gain.setValueAtTime(0.04, audioCtx.currentTime);
            noiseSource.connect(noiseFilter);
            noiseFilter.connect(noiseGain);
            noiseGain.connect(audioCtx.destination);
            noiseSource.start();
            soundNodes.push(noiseSource, noiseFilter, noiseGain);
            
            soundPlaying = true;
            calmSoundsTool.classList.add('active-tool');
            soundStatus.innerHTML = '<span class="sound-active-indicator"></span> soft nature sounds playing · tap again to stop';
          } catch (e) {
            soundStatus.textContent = '🎵 sound not supported in this browser';
            stopAllSounds();
          }
        }

        calmSoundsTool.addEventListener('click', () => {
          if (soundPlaying) {
            stopAllSounds();
            return;
          }
          if (breathActive) resetBreathingUI();
          gratitudeNoteBox.classList.add('hidden');
          gratitudeTool.classList.remove('active-tool');
          startCalmSoundscape();
        });

        // Mood Palette
        const colorMoodTool = document.getElementById('colorMoodTool');
        const root = document.documentElement;
        
        const calmPalettes = [
          { 
            name: 'soft dawn', emoji: '🌅',
            colors: {
              '--bg-gradient': 'linear-gradient(145deg, #f6efe9 0%, #e3edf5 100%)',
              '--card-bg': 'rgba(250, 247, 252, 0.7)',
              '--text-primary': '#2e3b4e', '--text-secondary': '#6a5e7c', '--text-tertiary': '#4e4b5c',
              '--accent': '#b8a3cc', '--accent-light': '#efe2f7', '--accent-dark': '#7c6b8f',
              '--input-bg': 'rgba(255, 255, 250, 0.75)', '--input-border': '#d9cfdf',
              '--button-bg': '#efe2f7', '--button-border': '#cfbedb', '--button-hover': '#e1cef0',
              '--mood-selected': '#e3d4f0', '--mood-selected-border': '#a58db8',
              '--tool-bg': 'rgba(252, 250, 255, 0.7)', '--tool-hover': 'rgba(255, 251, 250, 0.8)',
              '--affirmation-bg': 'rgba(255, 250, 245, 0.75)', '--breathing-bg': 'rgba(234, 225, 245, 0.55)',
              '--greeting-bg': 'rgba(239, 232, 245, 0.7)', '--shadow': 'rgba(148, 126, 158, 0.15)',
              '--orb-1': 'rgba(203, 182, 219, 0.25)', '--orb-2': 'rgba(167, 196, 188, 0.3)', '--orb-3': 'rgba(251, 225, 198, 0.4)',
              '--toggle-bg': '#ccc', '--footer-color': '#8b7f94'
            },
            description: 'gentle morning light'
          },
          { 
            name: 'lavender mist', emoji: '💜',
            colors: {
              '--bg-gradient': 'linear-gradient(145deg, #f2e9f9 0%, #dae9f0 100%)',
              '--card-bg': 'rgba(245, 240, 255, 0.75)',
              '--text-primary': '#3a2e4e', '--text-secondary': '#6b5b8a', '--text-tertiary': '#55476c',
              '--accent': '#9b8ec4', '--accent-light': '#e8dff5', '--accent-dark': '#6b5b8a',
              '--input-bg': 'rgba(250, 248, 255, 0.8)', '--input-border': '#c8bcdb',
              '--button-bg': '#e8dff5', '--button-border': '#c8bcdb', '--button-hover': '#d4c5ed',
              '--mood-selected': '#d4c5ed', '--mood-selected-border': '#9b8ec4',
              '--tool-bg': 'rgba(248, 245, 255, 0.75)', '--tool-hover': 'rgba(240, 235, 255, 0.85)',
              '--affirmation-bg': 'rgba(245, 240, 255, 0.8)', '--breathing-bg': 'rgba(235, 225, 250, 0.6)',
              '--greeting-bg': 'rgba(240, 232, 250, 0.75)', '--shadow': 'rgba(130, 110, 160, 0.18)',
              '--orb-1': 'rgba(195, 175, 225, 0.3)', '--orb-2': 'rgba(170, 190, 210, 0.35)', '--orb-3': 'rgba(230, 200, 220, 0.4)',
              '--toggle-bg': '#c8bcdb', '--footer-color': '#8b7fa8'
            },
            description: 'purple calm'
          }
        ];
        let paletteIndex = 0;

        function applyPalette(palette) {
          for (const [property, value] of Object.entries(palette.colors)) {
            root.style.setProperty(property, value);
          }
        }

        colorMoodTool.addEventListener('click', () => {
          paletteIndex = (paletteIndex + 1) % calmPalettes.length;
          const selected = calmPalettes[paletteIndex];
          applyPalette(selected);
          soundStatus.innerHTML = `${selected.emoji} ${selected.name} · ${selected.description}`;
          colorMoodTool.classList.add('active-tool');
          setTimeout(() => colorMoodTool.classList.remove('active-tool'), 1000);
          if (breathActive) resetBreathingUI();
          gratitudeNoteBox.classList.add('hidden');
          gratitudeTool.classList.remove('active-tool');
        });

        applyPalette(calmPalettes[0]);
      }

      // ========== INITIAL SETUP ==========
      if (onboardingComplete && userProfile) {
        onboardingTab.classList.remove('active');
        onboardingTab.style.display = 'none';
        homeTab.classList.add('active');
        document.getElementById('personalGreeting').textContent = 
          'hey ' + userProfile.name + ' ✦ feeling ' + userProfile.mood + ' · we got you';
        initMainApp(userProfile);
        
        // Pre-fill form for possible re-entry
        document.getElementById('nameInput').value = userProfile.name || '';
        document.getElementById('ageInput').value = userProfile.age || '';
        document.getElementById('genderSelect').value = userProfile.gender || '';
        document.getElementById('hobbiesInput').value = userProfile.hobbies || '';
        if (userProfile.mood) {
          document.querySelectorAll('.mood-option').forEach(opt => {
            if (opt.getAttribute('data-mood') === userProfile.mood) {
              opt.classList.add('selected');
            }
          });
        }
        
        // Auto-play sounds if enabled
        if (autoSoundToggle.checked) {
          setTimeout(() => {
            if (typeof startCalmSoundscape === 'function') startCalmSoundscape();
          }, 1000);
        }
      }

      // Cleanup on page unload
      window.addEventListener('beforeunload', () => {
        stopAllSounds();
        stopNotifications();
      });
    })();
  </script>
</body>
</html>
