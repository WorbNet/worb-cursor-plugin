---
name: standup-board
description: Render yesterday or today bioing standup as a board with status icons only. Use when the user asks for standup, daily board, or ayer/hoy. Adds entries only after confirm.
---

# Standup board

Connect to the **worb** MCP server (bioing).

## Tools

`whoami`, `list_org_members`, `list_standup_entries`, `add_standup_entry` (after confirm). New work: `list_projects`, `list_tasks`, `create_task` only after confirm. Prefer adding existing queue items via the task-queue flow, then `add_standup_entry`.

## Product rules

- Never invent members.
- Icons only (no status words): ⚪ pending, 🔵 in_progress, 🔴 blocked, 🟢 done.
- Title line, icon on the next line.
- Writes only after the user confirms.

## Workflow

1. Resolve dates: **hoy** = today, **ayer** = yesterday (user timezone if known, else UTC date).
2. `list_standup_entries` with `entry_date` or `from_date` + `to_date`. Optional `user_id` (default caller; leads may pass another member from `list_org_members`).
3. Render grouped by person, then project, using `task_title`, `task_status`, `project_name`.
4. To add work: identify an existing task (`list_tasks`) or propose `create_task`, then `add_standup_entry`. Confirm before any write.

Do not use Descript or Calendar from this skill.
