# Nanobanana - AI Image Generation Workflow

**Status:** Active
**Date:** 2026-02-21
**Use Case:** Generate and edit images using Google Gemini 3 Pro Image
**Source:** Adapted from OPC Skills (resciencelab/opc-skills)

## Overview

Generate and edit images using Google's Gemini 3 Pro Image model (`gemini-3-pro-image-preview`, nicknamed "Nano Banana Pro" 🍌).

## ATLAS Alignment

| ATLAS Phase | Workflow Step |
|-------------|---------------|
| Architect | Define image requirements (subject, style, size) |
| Trace | Check existing assets to incorporate |
| Link | Connect to Gemini API |
| Assemble | Generate variations, iterate |
| Stress-test | Verify output quality |

## Trigger

This workflow is invoked when user mentions:
- Generate images, create images
- AI image generation, Gemini image
- Logo creation, banner creation

## Prerequisites

**Required:**
- `GEMINI_API_KEY` - Get from [Google AI Studio](https://aistudio.google.com/apikey)
- Python 3.10+ with `google-genai` package

```bash
pip install google-genai pillow
```

## Quick Start

### Generate an image:
```bash
python3 scripts/generate.py "a cute robot mascot, pixel art style" -o robot.png
```

### Edit an existing image:
```bash
python3 scripts/generate.py "make the background blue" -i input.jpg -o output.png
```

### Generate with aspect ratio:
```bash
python3 scripts/generate.py "cinematic landscape" --ratio 21:9 -o landscape.png
```

### Generate 4K:
```bash
python3 scripts/generate.py "professional product photo" --size 4K -o product.png
```

## Script Reference

### `scripts/generate.py`

```
Usage: generate.py [OPTIONS] PROMPT

Arguments:
  PROMPT              Text prompt for image generation

Options:
  -o, --output PATH   Output file path (default: auto-generated)
  -i, --input PATH    Input image for editing (optional)
  -r, --ratio RATIO   Aspect ratio (1:1, 16:9, 9:16, 21:9, etc.)
  -s, --size SIZE     Image size: 2K or 4K (default: standard)
  --search            Enable Google Search grounding for accuracy
```

**Supported aspect ratios:**
- `1:1` - Square (default)
- `2:3`, `3:2` - Portrait/Landscape
- `4:5`, `5:4` - Photo
- `9:16`, `16:9` - Widescreen
- `21:9` - Ultra-wide/Cinematic

### `scripts/batch_generate.py`

```
Usage: batch_generate.py [OPTIONS] PROMPT

Options:
  -n, --count N       Number of images to generate (default: 10)
  -d, --dir PATH      Output directory
  -p, --prefix STR    Filename prefix (default: "image")
  -r, --ratio RATIO   Aspect ratio
  -s, --size SIZE     Image size (2K/4K)
  --delay SECONDS     Delay between generations (default: 3)
```

**Example:**
```bash
python3 scripts/batch_generate.py "pixel art logo" -n 20 -d ./logos -p logo
```

## Features

### Text-to-Image
- Photorealistic images
- Artistic styles (pixel art, illustration)
- Product photography
- Landscapes and scenes

### Image Editing
- Style transfer
- Object addition/removal
- Background changes
- Color adjustments

### High-Resolution Output
- **Standard**: Fast generation
- **2K**: Enhanced detail (2048px)
- **4K**: Maximum quality (3840px)

## Best Practices

### Prompt Writing
```
"A cozy coffee shop interior, warm lighting, vintage aesthetic,
wooden furniture, plants on shelves, morning sunlight through windows,
soft focus background, 35mm film photography style"
```

### Batch Tips
1. Generate 10-20 variations
2. Use consistent prompts for style coherence
3. Add 3-5 second delays to avoid rate limits

## Rate Limits

- Gemini API has usage quotas
- Add delays between batch generations
- Check quota at [Google AI Studio](https://aistudio.google.com/)

## Troubleshooting

**"API key not found"** → Set `GEMINI_API_KEY` environment variable

**"No image in response"** → Prompt may have triggered safety filters

**"Rate limit exceeded"** → Wait and retry, reduce batch size

## References

- [references/prompts.md](./references/prompts.md) - Prompt examples by category
