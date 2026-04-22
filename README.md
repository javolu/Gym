<!DOCTYPE html>

<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
<title>FitChallenge — 10 Semanas</title>
<link href="https://fonts.googleapis.com/css2?family=Bebas+Neue&family=DM+Sans:wght@300;400;500&family=DM+Mono:wght@400&display=swap" rel="stylesheet">
<style>
:root{
  --bg:#0a0a0a; --surface:#111; --card:#181818; --border:#252525;
  --red:#ff3c3c; --orange:#ff7c2a; --green:#3de07a; --blue:#4db8ff; --yellow:#ffe44d;
  --white:#f0ede8; --muted:#555; --muted2:#888;
  --gold:#ffd700; --silver:#c0c0c0; --bronze:#cd7f32;
}
*{margin:0;padding:0;box-sizing:border-box;-webkit-tap-highlight-color:transparent;}
html,body{height:100%;overflow:hidden;}
body{background:var(--bg);color:var(--white);font-family:'DM Sans',sans-serif;font-size:14px;}

/* ── PAGES ── */
.page{position:fixed;inset:0;overflow-y:auto;overflow-x:hidden;display:none;padding-bottom:90px;}
.page.on{display:block;}
.page::-webkit-scrollbar{display:none;}

/* ── TOP BAR ── */
.topbar{padding:22px 20px 10px;display:flex;justify-content:space-between;align-items:flex-end;position:sticky;top:0;z-index:50;background:linear-gradient(to bottom,var(–bg) 80%,transparent);}
.tb-title{font-family:‘Bebas Neue’,cursive;font-size:28px;letter-spacing:.05em;line-height:1;}
.tb-sub{font-family:‘DM Mono’,monospace;font-size:10px;color:var(–muted);letter-spacing:.12em;margin-top:2px;}
.tb-right{display:flex;align-items:center;gap:8px;}
.tb-user{font-family:‘DM Mono’,monospace;font-size:10px;color:var(–orange);border:1px solid rgba(255,124,42,.3);padding:5px 10px;border-radius:20px;}
.tb-logout{background:none;border:none;color:var(–muted);cursor:pointer;font-size:18px;padding:4px;}

/* ── SECTION LABEL ── */
.sl{font-family:‘DM Mono’,monospace;font-size:10px;color:var(–muted);letter-spacing:.14em;text-transform:uppercase;padding:16px 20px 8px;}

/* ── CARDS ── */
.card{background:var(–card);border:1px solid var(–border);border-radius:12px;margin:0 16px 10px;padding:18px;}
.c-title{font-family:‘Bebas Neue’,cursive;font-size:20px;letter-spacing:.05em;margin-bottom:10px;}
.card p{font-size:13px;color:var(–muted2);line-height:1.7;}

/* ── TABS ── */
.tabs{display:flex;gap:6px;padding:0 16px;margin-bottom:14px;overflow-x:auto;}
.tabs::-webkit-scrollbar{display:none;}
.tab{font-family:‘DM Mono’,monospace;font-size:10px;letter-spacing:.1em;text-transform:uppercase;padding:7px 14px;border-radius:20px;border:1px solid var(–border);background:var(–card);color:var(–muted);cursor:pointer;white-space:nowrap;}
.tab.on{background:rgba(255,60,60,.1);color:var(–red);border-color:rgba(255,60,60,.3);}

/* ── NAV ── */
.nav{position:fixed;bottom:0;left:0;right:0;background:rgba(8,8,8,.97);backdrop-filter:blur(20px);border-top:1px solid var(–border);display:flex;z-index:100;padding-bottom:env(safe-area-inset-bottom,0px);}
.nb{flex:1;padding:12px 4px 10px;border:none;background:none;color:var(–muted);cursor:pointer;display:flex;flex-direction:column;align-items:center;gap:3px;font-family:‘DM Mono’,monospace;font-size:8px;letter-spacing:.04em;text-transform:uppercase;}
.nb.on{color:var(–red);}
.nb svg{width:20px;height:20px;stroke:currentColor;fill:none;stroke-width:1.8;}

