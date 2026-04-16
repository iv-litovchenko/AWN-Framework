---
TYPE: SettingsRegistry
TITLE: Agent Settings Registry
DESCRIPTION: "Реестр системных настроек, влияющих на поведение агента."
VERSION: 2
STATUS: active
CREATED: 2026-04-16
UPDATED: 2026-04-16
---

Этот файл — реестр системных настроек агента.

Он нужен для настроек, которые влияют не на отдельную ноду, а на общее поведение агента:

- как писать ссылки;
- как называть новые файлы и папки;
- какие общие правила считать включёнными по умолчанию.

## Принцип

- `AGENTS.md` — базовый протокол среды.
- `AGENTS.NODES.md` — реестр нод.
- `AGENTS.SETTINGS-v2.md` — реестр системных настроек.

Настройки из этого файла применяются только как общий слой поведения. Они не заменяют прямую инструкцию пользователя в текущем запросе.

## Приоритет применения

1. Явная инструкция пользователя в текущем запросе.
2. Активная настройка из `AGENTS.SETTINGS-v2.md`.
3. Поведение по умолчанию из `AGENTS.md`.

## Контракт одной настройки

Каждая настройка должна иметь:

- `KEY` — уникальный системный идентификатор.
- `TITLE` — короткое человекочитаемое имя.
- `TYPE` — тип значения: `boolean`, `string`, `enum`, `number`.
- `VALUE` — текущее значение.
- `DEFAULT` — значение по умолчанию.
- `STATUS` — `draft`, `active`, `archive`.
- `SCOPE` — где влияет настройка: `global`, `creation`, `rendering`, `naming`, `output`.
- `DESCRIPTION` — что делает настройка и зачем нужна.
- `UPDATED` — дата последнего изменения.

## Реестр настроек

```yaml
SETTINGS:
  - KEY: links.markdown_compatible
    TITLE: "GitHub-совместимый Markdown для ссылок и превью"
    TYPE: boolean
    VALUE: true
    DEFAULT: true
    STATUS: active
    SCOPE: rendering
    DESCRIPTION: "Использовать стандартный Markdown для ссылок, изображений и якорей вместо wiki-синтаксиса."
    UPDATED: 2026-04-16

  - KEY: naming.camel_case
    TITLE: "CamelCase для новых файлов и папок"
    TYPE: boolean
    VALUE: true
    DEFAULT: true
    STATUS: active
    SCOPE: naming
    DESCRIPTION: "При создании новых файлов и папок использовать CamelCase, если пользователь не попросил иначе."
    UPDATED: 2026-04-16
```

## CRUD-протокол для настроек

### Создать настройку

1. Добавить новую запись в `SETTINGS`.
2. Задать уникальный `KEY`.
3. Заполнить все обязательные поля.
4. Установить `STATUS: active` или `STATUS: draft`.

### Изменить настройку

1. Менять `VALUE` и при необходимости `DESCRIPTION`.
2. Обновлять `UPDATED`.
3. Не переименовывать `KEY` без крайней необходимости.

### Архивировать настройку

1. Не удалять запись физически без особой причины.
2. Установить `STATUS: archive`.
3. При необходимости оставить пояснение в `DESCRIPTION`.

## Минимальная валидация

Перед принятием настройки в работу стоит проверять:

- уникален ли `KEY`;
- заполнены ли обязательные поля;
- допустим ли `TYPE`;
- допустим ли `STATUS`;
- есть ли `UPDATED`;
- не конфликтует ли настройка с уже существующими.

## Примечание

Этот файл лучше подходит для системных флагов поведения агента.

Если правило относится к конкретной предметной области, проекту, папке или сценарию, его лучше хранить в `*.node.md`, а не в реестре настроек.

## Варианты оформления реестра (для выбора)

Ниже 5 альтернатив, как можно оформлять настройки. Смысл один и тот же, меняется только форма представления.

### Вариант 1 — Таблица

md
## Настройки (таблично)

| KEY | Вкл | Тип | Значение | Область | Описание |
|---|---|---|---|---|---|
| links.markdown_compatible | ✅ | boolean | true | rendering | Использовать markdown-ссылки вместо wiki |
| naming.camel_case | ✅ | boolean | true | naming | Новые файлы/папки в CamelCase |

### Вариант 2 — Чеклист-карточки


## Настройки (карточки)

### links.markdown_compatible
- [x] Включено
- Тип: `boolean`
- Значение: `true`
- Область: `rendering`
- Описание: стандартный Markdown для ссылок и превью.

### naming.camel_case
- [x] Включено
- Тип: `boolean`
- Значение: `true`
- Область: `naming`
- Описание: новые файлы/папки в CamelCase.

### Вариант 3 — INI-стиль


## Настройки (INI-стиль)

[links]
markdown_compatible = true
; markdown-ссылки вместо wiki

[naming]
camel_case = true
; новые файлы/папки в CamelCase

### Вариант 4 — Чистый YAML-блок


## Настройки (YAML)

```yaml
settings:
  links:
    markdown_compatible: true
  naming:
    camel_case: true
```

### Вариант 5 — Гибрид (человек + машина)


## Быстрый статус

- links.markdown_compatible: ✅
- naming.camel_case: ✅

## Канонический блок (machine-readable)

```yaml
SETTINGS:
  - KEY: links.markdown_compatible
    TYPE: boolean
    VALUE: true
    STATUS: active

  - KEY: naming.camel_case
    TYPE: boolean
    VALUE: true
    STATUS: active
```
````
