<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>NDRF — Interactive Guide</title>
  <meta name="description" content="Interactive, single‑file website about India's National Disaster Response Force (NDRF): mission, preparedness tips, a battalion locator, and a quiz." />
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;800&display=swap" rel="stylesheet">
  <style>
    :root {
      --bg: #0f172a; --panel: #111827; --muted: #94a3b8; --text: #e5e7eb;
      --brand: #f97316; --brand-2: #2563eb; --ring: rgba(37, 99, 235, 0.35);
      --ok: #22c55e; --warn: #f59e0b; --danger: #ef4444; --card: #0b1220;
      --shadow: 0 10px 30px rgba(0,0,0,.35);
    }
    [data-theme="light"] {
      --bg: #f8fafc; --panel: #ffffff; --muted: #64748b; --text: #0f172a;
      --brand: #ef6c00; --brand-2: #1d4ed8; --ring: rgba(29,78,216,.25); --card: #ffffff;
      --shadow: 0 12px 24px rgba(2,6,23,.08);
    }

    * { box-sizing: border-box; }
    html { scroll-behavior: smooth; }
    body {
      margin:0; font-family: Inter, system-ui, -apple-system, Segoe UI, Roboto, "Helvetica Neue", Arial;
      background: radial-gradient(1200px 600px at 80% -20%, rgba(37,99,235,.08), transparent 60%),
                  radial-gradient(900px 500px at -10% 10%, rgba(249,115,22,.10), transparent 60%),
                  var(--bg);
      color: var(--text);
    }

    /* Layout */
    .container { max-width:1100px; margin:0 auto; padding:0 20px; }
    header { position:sticky; top:0; backdrop-filter:blur(8px); background: color-mix(in oklab,var(--bg) 88%,transparent); border-bottom:1px solid color-mix(in oklab,var(--muted) 20%,transparent); z-index:50; }
    nav { display:flex; align-items:center; justify-content:space-between; padding:14px 0; }
    nav .brand { display:flex; gap:10px; align-items:center; font-weight:800; letter-spacing:.2px; }
    .logo { width:34px; height:34px; border-radius:10px; background: conic-gradient(from 0deg, var(--brand), var(--brand-2)); box-shadow: inset 0 0 0 2px rgba(255,255,255,.08), var(--shadow); }
    .navlinks { display:flex; gap:14px; flex-wrap:wrap; }
    .navlinks a { text-decoration:none; color: var(--text); opacity:.8; padding:8px 12px; border-radius:10px; }
    .navlinks a:hover, .navlinks a:focus { outline:none; opacity:1; background: color-mix(in oklab,var(--panel) 88%,transparent); box-shadow:0 0 0 2px var(--ring); }
    .controls { display:flex; gap:8px; align-items:center; }
    .btn { background: linear-gradient(135deg,var(--brand),var(--brand-2)); color:#fff; border:none; padding:10px 14px; border-radius:12px; cursor:pointer; font-weight:600; box-shadow: var(--shadow); }
    .btn:focus { outline:none; box-shadow:0 0 0 3px var(--ring); }

    /* Hero */
    .hero { padding:52px 0 36px; }
    .hero-inner { display:grid; grid-template-columns:1.1fr .9fr; gap:24px; align-items:center; }
    .hero h1 { font-size:clamp(28px,4vw,44px); line-height:1.1; margin:0 0 10px; }
    .hero p { color: var(--muted); margin:0 0 18px; }
    .pill { display:inline-flex; gap:8px; align-items:center; font-size:12px; text-transform:uppercase; letter-spacing:.14em; color:#fff; background: linear-gradient(90deg,var(--brand-2),var(--brand)); padding:8px 12px; border-radius:999px; box-shadow: var(--shadow); }
    .card { background: linear-gradient(180deg,color-mix(in oklab,var(--panel) 84%,transparent), color-mix(in oklab,var(--panel) 90%,transparent)); border:1px solid color-mix(in oklab,var(--muted) 22%,transparent); border-radius:16px; padding:16px; box-shadow: var(--shadow); }

    /* Section headings */
    section { padding:56px 0; }
    h2 { font-size:clamp(22px,3vw,32px); margin:0 0 16px; }
    .sub { color: var(--muted); margin-bottom:20px; }

    /* About */
    .grid { display:grid; gap:16px; }
    .grid-2 { grid-template-columns: repeat(2, minmax(0,1fr)); }
    .kpi { display:grid; grid-template-columns: repeat(3,1fr); gap:12px; margin-top:12px; }
    .kpi .item { background: var(--card); border:1px solid color-mix(in oklab,var(--muted) 20%,transparent); border-radius:14px; padding:12px; text-align:center; }
    .kpi .num { font-weight:800; font-size:22px; }
    .kpi .lbl { font-size:12px; color: var(--muted); }

    /* Map */
    .map-wrap { display:grid; grid-template-columns:1.2fr .8fr; gap:18px; }
    .map { background: var(--card); border:1px solid color-mix(in oklab,var(--muted) 20%,transparent); border-radius:16px; padding:10px; position:relative; }
    .legend { display:flex; gap:8px; flex-wrap:wrap; font-size:12px; color:var(--muted); margin-top:8px; }
    .badge { display:inline-flex; align-items:center; gap:6px; background: color-mix(in oklab,var(--panel) 86%,transparent); padding:6px 10px; border-radius:999px; border:1px solid color-mix(in oklab,var(--muted) 18%,transparent); }
    .dot { width:10px; height:10px; border-radius:50%; background: var(--brand-2); box-shadow:0 0 0 2px rgba(37,99,235,.2); }
    svg { width:100%; height:auto; display:block; }
    .marker { cursor:pointer; transition: transform .1s ease; }
    .marker:focus, .marker:hover { outline:none; transform: scale(1.15); }
    .side { background: var(--card); border:1px solid color-mix(in oklab,var(--muted) 20%,transparent); border-radius:16px; padding:14px; }

    dialog { border:none; border-radius:16px; padding:0; max-width:520px; width:calc(100%-24px); box-shadow: var(--shadow); background: var(--panel); color: var(--text); }
    .modal-head { display:flex; justify-content:space-between; align-items:center; padding:14px 16px; border-bottom:1px solid color-mix(in oklab,var(--muted) 20%,transparent); }
    .modal-body { padding:16px; }
    .close { background:transparent; border:none; font-size:22px; color: var(--muted); cursor:pointer; }

    /* Accordion */
    .accordion { display:grid; gap:10px; }
    .acc-item { border:1px solid color-mix(in oklab,var(--muted) 22%,transparent); border-radius:14px; overflow:hidden; background: var(--card); }
    .acc-btn { width:100%; text-align:left; background:transparent; border:none; padding:14px; font-weight:600; color:var(--text); display:flex; justify-content:space-between; align-items:center; cursor:pointer; }
    .acc-panel { padding:0 14px 14px; color: var(--muted); display:none; }
    .acc-item[open] .acc-panel { display:block; }

    /* Resources */
    .res { display:grid; grid-template-columns: repeat(3,1fr); gap:14px; }
    .res a { display:block; text-decoration:none; color:var(--text); }
    .res .card p { color:var(--muted); margin:8px 0 0; font-size:14px; }

    /* Quiz */
    .quiz { display:grid; gap:12px; }
    .q { border:1px solid color-mix(in oklab,var(--muted) 22%,transparent); border-radius:14px; padding:14px; background: var(--card); }
    .q h4 { margin:0 0 10px; }
    .q label { display:block; margin-bottom:6px; cursor:pointer; }
    .score { font-weight:800; }

    /* Contact */
    form { display:grid; gap:10px; }
    input, textarea, select {
      width:100%; padding:12px 12px; background: var(--panel); color: var(--text);
      border:1px solid color-mix(in oklab,var(--muted) 24%,transparent); border-radius:12px;
    }
    input:focus, textarea:focus, select:focus { outline:none; box-shadow:0 0 0 3px var(--ring); }
    .note { color: var(--muted); font-size:12px; }

    footer { padding:36px 0; color: var(--muted); text-align:center; }

    /* Responsive */
    @media (max-width:960px) { .hero-inner{grid-template-columns:1fr;} .map-wrap{grid-template-columns:1fr;} .grid-2{grid-template-columns:1fr;} .res{grid-template-columns:1fr 1fr;} .kpi{grid-template-columns:repeat(3,1fr);} }
    @media (max-width:560px) { .res{grid-template-columns:1fr;} .kpi{grid-template-columns:1fr 1fr;} }
  </style>
</head>
<body>
<header>
  <div class="container">
    <nav aria-label="Primary">
      <a class="brand" href="#home">
        <span class="logo" aria-hidden="true"></span>
        <span>NDRF Interactive</span>
      </a>
      <div class="navlinks">
        <a href="#about">About</a>
        <a href="#locator">Battalion Locator</a>
        <a href="#tips">Safety Tips</a>
        <a href="#resources">Resources</a>
        <a href="#quiz">Quiz</a>
        <a href="#contact">Contact</a>
      </div>
      <div class="controls">
        <button class="btn" id="themeToggle" title="Toggle theme" aria-pressed="false">Theme</button>
      </div>
    </nav>
  </div>
</header>

<section class="hero" id="home">
<div style="text-align: center; margin-top: 40px;">
  <a href="game.html" 
     style="
       display: inline-block;
       background: linear-gradient(135deg, #0288d1, #ff7043);
       color: white;
       padding: 14px 30px;
       border-radius: 50px;
       text-decoration: none;
       font-size: 20px;
       font-weight: bold;
       box-shadow: 0 4px 15px rgba(0,0,0,0.2);
       transition: all 0.3s ease;
     "
     onmouseover="this.style.transform='scale(1.1)'; this.style.boxShadow='0 0 25px rgba(255,255,255,0.6)';" 
     onmouseout="this.style.transform='scale(1)'; this.style.boxShadow='0 4px 15px rgba(0,0,0,0.2)';">
     🦺 Play Disaster Ready Challenge
  </a>
</div>


  
  <div class="container hero-inner">
    <div>
      <span class="pill" aria-label="Emergency ready">Be Ready • Stay Safe</span>
      <h1>NDRF — National Disaster Response Force</h1>
      <p>Explore the mission and preparedness guidance of India's premier disaster response force. Learn safety basics, locate battalions, and test yourself with a quick quiz.</p>
      <div style="display:flex; gap:10px; flex-wrap:wrap; margin-top:12px;">
        <a href="#tips" class="btn">Start with Safety Tips</a>
        <a href="#quiz" class="btn" style="background:linear-gradient(135deg, var(--brand-2), var(--brand));">Take the Quiz</a>
      </div>
    </div>
    <div class="card" aria-hidden="true">
      <img src="https://upload.wikimedia.org/wikipedia/commons/6/63/Indian_Fireman_in_Action.jpg" alt="Fireman on duty" style="width:100%; height:auto; object-fit:cover; border-radius:16px;" />
    </div>
  </div>
</section>

<section id="about">
  <div class="container">
    <h2>About NDRF</h2>
    <p class="sub">The National Disaster Response Force (NDRF) is India’s specialized force for disaster management, equipped to respond quickly to emergencies nationwide.</p>
    <div class="grid grid-2">
      <div class="kpi">
        <div class="item"><div class="num">12</div><div class="lbl">Battalions</div></div>
        <div class="item"><div class="num">12,000+</div><div class="lbl">Personnel</div></div>
        <div class="item"><div class="num">1987</div><div class="lbl">Established</div></div>
      </div>
      <div>
        <p>Trained in disaster response, rescue operations, and medical aid, NDRF personnel are strategically located across India for rapid mobilization.</p>
      </div>
    </div>
  </div>
</section>

<section id="tips">
  <div class="container">
    <h2>Disaster Safety Tips</h2>
    <div class="accordion">
      <details class="acc-item"><summary class="acc-btn">Earthquake Safety</summary><div class="acc-panel"><p>Drop, Cover, and Hold On. Stay indoors if safe; avoid elevators.</p></div></details>
      <details class="acc-item"><summary class="acc-btn">Flood Safety</summary><div class="acc-panel"><p>Move to higher ground, avoid waterlogged areas, and listen to alerts.</p></div></details>
      <details class="acc-item"><summary class="acc-btn">Fire Safety</summary><div class="acc-panel"><p>Use stairs, not elevators; follow evacuation routes; call emergency services.</p></div></details>
    </div>
  </div>
</section>

<section id="resources">
  <div class="container">
    <h2>Resources</h2>
    <div class="res">
      <a href="https://ndrf.gov.in/" target="_blank" class="card"><strong>Official Website</strong><p>Learn about NDRF’s operations and initiatives.</p></a>
      <a href="https://www.ndma.gov.in/" target="_blank" class="card"><strong>NDMA</strong><p>National Disaster Management Authority official site.</p></a>
      <a href="https://www.nidm.gov.in/" target="_blank" class="card"><strong>NIDM</strong><p>Training and research in disaster management.</p></a>
    </div>
  </div>
</section>

<section id="quiz">
  <div class="container">
    <h2>Quick Quiz</h2>
    <div class="quiz">
      <div class="q">
        <h4>1. How many battalions does NDRF have?</h4>
        <label><input type="radio" name="q1" value="10"> 10</label>
        <label><input type="radio" name="q1" value="12"> 12</label>
        <label><input type="radio" name="q1" value="15"> 15</label>
      </div>
      <div class="q">
        <h4>2. What is NDRF’s main role?</h4>
        <label><input type="radio" name="q2" value="Disaster Response"> Disaster Response</label>
        <label><input type="radio" name="q2" value="Law Enforcement"> Law Enforcement</label>
        <label><input type="radio" name="q2" value="Transport"> Transport</label>
      </div>
      <button class="btn" id="checkQuiz">Check Score</button>
      <p class="score" id="quizScore"></p>
    </div>
  </div>
</section>

<section id="contact">
  <div class="container">
    <h2>Contact</h2>
    <form>
      <input type="text" placeholder="Your Name" required>
      <input type="email" placeholder="Email" required>
      <textarea placeholder="Message" rows="4" required></textarea>
      <button type="submit" class="btn">Send</button>
    </form>
    <p class="note">All fields are required.</p>
  </div>
</section>

<footer>
  <div class="container">
    <p>© 2025 NDRF Interactive. All rights reserved.</p>
  </div>
</footer>

<script>
  // Theme toggle
  const btn = document.getElementById('themeToggle');
  btn.addEventListener('click', ()=>{
    if(document.documentElement.dataset.theme==='light'){
      document.documentElement.dataset.theme='';
      btn.setAttribute('aria-pressed','false');
    } else {
      document.documentElement.dataset.theme='light';
      btn.setAttribute('aria-pressed','true');
    }
  });

  // Accordion
  document.querySelectorAll('.acc-btn').forEach(btn=>{
    btn.addEventListener('click', ()=>{ btn.parentElement.toggleAttribute('open'); });
  });

  // Quiz scoring
  const quizAnswers = {q1:'12',q2:'Disaster Response'};
  document.getElementById('checkQuiz').addEventListener('click', ()=>{
    let score=0;
    Object.keys(quizAnswers).forEach(k=>{
      const val = document.querySelector(`input[name="${k}"]:checked`);
      if(val && val.value===quizAnswers[k]) score++;
    });
    document.getElementById('quizScore').textContent = `Score: ${score}/${Object.keys(quizAnswers).length}`;
  });
</script>
</body>
</html>
