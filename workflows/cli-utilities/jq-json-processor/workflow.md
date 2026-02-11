# jq-json-processor

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/arnarsson/jq-json-processor/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/arnarsson/jq-json-processor/SKILL.md)
> Category: CLI Utilities

---

## Description

Process, filter, and transform JSON data using jq - the lightweight and flexible command-line JSON processor.

**Homepage:** https://jqlang.github.io/jq/
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Process, filter, and transform JSON data using jq - the lightweight and flexible command-line JSON processor.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run jq-json-processor`)
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
You are executing the jq-json-processor workflow. Use the following context:

Description: Process, filter, and transform JSON data using jq - the lightweight and flexible command-line JSON processor.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: jq-json-processor
category: CLI Utilities
version: 1.0.0
user_invocable: True
homepage: https://jqlang.github.io/jq/
```

---

## Original Skill Content



# jq JSON Processor

Process, filter, and transform JSON data with jq.

## Quick Examples

### Basic filtering
```bash
# Extract a field
echo '{"name":"Alice","age":30}' | jq '.name'
# Output: "Alice"

# Multiple fields
echo '{"name":"Alice","age":30}' | jq '{name: .name, age: .age}'

# Array indexing
echo '[1,2,3,4,5]' | jq '.[2]'
# Output: 3
```

### Working with arrays
```bash
# Map over array
echo '[{"name":"Alice"},{"name":"Bob"}]' | jq '.[].name'
# Output: "Alice" "Bob"

# Filter array
echo '[1,2,3,4,5]' | jq 'map(select(. > 2))'
# Output: [3,4,5]

# Length
echo '[1,2,3]' | jq 'length'
# Output: 3
```

### Common operations
```bash
# Pretty print JSON
cat file.json | jq '.'

# Compact output
cat file.json | jq -c '.'

# Raw output (no quotes)
echo '{"name":"Alice"}' | jq -r '.name'
# Output: Alice

# Sort keys
echo '{"z":1,"a":2}' | jq -S '.'
```

### Advanced filtering
```bash
# Select with conditions
jq '[.[] | select(.age > 25)]' people.json

# Group by
jq 'group_by(.category)' items.json

# Reduce
echo '[1,2,3,4,5]' | jq 'reduce .[] as $item (0; . + $item)'
# Output: 15
```

### Working with files
```bash
# Read from file
jq '.users[0].name' users.json

# Multiple files
jq -s '.[0] * .[1]' file1.json file2.json

# Modify and save
jq '.version = "2.0"' package.json > package.json.tmp && mv package.json.tmp package.json
```

## Common Use Cases

**Extract specific fields from API response:**
```bash
curl -s https://api.github.com/users/octocat | jq '{name: .name, repos: .public_repos, followers: .followers}'
```

**Convert CSV-like data:**
```bash
jq -r '.[] | [.name, .email, .age] | @csv' users.json
```

**Debug API responses:**
```bash
curl -s https://api.example.com/data | jq '.'
```

## Tips

- Use `-r` for raw string output (removes quotes)
- Use `-c` for compact output (single line)
- Use `-S` to sort object keys
- Use `--arg name value` to pass variables
- Pipe multiple jq operations: `jq '.a' | jq '.b'`

## Documentation

Full manual: https://jqlang.github.io/jq/manual/
Interactive tutorial: https://jqplay.org/

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
