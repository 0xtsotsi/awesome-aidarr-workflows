# staratheris-arya-reminders

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/staratheris/staratheris-arya-reminders/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/staratheris/staratheris-arya-reminders/SKILL.md)
> Category: CLI Utilities

---

## Description

Recordatorios en lenguaje natural (Bogotá). Crea cron jobs seguros y registra en markdown (y opcionalmente Sheets).

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Recordatorios en lenguaje natural (Bogotá). Crea cron jobs seguros y registra en markdown (y opcionalmente Sheets).

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run staratheris-arya-reminders`)
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
You are executing the staratheris-arya-reminders workflow. Use the following context:

Description: Recordatorios en lenguaje natural (Bogotá). Crea cron jobs seguros y registra en markdown (y opcionalmente Sheets).

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: staratheris-arya-reminders
category: CLI Utilities
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Arya Reminders

Recordatorios en lenguaje natural para OpenClaw, diseñados para Jaider.

## Qué hace

- Interpreta fechas/horas relativas y absolutas en español (y formatos comunes).
- Usa **America/Bogota** por defecto.
- Crea recordatorios **one-shot** (una sola vez) como cron jobs.
- Registra cada recordatorio en `memory/reminders.md`.
- (Opcional futuro) registrar en Google Sheets cuando esté habilitado.

## Uso (conversacional)

Ejemplos:
- "Recuérdame pagar la luz mañana a las 3pm"
- "Recuérdame en 45 minutos revisar el horno"
- "Recuérdame hoy a las 5:30pm llamar a mamá"
- "Recuérdame el viernes a las 9am entregar el taller"

## Comandos (manual)

### Crear recordatorio (una vez)

```bash
bash skills/arya-reminders/create-reminder.sh "Mensaje" "Cuándo"
```

### Revisar log

```bash
cat memory/reminders.md
```

## Notas

- No requiere APIs externas.
- Usa el tool `cron` del Gateway (no hardcodea rutas ni IDs ajenos).

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
