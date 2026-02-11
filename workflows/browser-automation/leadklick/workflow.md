# leadklick

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/big-roman123/leadklick/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/big-roman123/leadklick/SKILL.md)
> Category: Browser & Automation

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
**Trigger:** User-invocable (via `aidarr run leadklick`)
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
You are executing the leadklick workflow. Use the following context:

Description: 

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: leadklick
category: Browser & Automation
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content

# Lead Inbox Automator

Capture leads into a centralized Supabase database with automatic Make.com email automation.

## Description

This skill provides a complete lead management system for Clawd agents. It stores leads in Supabase, triggers Make.com webhooks for auto-reply emails, and tracks the full conversation lifecycle from "new" to "qualified".

## Configuration

```json
{
  "supabaseUrl": "https://your-project.supabase.co",
  "supabaseKey": "eyJ...your-service-role-key",
  "orgId": "550e8400-e29b-41d4-a716-446655440000",
  "defaultPriority": "medium"
}
```

**Important:** Use the Service Role Key, not the Anon Key, for full database access.

## Actions

### createLead

Create a new lead and automatically trigger the automation workflow.

**Parameters:**
- `email` (string, required): Contact email address
- `name` (string, optional): Contact person name
- `phone` (string, optional): Phone number
- `source` (string, optional): Origin channel (default: "clawd_agent")
- `priority` (string, optional): "low", "medium", "high", "urgent"
- `custom_fields` (object, optional): Any additional data

**Returns:**
```json
{
  "success": true,
  "lead_id": "uuid",
  "status": "new",
  "automation_triggered": true,
  "message": "Lead captured. Auto-reply will be sent within 60 seconds."
}
```

**Example:**
```typescript
const result = await skill.createLead({
  email: "customer@example.com",
  name: "Max Mustermann",
  source: "chat_bot",
  custom_fields: { product: "saas_basic" }
});
```

### getLead

Retrieve lead details including full conversation history.

**Parameters:**
- `id` (string, required): Lead UUID

**Returns:** Lead object with `conversations` array and `reply_pending` boolean.

### listLeads

List leads with filtering options.

**Parameters:**
- `status` (string, optional): Filter by status
- `priority` (string, optional): Filter by priority
- `limit` (number, optional): Max results (default: 50)
- `dateFrom` (string, optional): ISO date filter

**Returns:** Array of leads and total count.

### updateStatus

Update lead lifecycle status.

**Parameters:**
- `id` (string, required): Lead UUID
- `status` (string, required): "qualified", "won", "lost", etc.
- `notes` (string, optional): Qualification notes

### addConversation

Add a manual reply or note to the lead thread.

**Parameters:**
- `leadId` (string, required): Lead UUID
- `content` (string, required): Message text
- `subject` (string, optional): Subject line

### getAutomationStatus

Check if the auto-reply email was successfully sent.

**Parameters:**
- `leadId` (string, required): Lead UUID

**Returns:**
```json
{
  "auto_reply_sent": true,
  "minutes_since_creation": 2,
  "automation_ok": true
}
```

## Usage Flow

1. **Capture:** When a user expresses interest, call `createLead()`
2. **Verify:** After 60-120 seconds, call `getAutomationStatus()` to confirm auto-reply
3. **Qualify:** During conversation, update status to "qualified" if interested
4. **Log:** Use `addConversation()` to store your agent responses

## Error Handling

Common errors:
- Invalid email format
- Duplicate lead (within 24h)
- Missing Supabase credentials
- Automation timeout (>5min without reply)

## Schema

Leads table:
- id, email, name, phone, source, status, priority
- custom_fields (JSON), metadata (JSON)
- first_reply_sent_at, created_at

Conversations table:
- id, lead_id, direction (inbound/outbound/automated)
- content, subject, channel, sent_at

## Tags

lead, crm, sales, automation, email, supabase

## Version

1.0.0

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
