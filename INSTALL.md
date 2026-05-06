# AWN Framework: установка или обновление (v2)

Этот файл (инструкция для агента) помогает установить или обновить AWN Framework в проекте пользователя без путаницы.

## Для пользователя (кратко)

1. Открой этот файл в workspace и попроси агента выполнить установку.
2. Укажи, можно ли перезаписывать уже существующие файлы.
3. После завершения перезапусти сессию/приложение.

---

## Цель установки

После установки в корне проекта пользователя должны быть:

- базовые файлы AWN (с теми же путями, как в репозитории);
- каркас папок (`Assistant.Ai/`, `Templates/`, и нужные `Domains/`, `Inbox/`, `Tests/`);
- `AGENTS.md` как основной контракт;
- при необходимости стартовый файл под конкретную IDE/CLI (`CLAUDE.md`, `CODEX.md`, и т.д.).

---

## Правила для агента

1. Если файл уже существует, сначала запроси подтверждение на перезапись.
2. Копируй файлы с сохранением относительных путей.
3. Если качаешь отдельные файлы с GitHub, используй только `raw`-ссылки.
4. После завершения попроси пользователя перезапустить сессию/приложение.
5. После завершения предложи пользователю актуализировать реестр доменов и нод под реальный проект

---

## Шаг 1. Скопировать базовый каркас AWN

Источник: репозиторий `iv-litovchenko/AWN-Framework` (ветка `main`).
Прямая ссылка: [https://github.com/iv-litovchenko/AWN-Framework](https://github.com/iv-litovchenko/AWN-Framework)
База для `raw`-файлов: [https://raw.githubusercontent.com/iv-litovchenko/AWN-Framework/main/](https://raw.githubusercontent.com/iv-litovchenko/AWN-Framework/main/)

- `Assistant.Ai/` (cкопировать целиком)
- `Templates/`  (cкопировать целиком)
- `Dashboards/Area.node.md`
- `Domains/Index.node.md`
- `Domains/Categories.node.md`
- `Inbox/Area.node.md`
- `Tests/Area.node.md`
- `AGENTS.md`
- `AGENTS.FULL.md`
- `AGENTS.NODES.md`
- `AGENTS.NODES.CATALOG.md`
- `AGENTS.SETTINGS.md`
- `AGENTS.LLM_BOOTSTRAP_PRESET.md`
- `AGENTS.LLM_TEMPLATE_PRESET.md`
- `HEARTBEAT.md`
- `INSTALL.md`
- `README.md`
- `docker-compose.yml`
- `.env.example`
- `.gitignore` (добавить/смёржить правила AWN, не перезаписывать вслепую)

---

## Шаг 2. Добавить стартовый файл для среды (если нужен)

`AGENTS.md` всегда обязателен и всегда называется именно `AGENTS.md`.

Отдельно некоторые среды ожидают свой стартовый файл в корне:

- `CLAUDE.md` (Claude Code, Cursor с правилами под Claude)
- `GEMINI.md`
- `QWEN.md`
- `CODEX.md`
- `DEEPSEEK.md`
- `MISTRAL.md`

Действия:

1. Уточни, какой файл ожидает среда пользователя.
2. Скопируй ровно один соответствующий стартер из `raw`-источника:
   - `CLAUDE.md` → `https://raw.githubusercontent.com/iv-litovchenko/AWN-Framework/main/CLAUDE.md`
   - `GEMINI.md` → `https://raw.githubusercontent.com/iv-litovchenko/AWN-Framework/main/GEMINI.md`
   - `QWEN.md` → `https://raw.githubusercontent.com/iv-litovchenko/AWN-Framework/main/QWEN.md`
   - `CODEX.md` → `https://raw.githubusercontent.com/iv-litovchenko/AWN-Framework/main/CODEX.md`
   - `DEEPSEEK.md` → `https://raw.githubusercontent.com/iv-litovchenko/AWN-Framework/main/DEEPSEEK.md`
   - `MISTRAL.md` → `https://raw.githubusercontent.com/iv-litovchenko/AWN-Framework/main/MISTRAL.md`
3. Если стартер ссылается на `AGENTS.LLM_BOOTSTRAP_PRESET.md`, проверь, что он есть в корне.

Если среда читает `AGENTS.md` напрямую, отдельный стартовый файл можно не добавлять.
