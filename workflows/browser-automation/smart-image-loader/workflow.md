# smart-image-loader

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/tingwei1123/smart-image-loader/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/tingwei1123/smart-image-loader/SKILL.md)
> Category: Browser & Automation

---

## Description

Smart image loader that handles both URLs and local files, automatically downloads URLs to temporary locations, and displays images using the read tool. Use when a user wants to view or display an image, whether it's a web URL or a file in the workspace.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Smart image loader that handles both URLs and local files, automatically downloads URLs to temporary locations, and displays images using the read tool. Use when a user wants to view or display an image, whether it's a web URL or a file in the workspace.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run smart-image-loader`)
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
You are executing the smart-image-loader workflow. Use the following context:

Description: Smart image loader that handles both URLs and local files, automatically downloads URLs to temporary locations, and displays images using the read tool. Use when a user wants to view or display an image, whether it's a web URL or a file in the workspace.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: smart-image-loader
category: Browser & Automation
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Smart Image Loader

## Quick Start

When a user asks to display an image:

1. **Check if input is a URL or local path**
   - URLs start with `http://` or `https://`
   - Local paths are file paths in the workspace

2. **For URLs:**
   - Download the image to a temporary location using the Python script
   - Use `read` tool to display the image
   - Clean up the temporary file afterward

3. **For local files:**
   - Verify the file exists (relative to workspace or absolute path)
   - Use `read` tool directly to display the image

## Usage Examples

**User says:** "Show me this image: https://example.com/photo.jpg"

1. Run: `python3 scripts/smart_image_loader.py https://example.com/photo.jpg`
2. Script downloads to temp: `/tmp/dir/photo.jpg`
3. Use `read` tool on: `/tmp/dir/photo.jpg`
4. Clean up: Delete the temp file

**User says:** "Display ./images/logo.png"

1. Run: `python3 scripts/smart_image_loader.py ./images/logo.png`
2. Script verifies file exists
3. Use `read` tool on: `/home/node/clawd/images/logo.png` (absolute path)

## Script Usage

```bash
python3 scripts/smart_image_loader.py <image_path_or_url>
```

### Arguments

| Argument | Description |
|----------|-------------|
| `image_path_or_url` | Either a local file path (relative or absolute) or a URL |

### Output Format

The script returns a JSON-like output with:
- `Status`: SUCCESS or FAILED
- `Type`: url or local
- `File Path`: Local path for the `read` tool
- `Message`: Status description
- `Cleanup Needed`: true if temp file should be deleted

### Examples

```bash
# URL example
python3 scripts/smart_image_loader.py https://example.com/image.jpg
# Output: Downloads to /tmp/xyz/image.jpg, use read tool on that path

# Local file example (relative)
python3 scripts/smart_image_loader.py ./photos/vacation.jpg
# Output: File found at /home/node/clawd/photos/vacation.jpg

# Local file example (absolute)
python3 scripts/smart_image_loader.py /home/node/clawd/downloads/graphic.png
# Output: File found at /home/node/clawd/downloads/graphic.png
```

## Workflow Decision Tree

```
User asks to display an image
         |
         v
    Is it a URL? (http:// or https://)
         |
    +----+---------------------------+
    |                                 |
   YES                               NO
    |                                 |
    v                                 v
Download to temp              Does file exist?
    |                                 |
    v                          +-----+-----+
Use read tool                 |           |
    |                        YES          NO
    v                              |
Cleanup temp file              v
                           Use read tool
                               |
                               v
                          Done (no cleanup)
```

## Cleanup Guidelines

- **URL downloads**: Always clean up temporary files after displaying
- **Local files**: No cleanup needed (files remain in workspace)
- Use `exec` with `rm <file_path>` for cleanup

## Image Formats Supported

- JPEG (.jpg, .jpeg)
- PNG (.png)
- GIF (.gif)
- WebP (.webp)
- BMP (.bmp)

## Error Handling

| Scenario | Action |
|----------|--------|
| URL download fails | Report error to user |
| Local file not found | Report error to user |
| Invalid input | Show usage instructions |
---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
