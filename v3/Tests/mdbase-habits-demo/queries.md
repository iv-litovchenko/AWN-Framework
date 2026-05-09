# Query examples

## 1) Только ежедневные привычки

```yaml
query:
  types: [habit]
  where: 'frequency == "daily"'
```

## 2) Активные привычки с серией >= 7

```yaml
query:
  types: [habit]
  where:
    and:
      - "active == true"
      - "streak_days >= 7"
```
