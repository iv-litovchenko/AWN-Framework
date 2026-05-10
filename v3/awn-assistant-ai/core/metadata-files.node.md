---
AWN-TYPE: NODE/SOLO
AWN-TITLE: MetadataFiles — контракт *.metadata.md
AWN-DESC: "Контракт файлов *.metadata.md: что это, правило имени, поля шапки, примеры."
AWN-LOAD: on_demand
AWN-PRIORITY: 20
AWN-TRIGGERS:
  - metadata.md
  - sidecar
  - метаданные медиа
  - описание файла
  - бинарник
AWN-STATUS: active
AWN-MEMORY: none
AWN-AUTOMATIZATION: false
AWN-CRON: 0 9 * * *
AWN-CATEGORY: system
AWN-VERSION: 1.1.2
AWN-CREATED: 2026-05-05
AWN-UPDATED: 2026-05-07
---

# Sidecar-файлы (`*.metadata.md`)

> [!info] О файле
> Правила для файлов `*.metadata.md`. Сами sidecar-файлы по одному при старте **не** подгружаются — только когда работаешь с конкретным бинарником.

Текстовое описание бинарного файла (картинка, аудио, PDF) — чтобы агент понимал его смысл без открытия. Имя: `{полное_имя_файла}.metadata.md` в той же папке. Агент читает его вместо «немого» бинарника.
## Когда создавать

Новый `*.metadata.md` заводится **только по явному запросу пользователя** (описать бинарник, сделать sidecar, метаданные к файлу и т.п.). Без такого запроса не создавать проактивно.

## Правило имени (канон)

Имя = **полное имя носителя** + `.metadata.md`, в **той же папке** что и носитель.

| Носитель | Sidecar |
|----------|---------|
| `Assets/photo.png` | `Assets/photo.png.metadata.md` |
| `Assets/2026-05-05-lecture.mp3` | `Assets/2026-05-05-lecture.mp3.metadata.md` |
