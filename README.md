# Plugin de Worb

Conecta Cursor, Claude Desktop o Google Antigravity a tu cuenta de Worb y
trabaja con tus datos a través del servidor MCP de Worb.

## Qué puedes hacer

- Conectarte con tu propia cuenta de Worb.
- Iniciar sesión con OAuth.
- Leer tu perfil.
- Actualizar los campos de perfil permitidos.
- Ver los proyectos que creaste o a los que perteneces.
- Ver los hitos de esos proyectos.
- Ver las tareas que tienes asignadas.
- Ver la cola de tareas abiertas de cada proyecto.
- Leer tus entradas de standup de ayer y de hoy.
- Crear hitos en los proyectos que administras.
- Crear tareas asignadas a ti.
- Actualizar tareas de los proyectos a los que perteneces.

## Qué necesitas

- Cursor, Claude Desktop o Google Antigravity.
- Una cuenta activa de Worb.
- Internet para llegar al servidor MCP de Worb.

## Conexión

El servidor es:

https://app.worb.net/mcp

Cada persona autoriza su propia cuenta de Worb. La contraseña no se guarda en
el plugin.

## Cómo instalarlo

### Claude Desktop

Claude Desktop no lee los archivos del plugin. El conector se agrega en la
cuenta de Claude.

1. Abre **Configuración → Conectores → Agregar conector personalizado**.
2. En el nombre escribe **Worb**. Ese texto es el que aparece en la lista.
3. En la URL del servidor MCP escribe `https://app.worb.net/mcp`.
4. En autenticación deja **Iniciar sesión ahora**.
5. En cliente OAuth elige **Usar tu propio cliente OAuth**.
6. En el identificador del cliente escribe `claude-desktop-worb`.
7. Deja el secreto vacío y no agregues encabezados.
8. En **Avanzado**, deja el transporte en **HTTP transmitible**.
9. Haz clic en **Agregar**.
10. Haz clic en **Conectar**, inicia sesión en Worb y pulsa **Autorizar**.

Esa configuración queda en la cuenta de Claude, así que aparece en las otras
computadoras donde esa persona haya iniciado sesión. En un plan Team o
Enterprise, un propietario puede agregar el conector una vez para la
organización. Cada miembro igual entra con su propia cuenta de Worb.

### Cursor

El plugin de Cursor usa `.cursor-plugin/plugin.json` y `mcp.json`. Sirve para
entrar a la cuenta de Worb, ver el perfil, listar proyectos y administrar
tareas. El cliente OAuth ya va en el plugin: `cursor-worb`. Quien lo instala
no escribe ese nombre.

Copia esta carpeta del repositorio dentro de la carpeta local de plugins.
Cursor no carga un acceso directo que apunte afuera de esa carpeta.

En Mac, en Terminal:

```bash
mkdir -p ~/.cursor/plugins/local
cp -R /ruta/a/worb-plugin ~/.cursor/plugins/local/worb
```

En Windows, en PowerShell:

```powershell
New-Item -ItemType Directory -Force -Path "$env:USERPROFILE\.cursor\plugins\local"
Copy-Item -Recurse -Force "C:\ruta\a\worb-plugin" "$env:USERPROFILE\.cursor\plugins\local\worb"
```

La carpeta queda en:

- Mac: `~/.cursor/plugins/local/worb`
- Windows: `C:\Users\<usuario>\.cursor\plugins\local\worb`

Después:

1. Cierra Cursor y ábrelo de nuevo. También puedes abrir la paleta de comandos y ejecutar **Developer: Reload Window**.
2. Abre **Customize** en la barra lateral y confirma que aparece **Worb**.
3. Cuando Cursor pida conectar el servidor MCP, inicia sesión en Worb en el navegador y pulsa **Autorizar**.

### Google Antigravity

El plugin de Antigravity usa `.antigravity-plugin/plugin.json` y
`mcp_config.json`. Sirve para ver y actualizar el perfil, listar proyectos e
hitos, revisar el standup y administrar tareas. El cliente OAuth ya va en el
plugin: `antigravity-worb`.

