# email-news-digest

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/matthewxfz3/email-news-digest/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/matthewxfz3/email-news-digest/SKILL.md)
> Category: Search & Research

---

## Description

Summarize recent emails, generate a thematic image, and send a formatted HTML email report with the summary and image. Use for daily news digests, project updates, or any email-based reporting that needs visual enhancement and rich formatting.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Summarize recent emails, generate a thematic image, and send a formatted HTML email report with the summary and image. Use for daily news digests, project updates, or any email-based reporting that needs visual enhancement and rich formatting.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run email-news-digest`)
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
You are executing the email-news-digest workflow. Use the following context:

Description: Summarize recent emails, generate a thematic image, and send a formatted HTML email report with the summary and image. Use for daily news digests, project updates, or any email-based reporting that needs visual enhancement and rich formatting.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: email-news-digest
category: Search & Research
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Email News Digest

This skill automates the process of creating an AI-powered news digest from your recent emails, generating a relevant image, and sending a formatted HTML report.

## Usage

To use this skill, run the `process_and_send.sh` script with the required parameters:

```bash
skills/email-news-digest/scripts/process_and_send.sh \
    --recipients "matthewxfz@gmail.com,salonigoel.ssc@gmail.com" \
    --email-query "newer_than:2d subject:news" \
    --image-prompt "A sharp, modern western style image representing AI growth, fierce competition, and diverse applications."
```

### Parameters

*   `--recipients`: Comma-separated list of email addresses to send the digest to.
*   `--email-query`: Gmail search query to filter recent emails (e.g., "newer_than:2d subject:AI"). See [email-filters.md](references/email-filters.md) for more examples.
*   `--image-prompt`: A descriptive prompt for the AI image generation.

## How it Works

1.  **Email Retrieval:** Fetches the most recent email matching your query.
2.  **Content Summarization:** Extracts content and generates a structured summary (TL;DR, main title, and sections) using an internal Python script. (Note: The summarization script currently uses a placeholder summary; future enhancements will integrate a full LLM for dynamic summarization.)
3.  **Image Generation:** Creates a thematic image using the `nano-banana-pro` skill based on your `image-prompt`.
4.  **HTML Report Assembly:** Constructs a dynamic HTML email body using a template, incorporating the summary and a reference to the generated image.
5.  **Email Dispatch:** Sends the formatted HTML email with the image as an attachment using `gog gmail send`, employing a robust Base64 encoding/decoding method to handle complex HTML content safely.

## Summarization Standards

To ensure high-quality output, the summarization process within this skill adheres to the following standards:

*   **Key Insights & Trends:** Prioritize extracting major announcements, significant developments, and overarching trends rather than mere factual recitations.
*   **Conciseness:** The TL;DR should be 3-4 sentences, providing a quick overview. Detailed sections should elaborate succinctly.
*   **Accuracy & Fidelity:** Summaries must faithfully represent the original content without introducing new information or distorting facts.
*   **Clarity & Professionalism:** Use clear, straightforward, and professional language. Avoid jargon where simpler terms suffice.
*   **Bias Neutrality:** Summaries should be objective, presenting information as-is without injecting personal opinions or biases.

## Implementation Standards (Summarization Component)

*   **Modularity:** The summarization logic resides in `scripts/summarize_content.py` to ensure it's self-contained and easily upgradable.
*   **Input/Output:** The script should accept raw email content (or extracted text) as input and output a structured JSON object containing the TL;DR, main title, and markdown-formatted sections.
*   **Future LLM Integration:** The current Python script uses a placeholder. Future development will focus on integrating a robust Large Language Model (LLM) API (e.g., Gemini) to perform dynamic, context-aware summarization based on these standards.

## References

*   [email-filters.md](references/email-filters.md): Provides examples of Gmail search operators.
*   [html-template.html](references/html-template.html): The HTML structure used for the email report.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
