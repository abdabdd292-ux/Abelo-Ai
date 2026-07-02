<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no, viewport-fit=cover">
<meta name="theme-color" content="#0d0f14">
<title>Abelo AI - Assistant & Image Studio</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Poppins:wght@600;700;800&family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
<style>
:root{
  --bg:#0b0d12; --bg2:#131722; --bg3:#1b202c; --border:#262c3a;
  --text:#eef0f4; --text-dim:#98a1b3; --accent:#7c5cff; --accent2:#00d9b5;
  --danger:#ff5c5c; --warn:#ffb020; --bubble-user:linear-gradient(135deg,#7c5cff,#5b3df0);
  --bubble-ai:#181d29; --radius:18px; --vh: 1vh;
  --grad: linear-gradient(135deg,#7c5cff,#00d9b5);
}
*{box-sizing:border-box;margin:0;padding:0;-webkit-tap-highlight-color:transparent;}
html,body{height:calc(var(--vh,1vh)*100);overflow:hidden;}
body{
  background:var(--bg); color:var(--text);
  font-family:'Inter',-apple-system,BlinkMacSystemFont,'Segoe UI',Roboto,sans-serif;
  font-size:15px; display:flex; flex-direction:column; height:calc(var(--vh,1vh)*100);
  position:relative;
}
h1,h2,h3,.headline{font-family:'Poppins',sans-serif;}
button{font-family:inherit; cursor:pointer; border:none; outline:none; background:none; color:inherit;}
button:disabled{opacity:.5;pointer-events:none;}
input,textarea{font-family:inherit; outline:none; border:none; background:none; color:inherit;}
::-webkit-scrollbar{width:6px;height:6px;}
::-webkit-scrollbar-thumb{background:var(--border);border-radius:10px;}
img{max-width:100%;display:block;}

/* Ambient background glow */
#bgGlow{position:fixed;inset:0;z-index:0;pointer-events:none;overflow:hidden;}
#bgGlow::before, #bgGlow::after{
  content:'';position:absolute;width:340px;height:340px;border-radius:50%;filter:blur(90px);opacity:.16;
}
#bgGlow::before{background:var(--accent);top:-100px;left:-80px;}
#bgGlow::after{background:var(--accent2);bottom:-100px;right:-80px;}

#topbar{
  display:flex; align-items:center; justify-content:space-between;
  padding:14px 14px; background:rgba(19,23,34,.85); backdrop-filter:blur(10px);
  border-bottom:1px solid var(--border); flex-shrink:0; z-index:20;
}
#topbar .brand{display:flex;align-items:center;gap:9px;font-weight:800;font-size:18px;font-family:'Poppins',sans-serif;letter-spacing:-.2px;}
.logo-mark{width:30px;height:30px;border-radius:9px;background:var(--grad);display:flex;align-items:center;justify-content:center;font-size:15px;box-shadow:0 4px 14px rgba(124,92,255,.4);}
#topbar .icons{display:flex;gap:12px;align-items:center;}
#topbar .icon-btn{font-size:19px;padding:5px;border-radius:10px;}
#topbar .icon-btn:active{background:var(--bg3);}
.plan-badge{font-size:10.5px;padding:4px 10px;border-radius:20px;background:var(--grad);color:#fff;font-weight:700;letter-spacing:.3px;}
.plan-badge.free{background:var(--bg3);color:var(--text-dim);border:1px solid var(--border);}

#overlay{position:fixed;inset:0;background:rgba(0,0,0,.6);z-index:29;display:none;backdrop-filter:blur(2px);}
#overlay.show{display:block;}
#sidebar{
  position:fixed;top:0;left:0;height:100%;width:84%;max-width:320px;background:var(--bg2);
  border-right:1px solid var(--border);transform:translateX(-105%);transition:transform .3s cubic-bezier(.4,0,.2,1);
  z-index:30;display:flex;flex-direction:column;padding:16px;
}
#sidebar.open{transform:translateX(0);}
.streak-card{
  background:var(--grad);border-radius:14px;padding:12px 14px;margin-bottom:14px;
  display:flex;align-items:center;gap:10px;color:#fff;
}
.streak-card .num{font-size:20px;font-weight:800;font-family:'Poppins',sans-serif;}
.streak-card .lbl{font-size:11px;opacity:.9;}
#sidebar h3{font-size:12px;color:var(--text-dim);text-transform:uppercase;letter-spacing:.6px;margin:14px 0 8px;font-weight:700;}
.sb-btn{display:flex;align-items:center;gap:10px;padding:12px 13px;border-radius:13px;background:var(--bg3);margin-bottom:8px;font-size:14px;font-weight:600;transition:.15s;}
.sb-btn:active{background:var(--border);transform:scale(.98);}
#chatHistoryList{flex:1;overflow-y:auto;}
.hist-item{padding:10px 12px;border-radius:11px;font-size:13.5px;color:var(--text-dim);margin-bottom:4px;white-space:nowrap;overflow:hidden;text-overflow:ellipsis;display:flex;justify-content:space-between;align-items:center;gap:6px;}
.hist-item:active{background:var(--bg3);}
.hist-item .del{opacity:.5;font-size:15px;flex-shrink:0;}
.sidebar-footer{border-top:1px solid var(--border);padding-top:10px;margin-top:8px;}

#main{flex:1;display:flex;flex-direction:column;overflow:hidden;position:relative;z-index:1;}
.view{flex:1;display:none;flex-direction:column;overflow:hidden;}
.view.active{display:flex;}

#chatWindow{flex:1;overflow-y:auto;padding:16px 12px 8px;display:flex;flex-direction:column;gap:16px;position:relative;}
.empty-chat{flex:1;display:flex;flex-direction:column;align-items:center;justify-content:center;text-align:center;padding:30px;color:var(--text-dim);gap:8px;}
.empty-chat .emoji{font-size:42px;margin-bottom:6px;}
.msg{max-width:88%;display:flex;flex-direction:column;gap:5px;animation:fadeUp .3s ease;}
@keyframes fadeUp{from{opacity:0;transform:translateY(10px);}to{opacity:1;transform:translateY(0);}}
.msg.user{align-self:flex-end;align-items:flex-end;}
.msg.ai{align-self:flex-start;align-items:flex-start;}
.bubble{padding:12px 15px;border-radius:var(--radius);line-height:1.55;font-size:14.5px;white-space:pre-wrap;word-break:break-word;}
.msg.user .bubble{background:var(--bubble-user);color:#fff;border-bottom-right-radius:5px;box-shadow:0 4px 14px rgba(124,92,255,.25);}
.msg.ai .bubble{background:var(--bubble-ai);border:1px solid var(--border);border-bottom-left-radius:5px;}
.msg .meta{font-size:10.5px;color:var(--text-dim);padding:0 4px;display:flex;gap:8px;align-items:center;}
.msg-actions{display:flex;gap:6px;padding:0 4px;}
.msg-actions button{font-size:11px;color:var(--text-dim);background:var(--bg3);border:1px solid var(--border);padding:3px 9px;border-radius:8px;display:flex;align-items:center;gap:4px;}
.msg-actions button:active{background:var(--border);}
.bubble img.gen-img{border-radius:13px;margin-top:6px;max-width:240px;}
.bubble .img-actions{display:flex;gap:8px;margin-top:8px;}
.bubble .img-actions button{background:var(--bg3);padding:6px 10px;border-radius:8px;font-size:12px;border:1px solid var(--border);}
.typing{display:flex;gap:4px;padding:6px 4px;}
.typing span{width:6px;height:6px;background:var(--text-dim);border-radius:50%;animation:blink 1.2s infinite ease-in-out;}
.typing span:nth-child(2){animation-delay:.2s;}
.typing span:nth-child(3){animation-delay:.4s;}
@keyframes blink{0%,80%,100%{opacity:.2;}40%{opacity:1;}}

#scrollBottomBtn{
  position:absolute;bottom:14px;right:14px;width:38px;height:38px;border-radius:50%;
  background:var(--bg3);border:1px solid var(--border);display:none;align-items:center;justify-content:center;
  font-size:16px;box-shadow:0 4px 12px rgba(0,0,0,.3);z-index:5;
}
#scrollBottomBtn.show{display:flex;}

#quickChips{display:flex;gap:8px;padding:8px 12px;overflow-x:auto;flex-shrink:0;}
.chip{background:var(--bg3);border:1px solid var(--border);padding:7px 13px;border-radius:20px;font-size:12.5px;white-space:nowrap;color:var(--text-dim);font-weight:500;}

