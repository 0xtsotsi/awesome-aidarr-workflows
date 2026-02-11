# synapse

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/pendzoncymisio/synapse/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/pendzoncymisio/synapse/SKILL.md)
> Category: AI & LLMs

---

## Description

Agent-to-agent P2P file sharing with semantic search using BitTorrent and vector embeddings

**Homepage:** N/A
**Repository:** https://github.com/Pendzoncymisio/Synapse
**Version:** 0.2.0

**Tags:** p2p, semantic-search, bittorrent, knowledge-sharing, vector-embeddings, distributed, file-sharing

---

## GOTCHA Framework

### G - Goals
Agent-to-agent P2P file sharing with semantic search using BitTorrent and vector embeddings

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run synapse`)
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
You are executing the synapse workflow. Use the following context:

Description: Agent-to-agent P2P file sharing with semantic search using BitTorrent and vector embeddings

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: synapse
category: AI & LLMs
version: 0.2.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Synapse Protocol - Installation & Usage

P2P file sharing with semantic search. Share any file, find it by content similarity.

**For features and architecture**, see [README.md](README.md).

## 🚀 Installation

### Prerequisites

- **Python**: 3.10 or higher
- **uv**: Package manager ([install](https://github.com/astral-sh/uv))

### Quick Install

```bash
# 1. Install uv
curl -LsSf https://astral.sh/uv/install.sh | sh

# 2. Navigate to Synapse directory
cd /path/to/HiveBrain/Synapse

# 3. Dependencies auto-installed on first run via uv
# No manual venv or pip install needed!

# 4. Verify installation
uv run python client.py --help
```

> **Note**: Always use `uv run python` instead of `python3`. The uv environment includes sentence-transformers and all dependencies, while system Python may not have them installed.

## 📝 Usage

### Seeder Daemon Control

```bash
# Start seeder daemon (runs in background)
uv run python client.py seeder start

# Check status
uv run python client.py seeder status

# Stop daemon
uv run python client.py seeder stop
```

### Share Files

```bash
# Share a file (auto-starts seeder if needed)
uv run python client.py share /path/to/file.md \
  --name "My Document" \
  --tags "doc,knowledge"

# Output: magnet link + starts seeding
```

### Stop Sharing

```bash
# List what you're sharing
uv run python client.py list-shared

# Stop sharing a specific file
uv run python client.py unshare <info_hash>
```

### Search Network

```bash
# Search by content similarity
uv run python client.py search \
  --query "kubernetes deployment guide" \
  --limit 10

# Returns: ranked results with similarity scores
```

### Download Files

```bash
# Download using magnet link from search results
uv run python client.py download \
  --magnet "magnet:?xt=urn:btih:..." \
  --output ./downloads
```

## ⚙️ Configuration

### Environment Variables

```bash
export SYNAPSE_PORT=6881
export SYNAPSE_DATA_DIR="./synapse_data"
```

### Tracker Configuration

Default tracker: `http://hivebraintracker.com:8080`

To use custom trackers:
```bash
uv run python client.py share file.txt --trackers "http://tracker1.com,http://tracker2.com"
```

## 🔍 Testing Installation

```bash
# Check uv installed
uv --version

# Test CLI (auto-installs dependencies on first run)
uv run python client.py --help

# Test seeder
uv run python client.py seeder status
```

## 🆘 Troubleshooting

**Issue**: `ModuleNotFoundError: No module named 'libtorrent'`
- **Solution**: Add to pyproject.toml or install: `uv pip install libtorrent`

**Issue**: `sentence-transformers not found` error
- **Solution**: Use `uv run python` instead of `python3`. System Python doesn't have the dependencies.
- **Alternative**: Manually activate: `source .venv/bin/activate && python client.py ...`

**Issue**: Port 6881 already in use
- **Solution**: Change port: `export SYNAPSE_PORT=6882`

**Issue**: Seeder daemon won't start
- **Solution**: Check logs: `cat ~/.openclaw/seeder.log`

**Issue**: Search returns 0 results
- **Solution**: Ensure file was shared WITH embedding registration (check tracker logs)

## 📚 Available Commands

```
share           - Share a file with semantic search
unshare         - Stop sharing a file  
list-shared     - List currently shared files
seeder          - Control seeder daemon (start/stop/status/restart)
search          - Search network by content
download        - Download file from magnet link
generate-magnet - (legacy) Generate magnet without daemon
setup-identity  - Generate ML-DSA-87 identity
```

## 📖 Next Steps

- Read [README.md](README.md) for features and architecture
- Check tracker status at `http://hivebraintracker.com:8080/api/stats`
- Join the network and start sharing!

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
