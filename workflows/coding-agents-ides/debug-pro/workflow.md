# debug-pro

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/cmanfre7/debug-pro/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/cmanfre7/debug-pro/SKILL.md)
> Category: Coding Agents & IDEs

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
**Trigger:** User-invocable (via `aidarr run debug-pro`)
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
You are executing the debug-pro workflow. Use the following context:

Description: 

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: debug-pro
category: Coding Agents & IDEs
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content

# debug-pro

Systematic debugging methodology and language-specific debugging commands.

## The 7-Step Debugging Protocol

1. **Reproduce** — Get it to fail consistently. Document exact steps, inputs, and environment.
2. **Isolate** — Narrow scope. Comment out code, use binary search, check recent commits with `git bisect`.
3. **Hypothesize** — Form a specific, testable theory about the root cause.
4. **Instrument** — Add targeted logging, breakpoints, or assertions.
5. **Verify** — Confirm root cause. If hypothesis was wrong, return to step 3.
6. **Fix** — Apply the minimal correct fix. Resist the urge to refactor while debugging.
7. **Regression Test** — Write a test that catches this bug. Verify it passes.

## Language-Specific Debugging

### JavaScript / TypeScript
```bash
# Node.js debugger
node --inspect-brk app.js
# Chrome DevTools: chrome://inspect

# Console debugging
console.log(JSON.stringify(obj, null, 2))
console.trace('Call stack here')
console.time('perf'); /* code */ console.timeEnd('perf')

# Memory leaks
node --expose-gc --max-old-space-size=4096 app.js
```

### Python
```bash
# Built-in debugger
python -m pdb script.py

# Breakpoint in code
breakpoint()  # Python 3.7+

# Verbose tracing
python -X tracemalloc script.py

# Profile
python -m cProfile -s cumulative script.py
```

### Swift
```bash
# LLDB debugging
lldb ./MyApp
(lldb) breakpoint set --name main
(lldb) run
(lldb) po myVariable

# Xcode: Product → Profile (Instruments)
```

### CSS / Layout
```css
/* Outline all elements */
* { outline: 1px solid red !important; }

/* Debug specific element */
.debug { background: rgba(255,0,0,0.1) !important; }
```

### Network
```bash
# HTTP debugging
curl -v https://api.example.com/endpoint
curl -w "@curl-format.txt" -o /dev/null -s https://example.com

# DNS
dig example.com
nslookup example.com

# Ports
lsof -i :3000
netstat -tlnp
```

### Git Bisect
```bash
git bisect start
git bisect bad              # Current commit is broken
git bisect good abc1234     # Known good commit
# Git checks out middle commit — test it, then:
git bisect good  # or  git bisect bad
# Repeat until root cause commit is found
git bisect reset
```

## Common Error Patterns

| Error | Likely Cause | Fix |
|-------|-------------|-----|
| `Cannot read property of undefined` | Missing null check or wrong data shape | Add optional chaining (`?.`) or validate data |
| `ENOENT` | File/directory doesn't exist | Check path, create directory, use `existsSync` |
| `CORS error` | Backend missing CORS headers | Add CORS middleware with correct origins |
| `Module not found` | Missing dependency or wrong import path | `npm install`, check tsconfig paths |
| `Hydration mismatch` (React) | Server/client render different HTML | Ensure consistent rendering, use `useEffect` for client-only |
| `Segmentation fault` | Memory corruption, null pointer | Check array bounds, pointer validity |
| `Connection refused` | Service not running on expected port | Check if service is up, verify port/host |
| `Permission denied` | File/network permission issue | Check chmod, firewall, sudo |

## Quick Diagnostic Commands

```bash
# What's using this port?
lsof -i :PORT

# What's this process doing?
ps aux | grep PROCESS

# Watch file changes
fswatch -r ./src

# Disk space
df -h

# System resource usage
top -l 1 | head -10
```

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
