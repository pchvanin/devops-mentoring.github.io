---
layout: page
title: "DevOps/SRE FastTrack — Home"
---

<!-- Apple-like minimal UI: clean type, glass nav, big hero, elegant tiles -->
<style>
/* ===== Base & variables ===== */
:root{
  --bg:#fbfbfd; --panel:#ffffff; --text:#0b0b0f; --muted:#6b7280; --link:#0a84ff;
  --border:rgba(0,0,0,.08); --shadow:0 12px 30px rgba(0,0,0,.08);
  --radius:18px; --radius-sm:14px; --maxw:1180px;
  --tileA:linear-gradient(135deg,#eef2ff, #fafafa);
  --tileB:linear-gradient(135deg,#f5f9ff, #fafafa);
  --tileC:linear-gradient(135deg,#fff5f2, #fafafa);
}
@media (prefers-color-scheme: dark){
  :root{
    --bg:#0f1113; --panel:#14171a; --text:#f3f4f6; --muted:#a0a6ad;
    --border:rgba(255,255,255,.08); --shadow:0 14px 34px rgba(0,0,0,.45);
    --tileA:linear-gradient(135deg,#1b2333,#121416);
    --tileB:linear-gradient(135deg,#141e29,#121416);
    --tileC:linear-gradient(135deg,#221818,#121416);
  }
}

html, body, .page{ background:var(--bg); color:var(--text) }
*{ box-sizing:border-box }
h1,h2,h3{ letter-spacing:.2px; line-height:1.15 }
.wrap{ max-width:var(--maxw); margin:0 auto; padding:0 20px }

/* ===== Glass navbar ===== */
.nav{
  position:sticky; top:0; z-index:10;
  backdrop-filter:saturate(180%) blur(16px);
  -webkit-backdrop-filter:saturate(180%) blur(16px);
  background: color-mix(in srgb, var(--bg) 70%, transparent);
  border-bottom:1px solid var(--border);
}
.nav .inner{ display:flex; align-items:center; justify-content:space-between; height:56px }
.brand{ display:flex; gap:10px; align-items:center; font-weight:700 }
.brand .dot{ width:10px; height:10px; border-radius:50%; background:#0a84ff; box-shadow:0 0 0 3px rgba(10,132,255,.15) }
.nav a{ color:var(--text); text-decoration:none; opacity:.8 }
.nav a:hover{ opacity:1 }

/* ===== Hero ===== */
.hero{ margin:26px 0 18px; }
.hero .panel{
  border:1px solid var(--border); border-radius:var(--radius);
  background:var(--panel); box-shadow:var(--shadow);
  padding:40px 36px;
}
.hero h1{ font-size:clamp(32px,4vw,54px); margin:0 0 8px 0 }
.hero p{ margin:0; font-size:18px; color:var(--muted) }
.hero .cta{ margin-top:18px; display:flex; gap:12px; flex-wrap:wrap }
.btn{
  display:inline-flex; align-items:center; gap:8px;
  background:#0a84ff; color:#fff; text-decoration:none;
  padding:12px 18px; border-radius:999px; font-weight:600; box-shadow:var(--shadow)
}
.btn.ghost{
  background:transparent; color:var(--text);
  border:1px solid var(--border); padding:12px 16px
}

/* ===== Search ===== */
.search{ margin-top:18px; display:flex; align-items:center }
.search .input{ position:relative; width:100% }
.search input{
  width:100%; height:52px; border-radius:999px; border:1px solid var(--border);
  background:var(--panel); padding:0 46px 0 46px; color:var(--text);
  outline:none; box-shadow:var(--shadow); transition:border .15s ease, box-shadow .15s ease;
}
.search input:focus{ border-color:#0a84ff; box-shadow:0 0 0 4px color-mix(in srgb,#0a84ff 20%, transparent) }
.search .icon{ position:absolute; left:16px; top:50%; translate:0 -50%; opacity:.6 }
.search .kbd{ position:absolute; right:12px; top:50%; translate:0 -50%;
  border:1px solid var(--border); border-bottom-width:2px; border-radius:8px; padding:3px 8px; color:var(--muted) }
.meta{ margin-top:10px; color:var(--muted); font-weight:600 }

/* ===== Tiles (modules) ===== */
.tiles{ display:grid; grid-template-columns:repeat(12,1fr); gap:16px; margin:18px 0 10px }
.tile{
  grid-column: span 4; min-height: 170px;
  display:block; text-decoration:none; color:inherit;
  border:1px solid var(--border); border-radius:var(--radius-sm); overflow:hidden;
  background:var(--panel); box-shadow:var(--shadow); transition:transform .16s ease, box-shadow .2s ease, border-color .2s ease;
}
@media (max-width: 900px){ .tile{ grid-column: span 6 } }
@media (max-width: 640px){ .tile{ grid-column: span 12 } }
.tile:hover{ transform:translateY(-3px); box-shadow:0 20px 40px rgba(0,0,0,.14) }
.tile .heroA{ background:var(--tileA); height:56px; border-bottom:1px solid var(--border) }
.tile .heroB{ background:var(--tileB); height:56px; border-bottom:1px solid var(--border) }
.tile .heroC{ background:var(--tileC); height:56px; border-bottom:1px solid var(--border) }
.tile .inner{ padding:14px 16px }
.tile h3{ margin:0 0 6px 0; font-size:20px }
.tile p{ margin:0; color:var(--muted); min-height:44px }
.pills{ display:flex; gap:8px; flex-wrap:wrap; margin-top:12px }
.pill{
  font-size:12px; padding:4px 10px; border-radius:999px;
  border:1px solid var(--border); background:color-mix(in srgb, var(--panel) 90%, transparent); color:var(--text)
}

/* ===== Footer note ===== */
.note{ margin:14px 0 28px; color:var(--muted); font-size:14px }
a.inline{ color:#0a84ff; text-decoration:none }
a.inline:hover{ text-decoration:underline }
</style>

<!-- ===== NAVBAR ===== -->
<div class="nav">
  <div class="wrap inner">
    <div class="brand"><span class="dot"></span> DevOps/SRE FastTrack</div>
    <nav style="display:flex; gap:16px">
      <a href="{{ '/' | relative_url }}">Главная</a>
      <a href="{{ '/modules/00-foundations/' | relative_url }}">Начать</a>
      <a href="https://github.com/{{ site.github.owner_name }}/{{ site.github.repository_name }}">GitHub</a>
    </nav>
  </div>
</div>

<!-- ===== HERO ===== -->
<div class="wrap hero">
  <div class="panel">
    <h1>Курс DevOps/SRE до уровня Middle</h1>
    <p>Лаконичные уроки, практикум и самопроверка. От Linux и сетей до Kubernetes, CI/CD и SRE.</p>

    <div class="cta">
      <a class="btn" href="{{ '/modules/00-foundations/' | relative_url }}">Начать с Модуля 00</a>
      <a class="btn ghost" href="{{ '/modules/07-kubernetes/' | relative_url }}">Сразу к Kubernetes</a>
    </div>

    <div class="search" aria-label="Поиск модулей">
      <div class="input">
        <svg class="icon" width="20" height="20" viewBox="0 0 24 24" fill="none" aria-hidden="true">
          <path d="M21 21l-4.2-4.2M10.5 18a7.5 7.5 0 1 1 0-15 7.5 7.5 0 0 1 0 15Z" stroke="currentColor" stroke-width="1.6" />
        </svg>
        <input id="q" placeholder="Быстрый поиск по модулям… (нажми /)">
        <span class="kbd">/</span>
      </div>
    </div>
    <div class="meta">Доступно модулей: <span id="cnt">{{ site.modules | size }}</span></div>
  </div>
</div>

<!-- ===== MODULE TILES ===== -->
<div class="wrap tiles" id="tiles">
  {% assign list = site.modules | sort: "order" %}
  {% for m in list %}
    {% assign stripe = m.order | modulo: 3 %}
    <a class="tile" href="{{ m.url | relative_url }}"
       data-title="{{ m.title | escape }}"
       data-summary="{{ m.summary | default: 'В разработке' | escape }}"
       data-tags="{{ m.tags | join: ' ' | escape }}">
      <div class="{% if stripe == 0 %}heroA{% elsif stripe == 1 %}heroB{% else %}heroC{% endif %}"></div>
      <div class="inner">
        <h3>{{ m.title }}</h3>
        <p>{{ m.summary | default: "В разработке" }}</p>
        <div class="pills">
          <span class="pill">{{ m.track | default: "Core" }}</span>
          <span class="pill">{{ m.time | default: "90–120 мин" }}</span>
          {% if m.tags %}{% for t in m.tags %}<span class="pill">{{ t }}</span>{% endfor %}{% endif %}
        </div>
      </div>
    </a>
  {% endfor %}
</div>

<div class="wrap note">
  Совет: учись «в продакшн-манере» — маленькие изменения, частые коммиты, всё как код. Есть идеи — присылай PR в репозиторий.
</div>

<!-- ===== JS: search filter + hotkey ===== -->
<script>
(function(){
  const q = document.getElementById('q');
  const cnt = document.getElementById('cnt');
  const tiles = Array.from(document.querySelectorAll('#tiles .tile'));

  function apply(){
    const s = q.value.toLowerCase().trim();
    let visible = 0;
    tiles.forEach(t=>{
      const hay = (t.dataset.title + ' ' + t.dataset.summary + ' ' + t.dataset.tags).toLowerCase();
      const ok = !s || hay.includes(s);
      t.style.display = ok ? '' : 'none';
      if(ok) visible++;
    });
    cnt.textContent = visible;
  }
  q.addEventListener('input', apply);
  document.addEventListener('keydown', e=>{
    if(e.key === '/' && document.activeElement !== q){ e.preventDefault(); q.focus(); }
  });
  apply();
})();
</script>