/* ── BUTTONS ── */
.btn{border:none;border-radius:10px;cursor:pointer;font-family:‘DM Sans’,sans-serif;font-weight:500;transition:transform .1s,opacity .15s;}
.btn:active{transform:scale(.96);}
.btn-p{background:var(–red);color:#fff;padding:14px;font-size:14px;width:100%;border-radius:12px;}
.btn-s{background:var(–card);color:var(–muted2);border:1px solid var(–border);padding:8px 14px;font-size:12px;border-radius:8px;}
.btn-s.on{background:rgba(255,60,60,.1);color:var(–red);border-color:rgba(255,60,60,.3);}
.btn-green{background:var(–green);color:#000;padding:14px;font-size:14px;width:100%;border-radius:12px;font-weight:600;}

/* ── FORMS ── */
.fg{margin-bottom:14px;}
.fl{font-family:‘DM Mono’,monospace;font-size:10px;color:var(–muted);letter-spacing:.12em;text-transform:uppercase;display:block;margin-bottom:5px;}
.fi{width:100%;background:rgba(255,255,255,.05);border:1px solid var(–border);border-radius:8px;padding:12px 14px;color:var(–white);font-family:‘DM Sans’,sans-serif;font-size:14px;outline:none;transition:border-color .2s;}
.fi:focus{border-color:var(–red);}
.fi::placeholder{color:var(–muted);}
select.fi{cursor:pointer;}
textarea.fi{resize:none;min-height:60px;}
.err{color:var(–red);font-size:12px;margin-top:4px;display:none;}
.err.on{display:block;}

/* ── MODAL ── */
.overlay{position:fixed;inset:0;background:rgba(0,0,0,.8);backdrop-filter:blur(8px);z-index:300;display:none;align-items:flex-end;justify-content:center;}
.overlay.on{display:flex;}
.modal{background:#1a1a1a;border:1px solid var(–border);border-radius:20px 20px 0 0;width:100%;max-width:480px;padding:20px 20px 50px;max-height:90vh;overflow-y:auto;}
.modal::-webkit-scrollbar{display:none;}
.mhandle{width:36px;height:4px;background:var(–border);border-radius:2px;margin:0 auto 20px;}
.mtitle{font-family:‘Bebas Neue’,cursive;font-size:26px;letter-spacing:.05em;margin-bottom:20px;}

/* ── LOGIN PAGE ── */
#page-login{display:flex;flex-direction:column;align-items:center;justify-content:center;min-height:100vh;padding:30px 24px;background:var(–bg);}
#page-login.on{display:flex;}
.login-logo{font-family:‘Bebas Neue’,cursive;font-size:56px;letter-spacing:.08em;color:var(–red);text-align:center;line-height:.9;margin-bottom:8px;}
.login-tagline{font-family:‘DM Mono’,monospace;font-size:10px;color:var(–muted);letter-spacing:.2em;text-transform:uppercase;text-align:center;margin-bottom:40px;}
.login-box{width:100%;max-width:360px;}
.login-tabs{display:flex;gap:0;margin-bottom:24px;border:1px solid var(–border);border-radius:10px;overflow:hidden;}
.ltab{flex:1;padding:10px;text-align:center;font-family:‘DM Mono’,monospace;font-size:11px;letter-spacing:.1em;text-transform:uppercase;cursor:pointer;color:var(–muted);background:var(–card);transition:all .2s;}
.ltab.on{background:var(–red);color:#fff;}

/* ── KPI ── */
.kpi-row{display:grid;grid-template-columns:1fr 1fr;gap:10px;margin:0 16px 10px;}
.kpi{background:var(–card);border:1px solid var(–border);border-radius:12px;padding:16px;}
.kv{font-family:‘Bebas Neue’,cursive;font-size:28px;letter-spacing:.04em;line-height:1;}
.ku{font-family:‘DM Mono’,monospace;font-size:10px;color:var(–muted);}
.kl{font-family:‘DM Mono’,monospace;font-size:9px;color:var(–muted);letter-spacing:.1em;text-transform:uppercase;margin-top:4px;}
.kdelta{font-size:11px;margin-top:3px;}
.dn{color:var(–green);}.up{color:var(–red);}

/* ── EXERCISE LIST ── */
.ex-row{display:flex;justify-content:space-between;align-items:center;padding:9px 0;border-bottom:1px solid rgba(255,255,255,.05);}
.ex-row:last-child{border:none;}
.ex-n{font-size:13px;font-weight:500;}
.ex-s{font-family:‘DM Mono’,monospace;font-size:11px;color:var(–orange);}
.ex-s.c{color:var(–red);}

/* ── MEAL PLAN ── */
.mc{background:var(–card);border:1px solid var(–border);border-radius:12px;margin:0 16px 10px;padding:16px;}
.mt{font-family:‘DM Mono’,monospace;font-size:10px;color:var(–orange);letter-spacing:.14em;text-transform:uppercase;}
.mn{font-family:‘Bebas Neue’,cursive;font-size:17px;letter-spacing:.05em;margin:4px 0 10px;}
.mi{list-style:none;}
.mi li{font-size:13px;color:var(–muted2);padding:4px 0;border-bottom:1px solid rgba(255,255,255,.04);display:flex;gap:8px;}
.mi li:last-child{border:none;}
.mi li::before{content:’—’;color:var(–orange);font-size:10px;flex-shrink:0;margin-top:2px;}
.mm{display:flex;gap:6px;flex-wrap:wrap;margin-top:10px;}
.mac{font-family:‘DM Mono’,monospace;font-size:10px;padding:3px 8px;border-radius:6px;background:rgba(255,255,255,.05);color:var(–muted2);}

/* ── LEADERBOARD ── */
.lb-card{background:var(–card);border:1px solid var(–border);border-radius:12px;margin:0 16px 10px;overflow:hidden;}
.lb-row{display:flex;align-items:center;padding:14px 16px;border-bottom:1px solid rgba(255,255,255,.05);gap:12px;}
.lb-row:last-child{border:none;}
.lb-row.me{background:rgba(255,60,60,.06);}
.lb-rank{font-family:‘Bebas Neue’,cursive;font-size:22px;letter-spacing:.05em;width:28px;flex-shrink:0;text-align:center;}
.lb-rank.r1{color:var(–gold);}
.lb-rank.r2{color:var(–silver);}
.lb-rank.r3{color:var(–bronze);}
.lb-info{flex:1;}
.lb-name{font-size:14px;font-weight:500;}
.lb-meta{font-family:‘DM Mono’,monospace;font-size:10px;color:var(–muted);margin-top:2px;}
.lb-score{text-align:right;}
.lb-pts{font-family:‘Bebas Neue’,cursive;font-size:24px;letter-spacing:.04em;color:var(–orange);}
.lb-ptsl{font-family:‘DM Mono’,monospace;font-size:9px;color:var(–muted);}
.lb-bar-wrap{height:3px;background:rgba(255,255,255,.06);border-radius:2px;margin-top:6px;}
.lb-bar{height:3px;border-radius:2px;background:linear-gradient(90deg,var(–red),var(–orange));transition:width .4s;}

/* ── WINNER BANNER ── */
.winner-banner{margin:12px 16px;padding:20px;background:linear-gradient(135deg,rgba(255,215,0,.1),rgba(255,124,42,.06));border:1px solid rgba(255,215,0,.25);border-radius:14px;text-align:center;}
.winner-crown{font-size:40px;margin-bottom:8px;}
.winner-title{font-family:‘Bebas Neue’,cursive;font-size:14px;letter-spacing:.2em;color:var(–gold);margin-bottom:4px;}
.winner-name{font-family:‘Bebas Neue’,cursive;font-size:36px;letter-spacing:.05em;color:var(–white);}
.winner-pts{font-family:‘DM Mono’,monospace;font-size:11px;color:var(–muted);margin-top:4px;}

/* ── TODAY CARD ── */
.today-card{margin:12px 16px;padding:18px;background:linear-gradient(135deg,rgba(255,60,60,.1),rgba(255,124,42,.06));border:1px solid rgba(255,60,60,.2);border-radius:14px;}
.t-day{font-family:‘Bebas Neue’,cursive;font-size:32px;letter-spacing:.05em;line-height:1;}
.t-focus{font-family:‘DM Mono’,monospace;font-size:10px;color:var(–orange);letter-spacing:.12em;text-transform:uppercase;margin-top:4px;}

/* ── WEEK STRIP ── */
.wstrip{display:flex;gap:6px;margin:0 16px 10px;}
.wd{flex:1;background:var(–card);border:1px solid var(–border);border-radius:8px;padding:7px 4px;text-align:center;font-family:‘DM Mono’,monospace;font-size:9px;color:var(–muted);}
.wd.t{border-color:rgba(255,60,60,.4);color:var(–red);background:rgba(255,60,60,.06);}
.wd.d{border-color:rgba(61,224,122,.3);color:var(–green);background:rgba(61,224,122,.06);}
.wd span{display:block;font-size:12px;margin-bottom:1px;}

/* ── LOG ROW ── */
.lr{background:var(–card);border:1px solid var(–border);border-radius:12px;margin:0 16px 8px;padding:14px 16px;}
.lr-top{display:flex;justify-content:space-between;align-items:flex-start;margin-bottom:4px;}
.lr-date{font-family:‘DM Mono’,monospace;font-size:10px;color:var(–muted);letter-spacing:.1em;}
.lr-body{font-size:13px;color:var(–muted2);line-height:1.6;}
.tag{display:inline-block;font-family:‘DM Mono’,monospace;font-size:9px;padding:2px 7px;border-radius:6px;background:rgba(255,255,255,.05);color:var(–muted);margin-top:5px;}
.tag.g{background:rgba(61,224,122,.08);color:var(–green);}

/* ── CHART ── */
.cb{background:var(–card);border:1px solid var(–border);border-radius:12px;margin:0 16px 10px;padding:16px;}
.cl{font-family:‘DM Mono’,monospace;font-size:10px;color:var(–muted);letter-spacing:.12em;text-transform:uppercase;margin-bottom:12px;}
canvas{display:block;width:100% !important;}

/* ── EMPTY ── */
.empty{text-align:center;padding:40px 20px;}
.ei{font-size:36px;margin-bottom:12px;}
.empty p{font-size:13px;color:var(–muted);line-height:1.8;}

/* ── FAB ── */
.fab{position:fixed;bottom:76px;right:16px;width:50px;height:50px;border-radius:50%;background:var(–red);border:none;cursor:pointer;display:flex;align-items:center;justify-content:center;box-shadow:0 4px 18px rgba(255,60,60,.35);z-index:90;}
.fab svg{width:22px;height:22px;stroke:#fff;fill:none;stroke-width:2.5;}

/* ── WEEK TIMER ── */
.week-banner{margin:0 16px 10px;padding:14px 18px;background:var(–card);border:1px solid var(–border);border-radius:12px;display:flex;justify-content:space-between;align-items:center;}
.wb-left{font-family:‘Bebas Neue’,cursive;font-size:28px;letter-spacing:.05em;color:var(–white);}
.wb-sub{font-family:‘DM Mono’,monospace;font-size:10px;color:var(–muted);margin-top:2px;}
.wb-prog{text-align:right;}
.prog-bar{height:4px;background:rgba(255,255,255,.08);border-radius:2px;overflow:hidden;width:80px;margin-top:6px;}
.prog-fill{height:100%;border-radius:2px;background:linear-gradient(90deg,var(–red),var(–orange));}

/* ── MEDAL BADGES ── */
.medal{display:inline-block;font-size:16px;margin-right:4px;}

/* REGISTER STEP INDICATOR */
.steps{display:flex;gap:6px;margin-bottom:20px;justify-content:center;}
.step-dot{width:8px;height:8px;border-radius:50%;background:var(–border);}
.step-dot.on{background:var(–red);}

@keyframes up{from{opacity:0;transform:translateY(8px)}to{opacity:1;transform:translateY(0)}}
.page.on > * { animation: up .2s ease both; }
</style>

</head>
<body>

<!-- ══════════════════════════════════
     PAGE: LOGIN / REGISTER
══════════════════════════════════ -->

<div class="page on" id="page-login">
  <div class="login-logo">FIT<br>CHALLENGE</div>
  <div class="login-tagline">10 semanas · Competencia grupal</div>

  <div class="login-box">
    <div class="login-tabs">
      <div class="ltab on" id="ltab-login" onclick="showLoginTab('login')">Entrar</div>
      <div class="ltab" id="ltab-reg" onclick="showLoginTab('register')">Registro</div>
    </div>

```
<!-- LOGIN FORM -->
<div id="login-form">
  <div class="fg"><label class="fl">Usuario</label><input class="fi" type="text" id="l-user" placeholder="tu nombre de usuario" autocapitalize="none"></div>
  <div class="fg"><label class="fl">Contraseña</label><input class="fi" type="password" id="l-pass" placeholder="••••••••"></div>
  <div class="err" id="l-err">Usuario o contraseña incorrectos</div>
  <button class="btn btn-p" style="margin-top:8px;" onclick="doLogin()">Entrar →</button>
  <div style="text-align:center;margin-top:16px;font-size:12px;color:var(--muted);">¿Sin cuenta? <span style="color:var(--red);cursor:pointer;" onclick="showLoginTab('register')">Regístrate</span></div>
</div>

<!-- REGISTER FORM -->
<div id="register-form" style="display:none;">
  <div class="steps" id="reg-steps">
    <div class="step-dot on"></div><div class="step-dot"></div><div class="step-dot"></div>
  </div>

  <!-- STEP 1: Account -->
  <div id="reg-s1">
    <div style="font-family:'Bebas Neue',cursive;font-size:20px;letter-spacing:.05em;margin-bottom:16px;">Crea tu cuenta</div>
    <div class="fg"><label class="fl">Nombre de usuario</label><input class="fi" type="text" id="r-user" placeholder="sin espacios, ej: javier29" autocapitalize="none"></div>
    <div class="fg"><label class="fl">Contraseña</label><input class="fi" type="password" id="r-pass" placeholder="mínimo 6 caracteres"></div>
    <div class="fg"><label class="fl">Repetir contraseña</label><input class="fi" type="password" id="r-pass2" placeholder="••••••••"></div>
    <div class="err" id="r-err1"></div>
    <button class="btn btn-p" onclick="regStep1()">Siguiente →</button>
  </div>

  <!-- STEP 2: Personal data -->
  <div id="reg-s2" style="display:none;">
    <div style="font-family:'Bebas Neue',cursive;font-size:20px;letter-spacing:.05em;margin-bottom:16px;">Tus datos</div>
    <div class="fg"><label class="fl">Nombre completo</label><input class="fi" type="text" id="r-nombre" placeholder="ej. Carlos Ramírez"></div>
    <div class="fg"><label class="fl">Sexo</label>
      <select class="fi" id="r-sexo"><option value="H">Hombre</option><option value="M">Mujer</option></select>
    </div>
    <div style="display:grid;grid-template-columns:1fr 1fr;gap:10px;">
      <div class="fg"><label class="fl">Edad</label><input class="fi" type="number" id="r-edad" placeholder="29"></div>
      <div class="fg"><label class="fl">Altura (cm)</label><input class="fi" type="number" id="r-altura" placeholder="175"></div>
    </div>
    <div class="fg"><label class="fl">Peso actual (kg)</label><input class="fi" type="number" step="0.1" id="r-peso" placeholder="81.0"></div>
    <div class="err" id="r-err2"></div>
    <div style="display:flex;gap:8px;">
      <button class="btn btn-s" onclick="regBack(1)">← Atrás</button>
      <button class="btn btn-p" style="flex:1;" onclick="regStep2()">Siguiente →</button>
    </div>
  </div>

  <!-- STEP 3: Goals -->
  <div id="reg-s3" style="display:none;">
    <div style="font-family:'Bebas Neue',cursive;font-size:20px;letter-spacing:.05em;margin-bottom:16px;">Tu objetivo</div>
    <div class="fg"><label class="fl">Meta principal</label>
      <select class="fi" id="r-meta">
        <option value="bajar_grasa">Bajar grasa 🔥</option>
        <option value="recomposicion">Recomposición (bajar y tonificar) 💪</option>
        <option value="ganar_musculo">Ganar músculo 📈</option>
      </select>
    </div>
    <div class="fg"><label class="fl">Nivel de actividad actual</label>
      <select class="fi" id="r-act">
        <option value="sedentario">Sedentario (poco o nada de ejercicio)</option>
        <option value="moderado" selected>Moderado (1-3 días/semana)</option>
        <option value="activo">Activo (4+ días/semana)</option>
      </select>
    </div>
    <div class="fg"><label class="fl">Días disponibles para gym por semana</label>
      <select class="fi" id="r-dias">
        <option value="3">3 días</option>
        <option value="4" selected>4 días</option>
        <option value="5">5 días</option>
      </select>
    </div>
    <div class="err" id="r-err3"></div>
    <div style="display:flex;gap:8px;margin-top:4px;">
      <button class="btn btn-s" onclick="regBack(2)">← Atrás</button>
      <button class="btn btn-green" style="flex:1;" onclick="regStep3()">¡Unirme al reto!</button>
    </div>
  </div>
</div>
```

  </div>
</div>

<!-- ══════════════════════════════════
     MAIN APP (shown after login)
══════════════════════════════════ -->

<!-- PAGE: HOME -->

<div class="page" id="page-home">
  <div class="topbar">
    <div><div class="tb-title">INICIO</div><div class="tb-sub" id="home-sub">Semana 1 de 10</div></div>
    <div class="tb-right">
      <span class="tb-user" id="home-username">—</span>
      <button class="tb-logout" onclick="doLogout()" title="Salir">⏏</button>
    </div>
  </div>

  <div class="today-card">
    <div style="display:flex;justify-content:space-between;align-items:flex-start;">
      <div>
        <div class="t-day" id="home-dayname">LUNES</div>
        <div class="t-focus" id="home-focus">—</div>
      </div>
      <div style="text-align:right;">
        <div style="font-family:'Bebas Neue',cursive;font-size:26px;color:var(--red);" id="home-week">SEM 1</div>
        <div style="font-family:'DM Mono',monospace;font-size:9px;color:var(--muted);">DE 10</div>
      </div>
    </div>
  </div>

  <div class="wstrip" id="home-strip"></div>

  <div class="sl">Tu progreso</div>
  <div class="kpi-row">
    <div class="kpi"><div class="kv" id="h-peso">—</div><span class="ku"> kg</span><div class="kl">Peso actual</div><div class="kdelta" id="h-pd"></div></div>
    <div class="kpi"><div class="kv" id="h-score">0</div><span class="ku"> pts</span><div class="kl">Tu score</div><div class="kdelta" id="h-rank" style="color:var(--orange);"></div></div>
  </div>

  <div class="sl">Entreno de hoy</div>
  <div class="card">
    <div class="c-title" id="h-rname">—</div>
    <div id="h-rex"></div>
    <button class="btn btn-p" style="margin-top:14px;" onclick="goPage('page-rutinas')">Ver rutina completa →</button>
  </div>

  <div class="sl">Registro rápido</div>
  <div class="card">
    <div style="display:flex;gap:8px;">
      <button class="btn btn-s" style="flex:1;" onclick="openM('o-gym')">+ Entreno</button>
      <button class="btn btn-s" style="flex:1;" onclick="openM('o-meal')">+ Comida</button>
      <button class="btn btn-s" style="flex:1;" onclick="openM('o-med')">+ Medida</button>
    </div>
  </div>
</div>

<!-- PAGE: RUTINAS -->

<div class="page" id="page-rutinas">
  <div class="topbar"><div><div class="tb-title">Rutina</div><div class="tb-sub" id="rut-sub">Personalizada</div></div></div>
  <div class="tabs" id="rut-tabs"></div>
  <div id="rut-content"></div>
  <div class="sl">Tu plan nutricional</div>
  <div class="card" id="rut-macros"></div>
  <div id="rut-meals" style="margin-bottom:20px;"></div>
</div>

<!-- PAGE: LOG -->

<div class="page" id="page-log">
  <div class="topbar">
    <div><div class="tb-title">Mi Log</div><div class="tb-sub">Entrenos y comidas</div></div>
    <button style="font-family:'DM Mono',monospace;font-size:11px;color:var(--red);border:1px solid rgba(255,60,60,.3);padding:5px 10px;border-radius:20px;background:none;cursor:pointer;" onclick="openM('o-gym')">+ Log</button>
  </div>
  <div class="tabs">
    <div class="tab on" onclick="logTab('gym',this)">Gym</div>
    <div class="tab" onclick="logTab('comida',this)">Comida</div>
    <div class="tab" onclick="logTab('medidas',this)">Medidas</div>
  </div>
  <div id="log-gym-list"></div>
  <div id="log-comida-list" style="display:none;"></div>
  <div id="log-medidas-list" style="display:none;"></div>
</div>

<!-- PAGE: PROGRESO -->

<div class="page" id="page-prog">
  <div class="topbar">
    <div><div class="tb-title">Progreso</div><div class="tb-sub">Gráficas y medidas</div></div>
    <button style="font-family:'DM Mono',monospace;font-size:11px;color:var(--red);border:1px solid rgba(255,60,60,.3);padding:5px 10px;border-radius:20px;background:none;cursor:pointer;" onclick="openM('o-med')">+ Medida</button>
  </div>
  <div class="cb"><div class="cl">Peso (kg)</div><canvas id="c-peso" height="110"></canvas></div>
  <div class="sl">Historial de medidas</div>
  <div id="prog-list"></div>
</div>

<!-- PAGE: COMPETENCIA -->

<div class="page" id="page-comp">
  <div class="topbar"><div><div class="tb-title">Competencia</div><div class="tb-sub">10 semanas · Tabla general</div></div></div>
  <div id="comp-winner"></div>
  <div class="week-banner">
    <div>
      <div class="wb-left" id="comp-semana">SEM 1</div>
      <div class="wb-sub" id="comp-dias-left">70 días restantes</div>
    </div>
    <div class="wb-prog">
      <div style="font-family:'DM Mono',monospace;font-size:10px;color:var(--muted);text-align:right;" id="comp-pct">0%</div>
      <div class="prog-bar" style="margin-top:4px;"><div class="prog-fill" id="comp-prog" style="width:0%;"></div></div>
    </div>
  </div>
  <div class="sl">Clasificación</div>
  <div id="comp-lb"></div>
  <div class="sl">Estadísticas grupales</div>
  <div class="card" id="comp-stats"></div>
</div>

<!-- NAV -->

<nav class="nav" id="main-nav" style="display:none;">
  <button class="nb on" onclick="goPage('page-home',this)"><svg viewBox="0 0 24 24"><path d="M3 9.5L12 3l9 6.5V20a1 1 0 01-1 1H4a1 1 0 01-1-1z"/><path d="M9 21V12h6v9"/></svg>Inicio</button>
  <button class="nb" onclick="goPage('page-rutinas',this)"><svg viewBox="0 0 24 24"><path d="M6 4v16M18 4v16M3 8h18M3 16h18"/></svg>Rutina</button>
  <button class="nb" onclick="goPage('page-log',this)"><svg viewBox="0 0 24 24"><rect x="3" y="4" width="18" height="18" rx="2"/><path d="M16 2v4M8 2v4M3 10h18"/></svg>Log</button>
  <button class="nb" onclick="goPage('page-prog',this)"><svg viewBox="0 0 24 24"><polyline points="22 12 18 12 15 21 9 3 6 12 2 12"/></svg>Progreso</button>
  <button class="nb" onclick="goPage('page-comp',this)"><svg viewBox="0 0 24 24"><circle cx="12" cy="8" r="6"/><path d="M8 14l-4 7h16l-4-7"/></svg>Reto</button>
</nav>

<!-- MODALS -->

<!-- MODAL: GYM LOG -->

<div class="overlay" id="o-gym" onclick="if(event.target===this)closeM('o-gym');">
  <div class="modal">
    <div class="mhandle"></div>
    <div class="mtitle">Log de entreno</div>
    <div class="fg"><label class="fl">Fecha</label><input class="fi" type="date" id="gl-d"></div>
    <div class="fg"><label class="fl">Día entrenado</label><select class="fi" id="gl-day"></select></div>
    <div class="fg"><label class="fl">Duración (min)</label><input class="fi" type="number" placeholder="ej. 65" id="gl-dur"></div>
    <div class="fg">
      <label class="fl">Intensidad</label>
      <div style="display:flex;gap:8px;margin-top:4px;">
        <button class="btn btn-s" onclick="setInt(1,this)">😐 Suave</button>
        <button class="btn btn-s on" id="int-def" onclick="setInt(2,this)">💪 Normal</button>
        <button class="btn btn-s" onclick="setInt(3,this)">🔥 Brutal</button>
      </div>
    </div>
    <div class="fg"><label class="fl">Notas / PRs</label><textarea class="fi" placeholder="ej. Subí 5kg en sentadilla..." id="gl-n"></textarea></div>
    <button class="btn btn-p" onclick="saveGym()">Guardar entreno</button>
  </div>
</div>

<!-- MODAL: COMIDA -->

<div class="overlay" id="o-meal" onclick="if(event.target===this)closeM('o-meal');">
  <div class="modal">
    <div class="mhandle"></div>
    <div class="mtitle">Registrar comida</div>
    <div class="fg"><label class="fl">Fecha</label><input class="fi" type="date" id="ml-d"></div>
    <div class="fg"><label class="fl">Tiempo</label>
      <select class="fi" id="ml-t">
        <option>Desayuno</option><option>Colación mañana</option><option>Comida</option>
        <option>Pre-entreno</option><option>Cena</option><option>Otro</option>
      </select>
    </div>
    <div class="fg"><label class="fl">¿Qué comiste?</label><textarea class="fi" placeholder="ej. 3 huevos + avena + plátano" id="ml-f"></textarea></div>
    <div class="fg">
      <label class="fl">¿Seguiste tu plan?</label>
      <div style="display:flex;gap:8px;margin-top:4px;">
        <button class="btn btn-s on" id="pl-si" onclick="setPlan(true)">✓ Sí</button>
        <button class="btn btn-s" id="pl-no" onclick="setPlan(false)">✗ No</button>
      </div>
    </div>
    <div class="fg"><label class="fl">Agua hoy (litros)</label><input class="fi" type="number" step="0.5" placeholder="ej. 2.5" id="ml-a"></div>
    <button class="btn btn-p" onclick="saveMeal()">Guardar</button>
  </div>
</div>

<!-- MODAL: MEDIDAS -->

<div class="overlay" id="o-med" onclick="if(event.target===this)closeM('o-med');">
  <div class="modal">
    <div class="mhandle"></div>
    <div class="mtitle">Registrar medidas</div>
    <div class="fg"><label class="fl">Fecha</label><input class="fi" type="date" id="md-d"></div>
    <div class="fg"><label class="fl">Peso (kg)</label><input class="fi" type="number" step="0.1" placeholder="ej. 80.5" id="md-p"></div>
    <div class="fg"><label class="fl">Cintura (cm)</label><input class="fi" type="number" step="0.5" placeholder="ej. 86" id="md-c"></div>
    <div class="fg"><label class="fl">Pecho (cm)</label><input class="fi" type="number" step="0.5" placeholder="ej. 98" id="md-pe"></div>
    <div class="fg"><label class="fl">Cadera (cm)</label><input class="fi" type="number" step="0.5" placeholder="ej. 95" id="md-ca"></div>
    <div class="fg"><label class="fl">Brazo (cm)</label><input class="fi" type="number" step="0.5" placeholder="ej. 34" id="md-b"></div>
    <div class="fg"><label class="fl">Notas</label><textarea class="fi" placeholder="cómo te sentiste..." id="md-n"></textarea></div>
    <button class="btn btn-p" onclick="saveMed()">Guardar medidas</button>
  </div>
</div>

<script>
// ══════════════════════════════════════════════
// CONSTANTS & DATA
// ══════════════════════════════════════════════
var APP_KEY = 'fitchallenge_v1';
var COMPETITION_WEEKS = 10;

var ROUTINES_4 = [
  {day:'LUN',name:'PECHO + TRÍCEPS',ex:[{n:'Press banca plano',s:'4×10'},{n:'Press inclinado mancuernas',s:'4×12'},{n:'Aperturas cable',s:'3×15'},{n:'Jalones tríceps polea',s:'4×12'},{n:'Extensión tríceps 1 brazo',s:'3×12'},{n:'Caminadora 8% inclinación',s:'20 min',c:true}]},
  {day:'MAR',name:'ESPALDA + BÍCEPS',ex:[{n:'Jalón al pecho',s:'4×10'},{n:'Remo con barra',s:'4×10'},{n:'Remo máquina',s:'3×12'},{n:'Pull-over mancuerna',s:'3×12'},{n:'Curl bíceps barra',s:'4×12'},{n:'Curl martillo',s:'3×12'}]},
  {day:'JUE',name:'PIERNAS COMPLETO',ex:[{n:'Sentadilla con barra',s:'4×10'},{n:'Prensa de piernas',s:'4×12'},{n:'Peso muerto rumano',s:'4×10'},{n:'Zancadas caminando',s:'3×12/p'},{n:'Curl femoral máquina',s:'3×12'},{n:'Pantorrillas de pie',s:'4×20'},{n:'HIIT bike estática',s:'15 min',c:true}]},
  {day:'VIE',name:'HOMBROS + CORE',ex:[{n:'Press militar barra',s:'4×10'},{n:'Elevaciones laterales',s:'4×15'},{n:'Elevaciones frontales',s:'3×12'},{n:'Face pulls polea',s:'3×15'},{n:'Rueda abdominal',s:'4×10'},{n:'Plancha isométrica',s:'4×45 seg'},{n:'Caminadora 10% inclinación',s:'20 min',c:true}]},
  {day:'SÁB',name:'DESCANSO ACTIVO',ex:[{n:'Caminata 40 min',s:'tranquilo'},{n:'Estiramientos',s:'15 min'}]},
  {day:'DOM',name:'DESCANSO',ex:[{n:'Descanso o caminata',s:'opcional'},{n:'Meal prep semana',s:'recomendado'}]}
];
var ROUTINES_3 = [
  {day:'LUN',name:'FULL BODY A',ex:[{n:'Sentadilla con barra',s:'4×10'},{n:'Press banca plano',s:'4×10'},{n:'Jalón al pecho',s:'4×10'},{n:'Press militar mancuernas',s:'3×12'},{n:'Curl bíceps',s:'3×12'},{n:'Jalones tríceps',s:'3×12'},{n:'Cardio',s:'20 min',c:true}]},
  {day:'MIÉ',name:'FULL BODY B',ex:[{n:'Peso muerto',s:'4×8'},{n:'Press inclinado',s:'4×10'},{n:'Remo con barra',s:'4×10'},{n:'Zancadas',s:'3×12/p'},{n:'Curl martillo',s:'3×12'},{n:'Extensión tríceps',s:'3×12'}]},
  {day:'VIE',name:'FULL BODY C',ex:[{n:'Prensa de piernas',s:'4×12'},{n:'Aperturas en cable',s:'3×15'},{n:'Remo máquina',s:'3×12'},{n:'Elevaciones laterales',s:'4×15'},{n:'Pantorrillas',s:'4×20'},{n:'Core: plancha + crunch',s:'4×20 / 45 seg'}]},
  {day:'SAB',name:'DESCANSO ACTIVO',ex:[{n:'Caminata 40 min',s:'tranquilo'},{n:'Estiramientos',s:'15 min'}]},
  {day:'DOM',name:'DESCANSO',ex:[{n:'Descanso completo',s:''}]}
];
var ROUTINES_5 = ROUTINES_4.slice();
ROUTINES_5.splice(2,0,{day:'MIÉ',name:'CORE + HIIT',ex:[{n:'Plancha isométrica',s:'4×50 seg'},{n:'Mountain climbers',s:'4×35'},{n:'Elevaciones piernas',s:'4×20'},{n:'Crunches cruzados',s:'3×20'},{n:'Burpees',s:'4×12'},{n:'Jump squats',s:'3×15'},{n:'Trote / caminata',s:'30 min',c:true}]});

var FOCUS_MAP = {
  3: ['Full Body A','Descanso','Full Body B','Descanso','Full Body C','Descanso activo','Descanso'],
  4: ['Pecho + Tríceps','Espalda + Bíceps','Descanso','Piernas','Hombros + Core','Descanso activo','Descanso'],
  5: ['Pecho + Tríceps','Espalda + Bíceps','Core + HIIT','Piernas','Hombros + Core','Descanso activo','Descanso']
};

// ══════════════════════════════════════════════
// STORAGE
// ══════════════════════════════════════════════
var DB = { users: {}, competition: { startDate: null } };

function loadDB() {
  try {
    var s = localStorage.getItem(APP_KEY);
    if (s) DB = JSON.parse(s);
  } catch(e) {}
  if (!DB.users) DB.users = {};
  if (!DB.competition) DB.competition = { startDate: null };
}
function saveDB() {
  try { localStorage.setItem(APP_KEY, JSON.stringify(DB)); } catch(e) {}
}

// ══════════════════════════════════════════════
// AUTH
// ══════════════════════════════════════════════
var currentUser = null;

function hashPass(str) {
  var hash = 0;
  for (var i = 0; i < str.length; i++) {
    hash = ((hash << 5) - hash) + str.charCodeAt(i);
    hash |= 0;
  }
  return 'h_' + Math.abs(hash).toString(36);
}

function doLogin() {
  var u = document.getElementById('l-user').value.trim().toLowerCase();
  var p = document.getElementById('l-pass').value;
  var err = document.getElementById('l-err');
  if (!u || !p) { err.classList.add('on'); err.textContent = 'Completa todos los campos'; return; }
  var user = DB.users[u];
  if (!user || user.passHash !== hashPass(p)) { err.classList.add('on'); err.textContent = 'Usuario o contraseña incorrectos'; return; }
  err.classList.remove('on');
  currentUser = u;
  showApp();
}

function doLogout() {
  currentUser = null;
  document.getElementById('l-user').value = '';
  document.getElementById('l-pass').value = '';
  document.getElementById('l-err').classList.remove('on');
  document.getElementById('main-nav').style.display = 'none';
  goPage('page-login');
}

// ══════════════════════════════════════════════
// REGISTRATION
// ══════════════════════════════════════════════
var regData = {};

function showLoginTab(t) {
  document.getElementById('ltab-login').className = 'ltab' + (t==='login'?' on':'');
  document.getElementById('ltab-reg').className = 'ltab' + (t==='register'?' on':'');
  document.getElementById('login-form').style.display = t==='login' ? 'block' : 'none';
  document.getElementById('register-form').style.display = t==='register' ? 'block' : 'none';
}

function updateRegDots(step) {
  var dots = document.querySelectorAll('.step-dot');
  for (var i = 0; i < dots.length; i++) {
    dots[i].className = 'step-dot' + (i < step ? ' on' : '');
  }
}

function regStep1() {
  var u = document.getElementById('r-user').value.trim().toLowerCase();
  var p = document.getElementById('r-pass').value;
  var p2 = document.getElementById('r-pass2').value;
  var err = document.getElementById('r-err1');

  if (!u || u.length < 3) { err.classList.add('on'); err.textContent = 'Usuario mínimo 3 caracteres'; return; }
  if (/\s/.test(u)) { err.classList.add('on'); err.textContent = 'Sin espacios en el usuario'; return; }
  if (DB.users[u]) { err.classList.add('on'); err.textContent = 'Ese usuario ya existe'; return; }
  if (p.length < 6) { err.classList.add('on'); err.textContent = 'Contraseña mínimo 6 caracteres'; return; }
  if (p !== p2) { err.classList.add('on'); err.textContent = 'Las contraseñas no coinciden'; return; }
  if (Object.keys(DB.users).length >= 8) { err.classList.add('on'); err.textContent = 'Máximo 8 usuarios en la competencia'; return; }

  err.classList.remove('on');
  regData.username = u;
  regData.passHash = hashPass(p);
  document.getElementById('reg-s1').style.display = 'none';
  document.getElementById('reg-s2').style.display = 'block';
  updateRegDots(2);
}

function regStep2() {
  var nombre = document.getElementById('r-nombre').value.trim();
  var sexo = document.getElementById('r-sexo').value;
  var edad = parseInt(document.getElementById('r-edad').value);
  var altura = parseInt(document.getElementById('r-altura').value);
  var peso = parseFloat(document.getElementById('r-peso').value);
  var err = document.getElementById('r-err2');

  if (!nombre) { err.classList.add('on'); err.textContent = 'Ingresa tu nombre'; return; }
  if (!edad || edad < 15 || edad > 80) { err.classList.add('on'); err.textContent = 'Edad entre 15 y 80'; return; }
  if (!altura || altura < 140 || altura > 220) { err.classList.add('on'); err.textContent = 'Altura entre 140 y 220 cm'; return; }
  if (!peso || peso < 40 || peso > 200) { err.classList.add('on'); err.textContent = 'Peso entre 40 y 200 kg'; return; }

  err.classList.remove('on');
  regData.nombre = nombre; regData.sexo = sexo;
  regData.edad = edad; regData.altura = altura; regData.peso = peso;
  document.getElementById('reg-s2').style.display = 'none';
  document.getElementById('reg-s3').style.display = 'block';
  updateRegDots(3);
}

function regStep3() {
  var meta = document.getElementById('r-meta').value;
  var act = document.getElementById('r-act').value;
  var dias = parseInt(document.getElementById('r-dias').value);

  regData.meta = meta; regData.actividad = act; regData.diasGym = dias;
  regData.plan = generatePlan(regData);
  regData.pesoInicial = regData.peso;
  regData.gymLogs = []; regData.meals = []; regData.medidas = [];
  regData.medidas.push({ date: today(), peso: regData.peso, cintura: null, pecho: null, cadera: null, brazo: null, notas: 'Peso inicial', ts: Date.now() });
  regData.joinDate = today();

  DB.users[regData.username] = regData;
  if (!DB.competition.startDate) DB.competition.startDate = today();
  saveDB();

  currentUser = regData.username;
  showApp();
}

function regBack(step) {
  if (step === 1) { document.getElementById('reg-s2').style.display='none'; document.getElementById('reg-s1').style.display='block'; updateRegDots(1); }
  if (step === 2) { document.getElementById('reg-s3').style.display='none'; document.getElementById('reg-s2').style.display='block'; updateRegDots(2); }
}

// ══════════════════════════════════════════════
// PLAN GENERATOR
// ══════════════════════════════════════════════
function generatePlan(p) {
  var bmr = (p.sexo === 'H')
    ? 10*p.peso + 6.25*p.altura - 5*p.edad + 5
    : 10*p.peso + 6.25*p.altura - 5*p.edad - 161;
  var actF = {sedentario:1.2, moderado:1.375, activo:1.55};
  var tdee = bmr * (actF[p.actividad] || 1.375);
  var kcal, prot;
  if (p.meta === 'bajar_grasa') { kcal = Math.round(tdee - 400); prot = Math.round(p.peso * 2.2); }
  else if (p.meta === 'ganar_musculo') { kcal = Math.round(tdee + 300); prot = Math.round(p.peso * 2.0); }
  else { kcal = Math.round(tdee - 200); prot = Math.round(p.peso * 2.1); }
  var grasas = Math.round((kcal * 0.25) / 9);
  var carbos = Math.round((kcal - prot*4 - grasas*9) / 4);
  return { kcal:kcal, proteina:prot, carbos:carbos, grasas:grasas, tdee:Math.round(tdee), diasGym:p.diasGym||4 };
}

function getUserPlan(u) {
  return u.plan || generatePlan(u);
}

function getRoutines(diasGym) {
  if (diasGym <= 3) return ROUTINES_3;
  if (diasGym >= 5) return ROUTINES_5;
  return ROUTINES_4;
}

// ══════════════════════════════════════════════
// SCORE CALCULATOR
// ══════════════════════════════════════════════
function calcScore(u) {
  var score = 0;
  var kgBajados = (u.pesoInicial || u.peso) - getLatestPeso(u);
  if (u.meta === 'bajar_grasa' || u.meta === 'recomposicion') {
    if (kgBajados > 0) score += kgBajados * 10;
  } else {
    // muscle gain: reward consistency more than weight
  }
  score += (u.gymLogs ? u.gymLogs.length : 0) * 3;
  var planMeals = u.meals ? u.meals.filter(function(m){ return m.onPlan; }).length : 0;
  score += planMeals * 2;
  return Math.round(score);
}

function getLatestPeso(u) {
  if (!u.medidas || !u.medidas.length) return u.peso;
  var sorted = u.medidas.slice().sort(function(a,b){ return b.date > a.date ? 1 : -1; });
  return sorted[0].peso || u.peso;
}

// ══════════════════════════════════════════════
// NAVIGATION
// ══════════════════════════════════════════════
function goPage(id, btn) {
  var pages = document.querySelectorAll('.page');
  for (var i = 0; i < pages.length; i++) pages[i].classList.remove('on');
  var nbs = document.querySelectorAll('.nb');
  for (var i = 0; i < nbs.length; i++) nbs[i].classList.remove('on');
  document.getElementById(id).classList.add('on');
  if (btn) btn.classList.add('on');
  else {
    var sel = document.querySelector('.nb[onclick*="' + id + '"]');
    if (sel) sel.classList.add('on');
  }
  if (id === 'page-home') renderHome();
  if (id === 'page-rutinas') renderRutinas();
  if (id === 'page-prog') { renderProg(); drawWeightChart(); }
  if (id === 'page-log') renderLog('gym');
  if (id === 'page-comp') renderComp();
}

function showApp() {
  document.getElementById('main-nav').style.display = 'flex';
  goPage('page-home', document.querySelector('.nb'));
}

// ══════════════════════════════════════════════
// UTILS
// ══════════════════════════════════════════════
function today() { return new Date().toISOString().split('T')[0]; }

function fmtDate(s) {
  if (!s) return '';
  var d = new Date(s + 'T12:00:00');
  return d.toLocaleDateString('es-MX', {day:'numeric', month:'short'});
}

function weekStart() {
  var n = new Date(), dow = n.getDay(), diff = dow===0?6:dow-1, m = new Date(n);
  m.setDate(n.getDate()-diff); return m.toISOString().split('T')[0];
}

function getCompWeek() {
  var start = DB.competition.startDate || today();
  var s = new Date(start + 'T12:00:00');
  var diff = Math.floor((new Date()-s)/86400000);
  return Math.min(Math.floor(diff/7)+1, COMPETITION_WEEKS);
}

function getCompProgress() {
  var start = DB.competition.startDate || today();
  var s = new Date(start+'T12:00:00');
  var totalDays = COMPETITION_WEEKS * 7;
  var elapsed = Math.floor((new Date()-s)/86400000);
  return Math.min(elapsed/totalDays, 1);
}

function getDaysLeft() {
  var start = DB.competition.startDate || today();
  var s = new Date(start+'T12:00:00');
  var totalDays = COMPETITION_WEEKS * 7;
  var elapsed = Math.floor((new Date()-s)/86400000);
  return Math.max(totalDays - elapsed, 0);
}

function openM(id) {
  var dMap = {'o-gym':'gl-d','o-meal':'ml-d','o-med':'md-d'};
  if (dMap[id]) document.getElementById(dMap[id]).value = today();
  // populate gym day selector
  if (id === 'o-gym') {
    var u = DB.users[currentUser];
    var ruts = getRoutines(u.diasGym||4);
    var sel = document.getElementById('gl-day');
    sel.innerHTML = '';
    for (var i = 0; i < ruts.length; i++) {
      var o = document.createElement('option');
      o.textContent = ruts[i].day + ' — ' + ruts[i].name;
      sel.appendChild(o);
    }
  }
  document.getElementById(id).classList.add('on');
}
function closeM(id) { document.getElementById(id).classList.remove('on'); }

// ══════════════════════════════════════════════
// HOME RENDER
// ══════════════════════════════════════════════
function renderHome() {
  var u = DB.users[currentUser];
  if (!u) return;
  var dayNames = ['DOMINGO','LUNES','MARTES','MIÉRCOLES','JUEVES','VIERNES','SÁBADO'];
  var dow = new Date().getDay();
  var dias = u.diasGym || 4;
  var focusMap = FOCUS_MAP[dias] || FOCUS_MAP[4];

  document.getElementById('home-username').textContent = u.nombre || currentUser;
  document.getElementById('home-dayname').textContent = dayNames[dow];
  document.getElementById('home-focus').textContent = focusMap[dow];
  document.getElementById('home-week').textContent = 'SEM ' + getCompWeek();
  document.getElementById('home-sub').textContent = 'Semana ' + getCompWeek() + ' de ' + COMPETITION_WEEKS;

  // week strip
  var ws = weekStart();
  var labels = ['L','M','X','J','V','S','D'];
  var mapDow = [6,0,1,2,3,4,5];
  var todayIdx = mapDow[dow];
  var html = '';
  for (var i = 0; i < 7; i++) {
    var dd = new Date(ws+'T12:00:00'); dd.setDate(dd.getDate()+i);
    var ds = dd.toISOString().split('T')[0];
    var done = false;
    for (var j = 0; j < u.gymLogs.length; j++) { if (u.gymLogs[j].date === ds) { done=true; break; } }
    var cls = done ? 'wd d' : (todayIdx===i ? 'wd t' : 'wd');
    html += '<div class="' + cls + '"><span>' + (done?'✓':labels[i]) + '</span>' + labels[i] + '</div>';
  }
  document.getElementById('home-strip').innerHTML = html;

  // kpis
  var latestPeso = getLatestPeso(u);
  document.getElementById('h-peso').textContent = latestPeso || '—';
  if (u.medidas && u.medidas.length > 1) {
    var sorted = u.medidas.slice().sort(function(a,b){return b.date>a.date?1:-1;});
    var dp = sorted[0].peso && sorted[1].peso ? (sorted[0].peso - sorted[1].peso).toFixed(1) : null;
    if (dp !== null) {
      var epEl = document.getElementById('h-pd');
      epEl.textContent = (parseFloat(dp)>0?'+':'')+dp+' kg';
      epEl.className = 'kdelta '+(parseFloat(dp)<0?'dn':'up');
    }
  }
  var score = calcScore(u);
  document.getElementById('h-score').textContent = score;
  // rank
  var allScores = Object.keys(DB.users).map(function(k){ return calcScore(DB.users[k]); }).sort(function(a,b){return b-a;});
  var rank = allScores.indexOf(score) + 1;
  document.getElementById('h-rank').textContent = '#' + rank + ' de ' + Object.keys(DB.users).length;

  // routine preview
  var ruts = getRoutines(dias);
  var dayRut = ruts[dow] || ruts[0];
  document.getElementById('h-rname').textContent = dayRut.name;
  var exHtml = '';
  var lim = Math.min(dayRut.ex.length, 4);
  for (var i = 0; i < lim; i++) {
    exHtml += '<div class="ex-row"><span class="ex-n">'+dayRut.ex[i].n+'</span><span class="ex-s'+(dayRut.ex[i].c?' c':'')+'">'+dayRut.ex[i].s+'</span></div>';
  }
  if (dayRut.ex.length > 4) exHtml += '<div style="font-size:11px;color:var(--muted);padding:8px 0;">+'+(dayRut.ex.length-4)+' más...</div>';
  document.getElementById('h-rex').innerHTML = exHtml;
}

// ══════════════════════════════════════════════
// RUTINAS RENDER
// ══════════════════════════════════════════════
function renderRutinas() {
  var u = DB.users[currentUser];
  if (!u) return;
  var ruts = getRoutines(u.diasGym||4);
  var plan = getUserPlan(u);

  document.getElementById('rut-sub').textContent = u.diasGym + ' días/semana · ' + (u.meta==='bajar_grasa'?'Bajar grasa':u.meta==='ganar_musculo'?'Ganar músculo':'Recomposición');

  var tabsHtml = '';
  for (var i = 0; i < ruts.length; i++) {
    tabsHtml += '<div class="tab'+(i===0?' on':'')+'" onclick="selRut('+i+',this)">'+ruts[i].day+'</div>';
  }
  document.getElementById('rut-tabs').innerHTML = tabsHtml;
  renderRutDay(0, ruts);

  // macros card
  var metaLabel = u.meta==='bajar_grasa'?'Bajar grasa 🔥':u.meta==='ganar_musculo'?'Ganar músculo 📈':'Recomposición 💪';
  document.getElementById('rut-macros').innerHTML =
    '<div style="font-family:\'DM Mono\',monospace;font-size:10px;color:var(--muted);letter-spacing:.12em;margin-bottom:10px;">META: '+metaLabel+'</div>' +
    '<div style="display:flex;gap:8px;flex-wrap:wrap;">' +
    '<span class="mac" style="background:rgba(255,124,42,.1);color:var(--orange);">'+plan.kcal+' kcal/día</span>' +
    '<span class="mac">Prot: '+plan.proteina+'g</span>' +
    '<span class="mac">Carb: '+plan.carbos+'g</span>' +
    '<span class="mac">Gras: '+plan.grasas+'g</span>' +
    '</div>' +
    '<p style="margin-top:10px;font-size:12px;color:var(--muted);">Tu mantenimiento estimado: '+plan.tdee+' kcal. '+(u.meta==='bajar_grasa'?'Déficit de ~400 kcal para quemar grasa sin perder músculo.':u.meta==='ganar_musculo'?'Superávit de ~300 kcal para crecer músculo.':'Déficit leve de ~200 kcal para recomposición.')+'</p>';

  // meal plan adapted to calories
  renderMealPlan(plan, u.meta);
}

var _currentRuts = null;
function selRut(i, el) {
  var tabs = document.querySelectorAll('#rut-tabs .tab');
  for (var j=0;j<tabs.length;j++) tabs[j].classList.remove('on');
  el.classList.add('on');
  var u = DB.users[currentUser];
  renderRutDay(i, getRoutines(u.diasGym||4));
}

function renderRutDay(i, ruts) {
  var r = ruts[i];
  var exHtml = '';
  for (var j=0;j<r.ex.length;j++) {
    exHtml += '<div class="ex-row"><span class="ex-n">'+r.ex[j].n+'</span><span class="ex-s'+(r.ex[j].c?' c':'')+'">'+r.ex[j].s+'</span></div>';
  }
  document.getElementById('rut-content').innerHTML =
    '<div class="card"><div style="display:flex;justify-content:space-between;align-items:flex-start;margin-bottom:12px;">'+
    '<div><div style="font-family:\'DM Mono\',monospace;font-size:10px;color:var(--muted);letter-spacing:.12em;margin-bottom:4px;">'+r.day+'</div>'+
    '<div class="c-title" style="margin:0;">'+r.name+'</div></div>'+
    '<button class="btn btn-s" onclick="openM(\'o-gym\')">+ Log</button></div>'+
    exHtml+
    '<button class="btn btn-p" style="margin-top:16px;" onclick="openM(\'o-gym\')">Registrar entreno</button></div>';
}

function renderMealPlan(plan, meta) {
  var desayuno, snack, comida, preEntreno, cena;
  var kcal = plan.kcal;

  if (meta === 'bajar_grasa') {
    desayuno = {t:'07:00',n:'Arranque proteico',items:['4 claras + 2 huevos enteros','80g avena con agua','½ plátano o manzana','Café negro sin azúcar'],kcal:Math.round(kcal*.3)};
    snack    = {t:'10:30',n:'Colación',items:['200g yogur griego 0%','Frutos rojos','Canela al gusto'],kcal:Math.round(kcal*.1)};
    comida   = {t:'13:30',n:'La principal',items:['200g proteína magra (pollo/pavo/res)','120g arroz integral o camote','Ensalada grande','1 cdita aceite oliva'],kcal:Math.round(kcal*.3)};
    preEntreno={t:'16:30',n:'Pre-entreno',items:['100g atún en agua','2 rebanadas pan integral','Jitomate + mostaza'],kcal:Math.round(kcal*.15)};
    cena     = {t:'20:00',n:'Cena proteica',items:['200g proteína (salmón/pollo/res)','Verduras al vapor','½ taza frijoles o lentejas'],kcal:Math.round(kcal*.15)};
  } else if (meta === 'ganar_musculo') {
    desayuno = {t:'07:00',n:'Desayuno anabólico',items:['4 huevos enteros + 2 claras','150g avena con leche','1 plátano entero','30g nueces'],kcal:Math.round(kcal*.28)};
    snack    = {t:'10:30',n:'Colación',items:['200g yogur griego','Granola sin azúcar (30g)','Fruta de temporada'],kcal:Math.round(kcal*.12)};
    comida   = {t:'13:30',n:'La principal',items:['250g proteína (pollo/res/cerdo magro)','200g arroz blanco o papa','Ensalada + aguacate'],kcal:Math.round(kcal*.32)};
    preEntreno={t:'16:30',n:'Pre-entreno',items:['2 rebanadas pan integral','2 cucharadas crema cacahuate','1 plátano'],kcal:Math.round(kcal*.14)};
    cena     = {t:'20:00',n:'Cena',items:['200g proteína','Camote o arroz (100g)','Verduras salteadas'],kcal:Math.round(kcal*.14)};
  } else {
    desayuno = {t:'07:00',n:'Desayuno equilibrado',items:['3 huevos enteros + 2 claras','100g avena con agua','1 manzana o plátano','Café negro'],kcal:Math.round(kcal*.29)};
    snack    = {t:'10:30',n:'Colación',items:['200g yogur griego','Frutos rojos o naranja'],kcal:Math.round(kcal*.1)};
    comida   = {t:'13:30',n:'La principal',items:['200g proteína magra','120g arroz o camote','Ensalada grande'],kcal:Math.round(kcal*.3)};
    preEntreno={t:'16:30',n:'Pre-entreno',items:['100g atún o pechuga','2 rebanadas pan integral','Jitomate + mostaza'],kcal:Math.round(kcal*.16)};
    cena     = {t:'20:00',n:'Cena',items:['200g proteína','Verduras al vapor','Frijoles o lentejas'],kcal:Math.round(kcal*.15)};
  }

  var meals = [desayuno, snack, comida, preEntreno, cena];
  var html = '';
  for (var i=0;i<meals.length;i++) {
    var m = meals[i];
    var items = '';
    for (var j=0;j<m.items.length;j++) items += '<li>'+m.items[j]+'</li>';
    html += '<div class="mc"><div class="mt">'+m.t+'</div><div class="mn">'+m.n+'</div><ul class="mi">'+items+'</ul>'+
      '<div class="mm"><span class="mac" style="background:rgba(255,124,42,.1);color:var(--orange);">~'+m.kcal+' kcal</span></div></div>';
  }
  html += '<div class="mc" style="margin-bottom:20px;"><div class="mn">Total diario</div>'+
    '<div class="mm"><span class="mac" style="background:rgba(61,224,122,.1);color:var(--green);">'+plan.kcal+' kcal</span>'+
    '<span class="mac">Proteína: '+plan.proteina+'g</span></div></div>';
  document.getElementById('rut-meals').innerHTML = html;
}

// ══════════════════════════════════════════════
// LOG
// ══════════════════════════════════════════════
var gymInt = 2;
function setInt(v, btn) {
  gymInt = v;
  var btns = document.querySelectorAll('#o-gym .btn-s');
  for (var i=0;i<btns.length;i++) btns[i].classList.remove('on');
  btn.classList.add('on');
}

function saveGym() {
  var u = DB.users[currentUser];
  if (!u) return;
  var intL = {1:'Suave',2:'Normal',3:'Brutal'};
  u.gymLogs.push({
    date: document.getElementById('gl-d').value,
    day: document.getElementById('gl-day').value,
    dur: parseInt(document.getElementById('gl-dur').value)||null,
    intensity: intL[gymInt],
    notas: document.getElementById('gl-n').value.trim(),
    ts: Date.now()
  });
  saveDB(); closeM('o-gym');
  document.getElementById('gl-n').value=''; document.getElementById('gl-dur').value='';
  renderHome(); renderLog('gym');
}

var mealOnPlan = true;
function setPlan(v) {
  mealOnPlan = v;
  document.getElementById('pl-si').className='btn btn-s'+(v?' on':'');
  document.getElementById('pl-no').className='btn btn-s'+(!v?' on':'');
}

function saveMeal() {
  var u = DB.users[currentUser];
  if (!u) return;
  var food = document.getElementById('ml-f').value.trim();
  if (!food) { alert('Escribe qué comiste'); return; }
  u.meals.push({
    date: document.getElementById('ml-d').value,
    tiempo: document.getElementById('ml-t').value,
    food: food, onPlan: mealOnPlan,
    agua: parseFloat(document.getElementById('ml-a').value)||null,
    ts: Date.now()
  });
  saveDB(); closeM('o-meal');
  document.getElementById('ml-f').value=''; document.getElementById('ml-a').value='';
  renderHome();
}

function saveMed() {
  var u = DB.users[currentUser];
  if (!u) return;
  var peso = parseFloat(document.getElementById('md-p').value)||null;
  var cin = parseFloat(document.getElementById('md-c').value)||null;
  if (!peso && !cin) { alert('Ingresa al menos peso o cintura'); return; }
  u.medidas.push({
    date: document.getElementById('md-d').value,
    peso: peso, cintura: cin,
    pecho: parseFloat(document.getElementById('md-pe').value)||null,
    cadera: parseFloat(document.getElementById('md-ca').value)||null,
    brazo: parseFloat(document.getElementById('md-b').value)||null,
    notas: document.getElementById('md-n').value.trim(),
    ts: Date.now()
  });
  saveDB(); closeM('o-med');
  ['md-p','md-c','md-pe','md-ca','md-b','md-n'].forEach(function(id){ document.getElementById(id).value=''; });
  renderHome(); renderProg(); drawWeightChart();
}

function logTab(id, el) {
  var tabs = document.querySelectorAll('.tabs .tab');
  for (var i=0;i<tabs.length;i++) tabs[i].classList.remove('on');
  el.classList.add('on');
  document.getElementById('log-gym-list').style.display = id==='gym'?'block':'none';
  document.getElementById('log-comida-list').style.display = id==='comida'?'block':'none';
  document.getElementById('log-medidas-list').style.display = id==='medidas'?'block':'none';
  renderLog(id);
}

function renderLog(type) {
  var u = DB.users[currentUser];
  if (!u) return;

  if (type === 'gym') {
    var el = document.getElementById('log-gym-list');
    if (!u.gymLogs.length) { el.innerHTML='<div class="empty"><div class="ei">🏋️</div><p>Sin entrenos aún.<br>Toca "+ Log" para empezar.</p></div>'; return; }
    var sorted = u.gymLogs.slice().sort(function(a,b){return b.date>a.date?1:-1;});
    var ic={Suave:'😐',Normal:'💪',Brutal:'🔥'}, cc={Suave:'#4db8ff',Normal:'var(--orange)',Brutal:'var(--red)'};
    var html='', last='';
    for (var i=0;i<sorted.length;i++) {
      var g=sorted[i];
      if (g.date!==last){last=g.date;html+='<div class="sl">'+fmtDate(g.date)+'</div>';}
      html+='<div class="lr"><div class="lr-top"><span class="lr-date" style="color:'+(cc[g.intensity]||'var(--muted)')+';">'+(ic[g.intensity]||'')+' '+g.intensity+'</span>'+(g.dur?'<span style="font-family:\'DM Mono\',monospace;font-size:10px;color:var(--muted);">⏱ '+g.dur+' min</span>':'')+
        '</div><div class="lr-body" style="margin-top:4px;">'+g.day+'</div>'+(g.notas?'<div style="font-size:12px;color:var(--muted);margin-top:4px;">'+g.notas+'</div>':'')+
        '</div>';
    }
    el.innerHTML = html;
  }

  if (type === 'comida') {
    var el = document.getElementById('log-comida-list');
    if (!u.meals.length) { el.innerHTML='<div class="empty"><div class="ei">🍽️</div><p>Sin comidas registradas.</p></div>'; return; }
    var sorted = u.meals.slice().sort(function(a,b){return b.date>a.date?1:-1;});
    var html='', last='';
    for (var i=0;i<sorted.length;i++) {
      var m=sorted[i];
      if (m.date!==last){last=m.date;html+='<div class="sl">'+fmtDate(m.date)+'</div>';}
      html+='<div class="lr"><div class="lr-top"><span class="lr-date">'+m.tiempo+'</span>'+(m.agua?'<span style="font-family:\'DM Mono\',monospace;font-size:10px;color:#4db8ff;">💧 '+m.agua+'L</span>':'')+
        '</div><div class="lr-body">'+m.food+'</div><span class="tag'+(m.onPlan?' g':'')+'">'+( m.onPlan?'✓ Siguió el plan':'~ Fuera del plan')+'</span></div>';
    }
    el.innerHTML = html;
  }

  if (type === 'medidas') {
    var el = document.getElementById('log-medidas-list');
    if (!u.medidas.length) { el.innerHTML='<div class="empty"><div class="ei">📏</div><p>Sin medidas aún.</p></div>'; return; }
    var sorted = u.medidas.slice().sort(function(a,b){return b.date>a.date?1:-1;});
    var html='';
    for (var i=0;i<sorted.length;i++) {
      var m=sorted[i], prev=sorted[i+1]||null;
      var dp = (m.peso&&prev&&prev.peso)?(m.peso-prev.peso).toFixed(1):null;
      var det='';
      if (m.peso) { var dc2=dp!==null?('<span style="font-size:11px;margin-left:4px;color:'+(parseFloat(dp)<0?'var(--green)':'var(--red)')+';">'+(parseFloat(dp)>0?'+':'')+dp+'</span>'):''; det+='<div><span style="font-family:\'Bebas Neue\',cursive;font-size:20px;">'+m.peso+'</span><span style="font-family:\'DM Mono\',monospace;font-size:10px;color:var(--muted);"> kg</span>'+dc2+'</div>'; }
      if (m.cintura) det+='<div style="font-size:12px;color:var(--muted2);">Cintura: '+m.cintura+'cm</div>';
      if (m.pecho)   det+='<div style="font-size:12px;color:var(--muted2);">Pecho: '+m.pecho+'cm</div>';
      html+='<div class="lr"><div class="lr-top"><span class="lr-date">'+fmtDate(m.date)+'</span>'+(m.notas?'<span style="font-size:11px;color:var(--muted);">'+m.notas+'</span>':'')+
        '</div><div style="display:flex;gap:12px;flex-wrap:wrap;margin-top:6px;">'+det+'</div></div>';
    }
    el.innerHTML = html;
  }
}

// ══════════════════════════════════════════════
// PROGRESS CHART
// ══════════════════════════════════════════════
function renderProg() {
  var u = DB.users[currentUser];
  if (!u) return;
  renderLog('medidas');
}

function drawWeightChart() {
  var u = DB.users[currentUser];
  if (!u) return;
  var data = u.medidas.filter(function(m){return m.peso;}).sort(function(a,b){return a.date>b.date?1:-1;}).map(function(m){return{x:fmtDate(m.date),y:m.peso};});
  drawChart('c-peso', data, '#ff3c3c', Math.max(u.peso-15,40), u.peso+5);
}

function drawChart(id, data, color, yMin, yMax) {
  var cv = document.getElementById(id);
  if (!cv) return;
  var ctx = cv.getContext('2d');
  var W = cv.offsetWidth||320, H = parseInt(cv.getAttribute('height'))||110;
  var dpr = window.devicePixelRatio||1;
  cv.width=W*dpr; cv.height=H*dpr; ctx.scale(dpr,dpr);
  ctx.clearRect(0,0,W,H);
  if (!data.length) { ctx.fillStyle='#333'; ctx.font='12px DM Sans,sans-serif'; ctx.textAlign='center'; ctx.fillText('Sin datos aún',W/2,H/2); return; }
  var pad={l:36,r:12,t:8,b:28}, iW=W-pad.l-pad.r, iH=H-pad.t-pad.b;
  var vals=data.map(function(d){return d.y;}), lo=Math.min.apply(null,vals.concat([yMin])), hi=Math.max.apply(null,vals.concat([yMax])), rng=hi-lo||1;
  function tx(i){return pad.l+(data.length<2?iW/2:i/(data.length-1)*iW);}
  function ty(v){return pad.t+iH-((v-lo)/rng*iH);}
  for (var i=0;i<=3;i++){var y=pad.t+(i/3)*iH;ctx.strokeStyle='#1e1e1e';ctx.lineWidth=1;ctx.beginPath();ctx.moveTo(pad.l,y);ctx.lineTo(W-pad.r,y);ctx.stroke();ctx.fillStyle='#444';ctx.font='9px DM Mono,monospace';ctx.textAlign='right';ctx.fillText((hi-(i/3)*rng).toFixed(1),pad.l-4,y+3);}
  if (data.length>1){ctx.beginPath();ctx.moveTo(tx(0),ty(data[0].y));for(var i=1;i<data.length;i++)ctx.lineTo(tx(i),ty(data[i].y));ctx.lineTo(tx(data.length-1),H-pad.b);ctx.lineTo(tx(0),H-pad.b);ctx.closePath();var g=ctx.createLinearGradient(0,pad.t,0,H-pad.b);g.addColorStop(0,color+'30');g.addColorStop(1,color+'00');ctx.fillStyle=g;ctx.fill();ctx.beginPath();ctx.strokeStyle=color;ctx.lineWidth=2;ctx.lineJoin='round';ctx.moveTo(tx(0),ty(data[0].y));for(var i=1;i<data.length;i++)ctx.lineTo(tx(i),ty(data[i].y));ctx.stroke();}
  for(var i=0;i<data.length;i++){ctx.beginPath();ctx.arc(tx(i),ty(data[i].y),3.5,0,Math.PI*2);ctx.fillStyle=color;ctx.fill();if(data.length<=6||i===0||i===data.length-1){ctx.fillStyle='#555';ctx.font='9px DM Mono,monospace';ctx.textAlign='center';ctx.fillText(data[i].x,tx(i),H-pad.b+16);}}
}

// ══════════════════════════════════════════════
// COMPETITION
// ══════════════════════════════════════════════
function renderComp() {
  var sem = getCompWeek();
  var pct = getCompProgress();
  var daysLeft = getDaysLeft();
  var isOver = pct >= 1;

  document.getElementById('comp-semana').textContent = isOver ? 'FINAL' : 'SEM '+sem;
  document.getElementById('comp-dias-left').textContent = isOver ? '¡Competencia terminada!' : daysLeft+' días restantes';
  document.getElementById('comp-pct').textContent = Math.round(pct*100)+'%';
  document.getElementById('comp-prog').style.width = Math.round(pct*100)+'%';

  // build ranked list
  var userKeys = Object.keys(DB.users);
  var ranked = userKeys.map(function(k){
    var u = DB.users[k];
    return {
      key: k,
      nombre: u.nombre || k,
      score: calcScore(u),
      gymDias: u.gymLogs ? u.gymLogs.length : 0,
      dietaDias: u.meals ? u.meals.filter(function(m){return m.onPlan;}).length : 0,
      kgBajados: Math.max(0, (u.pesoInicial||u.peso) - getLatestPeso(u)).toFixed(1),
      meta: u.meta
    };
  }).sort(function(a,b){return b.score-a.score;});

  var maxScore = ranked.length > 0 ? ranked[0].score : 1;

  // winner banner (only if competition over OR if someone has a big lead)
  var winnerHtml = '';
  if (isOver && ranked.length > 0) {
    var winner = ranked[0];
    winnerHtml = '<div class="winner-banner"><div class="winner-crown">🏆</div>'+
      '<div class="winner-title">GANADOR DEL RETO</div>'+
      '<div class="winner-name">'+winner.nombre.toUpperCase()+'</div>'+
      '<div class="winner-pts">'+winner.score+' puntos finales</div></div>';
  }
  document.getElementById('comp-winner').innerHTML = winnerHtml;

  // leaderboard
  var rankIcons = ['🥇','🥈','🥉'];
  var lbHtml = '<div class="lb-card">';
  for (var i=0;i<ranked.length;i++) {
    var r = ranked[i];
    var isMe = r.key === currentUser;
    var rankCls = i===0?'r1':i===1?'r2':i===2?'r3':'';
    var barW = maxScore > 0 ? Math.round((r.score/maxScore)*100) : 0;
    var metaEmoji = r.meta==='bajar_grasa'?'🔥':r.meta==='ganar_musculo'?'💪':'⚡';
    lbHtml += '<div class="lb-row'+(isMe?' me':'')+'">'+
      '<div class="lb-rank '+rankCls+'">'+(i<3?rankIcons[i]:(i+1))+'</div>'+
      '<div class="lb-info">'+
        '<div class="lb-name">'+(isMe?'<span style="color:var(--orange);">★ </span>':'')+r.nombre+' '+metaEmoji+'</div>'+
        '<div class="lb-meta">🏋️ '+r.gymDias+'d gym · 🥗 '+r.dietaDias+'d dieta · ⬇️ '+r.kgBajados+'kg</div>'+
        '<div class="lb-bar-wrap"><div class="lb-bar" style="width:'+barW+'%;"></div></div>'+
      '</div>'+
      '<div class="lb-score"><div class="lb-pts">'+r.score+'</div><div class="lb-ptsl">pts</div></div>'+
    '</div>';
  }
  if (!ranked.length) lbHtml += '<div class="empty"><div class="ei">👥</div><p>Aún no hay participantes.</p></div>';
  lbHtml += '</div>';
  document.getElementById('comp-lb').innerHTML = lbHtml;

  // group stats
  var totalGym = ranked.reduce(function(s,r){return s+r.gymDias;},0);
  var totalDieta = ranked.reduce(function(s,r){return s+r.dietaDias;},0);
  var totalKg = ranked.reduce(function(s,r){return s+parseFloat(r.kgBajados);},0).toFixed(1);
  document.getElementById('comp-stats').innerHTML =
    '<div class="c-title">El grupo completo</div>'+
    '<div style="display:grid;grid-template-columns:1fr 1fr 1fr;gap:10px;text-align:center;">'+
    '<div><div style="font-family:\'Bebas Neue\',cursive;font-size:26px;color:var(--green);">'+totalGym+'</div><div style="font-family:\'DM Mono\',monospace;font-size:9px;color:var(--muted);">DÍAS GYM</div></div>'+
    '<div><div style="font-family:\'Bebas Neue\',cursive;font-size:26px;color:var(--orange);">'+totalDieta+'</div><div style="font-family:\'DM Mono\',monospace;font-size:9px;color:var(--muted);">DÍAS DIETA</div></div>'+
    '<div><div style="font-family:\'Bebas Neue\',cursive;font-size:26px;color:var(--red);">'+totalKg+'</div><div style="font-family:\'DM Mono\',monospace;font-size:9px;color:var(--muted);">KG BAJADOS</div></div>'+
    '</div>'+
    '<p style="margin-top:12px;font-size:12px;color:var(--muted);">Score = (kg perdidos×10) + (días gym×3) + (días dieta cumplida×2)</p>';
}

// ══════════════════════════════════════════════
// INIT
// ══════════════════════════════════════════════
loadDB();
// Show login
goPage('page-login');
</script>

</body>
</html>
