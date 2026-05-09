# Query examples

## 1) Все незавершенные задачи с приоритетом >= 3

```yaml
query:
  types: [task]
  where:
    and:
      - 'status != "done"'
      - "priority >= 3"
  order_by:
    - field: due_date
      direction: asc
```

## 2) Все задачи Alice

```yaml
query:
  types: [task]
  where: 'assignee == "[[alice]]"'
```

## 3) Задачи с тегом docs

```yaml
query:
  types: [task]
  where: 'tags.contains("docs")'
```

## 4) Только открытые задачи, лимит 1

```yaml
query:
  types: [task]
  where: 'status == "open"'
  limit: 1
```
