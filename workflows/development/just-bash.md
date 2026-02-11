# Just Bash - Sandboxed Bash for AI Agents

**Source:** Vercel Labs → AiDarr GOTCHA Conversion
**Original:** https://github.com/vercel-labs/just-bash
**Converted:** 2026-02-11

---

## Description

A simulated bash environment with an in-memory virtual filesystem, written in TypeScript. Designed for AI agents that need a secure, sandboxed bash environment.

Supports optional network access via `curl` with secure-by-default URL filtering.

**Key Benefits:**
- **Safe Execution**: No real disk access by default
- **Execution Protection**: Guards against infinite loops
- **Network Control**: Optional curl with URL allow-lists
- **Multiple Filesystem Modes**: InMemory, Overlay, ReadWrite, Mountable
- **AI-Optimized**: Ready-to-use AI SDK tool integration

---

## Goals (Usage Guide)

### Installation

```bash
npm install just-bash
```

For AI SDK integration:
```bash
npm install bash-tool
```

### Security Model

- Shell only has access to the provided file system
- Execution protected against infinite loops/recursion
- No network access by default
- Network access requires URL prefix allow-lists
- No binary/WASM support (use Vercel Sandbox for full VM)

### Basic API Usage

```typescript
import { Bash } from "just-bash";

const env = new Bash();
await env.exec('echo "Hello" > greeting.txt');
const result = await env.exec("cat greeting.txt");
console.log(result.stdout); // "Hello\n"
console.log(result.exitCode); // 0
```

**Each `exec()` is isolated**—env vars, functions, and cwd don't persist across calls (filesystem does).

### Configuration Options

```typescript
const env = new Bash({
  files: { "/data/file.txt": "content" },  // Initial files
  env: { MY_VAR: "value" },                 // Initial environment
  cwd: "/app",                              // Starting directory
  executionLimits: { maxCallDepth: 50 },    // Execution protection
});
```

### Filesystem Options

#### InMemoryFs (Default)
Pure in-memory, no disk access:
```typescript
const env = new Bash();
```

#### OverlayFs
Copy-on-write over real directory. Reads from disk, writes to memory:
```typescript
import { OverlayFs } from "just-bash/fs/overlay-fs";

const overlay = new OverlayFs({ root: "/path/to/project" });
const env = new Bash({ fs: overlay, cwd: overlay.getMountPoint() });

await env.exec("cat package.json"); // reads from disk
await env.exec('echo "modified" > package.json'); // stays in memory
```

#### ReadWriteFs
Direct read-write access to real directory:
```typescript
import { ReadWriteFs } from "just-bash/fs/read-write-fs";

const rwfs = new ReadWriteFs({ root: "/path/to/sandbox" });
const env = new Bash({ fs: rwfs });
```

#### MountableFs
Mount multiple filesystems at different paths:
```typescript
import { Bash, MountableFs, InMemoryFs } from "just-bash";
import { OverlayFs } from "just-bash/fs/overlay-fs";
import { ReadWriteFs } from "just-bash/fs/read-write-fs";

const fs = new MountableFs({ base: new InMemoryFs() });

// Mount read-only knowledge base
fs.mount("/mnt/knowledge", new OverlayFs({ root: "/path/to/knowledge", readOnly: true }));

// Mount read-write workspace
fs.mount("/home/agent", new ReadWriteFs({ root: "/path/to/workspace" }));

const bash = new Bash({ fs, cwd: "/home/agent" });
```

### AI SDK Tool Integration

For AI agents, use `bash-tool`:

```bash
npm install bash-tool
```

```typescript
import { createBashTool } from "bash-tool";
import { generateText } from "ai";

const bashTool = createBashTool({
  files: { "/data/users.json": '[{"name": "Alice"}, {"name": "Bob"}]' },
});

const result = await generateText({
  model: "anthropic/claude-sonnet-4",
  tools: { bash: bashTool },
  prompt: "Count the users in /data/users.json",
});
```

### Custom Commands

Extend just-bash with TypeScript commands:

```typescript
import { Bash, defineCommand } from "just-bash";

const hello = defineCommand("hello", async (args, ctx) => {
  const name = args[0] || "world";
  return { stdout: `Hello, ${name}!\n`, stderr: "", exitCode: 0 };
});

const bash = new Bash({ customCommands: [hello] });
await bash.exec("hello Alice"); // "Hello, Alice!\n"
```

### Network Access

Disabled by default. Enable with URL filtering:

```typescript
// Allow specific URLs with GET/HEAD only (safest)
const env = new Bash({
  network: {
    allowedUrlPrefixes: [
      "https://api.github.com/repos/myorg/",
      "https://api.example.com",
    ],
  },
});

// Allow specific URLs with additional methods
const env = new Bash({
  network: {
    allowedUrlPrefixes: ["https://api.example.com"],
    allowedMethods: ["GET", "HEAD", "POST"],
  },
});

// Allow all URLs (use with caution)
const env = new Bash({
  network: { dangerouslyAllowFullInternetAccess: true },
});
```

