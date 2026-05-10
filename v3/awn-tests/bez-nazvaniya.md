---
AWN-TYPE: NODE/TASK
AWN-TITLE: Задача
AWN-DESC: Управление задачами
properties:
  title:
    type: string
  description:
    type: text
  dueDate:
    type: date
  status:
    type: enum
    options:
      - open
      - in_progress
      - closed
homepage: https://github.com/pimalaya/himalaya
---

# Задача: {{ title }}

**Статус:** {{ status }}
**Дедлайн:** {{ dueDate | date }}

## Описание
{{ description }}
