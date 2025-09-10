---
layout: page
title: "📘 DevOps/SRE FastTrack — главная"
---

<!-- ===== HERO ===== -->
<style>
:root{
  --card-br:14px; --pill-br:999px; --shadow1:0 2px 8px rgba(0,0,0,.06); --shadow2:0 6px 16px rgba(0,0,0,.12);
}
.hero{
  background: linear-gradient(135deg,#1f5ea5 0%,#2d8f7e 56%,#35a96a 100%);
  border-radius: 18px; color:#fff; padding:28px 22px; margin:-8px 0 18px 0;
}
.hero h1{margin:0 0 6px 0; font-size:clamp(26px,3.6vw,40px); line-height:1.15}
.hero p{margin:6px 0 14px 0; font-size:16px; opacity:.95}
.search-wrap{display:flex; justify-content:center; margin-top:8px}
#q{
  width:min(820px,100%); height:44px; padding:0 16px 0 40px; border-radius:30px; border:none;
  box-shadow:var(--shadow1); outline:none; color:#222;
}
.search-wrap .icon{position:relative}
.search-wrap .icon:before{
  content:"🔎"; position:absolute; left:12px; top:8px; font-size:20px; opacity:.8
}
.count{margin-top:10px; text-align:center; font-weight:600}
</style>

<div class="hero">
  <h1>📘 DevOps/SRE FastTrack — главная</h1>
  <p>Курс ведёт от основ до уверенного DevOps/SRE Middle. Формат: краткая теория → практикум → самопроверка → чек-лист.</p>
  <div class="search-wrap">
    <div class="icon">
      <input id="q" placeholder="Фильтр по названию/описанию… (пример: Kubernetes, Ansible, CI/CD)">
    </div>
  </div>
  <div class="count">Всего модулей: <span id="cnt">{{ site.modules | size }}</span></div>
</div>

<!-- ===== CARDS ===== -->
<style>
.cards{display:grid; grid-template-columns:repeat(auto-fill,minmax(260px,1fr)); gap:14px; margin:10px 0 20px 0}
.card{
  display:block; text-decoration:none; color:inherit; background:#fff; border:1px solid #e9e9e9;
  border-radius:var(--card-br); padding:16px; box-shadow:var(--shadow1); transition:.15s
}
.card:hover{transform:translateY(-2px); box-shadow:var(--shadow2)}
.card h3{margin:0 0 6px 0}
.card p{margin:0; color:#444}
.pills{display:flex; gap:8px; margin-top:10px; flex-wrap:wrap}
.pill{font-size:12px; padding:2px 8px; border-radius:var(--pill-br); border:1px solid #e7e7e7; background:#f6f6f6}
.pill.core{background:#eef6ff; border-color:#d9ecff; color:#1463b8}
.muted{color:#666; font-size:14px}
.kbd{display:inline-block;border:1px solid #ddd;border-bottom-width:2px;border-radius:6px;padding:1px 6px;background:#fbfbfb}
</style>

<div class="cards" id="cards">
{% assign list = site.modules | sort: "order" %}
{% for m in list %}
  <a class="card" href="{{ m.url | relative_url }}"
     data-title="{{ m.title | escape }}"
     data-summary="{{ m.summary | default: 'В разработке' | escape }}"
     data-tags="{{ m.tags | join: ' ' | escape }}">
    <h3>{{ m.title }}</h3>
    <p class="muted">{{ m.summary | default: "В разработке" }}</p>
    <div class="pills">
      <span class="pill core">{{ m.track | default: "Core" }}</span>
      <span class="pill">{{ m.time | default: "90–120 мин" }}</span>
      {% if m.tags %}
        {% for t in m.tags %}<span class="pill">{{ t }}</span>{% endfor %}
      {% endif %}
    </div>
  </a>
{% endfor %}
</div>

<!-- ===== JS: фильтр + удобства ===== -->
<script>
(function(){
  const q = document.getElementById('q');
  const cnt = document.getElementById('cnt');
  const cards = Array.from(document.querySelectorAll('#cards .card'));

  function apply(){
    const s = q.value.toLowerCase().trim();
    let visible = 0;
    cards.forEach(c=>{
      const hay = (c.dataset.title + ' ' + c.dataset.summary + ' ' + c.dataset.tags).toLowerCase();
      const ok = !s || hay.includes(s);
      c.style.display = ok ? '' : 'none';
      if(ok) visible++;
    });
    cnt.textContent = visible;
  }
  q.addEventListener('input', apply);
  // горячая клавиша "/" — фокус на поиск
  document.addEventListener('keydown', e=>{
    if(e.key === '/' && document.activeElement !== q){
      e.preventDefault(); q.focus();
    }
  });
  apply();
})();
</script>

---

### Как работать с курсом
- Режим: 30–45 мин теория → 60–90 мин практика → 10–15 мин самопроверка.
- Инструменты: терминал (Linux/macOS), `bash`, Python 3.
- Лайфхак: нажми <span class="kbd">/</span> чтобы быстро перейти к поиску.
