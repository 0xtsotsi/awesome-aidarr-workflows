# side-peace

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/bitbrujo/side-peace/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/bitbrujo/side-peace/SKILL.md)
> Category: Coding Agents & IDEs

---

## Description

Minimal secure secret handoff. Zero external deps. Human opens browser form, submits secret, agent receives it via temp file. Secret NEVER appears in stdout/logs.

**Homepage:** N/A
**Repository:** N/A
**Version:** 1.1.0

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Minimal secure secret handoff. Zero external deps. Human opens browser form, submits secret, agent receives it via temp file. Secret NEVER appears in stdout/logs.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run side-peace`)
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
You are executing the side-peace workflow. Use the following context:

Description: Minimal secure secret handoff. Zero external deps. Human opens browser form, submits secret, agent receives it via temp file. Secret NEVER appears in stdout/logs.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: side-peace
category: Coding Agents & IDEs
version: 1.1.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Side_Peace 🍒

Dead simple secret handoff from human to AI. No npm packages to trust — just Node.js built-ins.

**Key security feature:** Secret is written to a temp file, NEVER printed to stdout. This prevents secrets from appearing in chat logs or command output.

## How It Works

1. Agent runs `node drop.js --label "API Key"`
2. Agent shares the URL with human
3. Human opens URL in browser, pastes secret, submits
4. Secret is saved to temp file (printed path only, not content)
5. Agent reads file, uses secret, deletes file

## Usage

```bash
# Basic - secret saved to random temp file
node skills/side-peace/drop.js --label "CLAWHUB_TOKEN"

# Custom output path
node skills/side-peace/drop.js --label "API_KEY" --output /tmp/my-secret.txt

# Custom port
node skills/side-peace/drop.js --port 4000 --label "TOKEN"
```

## Reading the Secret

After receiving, the secret is in the temp file:

```bash
# Read and use (example with clawhub)
SECRET=$(cat /tmp/side-peace-xxx.secret)
npx clawhub login --token "$SECRET" --no-browser
rm /tmp/side-peace-xxx.secret
```

Or one-liner:
```bash
cat /tmp/side-peace-xxx.secret | xargs -I{} npx clawhub login --token {} --no-browser; rm /tmp/side-peace-xxx.secret
```

## Security

- **Zero dependencies** — only Node.js built-ins
- **Secret never in stdout** — written to file with 0600 permissions
- **Memory only until saved** — temp file deleted after use
- **One-time** — server exits after receiving
- **~60 lines** — fully auditable

## Output

```
🍒 Side_Peace waiting...
   Label: CLAWHUB_TOKEN
   Output: /tmp/side-peace-a1b2c3d4.secret

   Local:    http://localhost:3000
   Network:  http://192.168.1.94:3000

Waiting for secret...

✓ Secret received and saved.
  File: /tmp/side-peace-a1b2c3d4.secret
  (Secret is NOT printed to stdout for security)
```

The secret is in the file. Read it, use it, delete it.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
