# Оглавление

1. [01 Описание спецификации AWN V5](#1-01-описание-спецификации-awn-v5)
   1.1. [Принципы содержимого](#11-принципы-содержимого)
   1.2. [О нодах и терминология](#12-о-нодах-и-терминология)
2. [02 Awn-файлы в корне workspace](#2-02-awn-файлы-в-корне-workspace)
   2.1. [Combined.documentation](#21-combineddocumentation)
   2.2. [Configuration.documentation](#22-configurationdocumentation)
   2.3. [Documentation.documentation](#23-documentationdocumentation)
3. [03 Структура папки-ноды](#3-03-структура-папки-ноды)
   3.1. [Workspace](#31-workspace)
   3.2. [Space](#32-space)
   3.3. [Cluster](#33-cluster)
   3.4. [Book](#34-book)
   3.5. [Collection](#35-collection)
   3.6. [Intro или Repo](#36-intro-или-repo)
   3.7. [Part](#37-part)
   3.8. [Vision](#38-vision)
4. [04 Типы памяти](#4-04-типы-памяти)
   4.1. [Inner — внутренняя память ноды](#41-inner--внутренняя-память-ноды)
   4.2. [Outer — внешняя память ноды](#42-outer--внешняя-память-ноды)
   4.3. [Log — журнал ноды](#43-log--журнал-ноды)
   4.4. [Sidecar — метаописание не-md файла](#44-sidecar--метаописание-не-md-файла)
   4.5. [Volume — приватная память ноды](#45-volume--приватная-память-ноды)
5. [05 Команды](#5-05-команды)
6. [06 Шаблоны](#6-06-шаблоны)

---

## 1. 01 Описание спецификации AWN V5

*Источник: [.awn-framework.project/00 Index.documentation.md](.awn-framework.project/00 Index.documentation.md) (строки 1-73)*

Ты работаешь в хранилище Obsidian. Баланс в том что и как видит человек и тем что и как видит видит ИИ (2 взаимопроникающих слоя)

> **Роль этого файла:** здесь описаны, принципы, команды, прозрачность. 

## Где мы работаем

Vault Obsidian — workspace агента. Не выходить за его пределы без явного разрешения пользователя.

## Метафора: клетки, узлы, синергия

Нода — как клетка организма: самодостаточный атом знания с понятной ролью. Цифровая экосистема строится из таких узлов — агент помнит и фиксирует происходящее в нужном файле, правит релевантные заметки, ориентируется где что лежит.

**Жёстких деревьев каталогов нет** — допустимы любые папки и файлы в vault. Важны не шаблоны папок, а договорённости и явные ноды.

Взаимодействие человека и ассистента — **синергия 1+1**: ясность агенту, опора и рост пользователю, без превращения памяти в кучу разрозненных дублей.

### 1.1. Принципы содержимого

Ориентиры для нод и заметок — не законы, но помогают не превратить vault в свалку.

#### Главные правила

**1. Не дублируй внутри одного файла.**

Одна мысль — один раз. Не повторяй одно и то же разными словами в разных местах одной ноды.

**2. Не дублируй между файлами — давай ссылку.**

Если факт уже есть в другой ноде — сошлись на неё, не копируй текст. Два одинаковых куска в разных файлах расходятся со временем и создают противоречия.

**3. Не вводи иерархию папок (областей/спейсов) там, где её нет в реальности или она избыточна.**

Папка оправдана, если внутри несколько связанных файлов с общим контекстом. Одиночная нода не требует своей папки — она живёт там, где логично.

**4. Принцип безопасной маршрутизации.**

Если не удаётся однозначно определить область/домен/папку для скрипта, текста, коллекции или документа (фото) — задавай уточняющий вопрос пользователю до создания/перемещения. Запрещено "угадывать" целевую папку при неоднозначности. "Неоднозначность" = есть 2+ равновероятных места, нет явных ключей в имени/контенте, или правило маршрутизации конфликтует.

#### Таблица принципов

| Принцип            | Суть                                                                                                                    |
| ------------------ | ----------------------------------------------------------------------------------------------------------------------- |
| **DRY**            | Один факт — один раз. Не дублировать текст между файлами — лучше ссылка на источник                                     |
| **DDD**            | Domain-Driven Design — домен и язык. Каждая область vault говорит на своём языке, ноды отражают реальные понятия домена |
| **KISS**           | Нода должна быть понятна с первого прочтения                                                                            |
| **YAGNI**          | Не создавать ноду «на будущее» — только когда реально нужна                                                             |
| **SRP** (из SOLID) | Одна нода — одна договорённость. Смешивать несвязанные темы в одном файле — плохо                                       |
| **APO**            | Atomicity / One Purpose — атом знания с понятной ролью                                                                  |
| **BDUF**           | Не строить вечную спецификацию заранее — держать договор в нодах, обновлять по мере роста                               |
| **Occam's Razor**  | Проще — вероятнее. Не плодить ноды и поля без реальной нужды                                                            |

### 1.2. О нодах и терминология

**AWN v3** — протокол человек ↔ агент в общем Vault.

- **Scope:** один Obsidian Vault.
- **Boundary:** агент не выходит за Vault без разрешения.
- **Модель:** Vault = OS для агента. Файловая структура = машинный API.

#### Нода (Node)

Базовая единица. `*.md`-файл из таблицы типов (§3). Нода — файл с договорённостью: правило, профиль, навык, контекст.

**Инварианты:**

- 1 нода = 1 атомарная идея = 1 место.
- Тип ноды задаёт роль и поведение (§3).
- Поля фронтматтера зависят от типа.
- `.md`-файлы вне таблицы §3 — **не ноды**.

Нода это более менее статичный элемент - это логика. Память это динамически наполняемое редактируемое содержимое.

Суффикс - это часть в названии папки или файла которая подсказыает назначение ее использования (роль).

---

## 2. 02 Awn-файлы в корне workspace

*Источник: [.awn-framework.project/01 Core/00 Index.documentation.md](.awn-framework.project/01 Core/00 Index.documentation.md) (строки 1-19)*

Системные файлы фреймворка AWN, живущие в корне workspace. Имеют общий префикс `awn.` — это отделяет их от пользовательского контента и `AGENTS.md`.

Все awn-файлы создаются и обновляются агентом по командам пользователя.

### Реестр awn-файлов

| Файл                            | Назначение                                                                                                                     |
| ------------------------------- | ------------------------------------------------------------------------------------------------------------------------------ |
| `awn.settings.md`               | Базовые настройки workspace: рендеринг ссылок, naming, приветствие, voice. Редактируется человеком.                            |
| `awn.registry.md`               | Реестр `*.node.md` workspace. Таблица маршрутов: запрос → `AWN-TRIGGERS` → подгружаемые ноды. Обновляется по запросу.          |
| `awn.documentation.combined.md` | Скомпилированная документация: оглавление + содержимое всех `*.documentation.md`. Генерируется командой `DocumentationUpdate`. |
| `awn.dependencies.md`           | Системные зависимости (аналог `requirements.txt` для сервера). Заполняется при установке/изменении зависимостей.               |

### Правила

- Файл `awn.*` создаётся **только когда реально нужен** — пустых заглушек не плодим.
- Если файла нет, а команде он понадобился — агент создаёт его при первой необходимости.
- Содержимое генерируется/обновляется агентом; человек правит руками только `awn.settings.md`.

### 2.1. Combined.documentation

*Источник: [.awn-framework.project/02 Components/01 Awn-files/Combined.documentation.md](.awn-framework.project/02 Components/01 Awn-files/Combined.documentation.md) (строки 1-9)*

Файл вида `*.combined.md` — скомпилированный (склеенный) файл, собранный из нескольких источников в один.

Например, документация из всех файлов `*.documentation.md` собирается в один `awn.documentation.combined.md` в корне vault.

Содержимое генерируется автоматически по команде агента — вручную не редактируется.

### 2.2. Configuration.documentation

*Источник: [.awn-framework.project/02 Components/01 Awn-files/Configuration.documentation.md](.awn-framework.project/02 Components/01 Awn-files/Configuration.documentation.md) (строки 1-9)*

Файл вида `*.configuration.md` — файл с конфигурацией для ноды.

- Может лежать рядом с нодой (`<имя>.configuration.md`) или произвольно — путь не фиксирован.
- Когда нода используется, агент подгружает её конфигурацию из соответствующего `*.configuration.md`.
- Содержимое файла может изменяться (в отличие от `*.documentation.md`).

### 2.3. Documentation.documentation

*Источник: [.awn-framework.project/02 Components/01 Awn-files/Documentation.documentation.md](.awn-framework.project/02 Components/01 Awn-files/Documentation.documentation.md) (строки 1-10)*

Файл вида `*.documentation.md` — файл с документацией. YAML-свойства не используются и не собираются — обрабатывается только тело файла.

- Может лежать рядом с нодой (`<имя>.documentation.md`) или произвольно — путь не фиксирован.
- Тело всех `*.documentation.md` собирается в единый файл `./awn.documentation.combined.md` (корень vault) в виде оглавления с параграфами — по команде «обнови документацию».
- Содержимое этих файлов **меняется только человеком** — агент сам по себе их не редактирует.

---

## 3. 03 Структура папки-ноды

*Источник: [.awn-framework.project/02 Components/02 Nodes-types/01 Folders/00 Index.documentation.md](.awn-framework.project/02 Components/02 Nodes-types/01 Folders/00 Index.documentation.md) (строки 1-42)*

Унифицированный словарь подпапок, которые могут жить внутри любой ноды-папки.

Подпапки создаются **по мере необходимости** — если их нет, ничего не ломается: агент работает с теми, которые есть.

### Подпапки

| Путь                  | Назначение                                                                                                                   |
| --------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| `_Assets/`            | Вложения к записям ноды (изображения, PDF, медиа). По умолчанию раскладываются по подпапкам текущей даты `YYYY-MM-DD/`.      |
| `_Children/`          | Дочерние ноды-папки (Space, Cluster, Book, Collection внутри родительской ноды). Не для файлов-нод — для тех есть `Parts/`.  |
| `_Parts/`             | Ноды-части. Используется, когда сложная нода разбита на несколько `*.node.md`. Часть нод можно располагать и вне этой папки. |
| `_Scripts/`           | Скрипты ноды: bash, python и др.                                                                                             |
| `_Inbox/`             | Входящий поток — сырые заметки `*.note.md` ещё не разобранные по полкам. Здесь беспорядок разрешён.                          |
| `_Content/`           | Внешняя память ноды: переработанные знания, заметки, логи обсуждений, выводы.                                                |
| `_Content/Artifacts/` | Выходные данные агента: саммари, аналитика, спарсенные данные.                                                               |
| `_Content/Trash/`     | Корзина для удалённого контента.                                                                                             |
| `_References/`        | Внешние знания: переработанные чужие материалы — конспекты, цитаты, PDF из книг и статей.                                    |
| `_Temporary/`         | Черновой стол: временные файлы, скриншоты, эксперименты без постоянного места.                                               |
| `_Logs/`              | Логи.                                                                                                                        |
| `_Templates/`         | Локальные шаблоны ноды (Skeleton, Node, Memory, Sidecar и т.п.).                                                             |
| `_Vision/`            | Представления данных (Views): дашборды, канбаны, mindmap-обзоры, списки.                                                     |

### Специальные файлы

| Файл   | Назначение                                                                                      |
| ------ | ----------------------------------------------------------------------------------------------- |
| `.env` | Переменные окружения для скриптов ноды: локальные ключи, пути. Не коммитить (см. `.gitignore`). |

### Правила

- Любая из перечисленных подпапок **опциональна** — создаётся только когда в ней появляется реальное содержимое.

### 3.1. Workspace

*Источник: [.awn-framework.project/02 Components/02 Nodes-types/01 Folders/01 Workspace.documentation.md](.awn-framework.project/02 Components/02 Nodes-types/01 Folders/01 Workspace.documentation.md) (строки 1-17)*

```
AWN-SCHEMA: Type.schema
AWN-ID: "1f213379-7b1c-4fcb-8e1c-890685a5865f"
AWN-SLUG: COMPONENT/WORKSPACE
AWN-TYPE: Folder
AWN-ALLOW-CHILDREN: true
AWN-LAYER: 0
AWN-NAME: Workspace
AWN-DESC: Корень workspace — описание проекта и точка входа в vault.
AWN-REGISTRY: true
```

# Workspace — корень рабочего пространства

Файл вида `README.node.md` в корне workspace — нода-описание самого пространства. Отвечает на вопросы: что это за проект, зачем он существует, что здесь лежит, как с этим работать.

Workspace — корневой контейнер для всех остальных нод. В одном workspace может быть только **один** такой файл, и лежит он в самом корне.

Если в корне workspace нет `README.node.md` — это ошибка состояния «не понятно, что за проект». Агент при старте предлагает создать корневую ноду.

### 3.2. Space

*Источник: [.awn-framework.project/02 Components/02 Nodes-types/01 Folders/02 Space.documentation.md](.awn-framework.project/02 Components/02 Nodes-types/01 Folders/02 Space.documentation.md) (строки 1-11)*

```
AWN-SCHEMA: Type.schema
AWN-ID: "c5c1f230-21cc-4b7f-8cd9-034d52a2da65"
AWN-SLUG: COMPONENT/SPACE
AWN-TYPE: Folder
AWN-ALLOW-CHILDREN: true
AWN-LAYER: 1
AWN-NAME: Space
AWN-DESC: Самостоятельная область знаний со своими правилами и контекстом.
AWN-REGISTRY: true
```

# Space — самостоятельная область знаний

Файл вида `<name>/Index.node.md` — нода-ориентир папки (область). Описывает: зачем папка существует, что в ней лежит, какие правила здесь действуют.

### 3.3. Cluster

*Источник: [.awn-framework.project/02 Components/02 Nodes-types/01 Folders/03 Cluster.documentation.md](.awn-framework.project/02 Components/02 Nodes-types/01 Folders/03 Cluster.documentation.md) (строки 1-10)*

```
AWN-SCHEMA: Type.schema
AWN-ID: "10e9bbb6-458e-4b3f-923c-3588614f3999"
AWN-SLUG: COMPONENT/CLUSTER
AWN-TYPE: Folder
AWN-ALLOW-CHILDREN: true
AWN-LAYER: 1
AWN-NAME: Cluster
AWN-DESC: Папка-группировка однотипных нод.
AWN-REGISTRY: true
```

# Cluster — группировка однотипных нод

Файл вида `<name>/Index.node.md` — нода-папка для группировки однотипных нод.

### 3.4. Book

*Источник: [.awn-framework.project/02 Components/02 Nodes-types/01 Folders/04 Book.documentation.md](.awn-framework.project/02 Components/02 Nodes-types/01 Folders/04 Book.documentation.md) (строки 1-10)*

```
AWN-SCHEMA: Type.schema
AWN-ID: "b8391a75-129c-440c-99ef-51c0198d27d6"
AWN-SLUG: COMPONENT/BOOK
AWN-TYPE: Folder
AWN-ALLOW-CHILDREN: true
AWN-LAYER: 1
AWN-NAME: Book
AWN-DESC: База знаний по одной теме — набор связанных заметок.
AWN-REGISTRY: true
```

# Book — база знаний по одной теме

Файл вида `<name>/Index.node.md` — нода-книга: набор связанных заметок по одной теме. Описывает, как с этой книгой работать и как добавлять в неё новые записи. Подходит для базы знаний по определённой тематике.

### 3.5. Collection

*Источник: [.awn-framework.project/02 Components/02 Nodes-types/01 Folders/05 Collection.documentation.md](.awn-framework.project/02 Components/02 Nodes-types/01 Folders/05 Collection.documentation.md) (строки 1-13)*

```
AWN-SCHEMA: Type.schema
AWN-ID: "b619c6ef-53ed-4fc7-837e-78a73033f9b7"
AWN-SLUG: COMPONENT/COLLECTION
AWN-TYPE: Folder
AWN-ALLOW-CHILDREN: true
AWN-LAYER: 1
AWN-NAME: Collection
AWN-DESC: База данных однотипных записей — аналог таблицы в папке.
AWN-REGISTRY: true
```

# Collection — база данных однотипных записей

Файл вида `<name>/Index.node.md` — нода-коллекция однотипных данных. Описывает, как с этой коллекцией работать и как добавлять записи. Аналог базы данных в папке. Подходит для однотипных данных: задачи, дневник, история финансов, логи и т.п.

### 3.6. Intro или Repo

*Источник: [.awn-framework.project/02 Components/02 Nodes-types/01 Folders/zzz 06 Intro ИЛИ REPO.documentation.md](.awn-framework.project/02 Components/02 Nodes-types/01 Folders/zzz 06 Intro ИЛИ REPO.documentation.md) (строки 1-3)*

```
AWN-CORE-TYPE: Folder
AWN-CORE-CHILDREN-ALLOW: "0"
AWN-CORE-ROLE: COMPONENT/REPO
```

Нода-справочник (репозиторий или интро). Просто справочная информация о папке, о том, что здесь находится. Составляется оглавление того, что есть в папке.

Внутрь этой папки система автоматически ничего не создаёт и вглубь не идёт. Папка конечна в контексте генерации структуры ИИ.

### 3.7. Part

*Источник: [.awn-framework.project/02 Components/02 Nodes-types/02 Files/01 Part.documentation.md](.awn-framework.project/02 Components/02 Nodes-types/02 Files/01 Part.documentation.md) (строки 1-17)*

```
AWN-SCHEMA: Type.schema
AWN-ID: "de53cb60-3245-4d67-a939-0b006084d051"
AWN-SLUG: COMPONENT/PART
AWN-TYPE: File
AWN-ALLOW-CHILDREN: false
AWN-LAYER: 2
AWN-NAME: Part
AWN-DESC: Атомарная нода-часть с одной задачей или правилом.
AWN-REGISTRY: true
```

# Part — атомарная нода-часть

Файл вида `*.node.md` — нода-часть. Содержит определённую логику или правило и выполняет одну конкретную задачу.

Может располагаться:

- в папке области напрямую (внутри Workspace, Space, Cluster, Book, Collection);
- в подпапке `parts/` родительской ноды — когда сложная нода разбита на несколько `*.node.md` частей.

### 3.8. Vision

*Источник: [.awn-framework.project/02 Components/02 Nodes-types/02 Files/zzz 02 Vision.documentation.md](.awn-framework.project/02 Components/02 Nodes-types/02 Files/zzz 02 Vision.documentation.md) (строки 1-1)*

// Todo - виды и представления данных ноды

---

## 4. 04 Типы памяти

*Источник: [раздел 04 в AWN-фреймворке](.awn-framework.project/02 Components/03 Memories-types)*

Команды — это то, что **запрашивает пользователь**, и **подсказки агенту**, как с этим правильно работать.

Каждая команда — отдельный `*.documentation.md` файл в этой папке с пошаговым протоколом выполнения. Агент при получении соответствующего запроса смотрит протокол и действует по нему.

### 4.1. Inner — внутренняя память ноды

*Источник: [.awn-framework.project/02 Components/03 Memories-types/Content/Inner.documentation.md](.awn-framework.project/02 Components/03 Memories-types/Content/Inner.documentation.md) (строки 1-12)*

```
AWN-SCHEMA: Type.schema
AWN-ID: "99c80278-1c96-4f31-8aac-31a8b4ff13f8"
AWN-SLUG: MEMORY/CONTENT/INNER
AWN-TYPE: File
AWN-ALLOW-CHILDREN: false
AWN-LAYER: 3
AWN-NAME: Inner
AWN-DESC: Внутренняя память ноды в файле-спутнике <name>.node.content.md.
AWN-REGISTRY: false
```

# Inner — внутренняя память ноды

Внутренняя память ноды пишется в файл вида `<name>.node.content.md` — файл-спутник, лежащий рядом с самой нодой `<name>.node.md`.

YAML-свойства (схемы) не используются — это просто текстовый поток памяти.

### 4.2. Outer — внешняя память ноды

*Источник: [.awn-framework.project/02 Components/03 Memories-types/Content/Outer.documentation.md](.awn-framework.project/02 Components/03 Memories-types/Content/Outer.documentation.md) (строки 1-10)*

```
AWN-SCHEMA: Type.schema
AWN-ID: 639a6c6d-75cc-478f-8f24-69ac708b45c7
AWN-SLUG: MEMORY/CONTENT/OUTER
AWN-TYPE: File
AWN-ALLOW-CHILDREN: false
AWN-LAYER: 3
AWN-NAME: Outer
AWN-DESC: Внешняя память ноды — записи в папке Content/.
AWN-REGISTRY: false
```

# Outer — внешняя память ноды

Внешняя память ноды складывается в папку `Content/`.

Базовый шаблон (схема) такой памяти имеет свой набор собственных полей.

### 4.3. Log — журнал ноды

*Источник: [.awn-framework.project/02 Components/03 Memories-types/Log.documentation.md](.awn-framework.project/02 Components/03 Memories-types/Log.documentation.md) (строки 1-11)*

```
AWN-SCHEMA: Type.schema
AWN-ID: "9f7526d3-1ddb-4d75-8128-09d30e139c21"
AWN-SLUG: MEMORY/LOG
AWN-TYPE: File
AWN-ALLOW-CHILDREN: false
AWN-LAYER: 3
AWN-NAME: Log
AWN-DESC: Журнал событий и истории работы с нодой.
AWN-REGISTRY: false
```

# Log — журнал ноды

Файл вида `*.log.md` — журнальная запись событий, действий или истории работы с нодой.

Обычно лежит в подпапке `Logs/` родительской ноды.

YAML-свойства не используются — это поток событий в свободной форме (дата + событие).

### 4.4. Sidecar — метаописание не-md файла

*Источник: [.awn-framework.project/02 Components/03 Memories-types/Sidecar.documentation.md](.awn-framework.project/02 Components/03 Memories-types/Sidecar.documentation.md) (строки 1-14)*

```
AWN-SCHEMA: Type.schema
AWN-ID: "a1070b7f-cb36-40ba-a56d-d3ee19d3236e"
AWN-SLUG: MEMORY/SIDECAR
AWN-TYPE: File
AWN-ALLOW-CHILDREN: false
AWN-LAYER: 3
AWN-NAME: Sidecar
AWN-DESC: Метаописание не-md файла (изображения, документа, медиа).
AWN-REGISTRY: false
```

# Sidecar — метаописание не-md файла

Файл вида `<filename.ext>.sidecar.md` — метаописание (sidecar) для бинарного файла: изображения, документа, аудио, видео и т.п.

Обычно лежит рядом с описываемым файлом, чаще всего в папке `Assets/`.

Sidecar именуется по **полному имени родителя**:
- `photo.jpg` → `photo.jpg.sidecar.md`
- `lecture.mp4` → `lecture.mp4.sidecar.md`

Создаётся по запросу.

### 4.5. Volume — приватная память ноды

*Источник: [.awn-framework.project/02 Components/03 Memories-types/Volume.documentation.md](.awn-framework.project/02 Components/03 Memories-types/Volume.documentation.md) (строки 1-15)*

```
AWN-SCHEMA: Type.schema
AWN-ID: "a817a592-da6b-4827-8435-3784bc87c3f9"
AWN-SLUG: MEMORY/VOLUME
AWN-TYPE: File
AWN-ALLOW-CHILDREN: false
AWN-LAYER: 3
AWN-NAME: Volume
AWN-DESC: Приватная память агента по ноде, рабочий конспект.
AWN-REGISTRY: false
```

# Volume — приватная память ноды

Файл вида `<name>.node.volume.md` — приватная память агента по конкретной ноде. Создаётся рядом с нодой как файл-спутник.

Назначение: история взаимодействия агента с нодой — что обсуждалось, как агент рассуждал, какие были промежуточные выводы. Аналог Docker volumes для агента.

**Не является источником правды и договорённостей** — это рабочий конспект, который агент использует для контекста.

YAML-свойства не используются.

Volume применим только к нодам-папкам и нодам-частям (Part):
- `<name>.node.volume.md` — для Part-ноды.
- `Index.node.volume.md` — для папки-ноды (Workspace, Space, Cluster…).

---

## 5. 05 Команды

*Источник: [.awn-framework.project/02 Components/04 Commands-types/00 Index.documentation.md](.awn-framework.project/02 Components/04 Commands-types/00 Index.documentation.md) (строки 1-28)*

Команды — это то, что **запрашивает пользователь**, и **подсказки агенту**, как с этим правильно работать.

Каждая команда — отдельный `*.documentation.md` файл в этой папке с пошаговым протоколом выполнения. Агент при получении соответствующего запроса смотрит протокол и действует по нему.

### Реестр команд

| Файл                                  | Команда (триггер пользователя) | Что делает                                                                |
| ------------------------------------- | ------------------------------ | ------------------------------------------------------------------------- |
| `01 CRUD Node.documentation.md`       | «создай ноду», «удали ноду»    | Создание, чтение, изменение и удаление нод `*.node.md`.                   |
| `02 CRUD Memory.documentation.md`     | «запомни», «забудь», «измени»  | CRUD-операции с памятью нод.                                              |
| `02.02 CRUD Properties.md`            | «измени свойства»              | CRUD над свойствами (YAML-полями) ноды. *(заглушка)*                      |
| `DocumentationUpdate.documentation.md`| «обнови документацию»          | Сборка всех `*.documentation.md` в `awn.documentation.combined.md`.       |
| `RegistryUpdate.documentation.md`     | «обнови реестр»                | Синхронизация `awn.registry.md` со всеми существующими `*.node.md`.       |

### Как добавить новую команду

1. Создать файл `<NN> <Имя команды>.documentation.md` в этой папке.
2. В теле описать:
   - **Триггер**: какие фразы пользователя её вызывают.
   - **Протокол**: пронумерованные шаги, что делает агент.
   - **Результат**: что меняется в vault.
3. Добавить строку в реестр выше.

---

## 6. 06 Шаблоны

*Источник: [.awn-framework.project/04 Templates/00 Index.documentation.md](.awn-framework.project/04 Templates/00 Index.documentation.md) (строки 1-24)*

Это порядок заполнения YAML-свойств и работы с ними. Схема описывает роль данного элемента в системе.

Канонические поля используют префикс `AWN-` — это отделяет системный контракт от пользовательских полей. Пользовательские поля (теги, заметки, метаданные проекта) пишутся без `AWN-`.

**Порядок ключей:** сначала все `AWN-*` поля, затем пользовательские. Состав полей может отличаться в зависимости от типа ноды.

### Контракт фронтматтера, формат шапки

В начале каждого файла-ноды и памяти ноды — блок YAML между `---`.

#### Обязательные поля (все ноды)

#### Что без фронтматтера

- **External** — произвольные файлы, не ноды.
- **`SKILL.md`** и прочие артефакты скилла — по правилам скилла, не по этому контракту, если иное не зафиксировано отдельно.

---

*Документация сгенерирована: 2026-05-18*