
## §2. Слои контекста

Архитектурные слои по функции. Не путать с глубиной в дереве (§3). 
### Слой 1. Space. Общий контекст и правила области

- Контейнер. Задаёт границы и правила для всего, что внутри.
- Может содержать вложенные Space (группировка областей).
- Файл: `_index.node.md` внутри `space-*/`.
- Пример: `awn-spaces/space-finance/_index.node.md`.
### Слой 2. Part (части). Самостоятельные объекты

- Атомарные сущности внутри Space.
- Описание, правила, инструкции — стабильное содержимое.
- Файл: `*.node.md`.
- Пример: `user.node.md`, `git-push.node.md`.
### Слой 3. Memory — Память, следы, опыт, факты, воспоминания

Не истина, а сырьё для рефлексии.
Workflow обработки знаний: **inbox → note → page.**

- **Notes** — поток времени: чаты, сырые или оригинальные заметки. `.note.md` (обычно в `inbox/` или `notes/` соответствующей области). 
- **Pages** —  переработанные, устаявшиеся знания над которыми мы работаем . `pages/*.page.md` (аналогия страниц книг).
- **Rows** — структурированные записи (задачи, финансы и т.п.). `databases/<type>/*.row.md`.
- **Sidecars** — описание не-`.md` файлов (медиа, изображения, документы, бинарники). `*.sidecar.md`.
- **Volumes** (`*.node.volume.md`) — это личная память  ноды: НЕ грузится в контекст по умолчанию, а подгружается по запросу, когда агент работает именно с этой нодой.
### Слой 4. View — представления

- Проекции над слоями 1, 2, 3, 5: list, kanban, dashboard, mindmap.
- Не несёт собственного контента — только рендер.
- Файл: `views/<type>/<name>.view.md`.
### Слой 5. External — не-ноды

- Всё вне таблицы §3: оригиналы медиа, обычные `*.md` (Reference), скрипты, конфиги.
- Видны системе как сырьё/приложения, в граф нод не входят.



## §4. Контракт фронтматтера, формат шапки

В начале каждого файла-ноды (§1) — блок YAML между `---`.

### Обязательные поля (все ноды)

| Поле         | Тип | Значение |
| ------------ | --- | -------- |
| `awn-id`     | str | Стабильный идентификатор ноды. Не менять после создания. Формат: ULID или UUID v4/v7. |
| `awn-type`   | str | Тип по §3: `Space`, `Part`, `Note`, `Page`, `Row`, `Sidecar`, `Volume`, `View`. |
| `awn-status` | str | Жизненный цикл: `draft` \| `active` \| `archived` \| `deprecated`. |

### Опциональные (по мере необходимости)

| Поле           | Тип | Назначение |
| -------------- | --- | ---------- |
| `awn-title`    | str | Человекочитаемое имя, если не очевидно из имени файла. |
| `awn-parent`   | str | `awn-id` родительской ноды. |
| `awn-category` | str | Slug категории домена (если вводишь таксономию). |
| `awn-updated`  | str | ISO 8601 дата последнего смыслового обновления. |

### Что без фронтматтера

- **External** — произвольные файлы, не ноды (§3).
- **`SKILL.md`** и прочие артефакты скилла — по правилам скилла, не по этому контракту, если иное не зафиксировано отдельно.

### Пример

```yaml
---
awn-id: "01JCXYZ..."
awn-type: Page
awn-status: active
awn-parent: "01JCPARENT..."
---
```

Канонические поля используют префикс `AWN-` — это отделяет системный контракт от пользовательских полей. Пользовательские поля (теги, заметки, метаданные проекта) пишутся без `AWN-`.

**Порядок ключей:** сначала все `AWN-*` поля, затем пользовательские. Состав полей может отличаться в зависимости от типа ноды.

```yaml
---
AWN-TYPE: "NODE/SOLO"
AWN-TITLE: Короткое имя
AWN-DESC: "Зачем эта нода — 1-2 строки"
AWN-LOAD: start | on_demand
AWN-PRIORITY: 01..100        # меньше = важнее
AWN-TRIGGERS: [слово, другое слово]
AWN-STATUS: active | disabled | draft | archive
AWN-CATEGORY: general          # slug категории; general — по умолчанию; system — системные ноды агента
AWN-MEMORY: none | internal | external | hybrid
AWN-AUTOMATIZATION: false    # true если нода запускается по расписанию
AWN-CRON: "0 9 * * *"        # расписание (только если AWN-AUTOMATIZATION: true)
AWN-VERSION: 1.0.0           # major — крупные изменения, minor — расширения, patch — правки
AWN-CREATED: YYYY-MM-DD
AWN-UPDATED: YYYY-MM-DD
# пользовательские поля — после AWN-блока:
TAGS: [тег1, тег2]
OTHER-KEY: example
---
```


Шаблоны нод обычно лежат в папке `templates/`.



### Скилл как Space (опционально)

```
SKILL.md
mcp.json
package.json
src/index.ts
config/
```

### Пример путей

```
awn-spaces/space-life/_index.node.md
awn-spaces/space-life/space-health/_index.node.md
awn-spaces/space-life/space-health/inbox/
awn-spaces/space-life/space-health/pages/
awn-spaces/space-life/space-health/databases/default/
awn-spaces/space-life/space-health/views/tasks/
awn-spaces/space-work/_index.node.md
awn-spaces/space-work/notes/
```



