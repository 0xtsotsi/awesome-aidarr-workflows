# tootbot

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/behrangsa/tootbot/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/behrangsa/tootbot/SKILL.md)
> Category: Communication

---

## Description

Publish content to Mastodon. Use when you need to post a Mastodon status.

**Homepage:** N/A
**Repository:** N/A
**Version:** 0.5.0

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Publish content to Mastodon. Use when you need to post a Mastodon status.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run tootbot`)
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
You are executing the tootbot workflow. Use the following context:

Description: Publish content to Mastodon. Use when you need to post a Mastodon status.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: tootbot
category: Communication
version: 0.5.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Mastodon Publisher

Publish content to Mastodon. Use when you need to share updates, posts, or media.

## Usage

### Post one or more statuses to Mastodon

Post a new status to Mastodon with Bun:

```bash
bun {baseDir}/scripts/tootbot.js '{"status": "Hello, Mastodon!"}' '{"status": "Goodby, Mastodon!"}'
```

JSON fields

| Name                  | Description                              | Type                                            | Example                                               | Required | Default  |
| --------------------- | ---------------------------------------- | ----------------------------------------------- | ----------------------------------------------------- | -------- | -------- |
| `status`              | The text content of the status           | string                                          | "Hello, World"                                        | yes^1    | N/A      |
| `visibility`          | Sets the visibility of the posted status | `public` or `private` or `unlisted` or `direct` | "private"                                             | no       | "public" |
| `language`            | ISO 639-1 language code for this status  | ISO-639-1 Language Code                         | "en"                                                  | no       |          |
| `scheduledAt`         | Datetime at which to schedule a status   | RFC3339 date time                               | "2029-02-03T15:30:45.000Z"                            | no       |          |
| `quoteApprovalPolicy` | Sets who is allowed to quote the status  | `public` or `followrs` or `nobody`              | "nobody"                                              | no       | "public  |
| `media`               | Media to be attached to the status       | array of `{file, description}` objects          | `{"file": "/path/to/foo.png", "description" : "Foo"}` | no^2     |          |

- ^1 `status` can be ommitted when one or `--media-path` parameters are present
- ^2 one or `media` objects must be present if `status` is ommitted
- ^2 `media.description` is optional

Environment Variables

| Name                    | Description                | Example                   |
| ----------------------- | -------------------------- | ------------------------- |
| `MASTODON_URL`          | Your Mastodon instance URL | `https://mastodon.social` |
| `MASTODON_ACCESS_TOKEN` | Your Mastodon access token | `xAyBzC`                  |

## Examples

- **Post a new status**

  ```bash
  bun {baseDir}/scripts/tootbot.js '{"status": "Hello, Mastodon"}'
  ```

  Read the output and summarize it for the user.

- **Post a scheduled status**

  ```bash
  bun {baseDir}/scripts/tootbot.js '{"status": "Hello, future!", "scheduledAt" : "2030-02-05T13:21:34.000Z"}'
  ```

  Read the output and summarize it for the user.

- **Post a scheduled status with visibility, language, quote approval policy, and a single media attachment**

  ```bash
  bun {baseDir}/scripts/tootbot.js <<EOF
  {
    "status" : "Dorood",
    "visibility" : "public",
    "language" : "fa",
    "scheduledAt" : "2029-02-03T15:30:45.123456789+03:30",
    "quoteApprovalPolicy" : "followers",
    "media" : [
      {
        "file" : "/path/to/media.png",
        "description" : "Nowrooz Pirooz"
      }
    ]
  }
  EOF
  ```

  Read the output and summarize it for the user.

- **Post a new status with media multiple attachments**

  ```bash
  bun {baseDir}/scripts/tootbot.js <<EOF
  {
    "status" : "Edsger W Dijkstra",
    "visibility" : "public",
    "language" : "fa",
    "scheduledAt" : "2029-02-03T15:30:45.123456789+03:30",
    "quoteApprovalPolicy" : "followers",
    "media" : [
      {
        "file" : "/path/to/dijkstra.png",
        "description" : "Portrait"
      },
      {
        "file" : "/path/to/signature.png",
        "description" : "Signature"
      }
    ]
  }
  EOF
  ```

- **Post a new status with media attachments and no status text**

  ```bash
  bun {baseDir}/scripts/tootbot.js <<EOF
  {
    "media" : [
      {
        "file" : "/path/to/flower-1.png",
        "description" : "White Rose"
      },
      {
        "file" : "/path/to/flower-2.png",
        "description" : "Red Rose"
      }
    ]
  }
  EOF
  ```

## Notes

- Requires `bun` to be installed and available in the PATH.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
