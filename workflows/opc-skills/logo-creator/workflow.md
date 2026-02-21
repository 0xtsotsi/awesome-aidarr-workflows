# Logo Creator Workflow

**Status:** Active
**Date:** 2026-02-21
**Use Case:** Create professional logos through AI image generation
**Source:** Adapted from OPC Skills (resciencelab/opc-skills)

## Overview

Create professional logos through AI image generation with an iterative design process, including background removal and SVG export.

## ATLAS Alignment

| ATLAS Phase | Workflow Step |
|-------------|---------------|
| Architect | Gather requirements (style, colors, ratio) |
| Trace | Check existing brand assets |
| Link | Connect to nanobanana for generation |
| Assemble | Generate variations, iterate with user |
| Stress-test | Crop, remove background, vectorize |

## Trigger

This workflow is invoked when user mentions:
- Logo, icon, favicon, brand mark
- Mascot, emblem, design a logo

## Prerequisites

**Required API Keys:**
- `GEMINI_API_KEY` - Get from [Google AI Studio](https://aistudio.google.com/apikey)
- `REMOVE_BG_API_KEY` - Get from [remove.bg](https://www.remove.bg/api)
- `RECRAFT_API_KEY` - Get from [recraft.ai](https://www.recraft.ai/)

**Required Skills:**
- `nanobanana` - AI image generation

## Output Location

```
.skill-archive/logo-creator/<yyyy-mm-dd-summaryname>/
  logo-01.png
  ...
  logo-final-cropped.png
  logo-final-nobg.png
  logo-final.svg
  preview.html
```

## Workflow Steps

### Phase 1: Architect (Requirements)

Gather requirements from user:

1. **Project/Brand name** - What is the logo for?
2. **Style preference:**
   - Pixel art / 8-bit retro
   - Minimalist / flat design
   - 3D / isometric
   - Hand-drawn / sketch
   - Mascot / character
   - Monogram / lettermark
   - Abstract / geometric

3. **Aspect ratio:**
   - `1:1` - Square (default for logos)
   - `16:9` - Wide
   - `4:3` - Standard

4. **Color preferences:**
   - Monochrome (black & white)
   - Specific brand colors
   - Let AI decide

**Wait for user confirmation before proceeding!**

### Phase 2: Trace (Existing Assets)

Check for existing brand assets to incorporate:
- Previous logos
- Brand colors
- Style guides

### Phase 3: Link (Connect to Generation)

Use nanobanana skill:

```bash
# Batch generate 20 logos
python3 <nanobanana>/scripts/batch_generate.py "{style} logo for {brand}, {description}, {colors}" \
  -n 20 --ratio 1:1 -d .skill-archive/logo-creator/<date-name> -p logo
```

### Phase 4: Assemble (Generate & Iterate)

**Generate 20 variations**
- Use sequential naming: `logo-01.png`, `logo-02.png`, etc.

**Create HTML Preview**
```bash
cp templates/preview.html .skill-archive/logo-creator/<name>/preview.html
open .skill-archive/logo-creator/<name>/preview.html
```

**Iterate with User**
- Ask which logos they prefer
- Generate more variations of favorites
- Use naming: `logo-{original}-v{n}.png`

### Phase 5: Stress-Test (Finalize)

**Crop to 1:1:**
```bash
python3 scripts/crop_logo.py {input.png} {output-cropped.png}
```

**Remove background:**
```bash
python3 scripts/remove_bg.py {input.png} {output-nobg.png}
```

**Convert to SVG:**
```bash
python3 scripts/vectorize.py {input.png} {output.svg}
```

## Prompt Patterns

**Pixel Art:**
```
Pixel art {subject} logo, 8-bit retro style, black pixels on white background
```

**Minimalist:**
```
Minimalist {subject} logo, flat design, clean lines, {color} on white
```

**Mascot:**
```
Cute {character} mascot logo, friendly expression, {colors}
```

## Final Deliverables

```
| File | Description | Size |
|------|-------------|------|
| logo.png | Original | 1024x1024 |
| logo-cropped.png | No margins | ~800x800 |
| logo-nobg.png | Transparent | ~800x800 |
| logo.svg | Vector | ~20KB |
```

## References

- [references/styles.md](./references/styles.md) - Logo style guide
