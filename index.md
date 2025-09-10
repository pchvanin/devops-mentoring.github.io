---
layout: page
title: "DevOps/SRE FastTrack — Home"
---

<!-- Apple/Loft minimal UI: all-in-one CSS + JS -->
<style>
/* ===== Theme palettes ===== */
:root{
  --bg:#fbfbfd; --text:#0b0b0f; --muted:#6b7280; --panel:#ffffff;
  --border:rgba(0,0,0,.08); --shadow:0 8px 24px rgba(0,0,0,.06);
  --accent:#0A84FF; --pill:#f2f4f7;
  --radius:16px; --radius-sm:12px; --maxw:1100px;
}
:root[data-theme="dark"]{
  --bg:#111315; --text:#f2f2f3; --muted:#a0a6ad; --panel:#16181c;
  --border:rgba(255,255,255,.08); --shadow:0 10px 28px rgba(0,0,0,.45);
  --accent:#0A84FF; --pill:#1f2329;
}
:root[data-theme="loft"]{
  --bg:#F4F1ED; --text:#1b1b1b; --muted:#6e6b66; --panel:#ffffff;
  --border:rgba(20,20,20,.08); --shadow:0 8px 24px rgba(44,32,22,.06);
  --accent:#8E6E53; --pill:#efeae4;
}

/* ===== Base ===== */
body, .page{ background:var(--bg); color:var(--text); }
.page{ padding-top:0 }
*{ box-sizing:border-box }
h1,h2,h3{ letter-spacing:.2px }

/* ===== Container ===== */
.wrap{ max-width:var(--maxw); margin:0 auto; padding:8px 16px }

/* ===== Hero ===== */
.hero{
  border:1px solid var(--border); border-radius:var(--radius);
  background:linear-gradient(180deg, rgba(10,132,255,.06), transparent 40%),
             var(--panel);
  box-shadow:var(--shadow);
  padding:28px 24px; margin:-8px 0 18px 0;
}
.hero h1{ margin:0 0 8px 0; font-size:clamp(28px,3.6vw,40px); }
.hero p{ margin:0; color:var(--muted); font-size:16px }
.controls{ display:flex; gap:10px; flex-wrap:wrap; align-items:center; margin-top:14px }

/* Theme buttons */
.theme{ display:flex; gap:8px; background:var(--pill); border-radius:999px; padding:4px }
.theme button{
  border:1px solid transparent; background:transparent; padding:6px 12px; border-radius:999px;
  color:var(--text); cursor:pointer; font-weight:600
}
.theme button[aria-pressed="true"]{ background:var(--panel); border-color:var(--border); box-shadow:var(--shadow) }

/* Search */
.search{ display:flex; gap:10px; align-items:center; margin-top:10px }
.search .input{
  flex:1; position:relative;
}
.search input{
  width:100%; height:48px; border-radius:999px; border:1px solid var(--border);
  background:var(--panel); color:var(--text); padding:0 44px 0 44px; outline:none;
  box-shadow:var(--shadow); transition:border .15s ease, box-shadow .15s ease;
}
.search input:focus{ border-color:var(--accent); box-shadow:0 0 0 3px color-mix(in srgb, var(--accent) 25%, transparent) }
.search .icon{ position:absolute; left:14px; top:50%; translate:0 -50%; opacity:.6 }
.search .kbd{ position:absolute; right:10px; top:50%; translate:0 -50%;
  border:1px solid var(--border); border-bottom-width:2px; border-radius:8px;
  padding:2px 8px; color:var(--muted); background:var(--panel) }

.meta{ margin-top:8px; color:var(--muted); font-weight:600 }

