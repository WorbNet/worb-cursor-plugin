---
name: standup-transcript-to-board
description: Turn a standup transcript into a proposed bioing standup board, then write tasks and standup entries only after the user confirms. Use when the user pastes a standup transcript, meeting notes, or asks to update the board from spoken standup.
---

# Standup transcript → board

Connect to the **worb** MCP server (bioing). Do not invent people, projects, or task IDs.

## Tools

`whoami`, `list_org_members`, `list_projects`, `list_tasks`, `get_task`, `create_task`, `update_task`, `list_standup_entries`, `add_standup_entry`. Optional: `remove_standup_entry`.

Descript, Google Calendar, and Drive are **not** part of this MCP. If the user has a transcript file, they paste it or attach it here.

## Product rules

- Members/assignees only from `list_org_members` (match names to `id` + `display_name`). Never invent members.
- Task statuses: `pending` | `in_progress` | `blocked` | `done` only.
- Short titles; full context in `description`.
- Propose first. **Wait for explicit user confirmation** before `create_task`, `update_task`, or `add_standup_entry`.

## Board rendering

One task per block:

```
Title of the task
⚪
```

Icons only on the second line (no status words): ⚪ pending, 🔵 in_progress, 🔴 blocked, 🟢 done.

Group by person, then by project name.

## Workflow

1. Call `whoami`, `list_org_members`, `list_projects`.
2. `list_tasks` (open by default). `list_standup_entries` for today (and yesterday if useful).
3. Parse the transcript: who spoke, what they worked on, blockers, new work. Map names to member ids.
4. Show a **proposal**: new tasks, status changes, standup adds (task + `entry_date`). Flag unmatched names instead of guessing.
5. After the user confirms, call write tools, then `list_standup_entries` and render the standup board.
