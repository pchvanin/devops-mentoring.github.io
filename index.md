---
layout: page
title: "DevOps/SRE FastTrack"
---

<!-- Inter + Playfair (минимум запросов, премиум-вид) -->
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600&family=Playfair+Display:wght@700&display=swap" rel="stylesheet">

<style>
/* ===== Ultra-minimal / auto light–dark ===== */
:root{
  --bg:#fbfbfd; --text:#0b0b0f; --muted:#6b7280; --panel:#ffffff;
  --border:rgba(0,0,0,.08);
  --radius:14px; --maxw:980px;
}
@media (prefers-color-scheme: dark){
  :root{
    --bg:#0f1113; --text:#f2f2f3; --muted:#a0a6ad; --panel:#14171a;
    --border:rgba(255,255,255,.10);
  }
}
html,body,.page{background:var(--bg);color:var(--text)}
*{box-sizing:border-box}
.wrap{max-width:var(--maxw);margin:0 auto;padding:8px 18px}
h1{font-family:"Playfair Display",Georgia,serif;font-weight:700;letter-spacing:-0.02em;line-height:1.12;
    font-size:clamp(32px,4.2vw,48px);margin:8px 0 6px}
.lead{color:var(--muted);margin:0 0 16px;font:500 16px/1.6 "Inter",system-ui,-apple-system,Segoe UI,Roboto,Arial,sans-serif}

/* Поиск */
.search{margin:6px 0 10px}
.search .input{position:relative}
.search input{
  width:100%;height:48px;border-radius:999px;border:1px solid var(--border);
  background:var(--panel);padding:0 44px;font:400 16px/1 "Inter",system-ui,-apple-system,Segoe UI,Roboto,Arial,sans-serif;
  color:var(--text);outline:none;
}
.search .icon{position:absolute;left:14px;top:50%;translate:0 -50%;opacity:.55}
.search .kbd{position:absolute;right:12px;top:50%;translate:0 -50%;
  border:1px solid var(--border);border-bottom-width:2px;border-radius:8px;padding:2px 8px;color:var(--muted);font:500 12px/1 "Inter",system-ui}
.meta{margin:8px 0 0;color:var(--muted);font:600 13px/1.6 "Inter",system-ui}

/* Список модулей */
.modules{list-style:none;margin:14px 0 24px;padding:0;display:grid;grid-template-columns:repeat(1,1fr);gap:8px}
@media (min-width:760px){ .modules{grid-template-columns:repeat(2,1fr)} }
.mod a{
  display:block;text-decoration:none;color:inherit;background:var(--panel);
  border:1px solid var(--border);border-radius:var(--radius);padding:14px 16px;transition:transform .08s ease;
}
.mod a:hover{transform:translateY(-1px)}
.mod-title{display:block;font:600 18px/1.3 "Inter",system-ui,-apple-system}
.mod-summary{display:block;color:var(--muted);margin-top:6px;font:400 14px/1.6 "Inter",system-ui}
.mod-meta{display:block;color:var(--muted);margin-top:8px;font:500 12px/1 "Inter",system-ui}
.sep{margin:0 6px;opacity:.4}
</style>

<div class="wrap">
  <h1>DevOps/SRE FastTrack</h1>
  <p class="lead">Минимальный интерфейс: поиск + модули. Никаких лишних кнопок, просто начни с нужной темы.</p>

  <div class="search" aria-label="Поиск по модулям">
    <div class="input">
      <svg class="icon" width="20" height="20" viewBox="0 0 24 24" fill="none" aria-hidden="true">
        <path d="M21 21l-4.2-4.2M10.5 18a7.5 7.5 0 1 1 0-15 7.5 7.5 0 0 1 0 15Z" stroke="currentColor" stroke-width="1.6" />
      </svg>
      <input id="q" placeholder="Найти модуль… (нажми /)">
      <span class="kbd">/</span>
    </div>
    <div class="meta">Модулей доступно: <span id="cnt">{{ site.modules | size }}</span></div>
  </div>

  <ul class="modules" id="mods">
    {% assign list = site.modules | sort: "order" %}
    {% for m in list %}
    <li class="mod">
      <a href="{{ m.url | relative_url }}"
         data-title="{{ m.title | escape }}"
         data-summary="{{ m.summary | default: 'В разработке' | escape }}"
         data-tags="{{ m.tags | join: ' ' | escape }}">
        <span class="mod-title">{{ m.title }}</span>
        <span class="mod-summary">{{ m.summary | default: "В разработке" }}</span>
        <span class="mod-meta">
          {{ m.track | default: "Core" }} <span class="sep">•</span> {{ m.time | default: "90–120 мин" }}
        </span>
      </a>
    </li>
    {% endfor %}
  </ul>
</div>

<script>
(function(){
  const q = document.getElementById('q');
  const cnt = document.getElementById('cnt');
  const items = Array.from(document.querySelectorAll('#mods .mod a'));

  function apply(){
    const s = q.value.toLowerCase().trim();
    let visible = 0;
    items.forEach(a=>{
      const hay = (a.dataset.title + ' ' + a.dataset.summary + ' ' + a.dataset.tags).toLowerCase();
      const ok = !s || hay.includes(s);
      a.parentElement.style.display = ok ? '' : 'none';
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
