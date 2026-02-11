# session-logs

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/guogang1024/session-logs/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/guogang1024/session-logs/SKILL.md)
> Category: Search & Research

---

## Description

Search and analyze your own session logs (older/parent conversations) using jq.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Search and analyze your own session logs (older/parent conversations) using jq.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run session-logs`)
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
You are executing the session-logs workflow. Use the following context:

Description: Search and analyze your own session logs (older/parent conversations) using jq.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: session-logs
category: Search & Research
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# session-logs

Search your complete conversation history stored in session JSONL files. Use this when a user references older/parent conversations or asks what was said before.

## Trigger

Use this skill when the user asks about prior chats, parent conversations, or historical context that isn’t in memory files.

## Location

Session logs live at: `~/.clawdbot/agents/<agentId>/sessions/` (use the `agent=<id>` value from the system prompt Runtime line).

- **`sessions.json`** - Index mapping session keys to session IDs
- **`<session-id>.jsonl`** - Full conversation transcript per session

## Structure

Each `.jsonl` file contains messages with:
- `type`: "session" (metadata) or "message"
- `timestamp`: ISO timestamp
- `message.role`: "user", "assistant", or "toolResult"
- `message.content[]`: Text, thinking, or tool calls (filter `type=="text"` for human-readable content)
- `message.usage.cost.total`: Cost per response

## Common Queries

### List all sessions by date and size
```bash
for f in ~/.clawdbot/agents/<agentId>/sessions/*.jsonl; do
  date=$(head -1 "$f" | jq -r '.timestamp' | cut -dT -f1)
  size=$(ls -lh "$f" | awk '{print $5}')
  echo "$date $size $(basename $f)"
done | sort -r
```

### Find sessions from a specific day
```bash
for f in ~/.clawdbot/agents/<agentId>/sessions/*.jsonl; do
  head -1 "$f" | jq -r '.timestamp' | grep -q "2026-01-06" && echo "$f"
done
```

### Extract user messages from a session
```bash
jq -r 'select(.message.role == "user") | .message.content[]? | select(.type == "text") | .text' <session>.jsonl
```

### Search for keyword in assistant responses
```bash
jq -r 'select(.message.role == "assistant") | .message.content[]? | select(.type == "text") | .text' <session>.jsonl | rg -i "keyword"
```

### Get total cost for a session
```bash
jq -s '[.[] | .message.usage.cost.total // 0] | add' <session>.jsonl
```

### Daily cost summary
```bash
for f in ~/.clawdbot/agents/<agentId>/sessions/*.jsonl; do
  date=$(head -1 "$f" | jq -r '.timestamp' | cut -dT -f1)
  cost=$(jq -s '[.[] | .message.usage.cost.total // 0] | add' "$f")
  echo "$date $cost"
done | awk '{a[$1]+=$2} END {for(d in a) print d, "$"a[d]}' | sort -r
```

### Count messages and tokens in a session
```bash
jq -s '{
  messages: length,
  user: [.[] | select(.message.role == "user")] | length,
  assistant: [.[] | select(.message.role == "assistant")] | length,
  first: .[0].timestamp,
  last: .[-1].timestamp
}' <session>.jsonl
```

### Tool usage breakdown
```bash
jq -r '.message.content[]? | select(.type == "toolCall") | .name' <session>.jsonl | sort | uniq -c | sort -rn
```

### Search across ALL sessions for a phrase
```bash
rg -l "phrase" ~/.clawdbot/agents/<agentId>/sessions/*.jsonl
```

## Tips

- Sessions are append-only JSONL (one JSON object per line)
- Large sessions can be several MB - use `head`/`tail` for sampling
- The `sessions.json` index maps chat providers (discord, whatsapp, etc.) to session IDs
- Deleted sessions have `.deleted.<timestamp>` suffix

## Fast text-only hint (low noise)

```bash
jq -r 'select(.type=="message") | .message.content[]? | select(.type=="text") | .text' ~/.clawdbot/agents/<agentId>/sessions/<id>.jsonl | rg 'keyword'
```

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
