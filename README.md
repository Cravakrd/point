<!DOCTYPE html>
<html lang="ckb" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1, user-scalable=no">
<title>CRAVA | کرافا</title>

<!-- Firebase SDKs -->
<script src="https://www.gstatic.com/firebasejs/10.8.0/firebase-app-compat.js"></script>
<script src="https://www.gstatic.com/firebasejs/10.8.0/firebase-database-compat.js"></script>

<style>
:root{
  --green:#1f6b3a;
  --green-light:#2e8b4f;
  --green-glow: rgba(46,139,79,0.55);
  --yellow:#f5a623;
  --yellow-2:#ffc531;
  --yellow-glow: rgba(255,197,49,0.55);
  --charcoal:#0d1210;
  --charcoal-2:#151b18;
  --charcoal-3:#1c2420;
  --card:#161d19;
  --text:#eef4ef;
  --text-dim:#9fb0a5;
  --danger:#e2544a;
  --radius:20px;
  --safe-b: env(safe-area-inset-bottom, 0px);
}

*{box-sizing:border-box; -webkit-tap-highlight-color:transparent;}
html,body{margin:0;padding:0;}
body{
  background:
    radial-gradient(circle at 15% 0%, rgba(46,139,79,0.18), transparent 55%),
    radial-gradient(circle at 85% 10%, rgba(255,197,49,0.10), transparent 45%),
    var(--charcoal);
  color:var(--text);
  font-family:'Segoe UI', Tahoma, 'Noto Sans Arabic', sans-serif;
  min-height:100vh;
  overflow-x:hidden;
  padding-bottom: calc(84px + var(--safe-b));
}

