---
name: habit
fields:
  title:
    type: string
    required: true
  frequency:
    type: enum
    values: [daily, weekly]
  streak_days:
    type: integer
    min: 0
  active:
    type: boolean
    default: true
---

# Type: habit

Привычка для личного трекера: периодичность, серия дней, активность.
