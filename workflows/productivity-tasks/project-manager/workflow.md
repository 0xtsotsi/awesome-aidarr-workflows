# project-manager

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/fr0ziii/project-manager/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/fr0ziii/project-manager/SKILL.md)
> Category: Productivity & Tasks

---

## Description

No description available.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
What this workflow accomplishes.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run project-manager`)
**Workflow:** Execute skill logic with context from AiDarr's ATLAS memory

### T - Tools
Required tools (add as needed):
- HTTP requests (for API calls)
- Memory system (ATLAS for persistence)
- Context retrieval (from GOTCHA workspace)

### C - Context
Required context sources:
- User preferences from ATLAS memory
- Relevant documents from workspace
- Historical execution data

### H - Hard Prompts

```prompt
You are executing the project-manager workflow. Use the following context:

Description: 

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: project-manager
category: Productivity & Tasks
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content

# Skill: Project Manager (Vivi OS)

## Descripción
Gestiona el sistema de proyectos interno basado en JSON. Permite crear tareas, moverlas por el tablero Kanban y sincronizar con Apple Reminders.

## Ubicación de Datos
Base de datos: `/Users/fz1/clawd/data/pm/projects.json`

## Comandos (Mental Model)

### 1. Listar Tareas
*   **Acción**: Leer el JSON y mostrar las tareas agrupadas por columna o filtradas por proyecto.
*   **Uso**: "Qué tenemos pendiente?", "Estado del proyecto SaaS".

### 2. Añadir Tarea (Add)
*   **Acción**: Insertar objeto en el array `tasks`.
*   **Campos**: `projectId`, `title`, `priority` (low/med/high/crit), `sync` (true/false).
*   **Efecto Secundario**: Si `sync: true`, ejecutar skill `apple-reminders` para crear recordatorio.

### 3. Mover Tarea (Move)
*   **Acción**: Actualizar `status` de una tarea.
*   **Estados**: `todo` -> `in_progress` -> `review` -> `done` (o `blocked`).
*   **Notificación**: Si se mueve a `review` o `blocked`, avisar a David en el chat.

### 4. Sincronizar (Sync)
*   **Acción**: Forzar actualización de tareas con `sync: true` en Apple Reminders (si cambiaron de estado).

## Reglas de Negocio
1.  **Review**: Solo mover a `review` si necesito aprobación explícita de David.
2.  **Focus**: Máximo 3 tareas en `in_progress` simultáneamente.
3.  **Night Shift**: El turno de noche debe leer este JSON para saber qué priorizar si no hay órdenes explícitas.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
