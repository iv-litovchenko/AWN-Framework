---
AWN-TYPE: "NODE/SOLO"
AWN-TITLE: MetadataFiles — контракт *.metadata.md
AWN-DESC: "Контракт файлов *.metadata.md: что это, правило имени, поля шапки, примеры."
AWN-LOAD: start
AWN-PRIORITY: 20
AWN-TRIGGERS: [metadata.md, sidecar, метаданные медиа, описание файла, бинарник]
AWN-STATUS: active
AWN-MEMORY: none
AWN-AUTOMATIZATION: false
AWN-CRON: "0 9 * * *"
AWN-CATEGORY: system
AWN-VERSION: 1.1.2
AWN-CREATED: 2026-05-05
AWN-UPDATED: 2026-05-07
---

# Sidecar-файлы (`*.metadata.md`)

> [!info] О файле
> Правила для файлов `*.metadata.md`. Сами sidecar-файлы по одному при старте **не** подгружаются — только когда работаешь с конкретным бинарником.

Текстовое описание бинарного файла (картинка, аудио, PDF) — чтобы агент понимал его смысл без открытия. Имя: `{полное_имя_файла}.metadata.md` в той же папке. Агент читает его вместо «немого» бинарника.

**Чем не является:**
- Не `*.node.md` — нет AWN-контракта, в реестр `AGENTS.NODES.md` не попадает
- Не `*.memory.md` — нет `AWN-OWNER` с путём к ноде и `AWN-TYPE: "RECORD/MEMORY"`
## Когда создавать

Новый `*.metadata.md` заводится **только по явному запросу пользователя** (описать бинарник, сделать sidecar, метаданные к файлу и т.п.). Без такого запроса не создавать проактивно.

## Правило имени (канон)

Имя = **полное имя носителя** + `.metadata.md`, в **той же папке** что и носитель.

| Носитель | Sidecar |
|----------|---------|
| `Assets/photo.png` | `Assets/photo.png.metadata.md` |
| `Assets/2026-05-05-lecture.mp3` | `Assets/2026-05-05-lecture.mp3.metadata.md` |

## Пример с привязкой к ноде

```yaml
---
AWN-TYPE: "RECORD/METADATA"
AWN-OWNER: Assets/2026-05-05-past-simple.mp3
AWN-STATUS: open
AWN-TITLE: Лекция — Past Simple (занятие 3)
AWN-CREATED: 2026-05-05
AWN-UPDATED: 2026-05-05
TAGS: [english, grammar, audio]
mediaKind: audio
summary: "Запись лекции по Past Simple — занятие 3."
relatedNode: Domains/EnglishLearning/Index.node.md
transcript: "00:00 — введение, 05:30 — примеры, 18:00 — упражнения"
---

# Лекция — Past Simple (занятие 3)

> Sidecar (`*.metadata.md`) к файлу `Assets/2026-05-05-past-simple.mp3`.
```
