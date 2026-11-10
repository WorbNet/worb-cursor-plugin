---
name: worb-projects
description: Use Worb to list the authenticated user's own projects through the Worb MCP server.
---

# Worb projects

Use the Worb MCP server when the user asks which projects they have, or asks to list, find, or summarize their own Worb projects.

## Available tools

### list_my_projects

Lists projects the authenticated user can access:

- projects where the user is a member
- projects the user created

Optional argument:

- `status`: `active`, `paused`, `completed`, or `cancelled`. Omit it to return every status.

Each project includes its code, name, description, status, type, dates, workspace organization, the user's access level, and whether they created it.

This tool requires the `projects:read` OAuth scope. If the call fails because that scope is missing, ask the user to reconnect Worb in Cursor so the permission is granted.

## Rules

- Use this tool instead of guessing the user's projects.
- Never ask the user for their Worb password or access token.
- Only list projects for the account authenticated through Worb OAuth.
- Report only the projects, codes, and statuses returned by the tool.
- An empty list means the user has no matching projects.
- Do not use this tool to read or change another user's projects.
