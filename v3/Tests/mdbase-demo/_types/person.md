---
name: person
validation: warn
fields:
  full_name:
    type: string
    required: true
  team:
    type: enum
    values: [engineering, design, ops]
  role:
    type: string
  email:
    type: string
---

# Type: person

Контакт человека для назначения задач и связок через `link`.
