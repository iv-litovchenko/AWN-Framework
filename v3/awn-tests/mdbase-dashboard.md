# mdbase Dashboard (Obsidian)

> [!info] Как использовать
> Этот дашборд использует `Dataview` code blocks.  
> Если таблицы не рендерятся, установи и включи плагин **Dataview** в Obsidian.

## Tasks (all)

```dataview
TABLE status, priority, assignee, due_date, tags
FROM "v3/awn-tests/mdbase-demo/tasks"
SORT due_date asc
```

## Tasks (open + in progress)

```dataview
TABLE status, priority, assignee, due_date
FROM "v3/awn-tests/mdbase-demo/tasks"
WHERE status != "done"
SORT priority desc, due_date asc
```

## Tasks (urgent)

```dataview
TABLE status, priority, assignee, due_date, tags
FROM "v3/awn-tests/mdbase-demo/tasks"
WHERE contains(tags, "urgent")
SORT due_date asc
```

## People

```dataview
TABLE full_name, team, role, email
FROM "v3/awn-tests/mdbase-demo/people"
SORT full_name asc
```

## Habits (all)

```dataview
TABLE frequency, streak_days, active
FROM "v3/awn-tests/mdbase-habits-demo/habits"
SORT streak_days desc
```

## Habits (active, streak >= 7)

```dataview
TABLE frequency, streak_days
FROM "v3/awn-tests/mdbase-habits-demo/habits"
WHERE active = true AND streak_days >= 7
SORT streak_days desc
```

## Quick links

- `v3/awn-tests/mdbase-demo/mdbase.yaml`
- `v3/awn-tests/mdbase-demo/_types/task.md`
- `v3/awn-tests/mdbase-demo/_types/person.md`
- `v3/awn-tests/mdbase-demo/queries.md`
- `v3/awn-tests/mdbase-habits-demo/mdbase.yaml`
- `v3/awn-tests/mdbase-habits-demo/_types/habit.md`
- `v3/awn-tests/mdbase-habits-demo/queries.md`
