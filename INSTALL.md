# Установка и обновление AWN Framework

Инструкция для **агента**: как скопировать базовые файлы AWN в корень проекта пользователя и при необходимости добавить стартовый md под конкретную IDE/CLI.

Человеку: попросите агента выполнить установку, **прикрепив этот файл** или открыв его в workspace, чтобы агент прочитал блок ниже.

Контекст проекта и философия AWN — в корневом [`README.md`](README.md). Полный контракт правил — в [`AGENTS.md`](AGENTS.md).

---

## INSTALL / UPDATE (инструкция для агента)

> [!TIP]
> **Как подключить (установить) фреймворк для своего агента**
>
> Попросите своего агента установить данный фреймворк, передав ему инструкцию, описанную ниже.
>
> Важно: при установке может выполняться перезапись соответствующих файлов, если они уже существуют.

### Инструкция для агента (промт на установку AWN-Framework)

```text
Контекст задачи:
Ты выполняешь установку (обновление) AWN Framework в текущий проект пользователя.
Ожидаемый результат: в корне проекта лежат базовые файлы AWN из шага 1; при необходимости для среды пользователя — стартовый md из шага 2 и `AGENTS.LLM_BOOTSTRAP_PRESET.md` (если стартер на него ссылается). Если среда читает только `AGENTS.md`, стартовый файл может не понадобиться — это нормально.

Общие правила:
1) Если файлы уже существуют, предложи замену и запроси подтверждение перед перезаписью.
2) После завершения установки попроси пользователя перезапустить сессию (или приложение).

Шаг 1. Загрузка базовых файлов

Скачай базовые файлы в корень проекта.

Скачай в корень проекта (для загрузки по HTTP используй **raw**-ссылки GitHub, иначе вместо файла придёт HTML страницы; шаблон: `https://raw.githubusercontent.com/iv-litovchenko/AWN-Framework/main/<путь-к-файлу-в-репо>`):

- https://github.com/iv-litovchenko/AWN-Framework/AGENTS.md в AGENTS.md
- https://github.com/iv-litovchenko/AWN-Framework/AGENTS.NODES.md в AGENTS.NODES.md
- https://github.com/iv-litovchenko/AWN-Framework/AGENTS.NODES.CATALOG.md в AGENTS.NODES.CATALOG.md
- https://github.com/iv-litovchenko/AWN-Framework/AGENTS.SETTINGS.md в AGENTS.SETTINGS.md
- https://github.com/iv-litovchenko/AWN-Framework/AGENTS.LLM_BOOTSTRAP_PRESET.md в AGENTS.LLM_BOOTSTRAP_PRESET.md
- https://github.com/iv-litovchenko/AWN-Framework/HEARTBEAT.md в HEARTBEAT.md
  
Если нет структуры под ноды ассистента — создай `Assistant.Ai/Nodes/` (или скопируй дерево `Assistant.Ai/` из репозитория).

- https://github.com/iv-litovchenko/AWN-Framework/Assistant.Ai/Nodes/RandomAnecdote.node.md в Assistant.Ai/Nodes/RandomAnecdote.node.md

- https://github.com/iv-litovchenko/AWN-Framework/Assistant.Ai/Nodes/MetadataFiles.node.md в Assistant.Ai/Nodes/MetadataFiles.node.md

Шаг 2. Стартовый md-файл для твоей IDE/CLI (не путать с AGENTS.md)

`AGENTS.md` — это **единый контракт правил и протокола AWN для агента** (полная/чистая сессия, ноды, реестр). Имя **фиксировано**: всегда `AGENTS.md` в корне проекта.

Отдельно нужен **стартовый файл под конкретную систему** — короткий указатель, который клиент подмешивает в контекст. Имя файла **зависит от продукта**; это **не** замена `AGENTS.md`. Типичные имена:

| Система / контекст | Имя стартового файла в корне проекта |
|--------------------|--------------------------------------|
| Claude Code, Cursor (правила под Claude) и т.п. | `CLAUDE.md` |
| Google Gemini CLI | `GEMINI.md` |
| Qwen / совместимые оболочки | `QWEN.md` |
| OpenAI Codex CLI | `CODEX.md` |
| DeepSeek | `DEEPSEEK.md` |
| Mistral | `MISTRAL.md` |

Готовые стартеры из AWN обычно ссылаются на `AGENTS.LLM_BOOTSTRAP_PRESET.md` (полная/чистая сессия, чтение `AGENTS.md` и `AGENTS.NODES.md`). Если копируешь такой стартер — **`AGENTS.LLM_BOOTSTRAP_PRESET.md` должен лежать в корне** (его добавили в шаге 1).

Уточни у пользователя или по документации среды, **какое имя файла** ожидается в корне workspace, и скачай **один** подходящий файл под это имя:

- https://github.com/iv-litovchenko/AWN-Framework/CLAUDE.md → `CLAUDE.md`
- https://github.com/iv-litovchenko/AWN-Framework/CODEX.md → `CODEX.md`
- https://github.com/iv-litovchenko/AWN-Framework/DEEPSEEK.md → `DEEPSEEK.md`
- https://github.com/iv-litovchenko/AWN-Framework/GEMINI.md → `GEMINI.md`
- https://github.com/iv-litovchenko/AWN-Framework/MISTRAL.md → `MISTRAL.md`
- https://github.com/iv-litovchenko/AWN-Framework/QWEN.md → `QWEN.md`
- https://github.com/iv-litovchenko/AWN-Framework/README.fix.md → `README.md`

Для OpenClaw-подобных систем, которые читают `AGENTS.md` **напрямую**, копирование `CLAUDE.md` / `GEMINI.md` и т.д. можно пропустить — пользователь должен убедиться, что среда подхватывает `AGENTS.md`.

Если готового стартера нет, создай файл с именем, которое требует среда, по шаблону https://github.com/iv-litovchenko/AWN-Framework/AGENTS.LLM_TEMPLATE_PRESET.md — содержимое должно вести к `./AGENTS.LLM_BOOTSTRAP_PRESET.md` или к тем же правилам чтения `./AGENTS.md`.

Шаг 3. Проверка и перезапуск

1) В корне есть `AGENTS.md` и `AGENTS.NODES.md`.  
2) Если использовал шаг 2 — стартовый файл **под ожидаемым именем** и при необходимости `AGENTS.LLM_BOOTSTRAP_PRESET.md`.  
3) Попроси пользователя перезапустить сессию или приложение.  
4) По желанию: в project rules среды — короткая отсылка к `AGENTS.md` или пресету, без длинного дублирования текста контракта.
5) Также обрати внимание пользователя на то, что в систему загружены 2 ноды в качестве примера:

- случайный анекдот с сохранением в память и
- описание медиафайлов в качестве эксперимента.
```
