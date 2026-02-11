# native-app-performance

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/steipete/native-app-performance/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/steipete/native-app-performance/SKILL.md)
> Category: CLI Utilities

---

## Description

Native macOS/iOS app performance profiling via xctrace/Time Profiler and CLI-only analysis of Instruments traces. Use when asked to profile, attach, record, or analyze Instruments .trace files, find hotspots, or optimize native app performance without opening Instruments UI.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Native macOS/iOS app performance profiling via xctrace/Time Profiler and CLI-only analysis of Instruments traces. Use when asked to profile, attach, record, or analyze Instruments .trace files, find hotspots, or optimize native app performance without opening Instruments UI.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run native-app-performance`)
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
You are executing the native-app-performance workflow. Use the following context:

Description: Native macOS/iOS app performance profiling via xctrace/Time Profiler and CLI-only analysis of Instruments traces. Use when asked to profile, attach, record, or analyze Instruments .trace files, find hotspots, or optimize native app performance without opening Instruments UI.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: native-app-performance
category: CLI Utilities
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Native App Performance (CLI-only)

Goal: record Time Profiler via `xctrace`, extract samples, symbolicate, and propose hotspots without opening Instruments.

## Quick start (CLI)

1) Record Time Profiler (attach):

```bash
# Start app yourself, then attach
xcrun xctrace record --template 'Time Profiler' --time-limit 90s --output /tmp/App.trace --attach <pid>
```

2) Record Time Profiler (launch):

```bash
xcrun xctrace record --template 'Time Profiler' --time-limit 90s --output /tmp/App.trace --launch -- /path/App.app/Contents/MacOS/App
```

3) Extract time samples:

```bash
scripts/extract_time_samples.py --trace /tmp/App.trace --output /tmp/time-sample.xml
```

4) Get load address for symbolication:

```bash
# While app is running
vmmap <pid> | rg -m1 "__TEXT" -n
```

5) Symbolicate + rank hotspots:

```bash
scripts/top_hotspots.py --samples /tmp/time-sample.xml \
  --binary /path/App.app/Contents/MacOS/App \
  --load-address 0x100000000 --top 30
```

## Workflow notes

- Always confirm you’re profiling the correct binary (local build vs /Applications). Prefer direct binary path for `--launch`.
- Ensure you trigger the slow path during capture (menu open/close, refresh, etc.).
- If stacks are empty, capture longer or avoid idle sections.
- `xcrun xctrace help record` and `xcrun xctrace help export` show correct flags.

## Included scripts

- `scripts/record_time_profiler.sh`: record via attach or launch.
- `scripts/extract_time_samples.py`: export time-sample XML from a trace.
- `scripts/top_hotspots.py`: symbolicate and rank top app frames.

## Gotchas

- ASLR means you must use the runtime `__TEXT` load address from `vmmap`.
- If using a new build, update the `--binary` path; symbols must match the trace.
- CLI-only flow: no need to open Instruments if stacks are symbolicated via `atos`.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
