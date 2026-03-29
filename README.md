<!DOCTYPE html>
<html lang="ur" dir="rtl">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width,initial-scale=1,maximum-scale=1,user-scalable=no,viewport-fit=cover"/>
<meta name="apple-mobile-web-app-capable" content="yes"/>
<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent"/>
<meta name="apple-mobile-web-app-title" content="حوالہ تصدیق"/>
<meta name="theme-color" content="#0a0f1e"/>
<title>تھیسس حوالہ تصدیق کار</title>

<!-- Fonts -->
<link rel="preconnect" href="https://fonts.googleapis.com"/>
<link href="https://fonts.googleapis.com/css2?family=Noto+Nastaliq+Urdu:wght@400;600;700&display=swap" rel="stylesheet"/>

<style>
:root{
  --bg:#0a0f1e;
  --surface:#111827;
  --card:#1a2235;
  --card2:#1e2a3d;
  --border:#243050;
  --gold:#d4a843;
  --gold2:#f0c060;
  --teal:#0fb8a0;
  --teal2:#14d4ba;
  --red:#e05565;
  --green:#2ecc8a;
  --yellow:#f0b429;
  --text:#e8edf8;
  --muted:#6b7fa3;
  --radius:18px;
  --nav-h:72px;
  --safe-top:env(safe-area-inset-top,0px);
  --safe-bottom:env(safe-area-inset-bottom,0px);
}
*{box-sizing:border-box;margin:0;padding:0;-webkit-tap-highlight-color:transparent}
html,body{
  height:100%;width:100%;overflow:hidden;
  background:var(--bg);color:var(--text);
  font-family:'Noto Nastaliq Urdu',serif;
  direction:rtl;
}

/* ── APP SHELL ── */
#app{
  display:flex;flex-direction:column;
  height:100vh;height:100dvh;
  position:relative;overflow:hidden;
}

