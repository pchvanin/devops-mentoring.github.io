---
layout: page
title: "DevOps/SRE FastTrack — RETRO"
---

<style>
/* ===== RETRO CRT THEME ===== */
:root{
  --bg:#000; --fg:#22ff55; --dim:#0f7; --accent:#8aff8a; --grid:#083; --border:#1a3; --card:#000;
}
.retro[data-theme="amber"]{ --fg:#ffbf00; --dim:#c98a00; --accent:#ffd45c; --grid:#7a4a00; --border:#a86700; }
.retro[data-theme="ice"]  { --fg:#00e5ff; --dim:#00a8bf; --accent:#7ff1ff; --grid:#006b77; --border:#0091a3; }
.retro[data-theme="doom"] { --fg:#ff3b3b; --dim:#c21f1f; --accent:#ff8080; --grid:#5d0d0d; --border:#7f1b1b; }

html,body{background:#000}
.page{background:transparent}
.retro{
  position:relative; color:var(--fg); font-family: ui-monospace, Menlo, Consolas, "Liberation Mono", monospace;
  letter-spacing:.3px; text-shadow: 0 0 6px color-mix(in srgb, var(--fg) 50%, transparent);
  border-radius:14px; padding:14px;
  box-shadow: 0 0 0 1px var(--border), inset 0 0 24px rgba(0,0,0,.8);
  background: radial-gradient(1200px 600px at 50% -20%, rgba(255,255,255,.05), transparent 60%),
              repeating-linear-gradient(0deg, rgba(255,255,255,.05) 0px, rgba(255,255,255,.05) 1px, transparent 2px, transparent 4px),
              #000;
  overflow:hidden;
}
/* vignette */
.retro:after{
  content:""; position:absolute; inset:0;
  background: radial-gradient(1200px 600px at 50% -20%, transparent, rgba(0,0,0,.35) 65%),
              radial-gradient(1200px 800px at 50% 120%, transparent, rgba(0,0,0,.55) 60%);
  pointer-events:none;
}
/* grid glow */
.retro:before{
  content:""; position:absolute; inset:0; opacity:.08; pointer-events:none;
  background: repeating-linear-gradient(90deg, var(--grid) 0, var(--grid) 1px, transparent 2px, transparent 12px),
              repeating-linear-gradient(0deg,  var(--grid) 0, var(--grid) 1px, transparent 2px, transparent 12px);
}

/* ===== HERO DOS banner ===== */
.hero{
  border:1px solid var(--border); background:var(--card);
  padding:16px; border-radius:10px; margin-bottom:12px;
  box-shadow: inset 0 0 0 2px rgba(255,255,255,.03);
}
.hero .logo{font-weight:700; font-size:18px}
.hero .banner{white-space:pre; line-height:1.15; font-weight:700; margin:4px 0 8px 0}
.blink{animation:blink 1.1s steps(1,start) infinite}
@keyframes blink{50%{opacity:.25}}

/* ===== DOS prompt search ===== */
.prompt{display:flex; align-items:center; gap:8px; margin:6px 0}
.prompt .path{color:var(--dim)}
#q{
  flex:1; background:transparent; border:none; outline:none; color:var(--fg);
  caret-color:var(--accent); font:inherit; padding:2px 0;
  border-bottom:1px dashed var(--border);
}
.small{opacity:.8; font-size:13px}

/* ===== palette buttons ===== */
.palette{display:flex; gap:6px; flex-wrap:wrap; margin-top:6px}
.palette button{
  background:transparent; color:var(--fg); border:1px solid var(--border);
  padding:2px 8px; border-radius:6px; cursor:pointer
}
.palette button:hover{box-shadow:0 0 8px color-mix(in srgb, var(--fg) 30%, transparent);}

/* ===== cards (MS-DOS windows) ===== */
.cards{display:grid; grid-template-columns:repeat(auto-fill,minmax(260px,1fr)); gap:10px; margin-top:10px}
.card{
  display:block; color:var(--fg); text-decoration:none; background:var(--card);
  border:1px solid var(--border); border-radius:8px; padding:12px;
  box-shadow: 0 0 0 2px rgba(255,255,255,.03), 0 0 18px rgba(0,255,128,.04);
  transition: transform .08s linear, box-shadow .12s ease;
}
.card:hover{ transform: translateY(-1px) scale(1.01);
  box-shadow: 0 0 0 2px rgba(255,255,255,.05), 0 0 22px color-mix(in srgb, var(--fg) 18%, transparent); }
.card h3{margin:0 0 4px 0; font-weight:700}
.card p{margin:0 0 6px 0; color:var(--accent)}
.pills{display:flex; gap:6px; flex-wrap:wrap}
.pill{font-size:12px; padding:1px 6px; border:1px dashed var(--border); border-radius:4px}

/* table-like counter line */
.hr{margin:10px 0; border-top:1px dashed var(--border)}
.count{font-weight:700}
a{color:var(--accent); text-decoration:none}
a:hover{text-decoration:underline}
</style>

<div class="retro" id="retro" data-theme="green">
  <div class="hero">
    <div class="logo">[ DevOps/SRE FastTrack ]</div>
    <div class="banner">██ DEVOPS ░ SRE ░ FASTTRACK ██
Сборка учебника: теория → практика → самопроверка → чек-лист</div>

    <div class="prompt">
      <span class="path">C:\DEVOPS></span>
      <input id="q" placeholder="find \"kubernetes | ansible | ci/cd | linux\"">
      <span class="blink">▌</span>
    </div>
    <div class="small">[Подсказка] Нажми <span style="border:1px solid var(--border);padding:0 4px">/</span> — фокус на поиск. Введи «iddqd» — включить DOOM-палитру.</div>

    <div class="hr"></div>
    <div class="small">Палитра:
      <span class="palette">
        <button data-theme="green">[ GREEN ]</button>
        <button data-theme="amber">[ AMBER ]</button>
        <button data-theme="ice">[ ICE ]</button>
        <button data-theme="doom">[ DOOM ]</button>
      </span>
      <span class="count" style="float:right">Modules: <span id="cnt">{{ site.modules | size }}</span></span>
    </div>
  </div>

  <div class="cards" id="cards">
    {% assign list = site.modules | sort: "order" %}
    {% for m in list %}
    <a class="card"
       href="{{ m.url | relative_url }}"
       data-title="{{ m.title | escape }}"
       data-summary="{{ m.summary | default: 'В разработке' | escape }}"
       data-tags="{{ m.tags | join: ' ' | escape }}">
      <h3>{{ m.title }}</h3>
      <p>{{ m.summary | default: "В разработке" }}</p>
      <div class="pills">
        <span class="pill">{{ m.track | default: "Core" }}</span>
        <span class="pill">{{ m.time | default: "90–120 мин" }}</span>
        {% if m.tags %}{% for t in m.tags %}<span class="pill">{{ t }}</span>{% endfor %}{% endif %}
      </div>
    </a>
    {% endfor %}
  </div>
</div>

<script>
(function(){
  const root = document.getElementById('retro');
  const q = document.getElementById('q');
  const cnt = document.getElementById('cnt');
  const cards = Array.from(document.querySelectorAll('#cards .card'));

  function apply(){
    const s = q.value.toLowerCase().trim();
    let visible=0;
    cards.forEach(c=>{
      const hay=(c.dataset.title+' '+c.dataset.summary+' '+c.dataset.tags).toLowerCase();
      const ok = !s || hay.includes(s);
      c.style.display = ok ? '' : 'none';
      if(ok) visible++;
    });
    cnt.textContent = visible;
  }
  q.addEventListener('input', apply);
  document.addEventListener('keydown', (e)=>{
    if(e.key === '/' && document.activeElement !== q){ e.preventDefault(); q.focus(); }
  });
  apply();

  // Palette switcher + persist
  const saved = localStorage.getItem('retro-theme');
  if(saved) root.setAttribute('data-theme', saved);
  document.querySelectorAll('.palette [data-theme]').forEach(btn=>{
    btn.addEventListener('click', ()=>{
      const th = btn.getAttribute('data-theme');
      root.setAttribute('data-theme', th);
      localStorage.setItem('retro-theme', th);
    });
  });

  // Easter egg: DOOM (type iddqd)
  let seq = '';
  document.addEventListener('keydown', (e)=>{
    if(/^[a-zA-Z]$/.test(e.key)) { seq = (seq + e.key.toLowerCase()).slice(-5); }
    if(seq === 'iddqd'){ root.setAttribute('data-theme','doom'); localStorage.setItem('retro-theme','doom'); seq=''; }
  });
})();
</script>
