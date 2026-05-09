---
name: task
validation: error
fields:
  title:
    type: string
    required: true
  status:
    type: enum
    values: [open, in_progress, done]
    default: open
  priority:
    type: integer
    min: 1
    max: 5
  assignee:
    type: link
    target: person
  due_date:
    type: date
  tags:
    type: list
    items:
      type: string
---

# Type: task

Задача в бэклоге.  
`status` отслеживает прогресс, `priority` задает срочность.
