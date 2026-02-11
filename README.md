<!doctype html>
<html lang="es">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>GO OLIVERITO GO</title>
  <style>
    :root{
      --bg:#0b1020; --card:#121a33; --muted:#9fb0ff;
      --text:#eaf0ff; --accent:#5eead4; --warn:#ffcc66; --bad:#ff6b6b;
      --good:#7CFF9B; --coin:#ffd166;
    }
    *{box-sizing:border-box;font-family:system-ui,-apple-system,Segoe UI,Roboto,Ubuntu,Cantarell,Noto Sans,sans-serif}
    body{margin:0;background:radial-gradient(900px 500px at 15% 10%, #1a2455 0%, var(--bg) 45%), var(--bg); color:var(--text);}
    .wrap{max-width:980px;margin:0 auto;padding:18px}
    h1{margin:8px 0 4px;font-size:22px}
    .sub{color:var(--muted);margin:0 0 14px}
    .grid{display:grid;grid-template-columns:1.2fr .8fr;gap:14px}
    @media (max-width:900px){.grid{grid-template-columns:1fr}}
    .card{background:linear-gradient(180deg, rgba(255,255,255,.06), rgba(255,255,255,.03));
      border:1px solid rgba(255,255,255,.12); border-radius:14px; padding:14px}
    .row{display:flex;gap:10px;flex-wrap:wrap;align-items:center}
    .stat{padding:10px 12px;border-radius:12px;background:rgba(255,255,255,.06);border:1px solid rgba(255,255,255,.10)}
    .stat b{display:block;font-size:12px;color:var(--muted);font-weight:600}
    .stat span{font-size:16px}
    .hearts{letter-spacing:2px}
    .bar{height:10px;border-radius:999px;background:rgba(255,255,255,.08);overflow:hidden;border:1px solid rgba(255,255,255,.12)}
    .fill{height:100%;background:linear-gradient(90deg,var(--accent),#60a5fa);width:0%}
    .qbox{padding:14px;border-radius:14px;background:rgba(0,0,0,.15);border:1px solid rgba(255,255,255,.10)}
    .q{font-size:28px;font-weight:750;letter-spacing:.2px}
    .mini{color:var(--muted);font-size:13px;margin-top:6px}
    .inputRow{display:flex;gap:10px;flex-wrap:wrap;margin-top:12px}
    input[type="text"]{flex:1;min-width:180px;padding:12px 12px;border-radius:12px;border:1px solid rgba(255,255,255,.14);
      background:rgba(0,0,0,.25);color:var(--text);font-size:16px}
    button{padding:11px 12px;border-radius:12px;border:1px solid rgba(255,255,255,.14);
      background:rgba(255,255,255,.08);color:var(--text);cursor:pointer}
    button:hover{background:rgba(255,255,255,.12)}
    button.primary{background:linear-gradient(90deg,var(--accent),#60a5fa);color:#06101b;border:none;font-weight:700}
    button.primary:hover{filter:brightness(1.05)}
    button.danger{background:rgba(255,107,107,.15);border-color:rgba(255,107,107,.35)}
    button.good{background:rgba(124,255,155,.14);border-color:rgba(124,255,155,.35)}
    button:disabled{opacity:.5;cursor:not-allowed}
    .msg{margin-top:10px;min-height:22px}
    .msg .ok{color:var(--good)}
    .msg .bad{color:var(--bad)}
    .msg .warn{color:var(--warn)}
    .shop{display:grid;grid-template-columns:1fr;gap:10px}
    .item{display:flex;justify-content:space-between;align-items:center;gap:10px;padding:10px;border-radius:12px;
      background:rgba(255,255,255,.05);border:1px solid rgba(255,255,255,.10)}
    .item .left{display:flex;flex-direction:column;gap:2px}
    .item .left .t{font-weight:700}
    .item .left .d{color:var(--muted);font-size:12px}
    .pill{padding:4px 9px;border-radius:999px;background:rgba(255,209,102,.12);border:1px solid rgba(255,209,102,.35);color:var(--coin);font-weight:700;font-size:12px}
    .log{max-height:220px;overflow:auto;padding-right:6px}
    .log p{margin:8px 0;color:rgba(234,240,255,.92);font-size:13px}
    .log small{color:var(--muted)}
    .footer{color:var(--muted);font-size:12px;margin-top:10px}
    .kbd{font-family:ui-monospace,SFMono-Regular,Menlo,Monaco,Consolas,monospace;font-size:12px;padding:2px 6px;border:1px solid rgba(255,255,255,.18);
      border-bottom-width:2px;border-radius:8px;background:rgba(0,0,0,.25);color:rgba(234,240,255,.92)}
  </style>
</head>
<body>
  <div class="wrap">
    <h1>GO OLIVERITO GO</h1>
    <p class="sub">Resuelve aritmética para ganar XP, monedas y subir de nivel. Si fallas, pierdes vida.</p>

    <div class="grid">
      <div class="card">
        <div class="row" style="margin-bottom:12px">
          <div class="stat"><b>Nivel</b><span id="lvl">1</span></div>
          <div class="stat"><b>XP</b><span id="xp">0</span> <span style="color:var(--muted)">/</span> <span id="xpNext">50</span></div>
          <div class="stat"><b>Vida</b><span class="hearts" id="hp">♥♥♥</span></div>
          <div class="stat"><b>Monedas</b><span id="coins">0</span> <span style="color:var(--coin)">●</span></div>
          <div class="stat"><b>Racha</b><span id="streak">0</span></div>
          <div class="stat"><b>Tiempo</b><span id="time">25</span>s</div>
        </div>

        <div class="bar" aria-label="barra xp"><div class="fill" id="xpBar"></div></div>

        <div class="qbox" style="margin-top:12px">
          <div class="row" style="justify-content:space-between">
            <div>
              <div class="q" id="question">Pulsa Iniciar</div>
              <div class="mini" id="qmeta">Modo: entrenamiento</div>
            </div>
            <div class="row">
              <button id="btnStart" class="primary">Iniciar</button>
              <button id="btnPause">Pausar</button>
              <button id="btnReset" class="danger">Reiniciar</button>
            </div>
          </div>

          <div class="inputRow">
            <input id="answer" type="text" inputmode="numeric" placeholder="Escribe tu respuesta…" autocomplete="off" />
            <button id="btnSubmit" class="good" disabled>Enviar (<span class="kbd">Enter</span>)</button>
            <button id="btnSkip" disabled>Re-roll</button>
          </div>

          <div class="msg" id="msg"></div>
        </div>

        <div class="footer">
          Consejos: Enter para enviar. Usa la tienda para comprar “pista”, “escudo” o “doble XP”. Guardado automático en este navegador.
        </div>
      </div>

      <div class="card">
        <h2 style="margin:0 0 10px;font-size:16px">HelicoTienda</h2>
        <div class="shop">
          <div class="item">
            <div class="left">
              <div class="t">Poción de vida <span class="pill">25</span></div>
              <div class="d">+1 corazón (máx. 5).</div>
            </div>
            <button id="buyLife">Comprar</button>
          </div>
          <div class="item">
            <div class="left">
              <div class="t">Pista <span class="pill">12</span></div>
              <div class="d">Muestra un paso o simplifica números (sin dar el resultado).</div>
            </div>
            <button id="buyHint">Comprar</button>
          </div>
          <div class="item">
            <div class="left">
              <div class="t">Escudo <span class="pill">18</span></div>
              <div class="d">Anula la próxima pérdida de vida.</div>
            </div>
            <button id="buyShield">Comprar</button>
          </div>
          <div class="item">
            <div class="left">
              <div class="t">Doble XP (1 ronda) <span class="pill">30</span></div>
              <div class="d">Duplica el XP del próximo acierto.</div>
            </div>
            <button id="buyDouble">Comprar</button>
          </div>
          <div class="item">
            <div class="left">
              <div class="t">Re-roll <span class="pill">10</span></div>
              <div class="d">Cambia la pregunta por otra del mismo nivel.</div>
            </div>
            <button id="buyReroll">Comprar</button>
          </div>
        </div>

        <h2 style="margin:14px 0 10px;font-size:16px">Registro</h2>
        <div class="log" id="log"></div>
      </div>
    </div>
  </div>

  <script>
    // Estado (persistente)
    const LS_KEY = "GO_OLIVERITO_GO_v1";
    const state = {
      lvl: 1,
      xp: 0,
      coins: 0,
      hp: 3,
      maxHp: 5,
      streak: 0,
      shield: 0,
      doubleXp: 0,
      hint: 0,
      rerollTokens: 0,
      running: false,
      paused: false,
      secondsLeft: 25,
      baseTime: 25,
      current: null,
      best: { xp: 0, lvl: 1, coins: 0 }
    };

    // Umbrales de nivel
    const lvlThresholds = [0, 50, 120, 220, 350, 520, 720];

    // UI
    const el = (id)=>document.getElementById(id);
    const ui = {
      lvl: el("lvl"), xp: el("xp"), xpNext: el("xpNext"), hp: el("hp"), coins: el("coins"),
      streak: el("streak"), time: el("time"), xpBar: el("xpBar"),
      question: el("question"), qmeta: el("qmeta"), answer: el("answer"),
      msg: el("msg"), log: el("log"),
      btnStart: el("btnStart"), btnPause: el("btnPause"), btnReset: el("btnReset"),
      btnSubmit: el("btnSubmit"), btnSkip: el("btnSkip"),
      buyLife: el("buyLife"), buyHint: el("buyHint"), buyShield: el("buyShield"),
      buyDouble: el("buyDouble"), buyReroll: el("buyReroll")
    };

    function save(){
      localStorage.setItem(LS_KEY, JSON.stringify(state));
    }
    function load(){
      const raw = localStorage.getItem(LS_KEY);
      if(!raw) return;
      try{
        const s = JSON.parse(raw);
        Object.assign(state, s);
      }catch(e){}
    }

    function logLine(text, kind=""){
      const p = document.createElement("p");
      p.innerHTML = (kind ? `<b>${kind}:</b> ` : "") + text + ` <small>(${new Date().toLocaleTimeString()})</small>`;
      ui.log.prepend(p);
    }

    function hearts(n){
      return "♥".repeat(Math.max(0,n)) + "♡".repeat(Math.max(0, state.maxHp - n));
    }

    function xpToNext(){
      const next = lvlThresholds[Math.min(state.lvl, lvlThresholds.length-1)];
      const next2 = lvlThresholds[Math.min(state.lvl+1, lvlThresholds.length-1)];
      return { cur: next, next: next2 };
    }

    function render(){
      ui.lvl.textContent = state.lvl;
      ui.xp.textContent = state.xp;
      ui.coins.textContent = state.coins;
      ui.hp.textContent = hearts(state.hp);
      ui.streak.textContent = state.streak;
      ui.time.textContent = state.secondsLeft;

      const t = xpToNext();
      ui.xpNext.textContent = t.next;
      const span = Math.max(1, t.next - t.cur);
      const pct = Math.min(100, Math.max(0, ((state.xp - t.cur) / span) * 100));
      ui.xpBar.style.width = pct + "%";

      ui.btnSubmit.disabled = !state.running || state.paused || state.hp<=0;
      ui.btnSkip.disabled = !state.running || state.paused || state.hp<=0;
      ui.btnPause.textContent = state.paused ? "Reanudar" : "Pausar";
      ui.btnStart.disabled = state.running && !state.paused;
    }

    // Utilidades
    const randInt = (a,b)=>Math.floor(Math.random()*(b-a+1))+a;
    const pick = (arr)=>arr[randInt(0,arr.length-1)];

    // Generador de preguntas por nivel
    function genQuestion(lvl){
      // Tipos: +, -, *, /, orden de operaciones, enteros, porcentajes simples, fracciones básicas
      // Mantenerlo aritmético (sin álgebra).
      let q = { text:"", answer:0, meta:"", hint:"" };

      const include = {
        addsub: true,
        muldiv: lvl >= 1,
        parens: lvl >= 2,
        ints: lvl >= 2,
        percent: lvl >= 3,
        frac: lvl >= 3
      };

      const types = [];
      if(include.addsub) types.push("addsub");
      if(include.muldiv) types.push("muldiv");
      if(include.parens) types.push("parens");
      if(include.ints) types.push("ints");
      if(include.percent) types.push("percent");
      if(include.frac) types.push("frac");

      const type = pick(types);

      if(type==="addsub"){
        const a = randInt(10, 60);
        const b = randInt(10, 60);
        const op = pick(["+","-"]);
        q.text = `${a} ${op} ${b}`;
        q.answer = (op==="+") ? (a+b) : (a-b);
        q.meta = "Suma/Resta";
        q.hint = op==="+" ? "Agrupa decenas: (a+b) = (a+10)+(b-10) si ayuda." : "Piensa en la diferencia: resta primero decenas y luego unidades.";
      }

      if(type==="muldiv"){
        const op = pick(["*","/"]);
        if(op==="*"){
          const a = randInt(7, 29);
          const b = randInt(3, 19);
          q.text = `${a} × ${b}`;
          q.answer = a*b;
          q.meta = "Multiplicación";
          q.hint = "Usa distributiva: a×b = a×(b1+b2). Ej: ×(10+5).";
        }else{
          const b = randInt(3, 14);
          const ans = randInt(6, 25);
          const a = b*ans;
          q.text = `${a} ÷ ${b}`;
          q.answer = ans;
          q.meta = "División exacta";
          q.hint = "Recuerda: a ÷ b = ? equivale a b×? = a.";
        }
      }

      if(type==="parens"){
        const a = randInt(2, 12);
        const b = randInt(2, 18);
        const c = randInt(2, 12);
        const form = pick([1,2,3]);
        if(form===1){
          // a*(b-c)+d
          const d = randInt(5, 30);
          q.text = `${a} × (${b} - ${c}) + ${d}`;
          q.answer = a*(b-c) + d;
          q.meta = "Jerarquía + paréntesis";
          q.hint = "Resuelve paréntesis primero, luego multiplicación, al final suma.";
        }else if(form===2){
          // (a+b)*c - d
          const d = randInt(5, 30);
          q.text = `(${a} + ${b}) × ${c} - ${d}`;
          q.answer = (a+b)*c - d;
          q.meta = "Jerarquía + paréntesis";
          q.hint = "Primero suma dentro del paréntesis; luego multiplica.";
        }else{
          // a + b*c - d
          const d = randInt(5, 30);
          q.text = `${a} + ${b} × ${c} - ${d}`;
          q.answer = a + b*c - d;
          q.meta = "Jerarquía de operaciones";
          q.hint = "Multiplicación antes que suma/resta.";
        }
      }

      if(type==="ints"){
        const a = randInt(-40, 40);
        const b = randInt(-40, 40);
        const op = pick(["+","-"]);
        q.text = `${a} ${op} (${b})`;
        q.answer = (op==="+") ? (a+b) : (a-b);
        q.meta = "Enteros con signos";
        q.hint = "Restar un número negativo equivale a sumar su opuesto.";
      }

      if(type==="percent"){
        // porcentaje de un número, redondeo exacto con múltiplos
        const base = pick([50, 80, 100, 120, 150, 200, 250, 300, 400]);
        const pct = pick([5,10,12,15,20,25,30,40]);
        q.text = `${pct}% de ${base}`;
        q.answer = Math.round((pct/100)*base);
        q.meta = "Porcentajes";
        q.hint = "Convierte: p% = p/100. 10% es 1/10, 25% es 1/4, 5% es la mitad de 10%.";
      }

      if(type==="frac"){
        // suma de fracciones con denominadores compatibles
        const den = pick([4,5,8,10,12]);
        const a = randInt(1, den-1);
        const b = randInt(1, den-1);
        // respuesta como fracción simplificada -> pedimos en decimal con 2 decimales para UX simple
        const val = (a/den) + (b/den);
        q.text = `${a}/${den} + ${b}/${den}  (responde en decimal, ej: 0.75)`;
        q.answer = Number(val.toFixed(2));
        q.meta = "Fracciones → decimal";
        q.hint = "Suma numeradores si el denominador es igual, luego divide para pasar a decimal.";
      }

      // Ajuste por nivel (rangos/tiempo)
      return q;
    }

    function formatAnswerExpected(q){
      if(q.meta.includes("Fracciones")) return "decimal (2 decimales)";
      return "número";
    }

    // Timer
    let timer = null;
    function resetTimer(){
      state.secondsLeft = Math.max(10, state.baseTime - (state.lvl-1)*2);
    }
    function startTimer(){
      clearInterval(timer);
      timer = setInterval(()=>{
        if(!state.running || state.paused) return;
        state.secondsLeft--;
        if(state.secondsLeft<=0){
          onTimeout();
        }
        render();
        save();
      }, 1000);
    }

    function onTimeout(){
      state.secondsLeft = 0;
      // timeout cuenta como fallo suave
      applyWrong("Tiempo agotado. Pierdes 1 vida.");
      nextQuestion();
    }

    // Reglas de recompensa
    function awardCorrect(fast=false){
      const baseXP = fast ? 15 : 10;
      const baseCoins = fast ? 8 : 5;
      const xpGain = (state.doubleXp>0) ? baseXP*2 : baseXP;
      const coinGain = baseCoins + Math.min(4, Math.floor(state.streak/3)); // mini bono por racha

      state.xp += xpGain;
      state.coins += coinGain;
      state.streak += 1;

      if(state.doubleXp>0) state.doubleXp = 0;

      ui.msg.innerHTML = `<span class="ok">Correcto.</span> +${xpGain} XP y +${coinGain} monedas.`;
      logLine(`Acierto (+${xpGain} XP, +${coinGain} monedas). Racha: ${state.streak}.`, "OK");

      levelUpCheck();
      save();
      render();
    }

    function applyWrong(text){
      state.streak = 0;
      if(state.shield>0){
        state.shield -= 1;
        ui.msg.innerHTML = `<span class="warn">${text}</span> Escudo activado: no pierdes vida.`;
        logLine(`${text} Escudo evitó daño.`, "ESCUDO");
      }else{
        state.hp -= 1;
        ui.msg.innerHTML = `<span class="bad">${text}</span>`;
        logLine(`${text} (HP ahora: ${state.hp}).`, "FALLO");
      }
      if(state.hp<=0){
        state.hp = 0;
        state.running = false;
        ui.question.textContent = "Game Over";
        ui.qmeta.textContent = "Puedes reiniciar para jugar de nuevo.";
        ui.msg.innerHTML = `<span class="bad">Sin vida. Fin del juego.</span>`;
        logLine("Fin del juego.", "GAME OVER");
      }
      save();
      render();
    }

    function levelUpCheck(){
      while(state.lvl < lvlThresholds.length-1 && state.xp >= lvlThresholds[state.lvl+1]){
        state.lvl += 1;
        state.hp = Math.min(state.maxHp, state.hp + 1); // recompensa suave
        ui.msg.innerHTML = `<span class="ok">¡Subiste a nivel ${state.lvl}!</span> (+1 vida)`;
        logLine(`Subió a nivel ${state.lvl}.`, "NIVEL");
      }
      if(state.xp > state.best.xp){
        state.best = { xp: state.xp, lvl: state.lvl, coins: state.coins };
      }
    }

    // Pista
    function showHint(){
      if(state.hint<=0){
        ui.msg.innerHTML = `<span class="warn">No tienes pistas. Cómpralas en la tienda.</span>`;
        return;
      }
      state.hint -= 1;
      ui.msg.innerHTML = `<span class="warn">Pista:</span> ${state.current.hint}`;
      logLine("Usó una pista.", "PISTA");
      save(); render();
    }

    // Preguntas
    function nextQuestion(){
      if(state.hp<=0) return;
      resetTimer();
      state.current = genQuestion(state.lvl);
      ui.question.textContent = state.current.text;
      ui.qmeta.textContent = `Nivel ${state.lvl} · ${state.current.meta} · Esperado: ${formatAnswerExpected(state.current)}`;
      ui.answer.value = "";
      ui.answer.focus();
      render();
      save();
    }

    function parseUserAnswer(q, raw){
      const s = raw.trim().replace(",", "."); // decimal con coma
      if(s==="") return null;
      // fracciones piden decimal con 2 decimales
      if(q.meta.includes("Fracciones")){
        const n = Number(s);
        if(Number.isNaN(n)) return null;
        return Number(n.toFixed(2));
      }
      const n = Number(s);
      if(Number.isNaN(n)) return null;
      // permitir enteros
      return Math.trunc(n);
    }

    function check(){
      if(!state.running || state.paused || state.hp<=0) return;
      const raw = ui.answer.value;
      const ua = parseUserAnswer(state.current, raw);

      if(ua===null){
        ui.msg.innerHTML = `<span class="warn">Escribe un número válido.</span>`;
        return;
      }

      const fast = state.secondsLeft >= Math.max(8, Math.floor(resetTimer));
      // Comparación: para fracciones en decimal a 2 decimales
      const ok = state.current.meta.includes("Fracciones")
        ? (Math.abs(ua - state.current.answer) < 0.001)
        : (ua === state.current.answer);

      if(ok){
        const isFast = state.secondsLeft >= 15;
        awardCorrect(isFast);
        nextQuestion();
      }else{
        applyWrong(`Incorrecto. La respuesta era ${state.current.answer}.`);
        nextQuestion();
      }
    }

    // Tienda (costos)
    function buy(cost, onOk){
      if(state.coins < cost){
        ui.msg.innerHTML = `<span class="warn">No tienes suficientes monedas.</span>`;
        return;
      }
      state.coins -= cost;
      onOk();
      save(); render();
    }

    // Eventos
    ui.btnStart.addEventListener("click", ()=>{
      state.running = true;
      state.paused = false;
      if(state.hp<=0){ state.hp=3; state.xp=0; state.coins=0; state.lvl=1; state.streak=0; state.shield=0; state.doubleXp=0; state.hint=0; state.rerollTokens=0; }
      resetTimer();
      startTimer();
      nextQuestion();
      logLine("Comenzó partida.", "INICIO");
      render(); save();
    });

    ui.btnPause.addEventListener("click", ()=>{
      if(!state.running) return;
      state.paused = !state.paused;
      ui.msg.innerHTML = state.paused ? `<span class="warn">Pausado.</span>` : "";
      render(); save();
    });

    ui.btnReset.addEventListener("click", ()=>{
      if(!confirm("¿Reiniciar progreso guardado?")) return;
      localStorage.removeItem(LS_KEY);
      location.reload();
    });

    ui.btnSubmit.addEventListener("click", check);
    ui.answer.addEventListener("keydown", (e)=>{
      if(e.key==="Enter") check();
      if(e.key.toLowerCase()==="h") showHint();
    });

    ui.btnSkip.addEventListener("click", ()=>{
      if(state.rerollTokens<=0){
        ui.msg.innerHTML = `<span class="warn">No tienes Re-roll. Cómpralo en la tienda.</span>`;
        return;
      }
      state.rerollTokens -= 1;
      logLine("Usó Re-roll.", "RE-ROLL");
      nextQuestion();
    });

    ui.buyLife.addEventListener("click", ()=>{
      buy(25, ()=>{
        if(state.hp>=state.maxHp){
          ui.msg.innerHTML = `<span class="warn">Ya tienes vida al máximo.</span>`;
          state.coins += 25; // reembolso simple
          return;
        }
        state.hp += 1;
        ui.msg.innerHTML = `<span class="ok">Compraste +1 vida.</span>`;
        logLine("Compró +1 vida.", "HelicoTIENDA");
      });
    });

    ui.buyHint.addEventListener("click", ()=>{
      buy(12, ()=>{
        state.hint += 1;
        ui.msg.innerHTML = `<span class="ok">Pista comprada.</span> Pulsa H para usarla.`;
        logLine("Compró pista.", "HelicoTIENDA");
      });
    });

    ui.buyShield.addEventListener("click", ()=>{
      buy(18, ()=>{
        state.shield += 1;
        ui.msg.innerHTML = `<span class="ok">Escudo comprado.</span> Se activará en el próximo fallo.`;
        logLine("Compró escudo.", "HelicoTIENDA");
      });
    });

    ui.buyDouble.addEventListener("click", ()=>{
      buy(30, ()=>{
        state.doubleXp += 1;
        ui.msg.innerHTML = `<span class="ok">Doble XP activado</span> para el próximo acierto.`;
        logLine("Compró doble XP.", "HelicoTIENDA");
      });
    });

    ui.buyReroll.addEventListener("click", ()=>{
      buy(10, ()=>{
        state.rerollTokens += 1;
        ui.msg.innerHTML = `<span class="ok">Re-roll comprado.</span> Úsalo con el botón Re-roll.`;
        logLine("Compró re-roll.", "HelicoTIENDA");
      });
    });

    // Inicio
    load();
    render();
    startTimer();
    if(state.running && state.hp>0){
      // continúa si estaba jugando
      nextQuestion();
      logLine("Continuó partida guardada.", "AUTO");
    }else{
      ui.qmeta.textContent = "Pulsa Iniciar para comenzar (se guarda en este navegador).";
    }
  </script>
</body>
</html>
