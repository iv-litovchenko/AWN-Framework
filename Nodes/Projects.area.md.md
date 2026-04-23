---
TYPE: AREA
MODE: SPACE
ROLE: Project_Manager
SOURCE_MANIFEST: "manifest.node.json"
---
# 🏗 Neuro-Map: Реестр Внешних Тел

Этот нейрон управляет связями между базой знаний и внешним кодом.

## 🛰 Состояние узлов (Auto-scan)
| Проект        | Путь                      | Стек              | Роль в системе            |
| :------------ | :------------------------ | :---------------- | :------------------------ |
| **Project 1** | `Projects/medknizhky@ext` | PHP 8.1 / WP      | Основной проект (филиалы) |
| **AWN Core**  | `Frameworks/AWN@ext`      | PHP 8.3           | Собственный фреймворк     |
| **Project 2** | `Projects/spravky@ext`    | Next.js / Payload | Редизайн агрегатора       |

## 🛠 Команды Регенерации
- `git-restore`: Скачать все отсутствующие `@ext` репозитории.
- `health-check`: Проверить версии PHP/Node на текущем сервере.

> **Инструкция для Aya:**
> 1. При переходе в любую папку с постфиксом `@ext`, используй контекст из этого манифеста.
> 2. Если папка пуста — выведи предупреждение: **"NODE_MISSING: Требуется синхронизация"**.


manifest.node.json

```
{
  "vault_name": "Aya-Cognitive-OS",
  "owner": "iv-litovchenko",
  "last_sync": "2026-04-23",
  "external_nodes": [
    {
      "id": "awn-framework",
      "path": "Development/Frameworks/AWN@ext",
      "source": "https://github.com/your-repo/awn-core.git",
      "type": "git-repo",
      "status": "development",
      "environment": {
        "engine": "PHP-Custom",
        "php": "8.3",
        "composer": true
      }
    },
  ],
  "infrastructure": {
    "required_tools": ["git", "docker", "ollama", "php", "node"],
    "os_target": "MacOS (MacBook Pro)"
  }
}
```