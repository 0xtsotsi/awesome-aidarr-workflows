# project-tree

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/lachlanglasgow/project-tree/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/lachlanglasgow/project-tree/SKILL.md)
> Category: Notes & PKM

---

## Description

Generate a visual directory tree of the ~/projects folder and update MEMORY.md with the result. Use when the user wants to view, update, or generate a project tree structure, or when they mention "project tree", "tree view", "folder structure", or "show me my projects".

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Generate a visual directory tree of the ~/projects folder and update MEMORY.md with the result. Use when the user wants to view, update, or generate a project tree structure, or when they mention "project tree", "tree view", "folder structure", or "show me my projects".

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run project-tree`)
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
You are executing the project-tree workflow. Use the following context:

Description: Generate a visual directory tree of the ~/projects folder and update MEMORY.md with the result. Use when the user wants to view, update, or generate a project tree structure, or when they mention "project tree", "tree view", "folder structure", or "show me my projects".

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: project-tree
category: Notes & PKM
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Project Tree

## Overview

Generate a visual tree structure of the ~/projects directory and automatically update MEMORY.md with the current project organization. The tree shows folders and .md files only, with smart grouping for consecutive numbered items.

## Usage

Run the tree generation script:

```bash
node ~/clawd/skills/project-tree/scripts/project-tree.js
```

Or use the convenience wrapper:

```bash
~/clawd/scripts/update-tree
```

## Features

- **Folder-only + .md files**: Only displays directories and markdown files, hiding code files and dependencies
- **Smart grouping**: Detects consecutive numbered sequences (e.g., `script1-video`, `script2-video`...) and collapses them into `script[1-28]-video/ (28 items)`
- **Auto-updates MEMORY.md**: The tree is automatically inserted into the PROJECT_TREE section of MEMORY.md
- **Configurable depth**: Default is 3 levels deep (adjustable in script)

## Configuration

Edit these values in `scripts/project-tree.js`:

- `MAX_DEPTH`: Number of directory levels to display (default: 3)
- `EXCLUDE_DIRS`: Directories to skip (node_modules, .git, etc.)
- `ROOT_DIR`: Base directory to scan (default: ~/projects)

## Automation (Hook)

You can automate project tree updates to run on every session `/reset`.

### 1. Enable Internal Hooks

Add to your `clawdbot.json`:

```json
{
  "hooks": {
    "internal": {
      "enabled": true
    }
  }
}
```

### 2. Create the Hook

Create `~/.clawdbot/hooks/reset-project-tree/HOOK.md`:

```markdown
---
name: reset-project-tree
description: "Generate project tree on session reset"
metadata: {"clawdbot":{"emoji":"🌳","events":["command:reset"],"requires":{"bins":["node"]}}}
---

Generates project tree when /reset is issued.
```

Create `~/.clawdbot/hooks/reset-project-tree/handler.ts`:

```typescript
import { execSync } from 'child_process';
import type { HookHandler } from '../../../src/hooks/hooks.js';

const handler: HookHandler = async (event) => {
  if (event.type !== 'command' || event.action !== 'reset') return;

  try {
    const scriptPath = `${event.context.workspaceDir}/skills/project-tree/scripts/project-tree.js`;
    execSync(`node ${scriptPath}`, { cwd: event.context.workspaceDir, stdio: 'pipe' });
    console.log('[reset-project-tree] Updated');
  } catch (err) {
    console.error('[reset-project-tree] Failed:', err instanceof Error ? err.message : String(err));
  }
};

export default handler;
```

### 3. Enable and Restart

```bash
clawdbot hooks enable reset-project-tree
clawdbot gateway restart
```

## Resources

### scripts/

- `project-tree.js` - Main tree generation script with smart grouping logic

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
