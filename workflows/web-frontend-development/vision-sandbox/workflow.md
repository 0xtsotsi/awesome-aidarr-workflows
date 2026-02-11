# vision-sandbox

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/johanesalxd/vision-sandbox/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/johanesalxd/vision-sandbox/SKILL.md)
> Category: Web & Frontend Development

---

## Description

Agentic Vision via Gemini's native Code Execution sandbox. Use for spatial grounding, visual math, and UI auditing.

**Homepage:** N/A
**Repository:** N/A
**Version:** 1.1.0

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Agentic Vision via Gemini's native Code Execution sandbox. Use for spatial grounding, visual math, and UI auditing.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run vision-sandbox`)
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
You are executing the vision-sandbox workflow. Use the following context:

Description: Agentic Vision via Gemini's native Code Execution sandbox. Use for spatial grounding, visual math, and UI auditing.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: vision-sandbox
category: Web & Frontend Development
version: 1.1.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Vision Sandbox 🔭

Leverage Gemini's native code execution to analyze images with high precision. The model writes and runs Python code in a Google-hosted sandbox to verify visual data, perfect for UI auditing, spatial grounding, and visual reasoning.

## Installation

```bash
clawhub install vision-sandbox
```

## Usage

```bash
uv run vision-sandbox --image "path/to/image.png" --prompt "Identify all buttons and provide [x, y] coordinates."
```

## Pattern Library

### 📍 Spatial Grounding
Ask the model to find specific items and return coordinates.
* **Prompt:** "Locate the 'Submit' button in this screenshot. Use code execution to verify its center point and return the [x, y] coordinates in a [0, 1000] scale."

### 🧮 Visual Math
Ask the model to count or calculate based on the image.
* **Prompt:** "Count the number of items in the list. Use Python to sum their values if prices are visible."

### 🖥️ UI Audit
Check layout and readability.
* **Prompt:** "Check if the header text overlaps with any icons. Use the sandbox to calculate the bounding box intersections."

### 🖐️ Counting & Logic
Solve visual counting tasks with code verification.
* **Prompt:** "Count the number of fingers on this hand. Use code execution to identify the bounding box for each finger and return the total count."

## Integration with OpenCode
This skill is designed to provide **Visual Grounding** for automated coding agents like OpenCode.
- **Step 1:** Use `vision-sandbox` to extract UI metadata (coordinates, sizes, colors).
- **Step 2:** Pass the JSON output to OpenCode to generate or fix CSS/HTML.

## Configuration
- **GEMINI_API_KEY**: Required environment variable.
- **Model**: Defaults to `gemini-3-flash-preview`.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
