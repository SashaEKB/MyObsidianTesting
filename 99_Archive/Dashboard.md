---
type: dashboard
created: 2026-06-17
---

# DevOps Dashboard

## Start Here

- [[Home]]
- [[00_Inbox/Контекст для новой сессии с AI]]
- [[00_Inbox/Plugin Workflow]]
- [[04_DevOps/DevOps Roadmap]]

## Daily Lessons

```dataview
TABLE date AS "Date", topics AS "Topics"
FROM "01_Daily"
WHERE type = "daily"
SORT date DESC
```

## Projects

```dataview
TABLE status AS "Status", topics AS "Topics"
FROM "05_Projects"
WHERE type = "project"
SORT file.name ASC
```

## Errors

```dataview
TABLE area AS "Area", status AS "Status"
FROM "06_Errors"
WHERE type = "error"
SORT file.name ASC
```

## Cheatsheets

```dataview
LIST
FROM "07_Cheatsheets"
SORT file.name ASC
```

## Open Tasks

```tasks
not done
sort by due
sort by filename
limit 50
```

## Next Good Topics

- Linux filesystem.
- Users and groups.
- Permissions: `chmod`, `chown`, `umask`.
- Processes: `ps`, `top`, `kill`.
- Services: `systemctl`, `journalctl`.
- Networking basics.
- Git basics.
- Docker basics.