### CLI Binary

```bash
npm install -g just-bash
```

```bash
# Execute inline script
just-bash -c 'ls -la && cat package.json | head -5'

# Execute with specific project root
just-bash -c 'grep -r "TODO" src/' --root /path/to/project

# Get JSON output
just-bash -c 'echo hello' --json
```

### Execution Protection

```typescript
const env = new Bash({
  executionLimits: {
    maxCallDepth: 100,        // Max function recursion depth
    maxCommandCount: 10000,   // Max total commands executed
    maxLoopIterations: 10000, // Max iterations per loop
    maxAwkIterations: 10000,  // Max iterations in awk programs
    maxSedIterations: 10000,  // Max iterations in sed scripts
  },
});
```

### Supported Commands

**File Operations:** cat, cp, file, ln, ls, mkdir, mv, rm, rmdir, stat, touch, tree

**Text Processing:** awk, base64, column, comm, cut, diff, grep, head, join, md5sum, sed, sort, tail, tr, uniq, wc

**Data Processing:** jq (JSON), python3 (Pyodide), sqlite3 (WASM), xan (CSV), yq (YAML/XML/TOML/CSV)

**Compression:** gzip, gunzip, tar

**Navigation:** basename, cd, dirname, du, echo, env, find, pwd, which, whoami

**Network:** curl, html-to-markdown (when network enabled)

**Shell Features:** Pipes, redirections, variables, glob patterns, if/then/else, functions, loops

---

## Orchestration

**When to use just-bash:**

1. **Safe Code Exploration** - Let agents explore codebases without risk of modification
2. **Workflow Testing** - Test workflows in isolation before real execution
3. **Educational Environments** - Teaching bash without real filesystem risks
4. **CI/CD Simulation** - Test scripts in a controlled environment
5. **Browser-Based Tools** - Can run in browser environments

**When NOT to use:**

- Need to run real binaries (node, python, custom executables)
- Require full system access
- Need persistent state across exec calls
- Running untrusted code from external sources

---

## Tools

just-bash includes these built-in tools:

| Category | Commands |
|----------|----------|
| File | cat, cp, ln, ls, mkdir, mv, rm, touch, tree |
| Text | grep, sed, awk, head, tail, sort, uniq, wc |
| Data | jq, python3, sqlite3, xan, yq |
| Archive | tar, gzip |
| Network | curl (when enabled) |

---

## Context

**Use Cases for AiDarr:**

1. **Sandboxed Bash Tool** - Add a "safe mode" to Pocket Agent's Bash tool
2. **Code Analysis** - Let agents explore codebases safely
3. **Pre-flight Checks** - Test commands before real execution
4. **Training Simulations** - Practice workflows without real consequences

**Related Projects:**
- [bash-tool](https://github.com/vercel-labs/bash-tool) - AI SDK integration
- [@vercel/sandbox](https://vercel.com/docs/vercel-sandbox) - Full VM sandbox

---

## Hard Prompts

**System Prompt for AI Agents:**

```
You are working with just-bash, a sandboxed bash environment for AI agents.

Key constraints:
- All filesystem operations are in-memory (unless configured otherwise)
- Each exec() call is isolated (filesystem persists, env vars do not)
- Network access requires pre-approved URL allow-lists
- Execution is protected against infinite loops

Best practices:
- Read files completely before modifying
- Use OverlayFs for safe code exploration
- Enable network only with specific URL allow-lists
- Test commands in sandbox before real execution

When you need real disk access, use ReadWriteFs or real bash.
When you need full VM capabilities, use Vercel Sandbox instead.
```

---

## Args

**Configuration Options:**

```yaml
# Filesystem mode
filesystem_mode: "InMemoryFs"  # Options: InMemoryFs, OverlayFs, ReadWriteFs, MountableFs

# Network access
network:
  enabled: false
  allowed_urls: []
  allowed_methods: ["GET", "HEAD"]

# Execution limits
execution_limits:
  max_call_depth: 100
  max_command_count: 10000
  max_loop_iterations: 10000

# Working directory
cwd: "/home/user"

# Initial files
files: {}
```

**Runtime Parameters:**

```yaml
# Per-exec overrides
env: {}
timeout: 300
cwd: null
```

---

## Metadata

**Conversion Notes:**
- Converted from Vercel Labs just-bash repository
- TypeScript/JavaScript library for Node.js and browser
- Apache-2.0 licensed
- 572+ GitHub stars

**Category:** Development Tools
**Tags:** bash, sandbox, security, typescript, ai-agents, filesystem

**Repository:** https://github.com/vercel-labs/just-bash
**Documentation:** https://justbash.dev/

**Use in AiDarr:**
- Safe bash alternative for risky operations
- Code exploration without modification
- Workflow testing environment
- Educational tool for bash scripting