/* ── HEADER ── */
.header{
  flex-shrink:0;
  padding:calc(var(--safe-top) + 12px) 20px 14px;
  background:linear-gradient(160deg,#0d1730 0%,#0a1525 100%);
  border-bottom:1px solid var(--border);
  position:relative;
  z-index:10;
}
.header::after{
  content:'';position:absolute;bottom:-1px;left:0;right:0;height:1px;
  background:linear-gradient(90deg,transparent,var(--gold),transparent);
}
.header-top{display:flex;align-items:center;justify-content:space-between}
.app-title{font-size:1.25rem;font-weight:700;color:var(--gold2);letter-spacing:0.02em;line-height:1.3}
.app-sub{font-size:0.7rem;color:var(--muted);margin-top:2px}
.install-btn{
  background:linear-gradient(135deg,var(--gold),#b8902e);
  color:#0a0f1e;border:none;border-radius:12px;
  padding:8px 14px;font-size:0.72rem;font-weight:700;
  cursor:pointer;font-family:inherit;white-space:nowrap;
  box-shadow:0 4px 15px rgba(212,168,67,0.35);
}
.install-btn:active{transform:scale(0.96)}

/* ── STATUS BAR ── */
.status-bar{
  display:none;flex-shrink:0;
  padding:10px 16px;
  background:linear-gradient(90deg,#0c1628,#0f1e35);
  border-bottom:1px solid #1e3050;
  gap:10px;align-items:center;
}
.status-bar.active{display:flex}
.spin{
  width:16px;height:16px;flex-shrink:0;
  border:2px solid var(--teal);border-top-color:transparent;
  border-radius:50%;animation:spin 0.8s linear infinite;
}
@keyframes spin{to{transform:rotate(360deg)}}
.status-text{font-size:0.75rem;color:#8ab4d0;flex:1;overflow:hidden;text-overflow:ellipsis;white-space:nowrap}
.progress-wrap{display:flex;align-items:center;gap:6px;flex-shrink:0}
.progress-bar{width:60px;height:5px;background:#1e3050;border-radius:3px;overflow:hidden}
.progress-fill{height:100%;background:linear-gradient(90deg,var(--teal),var(--teal2));border-radius:3px;transition:width 0.3s}
.progress-pct{font-size:0.68rem;color:var(--muted);min-width:28px;text-align:left}

/* ── SCROLL AREA ── */
.pages{flex:1;overflow:hidden;position:relative}
.page{
  position:absolute;inset:0;
  overflow-y:auto;-webkit-overflow-scrolling:touch;
  padding:16px 16px calc(var(--nav-h) + 16px + var(--safe-bottom));
  opacity:0;pointer-events:none;transform:translateY(12px);
  transition:opacity 0.25s ease,transform 0.25s ease;
}
.page.active{opacity:1;pointer-events:auto;transform:none}

/* ── BOTTOM NAV ── */
.bottom-nav{
  flex-shrink:0;
  height:calc(var(--nav-h) + var(--safe-bottom));
  padding-bottom:var(--safe-bottom);
  background:#0c1628;
  border-top:1px solid var(--border);
  display:flex;z-index:20;
  position:relative;
}
.bottom-nav::before{
  content:'';position:absolute;top:-1px;left:0;right:0;height:1px;
  background:linear-gradient(90deg,transparent,var(--gold)40,transparent);
}
.nav-btn{
  flex:1;display:flex;flex-direction:column;align-items:center;justify-content:center;
  gap:4px;background:none;border:none;cursor:pointer;
  color:var(--muted);transition:color 0.2s;position:relative;
  font-family:inherit;
}
.nav-btn.active{color:var(--gold2)}
.nav-btn.active .nav-icon::after{
  content:'';position:absolute;bottom:-8px;left:50%;transform:translateX(-50%);
  width:4px;height:4px;border-radius:50%;background:var(--gold2);
}
.nav-icon{font-size:1.4rem;position:relative;display:flex;align-items:center;justify-content:center}
.nav-label{font-size:0.6rem;text-align:center;line-height:1}
.nav-badge{
  position:absolute;top:-4px;right:-8px;
  background:var(--teal);color:#fff;
  font-size:0.55rem;min-width:16px;height:16px;
  border-radius:8px;display:flex;align-items:center;justify-content:center;
  padding:0 4px;font-weight:700;
}

/* ── CARDS & COMPONENTS ── */
.card{
  background:var(--card);border:1px solid var(--border);
  border-radius:var(--radius);padding:16px;margin-bottom:12px;
}
.card-title{color:var(--gold);font-size:0.9rem;font-weight:600;margin-bottom:12px;display:flex;align-items:center;gap:6px}

/* Drop Zone */
.dropzone{
  border:2px dashed var(--border);border-radius:var(--radius);
  padding:32px 16px;text-align:center;cursor:pointer;
  transition:all 0.25s;background:var(--card);margin-bottom:12px;
  -webkit-user-select:none;user-select:none;
}
.dropzone:active{border-color:var(--teal);background:#0d1e2e;transform:scale(0.99)}
.dropzone.drag{border-color:var(--teal);background:#0d1e2e}
.dropzone .dz-icon{font-size:2.8rem;margin-bottom:10px;display:block}
.dropzone .dz-title{color:var(--text);font-size:1rem;font-weight:600;line-height:1.4}
.dropzone .dz-sub{color:var(--muted);font-size:0.72rem;margin-top:6px}
.dropzone.disabled{opacity:0.45;pointer-events:none}

/* Buttons */
.btn{
  width:100%;padding:16px;border:none;border-radius:14px;
  font-family:inherit;font-size:1rem;font-weight:700;cursor:pointer;
  transition:all 0.2s;margin-bottom:10px;
}
.btn:active{transform:scale(0.98)}
.btn:disabled{opacity:0.4;pointer-events:none}
.btn-primary{background:linear-gradient(135deg,#1a5f9e,#0d3a6e);color:#fff;box-shadow:0 6px 20px rgba(13,58,110,0.5)}
.btn-gold{background:linear-gradient(135deg,var(--gold),#b8902e);color:#0a0f1e;box-shadow:0 6px 20px rgba(212,168,67,0.35)}
.btn-teal{background:linear-gradient(135deg,var(--teal),#0a9a85);color:#fff;box-shadow:0 6px 20px rgba(15,184,160,0.35)}
.btn-outline{background:transparent;border:1.5px solid var(--border);color:var(--muted)}

/* Book list */
.book-item{
  background:var(--card2);border:1px solid var(--border);border-radius:12px;
  padding:12px 14px;margin-bottom:8px;display:flex;align-items:center;gap:10px;
}
.book-num{color:var(--muted);font-size:0.7rem;min-width:22px;text-align:center}
.book-info{flex:1;min-width:0}
.book-name{font-size:0.85rem;color:var(--text);white-space:nowrap;overflow:hidden;text-overflow:ellipsis}
.book-meta{font-size:0.68rem;color:var(--muted);margin-top:2px}
.book-del{background:none;border:none;color:#3a4a60;font-size:1.2rem;cursor:pointer;padding:4px;transition:color 0.2s}
.book-del:active{color:var(--red)}

/* Stats */
.stats-grid{display:grid;grid-template-columns:1fr 1fr;gap:10px;margin-bottom:12px}
.stat-card{background:var(--card2);border-radius:14px;padding:14px;text-align:center;border:1px solid var(--border)}
.stat-card.green{border-color:#1a4a35}
.stat-card.red{border-color:#4a1a25}
.stat-card.yellow{border-color:#4a3a10}
.stat-card.full{grid-column:1/-1;display:flex;align-items:center;justify-content:space-between;padding:18px 20px}
.stat-val{font-size:1.8rem;font-weight:700;line-height:1}
.stat-val.green{color:var(--green)}
.stat-val.red{color:var(--red)}
.stat-val.yellow{color:var(--yellow)}
.stat-val.white{color:var(--text)}
.stat-lbl{font-size:0.7rem;color:var(--muted);margin-top:4px}
.accuracy-ring{width:72px;height:72px;flex-shrink:0}
.accuracy-ring svg{transform:rotate(-90deg)}

/* Citation / Result cards */
.cit-card{
  background:var(--card2);border:1px solid var(--border);
  border-radius:14px;padding:14px;margin-bottom:8px;
}
.cit-card.correct{border-color:#1a4a35;background:#0d1f18}
.cit-card.incorrect{border-color:#4a1a25;background:#1f0d12}
.cit-card.not_found{border-color:#4a3a10;background:#1f1a0d}
.cit-head{display:flex;align-items:flex-start;justify-content:space-between;gap:8px;cursor:pointer}
.cit-left{display:flex;align-items:flex-start;gap:8px;flex:1;min-width:0}
.cit-icon{font-size:1.1rem;flex-shrink:0;margin-top:2px}
.cit-title{font-size:0.85rem;color:var(--text);line-height:1.4;font-weight:600}
.cit-book{font-size:0.7rem;color:var(--muted);margin-top:3px}
.cit-toggle{color:var(--muted);font-size:0.75rem;flex-shrink:0;transition:transform 0.2s}
.cit-toggle.open{transform:rotate(180deg)}
.cit-pills{display:flex;flex-wrap:wrap;gap:6px;margin-top:10px}
.pill{
  font-size:0.65rem;padding:4px 10px;border-radius:20px;
  display:flex;align-items:center;gap:4px;
}
.pill-page{background:#1a2e4a;color:#7ab3e0}
.pill-page.wrong{background:#4a1a20;color:#f08090;text-decoration:line-through}
.pill-correct{background:#1a4a30;color:#60e0a0;font-weight:700}
.pill-ed{background:#2a2015;color:#d0a840}
.pill-ed.wrong{text-decoration:line-through;background:#4a2a15;color:#f09040}
.pill-ed-ok{background:#1a4a30;color:#60e0a0;font-weight:700}
.pill-conf{
  background:#1e2840;color:var(--muted);
}
.pill-conf.high{color:var(--green)}
.pill-conf.medium{color:var(--yellow)}
.pill-conf.low{color:var(--red)}
.cit-body{margin-top:12px;padding-top:12px;border-top:1px solid var(--border);display:none}
.cit-body.open{display:block}
.cit-notes{font-size:0.78rem;color:#a0b8d0;line-height:1.7}
.cit-suggestion{
  background:#0d1c2e;border:1px solid #1a3050;border-radius:10px;
  padding:10px;margin-top:8px;font-size:0.75rem;color:#c0d8f0;line-height:1.6;
}
.cit-suggestion-lbl{font-size:0.65rem;color:var(--teal);margin-bottom:4px}
.cit-orig{font-size:0.65rem;color:var(--muted);margin-top:8px;font-style:italic;line-height:1.5}

/* Filter tabs */
.filter-bar{display:flex;gap:6px;margin-bottom:14px;overflow-x:auto;padding-bottom:4px}
.filter-bar::-webkit-scrollbar{display:none}
.filter-tab{
  flex-shrink:0;padding:6px 14px;border-radius:20px;font-size:0.72rem;font-weight:600;
  background:var(--card2);border:1px solid var(--border);color:var(--muted);cursor:pointer;
  font-family:inherit;transition:all 0.2s;
}
.filter-tab.active{background:var(--gold);border-color:var(--gold);color:#0a0f1e}

/* Alert */
.alert{
  border-radius:12px;padding:12px 14px;
  display:flex;align-items:flex-start;gap:8px;margin-bottom:12px;font-size:0.8rem;line-height:1.5;
}
.alert-warn{background:#1f1a08;border:1px solid #5a4515;color:#d4a040}
.alert-success{background:#0d1f18;border:1px solid #1a5a35;color:#40c070}
.alert-info{background:#0d1828;border:1px solid #1a3560;color:#5090d0}

/* Empty state */
.empty{text-align:center;padding:60px 20px}
.empty-icon{font-size:3.5rem;margin-bottom:14px;display:block}
.empty-title{color:var(--text);font-size:1.05rem;margin-bottom:6px}
.empty-sub{color:var(--muted);font-size:0.75rem;line-height:1.6}

/* Section header */
.sec-header{display:flex;align-items:center;justify-content:space-between;margin-bottom:10px}
.sec-title{font-size:0.85rem;color:var(--gold);font-weight:600}
.sec-count{font-size:0.72rem;color:var(--muted);background:var(--card2);padding:3px 10px;border-radius:20px;border:1px solid var(--border)}

/* Scrollbar */
::-webkit-scrollbar{width:4px}
::-webkit-scrollbar-track{background:transparent}
::-webkit-scrollbar-thumb{background:var(--border);border-radius:2px}

/* Toast */
.toast{
  position:fixed;bottom:calc(var(--nav-h) + 16px + var(--safe-bottom));
  left:16px;right:16px;z-index:999;
  background:#1e2840;border:1px solid var(--teal);border-radius:14px;
  padding:12px 16px;font-size:0.8rem;color:var(--teal2);
  transform:translateY(20px);opacity:0;
  transition:all 0.3s;pointer-events:none;text-align:center;
}
.toast.show{transform:none;opacity:1}

/* Animated gradient bg */
.page-bg{
  position:fixed;inset:0;z-index:0;pointer-events:none;
  background:radial-gradient(ellipse at 20% 20%,#0d1f3a 0%,transparent 60%),
             radial-gradient(ellipse at 80% 80%,#0a1a2e 0%,transparent 60%);
}
</style>
</head>
<body>
<div class="page-bg"></div>

<div id="app">
  <!-- HEADER -->
  <div class="header">
    <div class="header-top">
      <div>
        <div class="app-title">📜 حوالہ تصدیق کار</div>
        <div class="app-sub">Thesis Citation Verifier · AI Powered</div>
      </div>
      <button class="install-btn" id="installBtn" style="display:none" onclick="installApp()">📲 انسٹال</button>
    </div>
  </div>

  <!-- STATUS BAR -->
  <div class="status-bar" id="statusBar">
    <div class="spin"></div>
    <div class="status-text" id="statusText">لوڈ ہو رہا ہے...</div>
    <div class="progress-wrap" id="progressWrap" style="display:none">
      <div class="progress-bar"><div class="progress-fill" id="progressFill" style="width:0%"></div></div>
      <div class="progress-pct" id="progressPct">0%</div>
    </div>
  </div>

  <!-- PAGES -->
  <div class="pages">

    <!-- PAGE 0: Library -->
    <div class="page active" id="page-0">
      <div class="dropzone" id="bookDrop" onclick="document.getElementById('bookInput').click()">
        <span class="dz-icon">📚</span>
        <div class="dz-title">حوالہ جاتی کتابیں اپلوڈ کریں</div>
        <div class="dz-sub">ایک یا زیادہ PDF فائلیں منتخب کریں<br/>تقریباً 200 کتابیں قبول کی جا سکتی ہیں</div>
      </div>
      <input type="file" id="bookInput" accept=".pdf" multiple style="display:none" onchange="handleBookFiles(this.files)"/>

      <div id="bookListWrap" style="display:none">
        <div class="sec-header">
          <div class="sec-title">📖 لائبریری</div>
          <div class="sec-count" id="bookCount">0 کتابیں</div>
        </div>
        <div id="bookList"></div>
      </div>
    </div>

    <!-- PAGE 1: Thesis -->
    <div class="page" id="page-1">
      <div class="dropzone" id="thesisDrop" onclick="document.getElementById('thesisInput').click()">
        <span class="dz-icon">📄</span>
        <div class="dz-title">اپنا تھیسس اپلوڈ کریں</div>
        <div class="dz-sub">PDF فارمیٹ میں</div>
      </div>
      <input type="file" id="thesisInput" accept=".pdf" style="display:none" onchange="handleThesisFile(this.files)"/>

      <div id="thesisInfo" style="display:none">
        <div class="alert alert-success">
          <span>✅</span>
          <div>
            <div style="font-weight:600" id="thesisName">—</div>
            <div id="thesisPages" style="font-size:0.72rem;margin-top:2px"></div>
          </div>
        </div>
      </div>

      <div id="noBooksWarn" class="alert alert-warn" style="display:none">
        <span>⚠️</span>
        <span>بہتر نتائج کے لئے پہلے لائبریری میں کتابیں اپلوڈ کریں</span>
      </div>

      <button class="btn btn-gold" id="extractBtn" style="display:none" onclick="extractCitations()">
        📑 حوالہ جات نکالیں
      </button>
      <button class="btn btn-teal" id="verifyBtn" style="display:none" onclick="verifyCitations()">
        ✅ تمام حوالہ جات کی تصدیق کریں
      </button>
    </div>

    <!-- PAGE 2: Citations -->
    <div class="page" id="page-2">
      <div id="citEmpty" class="empty">
        <span class="empty-icon">🔍</span>
        <div class="empty-title">ابھی کوئی حوالہ جات نہیں</div>
        <div class="empty-sub">تھیسس اپلوڈ کریں اور<br/>"حوالہ جات نکالیں" کا بٹن دبائیں</div>
      </div>
      <div id="citWrap" style="display:none">
        <div class="sec-header">
          <div class="sec-title">🔍 ملے ہوئے حوالہ جات</div>
          <div class="sec-count" id="citCount">0</div>
        </div>
        <div id="citList"></div>
      </div>
    </div>

    <!-- PAGE 3: Results -->
    <div class="page" id="page-3">
      <div id="resEmpty" class="empty">
        <span class="empty-icon">📊</span>
        <div class="empty-title">ابھی کوئی نتائج نہیں</div>
        <div class="empty-sub">حوالہ جات نکالیں اور تصدیق کریں</div>
      </div>
      <div id="resWrap" style="display:none">
        <!-- Accuracy ring -->
        <div class="stats-grid" id="statsGrid"></div>
        <!-- Filter -->
        <div class="filter-bar" id="filterBar"></div>
        <!-- List -->
        <div id="resList"></div>
        <!-- Correction summary -->
        <div id="corrSummary" style="display:none">
          <div class="card" style="border-color:#4a1a25">
            <div class="card-title">📋 اصلاح کی ضرورت والے حوالہ جات</div>
            <div id="corrList" style="font-size:0.8rem;line-height:2"></div>
          </div>
        </div>
      </div>
    </div>

  </div><!-- /pages -->

  <!-- BOTTOM NAV -->
  <nav class="bottom-nav">
    <button class="nav-btn active" id="nav-0" onclick="switchTab(0)">
      <div class="nav-icon">📚<span class="nav-badge" id="badge-0" style="display:none">0</span></div>
      <div class="nav-label">لائبریری</div>
    </button>
    <button class="nav-btn" id="nav-1" onclick="switchTab(1)">
      <div class="nav-icon">📄<span class="nav-badge" id="badge-1" style="display:none">✓</span></div>
      <div class="nav-label">تھیسس</div>
    </button>
    <button class="nav-btn" id="nav-2" onclick="switchTab(2)">
      <div class="nav-icon">🔍<span class="nav-badge" id="badge-2" style="display:none">0</span></div>
      <div class="nav-label">حوالہ جات</div>
    </button>
    <button class="nav-btn" id="nav-3" onclick="switchTab(3)">
      <div class="nav-icon">📊<span class="nav-badge" id="badge-3" style="display:none">0</span></div>
      <div class="nav-label">نتائج</div>
    </button>
  </nav>
</div>

<div class="toast" id="toast"></div>

<!-- PDF.js -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.11.174/pdf.min.js"></script>
<script>
pdfjsLib.GlobalWorkerOptions.workerSrc =
  'https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.11.174/pdf.worker.min.js';

// ── STATE ──────────────────────────────────────────
let books = [];
let thesis = null;
let citations = [];
let results = [];
let currentTab = 0;
let busy = false;
let currentFilter = 'all';
let deferredPrompt = null;

// ── PWA INSTALL ────────────────────────────────────
window.addEventListener('beforeinstallprompt', e => {
  e.preventDefault();
  deferredPrompt = e;
  document.getElementById('installBtn').style.display = 'flex';
});
async function installApp(){
  if (!deferredPrompt) return;
  deferredPrompt.prompt();
  await deferredPrompt.userChoice;
  deferredPrompt = null;
  document.getElementById('installBtn').style.display = 'none';
}

// ── NAV ────────────────────────────────────────────
function switchTab(n){
  document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
  document.querySelectorAll('.nav-btn').forEach(b => b.classList.remove('active'));
  document.getElementById('page-' + n).classList.add('active');
  document.getElementById('nav-' + n).classList.add('active');
  currentTab = n;
}

// ── STATUS ─────────────────────────────────────────
function setStatus(msg, pct){
  const bar = document.getElementById('statusBar');
  if(!msg){ bar.classList.remove('active'); return; }
  bar.classList.add('active');
  document.getElementById('statusText').textContent = msg;
  const pw = document.getElementById('progressWrap');
  if(pct !== undefined){
    pw.style.display = 'flex';
    document.getElementById('progressFill').style.width = pct + '%';
    document.getElementById('progressPct').textContent = pct + '%';
  } else {
    pw.style.display = 'none';
  }
}
function clearStatus(){ setStatus(null); }

// ── TOAST ──────────────────────────────────────────
let toastTimer;
function showToast(msg){
  const t = document.getElementById('toast');
  t.textContent = msg;
  t.classList.add('show');
  clearTimeout(toastTimer);
  toastTimer = setTimeout(() => t.classList.remove('show'), 2800);
}

// ── PDF TEXT EXTRACT ───────────────────────────────
async function extractPages(file){
  return new Promise((res, rej) => {
    const reader = new FileReader();
    reader.onload = async e => {
      try {
        const pdf = await pdfjsLib.getDocument({ data: e.target.result }).promise;
        const pages = {};
        for(let i = 1; i <= Math.min(pdf.numPages, 600); i++){
          const page = await pdf.getPage(i);
          const content = await page.getTextContent();
          pages[i] = content.items.map(x => x.str).join(' ');
        }
        res({ pages, numPages: pdf.numPages });
      } catch(err){ rej(err); }
    };
    reader.readAsArrayBuffer(file);
  });
}

// ── CLAUDE API ─────────────────────────────────────
async function callClaude(system, user, maxT = 3000){
  const r = await fetch('https://api.anthropic.com/v1/messages', {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({
      model: 'claude-sonnet-4-20250514',
      max_tokens: maxT,
      system,
      messages: [{ role: 'user', content: user }]
    })
  });
  const d = await r.json();
  if(d.error) throw new Error(d.error.message);
  return d.content.map(c => c.text || '').join('');
}
function parseJSON(raw){
  return JSON.parse(raw.replace(/```json|```/g,'').trim());
}

// ── BOOKS ──────────────────────────────────────────
async function handleBookFiles(files){
  if(busy || !files.length) return;
  busy = true;
  disableDrops(true);
  const arr = Array.from(files);
  for(let i = 0; i < arr.length; i++){
    const f = arr[i];
    setStatus(`📖 ${f.name.slice(0,30)} (${i+1}/${arr.length})`, Math.round((i+1)/arr.length*100));
    try {
      const { pages, numPages } = await extractPages(f);
      books.push({ id: Date.now()+i, name: f.name.replace(/\.pdf$/i,''), filename: f.name, pages, numPages, sizeMB: (f.size/1048576).toFixed(2) });
    } catch(e){ console.error(f.name, e); }
  }
  busy = false;
  disableDrops(false);
  clearStatus();
  renderBooks();
  updateBadges();
  showToast(`✅ ${arr.length} کتابیں اپلوڈ ہو گئیں`);
}

function renderBooks(){
  const list = document.getElementById('bookList');
  const wrap = document.getElementById('bookListWrap');
  if(!books.length){ wrap.style.display = 'none'; return; }
  wrap.style.display = 'block';
  document.getElementById('bookCount').textContent = books.length + ' کتابیں';
  list.innerHTML = books.map((b,i) => `
    <div class="book-item">
      <div class="book-num">${i+1}</div>
      <div class="book-info">
        <div class="book-name">${esc(b.name)}</div>
        <div class="book-meta">${b.numPages} صفحات · ${b.sizeMB} MB</div>
      </div>
      <button class="book-del" onclick="delBook(${b.id})">✕</button>
    </div>`).join('');
}
function delBook(id){
  books = books.filter(b => b.id !== id);
  renderBooks();
  updateBadges();
}

// ── THESIS ─────────────────────────────────────────
async function handleThesisFile(files){
  if(busy || !files.length) return;
  busy = true;
  disableDrops(true);
  setStatus('📄 تھیسس لوڈ ہو رہا ہے...');
  try {
    const f = files[0];
    const { pages, numPages } = await extractPages(f);
    const text = Object.values(pages).join('\n\n');
    thesis = { name: f.name, text, pages, numPages };
    citations = []; results = [];
    renderThesisInfo();
    showToast('✅ تھیسس لوڈ ہو گیا');
  } catch(e){ showToast('⚠️ خطا: ' + e.message); }
  busy = false;
  disableDrops(false);
  clearStatus();
  updateBadges();
}

function renderThesisInfo(){
  if(!thesis) return;
  document.getElementById('thesisInfo').style.display = 'block';
  document.getElementById('thesisName').textContent = thesis.name;
  document.getElementById('thesisPages').textContent = thesis.numPages + ' صفحات لوڈ شدہ';
  document.getElementById('extractBtn').style.display = 'block';
  document.getElementById('noBooksWarn').style.display = books.length ? 'none' : 'flex';
  document.getElementById('verifyBtn').style.display = citations.length ? 'block' : 'none';
}

// ── EXTRACT CITATIONS ──────────────────────────────
async function extractCitations(){
  if(!thesis || busy) return;
  busy = true;
  disableDrops(true);
  citations = [];
  results = [];
  document.getElementById('verifyBtn').style.display = 'none';

  const chunkSz = 10000;
  const txt = thesis.text;
  const chunks = [];
  for(let i = 0; i < txt.length; i += chunkSz) chunks.push(txt.slice(i, i+chunkSz));

  let all = [];
  for(let i = 0; i < chunks.length; i++){
    setStatus(`🔍 حصہ ${i+1}/${chunks.length} میں حوالہ جات تلاش ہو رہے ہیں`, Math.round((i+1)/chunks.length*100));
    try {
      const raw = await callClaude(
        `You are a thesis citation extractor. Extract ALL citations, in-text references, and bibliography entries.
Return ONLY a valid JSON array. No markdown, no explanation, nothing else.
Schema: [{"bookTitle":"","author":"","page":"","edition":"","year":"","volume":"","originalText":"exact citation text","context":"brief surrounding text"}]
If nothing found, return []`,
        `Extract all citations from this text:\n\n${chunks[i]}`
      );
      const found = parseJSON(raw);
      if(Array.isArray(found)) all = [...all, ...found];
    } catch(e){ console.error('chunk', i, e); }
  }

  // Deduplicate
  const seen = new Set();
  citations = all.filter(c => {
    const k = ((c.bookTitle||'')+(c.page||'')).toLowerCase().trim();
    if(!k || seen.has(k)) return false;
    seen.add(k); return true;
  }).map((c,i) => ({ ...c, id: i+1 }));

  busy = false;
  disableDrops(false);
  clearStatus();
  renderCitations();
  renderThesisInfo();
  updateBadges();
  showToast(`✅ ${citations.length} حوالہ جات ملے`);
  switchTab(2);
}

function renderCitations(){
  const empty = document.getElementById('citEmpty');
  const wrap = document.getElementById('citWrap');
  if(!citations.length){ empty.style.display = 'block'; wrap.style.display = 'none'; return; }
  empty.style.display = 'none';
  wrap.style.display = 'block';
  document.getElementById('citCount').textContent = citations.length;
  document.getElementById('citList').innerHTML = citations.map((c,i) => `
    <div class="cit-card">
      <div class="cit-head">
        <div class="cit-left">
          <span class="cit-icon">📌</span>
          <div>
            <div class="cit-title">${esc(c.bookTitle||'عنوان نامعلوم')}</div>
            ${c.author ? `<div class="cit-book">✍️ ${esc(c.author)}</div>` : ''}
          </div>
        </div>
      </div>
      <div class="cit-pills">
        ${c.page ? `<span class="pill pill-page">📄 ص: ${esc(c.page)}</span>` : ''}
        ${c.edition ? `<span class="pill pill-ed">📗 ط: ${esc(c.edition)}</span>` : ''}
        ${c.year ? `<span class="pill pill-page">🗓 ${esc(c.year)}</span>` : ''}
      </div>
    </div>`).join('');
}

// ── VERIFY ─────────────────────────────────────────
async function verifyCitations(){
  if(!citations.length || busy) return;
  busy = true;
  disableDrops(true);
  results = [];
  switchTab(3);

  for(let i = 0; i < citations.length; i++){
    const c = citations[i];
    setStatus(`✅ تصدیق ${i+1}/${citations.length}: ${(c.bookTitle||'').slice(0,25)}`, Math.round((i+1)/citations.length*100));

    // Fuzzy match
    const q = (c.bookTitle||'').toLowerCase();
    const matched = books.find(b => {
      const bn = b.name.toLowerCase();
      const q5 = q.slice(0,6), b5 = bn.slice(0,6);
      return (q5 && bn.includes(q5)) || (b5 && q.includes(b5));
    });

    if(!matched){
      results.push({ ...c, bookFound:null, status:'not_found',
        notes:'یہ کتاب لائبریری میں نہیں ملی — براہ کرم کتاب اپلوڈ کریں' });
      renderResultsLive();
      continue;
    }

    // Page context
    const cp = parseInt(c.page)||0;
    const pCtx = {};
    if(cp > 0){
      for(let p = Math.max(1,cp-3); p <= Math.min(matched.numPages,cp+3); p++)
        if(matched.pages[p]) pCtx[p] = matched.pages[p].slice(0,500);
    } else {
      Object.keys(matched.pages).slice(0,5).forEach(p => pCtx[p] = matched.pages[p].slice(0,250));
    }

    try {
      const raw = await callClaude(
        `You are an academic citation verifier. Check if the page number and edition are correct.
Return ONLY JSON (no markdown):
{"isCorrect":true/false,"correctPage":null or number,"correctEdition":null or string,"confidence":"high/medium/low","notes":"brief explanation in Urdu (20-50 words)","suggestion":"corrected citation in Urdu if needed, else null"}`,
        `Citation: book="${matched.name}", page=${c.page||'?'}, edition=${c.edition||'?'}
Author: ${c.author||'?'}, Year: ${c.year||'?'}
Original: "${(c.originalText||'').slice(0,200)}"
Book content: ${JSON.stringify(pCtx)}`, 500
      );
      const v = parseJSON(raw);
      results.push({ ...c, bookFound:matched.name,
        status: v.isCorrect?'correct':'incorrect',
        correctPage:v.correctPage, correctEdition:v.correctEdition,
        confidence:v.confidence, notes:v.notes, suggestion:v.suggestion });
    } catch(e){
      results.push({ ...c, bookFound:matched.name, status:'error', notes:'خطا: '+e.message });
    }
    renderResultsLive();
  }

  busy = false;
  disableDrops(false);
  clearStatus();
  updateBadges();
  const acc = Math.round(results.filter(r=>r.status==='correct').length/results.length*100);
  showToast(`📊 تصدیق مکمل — درستی: ${acc}%`);
}

function renderResultsLive(){
  const empty = document.getElementById('resEmpty');
  const wrap = document.getElementById('resWrap');
  if(!results.length){ empty.style.display='block'; wrap.style.display='none'; return; }
  empty.style.display='none'; wrap.style.display='block';

  const correct = results.filter(r=>r.status==='correct').length;
  const incorrect = results.filter(r=>r.status==='incorrect').length;
  const notFound = results.filter(r=>r.status==='not_found').length;
  const total = results.length;
  const acc = total ? Math.round(correct/total*100) : 0;
  const ringColor = acc >= 80 ? '#2ecc8a' : acc >= 50 ? '#f0b429' : '#e05565';
  const dash = acc;

  document.getElementById('statsGrid').innerHTML = `
    <div class="stat-card full">
      <div>
        <div class="stat-val white" style="font-size:2.2rem">${acc}%</div>
        <div class="stat-lbl">مجموعی درستی (${total} حوالہ جات)</div>
      </div>
      <svg class="accuracy-ring" viewBox="0 0 36 36">
        <circle cx="18" cy="18" r="15.9" fill="none" stroke="#1e293b" stroke-width="3"/>
        <circle cx="18" cy="18" r="15.9" fill="none" stroke="${ringColor}" stroke-width="3"
          stroke-dasharray="${dash} ${100-dash}" stroke-linecap="round"
          style="transform:rotate(-90deg);transform-origin:50% 50%;transition:stroke-dasharray 0.5s"/>
        <text x="18" y="22" text-anchor="middle" fill="${ringColor}" font-size="8" font-weight="bold">${acc}%</text>
      </svg>
    </div>
    <div class="stat-card green"><div class="stat-val green">${correct}</div><div class="stat-lbl">درست ✅</div></div>
    <div class="stat-card red"><div class="stat-val red">${incorrect}</div><div class="stat-lbl">غلط ❌</div></div>
    <div class="stat-card yellow"><div class="stat-val yellow">${notFound}</div><div class="stat-lbl">نہیں ملی ⚠️</div></div>
    <div class="stat-card"><div class="stat-val" style="color:var(--muted)">${results.filter(r=>r.status==='error').length}</div><div class="stat-lbl">خطا 🔧</div></div>
  `;

  // Filters
  const filters = [
    ['all','تمام',total],
    ['incorrect','غلط',incorrect],
    ['correct','درست',correct],
    ['not_found','نہیں ملی',notFound],
  ];
  document.getElementById('filterBar').innerHTML = filters.map(([v,l,c]) =>
    `<button class="filter-tab${currentFilter===v?' active':''}" onclick="setFilter('${v}')">${l} (${c})</button>`
  ).join('');

  renderResultsList();

  // Correction summary
  const wrong = results.filter(r=>r.status==='incorrect');
  const cs = document.getElementById('corrSummary');
  if(wrong.length && currentFilter==='all'){
    cs.style.display='block';
    document.getElementById('corrList').innerHTML = wrong.map(r =>
      `<div>📌 <span style="color:#f08090">${esc((r.bookTitle||'').slice(0,35))}</span>
       <span style="color:var(--muted)"> — درج صفحہ: </span>
       <span style="color:#f08090;text-decoration:line-through">${esc(r.page||'—')}</span>
       ${r.correctPage ? ` <span style="color:var(--muted)">←</span> <span style="color:#60e0a0;font-weight:700">${r.correctPage}</span>` : ''}</div>`
    ).join('');
  } else { cs.style.display='none'; }
}

function setFilter(f){
  currentFilter = f;
  renderResultsLive();
}

function renderResultsList(){
  const filtered = currentFilter==='all' ? results : results.filter(r=>r.status===currentFilter);
  const icons = { correct:'✅', incorrect:'❌', not_found:'⚠️', error:'🔧' };
  const confLabel = { high:'یقینی', medium:'متوسط', low:'کم' };

  document.getElementById('resList').innerHTML = filtered.map((r,i) => `
    <div class="cit-card ${r.status}" id="rc-${i}">
      <div class="cit-head" onclick="toggleResult(${i})">
        <div class="cit-left">
          <span class="cit-icon">${icons[r.status]||'❓'}</span>
          <div>
            <div class="cit-title">${esc((r.bookTitle||'عنوان نامعلوم').slice(0,48))}</div>
            ${r.bookFound ? `<div class="cit-book">📚 ${esc(r.bookFound.slice(0,40))}</div>` : ''}
          </div>
        </div>
        <span class="cit-toggle" id="tog-${i}">▼</span>
      </div>
      <div class="cit-pills">
        ${r.page ? `<span class="pill ${r.status==='incorrect'?'pill-page wrong':'pill-page'}">📄 ص: ${esc(r.page)}</span>` : ''}
        ${r.correctPage && r.status==='incorrect' ? `<span class="pill pill-correct">✅ ص: ${r.correctPage}</span>` : ''}
        ${r.edition ? `<span class="pill ${r.correctEdition?'pill-ed wrong':'pill-ed'}">📗 ط: ${esc(r.edition)}</span>` : ''}
        ${r.correctEdition ? `<span class="pill pill-ed-ok">✅ ط: ${esc(r.correctEdition)}</span>` : ''}
        ${r.confidence ? `<span class="pill pill-conf ${r.confidence}">${confLabel[r.confidence]||r.confidence}</span>` : ''}
      </div>
      <div class="cit-body" id="cb-${i}">
        ${r.notes ? `<div class="cit-notes">${esc(r.notes)}</div>` : ''}
        ${r.suggestion ? `<div class="cit-suggestion"><div class="cit-suggestion-lbl">📝 اصلاح شدہ حوالہ:</div>${esc(r.suggestion)}</div>` : ''}
        ${r.originalText ? `<div class="cit-orig">"${esc(r.originalText.slice(0,150))}"</div>` : ''}
      </div>
    </div>`).join('');
}

function toggleResult(i){
  const body = document.getElementById('cb-'+i);
  const tog = document.getElementById('tog-'+i);
  const open = body.classList.toggle('open');
  tog.classList.toggle('open', open);
}

// ── HELPERS ────────────────────────────────────────
function esc(s){ return String(s||'').replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;').replace(/"/g,'&quot;'); }

function disableDrops(d){
  ['bookDrop','thesisDrop'].forEach(id => {
    document.getElementById(id).classList.toggle('disabled', d);
  });
  ['bookInput','thesisInput'].forEach(id => {
    document.getElementById(id).disabled = d;
  });
  document.getElementById('extractBtn').disabled = d;
  document.getElementById('verifyBtn').disabled = d;
}

function updateBadges(){
  const b0 = document.getElementById('badge-0');
  if(books.length){ b0.style.display='flex'; b0.textContent=books.length; }
  else b0.style.display='none';

  const b1 = document.getElementById('badge-1');
  if(thesis){ b1.style.display='flex'; b1.textContent='✓'; }
  else b1.style.display='none';

  const b2 = document.getElementById('badge-2');
  if(citations.length){ b2.style.display='flex'; b2.textContent=citations.length; }
  else b2.style.display='none';

  const b3 = document.getElementById('badge-3');
  if(results.length){ b3.style.display='flex'; b3.textContent=results.length; }
  else b3.style.display='none';

  if(thesis){
    document.getElementById('noBooksWarn').style.display = books.length ? 'none' : 'flex';
    document.getElementById('verifyBtn').style.display = citations.length ? 'block' : 'none';
    document.getElementById('verifyBtn').textContent = `✅ تمام حوالہ جات کی تصدیق کریں (${citations.length})`;
  }
}

// Drag & drop for book zone
const bd = document.getElementById('bookDrop');
['dragover','dragenter'].forEach(e => bd.addEventListener(e, ev => { ev.preventDefault(); bd.classList.add('drag'); }));
['dragleave','dragend'].forEach(e => bd.addEventListener(e, () => bd.classList.remove('drag')));
bd.addEventListener('drop', ev => {
  ev.preventDefault(); bd.classList.remove('drag');
  const fs = Array.from(ev.dataTransfer.files).filter(f => f.name.toLowerCase().endsWith('.pdf'));
  if(fs.length) handleBookFiles(fs);
});

const td = document.getElementById('thesisDrop');
td.addEventListener('dragover', e => { e.preventDefault(); td.classList.add('drag'); });
td.addEventListener('dragleave', () => td.classList.remove('drag'));
td.addEventListener('drop', ev => {
  ev.preventDefault(); td.classList.remove('drag');
  const fs = Array.from(ev.dataTransfer.files).filter(f => f.name.toLowerCase().endsWith('.pdf'));
  if(fs.length) handleThesisFile(fs);
});
</script>
</body>
</html>
