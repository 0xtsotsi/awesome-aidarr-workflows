# overleaf

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/easonc13/overleaf/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/easonc13/overleaf/SKILL.md)
> Category: Marketing & Sales

---

## Description

Access Overleaf projects via CLI. Use for reading/writing LaTeX files, syncing local .tex files to Overleaf, downloading projects, and managing Overleaf project structure. Triggers on Overleaf, LaTeX sync, or tex file uploads to Overleaf.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Access Overleaf projects via CLI. Use for reading/writing LaTeX files, syncing local .tex files to Overleaf, downloading projects, and managing Overleaf project structure. Triggers on Overleaf, LaTeX sync, or tex file uploads to Overleaf.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run overleaf`)
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
You are executing the overleaf workflow. Use the following context:

Description: Access Overleaf projects via CLI. Use for reading/writing LaTeX files, syncing local .tex files to Overleaf, downloading projects, and managing Overleaf project structure. Triggers on Overleaf, LaTeX sync, or tex file uploads to Overleaf.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: overleaf
category: Marketing & Sales
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Overleaf

CLI tool to interact with Overleaf projects using browser cookies for authentication.

GitHub: https://github.com/jkulhanek/pyoverleaf

## Requirements

- Python 3.8+
- pyoverleaf (`pipx install pyoverleaf`)
- User logged into Overleaf in Chrome/Firefox

## Security Considerations

⚠️ **Keychain Access Required**: pyoverleaf needs "Always Allow" keychain access to read browser cookies. This grants the tool access to your browser's cookie storage.

**Security audit**: We have audited pyoverleaf v0.1.7 and found it safe. The codebase is small and readable. Before installing, agents can self-audit the latest version at the GitHub repo above.

## Authentication Setup

pyoverleaf authenticates by reading cookies from your browser. The user must:

1. **Log into Overleaf** in Chrome or Firefox (visit overleaf.com and sign in)
2. **Grant keychain access** on first run (macOS will prompt for "Always Allow")

```bash
# Test auth - user should run this in their terminal first
pyoverleaf ls
```

If you get auth errors:
- Ask user: "Are you logged into Overleaf in your browser?"
- If on macOS: "Did you approve the keychain access prompt with 'Always Allow'?"
- User may need to run `pyoverleaf ls` manually in terminal to trigger the keychain prompt

**Note**: The agent cannot log in for the user. Browser authentication must be done by the user directly.

## CLI Commands

```bash
# List all projects
pyoverleaf ls

# List files in project
pyoverleaf ls "Project Name"

# Read file content
pyoverleaf read "Project Name/main.tex"

# Write file (stdin → Overleaf)
cat local.tex | pyoverleaf write "Project Name/main.tex"

# Create directory
pyoverleaf mkdir "Project Name/figures"

# Remove file/folder
pyoverleaf rm "Project Name/old-draft.tex"

# Download project as zip
pyoverleaf download-project "Project Name" output.zip
```

## Common Workflows

### Download from Overleaf

```bash
pyoverleaf download-project "Project Name" /tmp/latest.zip
unzip -o /tmp/latest.zip -d /tmp/latest
cp /tmp/latest/main.tex /path/to/local/main.tex
```

### Upload to Overleaf (Python API recommended)

The CLI `write` command has websocket issues. Use Python API for reliable uploads:

```python
import pyoverleaf

api = pyoverleaf.Api()
api.login_from_browser()

# List projects to get project ID
for proj in api.get_projects():
    print(proj.name, proj.id)

# Upload file (direct overwrite)
project_id = "your_project_id_here"
with open('main.tex', 'rb') as f:
    content = f.read()
root = api.project_get_files(project_id)
api.project_upload_file(project_id, root.id, "main.tex", content)
```

**Why direct overwrite?** This method preserves Overleaf's version history. Users can see exactly what changed via Overleaf's History feature, making it easy to review agent edits and revert if needed.

## Self-hosted Overleaf

```bash
# Via env var
export PYOVERLEAF_HOST=overleaf.mycompany.com
pyoverleaf ls

# Via flag
pyoverleaf --host overleaf.mycompany.com ls
```

## Eason's Workflow Requirements

**When pulling from Overleaf:**
1. Download Overleaf version to `/tmp/`
2. Compare with local version using `diff`
3. Report differences to Eason (summarize what changed)
4. Ask: merge? overwrite local? overwrite Overleaf? or other?
5. Only proceed after Eason confirms

**Push rules (from TOOLS.md):**
- ❌ 禁止自行推送到 Overleaf
- ✅ 只能從 Overleaf 拉到 local
- ⚠️ 推送需要 Eason 明確授權，每次授權只能推一次

## Example

Here's an example of using the Overleaf skill to remove em dashes (a common AI writing artifact) from a paper and push the changes:

![Example: Remove em dashes and push to Overleaf](example-em-dash.jpg)

## Troubleshooting

- **Auth error**: User needs to log into Overleaf in browser first
- **Keychain Access Denied** (macOS): pyoverleaf needs keychain access to read browser cookies. User must run `pyoverleaf ls` in their terminal and click "Always Allow" on the keychain prompt
- **Project not found**: Use exact project name (case-sensitive), check with `pyoverleaf ls`
- **Permission denied**: User may not have edit access to the project

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
