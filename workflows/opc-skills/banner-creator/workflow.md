# Banner Creator Workflow

**Status:** Active
**Date:** 2026-02-21
**Use Case:** Create professional banners through AI image generation with iterative design
**Source:** Adapted from OPC Skills (resciencelab/opc-skills)

## Overview

Generate professional banners for GitHub, Twitter, websites, and more through iterative AI image generation.

## ATLAS Alignment

| ATLAS Phase | Workflow Step |
|-------------|---------------|
| Architect | Gather requirements, define target platform |
| Trace | Check existing brand assets |
| Link | Connect to nanobanana skill for generation |
| Assemble | Generate variations, iterate with user |
| Stress-test | Preview in browser, crop to target |

## Trigger

This workflow is invoked when user mentions:
- Banner, header, hero image, cover image
- GitHub banner, Twitter header, readme banner
- Any wide format promotional image

## Prerequisites

**Required API Keys:**
- `GEMINI_API_KEY` - Get from [Google AI Studio](https://aistudio.google.com/apikey)

**Required Skills:**
- `nanobanana` - AI image generation (Gemini 3 Pro Image)

## Output Location

```
.skill-archive/banner-creator/<yyyy-mm-dd-summaryname>/
  banner-01.png
  banner-02.png
  ...
  banner-final-cropped.png
  preview.html
```

## Workflow Steps

### Phase 1: Architect (Requirements)

Gather requirements from user:

1. **Purpose** - Where will the banner be used?
   - GitHub README (2:1)
   - Twitter/X header (3:1)
   - LinkedIn banner
   - Website hero (16:9)
   - YouTube channel art

2. **Style preference**
   - Match existing logo/brand?
   - Pixel art / 8-bit retro
   - Minimalist / flat design
   - Gradient / modern

3. **Content elements**
   - Brand name / project name?
   - Tagline / slogan?
   - Logo character to include?

4. **Color preferences**

**Wait for user confirmation before proceeding!**

### Phase 2: Trace (Existing Assets)

Check for existing brand assets to incorporate:
- Logo files
- Brand colors
- Previous banners
- Character assets

### Phase 3: Link (Connect to Generation)

Use nanobanana skill for generation:

```bash
# Batch generate 20 banners
python3 <nanobanana_skill_dir>/scripts/batch_generate.py "{style} banner for {brand}, {description}" \
  -n 20 --ratio 21:9 -d .skill-archive/banner-creator/<date-name> -p banner
```

### Phase 4: Assemble (Generate & Iterate)

**Step 1: Generate 20 variations**
- Generate at `21:9` ratio (widest), crop later
- Use sequential naming: `banner-01.png`, `banner-02.png`, etc.

**Step 2: Create HTML Preview**
```bash
cp <skill_dir>/templates/preview.html .skill-archive/banner-creator/<name>/preview.html
open .skill-archive/banner-creator/<name>/preview.html
```

**Step 3: Iterate with User**
- Ask which banners they prefer
- Generate 10-20 more variations of favorites
- Use naming: `banner-{original}-v{n}.png`

**Step 4: Crop to Target**
```bash
python3 <skill_dir>/scripts/crop_banner.py {input.png} {output.png} --ratio 2:1 --width 1280
```

### Phase 5: Stress-Test (Deliver)

Present final deliverables:
```
| File | Description | Size |
|------|-------------|------|
| banner-03.png | Original (21:9) | 2016x864 |
| banner-03-cropped.png | GitHub README (2:1) | 1280x640 |
```

## Common Aspect Ratios

Generate at widest, then crop:
- `21:9` - Ultra-wide (for generation)
- `16:9` - Website hero
- `3:1` - Twitter header
- `2:1` - GitHub README

## Prompt Patterns

**With Text:**
```
Wide banner for {brand}, {style} style, featuring "{text}" prominently, {colors}
```

**With Character:**
```
Wide banner featuring {character}, {style} style, "{brand}" text, {colors}
```

**Abstract:**
```
Abstract {style} banner, {colors} gradient, geometric patterns, "{brand}" centered
```

## References

- [references/formats.md](./references/formats.md) - Common banner sizes by platform
