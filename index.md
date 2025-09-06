---
layout: page
title: "📘 DevOps/SRE FastTrack — главная"
---

<style>
/* Простая сетка карточек без внешних файлов */
.cards {display:grid;grid-template-columns:repeat(auto-fill,minmax(260px,1fr));gap:14px;margin:18px 0}
.card{display:block;border:1px solid #e6e6e6;border-radius:14px;padding:16px;text-decoration:none;background:#fff;box-shadow:0 2px 8px rgba(0,0,0,.04);transition:.15s}
.card:hover{transform:translateY(-2px);box-shadow:0 6px 16px rgba(0,0,0,.08)}
.card h3{margin:4px 0 6px 0}
.badge{display:inline-block;font-size:12px;padding:2px 8px;border-radius:999px;border:1px solid #e9e9e9;background:#f6f6f6;margin-right:6px}
.kbd{display:inline-block;border:1px solid #ddd;border-bottom-width:2px;border-radius:6px;padding:2px 6px;font-family:ui-monospace, SFMono-Regular, Menlo, Monaco, Consolas, "Liberation Mono", "Courier New", monospace;background:#fbfbfb}
.toc a{margin-right:10px}
</style>

> Добро пожаловать! Это **практический курс**, который ведёт от основ до уверенного уровня **DevOps/SRE Middle**.  
> Формат: теория кратко → практикум → самопроверка → чек-лист навыков. Всё без внешних ссылок.

<div class="toc">
<strong>Быстрые ссылки:</strong>
<a href="#cto-takoe-devops">Что такое DevOps</a> •
<a href="#devops-engineer-role">Роль DevOps инженера</a> •
<a href="#skill-matrix">Матрица навыков Middle</a> •
<a href="#roadmap">Дорожная карта модулей</a> •
<a href="#how-to-study">Как учиться</a> •
<a href="#faq">FAQ и мифы</a>
</div>

---

## <a id="cto-takoe-devops"></a>Что такое DevOps

**DevOps** — это не должность и не набор инструментов. Это **культура и инженерные практики**, которые объединяют разработку (Dev) и эксплуатацию (Ops), чтобы **быстрее и безопаснее** доставлять изменения до пользователей.

Ключевые принципы:
- **Flow (поток):** короткие итерации, маленькие изменения, непрерывная доставка.
- **Feedback (обратная связь):** метрики и логи в реальном времени, быстрый фидбек из продакшена.
- **Learning (обучение):** постмортемы без обвинений, эксперименты, автоматизация ручных операций.

Базовые практики:
- **CI/CD** (continuous integration / delivery/deployment)
- **Инфраструктура как код** (IaC)
- **Контейнеризация и оркестрация** (Docker/Kubernetes)
- **Наблюдаемость** (метрики, логи, трассировки)
- **Надёжность** (SLO/SLI, error budgets, инцидент-менеджмент)
- **Безопасность как часть пайплайна** (shift-left security)

---

## <a id="devops-engineer-role"></a>Кто такой DevOps-инженер и чем он занимается

### Цель роли
Сократить время от идеи до стабильной поставки в продакшен при контролируемых рисках и прогнозируемом качестве.

### Ежедневные задачи
- Проектирование и поддержка CI/CD (GitLab/Jenkins/GitHub Actions).
- Описания инфраструктуры в коде (Ansible/Terraform), ревью изменений.
- Сборка/сканирование образов, управление реестрами (Harbor/Registry).
- Эксплуатация Kubernetes/VM: деплой, авто-масштабирование, сети, секреты.
- Наблюдаемость: Prometheus/Grafana/Alertmanager, EFK/ELK, трассировки.
- Надёжность: SLO, алерты, on-call, постмортемы, runbooks.
- Безопасность: секрет-менеджмент (Vault/Sealed Secrets), политика образов, RBAC.
- Оптимизация стоимости и производительности.
- Автоматизация рутинных операций и написание инструментов (Bash/Python).

### Что **не** есть DevOps
- Не «админ, который всё чинит руками».
- Не «человек-оркестр, который один пишет и поддерживает продукты».
- Не «только Kubernetes» и не «только Jenkins». Инструменты — это средство.

---

## <a id="skill-matrix"></a>Матрица навыков (цель уровня Middle)

**Знания**
- ОС и системное ПО: процессы, память, диски, сети; базовый троблшутинг Linux.
- Сети: TCP/IP, DNS, HTTP, TLS, балансировка L4/L7, NAT, overlay в k8s.
- Контейнеры: образы, слои, cgroups/namespaces, сети/тома, multi-stage build.
- Kubernetes: деплойменты, сервисы, пробы, ингресс, HPA, RBAC, storage, Helm.
- CI/CD: стратегии (blue/green, canary), артефакты, миграции БД, rollback/rollout.
- IaC: Ansible (идемпотентность, роли, инвентори), Terraform (state, модули).
- Observability: Prometheus/Grafana, алертинг по SLO, EFK/ELK, трейсинг.
- Базы и кэши (на уровне эксплуатации): PostgreSQL, Redis; бэкапы/HA/мониторинг.
- MQ и стриминг: Kafka/RabbitMQ (базовая эксплуатация).
- Security: secrets, RBAC, образ-полиции, scanning, минимизация прав.

**Умения**
- Проектировать и поддерживать pipeline до продакшена «под ключ».
- Автоматизировать развертывание окружений (stage/prod) из кода.
- Диагностировать инциденты end-to-end (от алерта до RCA).
- Писать надёжные скрипты (Bash, Python) и небольшие утилиты-боты.
- Документировать через runbooks и готовить постмортемы «без обвинений».

**Артефакты Middle-уровня** (что должен уметь показать):
- Репозиторий с рабочим CI/CD (lint → тесты → сборка → выпуск → деплой).
- Набор Terraform/Ansible для развертывания «микросервиса» в k8s.
- Dashboard со SLO, алертами и playbook’ами на инциденты.

---

## <a id="roadmap"></a>Дорожная карта и модули курса

Ниже — карта модулей. Модули пока пустые (заглушки), но страницы уже открываются — позже мы наполним их теорией и практикой.

<div class="cards">

{% assign list = site.modules | sort: "order" %}
{% for m in list %}
  <a class="card" href="{{ m.url }}">
    <span class="badge">{{ m.track | default: "Core" }}</span>
    <span class="badge">{{ m.time | default: "90–120 мин" }}</span>
    <h3>{{ m.title }}</h3>
    <p>{{ m.summary | default: "В разработке" }}</p>
  </a>
{% endfor %}

</div>

**Рекомендованный путь:**  
Linux → Сети → Bash → Git → Python-для-Ops → Docker → Kubernetes → CI/CD → Ansible → Terraform → Observability → Logging → SRE → Security → Databases/MQ → Cloud.

---

## <a id="how-to-study"></a>Как учиться на максимум

- Режим: 10 дней × 2–3 часа. Каждый день:  
  теория 30–45 мин → практика 60–90 мин → самопроверка 10–15 мин.
- Инструменты: терминал (Linux/macOS), `bash`, Python 3.
- Привычки: **маленькие коммиты**, PR-ревью, «одна задача — один MR», **инфраструктура как код**.
- Мини-проект: собери **pet-service** (API) → заверни в Docker → деплой в k8s → добавь CI/CD и мониторинг.

---

## <a id="faq"></a>FAQ и мифы

**DevOps = Kubernetes?**  
Нет. Kubernetes — один из инструментов. DevOps — про поток ценности, обратную связь и обучение.

**Нужен ли сильный кодинг?**  
Нужен **инженерный подход** и умение автоматизировать. Bash обязателен, Python — очень желателен.

**Что важнее — инструменты или подходы?**  
Подходы. Инструменты меняются, но SLO, идемпотентность, мониторинг и надёжный CI/CD — остаются.

---

> Готов идти дальше? Открывай первый модуль из карты выше.  
> Все правки и идеи — через Issues/PR.
