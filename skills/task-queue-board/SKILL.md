---
name: task-queue-board
description: Render the bioing open-task queue as a board (person, project, title, status icon). Use when the user asks for the task queue, backlog, or what is open. Can pick tasks to add to standup after confirm.
---

# Task queue board

Connect to the **worb** MCP server (bioing).

## Tools

`list_org_members`, `list_projects`, `list_tasks`, `get_task`, `add_standup_entry` (only after confirm).

## Product rules

- Never invent members. Labels from live member and project lists.
- Default `list_tasks` to open work: `pending`, `in_progress`, `blocked` (not `done` unless asked).
- Board: title on one line, status icon only on the next (⚪ pending, 🔵 in_progress, 🔴 blocked, 🟢 done). No status words.

## Render

Group **person** (`assigned_to` / member display name) → **project** → tasks:

```
## Name

### Project name

Task title
🔵
```

Unassigned tasks go under a clear “Unassigned” heading.

## Add to standup

If the user picks tasks for standup: propose `add_standup_entry` with `task_id` and `entry_date` (default today). **Wait for confirm**, then write. Do not create calendar events.
