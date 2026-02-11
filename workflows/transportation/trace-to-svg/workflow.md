# trace-to-svg

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/ajmwagar/trace-to-svg/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/ajmwagar/trace-to-svg/SKILL.md)
> Category: Transportation

---

## Description

Trace bitmap images (PNG/JPG/WebP) into clean SVG paths using potrace/mkbitmap. Use to convert logos/silhouettes into vectors for downstream CAD workflows (e.g., create-dxf etch_svg_path) and for turning reference images into manufacturable outlines.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Trace bitmap images (PNG/JPG/WebP) into clean SVG paths using potrace/mkbitmap. Use to convert logos/silhouettes into vectors for downstream CAD workflows (e.g., create-dxf etch_svg_path) and for turning reference images into manufacturable outlines.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run trace-to-svg`)
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
You are executing the trace-to-svg workflow. Use the following context:

Description: Trace bitmap images (PNG/JPG/WebP) into clean SVG paths using potrace/mkbitmap. Use to convert logos/silhouettes into vectors for downstream CAD workflows (e.g., create-dxf etch_svg_path) and for turning reference images into manufacturable outlines.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: trace-to-svg
category: Transportation
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# trace-to-svg

Convert a bitmap into a vector SVG using `mkbitmap` + `potrace`.

## Quick start

```bash
# 1) Produce a silhouette-friendly SVG
bash scripts/trace_to_svg.sh input.png --out out.svg

# 2) Higher contrast + less noise
bash scripts/trace_to_svg.sh input.png --out out.svg --threshold 0.6 --turdsize 20

# 3) Feed into create-dxf (example)
# - set create-dxf drawing.etch_svg_paths[].d to the SVG path `d` you want, or
# - store the traced SVG and reference it in your pipeline.
```

## Notes

- This is best for **logos, silhouettes, high-contrast shapes**.
- For photos or complex shading, results depend heavily on thresholding.
- Output is usually one or more `<path>` elements.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
