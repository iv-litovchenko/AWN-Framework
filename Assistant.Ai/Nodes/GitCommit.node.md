---
AWN-TYPE: "NODE/SOLO"
AWN-TITLE: Git Commit Basics (GitWorkflow)
AWN-DESC: "Нода-заглушка: как безопасно и понятно коммитить изменения; базовый GitWorkflow."
AWN-LOAD: on_demand
AWN-PRIORITY: 55
AWN-TRIGGERS: [git, commit, коммит, git commit, сохранить изменения, gitworkflow, git workflow]
AWN-STATUS: disabled
AWN-MEMORY: none
AWN-AUTOMATIZATION: false
AWN-CATEGORY: dev
AWN-VERSION: 0.1.0
AWN-CREATED: 2026-05-06
AWN-UPDATED: 2026-05-06
---

# Git Commit Basics

> [!info] О файле
> Заглушка ноды с минимальным процессом коммита и базовыми правилами безопасности.

## Назначение

Быстро напомнить, как коммитить изменения в git без лишнего риска.

## Быстрый сценарий

1. Проверить состояние:
   ```bash
   git status
   ```
2. Посмотреть изменения:
   ```bash
   git diff
   ```
3. Добавить нужные файлы:
   ```bash
   git add <file1> <file2>
   ```
   или все изменения:
   ```bash
   git add .
   ```
4. Создать коммит:
   ```bash
   git commit -m "feat: кратко что изменено и зачем"
   ```
5. Проверить, что коммит создан:
   ```bash
   git log --oneline -n 10
   ```

## Формат сообщений коммита (черновик)

- `feat:` новая функциональность
- `fix:` исправление багов
- `docs:` изменения документации
- `refactor:` рефакторинг без изменения поведения
- `chore:` сервисные изменения

Пример:
```bash
git commit -m "fix: исправлен обработчик пустого ответа API"
```

## Правила / Ограничения

- Не коммитить секреты (`.env`, токены, ключи, приватные конфиги).
- Делать маленькие логические коммиты вместо одного большого.
- Перед коммитом обязательно смотреть `git diff`.

## TODO

- Добавить правила по ветвлению.
- Добавить примеры плохих и хороших commit messages.
- Добавить шаги для `git push` и открытия PR.
