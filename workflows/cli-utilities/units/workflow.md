# units

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/asleep123/units/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/asleep123/units/SKILL.md)
> Category: CLI Utilities

---

## Description

Perform unit conversions and calculations using GNU Units.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Perform unit conversions and calculations using GNU Units.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run units`)
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
You are executing the units workflow. Use the following context:

Description: Perform unit conversions and calculations using GNU Units.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: units
category: CLI Utilities
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# GNU Units Skill

Use GNU `units` to perform unit conversions and calculations via the command line. Can be installed using brew and apt under "units".

## Usage

Use the `bash` tool to run the `units` command. Use the `-t` (terse) flag to get just the numeric result.

```bash
units -t 'from-unit' 'to-unit'
```

### Examples

**Basic Conversion:**
```bash
units -t '10 kg' 'lbs'
# Output: 22.046226
```

**Compound Units:**
```bash
units -t '60 miles/hour' 'm/s'
# Output: 26.8224
```

**Temperature (Non-linear):**
Temperature requires specific syntax: `tempF(x)`, `tempC(x)`, `tempK(x)`.
```bash
units -t 'tempF(98.6)' 'tempC'
# Output: 37
```

**Time:**
```bash
units -t '2 weeks' 'seconds'
```

**Rounding Output:**
To round to specific decimal places (e.g. 3 places), use `-o "%.3f"`:
```bash
units -t -o "%.3f" '10 kg' 'lbs'
# Output: 22.046
```

**Definition Lookup:**
To see what a unit definition is (without converting), omit the second argument (without `-t` is more verbose/useful for definitions):
```bash
units '1 acre'
```

## Notes

- **Currency:** `units` supports currency (USD, EUR, etc.), but exchange rates may be out of date as they are static in the definitions file.
- **Safety:** Always quote your units to prevent shell expansion issues (e.g. `units -t '1/2 inch' 'mm'`).

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
