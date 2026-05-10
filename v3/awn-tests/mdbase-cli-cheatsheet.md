# mdbase CLI Cheatsheet

Quick command reference for local demo collections:

- `v3/awn-tests/mdbase-demo`
- `v3/awn-tests/mdbase-habits-demo`

## 0) Run from collection folder

`mdbase` looks for `mdbase.yaml` in the current directory.

```bash
cd "v3/awn-tests/mdbase-demo"
```

## 1) Validate collection

```bash
npx -y --package mdbase-cli mdbase validate .
```

## 2) Query all tasks

```bash
npx -y --package mdbase-cli mdbase query "" --types task --format table
```

## 3) Query non-done tasks

```bash
npx -y --package mdbase-cli mdbase query 'status != "done"' \
  --types task \
  --fields title,status,priority,assignee,due_date \
  --order-by -priority,due_date \
  --format table
```

## 4) Query urgent tasks by tag

```bash
npx -y --package mdbase-cli mdbase query 'tags.contains("urgent")' \
  --types task \
  --fields title,status,priority,tags \
  --format table
```

## 5) Query tasks assigned to Alice (wikilink style)

```bash
npx -y --package mdbase-cli mdbase query 'assignee == "[[alice]]"' \
  --types task \
  --fields title,status,assignee \
  --format table
```

## 6) Create a task

```bash
npx -y --package mdbase-cli mdbase create "tasks/new-task.md" \
  -t task \
  -f title="New task" status=open priority=3 due_date=2026-05-30 \
  --body "Task body text."
```

## 7) Update fields

```bash
npx -y --package mdbase-cli mdbase update "tasks/new-task.md" \
  -f status=in_progress priority=4
```

## 8) Set link field (markdown link style)

```bash
npx -y --package mdbase-cli mdbase update "tasks/new-task.md" \
  -f assignee="[alice](../people/alice.md)"
```

## 9) Read one file with parsed metadata

```bash
npx -y --package mdbase-cli mdbase read "tasks/new-task.md"
```

## 10) Rename with reference updates

```bash
npx -y --package mdbase-cli mdbase rename \
  "tasks/new-task.md" \
  "tasks/new-task-renamed.md"
```

## 11) Delete a file

```bash
npx -y --package mdbase-cli mdbase delete "tasks/new-task-renamed.md"
```

## 12) Lint and format frontmatter

```bash
npx -y --package mdbase-cli mdbase lint .
npx -y --package mdbase-cli mdbase fmt .
```

## 13) Collection stats

```bash
npx -y --package mdbase-cli mdbase stats
```

## 14) Types overview

```bash
npx -y --package mdbase-cli mdbase types --help
```

## 15) Habits demo quick switch

```bash
cd "../mdbase-habits-demo"
npx -y --package mdbase-cli mdbase validate .
npx -y --package mdbase-cli mdbase query 'active == true && streak_days >= 7' \
  --types habit \
  --fields title,frequency,streak_days,active \
  --format table
```

## Notes

- If `validate -c` fails with alias-related error, use `validate .`.
- Keep commands inside the collection root where `mdbase.yaml` exists.
