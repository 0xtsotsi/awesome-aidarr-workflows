# gitai-skill

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/leandrosilvaferreira/gitai-skill/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/leandrosilvaferreira/gitai-skill/SKILL.md)
> Category: AI & LLMs

---

## Description

Boost developer productivity with Gitai: An AI-powered Git automation tool that analyzes code changes and generates semantic Conventional Commits instantly. Supports Node.js, Python, Java, Go, PHP, and more. Compatible with OpenAI, Anthropic, and Groq.

**Homepage:** N/A
**Repository:** N/A
**Version:** 1.0.0

**Tags:** git, automation, ai, commit, conventional-commits, workflow, productivity, dev-tools, openai, anthropic, groq, llm

---

## GOTCHA Framework

### G - Goals
Boost developer productivity with Gitai: An AI-powered Git automation tool that analyzes code changes and generates semantic Conventional Commits instantly. Supports Node.js, Python, Java, Go, PHP, and more. Compatible with OpenAI, Anthropic, and Groq.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run gitai-skill`)
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
You are executing the gitai-skill workflow. Use the following context:

Description: Boost developer productivity with Gitai: An AI-powered Git automation tool that analyzes code changes and generates semantic Conventional Commits instantly. Supports Node.js, Python, Java, Go, PHP, and more. Compatible with OpenAI, Anthropic, and Groq.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: gitai-skill
category: AI & LLMs
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Gitai Automation - AI-Powered Git Workflow

> **Transform your development workflow with intelligent, automated commit management.**

Gitai analyzes your code changes to generate precise, descriptive commit messages following the **Conventional Commits** standard. It eliminates the friction of writing commit messages, ensuring a clean, semantic, and professional git history automatically.

**Key capabilities:**
-   **Universal Language Support**: Analyzes Node.js, Python, Java, Go, PHP, and more.
-   **Multi-LLM Support**: Choose your preferred AI brain—OpenAI (GPT), Anthropic (Claude), or Groq.
-   **Workflow Automation**: Stages, commits, and pushes changes in a single command.
-   **Standardized History**: Enforces consistency across your project's version history.

---

## 📦 Prerequisites (MANDATORY)

This skill requires the `@notyped/gitai` CLI tool to be installed and configured on the system **BEFORE** the agent can operate.

**The AGENT MUST NOT attempt to install this package or configure it.**

1.  **CHECK** if `gitai` is available:
    ```bash
    command -v gitai
    ```
2.  **IF MISSING**, STOP immediately and inform the user:
    > "The `gitai` CLI tool is not installed. Please install it globally (e.g., `npm install -g @notyped/gitai`) and configure it before using this skill."
    
3.  **CHECK** if `~/.gitai` exists.
4.  **IF MISSING**, STOP immediately and inform the user:
    > "The `gitai` tool is installed but not configured. Please run `gitai` in your terminal to complete the setup."

5.  **ONLY PROCEED** if both checks pass.

## 🚀 Usage & Workflows

### Command Structure
Based on `gitai --help`:
```bash
gitai [options] [projectPath] [baseMessage]
```

**Arguments:**
- `projectPath`: The path to the project (default: ".").
- `baseMessage`: The base commit message (Optional).

**Options:**
- `-p, --push`: Whether to push after committing (default: false).
- `-V, --version`: Output the version number.
- `-h, --help`: Display help for command.

### Standard Workflows

| Command | Action Description |
|---------|--------------------|
| `gitai . ''` | Analyzes current folder, Generates message and commits |
| `gitai . '' --push` | Analyzes current folder, Generates message, commits, AND pushes to remote |
| `gitai ./frontend 'ui update'` | Analyzes only the `./frontend` directory, Generates message and commits |

### Verification
Check which version of Gitai is currently active:
```bash
gitai --version
```



---

## ⚠️ Troubleshooting

-   **Interactive Wizard Hangs**: If `gitai` hangs waiting for input, it means `~/.gitai` is missing or invalid. create the file manually as described in Step 2.
-   **Node Version Error**: Ensure Node.js 18+ is active (`node -v`).
-   **API Errors**: Check the `API_KEY` in `~/.gitai`.

---

## Links
- **GitHub**: [https://github.com/leandrosilvaferreira/gitai-skill](https://github.com/leandrosilvaferreira/gitai-skill)
- **Issues**: [https://github.com/leandrosilvaferreira/gitai-skill/issues](https://github.com/leandrosilvaferreira/gitai-skill/issues)

## Author
- **Leandro Zuck**
- **GitHub**: [https://github.com/leandrosilvaferreira](https://github.com/leandrosilvaferreira)
- **Email**: leandrosilvaferreira@gmail.com

## License
MIT

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
