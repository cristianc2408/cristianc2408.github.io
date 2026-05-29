<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Reserva tu Cancha</title>
<link href="https://fonts.googleapis.com/css2?family=DM+Sans:wght@400;500;600&family=Syne:wght@700;800&display=swap" rel="stylesheet">
<style>
  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  :root {
    --green: #1a6b3c;
    --green-light: #e8f5ee;
    --green-mid: #2d9a5a;
    --sand: #f5f0e8;
    --sand-dark: #e8dfc8;
    --blue: #1a4a7a;
    --blue-light: #e8f0f8;
    --text: #1a1a1a;
    --text-muted: #666;
    --border: #ddd;
    --white: #ffffff;
    --radius: 12px;
    --shadow: 0 2px 12px rgba(0,0,0,0.08);
  }

  body {
    font-family: 'DM Sans', sans-serif;
    background: var(--sand);
    color: var(--text);
    min-height: 100vh;
  }

  header {
    background: var(--green);
    color: white;
    padding: 0 2rem;
    display: flex;
    align-items: center;
    justify-content: space-between;
    height: 64px;
    position: sticky;
    top: 0;
    z-index: 100;
  }

  header h1 {
    font-family: 'Syne', sans-serif;
    font-size: 1.3rem;
    letter-spacing: -0.01em;
  }

  header span {
    font-size: 0.8rem;
    opacity: 0.75;
    background: rgba(255,255,255,0.15);
    padding: 4px 12px;
    border-radius: 20px;
  }

  .hero {
    background: linear-gradient(135deg, var(--green) 0%, #0f4a28 100%);
    color: white;
    padding: 3rem 2rem 2rem;
    text-align: center;
  }

  .hero h2 {
    font-family: 'Syne', sans-serif;
    font-size: clamp(1.8rem, 5vw, 2.8rem);
    margin-bottom: 0.5rem;
    letter-spacing: -0.02em;
  }

  .hero p { opacity: 0.8; font-size: 1rem; }

  .courts-row {
    display: flex;
    justify-content: center;
    gap: 1rem;
    margin-top: 1.5rem;
    flex-wrap: wrap;
  }

  .court-pill {
    background: rgba(255,255,255,0.15);
    border: 1px solid rgba(255,255,255,0.3);
    color: white;
    padding: 6px 16px;
    border-radius: 20px;
    font-size: 0.85rem;
    cursor: pointer;
    transition: all 0.2s;
  }

  .court-pill:hover, .court-pill.active {
    background: white;
    color: var(--green);
    font-weight: 600;
  }

  main {
    max-width: 860px;
    margin: 0 auto;
    padding: 2rem 1rem;
  }

  .tabs {
    display: flex;
    gap: 0;
    background: white;
    border-radius: var(--radius);
    padding: 4px;
    margin-bottom: 1.5rem;
    box-shadow: var(--shadow);
  }

  .tab-btn {
    flex: 1;
    padding: 10px;
    border: none;
    background: transparent;
    font-family: 'DM Sans', sans-serif;
    font-size: 0.9rem;
    cursor: pointer;
    border-radius: 8px;
    transition: all 0.2s;
    color: var(--text-muted);
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 6px;
  }

  .tab-btn.active {
    background: var(--green);
    color: white;
    font-weight: 600;
  }

  .tab-panel { display: none; }
  .tab-panel.active { display: block; }

  .card {
    background: white;
    border-radius: var(--radius);
    padding: 1.5rem;
    box-shadow: var(--shadow);
    margin-bottom: 1rem;
  }

  .card h3 {
    font-family: 'Syne', sans-serif;
    font-size: 1rem;
    margin-bottom: 1rem;
    color: var(--green);
    display: flex;
    align-items: center;
    gap: 8px;
  }

  .courts-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(180px, 1fr));
    gap: 10px;
  }

  .court-card {
    border: 2px solid var(--border);
    border-radius: var(--radius);
    padding: 1rem;
    cursor: pointer;
    transition: all 0.2s;
    text-align: center;
  }

  .court-card:hover { border-color: var(--green-mid); background: var(--green-light); }
  .court-card.selected { border-color: var(--green); background: var(--green-light); }

  .court-card .icon { font-size: 2rem; margin-bottom: 6px; }
  .court-card .name { font-weight: 600; font-size: 0.9rem; }
  .court-card .detail { font-size: 0.75rem; color: var(--text-muted); margin-top: 2px; }
  .court-card .avail { font-size: 0.75rem; margin-top: 6px; padding: 2px 8px; border-radius: 10px; display: inline-block; }
  .avail.ok { background: var(--green-light); color: var(--green); font-weight: 600; }
  .avail.busy { background: #fff3e0; color: #e65100; font-weight: 600; }

  .date-row {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 10px;
  }

  .field label {
    display: block;
    font-size: 0.8rem;
    color: var(--text-muted);
    margin-bottom: 4px;
    font-weight: 500;
  }

  .field input, .field select {
    width: 100%;
    padding: 10px 12px;
    border: 1.5px solid var(--border);
    border-radius: 8px;
    font-family: 'DM Sans', sans-serif;
    font-size: 0.9rem;
    background: white;
    color: var(--text);
    transition: border-color 0.2s;
  }

  .field input:focus, .field select:focus {
    outline: none;
    border-color: var(--green);
  }

  .hours-grid {
    display: grid;
    grid-template-columns: repeat(5, 1fr);
    gap: 6px;
  }

  @media(max-width:480px) { .hours-grid { grid-template-columns: repeat(4,1fr); } }

  .hour-btn {
    padding: 8px 4px;
    border: 1.5px solid var(--border);
    border-radius: 8px;
    background: white;
    font-family: 'DM Sans', sans-serif;
    font-size: 0.8rem;
    cursor: pointer;
    transition: all 0.15s;
    text-align: center;
  }

  .hour-btn:hover:not(.taken) { border-color: var(--green); background: var(--green-light); }
  .hour-btn.selected { background: var(--green); color: white; border-color: var(--green); font-weight: 600; }
  .hour-btn.taken { background: #f5f5f5; color: #bbb; text-decoration: line-through; cursor: not-allowed; }

  .form-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 10px;
  }

  @media(max-width:480px) { .form-grid { grid-template-columns: 1fr; } .date-row { grid-template-columns: 1fr; } }

  .btn-main {
    width: 100%;
    padding: 14px;
    background: var(--green);
    color: white;
    border: none;
    border-radius: var(--radius);
    font-family: 'Syne', sans-serif;
    font-size: 1rem;
    font-weight: 700;
    cursor: pointer;
    transition: background 0.2s;
    margin-top: 4px;
    letter-spacing: 0.01em;
  }

  .btn-main:hover { background: #0f4a28; }

  .confirm-box {
    background: var(--green-light);
    border: 1.5px solid var(--green-mid);
    border-radius: var(--radius);
    padding: 1.2rem 1.5rem;
    margin-top: 1rem;
    display: none;
    animation: fadeIn 0.3s ease;
  }

  .confirm-box h4 { color: var(--green); font-weight: 700; margin-bottom: 6px; font-family: 'Syne', sans-serif; }
  .confirm-box p { font-size: 0.9rem; color: #2d5a3d; line-height: 1.7; }

  @keyframes fadeIn { from { opacity:0; transform: translateY(6px); } to { opacity:1; transform: translateY(0); } }

  .steps {
    display: flex;
    align-items: center;
    gap: 0;
    margin-bottom: 1.5rem;
    background: white;
    border-radius: var(--radius);
    padding: 1rem 1.5rem;
    box-shadow: var(--shadow);
  }

  .step {
    display: flex;
    align-items: center;
    gap: 8px;
    flex: 1;
    font-size: 0.8rem;
    color: var(--text-muted);
  }

  .step .num {
    width: 26px; height: 26px;
    border-radius: 50%;
    border: 2px solid var(--border);
    display: flex; align-items: center; justify-content: center;
    font-weight: 700; font-size: 0.75rem;
    flex-shrink: 0;
  }

  .step.done .num { background: var(--green); border-color: var(--green); color: white; }
  .step.active .num { border-color: var(--green); color: var(--green); }
  .step.active { color: var(--text); font-weight: 600; }

  .step-line { width: 20px; height: 2px; background: var(--border); flex-shrink: 0; margin: 0 4px; }
  .step-line.done { background: var(--green); }

  /* CHAT */
  .chat-wrap {
    background: white;
    border-radius: var(--radius);
    box-shadow: var(--shadow);
    overflow: hidden;
  }

  .chat-header {
    background: var(--green);
    color: white;
    padding: 1rem 1.5rem;
    display: flex;
    align-items: center;
    gap: 10px;
  }

  .chat-header .avatar {
    width: 36px; height: 36px;
    background: rgba(255,255,255,0.2);
    border-radius: 50%;
    display: flex; align-items: center; justify-content: center;
    font-size: 1.2rem;
  }

  .chat-header h3 { font-family: 'Syne', sans-serif; font-size: 1rem; }
  .chat-header p { font-size: 0.75rem; opacity: 0.8; }

  .chat-messages {
    padding: 1rem;
    min-height: 280px;
    max-height: 400px;
    overflow-y: auto;
    display: flex;
    flex-direction: column;
    gap: 10px;
    background: var(--sand);
  }

  .msg {
    max-width: 82%;
    padding: 10px 14px;
    border-radius: 16px;
    font-size: 0.88rem;
    line-height: 1.6;
  }

  .msg.ai {
    background: white;
    color: var(--text);
    align-self: flex-start;
    border-bottom-left-radius: 4px;
    box-shadow: 0 1px 4px rgba(0,0,0,0.06);
  }

  .msg.user {
    background: var(--green);
    color: white;
    align-self: flex-end;
    border-bottom-right-radius: 4px;
  }

  .quick-btns {
    display: flex;
    gap: 6px;
    flex-wrap: wrap;
    padding: 10px 1rem;
    background: var(--sand);
    border-top: 1px solid var(--sand-dark);
  }

  .quick-btn {
    padding: 5px 12px;
    border: 1.5px solid var(--green-mid);
    background: white;
    color: var(--green);
    border-radius: 20px;
    font-size: 0.78rem;
    cursor: pointer;
    font-family: 'DM Sans', sans-serif;
    transition: all 0.15s;
  }

  .quick-btn:hover { background: var(--green); color: white; }

  .chat-input-row {
    display: flex;
    padding: 10px;
    gap: 8px;
    border-top: 1px solid var(--border);
    background: white;
  }

  .chat-input-row input {
    flex: 1;
    padding: 10px 14px;
    border: 1.5px solid var(--border);
    border-radius: 24px;
    font-family: 'DM Sans', sans-serif;
    font-size: 0.9rem;
    color: var(--text);
    background: var(--sand);
  }

  .chat-input-row input:focus { outline: none; border-color: var(--green); }

  .send-btn {
    width: 42px; height: 42px;
    background: var(--green);
    border: none;
    border-radius: 50%;
    color: white;
    font-size: 1rem;
    cursor: pointer;
    display: flex; align-items: center; justify-content: center;
    transition: background 0.2s;
    flex-shrink: 0;
  }

  .send-btn:hover { background: #0f4a28; }

  .typing span {
    display: inline-block;
    width: 7px; height: 7px;
    background: var(--text-muted);
    border-radius: 50%;
    margin: 0 2px;
    animation: bounce 1.2s infinite;
  }
  .typing span:nth-child(2) { animation-delay: 0.2s; }
  .typing span:nth-child(3) { animation-delay: 0.4s; }
  @keyframes bounce { 0%,60%,100%{transform:translateY(0)} 30%{transform:translateY(-6px)} }

  footer {
    text-align: center;
    padding: 2rem;
    font-size: 0.8rem;
    color: var(--text-muted);
    border-top: 1px solid var(--sand-dark);
    margin-top: 2rem;
  }
</style>
</head>
<body>

<header>
  <h1>⚽ ComplexoDeportivo</h1>
  <span>Reservas en línea</span>
</header>

<div class="hero">
  <h2>Reserva tu cancha favorita</h2>
  <p>Disponibilidad en tiempo real · Confirmación inmediata</p>
  <div class="courts-row">
    <div class="court-pill active">⚽ 2 canchas de fútbol</div>
    <div class="court-pill">🏐 2 canchas voley playa</div>
  </div>
</div>

<main>

  <div class="tabs">
    <button class="tab-btn active" onclick="setTab('reserva',this)">📅 Hacer reserva</button>
    <button class="tab-btn" onclick="setTab('asistente',this)">🤖 Asistente IA</button>
  </div>

  <!-- TAB RESERVA -->
  <div class="tab-panel active" id="tab-reserva">

    <div class="steps">
      <div class="step active" id="s1"><div class="num">1</div><span>Cancha</span></div>
      <div class="step-line" id="sl1"></div>
      <div class="step" id="s2"><div class="num">2</div><span>Horario</span></div>
      <div class="step-line" id="sl2"></div>
      <div class="step" id="s3"><div class="num">3</div><span>Datos</span></div>
      <div class="step-line" id="sl3"></div>
      <div class="step" id="s4"><div class="num">✓</div><span>Listo</span></div>
    </div>

    <div class="card">
      <h3>🏟️ Elige una cancha</h3>
      <div class="courts-grid">
        <div class="court-card selected" id="c1" onclick="selectCourt('Fútbol 1','c1')">
          <div class="icon">⚽</div>
          <div class="name">Fútbol 1</div>
          <div class="detail">Césped sintético · 10 jugadores</div>
          <div class="avail ok">Disponible</div>
        </div>
        <div class="court-card" id="c2" onclick="selectCourt('Fútbol 2','c2')">
          <div class="icon">⚽</div>
          <div class="name">Fútbol 2</div>
          <div class="detail">Césped sintético · 10 jugadores</div>
          <div class="avail ok">Disponible</div>
        </div>
        <div class="court-card" id="c3" onclick="selectCourt('Voley Playa 1','c3')">
          <div class="icon">🏐</div>
          <div class="name">Voley Playa 1</div>
          <div class="detail">Arena fina · 6 jugadores</div>
          <div class="avail ok">Disponible</div>
        </div>
        <div class="court-card" id="c4" onclick="selectCourt('Voley Playa 2','c4')">
          <div class="icon">🏐</div>
          <div class="name">Voley Playa 2</div>
          <div class="detail">Arena fina · 6 jugadores</div>
          <div class="avail busy">Ocupada 14-16h</div>
        </div>
      </div>
    </div>

    <div class="card">
      <h3>📅 Fecha y horario</h3>
      <div class="date-row" style="margin-bottom:1rem;">
        <div class="field">
          <label>Fecha</label>
          <input type="date" id="fecha" />
        </div>
        <div class="field">
          <label>Duración</label>
          <select id="duracion">
            <option>1 hora</option>
            <option>2 horas</option>
            <option>3 horas</option>
          </select>
        </div>
      </div>
      <p style="font-size:0.8rem;color:var(--text-muted);margin-bottom:10px;font-weight:500;">Horarios disponibles</p>
      <div class="hours-grid" id="hours-grid"></div>
    </div>

    <div class="card">
      <h3>👤 Tus datos</h3>
      <div class="form-grid" style="margin-bottom:10px;">
        <div class="field">
          <label>Nombre completo</label>
          <input type="text" id="nombre" placeholder="Ej: Carlos Pérez" />
        </div>
        <div class="field">
          <label>Teléfono / WhatsApp</label>
          <input type="tel" id="telefono" placeholder="Ej: 3001234567" />
        </div>
      </div>
      <div class="field">
        <label>Correo electrónico</label>
        <input type="email" id="email" placeholder="correo@ejemplo.com" />
      </div>
      <button class="btn-main" style="margin-top:1.2rem;" onclick="confirmar()">✅ Confirmar reserva</button>
      <div class="confirm-box" id="confirm-box">
        <h4>¡Reserva confirmada! 🎉</h4>
        <p id="confirm-text"></p>
      </div>
    </div>

  </div>

  <!-- TAB ASISTENTE -->
  <div class="tab-panel" id="tab-asistente">
    <div class="chat-wrap">
      <div class="chat-header">
        <div class="avatar">🤖</div>
        <div>
          <h3>Asistente de Reservas</h3>
          <p>Powered by Claude AI · Responde al instante</p>
        </div>
      </div>
      <div class="chat-messages" id="chat-messages">
        <div class="msg ai">¡Hola! 👋 Soy tu asistente de reservas. Puedo ayudarte con disponibilidad, precios, horarios o cualquier duda. ¿En qué te puedo ayudar?</div>
      </div>
      <div class="quick-btns">
        <button class="quick-btn" onclick="quickMsg('¿Qué canchas están disponibles hoy?')">Disponibilidad hoy</button>
        <button class="quick-btn" onclick="quickMsg('¿Cuánto cuesta una hora de fútbol?')">Precios</button>
        <button class="quick-btn" onclick="quickMsg('Quiero reservar el sábado a las 4pm para fútbol')">Reservar sábado</button>
        <button class="quick-btn" onclick="quickMsg('¿Cuáles son los horarios de atención?')">Horarios</button>
      </div>
      <div class="chat-input-row">
        <input type="text" id="chat-input" placeholder="Escribe tu pregunta..." onkeydown="if(event.key==='Enter') sendChat()" />
        <button class="send-btn" onclick="sendChat()" aria-label="Enviar">➤</button>
      </div>
    </div>
  </div>

</main>

<footer>
  © 2025 ComplexoDeportivo · Reservas en línea · Desarrollado con ❤️ y Claude AI
</footer>

<script>
const HOURS = ['7:00','8:00','9:00','10:00','11:00','12:00','13:00','14:00','15:00','16:00','17:00','18:00','19:00','20:00','21:00'];
const TAKEN = { c4: ['14:00','15:00'] };

let selectedCourt = 'Fútbol 1';
let selectedCourtId = 'c1';
let selectedHour = null;
let chatHistory = [];
let isLoading = false;

// Set today's date
const today = new Date();
const yyyy = today.getFullYear();
const mm = String(today.getMonth()+1).padStart(2,'0');
const dd = String(today.getDate()).padStart(2,'0');
document.getElementById('fecha').value = `${yyyy}-${mm}-${dd}`;
document.getElementById('fecha').min = `${yyyy}-${mm}-${dd}`;

renderHours('c1');

function setTab(tab, el) {
  document.querySelectorAll('.tab-btn').forEach(t => t.classList.remove('active'));
  document.querySelectorAll('.tab-panel').forEach(p => p.classList.remove('active'));
  el.classList.add('active');
  document.getElementById('tab-'+tab).classList.add('active');
}

function selectCourt(name, id) {
  document.querySelectorAll('.court-card').forEach(c => c.classList.remove('selected'));
  document.getElementById(id).classList.add('selected');
  selectedCourt = name;
  selectedCourtId = id;
  selectedHour = null;
  renderHours(id);
  updateStep(2);
}

function renderHours(cid) {
  const g = document.getElementById('hours-grid');
  g.innerHTML = '';
  const taken = TAKEN[cid] || [];
  HOURS.forEach(h => {
    const b = document.createElement('button');
    b.className = 'hour-btn' + (taken.includes(h) ? ' taken' : '');
    b.textContent = h;
    if (!taken.includes(h)) b.onclick = () => selectHour(h, b);
    g.appendChild(b);
  });
}

function selectHour(h, btn) {
  document.querySelectorAll('.hour-btn').forEach(b => b.classList.remove('selected'));
  btn.classList.add('selected');
  selectedHour = h;
  updateStep(3);
}

function updateStep(n) {
  for (let i = 1; i <= 4; i++) {
    const s = document.getElementById('s'+i);
    const l = document.getElementById('sl'+i);
    if (!s) continue;
    s.className = 'step' + (i < n ? ' done' : i === n ? ' active' : '');
    if (l) l.className = 'step-line' + (i < n ? ' done' : '');
  }
}

function confirmar() {
  const nombre = document.getElementById('nombre').value.trim();
  const tel = document.getElementById('telefono').value.trim();
  const email = document.getElementById('email').value.trim();
  const fecha = document.getElementById('fecha').value;
  const dur = document.getElementById('duracion').value;

  if (!nombre || !tel || !fecha || !selectedHour) {
    alert('Por favor completa nombre, teléfono, fecha y selecciona un horario.');
    return;
  }

  const box = document.getElementById('confirm-box');
  const txt = document.getElementById('confirm-text');
  const fechaFmt = new Date(fecha + 'T12:00:00').toLocaleDateString('es-CO', {
    weekday: 'long', year: 'numeric', month: 'long', day: 'numeric'
  });

  txt.innerHTML = `<strong>Cancha:</strong> ${selectedCourt} &nbsp;·&nbsp; <strong>Fecha:</strong> ${fechaFmt}<br>
    <strong>Hora:</strong> ${selectedHour} &nbsp;·&nbsp; <strong>Duración:</strong> ${dur}<br>
    <strong>Titular:</strong> ${nombre} &nbsp;·&nbsp; <strong>Tel:</strong> ${tel}
    ${email ? '<br><strong>Email:</strong> ' + email : ''}`;
  box.style.display = 'block';
  box.scrollIntoView({ behavior: 'smooth', block: 'nearest' });
  updateStep(4);
}

// CHAT
function quickMsg(txt) {
  document.getElementById('chat-input').value = txt;
  sendChat();
}

async function sendChat() {
  if (isLoading) return;
  const inp = document.getElementById('chat-input');
  const msg = inp.value.trim();
  if (!msg) return;
  inp.value = '';

  addMsg(msg, 'user');
  chatHistory.push({ role: 'user', content: msg });

  isLoading = true;
  const loadEl = addTyping();

  try {
    const res = await fetch('https://api.anthropic.com/v1/messages', {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({
        model: 'claude-sonnet-4-20250514',
        max_tokens: 1000,
        system: `Eres el asistente de reservas de un complejo deportivo llamado "ComplexoDeportivo" ubicado en Colombia.
Canchas disponibles:
- Fútbol 1: césped sintético, hasta 10 jugadores, $30.000 COP/hora
- Fútbol 2: césped sintético, hasta 10 jugadores, $30.000 COP/hora
- Voley Playa 1: arena fina, hasta 6 jugadores, $20.000 COP/hora
- Voley Playa 2: arena fina, hasta 6 jugadores, $20.000 COP/hora (hoy ocupada de 14:00 a 16:00)
Horario de atención: 7am a 10pm todos los días.
Responde en español colombiano, de forma amable, breve y útil (máximo 3 líneas). Si el usuario quiere reservar, indícale que use la pestaña "Hacer reserva".`,
        messages: chatHistory.slice(-10)
      })
    });

    const data = await res.json();
    const reply = data.content?.find(c => c.type === 'text')?.text || 'Lo siento, no pude procesar tu pregunta. Intenta de nuevo.';
    loadEl.remove();
    addMsg(reply, 'ai');
    chatHistory.push({ role: 'assistant', content: reply });
  } catch (e) {
    loadEl.remove();
    addMsg('Hubo un problema conectando con el asistente. Verifica tu conexión e intenta de nuevo.', 'ai');
  }
  isLoading = false;
}

function addMsg(text, role) {
  const area = document.getElementById('chat-messages');
  const d = document.createElement('div');
  d.className = 'msg ' + (role === 'user' ? 'user' : 'ai');
  d.textContent = text;
  area.appendChild(d);
  area.scrollTop = area.scrollHeight;
  return d;
}

function addTyping() {
  const area = document.getElementById('chat-messages');
  const d = document.createElement('div');
  d.className = 'msg ai typing';
  d.innerHTML = '<span></span><span></span><span></span>';
  area.appendChild(d);
  area.scrollTop = area.scrollHeight;
  return d;
}
</script>
</body>
</html>
