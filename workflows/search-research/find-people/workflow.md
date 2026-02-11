# find-people

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/tzannetosgiannis/find-people/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/tzannetosgiannis/find-people/SKILL.md)
> Category: Search & Research

---

## Description

Open Source Intelligence (OSINT) tool for researching individuals - professional backgrounds, career timelines, due diligence, competitive intelligence, and investor research. Use when users need to research people, verify credentials, or gather professional information. Costs $0.15 USDC per request via x402 protocol on Base network.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Open Source Intelligence (OSINT) tool for researching individuals - professional backgrounds, career timelines, due diligence, competitive intelligence, and investor research. Use when users need to research people, verify credentials, or gather professional information. Costs $0.15 USDC per request via x402 protocol on Base network.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run find-people`)
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
You are executing the find-people workflow. Use the following context:

Description: Open Source Intelligence (OSINT) tool for researching individuals - professional backgrounds, career timelines, due diligence, competitive intelligence, and investor research. Use when users need to research people, verify credentials, or gather professional information. Costs $0.15 USDC per request via x402 protocol on Base network.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: find-people
category: Search & Research
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Find People (OSINT)

Research individuals using Open Source Intelligence gathering and AI-powered analysis.

## Configuration

The private key must be available via one of these methods:

**Option 1: Environment variable**
```bash
export X402_PRIVATE_KEY="0x..."
```

**Option 2: Config file (Recommended)**

The script checks for `x402-config.json` in these locations (in order):
1. Current directory: `./x402-config.json`
2. Home directory: `~/.x402-config.json` ← **Recommended**
3. Working directory: `$PWD/x402-config.json`

Create the config file:
```json
{
  "private_key": "0x1234567890abcdef..."
}
```

**Example (home directory - works for any user):**
```bash
echo '{"private_key": "0x..."}' > ~/.x402-config.json
```

## Usage

Run the research script with a person's name or description:

```bash
scripts/research.sh "<person query>"
```

The script:
- Executes OSINT research with payment handling
- Costs $0.15 USDC per request (Base network)
- Returns comprehensive AI-processed intelligence report

## Examples

**User:** "Find information about the founder of Ethereum"
```bash
scripts/research.sh "Vitalik Buterin Ethereum founder"
```

**User:** "Research the CEO of OpenAI"
```bash
scripts/research.sh "Sam Altman OpenAI CEO"
```

**User:** "Tell me about Elon Musk's career timeline"
```bash
scripts/research.sh "Elon Musk career history"
```

## Capabilities
- Professional background research
- Career timeline verification
- Due diligence on potential hires/partners
- Competitive intelligence on industry leaders
- Investor research on startup founders
- Educational background verification
- Public accomplishments and publications

## Error Handling
- **"Payment failed: Not enough USDC"** → Inform user to top up Base wallet with USDC
- **"X402 private key missing"** → Guide user to configure private key (see Configuration above)
- **Timeout errors** → The API has a 5-minute timeout; comprehensive research may take time

## Use Cases
- **Hiring:** Verify candidate backgrounds and experience
- **Partnerships:** Due diligence on potential business partners
- **Investment:** Research startup founders and leadership teams
- **Competitive Analysis:** Track industry leaders and their moves
- **Journalism:** Background research for interviews or articles

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
