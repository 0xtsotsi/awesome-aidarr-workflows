



# Gemini YouTube Video Transcript

Create a **verbatim transcript** for a YouTube URL using **Google Gemini**.

**Output format**
- First line: YouTube video title
- Then transcript lines only in the form:

```
Speaker: text
```

**Requirements**
- No time codes
- No extra headings / lists / commentary

## Usage

```bash
python3 {baseDir}/scripts/youtube_transcript.py "https://www.youtube.com/watch?v=..."
```

Options:
- `--out <path>` Write transcript to a specific file (default: auto-named in the workspace `out/` folder).

## Delivery

When chatting: send the resulting transcript as a document/attachment.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
