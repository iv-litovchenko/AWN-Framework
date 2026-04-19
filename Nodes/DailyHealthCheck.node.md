---
AWN-TYPE: "NODE/SOLO"
AWN-TITLE: Daily Health Check
AWN-DESCRIPTION: "Ежедневная проверка здоровья системы и генерация отчёта"
AWN-REQUIRE: on_demand
AWN-PRIORITY: 30
AWN-TRIGGERS: ["health check", "проверка здоровья", "ежедневный отчёт"]
AWN-AUTOMATIZATION: true
AWN-CRON: "30 8 * * *"  # Каждый день в 8:30 утра
AWN-STATUS: active
AWN-VERSION: 1.0.0
AWN-CREATED: 2026-04-19
AWN-UPDATED: 2026-04-19
AWN-MEMORY: external
---

# Daily Health Check

> [!info] О файле  
> Автоматизированная ежедневная проверка системы: создаёт отчёт о состоянии в 8:30 утра.

## Что проверяет

1. **Доступность сервисов**: проверяет ключевые endpoints
2. **Место на диске**: мониторит свободное пространство
3. **Логи ошибок**: анализирует recent errors
4. **Производительность**: проверяет время ответа

## Формат отчёта

Отчёт сохраняется в: `Reports/Health/{дата}-health-report.md`

```markdown
# Health Report - {дата}

## ✅ Сервисы
- Service A: доступен (200ms)
- Service B: доступен (150ms)

## 💾 Диск
- Свободно: 45GB / 120GB
- Использовано: 63%

## ⚠️ Предупреждения
- Нет критических ошибок

## 📊 Метрики
- CPU: 45%
- Memory: 60%
- Uptime: 14 days
```

## Ручной запуск

Триггер: "health check" или "проверка здоровья"