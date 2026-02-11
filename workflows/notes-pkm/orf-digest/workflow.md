# orf-digest

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/cpojer/orf/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/cpojer/orf/SKILL.md)
> Category: Notes & PKM

---

## Description

On-demand ORF news digest in German. Use when the user says 'orf', 'pull orf', or 'orf 10'. Focus on Austrian politics (Inland) and international politics (Ausland) + major headlines; exclude sports. Send each item as its own message (Title + Age + Link). Then generate a Nano Banana image in a cartoon ZiB studio with the anchor presenting the news, plus subtle Easter eggs based on the selected stories.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
On-demand ORF news digest in German. Use when the user says 'orf', 'pull orf', or 'orf 10'. Focus on Austrian politics (Inland) and international politics (Ausland) + major headlines; exclude sports. Send each item as its own message (Title + Age + Link). Then generate a Nano Banana image in a cartoon ZiB studio with the anchor presenting the news, plus subtle Easter eggs based on the selected stories.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run orf-digest`)
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
You are executing the orf-digest workflow. Use the following context:

Description: On-demand ORF news digest in German. Use when the user says 'orf', 'pull orf', or 'orf 10'. Focus on Austrian politics (Inland) and international politics (Ausland) + major headlines; exclude sports. Send each item as its own message (Title + Age + Link). Then generate a Nano Banana image in a cartoon ZiB studio with the anchor presenting the news, plus subtle Easter eggs based on the selected stories.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: orf-digest
category: Notes & PKM
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# ORF Digest (news.orf.at)

## Command format

Interpret a user message that starts with `orf` as a request for an ORF News digest.

Supported forms:

- `orf` → default 5 items
- `orf <n>` → n items (max 15)
- `orf inland` / `orf ausland` → bias selection
- `orf <n> inland|ausland` → both

## Source + scope

- Primary source: `news.orf.at` (German)
- Prefer: **Inland** politics, **Ausland** / international politics, and major headlines.
- Exclude: sports (Sport).

## Output requirements

- Do **not** send any extra commentary/preamble/epilogue.
- Send results as **individual messages**.
- Each item message must be exactly:
  - first line: the headline (German)
  - second line: `<age>` (e.g. `45m ago`, `6h ago`, `2d ago`)
  - third line: the ORF link
- After the item messages, send **one final message** with the generated image.
  - The image must visually incorporate the pulled news on the wraparound studio video wall using **4–6 distinct story panels**.
  - **Panel layout (must):**
    - TOP: big bold text (1–2 words, ALL CAPS). You must invent this.
    - MIDDLE: smaller text (3–6 words) that describes the story. You must invent this.
      - The two lines must **not** form a connected sentence.
      - Avoid repeating the same words between the two lines.
    - BOTTOM: exactly 1–2 simple icons (no maps, no busy collages)
    - **Icon variety:** make icons distinct across panels whenever possible.
      - Do not reuse the same icon pair across multiple panels.
      - Avoid overusing generic icons (e.g. globe + pin); only use them when no better match exists.
  - **Readability:** keep text minimal and large enough to render cleanly.
  - No logos/watermarks.
  - If the chat provider requires non-empty text for media, use a minimal caption `.`.

## Procedure

1. Parse `n` and optional `focus` (`inland`|`ausland`) from the user message.
2. Run `python3 skills/orf-digest/scripts/orf.py --count <n> --focus <focus> --format json`.
3. Send each returned item as its own message (3-line format).
4. Generate the ZiB studio mood image via Nano Banana:
   - Build prompt from items: `python3 skills/orf-digest/scripts/orf.py --count <n> --focus <focus> --format json | node skills/orf-digest/scripts/zib_prompt.mjs`
   - Generate: `skills/orf-digest/scripts/generate_zib_nano_banana.sh ./tmp/orf-zib/zib.png`
   - Send image as final message.

If fetching/parsing fails or returns 0 items:
- Use the browser tool to open `https://news.orf.at/`, pick N non-sport headlines by judgment, and send them in the same 3-line format.
- Still generate a ZiB studio image with a few generic political-news Easter eggs.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
