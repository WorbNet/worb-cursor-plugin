# WORB Cursor plugin

Connect [Cursor](https://cursor.com) and Grok Bot to **bioing** (tasks and standup) through a remote MCP server. You sign in with the same Google account as Prisma. This repo is **packaging only**: no database keys, no Edge Function source.

- GitHub: [WorbNet/worb-cursor-plugin](https://github.com/WorbNet/worb-cursor-plugin)
- MCP: `https://tazupqaykakgkbwmtxbl.supabase.co/functions/v1/mcp`
- Consent (production): [https://app.worb.net/oauth/consent](https://app.worb.net/oauth/consent)

## Install (local)

Until the plugin is on the [Cursor Marketplace](https://cursor.com/marketplace/publish):

1. **Customize → Plugins → + Add** and choose this repo folder (`worb-cursor-plugin`), **or**
2. Copy into Cursor’s local plugins directory:

```bash
rsync -a --exclude .git ./ ~/.cursor/plugins/local/worb/
```

Reload Cursor, enable **WORB** under Plugins, then **Authenticate** on the `worb` MCP server. The browser should open bioing Google login and the consent screen on `app.worb.net` once that route is deployed.

## Skills

| Skill | Use |
|--------|-----|
| `standup-transcript-to-board` | Transcript → proposed board → writes after confirm |
| `task-queue-board` | Open task queue by person and project |
| `standup-board` | Yesterday / today standup board |

Agents must **propose, then wait for your OK** before creating or updating tasks or standup rows. Members come only from the live org list.

## Example prompts

**English**

- Render the open task queue as a board.
- Show today’s standup board.
- Here’s yesterday’s standup transcript. Propose board updates; don’t write until I confirm.

**Español**

- Muéstrame el tablero de la cola de tareas abiertas.
- Standup de hoy, solo iconos de estado.
- Te pego la transcripción del standup. Propón cambios; no escribas hasta que confirme.

## Security

- No Supabase service role, anon key, or database password in this plugin.
- Access is a user OAuth token. **Row Level Security** on bioing decides what you can see.
- Calendar, Drive, and Descript stay as separate connectors.

## Marketplace

Do not submit until Phase A (consent on `app.worb.net` + MCP OAuth) is stable. Then publish from [cursor.com/marketplace/publish](https://cursor.com/marketplace/publish) with this public repo URL.
