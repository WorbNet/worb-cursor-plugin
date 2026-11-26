# WORB | Prisma Plugin 

Usa tu cuenta de Worb desde Cursor, Claude Desktop o Google Antigravity.

Cada persona entra con su propia cuenta. El plugin no guarda la contraseña.

## Antigravity

No está en el Marketplace. Se instala desde GitHub. Cierra Antigravity por completo antes de instalar.

`agy` no viene con la app. Instálalo una vez.

Mac:

```bash
curl -fsSL https://antigravity.google/cli/install.sh | bash
```

Windows (PowerShell):

```powershell
irm https://antigravity.google/cli/install.ps1 | iex
```

Si dice `agy: command not found`, abre una terminal nueva.

```bash
agy plugin install https://github.com/WorbNet/worb-cursor-plugin
```

Abre Antigravity.

1. **Customizations → Installed → Worb**.
2. Pestaña **Accounts**. Inicia sesión.
3. En el navegador, confirma que la aplicación es `antigravity-worb` y pulsa **Autorizar**.
4. Pega el código en **Paste code** y pulsa **Submit**.

La cuenta queda en **CONNECTED**. En el primer chat, permite `worb_worb/list_my_projects`.

## Cursor

1. Abre **Customize**.
2. Pulsa **+ Add** y elige **From GitHub Repository**.
3. Pega `https://github.com/WorbNet/worb-cursor-plugin`.
4. Abre **Worb** y pulsa **Sign In**.
5. En el navegador pulsa **Autorizar**.

El servidor `worb` queda con las 10 herramientas. Ya puedes usarlo en el chat.

## Claude Desktop

Claude no instala este repositorio. El conector se crea en la cuenta.

1. **Configuración → Conectores → Agregar conector personalizado**.
2. Nombre: **Prisma**.
3. URL: `https://app.worb.net/mcp`.
4. Autenticación: **Iniciar sesión ahora**.
5. Cliente OAuth: **Usar tu propio cliente OAuth**.
6. Identificador: `claude-desktop-worb`. Secreto vacío. Sin encabezados.
7. **Agregar**, luego **Conectar**, y en Worb pulsa **Autorizar**.

Queda en la cuenta de Claude. En Team o Enterprise, un propietario puede agregarlo para la organización. Cada miembro entra con su cuenta de Worb.

## Herramientas

| Herramienta | Hace |
| --- | --- |
| `get_my_profile` | Lee tu perfil. |
| `update_my_profile` | Actualiza los campos permitidos. |
| `list_my_projects` | Proyectos que creaste o a los que perteneces. `status`: `active`, `paused`, `completed`, `cancelled`. |
| `list_my_milestones` | Hitos de esos proyectos. `project_id`, `status`: `planned`, `in_progress`, `done`, `blocked`. |
| `list_my_tasks` | Tareas asignadas a ti. `project_id`, `status`: `pending`, `in_progress`, `done`, `blocked`, `include_archived`. |
| `get_task_queue` | Tareas abiertas por proyecto. Sin `done` y sin `archived_at`. `project_id` opcional. |
| `get_standup` | Standup de ayer y hoy, hora de Bogotá. |
| `create_milestone` | Crea un hito. Requiere `project_id`, `title`. Opcional `due_date`, `status`. Alcance `projects:write`. |
| `create_task` | Crea una tarea asignada a ti. Requiere `project_id`, `title`, `description`, `milestone_id`. Alcance `tasks:write`. |
| `update_task` | Actualiza una tarea tuya. Requiere `task_id`. Alcance `tasks:write`. |

Sitio: https://app.worb.net
