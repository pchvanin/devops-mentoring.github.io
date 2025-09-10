---
layout: page
title: "DevOps/SRE FastTrack — DOOM Edition"
---

<style>
/* ===== DOOM THEME (читабельно) ===== */
:root{
  --bg: #0c0d0f;          /* графитовый фон */
  --surface:#15171a;      /* фон карточек */
  --border:#2c2f36;       /* границы */
  --text:#e8e6df;         /* основной текст */
  --muted:#a7a7a7;        /* вторичный */
  --accent:#ff3b3b;       /* алый DOOM */
  --accent2:#f2a900;      /* золотой акцент */
  --shadow:0 2px 10px rgba(0,0,0,.35);
  --round:14px;
}

body, .page{ background: var(--bg); color: var(--text); }
.page{ padding-top: 0; }

/* HERO */
.hero{
  position:relative;
  margin:-8px 0 18px 0;
  border-radius: var(--round);
  background:
    linear-gradient(180deg, rgba(255,59,59,.14), transparent 40%),
    linear-gradient(90deg, #751c1c 0%, #241c1c 60%);
  border:1px solid #3b2323;
  box-shadow: var(--shadow), inset 0 0 0 1px rgba(255,255,255,.04);
  padding:22px 18px;
}
.hero h1{
  margin:2px 0 8px 0;
  font-size: clamp(28px,3.6vw,42px);
  letter-spacing: .5px;
  text-shadow: 0 2px 0 rgba(0,0,0,.4);
}
.hero p{ margin:0 0 14px 0; color: var(--muted); font-size: 16px; }

.controls{ display:flex; gap:10px; flex-wrap:wrap; align-items:center; }
.toggle{
  display:inline-flex; gap:8px; align-items:center;
  background: #1b1e23; border:1px solid var(--border); color: var(--text);
  padding:8px 10px; border-radius: 10px; cursor:pointer; user-select:none;
}
.toggle input{ accent-color: var(--accent); }

/* SEARCH */
.search{
  display:flex; align-items:center; gap:10px; margin-top:8px;
}
#q{
  flex:1; height:46px; padding:0 14px;
  background:#121417; color:var(--text);
  border:1px solid var(--border); border-radius: 10px;
  outline:none; box-shadow: var(--shadow);
}
#q:focus{ border-color: var(--accent); box-shadow: 0 0 0 2px rgba(255,59,59,.25); }
.count{ margin-top:8px; font-weight:600; color: var(--muted); }

/* CARDS */
.cards{ display:grid; grid-template-columns:repeat(auto-fill,minmax(270px,1fr)); gap:14px; margin-top:10px; }
.card{
  display:block; text-decoration:none; color:inherit;
  background: var(--surface); border:1px solid var(--border); border-radius: 12px;
  box-shadow: var(--shadow); padding: 0; overflow:hidden; transition: transform .1s ease, box-shadow .15s ease;
}
.card:hover{ transform: translateY(-2px); box-shadow: 0 6px 22px rgba(0,0,0,.45); }