/* Cards */
.cards{ display:grid; grid-template-columns:repeat(auto-fill,minmax(280px,1fr)); gap:14px; margin-top:14px }
.card{
  display:block; text-decoration:none; color:inherit; background:var(--panel);
  border:1px solid var(--border); border-radius:var(--radius-sm); overflow:hidden;
  box-shadow:var(--shadow); transition: transform .14s ease, box-shadow .18s ease;
}
.card:hover{ transform: translateY(-2px); box-shadow:0 14px 32px rgba(0,0,0,.10) }
.card .inner{ padding:16px 16px 14px }
.card h3{ margin:0 0 6px 0; font-size:18px }
.card p{ margin:0; color:var(--muted); min-height:40px }

/* Pills */
.pills{ display:flex; gap:8px; flex-wrap:wrap; margin-top:12px }
.pill{
  font-size:12px; padding:4px 10px; border-radius:999px;
  border:1px solid var(--border); background:var(--pill); color:var(--text)
}
.pill.core{ border-color:color-mix(in srgb, var(--accent) 22%, var(--border)); }

/* Footer note */
.note{ margin:18px 0 6px; color:var(--muted); font-size:14px }
</style>

<div class="wrap">
  <div class="hero">
    <h1>DevOps/SRE FastTrack</h1>
    <p>Суперлаконичный курс до уровня Middle: теория кратко → практика → самопроверка → чек-лист.</p>

    <div class="controls">
      <div class="theme" role="tablist" aria-label="Theme">
        <button role="tab" data-theme="light" aria-pressed="true">Light</button>
        <button role="tab" data-theme="dark" aria-pressed="false">Dark</button>
        <button role="tab" data-theme="loft" aria-pressed="false">Loft</button>
      </div>
      <div class="meta">Модулей: <span id="cnt">{{ site.modules | size }}</span></div>
    </div>

    <div class="search" aria-label="Search modules">
      <div class="input">
        <svg class="icon" width="20" height="20" viewBox="0 0 24 24" fill="none" aria-hidden="true">
          <path d="M21 21l-4.2-4.2M10.5 18a7.5 7.5 0 1 1 0-15 7.5 7.5 0 0 1 0 15Z" stroke="currentColor" stroke-width="1.6" />
        </svg>
        <input id="q" placeholder="Быстрый поиск по модулям… (нажми /)">
        <span class="kbd">/</span>
      </div>
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
      <div class="inner">
        <h3>{{ m.title }}</h3>
        <p>{{ m.summary | default: "В разработке" }}</p>
        <div class="pills">
          <span class="pill core">{{ m.track | default: "Core" }}</span>
          <span class="pill">{{ m.time | default: "90–120 мин" }}</span>
          {% if m.tags %}{% for t in m.tags %}<span class="pill">{{ t }}</span>{% endfor %}{% endif %}
        </div>
      </div>
    </a>
    {% endfor %}
  </div>

  <p class="note">Совет: маленькие шаги, частые коммиты, всё — как код. Хоткей для поиска — «/».</p>
</div>

<script>
(function(){
  // --- THEME
  const root = document.documentElement;
  const saved = localStorage.getItem('course-theme');
  if(saved){ root.setAttribute('data-theme', saved); document.querySelectorAll('.theme [data-theme]').forEach(b=>b.setAttribute('aria-pressed', b.dataset.theme===saved)); }

  document.querySelectorAll('.theme [data-theme]').forEach(btn=>{
    btn.addEventListener('click', ()=>{
      document.querySelectorAll('.theme [data-theme]').forEach(b=>b.setAttribute('aria-pressed','false'));
      btn.setAttribute('aria-pressed','true');
      const th = btn.getAttribute('data-theme');
      root.setAttribute('data-theme', th==='light' ? '' : th); // пусто = light
      localStorage.setItem('course-theme', th);
    });
  });

  // --- FILTER
  const q = document.getElementById('q');
  const cnt = document.getElementById('cnt');
  const cards = Array.from(document.querySelectorAll('#cards .card'));
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
    if(e.key==='/' && document.activeElement!==q){ e.preventDefault(); q.focus(); }
  });
  apply();
})();
</script>