::selection{background:var(--yellow); color:#111;}
button{font-family:inherit;}
::-webkit-scrollbar{width:6px;}
::-webkit-scrollbar-thumb{background:var(--green-light); border-radius:10px;}

header.topbar{
  position:sticky; top:0; z-index:50;
  display:flex; align-items:center; justify-content:space-between;
  padding:12px 16px;
  background:linear-gradient(180deg, rgba(13,18,16,0.97), rgba(13,18,16,0.86));
  backdrop-filter:blur(10px);
  border-bottom:1px solid rgba(255,197,49,0.15);
  box-shadow:0 8px 24px rgba(0,0,0,0.45);
}
.brand{display:flex; align-items:center; gap:10px;}
.brand img{
  height:42px; width:auto; object-fit:contain;
  filter:drop-shadow(0 0 10px rgba(255,197,49,0.35)) drop-shadow(0 0 18px rgba(46,139,79,0.25));
}
.brand-sub{ font-size:10px; color:var(--text-dim); letter-spacing:1px; margin-top:2px; }
.points-pill{
  display:flex; align-items:center; gap:6px;
  background:linear-gradient(145deg, #1a231d, #10160f);
  border:1px solid rgba(255,197,49,0.35);
  padding:8px 14px; border-radius:30px;
  box-shadow: inset 0 1px 0 rgba(255,255,255,0.05), 0 4px 14px rgba(0,0,0,0.5), 0 0 14px var(--yellow-glow);
  font-weight:700; font-size:13px; color:var(--yellow-2);
}
.points-pill svg{width:16px; height:16px;}

main{max-width:520px; margin:0 auto; padding:18px 16px 8px;}
.hero{
  position:relative; border-radius: var(--radius); padding:26px 20px; margin-bottom:20px;
  background: linear-gradient(135deg, rgba(46,139,79,0.25), rgba(255,197,49,0.06) 60%), linear-gradient(160deg, var(--charcoal-3), var(--charcoal-2));
  border:1px solid rgba(255,197,49,0.18);
  box-shadow: 0 16px 40px rgba(0,0,0,0.55), inset 0 1px 0 rgba(255,255,255,0.04);
  overflow:hidden; text-align:center;
}
.hero h1{
  position:relative; margin:0 0 6px; font-size:26px; letter-spacing:.5px;
  background:linear-gradient(90deg, var(--yellow-2), #ffe08a, var(--yellow-2));
  -webkit-background-clip:text; background-clip:text; color:transparent;
}
.hero p{position:relative; margin:0; color:var(--text-dim); font-size:13.5px; line-height:1.7;}

.card{
  position:relative; background:linear-gradient(160deg, var(--charcoal-3), var(--card));
  border-radius:var(--radius); padding:18px; margin-bottom:16px;
  border:1px solid rgba(255,255,255,0.06);
  box-shadow: 0 1px 0 rgba(255,255,255,0.06) inset, 0 14px 30px rgba(0,0,0,0.55), 0 2px 0 rgba(0,0,0,0.6);
}
.card-title{
  display:flex; align-items:center; gap:8px; font-size:15px; font-weight:800; margin:0 0 4px; color:var(--text);
}
.card-title .dot{
  width:8px; height:8px; border-radius:50%; background:var(--yellow); box-shadow:0 0 10px var(--yellow);
}
.card-sub{color:var(--text-dim); font-size:12.5px; margin:0 0 14px; line-height:1.6;}

.field{
  width:100%; padding:14px 16px; border-radius:14px;
  background:#0f1512; border:1px solid rgba(255,255,255,0.08);
  color:var(--text); font-size:15px; outline:none;
  box-shadow: inset 0 2px 6px rgba(0,0,0,0.5);
}
.field:focus{ border-color:var(--yellow); box-shadow:inset 0 2px 6px rgba(0,0,0,0.5), 0 0 0 3px rgba(255,197,49,0.18);}
.field::placeholder{color:#5f6d64;}

.btn{
  width:100%; border:none; cursor:pointer;
  padding:14px 18px; border-radius:14px; font-weight:800; font-size:15px;
  transition: transform .15s ease, filter .2s ease;
}
.btn:active{ transform:translateY(2px) scale(.985); }
.btn-primary{
  color:#0c1310; background:linear-gradient(145deg, var(--yellow-2), var(--yellow));
  box-shadow: 0 10px 22px rgba(255,166,35,0.35);
}
.btn-green{
  color:#eafff0; background:linear-gradient(145deg, var(--green-light), var(--green));
  box-shadow: 0 10px 22px rgba(31,107,58,0.45);
}
.btn-danger{
  color:#fff; background:linear-gradient(145deg, #e2544a, #b33930);
  padding:8px 12px; font-size:12px; border-radius:10px; width:auto;
}
.msg{
  margin-top:10px; font-size:13px; padding:10px 12px; border-radius:10px; border:1px solid transparent; display:none;
}
.msg.show{display:block;}
.msg.ok{ background:rgba(46,139,79,0.15); color:#8de5a8; border-color:rgba(46,139,79,0.4);}
.msg.err{ background:rgba(226,84,74,0.14); color:#ff9d94; border-color:rgba(226,84,74,0.4);}

.userbar{ display:flex; align-items:center; justify-content:space-between; gap:10px; margin-bottom:16px; }
.userchip{
  display:flex; align-items:center; gap:10px; background:linear-gradient(145deg, var(--charcoal-3), var(--card));
  border:1px solid rgba(255,255,255,0.07); border-radius:16px; padding:10px 14px; flex:1;
}
.avatar{
  width:38px; height:38px; border-radius:50%; display:flex; align-items:center; justify-content:center;
  font-weight:800; font-size:15px; color:#0c1310; background:linear-gradient(145deg, var(--yellow-2), var(--green-light));
}
.userchip .uname{font-weight:700; font-size:14px;}
.userchip .upts{font-size:11.5px; color:var(--text-dim);}
.logout-btn{
  background:none; border:1px solid rgba(226,84,74,0.4); color:#ff9d94;
  border-radius:12px; padding:9px 12px; font-size:12px; font-weight:700; cursor:pointer;
}

.wheel-wrap{
  position:relative; width:min(78vw, 300px); aspect-ratio:1/1; margin:6px auto 18px;
  filter: drop-shadow(0 18px 30px rgba(0,0,0,0.6));
}
.pointer{
  position:absolute; top:-14px; left:50%; transform:translateX(-50%);
  width:0; height:0; z-index:5;
  border-left:14px solid transparent; border-right:14px solid transparent;
  border-top:24px solid var(--yellow-2);
}
.wheel-ring{
  position:absolute; inset:-8px; border-radius:50%;
  background:conic-gradient(var(--yellow-2), var(--green-light), var(--yellow-2), var(--green-light), var(--yellow-2), var(--green-light), var(--yellow-2));
}
.wheel{
  position:absolute; inset:6px; border-radius:50%; overflow:hidden; border:4px solid #0c110d;
  transition: transform 4.2s cubic-bezier(.14,.85,.15,1);
}
.wheel-label {
  position: absolute; top: 50%; left: 50%; width: 95px; text-align: center; font-size: 13px; font-weight: 800; z-index: 10;
}
.wheel-hub{
  position:absolute; top:50%; left:50%; transform:translate(-50%,-50%);
  width:22%; height:22%; border-radius:50%; z-index:4;
  background:radial-gradient(circle at 35% 30%, #ffe08a, var(--yellow) 60%, #c97e00 100%);
  display:flex; align-items:center; justify-content:center;
}
.wheel-hub span{font-size:16px;}
.spin-hint{ text-align:center; color:var(--text-dim); font-size:12.5px; margin-bottom:10px; }

.lb-row{
  display:flex; align-items:center; gap:10px; padding:11px 10px; border-radius:14px;
  background:rgba(255,255,255,0.02); margin-bottom:8px; border:1px solid rgba(255,255,255,0.04);
}
.lb-rank{
  width:30px; height:30px; border-radius:10px; flex:none; display:flex; align-items:center; justify-content:center;
  font-weight:800; font-size:13px; color:var(--text-dim); background:rgba(255,255,255,0.04);
}
.lb-row.gold .lb-rank{ background:linear-gradient(145deg,#ffe08a,#d69b1f); color:#3a2a00;}
.lb-row.silver .lb-rank{ background:linear-gradient(145deg,#eef3f1,#a9b4b0); color:#22302a;}
.lb-row.bronze .lb-rank{ background:linear-gradient(145deg,#e0a066,#8a5427); color:#301c07;}
.lb-name{flex:1; font-size:13.5px; font-weight:700; overflow:hidden; text-overflow:ellipsis; white-space:nowrap;}
.lb-pts{font-size:13px; font-weight:800; color:var(--yellow-2); margin-left:6px;}
.lb-empty{ text-align:center; color:var(--text-dim); font-size:13px; padding:20px 0;}

nav.tabbar{
  position:fixed; bottom:0; left:0; right:0; z-index:60;
  display:flex; justify-content:space-around; padding:9px 8px calc(9px + var(--safe-b));
  background:linear-gradient(0deg, rgba(9,13,11,0.98), rgba(13,18,16,0.9));
  border-top:1px solid rgba(255,197,49,0.15); backdrop-filter:blur(10px);
}
.tab-btn{
  background:none; border:none; color:var(--text-dim);
  display:flex; flex-direction:column; align-items:center; gap:3px;
  font-size:10.5px; font-weight:700; padding:6px 14px; border-radius:12px; cursor:pointer;
}
.tab-btn svg{width:21px; height:21px;}
.tab-btn.active{ color:var(--yellow-2); }

.section{display:none;}
.section.active{display:block; animation:fadeUp .35s ease;}
@keyframes fadeUp{ from{opacity:0; transform:translateY(8px);} to{opacity:1; transform:translateY(0);} }
.codes-note{ font-size:11px; color:var(--text-dim); margin-top:10px; line-height:1.7; }

.result-overlay{
  position:fixed; inset:0; z-index:100; display:none; align-items:center; justify-content:center;
  background:rgba(6,9,7,0.75); backdrop-filter:blur(4px); padding:20px;
}
.result-overlay.show{ display:flex; }
.result-card{
  width:100%; max-width:340px; text-align:center; background:linear-gradient(160deg, var(--charcoal-3), var(--card));
  border:1px solid rgba(255,197,49,0.35); border-radius:22px; padding:30px 24px 26px;
}
.result-emoji{ font-size:46px; margin-bottom:6px; }
.result-title{ font-size:19px; font-weight:800; margin:0 0 6px; color:var(--yellow-2); }
.result-sub{ font-size:13px; color:var(--text-dim); margin:0 0 18px; }

.admin-trigger {
  text-align: center; margin-top: 30px; font-size: 11px; color: var(--text-dim); cursor: pointer; opacity: 0.5;
}
.admin-trigger:hover { opacity: 1; color: var(--yellow); }
</style>
</head>
<body>

<header class="topbar">
  <div class="brand">
    <img src="crlogo.png" alt="CRAVA logo" onerror="this.style.display='none'">
    <div><div class="brand-sub">سۆران · فرێش جوس و فرایز</div></div>
  </div>
  <div class="points-pill" id="headerPoints">
    <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.4"><path d="M12 2l2.6 6.6L22 9.2l-5.4 4.6L18.2 21 12 17l-6.2 4 1.6-7.2L2 9.2l7.4-.6z"/></svg>
    <span id="headerPointsVal">0</span>
  </div>
</header>

<main>
  <!-- AUTH -->
  <section class="section" id="section-auth">
    <div class="hero">
      <h1>بەخێربێیت بۆ CRAVA</h1>
      <p>ناوت و پاسوۆردەکەت بنووسە بۆ چوونەژوورەوە یان دروستکردنی هەژماری نوێ.</p>
    </div>
    <div class="card">
      <h3 class="card-title"><span class="dot"></span> چوونەژوورەوە / تۆمارکردن</h3>
      <p class="card-sub">ئەگەر ناوت هەبێت پاسوۆردەکەی دەنوسیت، ئەگەر نوێش بێت پاسوۆردێکی نوێ دادەنێیت.</p>
      <input id="nameInput" class="field" type="text" placeholder="ناو یان @یوزەری ئینستاگرام" maxlength="30" style="margin-bottom:10px;">
      <input id="passInput" class="field" type="password" placeholder="پاسوۆرد" maxlength="30">
      <div style="height:12px"></div>
      <button class="btn btn-primary" id="loginBtn">چوونەژوورەوە</button>
      <div class="msg" id="authMsg"></div>
    </div>
  </section>

  <!-- HOME -->
  <section class="section" id="section-home">
    <div class="userbar">
      <div class="userchip">
        <div class="avatar" id="avatarLetter">C</div>
        <div>
          <div class="uname" id="homeUserName">-</div>
          <div class="upts"><span id="homeUserPts">0</span> خاڵ</div>
        </div>
      </div>
      <button class="logout-btn" id="logoutBtn">دەرچوون</button>
    </div>
    <div class="hero" style="padding:22px 18px;">
      <h1 style="font-size:20px;">کۆدی وەصڵ داخڵ بکە</h1>
      <p>پاش کڕینت، کۆدی سەر وەصڵەکەت بنووسە بۆ بەدەستهێنانی خاڵ و کردنەوەی چەرخی خۆشییەکان 🎡</p>
    </div>
    <div class="card">
      <h3 class="card-title"><span class="dot"></span> بەکارهێنانی کۆد</h3>
      <p class="card-sub">نموونە: CRAVA-2026-A1 — هەر کۆدێک تەنها یەک جار بەکاردێت.</p>
      <input id="codeInput" class="field" type="text" placeholder="CRAVA-2026-XX" style="text-transform:uppercase;">
      <div style="height:12px"></div>
      <button class="btn btn-green" id="redeemBtn">پشکنین و وەرگرتنی خاڵ</button>
      <div class="msg" id="codeMsg"></div>
      <div class="codes-note">هەر کۆدێکی دروست ١٠٠ خاڵت پێدەدات و یەک جەخماوی چەرخی خۆشییەکانت بۆ دەکاتەوە.</div>
    </div>
  </section>

  <!-- WHEEL -->
  <section class="section" id="section-wheel">
    <div class="card" style="text-align:center;">
      <h3 class="card-title" style="justify-content:center;"><span class="dot"></span> چەرخی خۆشییەکانی CRAVA</h3>
      <p class="card-sub" id="wheelInfo">بۆ خستنەکار، سەرەتا کۆدی وەصڵێکی دروست بنووسە.</p>
      <div class="wheel-wrap">
        <div class="pointer"></div>
        <div class="wheel-ring"></div>
        <div class="wheel" id="wheelEl"></div>
        <div class="wheel-hub"><span>🍟</span></div>
      </div>
      <div class="spin-hint" id="spinCount">جەخماوی بەردەست: <b id="spinsLeft">0</b></div>
      <button class="btn btn-primary" id="spinBtn" disabled>🎡 سوڕاندنی چەرخ</button>
    </div>
  </section>

  <!-- LEADERBOARD -->
  <section class="section" id="section-leaderboard">
    <div class="card">
      <h3 class="card-title"><span class="dot"></span> پێشەنگەکان</h3>
      <p class="card-sub">لیستی خاڵترین بەکارهێنەرانی CRAVA — بە شێوەی ڕاستەوخۆ نوێ دەبێتەوە.</p>
      <div id="leaderboardList"></div>
    </div>
    <div class="admin-trigger" id="openAdminBtn">🔐 بەڕێوەبەر (Admin)</div>
  </section>

  <!-- ADMIN SECTION -->
  <section class="section" id="section-admin">
    <div class="card">
      <h3 class="card-title"><span class="dot"></span> بەڕێوەبردنی بەکارهێنەران</h3>
      <p class="card-sub">لێرەدا دەتوانیت هەر بەکارهێنەرێک کە بتهەوێت بیسڕیتەوە.</p>
      <div id="adminList"></div>
    </div>

    <div class="card">
      <h3 class="card-title"><span class="dot"></span> مێژووی بردنەوەکانی چەرخ (Spin History)</h3>
      <p class="card-sub">بینینی ئەوەی کێ چەرخەکەی سووڕاندووە و چی بۆ دەرچووە:</p>
      <div id="adminSpinHistory"></div>
    </div>

    <div style="height:10px"></div>
    <button class="btn btn-primary" id="backToAppBtn">گەڕانەوە بۆ سایتەکە</button>
  </section>
</main>

<nav class="tabbar" id="tabbar" style="display:none;">
  <button class="tab-btn active" data-tab="home">
    <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M3 11l9-8 9 8"/><path d="M5 10v10h14V10"/></svg>
    سەرەکی
  </button>
  <button class="tab-btn" data-tab="wheel">
    <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><circle cx="12" cy="12" r="9"/><path d="M12 3v9l6 3"/></svg>
    چەرخ
  </button>
  <button class="tab-btn" data-tab="leaderboard">
    <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M8 21V10M16 21V4M4 21v-6"/></svg>
    پێشەنگ
  </button>
</nav>

<div class="result-overlay" id="resultOverlay">
  <div class="result-card">
    <div class="result-emoji" id="resultEmoji">🎉</div>
    <h3 class="result-title" id="resultTitle">پیرۆزە!</h3>
    <p class="result-sub" id="resultSub">تۆ براوەی خاڵ بوویت</p>
    <button class="btn btn-primary" id="resultCloseBtn">باشە</button>
  </div>
</div>

<script>
(function(){
  "use strict";
  const firebaseConfig = {
    apiKey: "AIzaSyC_6pie74vrvFIYJDT0QOaQeLaZO8fSWOo",
    authDomain: "crava-65b13.firebaseapp.com",
    databaseURL: "https://crava-65b13-default-rtdb.firebaseio.com",
    projectId: "crava-65b13",
    storageBucket: "crava-65b13.firebasestorage.app",
    messagingSenderId: "697423980333",
    appId: "1:697423980333:web:16b446f8e69e94c2bf95a4"
  };

  firebase.initializeApp(firebaseConfig);
  const db = firebase.database();

  var VALID_CODES = ["CRAVA-2026-A1","CRAVA-2026-B2","CRAVA-2026-C3","CRAVA-2026-D4","CRAVA-2026-E5",
                      "CRAVA-2026-F6","CRAVA-2026-G7","CRAVA-2026-H8","CRAVA-2026-I9","CRAVA-2026-J10"];
  var CODE_REWARD_POINTS = 100;
  var STARTING_POINTS = 10;
  var SESSION_KEY = "crava_session_v1";

  var WHEEL_SEGMENTS = [
    { label:"دووبارە هەوڵبدەوە", type:"none",   points:0,   weight:48 }, 
    { label:"+٥٠ خاڵ",         type:"points", points:50,  weight:48 },
    { label:"فرایزی خۆڕایی",   type:"fries",  points:0,   weight:1  }, 
    { label:"+١٠٠ خاڵ",        type:"points", points:100, weight:2  },
    { label:"جوسی خۆڕایی",     type:"juice",  points:0,   weight:0.5 }, 
    { label:"+٢٥٠ خاڵ",        type:"points", points:250, weight:0.5 } 
  ];
  var SEG_COUNT = WHEEL_SEGMENTS.length;
  var SEG_ANGLE = 360 / SEG_COUNT;
  var SEG_COLORS_CSS = ["#f5a623","#1f6b3a","#ffc531","#2e8b4f","#e0a066","#175c30"];

  function normalizeName(n){ return n.trim().replace(/^@+/,"").toLowerCase(); }
  var currentUser = null;

  var el = {
    authSection: document.getElementById("section-auth"),
    homeSection: document.getElementById("section-home"),
    wheelSection: document.getElementById("section-wheel"),
    lbSection: document.getElementById("section-leaderboard"),
    adminSection: document.getElementById("section-admin"),
    tabbar: document.getElementById("tabbar"),
    nameInput: document.getElementById("nameInput"),
    passInput: document.getElementById("passInput"),
    loginBtn: document.getElementById("loginBtn"),
    authMsg: document.getElementById("authMsg"),
    headerPointsVal: document.getElementById("headerPointsVal"),
    homeUserName: document.getElementById("homeUserName"),
    homeUserPts: document.getElementById("homeUserPts"),
    avatarLetter: document.getElementById("avatarLetter"),
    logoutBtn: document.getElementById("logoutBtn"),
    codeInput: document.getElementById("codeInput"),
    redeemBtn: document.getElementById("redeemBtn"),
    codeMsg: document.getElementById("codeMsg"),
    wheelEl: document.getElementById("wheelEl"),
    spinBtn: document.getElementById("spinBtn"),
    spinsLeft: document.getElementById("spinsLeft"),
    wheelInfo: document.getElementById("wheelInfo"),
    leaderboardList: document.getElementById("leaderboardList"),
    adminList: document.getElementById("adminList"),
    adminSpinHistory: document.getElementById("adminSpinHistory"),
    openAdminBtn: document.getElementById("openAdminBtn"),
    backToAppBtn: document.getElementById("backToAppBtn"),
    resultOverlay: document.getElementById("resultOverlay"),
    resultEmoji: document.getElementById("resultEmoji"),
    resultTitle: document.getElementById("resultTitle"),
    resultSub: document.getElementById("resultSub"),
    resultCloseBtn: document.getElementById("resultCloseBtn")
  };

  function buildWheel(){
    el.wheelEl.innerHTML = "";
    var colors = [];
    for(var i=0; i<SEG_COUNT; i++){
      var seg = WHEEL_SEGMENTS[i];
      var startAngle = i * SEG_ANGLE;
      var endAngle = (i + 1) * SEG_ANGLE;
      colors.push(SEG_COLORS_CSS[i % SEG_COLORS_CSS.length] + " " + startAngle + "deg " + endAngle + "deg");

      var labelDiv = document.createElement("div");
      labelDiv.className = "wheel-label";
      var midAngle = startAngle + (SEG_ANGLE / 2);
      labelDiv.style.transform = "translate(-50%, -50%) rotate(" + midAngle + "deg) translateY(-85px) rotate(90deg)";
      labelDiv.style.color = (i % 2 === 1) ? "#f3f7f4" : "#12160f";
      labelDiv.textContent = seg.label;
      el.wheelEl.appendChild(labelDiv);
    }
    el.wheelEl.style.background = "conic-gradient(from 0deg, " + colors.join(", ") + ")";
  }

  function goSection(name){
    [el.authSection, el.homeSection, el.wheelSection, el.lbSection, el.adminSection].forEach(function(s){ s.classList.remove("active"); });
    if(name === "auth"){ el.authSection.classList.add("active"); el.tabbar.style.display="none"; }
    if(name === "home"){ el.homeSection.classList.add("active"); el.tabbar.style.display="flex"; setActiveTab("home"); }
    if(name === "wheel"){ el.wheelSection.classList.add("active"); el.tabbar.style.display="flex"; setActiveTab("wheel"); }
    if(name === "leaderboard"){ el.lbSection.classList.add("active"); el.tabbar.style.display="flex"; setActiveTab("leaderboard"); }
    if(name === "admin"){ el.adminSection.classList.add("active"); el.tabbar.style.display="none"; }
  }

  function setActiveTab(name){
    document.querySelectorAll(".tab-btn").forEach(function(b){
      b.classList.toggle("active", b.getAttribute("data-tab") === name);
    });
  }

  function showMsg(node, text, ok){
    node.textContent = text;
    node.classList.remove("ok","err");
    node.classList.add(ok ? "ok" : "err", "show");
  }

  function refreshUserUI(){
    if(!currentUser) return;
    el.headerPointsVal.textContent = currentUser.points;
    el.homeUserName.textContent = currentUser.name;
    el.homeUserPts.textContent = currentUser.points;
    el.avatarLetter.textContent = currentUser.name.charAt(0).toUpperCase();
    el.spinsLeft.textContent = currentUser.spins;
    el.spinBtn.disabled = currentUser.spins <= 0;
    el.wheelInfo.textContent = currentUser.spins > 0
      ? "چەرخ ئامادەیە! دوگمەی سوڕاندن دابگرە."
      : "بۆ خستنەکار، سەرەتا کۆدی وەصڵێکی دروست بنووسە.";
  }

  el.loginBtn.addEventListener("click", function(){
    var raw = el.nameInput.value || "";
    var name = raw.trim();
    var pass = (el.passInput.value || "").trim();

    if(name.length < 2){ showMsg(el.authMsg, "تکایە ناوێکی گونجاو بنووسە (لانیکەم ٢ پیت).", false); return; }
    if(pass.length < 3){ showMsg(el.authMsg, "تکایە پاسوۆردێک بنووسە (لانیکەم ٣ پیت).", false); return; }
    
    el.loginBtn.disabled = true;
    el.loginBtn.textContent = "چاوەڕێبە...";
    var key = normalizeName(name);

    db.ref('users/' + key).once('value').then(function(snapshot) {
      if(snapshot.exists()) {
        var userData = snapshot.val();
        
        // ئەگەر پاسوۆرد لە داتابەیسدا هەبوو و هی ئێستا جیاواز بوو
        if(userData.pass && userData.pass !== pass) {
          showMsg(el.authMsg, "پاسوۆردەکە هەڵەیە! تکایە دڵنیابەوە.", false);
          el.loginBtn.disabled = false;
          el.loginBtn.textContent = "چوونەژوورەوە";
          return; // لێرەدا دەوەستێت و ڕێگە نادات بچێتە ژوورەوە
        }

        // ئەگەر هەژمارەکە کۆن بوو و پاسوۆردی نەبوو، ئەم پاسوۆردە نوێیەی بۆ تۆمار دەکات
        if(!userData.pass) {
          userData.pass = pass;
          db.ref('users/' + key).update({ pass: pass });
        }

        currentUser = userData;
        currentUser.key = key;
        showMsg(el.authMsg, "بەخێربێیتەوە " + currentUser.name + "!", true);
      } else {
        // ئەگەر ناوەکە بوونی نەبوو، یەکێکی نوێ دروست دەکات
        currentUser = { name: name, pass: pass, points: STARTING_POINTS, spins: 0 };
        db.ref('users/' + key).set(currentUser);
        currentUser.key = key;
        showMsg(el.authMsg, "هەژمارت دروستکرا! " + STARTING_POINTS + " خاڵی سەرەتایی وەرگیرا 🎉", true);
      }
      localStorage.setItem(SESSION_KEY, key);
      setTimeout(function(){
        refreshUserUI();
        goSection("home");
        el.loginBtn.disabled = false;
        el.loginBtn.textContent = "چوونەژوورەوە";
      }, 800);
    }).catch(function(){
      showMsg(el.authMsg, "هەڵەیەک ڕوویدا لە پەیوەندیکردن.", false);
      el.loginBtn.disabled = false;
      el.loginBtn.textContent = "چوونەژوورەوە";
    });
  });

  el.logoutBtn.addEventListener("click", function(){
    localStorage.removeItem(SESSION_KEY);
    currentUser = null;
    el.nameInput.value = "";
    el.passInput.value = "";
    el.authMsg.classList.remove("show");
    goSection("auth");
  });

  el.redeemBtn.addEventListener("click", function(){
    if(!currentUser) return;
    var code = (el.codeInput.value || "").trim().toUpperCase();
    if(!code){ showMsg(el.codeMsg, "تکایە کۆدەکە بنووسە.", false); return; }
    if(VALID_CODES.indexOf(code) === -1){ showMsg(el.codeMsg, "ئەم کۆدە نادروستە. تکایە دووبارە پشکنینی بکەرەوە.", false); return; }
    
    el.redeemBtn.disabled = true;

    db.ref('used_codes/' + code).once('value').then(function(snapshot) {
      if(snapshot.exists()){
        showMsg(el.codeMsg, "ئەم کۆدە پێشتر بەکارهاتووە. هەر کۆدێک تەنها یەک جار کاردەکات.", false);
        el.redeemBtn.disabled = false;
      } else {
        db.ref('used_codes/' + code).set({ by: currentUser.key, at: Date.now() });
        currentUser.points += CODE_REWARD_POINTS;
        currentUser.spins += 1;
        db.ref('users/' + currentUser.key).update({ points: currentUser.points, spins: currentUser.spins });
        refreshUserUI();
        showMsg(el.codeMsg, "سەرکەوتوو بوو! " + CODE_REWARD_POINTS + " خاڵ زیادکرا و یەک جەخماوی چەرخ کرایەوە 🎡", true);
        el.codeInput.value = "";
        el.redeemBtn.disabled = false;
      }
    });
  });

  var isSpinning = false;
  var currentRotation = 0;

  function pickWeightedSegment(){
    var totalWeight = WHEEL_SEGMENTS.reduce(function(sum, s){ return sum + s.weight; }, 0);
    var r = Math.random() * totalWeight;
    var acc = 0;
    for(var i=0;i<SEG_COUNT;i++){
      acc += WHEEL_SEGMENTS[i].weight;
      if(r <= acc) return i;
    }
    return SEG_COUNT - 1;
  }

  el.spinBtn.addEventListener("click", function(){
    if(isSpinning || !currentUser || currentUser.spins <= 0) return;
    isSpinning = true;
    el.spinBtn.disabled = true;

    var winIndex = pickWeightedSegment();
    var seg = WHEEL_SEGMENTS[winIndex];
    var jitter = (Math.random() - 0.5) * (SEG_ANGLE * 0.6);
    var segCenter = (winIndex * SEG_ANGLE) + (SEG_ANGLE/2) + jitter;
    var baseTarget = (360 - segCenter) % 360;
    var fullSpins = 6; 
    var normalizedCurrent = currentRotation % 360;
    var deltaToTarget = (baseTarget - normalizedCurrent + 360) % 360;
    var finalRotation = currentRotation + (fullSpins * 360) + deltaToTarget;

    currentRotation = finalRotation;
    el.wheelEl.style.transform = "rotate(" + finalRotation + "deg)";

    setTimeout(function(){
      isSpinning = false;
      currentUser.spins -= 1;
      if(seg.type === "points") { currentUser.points += seg.points; }
      
      db.ref('users/' + currentUser.key).update({ points: currentUser.points, spins: currentUser.spins });

      db.ref('spin_history').push({
        name: currentUser.name,
        result: seg.label,
        time: new Date().toLocaleString()
      });

      refreshUserUI();
      showResult(seg);
    }, 4300);
  });

  function showResult(seg){
    var emoji = "🎉", title = "پیرۆزە!", sub = "";
    if(seg.type === "points"){
      emoji = "💰"; title = "براوەی " + seg.points + " خاڵ بوویت!";
      sub = "خاڵەکانت زیادکران بۆ ژمارەی گشتیت.";
    } else if(seg.type === "juice"){
      emoji = "🥤"; title = "جوسی خۆڕایی بردتەوە!";
      sub = "ئەم پەیامە بۆ کارمەندی خشتەکە پیشان بدە.";
    } else if(seg.type === "fries"){
      emoji = "🍟"; title = "فرایزی خۆڕایی بردتەوە!";
      sub = "ئەم پەیامە بۆ کارمەندی خشتەکە پیشان بدە.";
    } else {
      emoji = "🔁"; title = "ئەمجارە هیچ نەبوو!";
      sub = "کۆدێکی تر بەکاربهێنە بۆ هەوڵدانەوە.";
    }
    el.resultEmoji.textContent = emoji;
    el.resultTitle.textContent = title;
    el.resultSub.textContent = sub;
    el.resultOverlay.classList.add("show");
  }

  el.resultCloseBtn.addEventListener("click", function(){ el.resultOverlay.classList.remove("show"); });

  el.openAdminBtn.addEventListener("click", function(){
    var pass = prompt("تکایە وشەی تێپەڕی بەڕێوەبەر (Admin Password) بنووسە:");
    if(pass === "crava2026") {
      goSection("admin");
    } else if(pass !== null) {
      alert("وشەی تێپەڕ نادروستە!");
    }
  });

  el.backToAppBtn.addEventListener("click", function(){
    goSection("leaderboard");
  });

  db.ref('users').on('value', function(snapshot) {
    var users = snapshot.val() || {};
    var list = Object.keys(users).map(function(k){
      return { key: k, name: users[k].name, points: users[k].points };
    });
    list.sort(function(a,b){ return b.points - a.points; });
    
    el.leaderboardList.innerHTML = "";
    if(list.length === 0){
      el.leaderboardList.innerHTML = '<div class="lb-empty">هێشتا هیچ بەکارهێنەرێک تۆمار نەکراوە. یەکەم کەس بە!</div>';
    } else {
      var rankClass = ["gold","silver","bronze"];
      var rankBadge = ["🥇","🥈","🥉"];
      list.forEach(function(u, idx){
        var row = document.createElement("div");
        row.className = "lb-row" + (idx < 3 ? " " + rankClass[idx] : "") + (currentUser && u.key === currentUser.key ? " me" : "");
        var rankContent = idx < 3 ? rankBadge[idx] : (idx+1);
        row.innerHTML =
          '<div class="lb-rank">' + rankContent + '</div>' +
          '<div class="lb-name">' + escapeHtml(u.name) + '</div>' +
          '<div class="lb-pts">' + u.points + ' خاڵ</div>';
        el.leaderboardList.appendChild(row);
      });
    }

    el.adminList.innerHTML = "";
    if(list.length === 0){
      el.adminList.innerHTML = '<div class="lb-empty">هیچ بەکارهێنەرێک نییە.</div>';
    } else {
      list.forEach(function(u){
        var adminRow = document.createElement("div");
        adminRow.className = "lb-row";
        adminRow.innerHTML =
          '<div class="lb-name"><b>' + escapeHtml(u.name) + '</b> <span style="font-size:11px; color:var(--text-dim);">(' + u.points + ' خاڵ)</span></div>' +
          '<button class="btn btn-danger" data-key="' + u.key + '">سڕینەوە</button>';
        
        adminRow.querySelector("button").addEventListener("click", function(){
          if(confirm("دڵنیای لە سڕینەوەی '" + u.name + "'؟")) {
            db.ref('users/' + u.key).remove();
          }
        });
        el.adminList.appendChild(adminRow);
      });
    }
  });

  db.ref('spin_history').limitToLast(20).on('value', function(snapshot) {
    var histories = snapshot.val() || {};
    var keys = Object.keys(histories).reverse();
    
    el.adminSpinHistory.innerHTML = "";
    if(keys.length === 0){
      el.adminSpinHistory.innerHTML = '<div class="lb-empty">هێشتا هیچ کەسێک چەرخی نەسوڕاندووە.</div>';
      return;
    }

    keys.forEach(function(k){
      var h = histories[k];
      var row = document.createElement("div");
      row.className = "lb-row";
      row.innerHTML =
        '<div class="lb-name"><b>' + escapeHtml(h.name) + '</b><br><span style="font-size:11px; color:var(--text-dim);">' + (h.time || '') + '</span></div>' +
        '<div class="lb-pts" style="color:var(--yellow-2); font-size:13px;">' + escapeHtml(h.result) + '</div>';
      el.adminSpinHistory.appendChild(row);
    });
  });

  function escapeHtml(s){
    return String(s).replace(/[&<>"']/g, function(c){
      return {"&":"&amp;","<":"&lt;",">":"&gt;",'"':"&quot;","'":"&#39;"}[c];
    });
  }

  document.querySelectorAll(".tab-btn").forEach(function(btn){
    btn.addEventListener("click", function(){ goSection(btn.getAttribute("data-tab")); });
  });

  function init(){
    buildWheel();
    var savedKey = localStorage.getItem(SESSION_KEY);
    if(savedKey){
      db.ref('users/' + savedKey).once('value').then(function(snapshot) {
        if(snapshot.exists()){
          currentUser = snapshot.val();
          currentUser.key = savedKey;
          refreshUserUI();
          goSection("home");
        } else {
          goSection("auth");
        }
      }).catch(function(){ goSection("auth"); });
    } else {
      goSection("auth");
    }
  }

  init();
})();
</script>
</body>
</html>