Copia esta carpeta del repositorio a la carpeta de plugins de Antigravity.
Si Antigravity está abierto, ciérralo por completo antes de copiar. Cerrar la
ventana no basta: sal de la app.

En Mac, en Terminal:

```bash
mkdir -p ~/.gemini/config/plugins
cp -R /ruta/a/worb-plugin ~/.gemini/config/plugins/worb
```

En Windows, en PowerShell:

```powershell
New-Item -ItemType Directory -Force -Path "$env:USERPROFILE\.gemini\config\plugins"
Copy-Item -Recurse -Force "C:\ruta\a\worb-plugin" "$env:USERPROFILE\.gemini\config\plugins\worb"
```

La carpeta queda en:

- Mac: `~/.gemini/config/plugins/worb`
- Windows: `C:\Users\<usuario>\.gemini\config\plugins\worb`

Si tienes la CLI `agy`, el mismo paso en Mac y en Windows es:

```bash
agy plugin install /ruta/a/worb-plugin
```

Abre Antigravity de nuevo.

En la app:

1. Haz clic en **Customizations** en la barra lateral.
2. Abre la pestaña **Installed**.
3. Busca **Worb** y baja hasta **MCP Servers**. El servidor se llama `worb_worb` y apunta a `https://app.worb.net/mcp`.
4. Haz clic en **Authenticate**.
5. Termina el inicio de sesión de Worb en el navegador, copia el código de autorización, pégalo en **Enter authorization code** y haz clic en **Submit**.

En el editor:

1. Haz clic en **…** arriba del panel del agente.
2. Elige **MCP Servers**.
3. Si el servidor no está en la lista, abre **Manage MCP Servers** y autentica el mismo servidor de Worb.

Cuando la conexión funciona, las herramientas aparecen con el prefijo
`worb_worb_`, por ejemplo `worb_worb_get_my_profile`. Puedes probar con
“Muéstrame mis tareas abiertas de Worb”.

## Operaciones

- `get_my_profile`: lee el perfil de la persona autenticada.
- `update_my_profile`: actualiza los campos permitidos de ese perfil.
- `list_my_projects`: lista los proyectos que creó o a los que pertenece. Filtro opcional `status`: `active`, `paused`, `completed` o `cancelled`.
- `list_my_milestones`: lista los hitos de esos proyectos. Filtros opcionales `project_id` y `status` (`planned`, `in_progress`, `done`, `blocked`).
- `list_my_tasks`: lista las tareas asignadas a esa persona. Filtros opcionales `project_id`, `status` (`pending`, `in_progress`, `done`, `blocked`) e `include_archived`.
- `get_task_queue`: cola de tareas abiertas, agrupada por proyecto. Incluye las tareas cuyo estado no es `done` y que no tienen `archived_at`. Filtro opcional `project_id`.
- `get_standup`: entradas de standup de ayer y de hoy (`America/Bogota`) en `standup_entries`.
- `create_milestone`: crea un hito en un proyecto que la persona puede administrar. Requiere `project_id` y `title`. Opcionales `due_date` (`YYYY-MM-DD`) y `status` (`planned` por defecto, o `in_progress`, `done`, `blocked`). Requiere el alcance `projects:write`.
- `create_task`: crea una tarea asignada a la persona autenticada. Requiere `project_id`, `title`, `description` y `milestone_id`. Opcional `status` (`pending` por defecto). También la agrega en `task_assignees`. Requiere el alcance `tasks:write`.
- `update_task`: actualiza una tarea de un proyecto al que pertenece. Requiere `task_id`. Opcionales `title`, `status`, `description` y `milestone_id`. Requiere el alcance `tasks:write`.

Las operaciones disponibles dependen de las herramientas que exponga el servidor MCP de Worb.

## Seguridad

- No compartas tu contraseña de Worb ni tus tokens de acceso.
- Cada persona entra a su propia cuenta con OAuth.
- Los permisos los aplica el servidor de Worb.
- No guardes credenciales privadas en este repositorio.

## Soporte

Sitio: https://app.worb.net
