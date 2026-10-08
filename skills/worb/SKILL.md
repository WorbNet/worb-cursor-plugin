---
name: worb
description: Use Worb to read and update the authenticated user's own profile through the Worb MCP server.
---

# Worb — Cursor Skill

Use the Worb MCP server when the user asks to consult or update information
stored in their Worb account.

## Available tools

### get_my_profile

Use this tool when the user wants to see their own Worb profile.

### update_my_profile

Use this tool when the user explicitly asks to modify their own profile.

## Rules

- Use the Worb MCP tools instead of guessing the user's profile data.
- Never ask the user to provide their Worb password or access token in chat.
- Only access the account authenticated through Worb OAuth.
- Never attempt to read or modify another user's account.
- Before modifying profile data, identify the requested fields and values.
- After an update, verify the result by reading the profile again when appropriate.
- If authentication fails, ask the user to reconnect Worb through Cursor.
- If a requested operation is unavailable, explain that limitation honestly.
- Do not claim that a change succeeded unless the MCP tool confirms it.