/* верхняя «HUD» полоса */
.card .bar{
  height:8px;
  background: linear-gradient(90deg, var(--accent) 0%, #b21e1e 40%, #6a1515 100%);
  border-bottom:1px solid #3b2323;
}
.card .inner{ padding:14px; }
.card h3{ margin:0 0 6px 0; font-size: 18px; }
.card p{ margin:0; color: var(--muted); min-height: 40px; }

.pills{ display:flex; gap:8px; flex-wrap:wrap; margin-top:10px; }
.pill{
  font-size:12px; padding:3px 8px; border-radius:999px;
  border:1px solid var(--border); background:#101216; color:var(--text);
}
.pill.core{ border-color:#592222; background:#1a1212; color:#ffb3b3; }
.pill.time{ border-color:#4a3a00; background:#181308; color:#ffd777; }

/* CRT FX (мягкий, опциональный) */
.crt{ position:relative; }
.crt:before{
  content:""; position:absolute; inset:0; pointer-events:none; opacity:.07;
  background:
    repeating-linear-gradient(0deg, rgba(255,255,255,.15) 0px, rgba(255,255,255,.15) 1px, transparent 2px, transparent 4px);
  mix-blend-mode: screen; border-radius: var(--round);
}

/* HIGH CONTRAST mode */
:root[data-contrast="on"]{
  --muted:#d7d6cf;
  --border:#3a3e46;
}

/* small helper */
.kbd{display:inline-block;border:1px solid var(--border);border-bottom-width:2px;border-radius:6px;padding:2px 6px;background:#101216}
</style>

<div class="hero crt" id="hero">
  <h1>DOOM Edition — DevOps/SRE FastTrack</h1>
  <p>Улучшенная читабельность: крупный шрифт, минимум «CRT», контрастные алые акценты. Формат курса: краткая теория → практика → самопроверка → чек-лист.</p>

  <div class="controls">
    <label class="toggle"><input type="checkbox" id="fx"> CRT FX</label>
    <label class="toggle"><input type="checkbox" id="hc"> High-contrast</label>
    <span class="toggle" id="bigger">A↑</span>
    <span class="toggle" id="smaller">A↓</span>
    <span class="count">Модулей: <strong id="cnt">{{ site.modules | size }}</strong></span>
  </div>

  <div class="search">
    <input id="q" placeholder="Поиск по модулям… (например: kubernetes, ansible, ci/cd). Нажми «/» чтобы сфокусировать.">
  </div>
</div>

<div class="cards" id="cards">
{% assign list = site.modules | sort: "order" %}
{% for m in list %}
  <a class="card" href="{{ m.url | relative_url }}"
     data-title="{{ m.title | escape }}"
     data-summary="{{ m.summary | default: 'В разработке' | escape }}"
     data-tags="{{ m.tags | join: ' ' | escape }}">
    <div class="bar"></div>
    <div class="inner">
      <h3>{{ m.title }}</h3>
      <p>{{ m.summary | default: "В разработке" }}</p>
      <div class="pills">
        <span class="pill core">{{ m.track | default: "Core" }}</span>
        <span class="pill time">{{ m.time | default: "90–120 мин" }}</span>
        {% if m.tags %}{% for t in m.tags %}<span class="pill">{{ t }}</span>{% endfor %}{% endif %}
      </div>
    </div>
  </a>
{% endfor %}
</div>

<script>
(function(){
  const q = document.getElementById('q');
  const cnt = document.getElementById('cnt');
  const cards = Array.from(document.querySelectorAll('#cards .card'));
  const hero = document.getElementById('hero');
  const fx = document.getElementById('fx');
  const hc = document.getElementById('hc');
  const bigger = document.getElementById('bigger');
  const smaller = document.getElementById('smaller');

  // --- Filter
  function apply(){
    const s = q.value.toLowerCase().trim();
    let visible=0;
    cards.forEach(c=>{
      const hay=(c.dataset.title+' '+c.dataset.summary+' '+c.dataset.tags).toLowerCase();
      const ok=!s || hay.includes(s);
      c.style.display = ok ? '' : 'none';
      if(ok) visible++;
    });
    cnt.textContent = visible;
  }
  q.addEventListener('input', apply);
  document.addEventListener('keydown', e=>{
    if(e.key === '/' && document.activeElement !== q){ e.preventDefault(); q.focus(); }
  });
  apply();

  // --- CRT FX toggle (soft)
  const fxSaved = localStorage.getItem('doom-crt') === 'on';
  fx.checked = fxSaved;
  hero.classList.toggle('crt', fx.checked);
  fx.addEventListener('change', ()=>{
    hero.classList.toggle('crt', fx.checked);
    localStorage.setItem('doom-crt', fx.checked ? 'on' : 'off');
  });

  // --- High contrast toggle
  const hcSaved = localStorage.getItem('doom-contrast') === 'on';
  if(hcSaved) document.documentElement.setAttribute('data-contrast','on');
  hc.checked = hcSaved;
  hc.addEventListener('change', ()=>{
    if(hc.checked) document.documentElement.setAttribute('data-contrast','on');
    else document.documentElement.removeAttribute('data-contrast');
    localStorage.setItem('doom-contrast', hc.checked ? 'on' : 'off');
  });

  // --- Font size quick controls
  const root = document.documentElement;
  const key = 'doom-fontscale';
  const scale = parseFloat(localStorage.getItem(key) || '1');
  root.style.fontSize = (scale*100) + '%';
  function setScale(v){ root.style.fontSize=(v*100)+'%'; localStorage.setItem(key, v.toFixed(2)); }
  bigger.addEventListener('click', ()=> setScale(Math.min(1.4, (parseFloat(localStorage.getItem(key) || '1') + 0.05))));
  smaller.addEventListener('click',()=> setScale(Math.max(0.85,(parseFloat(localStorage.getItem(key) || '1') - 0.05))));
})();
</script>
