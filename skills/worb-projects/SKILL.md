---
name: worb-projects
description: Use Worb to list the authenticated user's own projects, milestones, tasks, open task queues, and standup through the Worb MCP server.
---

# Worb projects

Use the Worb MCP server when the user asks which projects, milestones, or tasks they have, asks for the open task queue of a project, or asks for their standup.

## Available tools

### list_my_projects

Lists projects the authenticated user can access:

- projects where the user is a member
- projects the user created

Optional argument:

- `status`: `active`, `paused`, `completed`, or `cancelled`. Omit it to return every status.

Each project includes its code, name, description, status, type, dates, workspace organization, the user's access level, and whether they created it.

This tool requires the `projects:read` OAuth scope. If the call fails because that scope is missing, ask the user to reconnect Worb in Cursor so the permission is granted.

### list_my_milestones

Lists milestones on projects where the authenticated user is a member.

Optional arguments:

- `project_id`: limit the list to one project the user belongs to.
- `status`: `planned`, `in_progress`, `done`, or `blocked`. Omit it to return every status.

Each milestone includes its title, status, due date, completion time, sort order, and the project code and name.

This tool uses the same `projects:read` OAuth scope as `list_my_projects`.

### list_my_tasks

Lists tasks assigned to the authenticated user on projects where they are a member. A task counts when `assigned_user_id` is the user or the user is in `task_assignees`.

Optional arguments:

- `project_id`: limit the list to one project the user belongs to.
- `status`: `pending`, `in_progress`, `done`, or `blocked`. Omit it to return every status.
- `include_archived`: set to true to include tasks archived with a completed milestone. Omit it to hide archived tasks.

Each task includes its title, description, status, priority, due date, tags, project code and name, and milestone title.

This tool uses the same `projects:read` OAuth scope as `list_my_projects`.

### get_task_queue

Returns the open task queue grouped by project. A task is open when its status is not `done` and `archived_at` is empty. The queue includes every open task on projects where the authenticated user is a member, not only tasks assigned to them.

Optional argument:

- `project_id`: limit the queue to one project the user belongs to. If that project has no open tasks, it is still returned with an empty task list.

Projects with no open tasks are omitted when `project_id` is not provided. Within each project, tasks are ordered by priority (`urgent`, `high`, `medium`, `low`) and then by due date.

This tool uses the same `projects:read` OAuth scope as `list_my_projects`.

### get_standup

Reads the authenticated user's rows in `standup_entries` whose `entry_date` is yesterday or today in `America/Bogota`. Each entry includes the note and the current task title, status, priority, and project.

Both days are always returned. An empty `entries` list means the user has no standup tasks for that day.

This tool uses the same `projects:read` OAuth scope as `list_my_projects`.

### create_milestone

Creates a milestone in a project the user can manage. The user must be a project owner or a project admin.

Arguments:

- `project_id`: required.
- `title`: required.
- `due_date`: optional date in `YYYY-MM-DD`.
- `status`: optional. One of `planned`, `in_progress`, `done`, or `blocked`. Defaults to `planned`.

Confirm the project and title with the user before calling this tool. Do not say the milestone was created unless the tool returns it.

This tool requires the `projects:write` OAuth scope. If the call fails because that scope is missing, ask the user to reconnect Worb in Cursor so the permission is granted.

### create_task

Creates a task in a milestone and assigns it to the authenticated user. The user must be an owner, admin, or member of the project. The tool also inserts that user into `task_assignees` and sets `assigned_user_id`.

Arguments:

- `project_id`: required.
- `title`: required.
- `description`: required. Use an empty string when there is no description.
- `milestone_id`: required. It must belong to `project_id`.
- `status`: optional. One of `pending`, `in_progress`, `done`, or `blocked`. Defaults to `pending`.

Confirm the project, milestone, and title before calling this tool. Do not say the task was created unless the tool returns it.

This tool requires the `tasks:write` OAuth scope. If the call fails because that scope is missing, ask the user to reconnect Worb in Cursor so the permission is granted.

### update_task

Updates an existing task. The user must be an owner, admin, or member of the task's project. At least one optional field is required.

Arguments:

- `task_id`: required.
- `title`: optional.
- `status`: optional. One of `pending`, `in_progress`, `done`, or `blocked`.
- `description`: optional. Use an empty string to clear it.
- `milestone_id`: optional. It must belong to the task's project.

Confirm the task and the new values before calling this tool. Do not say the task was updated unless the tool returns it.

This tool requires the `tasks:write` OAuth scope.

## Rules

- Use these tools instead of guessing the user's projects, milestones, tasks, open queues, or standup.
- Never ask the user for their Worb password or access token.
- Only list projects, milestones, tasks, and standup entries for the account authenticated through Worb OAuth.
- Report only the projects, milestones, tasks, standup entries, codes, and statuses returned by the tools.
- An empty list means the user has no matching projects, milestones, tasks, or standup entries.
- Do not use these tools to read or change another user's projects, milestones, tasks, or standup.
