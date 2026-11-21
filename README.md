
# Worb for Cursor

Connect Cursor to your Worb account and interact with your data through
the Worb MCP server.

## Features

- Connect using your own Worb account.
- Authenticate securely through OAuth.
- Read your own Worb profile.
- Update supported profile fields.
- List the projects you belong to or created.
- List milestones on projects you belong to.
- List tasks assigned to you.
- See the open task queue for each project you belong to.
- Read your standup entries for yesterday and today.
- Create milestones in projects you manage.
- Create tasks assigned to you.
- Update tasks in projects you belong to.
- Use Worb from compatible Cursor projects.

## Requirements

- Cursor with support for MCP servers and plugins.
- An active Worb account.
- Internet access to reach the Worb MCP server.

## Connection

Worb uses the hosted MCP server:

https://app.worb.net/mcp

Authentication is handled through Worb OAuth. Each user must authorize
their own account.

## Installation

This plugin is being prepared for distribution through GitHub and the
Cursor Marketplace.

Once published, install Worb from the Cursor Marketplace and follow
the authentication prompt to connect your Worb account.

## Available operations

- `get_my_profile`: retrieve the authenticated user's profile.
- `update_my_profile`: update supported fields in that profile.
- `list_my_projects`: list projects the authenticated user belongs to or created. Optional `status` filter: `active`, `paused`, `completed`, or `cancelled`.
- `list_my_milestones`: list milestones on projects the authenticated user belongs to. Optional `project_id` and `status` (`planned`, `in_progress`, `done`, `blocked`).
- `list_my_tasks`: list tasks assigned to the authenticated user. Optional `project_id`, `status` (`pending`, `in_progress`, `done`, `blocked`), and `include_archived`.
- `get_task_queue`: open task queue grouped by project. Includes tasks whose status is not `done` and that have no `archived_at`. Optional `project_id`.
- `get_standup`: the authenticated user's standup entries for yesterday and today (`America/Bogota`) from `standup_entries`.
- `create_milestone`: create a milestone in a project the user can manage. Requires `project_id` and `title`. Optional `due_date` (`YYYY-MM-DD`) and `status` (`planned` by default, or `in_progress`, `done`, `blocked`). Requires the `projects:write` scope.
- `create_task`: create a task assigned to the authenticated user. Requires `project_id`, `title`, `description`, and `milestone_id`. Optional `status` (`pending` by default). Also inserts the user into `task_assignees`. Requires the `tasks:write` scope.
- `update_task`: update a task in a project the user belongs to. Requires `task_id`. Optional `title`, `status`, `description`, and `milestone_id`. Requires the `tasks:write` scope.

Available operations depend on the tools exposed by the Worb MCP server.

## Security

- Never share your Worb password or access tokens.
- Each user accesses their own account through OAuth.
- Access permissions are enforced by the Worb server.
- Do not store private credentials in this repository.

## Support

Website: https://app.worb.net