#inputBar{display:flex;align-items:flex-end;gap:8px;padding:10px 10px calc(10px + env(safe-area-inset-bottom));background:rgba(19,23,34,.9);backdrop-filter:blur(10px);border-top:1px solid var(--border);flex-shrink:0;}
#inputBar textarea{flex:1;background:var(--bg3);border:1px solid var(--border);border-radius:22px;padding:12px 16px;max-height:100px;min-height:44px;resize:none;font-size:14.5px;}
.round-btn{width:44px;height:44px;border-radius:50%;background:var(--bg3);border:1px solid var(--border);display:flex;align-items:center;justify-content:center;font-size:18px;flex-shrink:0;transition:.15s;}
.round-btn:active{transform:scale(.92);}
.round-btn.primary{background:var(--grad);border:none;color:#fff;box-shadow:0 4px 14px rgba(124,92,255,.35);}
.round-btn.active{background:var(--danger);color:#fff;animation:pulse 1s infinite;}
@keyframes pulse{0%{box-shadow:0 0 0 0 rgba(255,92,92,.5);}70%{box-shadow:0 0 0 10px rgba(255,92,92,0);}100%{box-shadow:0 0 0 0 rgba(255,92,92,0);}}

#bottomNav{display:flex;background:var(--bg2);border-top:1px solid var(--border);flex-shrink:0;padding-bottom:env(safe-area-inset-bottom);}
.nav-btn{flex:1;display:flex;flex-direction:column;align-items:center;gap:3px;padding:10px 0 8px;color:var(--text-dim);font-size:10.5px;font-weight:600;transition:.15s;}
.nav-btn .ic{font-size:20px;}
.nav-btn.active{color:var(--accent);}

#studioView{padding:14px;overflow-y:auto;gap:16px;}
.studio-card{background:var(--bg2);border:1px solid var(--border);border-radius:var(--radius);padding:17px;margin-bottom:14px;}
.studio-card h3{font-size:15.5px;margin-bottom:10px;display:flex;align-items:center;gap:8px;font-weight:700;}
.studio-card textarea, .studio-card input[type=text]{width:100%;background:var(--bg3);border:1px solid var(--border);border-radius:13px;padding:12px;font-size:14px;margin-bottom:10px;}
.studio-card textarea{min-height:70px;resize:vertical;}
.btn-full{width:100%;padding:13px;border-radius:13px;background:var(--grad);color:#fff;font-weight:700;font-size:14.5px;box-shadow:0 4px 14px rgba(124,92,255,.3);}
.btn-full.secondary{background:var(--bg3);border:1px solid var(--border);color:var(--text);box-shadow:none;}
.btn-full:disabled{opacity:.5;}
.upload-zone{border:2px dashed var(--border);border-radius:15px;padding:26px 12px;text-align:center;color:var(--text-dim);margin-bottom:10px;font-size:13px;}
.tool-grid{display:grid;grid-template-columns:1fr 1fr;gap:9px;margin-top:10px;}
.tool-grid button{background:var(--bg3);border:1px solid var(--border);border-radius:13px;padding:13px 6px;font-size:12.5px;display:flex;flex-direction:column;align-items:center;gap:6px;position:relative;font-weight:600;}
.tool-grid button .ic{font-size:21px;}
.lock-tag{position:absolute;top:4px;right:6px;font-size:9px;background:var(--grad);color:#fff;padding:2px 6px;border-radius:6px;font-weight:700;}
#studioPreview{width:100%;border-radius:13px;margin:10px 0;max-height:320px;object-fit:contain;background:#000;}
canvas{display:none;}
.slider-row{display:flex;align-items:center;gap:10px;margin-bottom:10px;font-size:12.5px;color:var(--text-dim);}
.slider-row input[type=range]{flex:1;accent-color:var(--accent);}
.result-badge{font-size:11px;background:rgba(0,217,181,.15);color:var(--accent2);padding:4px 9px;border-radius:8px;display:inline-block;margin-bottom:8px;font-weight:700;}

#filesView{padding:14px;overflow-y:auto;}
.file-item{background:var(--bg2);border:1px solid var(--border);border-radius:13px;padding:12px;display:flex;align-items:center;gap:12px;margin-bottom:8px;}
.file-item .fic{font-size:22px;}
.file-item .finfo{flex:1;overflow:hidden;}
.file-item .fname{font-size:13.5px;font-weight:600;white-space:nowrap;overflow:hidden;text-overflow:ellipsis;}
.file-item .fsize{font-size:11px;color:var(--text-dim);}

.modal-bg{position:fixed;inset:0;background:rgba(0,0,0,.65);z-index:50;display:none;align-items:flex-end;justify-content:center;}
.modal-bg.show{display:flex;}
.modal{background:var(--bg2);width:100%;max-width:480px;border-radius:22px 22px 0 0;padding:22px;max-height:88vh;overflow-y:auto;animation:slideUp .3s cubic-bezier(.4,0,.2,1);}
@keyframes slideUp{from{transform:translateY(100%);}to{transform:translateY(0);}}
.modal h2{font-size:19px;margin-bottom:14px;display:flex;justify-content:space-between;align-items:center;font-weight:700;}
.modal h2 .close{font-size:22px;color:var(--text-dim);}
.field{margin-bottom:12px;}
.field label{font-size:12px;color:var(--text-dim);display:block;margin-bottom:6px;font-weight:600;}
.field input,.field textarea{width:100%;background:var(--bg3);border:1px solid var(--border);border-radius:11px;padding:12px;font-size:14px;}

/* Pricing comparison table */
.price-header{text-align:center;margin-bottom:18px;}
.price-header .emoji{font-size:34px;}
.compare-table{width:100%;border-collapse:collapse;font-size:12.5px;margin-bottom:16px;}
.compare-table th{padding:10px 4px;text-align:center;font-family:'Poppins',sans-serif;font-size:12.5px;}
.compare-table th:first-child{text-align:left;}
.compare-table th.premium-col{background:var(--grad);color:#fff;border-radius:10px 10px 0 0;}
.compare-table td{padding:9px 4px;text-align:center;border-top:1px solid var(--border);color:var(--text-dim);}
.compare-table td:first-child{text-align:left;color:var(--text);font-weight:500;}
.compare-table td.premium-col{background:rgba(124,92,255,.08);}
.compare-table .yes{color:var(--accent2);font-weight:700;}
.compare-table .no{color:var(--text-dim);opacity:.4;}
.upgrade-cta{background:var(--grad);border-radius:16px;padding:18px;text-align:center;color:#fff;margin-top:8px;}
.upgrade-cta .price-big{font-size:26px;font-weight:800;font-family:'Poppins',sans-serif;margin:4px 0;}
.upgrade-cta button{width:100%;background:#fff;color:var(--accent);font-weight:700;padding:12px;border-radius:12px;margin-top:12px;font-size:14.5px;}

.stat-row{display:flex;justify-content:space-between;padding:10px 0;border-bottom:1px solid var(--border);font-size:13.5px;}
.stat-row b{color:var(--accent2);}
.toggle-row{display:flex;justify-content:space-between;align-items:center;padding:10px 0;border-bottom:1px solid var(--border);}
.switch{width:44px;height:24px;border-radius:20px;background:var(--bg3);position:relative;border:1px solid var(--border);}
.switch.on{background:var(--accent2);}
.switch::after{content:'';position:absolute;width:18px;height:18px;background:#fff;border-radius:50%;top:2px;left:2px;transition:.2s;}
.switch.on::after{left:22px;}
.toast{position:fixed;bottom:90px;left:50%;transform:translateX(-50%);background:var(--bg3);border:1px solid var(--border);padding:11px 18px;border-radius:30px;font-size:13px;z-index:99;opacity:0;transition:.3s;pointer-events:none;max-width:85%;text-align:center;font-weight:500;}
.toast.show{opacity:1;bottom:100px;}
.toast.error{border-color:var(--danger);color:#ffb3b3;}
.lang-toggle{display:flex;background:var(--bg3);border-radius:20px;padding:3px;margin-bottom:10px;}
.lang-toggle button{flex:1;padding:9px;border-radius:18px;font-size:12.5px;color:var(--text-dim);font-weight:600;}
.lang-toggle button.active{background:var(--grad);color:#fff;}
.warn-note{font-size:11px;color:var(--warn);background:rgba(255,176,32,.1);border:1px solid rgba(255,176,32,.3);padding:9px 11px;border-radius:11px;margin-bottom:10px;line-height:1.5;}
.ok-note{font-size:11px;color:var(--accent2);background:rgba(0,217,181,.1);border:1px solid rgba(0,217,181,.3);padding:9px 11px;border-radius:11px;margin-bottom:10px;line-height:1.5;}

/* Theme picker */
.theme-grid{display:grid;grid-template-columns:repeat(3,1fr);gap:10px;margin-bottom:14px;}
.theme-swatch{aspect-ratio:1;border-radius:14px;position:relative;border:2px solid transparent;display:flex;align-items:flex-end;justify-content:center;padding-bottom:6px;}
.theme-swatch.selected{border-color:#fff;}
.theme-swatch .swatch-lock{position:absolute;top:6px;right:6px;font-size:9px;background:rgba(0,0,0,.4);color:#fff;padding:2px 5px;border-radius:5px;}
.theme-swatch span{font-size:10px;color:#fff;font-weight:700;text-shadow:0 1px 3px rgba(0,0,0,.5);}

/* Onboarding */
#onboardModal{position:fixed;inset:0;background:var(--bg);z-index:100;display:none;flex-direction:column;}
#onboardModal.show{display:flex;}
.onboard-slides{flex:1;display:flex;overflow-x:auto;scroll-snap-type:x mandatory;}
.onboard-slide{min-width:100%;scroll-snap-align:start;display:flex;flex-direction:column;align-items:center;justify-content:center;text-align:center;padding:40px 30px;gap:14px;}
.onboard-slide .big-emoji{font-size:70px;}
.onboard-slide h2{font-size:23px;}
.onboard-slide p{color:var(--text-dim);font-size:14.5px;line-height:1.6;max-width:300px;}
.onboard-dots{display:flex;justify-content:center;gap:7px;padding:14px;}
.onboard-dots span{width:7px;height:7px;border-radius:50%;background:var(--bg3);}
.onboard-footer{padding:16px 20px calc(20px + env(safe-area-inset-bottom));}

/* Confetti */
.confetti-piece{position:fixed;width:8px;height:14px;top:-20px;z-index:200;pointer-events:none;animation:confettiFall 2.6s ease-in forwards;}
@keyframes confettiFall{
  0%{transform:translateY(0) rotate(0deg);opacity:1;}
  100%{transform:translateY(110vh) rotate(540deg);opacity:0;}
}
</style>
</head>
<body>

<div id="bgGlow"></div>

<div id="topbar">
  <button class="icon-btn" onclick="toggleSidebar(true)">☰</button>
  <div class="brand"><span class="logo-mark">✨</span> Abelo AI</div>
  <div class="icons">
    <span class="plan-badge free" id="planBadge">FREE</span>
    <button class="icon-btn" onclick="openModal('settingsModal')">⚙️</button>
  </div>
</div>

<div id="overlay" onclick="toggleSidebar(false)"></div>

<div id="sidebar">
  <div class="streak-card">
    <span style="font-size:22px">🔥</span>
    <div><div class="num" id="streakNum">1</div><div class="lbl">day streak</div></div>
  </div>
  <button class="sb-btn" onclick="newChat()">➕ New Chat</button>
  <button class="sb-btn" onclick="openModal('subModal');toggleSidebar(false)">💎 Upgrade to Premium</button>
  <button class="sb-btn" onclick="openModal('themeModal');toggleSidebar(false)">🎨 App Theme</button>
  <h3>Chat History</h3>
  <div id="chatHistoryList"></div>
  <div class="sidebar-footer">
    <button class="sb-btn" onclick="openModal('settingsModal');toggleSidebar(false)">⚙️ Settings</button>
    <button class="sb-btn" onclick="openAdminLogin()">👑 Owner Panel</button>
  </div>
</div>

<div id="main">

  <div class="view active" id="chatView" data-view="chat">
    <div id="chatWindow">
      <button id="scrollBottomBtn" onclick="scrollChatToBottom()">⬇️</button>
    </div>
    <div id="quickChips">
      <div class="chip" onclick="quickPrompt('Explain this like I\'m 5:')">💡 Explain simply</div>
      <div class="chip" onclick="quickPrompt('Write code for:')">💻 Write code</div>
      <div class="chip" onclick="quickPrompt('Help me write:')">✍️ Writing help</div>
      <div class="chip" onclick="quickPrompt('Give me advice about:')">🎯 Advice</div>
      <div class="chip" onclick="switchView('studio')">🎨 Generate image</div>
    </div>
    <div id="inputBar">
      <button class="round-btn" onclick="triggerFileUpload('chat')">📎</button>
      <textarea id="chatInput" placeholder="Message Abelo AI... (EN/አማ)" rows="1" oninput="autoGrow(this)" onkeydown="handleInputKey(event)"></textarea>
      <button class="round-btn" id="micBtn" onclick="toggleVoiceInput()">🎤</button>
      <button class="round-btn primary" id="sendBtn" onclick="sendMessage()">➤</button>
    </div>
    <input type="file" id="hiddenFileInput" style="display:none" onchange="handleFileUpload(event)">
  </div>

  <div class="view" id="studioView" data-view="studio">
    <div class="lang-toggle">
      <button class="active" onclick="setStudioTab('generate',this)">Generate</button>
      <button onclick="setStudioTab('edit',this)">Edit / Enhance</button>
    </div>

    <div id="generateTab">
      <div class="studio-card">
        <h3>🖼️ Text → Image</h3>
        <textarea id="imgPrompt" placeholder="Describe the image... e.g. 'a lion wearing sunglasses, digital art'"></textarea>
        <button class="btn-full" id="genBtn" onclick="generateImage()">✨ Generate Image</button>
      </div>
      <div class="studio-card" id="genResultCard" style="display:none">
        <span class="result-badge">✅ Generated</span>
        <img id="genResultImg" style="border-radius:13px;width:100%;">
        <div class="tool-grid">
          <button onclick="downloadCurrentImage()"><span class="ic">⬇️</span>Download</button>
          <button onclick="sendGenToChat()"><span class="ic">💬</span>Send to Chat</button>
        </div>
      </div>
    </div>

    <div id="editTab" style="display:none">
      <div class="studio-card">
        <h3>📤 Upload Image</h3>
        <div class="upload-zone" onclick="document.getElementById('editFileInput').click()">Tap to upload an image (JPG/PNG)</div>
        <input type="file" id="editFileInput" accept="image/*" style="display:none" onchange="loadEditImage(event)">
        <img id="studioPreview" style="display:none">
        <canvas id="editCanvas"></canvas>
      </div>

      <div class="studio-card">
        <h3>🛠️ AI Tools</h3>
        <div class="tool-grid">
          <button onclick="removeBackground()">
            <span class="ic">✂️</span>Remove BG
            <span class="lock-tag" id="lock_removebg" style="display:none">PRO</span>
          </button>
          <button onclick="enhanceImage()">
            <span class="ic">🔎</span>Enhance / Upscale
            <span class="lock-tag" id="lock_enhance" style="display:none">PRO</span>
          </button>
          <button onclick="applyFilter('blur')"><span class="ic">🌫️</span>Blur</button>
          <button onclick="applyFilter('sharpen')"><span class="ic">🔪</span>Sharpen</button>
          <button onclick="applyFilter('grayscale')"><span class="ic">⚫</span>Grayscale</button>
          <button onclick="applyFilter('bright')"><span class="ic">☀️</span>Brighten</button>
        </div>
      </div>

      <div class="studio-card">
        <h3>✂️ Crop & Resize</h3>
        <div class="slider-row">Width: <input type="range" id="resizeW" min="50" max="1200" value="500" oninput="document.getElementById('wLbl').innerText=this.value"><span id="wLbl">500</span></div>
        <div class="slider-row">Height: <input type="range" id="resizeH" min="50" max="1200" value="500" oninput="document.getElementById('hLbl').innerText=this.value"><span id="hLbl">500</span></div>
        <button class="btn-full secondary" onclick="resizeImage()">Apply Resize</button>
      </div>

      <div class="studio-card">
        <button class="btn-full" onclick="downloadCurrentImage()">⬇️ Download Edited Image</button>
      </div>
    </div>
  </div>

  <div class="view" id="filesView" data-view="files">
    <button class="btn-full secondary" style="margin-bottom:14px" onclick="triggerFileUpload('files')">📎 Upload File</button>
    <div id="filesList"></div>
  </div>

  <div id="bottomNav">
    <button class="nav-btn active" data-view="chat" onclick="switchView('chat')"><span class="ic">💬</span>Chat</button>
    <button class="nav-btn" data-view="studio" onclick="switchView('studio')"><span class="ic">🎨</span>Studio</button>
    <button class="nav-btn" data-view="files" onclick="switchView('files')"><span class="ic">📁</span>Files</button>
    <button class="nav-btn" onclick="openModal('subModal')"><span class="ic">💎</span>Premium</button>
  </div>
</div>

<!-- ============ ONBOARDING ============ -->
<div id="onboardModal">
  <div class="onboard-slides" id="onboardSlides">
    <div class="onboard-slide">
      <div class="big-emoji">✨</div>
      <h2>Welcome to Abelo AI</h2>
      <p>Your all-in-one AI assistant — chat, create images, and edit photos, all in one app. Built for Ethiopia 🇪🇹, works in English & አማርኛ.</p>
    </div>
    <div class="onboard-slide">
      <div class="big-emoji">🎨</div>
      <h2>Create stunning images</h2>
      <p>Describe anything and watch it come to life. Then remove backgrounds, upscale, and apply pro filters right on your phone.</p>
    </div>
    <div class="onboard-slide">
      <div class="big-emoji">🎤</div>
      <h2>Talk, don't type</h2>
      <p>Use voice input and let Abelo AI read replies out loud. Fast, hands-free, and simple for everyone.</p>
    </div>
  </div>
  <div class="onboard-dots" id="onboardDots"></div>
  <div class="onboard-footer">
    <button class="btn-full" onclick="closeOnboarding()">Get Started 🚀</button>
  </div>
</div>

<!-- ============ SETTINGS MODAL ============ -->
<div class="modal-bg" id="settingsModal">
  <div class="modal">
    <h2>Settings <span class="close" onclick="closeModal('settingsModal')">✕</span></h2>
    <div class="ok-note">✅ All AI keys live safely on your backend server — nothing secret is stored in this app.</div>
    <div class="field">
      <label>Backend URL (your deployed Worker)</label>
      <input type="text" id="backendUrlInput" placeholder="https://abelo-ai-backend.yourname.workers.dev">
    </div>
    <button class="btn-full" onclick="saveBackendUrl()">Save</button>
    <p style="font-size:11.5px;color:var(--text-dim);margin-top:12px;line-height:1.5">
      🔧 This is the URL of the Cloudflare Worker that holds your OpenAI / Gemini / ClipDrop / Remove.bg keys.
    </p>
  </div>
</div>

<!-- ============ THEME PICKER ============ -->
<div class="modal-bg" id="themeModal">
  <div class="modal">
    <h2>App Theme <span class="close" onclick="closeModal('themeModal')">✕</span></h2>
    <p style="font-size:12.5px;color:var(--text-dim);margin-bottom:14px">Pick an accent color. 3 exclusive gradients are unlocked with Premium 💎</p>
    <div class="theme-grid" id="themeGrid"></div>
  </div>
</div>

<!-- ============ SUBSCRIPTION / PRICING ============ -->
<div class="modal-bg" id="subModal">
  <div class="modal">
    <h2>Choose Your Plan <span class="close" onclick="closeModal('subModal')">✕</span></h2>
    <div class="price-header">
      <div class="emoji">💎</div>
      <p style="color:var(--text-dim);font-size:13px;margin-top:4px">Unlock the full power of Abelo AI</p>
    </div>
    <table class="compare-table">
      <tr><th></th><th>Free</th><th class="premium-col">Premium</th></tr>
      <tr><td>Chat messages</td><td>15 / day</td><td class="premium-col yes">Unlimited</td></tr>
      <tr><td>Image generation</td><td>3 / day</td><td class="premium-col yes">Unlimited</td></tr>
      <tr><td>Filters & resize</td><td class="yes">✓</td><td class="premium-col yes">✓</td></tr>
      <tr><td>Remove background</td><td class="no">✕</td><td class="premium-col yes">✓</td></tr>
      <tr><td>AI upscale / enhance</td><td class="no">✕</td><td class="premium-col yes">✓</td></tr>
      <tr><td>Theme colors</td><td>3 basic</td><td class="premium-col yes">All 6 themes</td></tr>
      <tr><td>Response speed</td><td>Standard</td><td class="premium-col yes">Priority</td></tr>
      <tr><td>Support</td><td>Community</td><td class="premium-col yes">Priority</td></tr>
    </table>
    <div class="upgrade-cta">
      <div style="font-size:13px;opacity:.9">Premium Plan</div>
      <div class="price-big">299 ETB<span style="font-size:13px;font-weight:400"> / month</span></div>
      <button onclick="mockUpgrade()">Upgrade Now 🚀</button>
    </div>
    <p style="font-size:10.5px;color:var(--text-dim);text-align:center;margin-top:10px">This checkout is a UI mock. Real ETB payments need Chapa / Telebirr / SantimPay verified on your backend.</p>
  </div>
</div>

<div class="modal-bg" id="adminLoginModal">
  <div class="modal">
    <h2>Owner Login <span class="close" onclick="closeModal('adminLoginModal')">✕</span></h2>
    <div class="field"><label>Admin Password</label><input type="password" id="adminPassInput" placeholder="Enter password" onkeydown="if(event.key==='Enter')checkAdminLogin()"></div>
    <button class="btn-full" onclick="checkAdminLogin()">Login</button>
  </div>
</div>

<div class="modal-bg" id="adminPanelModal">
  <div class="modal">
    <h2>👑 Owner Dashboard <span class="close" onclick="closeModal('adminPanelModal')">✕</span></h2>
    <div class="stat-row"><span>Messages Sent Today</span><b id="statMsgs">0</b></div>
    <div class="stat-row"><span>Images Generated Today</span><b id="statImgs">0</b></div>
    <div class="stat-row"><span>Images Edited (lifetime)</span><b id="statEdits">0</b></div>
    <div class="stat-row"><span>Registered Devices (mock)</span><b id="statUsers">1</b></div>
    <div class="stat-row"><span>Current Plan</span><b id="statPlan">FREE</b></div>
    <h3 style="margin:16px 0 6px;font-size:14px;">Feature Controls</h3>
    <div class="toggle-row"><span>AI Chat Enabled</span><div class="switch on" id="tgl_chat" onclick="toggleFeature('chat',this)"></div></div>
    <div class="toggle-row"><span>Image Generation Enabled</span><div class="switch on" id="tgl_gen" onclick="toggleFeature('gen',this)"></div></div>
    <div class="toggle-row"><span>Image Editing Enabled</span><div class="switch on" id="tgl_edit" onclick="toggleFeature('edit',this)"></div></div>
    <div class="toggle-row"><span>Voice Features Enabled</span><div class="switch on" id="tgl_voice" onclick="toggleFeature('voice',this)"></div></div>
    <button class="btn-full" style="margin-top:14px" onclick="forcePremium()">🎁 Grant This Device Premium</button>
    <button class="btn-full secondary" style="margin-top:8px" onclick="openModal('adminChangePassModal')">🔑 Change Admin Password</button>
    <button class="btn-full secondary" style="margin-top:8px" onclick="resetAllData()">🗑️ Reset All App Data</button>
  </div>
</div>

<div class="modal-bg" id="adminChangePassModal">
  <div class="modal">
    <h2>Change Admin Password <span class="close" onclick="closeModal('adminChangePassModal')">✕</span></h2>
    <div class="field"><label>New Password</label><input type="password" id="newAdminPass" placeholder="Minimum 6 characters"></div>
    <button class="btn-full" onclick="changeAdminPassword()">Save New Password</button>
  </div>
</div>

<div class="modal-bg" id="filePreviewModal">
  <div class="modal">
    <h2>File Preview <span class="close" onclick="closeModal('filePreviewModal')">✕</span></h2>
    <div id="filePreviewBody" style="font-size:13px;line-height:1.6;white-space:pre-wrap;word-break:break-word;"></div>
  </div>
</div>

<div class="toast" id="toast"></div>

<script>
/* ==========================================================================
   ABELO AI — SINGLE FILE PRODUCTION APP (client)
   All AI calls route through YOUR backend proxy (Cloudflare Worker).
   Settings ⚙️ → paste your Worker URL. See earlier setup notes for the
   Worker code itself (unchanged from before — no backend edits needed).
   ========================================================================== */

const DEFAULT_ADMIN_PASSWORD = "abelo2026";

const THEMES = [
  { id:'violet', name:'Violet', grad:'linear-gradient(135deg,#7c5cff,#00d9b5)', pro:false },
  { id:'sunset', name:'Sunset', grad:'linear-gradient(135deg,#ff5c8a,#ffb020)', pro:false },
  { id:'ocean',  name:'Ocean',  grad:'linear-gradient(135deg,#00c2ff,#5b3df0)', pro:false },
  { id:'gold',   name:'Gold',   grad:'linear-gradient(135deg,#f7b733,#fc4a1a)', pro:true },
  { id:'emerald',name:'Emerald',grad:'linear-gradient(135deg,#11998e,#38ef7d)', pro:true },
  { id:'rose',   name:'Rose Gold', grad:'linear-gradient(135deg,#f857a6,#ff5858)', pro:true }
];

function safeParse(key, fallback){
  try{ const raw = localStorage.getItem(key); return raw===null ? fallback : JSON.parse(raw); }
  catch(e){ console.warn('Corrupted key repaired:', key); return fallback; }
}
async function sha256(text){
  const enc = new TextEncoder().encode(text);
  const buf = await crypto.subtle.digest('SHA-256', enc);
  return Array.from(new Uint8Array(buf)).map(b=>b.toString(16).padStart(2,'0')).join('');
}

let state = {
  chats: safeParse('abelo_chats', []),
  currentChatId: null,
  backendUrl: localStorage.getItem('abelo_backend_url') || '',
  usage: safeParse('abelo_usage', {msgs:0, imgs:0, edits:0, day:null}),
  plan: localStorage.getItem('abelo_plan') || 'free',
  features: safeParse('abelo_features', {chat:true, gen:true, edit:true, voice:true}),
  files: safeParse('abelo_files', []),
  adminHash: localStorage.getItem('abelo_admin_hash') || null,
  theme: localStorage.getItem('abelo_theme') || 'violet',
  streak: safeParse('abelo_streak', {count:1, lastDay:null}),
  limits: { free: { msgs: 15, imgs: 3 } }
};
let recognition = null, isListening = false;
let currentGenImageURL = null;
let fileUploadContext = 'chat';
let sending = false;

function persist(){
  try{
    localStorage.setItem('abelo_chats', JSON.stringify(state.chats));
    localStorage.setItem('abelo_usage', JSON.stringify(state.usage));
    localStorage.setItem('abelo_plan', state.plan);
    localStorage.setItem('abelo_features', JSON.stringify(state.features));
    localStorage.setItem('abelo_files', JSON.stringify(state.files));
    localStorage.setItem('abelo_streak', JSON.stringify(state.streak));
  }catch(e){ showToast('Storage full — try deleting old files/chats', true); }
}

window.onload = async function(){
  fixViewportHeight();
  window.addEventListener('resize', fixViewportHeight);

  if(!state.adminHash){
    state.adminHash = await sha256(DEFAULT_ADMIN_PASSWORD);
    localStorage.setItem('abelo_admin_hash', state.adminHash);
  }

  checkDailyReset();
  updateStreak();
  applyTheme(state.theme);
  buildThemeGrid();
  document.getElementById('backendUrlInput').value = state.backendUrl;
  updatePlanBadge();
  renderHistoryList();
  if(state.chats.length === 0){ newChat(); } else { state.currentChatId = state.chats[0].id; renderChat(); }
  renderFiles();
  setupSpeechRecognition();
  setupScrollListener();

  if(!localStorage.getItem('abelo_onboarded')){
    document.getElementById('onboardModal').classList.add('show');
    buildOnboardDots();
  }

  if(!state.backendUrl){ showToast('Add your Backend URL in Settings ⚙️ to enable AI features', true); }
  if(location.protocol !== 'https:' && location.hostname !== 'localhost' && location.protocol !== 'file:'){
    showToast('Voice features need HTTPS to work reliably', true);
  }
};

function fixViewportHeight(){ document.documentElement.style.setProperty('--vh', (window.innerHeight * 0.01) + 'px'); }
function checkDailyReset(){
  const today = new Date().toDateString();
  if(state.usage.day !== today){ state.usage.msgs=0; state.usage.imgs=0; state.usage.day=today; persist(); }
}
function updateStreak(){
  const today = new Date().toDateString();
  if(state.streak.lastDay === today) { document.getElementById('streakNum').innerText = state.streak.count; return; }
  const yesterday = new Date(Date.now()-86400000).toDateString();
  if(state.streak.lastDay === yesterday){ state.streak.count++; } else if(state.streak.lastDay !== null){ state.streak.count = 1; }
  state.streak.lastDay = today;
  persist();
  document.getElementById('streakNum').innerText = state.streak.count;
}

/* ---------------- ONBOARDING ---------------- */
function buildOnboardDots(){
  const dots = document.getElementById('onboardDots');
  dots.innerHTML = '';
  for(let i=0;i<3;i++){ const d=document.createElement('span'); dots.appendChild(d); }
  const slides = document.getElementById('onboardSlides');
  slides.onscroll = ()=>{
    const idx = Math.round(slides.scrollLeft / slides.offsetWidth);
    [...dots.children].forEach((d,i)=> d.style.background = i===idx ? 'var(--accent)' : 'var(--bg3)');
  };
  dots.children[0].style.background = 'var(--accent)';
}
function closeOnboarding(){
  localStorage.setItem('abelo_onboarded', '1');
  document.getElementById('onboardModal').classList.remove('show');
}

/* ---------------- THEME ---------------- */
function applyTheme(id){
  const t = THEMES.find(x=>x.id===id) || THEMES[0];
  document.documentElement.style.setProperty('--grad', t.grad);
  document.documentElement.style.setProperty('--accent', t.grad.match(/#[0-9a-fA-F]{6}/)[0]);
}
function buildThemeGrid(){
  const grid = document.getElementById('themeGrid');
  grid.innerHTML = '';
  THEMES.forEach(t=>{
    const el = document.createElement('div');
    el.className = 'theme-swatch' + (state.theme===t.id ? ' selected' : '');
    el.style.background = t.grad;
    el.innerHTML = `<span>${t.name}</span>` + (t.pro && state.plan!=='premium' ? '<span class="swatch-lock">PRO</span>' : '');
    el.onclick = ()=>selectTheme(t);
    grid.appendChild(el);
  });
}
function selectTheme(t){
  if(t.pro && state.plan!=='premium'){ showToast('This theme is Premium-only 💎', true); openModal('subModal'); return; }
  state.theme = t.id;
  localStorage.setItem('abelo_theme', t.id);
  applyTheme(t.id);
  buildThemeGrid();
  showToast('Theme applied: '+t.name);
}

/* ---------------- UI NAV ---------------- */
function toggleSidebar(open){
  document.getElementById('sidebar').classList.toggle('open', open);
  document.getElementById('overlay').classList.toggle('show', open);
}
function switchView(name){
  document.querySelectorAll('.view').forEach(v=>v.classList.remove('active'));
  document.querySelectorAll('.nav-btn').forEach(b=>b.classList.remove('active'));
  const target = document.querySelector('.view[data-view="'+name+'"]');
  if(target) target.classList.add('active');
  const navBtn = document.querySelector('.nav-btn[data-view="'+name+'"]');
  if(navBtn) navBtn.classList.add('active');
  if(name==='files') renderFiles();
}
function openModal(id){
  document.getElementById(id).classList.add('show');
  if(id==='themeModal') buildThemeGrid();
}
function closeModal(id){ document.getElementById(id).classList.remove('show'); }
function showToast(msg, isError){
  const t = document.getElementById('toast');
  t.innerText = msg;
  t.classList.toggle('error', !!isError);
  t.classList.add('show');
  clearTimeout(t._timer);
  t._timer = setTimeout(()=>t.classList.remove('show'), 2600);
}
function autoGrow(el){ el.style.height='auto'; el.style.height=Math.min(el.scrollHeight,100)+'px'; }
function handleInputKey(e){ if(e.key === 'Enter' && !e.shiftKey){ e.preventDefault(); sendMessage(); } }
function quickPrompt(prefix){ const inp=document.getElementById('chatInput'); inp.value = prefix+' '; inp.focus(); }

/* ---------------- SCROLL-TO-BOTTOM ---------------- */
function setupScrollListener(){
  const win = document.getElementById('chatWindow');
  win.addEventListener('scroll', ()=>{
    const nearBottom = win.scrollHeight - win.scrollTop - win.clientHeight < 120;
    document.getElementById('scrollBottomBtn').classList.toggle('show', !nearBottom);
  });
}
function scrollChatToBottom(){
  const win = document.getElementById('chatWindow');
  win.scrollTo({top: win.scrollHeight, behavior:'smooth'});
}

/* ---------------- CHAT SYSTEM ---------------- */
function newChat(){
  const chat = { id: 'c'+Date.now(), title: 'New Chat', messages: [
    {role:'ai', text:"Hi! I'm Abelo AI ✨ I can chat, write code, and even generate images. How can I help you today? (English or አማርኛ)"}
  ]};
  state.chats.unshift(chat);
  state.currentChatId = chat.id;
  persist(); renderHistoryList(); renderChat(); toggleSidebar(false);
}
function loadChat(id){ state.currentChatId = id; renderChat(); toggleSidebar(false); }
function deleteChat(id, ev){
  ev.stopPropagation();
  state.chats = state.chats.filter(c=>c.id!==id);
  persist();
  if(state.chats.length===0) newChat(); else { state.currentChatId = state.chats[0].id; renderChat(); }
  renderHistoryList();
}
function getCurrentChat(){ return state.chats.find(c=>c.id===state.currentChatId); }

function renderHistoryList(){
  const list = document.getElementById('chatHistoryList');
  list.innerHTML = '';
  state.chats.forEach(c=>{
    const div = document.createElement('div');
    div.className = 'hist-item';
    div.onclick = ()=>loadChat(c.id);
    const nameSpan = document.createElement('span'); nameSpan.textContent = c.title;
    const delSpan = document.createElement('span'); delSpan.className='del'; delSpan.textContent='✕';
    delSpan.onclick = (ev)=>deleteChat(c.id, ev);
    div.appendChild(nameSpan); div.appendChild(delSpan);
    list.appendChild(div);
  });
}

function renderChat(){
  const chat = getCurrentChat();
  const win = document.getElementById('chatWindow');
  win.innerHTML = '';
  if(!chat) return;
  if(chat.messages.length===0){
    win.innerHTML = `<div class="empty-chat"><div class="emoji">💬</div><div>Start a conversation with Abelo AI</div></div>`;
    return;
  }
  chat.messages.forEach(m=> win.appendChild(buildMessageEl(m)) );
  win.appendChild(makeScrollBtn());
  win.scrollTop = win.scrollHeight;
}
function makeScrollBtn(){
  const btn = document.createElement('button');
  btn.id = 'scrollBottomBtn';
  btn.innerText = '⬇️';
  btn.onclick = scrollChatToBottom;
  return btn;
}

function buildMessageEl(m){
  const wrap = document.createElement('div');
  wrap.className = 'msg ' + (m.role==='user'?'user':'ai');
  const bubble = document.createElement('div');
  bubble.className = 'bubble';
  bubble.textContent = m.text;
  if(m.image){
    const img = document.createElement('img'); img.src=m.image; img.className='gen-img';
    bubble.appendChild(img);
    const actions = document.createElement('div'); actions.className='img-actions';
    const dlBtn = document.createElement('button'); dlBtn.textContent='⬇️ Download';
    dlBtn.onclick = ()=>downloadImageURL(m.image);
    actions.appendChild(dlBtn); bubble.appendChild(actions);
  }
  wrap.appendChild(bubble);

  if(m.role==='ai' && m.text){
    const actions = document.createElement('div'); actions.className='msg-actions';
    const copyBtn = document.createElement('button'); copyBtn.innerHTML='📋 Copy';
    copyBtn.onclick = ()=>{ navigator.clipboard?.writeText(m.text); showToast('Copied ✅'); };
    const speakBtn = document.createElement('button'); speakBtn.innerHTML='🔊 Listen';
    speakBtn.onclick = ()=>speak(m.text);
    actions.appendChild(copyBtn); actions.appendChild(speakBtn);
    wrap.appendChild(actions);
  }

  const meta = document.createElement('div'); meta.className='meta'; meta.textContent = m.role==='user' ? 'You' : 'Abelo AI';
  wrap.appendChild(meta);
  return wrap;
}

async function sendMessage(){
  if(sending) return;
  if(!state.features.chat){ showToast('Chat is disabled by admin', true); return; }
  if(!state.backendUrl){ showToast('Set your Backend URL in Settings ⚙️ first', true); openModal('settingsModal'); return; }
  const input = document.getElementById('chatInput');
  const text = input.value.trim();
  if(!text) return;

  checkDailyReset();
  if(state.plan==='free' && state.usage.msgs >= state.limits.free.msgs){
    showToast('Daily free limit reached. Upgrade to Premium 💎', true);
    openModal('subModal'); return;
  }

  const chat = getCurrentChat();
  chat.messages.push({role:'user', text});
  if(chat.title==='New Chat') chat.title = text.slice(0,28);
  input.value=''; autoGrow(input);
  renderChat(); showTyping();
  sending = true; document.getElementById('sendBtn').disabled = true;

  try{
    const reply = await callAI(chat.messages);
    hideTyping();
    chat.messages.push({role:'ai', text: reply});
    state.usage.msgs++; persist(); renderChat(); speak(reply);
  }catch(err){
    hideTyping();
    chat.messages.push({role:'ai', text: '⚠️ ' + err.message});
    persist(); renderChat(); showToast(err.message, true);
  }finally{
    sending = false; document.getElementById('sendBtn').disabled = false;
  }
  renderHistoryList();
}
function showTyping(){
  const win = document.getElementById('chatWindow');
  const t = document.createElement('div');
  t.className='msg ai'; t.id='typingIndicator';
  t.innerHTML = `<div class="bubble"><div class="typing"><span></span><span></span><span></span></div></div>`;
  win.appendChild(t); win.scrollTop = win.scrollHeight;
}
function hideTyping(){ const t=document.getElementById('typingIndicator'); if(t) t.remove(); }

async function callAI(history){
  const payload = {
    messages: [
      {role:'system', content:'You are Abelo AI, a helpful bilingual assistant (English + Amharic). Be concise and clear.'},
      ...history.slice(-10).map(m=>({role: m.role==='user'?'user':'assistant', content:m.text}))
    ]
  };
  let res;
  try{
    res = await fetch(state.backendUrl.replace(/\/$/,'') + '/chat', {
      method:'POST', headers:{'Content-Type':'application/json'}, body: JSON.stringify(payload)
    });
  }catch(e){ throw new Error('Could not reach your backend. Check the Backend URL and your internet connection.'); }
  const data = await res.json().catch(()=>({}));
  if(!res.ok || data.error) throw new Error(data.error || ('Backend error ('+res.status+')'));
  return data.reply;
}

/* ---------------- VOICE ---------------- */
function setupSpeechRecognition(){
  const SR = window.SpeechRecognition || window.webkitSpeechRecognition;
  if(!SR) return;
  recognition = new SR();
  recognition.continuous = false; recognition.interimResults = false; recognition.lang = 'en-US';
  recognition.onresult = (e)=>{
    const inp = document.getElementById('chatInput');
    inp.value += e.results[0][0].transcript; autoGrow(inp);
  };
  recognition.onend = ()=>{ isListening=false; document.getElementById('micBtn').classList.remove('active'); };
  recognition.onerror = (e)=>{
    isListening=false; document.getElementById('micBtn').classList.remove('active');
    const msgs = { 'not-allowed':'Microphone permission denied', 'no-speech':'No speech detected', 'network':'Voice recognition network error' };
    showToast(msgs[e.error] || ('Voice error: '+e.error), true);
  };
}
function toggleVoiceInput(){
  if(!state.features.voice){ showToast('Voice disabled by admin', true); return; }
  if(!recognition){ showToast('Voice input not supported on this browser', true); return; }
  if(isListening){ recognition.stop(); return; }
  try{ recognition.start(); isListening=true; document.getElementById('micBtn').classList.add('active'); }
  catch(e){ showToast('Could not start microphone', true); }
}
function speak(text){
  if(!state.features.voice) return;
  if(!('speechSynthesis' in window)) return;
  window.speechSynthesis.cancel();
  const utter = new SpeechSynthesisUtterance(text);
  utter.rate = 1; utter.pitch = 1;
  window.speechSynthesis.speak(utter);
}

/* ---------------- IMAGE GENERATION ---------------- */
async function generateImage(){
  if(!state.features.gen){ showToast('Image generation disabled by admin', true); return; }
  if(!state.backendUrl){ showToast('Set your Backend URL in Settings ⚙️ first', true); openModal('settingsModal'); return; }
  const promptEl = document.getElementById('imgPrompt');
  const prompt = promptEl.value.trim();
  if(!prompt){ showToast('Enter a prompt first', true); return; }

  checkDailyReset();
  if(state.plan==='free' && state.usage.imgs >= state.limits.free.imgs){
    showToast('Daily free image limit reached. Upgrade 💎', true);
    openModal('subModal'); return;
  }

  const btn = document.getElementById('genBtn');
  btn.disabled = true; showToast('Generating image...');
  try{
    const url = await callImageGenAPI(prompt);
    currentGenImageURL = url;
    document.getElementById('genResultCard').style.display='block';
    document.getElementById('genResultImg').src = url;
    state.usage.imgs++; persist();
    showToast('Image ready ✅');
  }catch(err){ showToast(err.message, true); }
  finally{ btn.disabled = false; }
}
async function callImageGenAPI(prompt){
  let res;
  try{
    res = await fetch(state.backendUrl.replace(/\/$/,'') + '/generate-image', {
      method:'POST', headers:{'Content-Type':'application/json'}, body: JSON.stringify({ prompt })
    });
  }catch(e){ throw new Error('Could not reach your backend for image generation.'); }
  const contentType = res.headers.get('Content-Type') || '';
  if(contentType.includes('application/json')){
    const data = await res.json();
    if(!res.ok || data.error) throw new Error(data.error || 'Image generation failed');
    return data.url;
  }
  if(!res.ok) throw new Error('Image generation failed ('+res.status+')');
  const blob = await res.blob();
  return URL.createObjectURL(blob);
}
function sendGenToChat(){
  if(!currentGenImageURL) return;
  const chat = getCurrentChat();
  chat.messages.push({role:'ai', text:'Here is your generated image:', image: currentGenImageURL});
  persist(); renderChat(); switchView('chat');
}
async function downloadImageURL(url){
  try{
    const res = await fetch(url); const blob = await res.blob();
    const objUrl = URL.createObjectURL(blob);
    const a = document.createElement('a'); a.href=objUrl; a.download='abelo-ai-image.png';
    document.body.appendChild(a); a.click(); a.remove();
    setTimeout(()=>URL.revokeObjectURL(objUrl), 3000);
  }catch(e){ showToast('Could not auto-download — opening image, long-press to save', true); window.open(url,'_blank'); }
}
function downloadCurrentImage(){
  const canvas = document.getElementById('editCanvas');
  if(canvas.style.display !== 'none' && canvas.width>0){
    const a = document.createElement('a'); a.href=canvas.toDataURL('image/png'); a.download='abelo-ai-edited.png';
    document.body.appendChild(a); a.click(); a.remove();
  } else if(currentGenImageURL){ downloadImageURL(currentGenImageURL); }
  else{ showToast('Nothing to download yet', true); }
}

/* ---------------- STUDIO TABS ---------------- */
function setStudioTab(tab, btn){
  document.querySelectorAll('.lang-toggle button').forEach(b=>b.classList.remove('active'));
  btn.classList.add('active');
  document.getElementById('generateTab').style.display = tab==='generate' ? 'block':'none';
  document.getElementById('editTab').style.display = tab==='edit' ? 'block':'none';
}
function updateLockTags(){
  const premium = state.plan === 'premium';
  document.getElementById('lock_removebg').style.display = premium ? 'none' : 'block';
  document.getElementById('lock_enhance').style.display = premium ? 'none' : 'block';
}

/* ---------------- IMAGE EDITING ---------------- */
function loadEditImage(ev){
  const file = ev.target.files[0]; if(!file) return;
  const reader = new FileReader();
  reader.onload = function(e){
    const img = new Image();
    img.onload = function(){
      const canvas = document.getElementById('editCanvas'); const ctx = canvas.getContext('2d');
      canvas.width = img.width; canvas.height = img.height; ctx.drawImage(img,0,0);
      canvas.style.display='block';
      document.getElementById('resizeW').value = Math.min(img.width,1200);
      document.getElementById('resizeH').value = Math.min(img.height,1200);
      document.getElementById('wLbl').innerText = document.getElementById('resizeW').value;
      document.getElementById('hLbl').innerText = document.getElementById('resizeH').value;
      showCanvasAsPreview();
    };
    img.onerror = ()=> showToast('Could not load that image file', true);
    img.src = e.target.result;
  };
  reader.readAsDataURL(file);
}
function showCanvasAsPreview(){
  const canvas = document.getElementById('editCanvas'); const preview = document.getElementById('studioPreview');
  preview.src = canvas.toDataURL('image/png'); preview.style.display='block';
}
function applyFilter(type){
  if(!state.features.edit){ showToast('Editing disabled by admin', true); return; }
  const canvas = document.getElementById('editCanvas');
  if(!canvas.width){ showToast('Upload an image first', true); return; }
  const ctx = canvas.getContext('2d');
  if(type==='grayscale' || type==='bright'){
    const imgData = ctx.getImageData(0,0,canvas.width,canvas.height); const d = imgData.data;
    if(type==='grayscale'){ for(let i=0;i<d.length;i+=4){ const avg=(d[i]+d[i+1]+d[i+2])/3; d[i]=d[i+1]=d[i+2]=avg; } }
    else { for(let i=0;i<d.length;i+=4){ d[i]=Math.min(255,d[i]*1.25); d[i+1]=Math.min(255,d[i+1]*1.25); d[i+2]=Math.min(255,d[i+2]*1.25); } }
    ctx.putImageData(imgData,0,0);
  } else if(type==='blur'){
    const tmp = document.createElement('canvas'); tmp.width=canvas.width; tmp.height=canvas.height;
    tmp.getContext('2d').drawImage(canvas,0,0);
    ctx.clearRect(0,0,canvas.width,canvas.height); ctx.filter='blur(3px)'; ctx.drawImage(tmp,0,0); ctx.filter='none';
  } else if(type==='sharpen'){ applyConvolution(ctx, canvas, [0,-1,0,-1,5,-1,0,-1,0]); }
  showCanvasAsPreview(); state.usage.edits++; persist(); showToast('Filter applied ✅');
}
function applyConvolution(ctx, canvas, weights){
  const w=canvas.width, h=canvas.height;
  const src = ctx.getImageData(0,0,w,h); const dst = ctx.createImageData(w,h);
  const side = Math.round(Math.sqrt(weights.length)); const half = Math.floor(side/2);
  const sd = src.data, dd = dst.data;
  for(let y=0;y<h;y++){ for(let x=0;x<w;x++){
    let r=0,g=0,b=0;
    for(let cy=0;cy<side;cy++){ for(let cx=0;cx<side;cx++){
      const scy = Math.min(h-1,Math.max(0,y+cy-half)); const scx = Math.min(w-1,Math.max(0,x+cx-half));
      const srcOff = (scy*w+scx)*4; const wt = weights[cy*side+cx];
      r += sd[srcOff]*wt; g += sd[srcOff+1]*wt; b += sd[srcOff+2]*wt;
    }}
    const dstOff=(y*w+x)*4;
    dd[dstOff]=Math.min(255,Math.max(0,r)); dd[dstOff+1]=Math.min(255,Math.max(0,g)); dd[dstOff+2]=Math.min(255,Math.max(0,b)); dd[dstOff+3]=sd[dstOff+3];
  }}
  ctx.putImageData(dst,0,0);
}
function resizeImage(){
  const canvas = document.getElementById('editCanvas');
  if(!canvas.width){ showToast('Upload an image first', true); return; }
  const newW = parseInt(document.getElementById('resizeW').value); const newH = parseInt(document.getElementById('resizeH').value);
  const tmp = document.createElement('canvas'); tmp.width=canvas.width; tmp.height=canvas.height;
  tmp.getContext('2d').drawImage(canvas,0,0);
  canvas.width=newW; canvas.height=newH; canvas.getContext('2d').drawImage(tmp,0,0,newW,newH);
  showCanvasAsPreview(); showToast('Resized to '+newW+'x'+newH);
}

/* ---------------- REMOVE BACKGROUND / ENHANCE ---------------- */
async function removeBackground(){
  if(!state.features.edit){ showToast('Editing disabled by admin', true); return; }
  if(state.plan !== 'premium'){ showToast('Remove Background is a Premium feature 💎', true); openModal('subModal'); return; }
  if(!state.backendUrl){ showToast('Set your Backend URL in Settings ⚙️ first', true); openModal('settingsModal'); return; }
  const canvas = document.getElementById('editCanvas');
  if(!canvas.width){ showToast('Upload an image first', true); return; }
  showToast('Removing background...');
  try{
    const blob = await new Promise(res=>canvas.toBlob(res,'image/png'));
    const fd = new FormData(); fd.append('image_file', blob, 'image.png');
    const res = await fetch(state.backendUrl.replace(/\/$/,'') + '/remove-bg', { method:'POST', body: fd });
    if(!res.ok){ const errBody = await res.json().catch(()=>({})); throw new Error(errBody.error || 'Remove background failed ('+res.status+')'); }
    const resultBlob = await res.blob();
    await drawBlobToCanvas(resultBlob, canvas);
    state.usage.edits++; persist(); showToast('Background removed ✅');
  }catch(err){ showToast(err.message, true); }
}
async function enhanceImage(){
  if(!state.features.edit){ showToast('Editing disabled by admin', true); return; }
  if(state.plan !== 'premium'){ showToast('Enhance/Upscale is a Premium feature 💎', true); openModal('subModal'); return; }
  if(!state.backendUrl){ showToast('Set your Backend URL in Settings ⚙️ first', true); openModal('settingsModal'); return; }
  const canvas = document.getElementById('editCanvas');
  if(!canvas.width){ showToast('Upload an image first', true); return; }
  showToast('Enhancing image...');
  try{
    const blob = await new Promise(res=>canvas.toBlob(res,'image/png'));
    const fd = new FormData(); fd.append('image_file', blob, 'image.png');
    fd.append('target_width', Math.min(canvas.width*2, 4000)); fd.append('target_height', Math.min(canvas.height*2, 4000));
    const res = await fetch(state.backendUrl.replace(/\/$/,'') + '/upscale', { method:'POST', body: fd });
    if(!res.ok){ const errBody = await res.json().catch(()=>({})); throw new Error(errBody.error || 'Enhance failed ('+res.status+')'); }
    const resultBlob = await res.blob();
    await drawBlobToCanvas(resultBlob, canvas);
    state.usage.edits++; persist(); showToast('Image enhanced ✅');
  }catch(err){ showToast(err.message, true); }
}
function drawBlobToCanvas(blob, canvas){
  return new Promise((resolve, reject)=>{
    const url = URL.createObjectURL(blob); const img = new Image();
    img.onload = ()=>{
      canvas.width=img.width; canvas.height=img.height; canvas.getContext('2d').drawImage(img,0,0);
      showCanvasAsPreview(); URL.revokeObjectURL(url); resolve();
    };
    img.onerror = ()=>{ URL.revokeObjectURL(url); reject(new Error('Failed to load processed image')); };
    img.src = url;
  });
}

/* ---------------- FILE SYSTEM ---------------- */
function triggerFileUpload(context){ fileUploadContext = context || 'files'; document.getElementById('hiddenFileInput').click(); }
function handleFileUpload(ev){
  const file = ev.target.files[0]; ev.target.value = ''; if(!file) return;
  if(file.size > 3*1024*1024){ showToast('File too large for local storage (max 3MB)', true); return; }
  const reader = new FileReader();
  reader.onload = function(e){
    state.files.unshift({ name:file.name, type:file.type, size:file.size, data:e.target.result, date:Date.now() });
    persist(); renderFiles(); showToast('File uploaded: '+file.name);
    if(fileUploadContext === 'chat' && file.type.startsWith('image/')){
      const chat = getCurrentChat();
      chat.messages.push({role:'user', text:'📎 Uploaded: '+file.name, image:e.target.result});
      persist(); renderChat();
    }
  };
  reader.onerror = ()=> showToast('Could not read that file', true);
  reader.readAsDataURL(file);
}
function renderFiles(){
  const list = document.getElementById('filesList'); if(!list) return;
  list.innerHTML = '';
  if(state.files.length===0){ list.innerHTML = '<div class="empty-chat" style="padding-top:40px"><div class="emoji">📁</div>No files uploaded yet</div>'; return; }
  state.files.forEach((f,i)=>{
    const div = document.createElement('div'); div.className='file-item';
    const icon = f.type.startsWith('image/') ? '🖼️' : f.type.includes('pdf') ? '📕' : '📄';
    div.innerHTML = `<span class="fic">${icon}</span>
      <div class="finfo"><div class="fname"></div><div class="fsize">${(f.size/1024).toFixed(1)} KB</div></div>
      <button data-act="preview" style="font-size:16px">👁️</button>
      <button data-act="download" style="font-size:18px">⬇️</button>`;
    div.querySelector('.fname').textContent = f.name;
    div.querySelector('[data-act="preview"]').onclick = ()=>previewFile(i);
    div.querySelector('[data-act="download"]').onclick = ()=>downloadFile(i);
    list.appendChild(div);
  });
}
function previewFile(i){
  const f = state.files[i]; const body = document.getElementById('filePreviewBody'); body.innerHTML = '';
  if(f.type.startsWith('image/')){ const img=document.createElement('img'); img.src=f.data; img.style.borderRadius='13px'; body.appendChild(img); }
  else if(f.type.startsWith('text/') || f.type === 'application/json'){
    try{ body.textContent = atob(f.data.split(',')[1]).slice(0, 5000); } catch(e){ body.textContent='Could not decode this file for preview.'; }
  } else if(f.type === 'application/pdf'){
    const iframe = document.createElement('iframe'); iframe.src=f.data; iframe.style.width='100%'; iframe.style.height='60vh'; iframe.style.border='none'; iframe.style.borderRadius='13px';
    body.appendChild(iframe);
  } else { body.textContent = 'Preview not available for this file type — use download instead.'; }
  openModal('filePreviewModal');
}
function downloadFile(i){
  const f = state.files[i]; const a = document.createElement('a'); a.href=f.data; a.download=f.name;
  document.body.appendChild(a); a.click(); a.remove();
}

/* ---------------- SETTINGS ---------------- */
function saveBackendUrl(){
  const val = document.getElementById('backendUrlInput').value.trim();
  state.backendUrl = val; localStorage.setItem('abelo_backend_url', val);
  closeModal('settingsModal'); showToast('Backend URL saved ✅');
}

/* ---------------- SUBSCRIPTION ---------------- */
function updatePlanBadge(){
  const badge = document.getElementById('planBadge');
  if(state.plan==='premium'){ badge.innerText='PREMIUM'; badge.classList.remove('free'); }
  else { badge.innerText='FREE'; badge.classList.add('free'); }
  updateLockTags();
}
function mockUpgrade(){
  // 💰 MOCK PAYMENT — replace with a real server-verified Chapa/Telebirr/SantimPay
  // checkout confirmed by YOUR backend before granting premium.
  showToast('Processing payment...');
  setTimeout(()=>{
    state.plan='premium'; persist(); updatePlanBadge();
    closeModal('subModal'); showToast('🎉 Upgraded to Premium!');
    launchConfetti();
  }, 1200);
}
function launchConfetti(){
  const colors = ['#7c5cff','#00d9b5','#ffb020','#ff5c8a'];
  for(let i=0;i<40;i++){
    const piece = document.createElement('div');
    piece.className = 'confetti-piece';
    piece.style.left = Math.random()*100 + 'vw';
    piece.style.background = colors[Math.floor(Math.random()*colors.length)];
    piece.style.animationDelay = (Math.random()*0.5)+'s';
    piece.style.transform = 'rotate('+Math.random()*360+'deg)';
    document.body.appendChild(piece);
    setTimeout(()=>piece.remove(), 3200);
  }
}

/* ---------------- ADMIN PANEL ---------------- */
function openAdminLogin(){ toggleSidebar(false); openModal('adminLoginModal'); }
async function checkAdminLogin(){
  const pass = document.getElementById('adminPassInput').value;
  const hash = await sha256(pass);
  if(hash === state.adminHash){ closeModal('adminLoginModal'); document.getElementById('adminPassInput').value=''; openAdminPanel(); }
  else{ showToast('Wrong password', true); }
}
function openAdminPanel(){
  checkDailyReset();
  document.getElementById('statMsgs').innerText = state.usage.msgs;
  document.getElementById('statImgs').innerText = state.usage.imgs;
  document.getElementById('statEdits').innerText = state.usage.edits;
  document.getElementById('statUsers').innerText = 1;
  document.getElementById('statPlan').innerText = state.plan.toUpperCase();
  ['chat','gen','edit','voice'].forEach(f=>{ document.getElementById('tgl_'+f).classList.toggle('on', state.features[f]); });
  openModal('adminPanelModal');
}
function toggleFeature(f, el){
  state.features[f] = !state.features[f]; el.classList.toggle('on', state.features[f]); persist();
  showToast((state.features[f]?'Enabled ':'Disabled ')+f);
}
function forcePremium(){ state.plan='premium'; persist(); updatePlanBadge(); showToast('This device granted Premium'); }
async function changeAdminPassword(){
  const val = document.getElementById('newAdminPass').value;
  if(val.length < 6){ showToast('Password must be at least 6 characters', true); return; }
  state.adminHash = await sha256(val); localStorage.setItem('abelo_admin_hash', state.adminHash);
  document.getElementById('newAdminPass').value=''; closeModal('adminChangePassModal'); showToast('Admin password updated ✅');
}
function resetAllData(){
  if(!confirm('This will erase all chats, files, and settings on this device. Continue?')) return;
  localStorage.clear(); location.reload();
}
</script>
</body>
</html>
