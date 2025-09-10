---
layout: page
title: "DevOps/SRE FastTrack — Home"
---

<!-- Premium fonts -->
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@300..900&family=Playfair+Display:wght@400..900&display=swap" rel="stylesheet">

<style>
/* ===== LUX THEME (Inter + Playfair) ===== */
:root{
  --bg:#F5F4F2; --panel:#FFFFFF; --text:#171717; --muted:#6E6B66; --link:#0A84FF;
  --border:rgba(20,20,20,.08); --shadow:0 18px 38px rgba(44,32,22,.10);
  --radius:20px; --radius-sm:16px; --maxw:1180px;
  --tileA:linear-gradient(135deg,#fff,#F7F5F2);
  --tileB:linear-gradient(135deg,#fff,#F4F7FA);
  --tileC:linear-gradient(135deg,#fff,#F8F4FF);
}
@media (prefers-color-scheme: dark){
  :root{
    --bg:#0F1113; --panel:#14171A; --text:#F2F2F3; --muted:#A0A6AD; --link:#86b7ff;
    --border:rgba(255,255,255,.08); --shadow:0 18px 34px rgba(0,0,0,.45);
    --tileA:linear-gradient(135deg,#1b1f24,#16181c);
    --tileB:linear-gradient(135deg,#161c22,#14171a);
    --tileC:linear-gradient(135deg,#1f1824,#14171a);
  }
}

html, body, .page{ background:var(--bg); color:var(--text) }
*{ box-sizing:border-box }
h1,h2,h3{ line-height:1.15; letter-spacing:-0.02em }
.wrap{ max-width:var(--maxw); margin:0 auto; padding:0 22px }
a{ color:var(--link); text-decoration:none } a:hover{ text-decoration:underline }

/* Typography */
body{
  font-family:"Inter",system-ui,-apple-system,"Segoe UI",Roboto,"Helvetica Neue",Arial,"Noto Sans","Liberation Sans",sans-serif;
  font-optical-sizing:auto; -webkit-font-smoothing:antialiased; text-rendering:optimizeLegibility; line-height:1.6;
}
h1,h2,h3{ font-family:"Playfair Display",Georgia,"Times New Roman",serif }
h1{ font-weight:700 } h2{ font-weight:700 } h3{ font-weight:700 }

/* Glass navbar */
.nav{
  position:sticky; top:0; z-index:10; border-bottom:1px solid var(--border);
  backdrop-filter:saturate(180%) blur(16px); -webkit-backdrop-filter:saturate(180%) blur(16px);
  background:color-mix(in srgb, var(--bg) 70%, transparent);
}
.nav .inner{ height:64px; display:flex; align-items:center; justify-content:space-between }
.brand{ display:flex; align-items:center; gap:10px; font-weight:700; letter-spacing:.01em }
.brand .mark{ width:10px; height:10px; border-radius:50%; background:#9A7B5D; box-shadow:0 0 0 4px rgba(154,123,93,.18) }
.nav a{ color:var(--text); text-decoration:none; opacity:.85 } .nav a:hover{ opacity:1 }

/* Hero */
.hero{ margin:28px 0 20px }
.panel{
  border:1px solid var(--border); border-radius:var(--radius); background:var(--panel); box-shadow:var(--shadow);
  padding:44px 40px;
}
.hero h1{ margin:0 0 10px; font-size:clamp(36px,4.6vw,58px) }
.hero p{ margin:0; font-size:18px; color:var(--muted) }
.cta{ margin-top:22px; display:flex; gap:12px; flex-wrap:wrap }
.btn{
  display:inline-flex; align-items:center; gap:10px; border-radius:999px; font-weight:600;
  padding:14px 18px; text-decoration:none; box-shadow:var(--shadow)
}
.btn.primary{ background:#1C1C1C; color:#fff; border:1px solid rgba(0,0,0,.12) }
@media (prefers-color-scheme: dark){ .btn.primary{ background:#EAEAEA; color:#0f1113; border-color:rgba(255,255,255,.14) } }
.btn.ghost{ background:transparent; color:var(--text); border:1px solid var(--border) }

/* Search */
.search{ margin-top:20px }
.search .input{ position:relative }
.search input{
  width:100%; height:54px; border-radius:999px; border:1px solid var(--border);
  background:var(--panel); padding:0 54px; color:var(--text);
  outline:none; box-shadow:var(--shadow); transition:border .15s ease, box-shadow .15s ease;
}
.search input:focus{ border-color:#9A7B5D; box-shadow:0 0 0 5px color-mix(in srgb,#9A7B5D 22%, transparent) }
.search .icon{ position:absolute; left:18px; top:50%; translate:0 -50%; opacity:.55 }
.search .kbd{ position:absolute; right:16px; top:50%; translate:0 -50%;
  border:1px solid var(--border); border-bottom-width:2px; border-radius:8px; padding:3px 8px; color:var(--muted) }
.meta{ margin-top:12px; color:var(--muted); font-weight:600 }

/* Tiles */
.tiles{ display:grid; grid-template-columns:repeat(12,1fr); gap:18px; margin:22px 0 12px }
.tile{
  grid-column:span 4; min-height:190px; display:block; text-decoration:none; color:inherit;
  border:1px solid var(--border); border-radius:var(--radius-sm); overflow:hidden;
  background:var(--panel); box-shadow:var(--shadow);
  transition:transform .16s ease, box-shadow .22s ease, border-color .22s ease;
}
@media (max-width: 980px){ .tile{ grid-column:span 6 } }
@media (max-width: 640px){ .tile{ grid-column:span 12 } }
.tile:hover{ transform:translateY(-3px); box-shadow:0 28px 56px rgba(0,0,0,.12) }
.tile .capA,.tile .capB,.tile .capC{ height:64px; border-bottom:1px solid var(--border) }
.tile .capA{ background:var(--tileA) } .tile .capB{ background:var(--tileB) } .tile .capC{ background:var(--tileC) }
.tile .inner{ padding:16px 18px }
.tile h3{ margin:0 0 8px; font-size:22px }
.tile p{ margin:0; color:var(--muted); min-height:46px }
.pills{ display:flex; gap:8px; flex-wrap:wrap; margin-top:12px }
.pill{
  font-size:12px; padding:5px 11px; border-radius:999px;
  border:1px solid var(--border); background:color-mix(in srgb, var(--panel) 92%, transparent); color:var(--text); font-weight:600;
}

/* Footer note */
.note{ margin:16px 0 30px; color:var(--muted); font-size:14px }
</style>

<!-- NAV -->
<div class="nav">
  <div class="wrap inner">
    <div class="brand"><span class="mark"></span> DevOps/SRE FastTrack</div>
    <nav style="display:flex; gap:18px">
      <a href="{{ '/' | relative_url }}">Главная</a>
      <a href="{{ '/modules/00-foundations/' | relative_url }}">Старт</a>
      <a href="https://github.com/{{ site.github.owner_name }}/{{ site.github.repository_name }}">GitHub</a>
    </nav>
  </div>
</div>

<!-- HERO -->
<div class="wrap hero">
  <div class="panel">
    <h1>DevOps/SRE до уровня Middle</h1>
    <p>Лаконичные материалы, сильная практика и самопроверка. От Linux и сетей до Kubernetes, CI/CD и SRE.</p>

    <div class="cta">
      <a class="btn primary" href="{{ '/modules/00-foundations/' | relative_url }}">Начать курс</a>
      <a class="btn ghost" href="{{ '/modules/07-kubernetes/' | relative_url }}">Сразу к Kubernetes</a>
    </div>

    <div class="search" aria-label="Поиск модулей">
      <div class="input">
        <svg class="icon" width="20" height="20" viewBox="0 0 24 24" fill="none" aria-hidden="true">
          <path d="M21 21l-4.2-4.2M10.5 18a7.5 7.5 0 1 1 0-15 7.5 7.5 0 0 1 0 15Z" stroke="currentColor" stroke-width="1.6" />
        </svg>
        <input id="q" placeholder="Поиск по модулям… (нажми /)">
        <span class="kbd">/</span>
      </div>
    </div>
    <div class="meta">Доступно модулей: <span id="cnt">{{ site.modules | size }}</span></div>
  </div>
</div>

<!-- TILES -->
<div class="wrap tiles" id="tiles">
  {% assign list = site.modules | sort: "order" %}
  {% for m in list %}
    {% assign stripe = m.order | modulo: 3 %}
    <a class="tile" href="{{ m.url | relative_url }}"
       data-title="{{ m.title | escape }}"
       data-summary="{{ m.summary | default: 'В разработке' | escape }}"
       data-tags="{{ m.tags | join: ' ' | escape }}">
      <div class="{% if stripe == 0 %}capA{% elsif stripe == 1 %}capB{% else %}capC{% endif %}"></div>
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
  Совет: двигайся маленькими шагами, делай частые коммиты и держи всё как код. Нашёл неточность — PR приветствуется.
</div>

<script>
(function(){
  const q = document.getElementById('q');
  const cnt = document.getElementById('cnt');
  const tiles = Array.from(document.querySelectorAll('#tiles .tile'));

  function apply(){
    const s = q.value.toLowerCase().trim();
    let visible=0;
    tiles.forEach(t=>{
      const hay=(t.dataset.title+' '+t.dataset.summary+' '+t.dataset.tags).toLowerCase();
      const ok=!s || hay.includes(s);
      t.style.display = ok ? '' : 'none';
      if(ok) visible++;
    });
    cnt.textContent = visible;
  }
  q.addEventListener('input', apply);
  document.addEventListener('keydown', e=>{
    if(e.key==='/' && document.activeElement!==q){ e.preventDefault(); q.focus(); }
  });
  apply();
})();
</script>
