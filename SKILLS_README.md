# Skills Library

This directory contains reusable skill modules for AiDarr/TinyClaw agents.

## OPC Skills Collection

Converted from [ReScienceLab/opc-skills](https://github.com/ReScienceLab/opc-skills)

### 🎨 Image Generation & Design Skills

#### 1. banner-creator
Create professional banners using AI image generation through an iterative design process.

**Usage:**
```
skill: banner-creator
```

**Features:**
- Generate banners for GitHub README, Twitter headers, LinkedIn, website heroes
- Iterative design process with user feedback
- Auto-crop to target aspect ratios
- Batch generation (20+ variations)

**Requirements:**
- `GEMINI_API_KEY` environment variable
- Requires `nanobanana` skill

**Files:**
- `scripts/generate.py` - Single banner generation
- `scripts/batch_generate.py` - Batch generation with auto-delay
- `scripts/crop_banner.py` - Crop to target ratio
- `templates/preview.html` - HTML preview template

---

#### 2. logo-creator
Create logos using AI image generation with iterative refinement.

**Usage:**
```
skill: logo-creator
```

**Features:**
- Generate logo concepts and variations
- Support for multiple logo styles (minimalist, pixel art, gradient, etc.)
- Auto-crop to square format
- Batch generation for rapid iteration

**Requirements:**
- `GEMINI_API_KEY` environment variable
- Requires `nanobanana` skill

---

#### 3. nanobanana
AI image generation using Google Gemini 3 Pro Image API.

**Usage:**
```
skill: nanobanana
```

**Features:**
- Generate images from text prompts
- Edit existing images with AI
- Support for multiple aspect ratios (1:1, 16:9, 21:9, etc.)
- Batch generation capabilities

**Requirements:**
- `GEMINI_API_KEY` environment variable

**Get API Key:** https://aistudio.google.com/apikey

---

### 📱 Marketing & Social Media Skills

#### 4. producthunt
Prepare and launch products on Product Hunt.

**Usage:**
```
skill: producthunt
```

**Features:**
- Launch strategy templates
- Post creation guidelines
- Community engagement tips

---

#### 5. reddit
Engage with Reddit communities and create content.

**Usage:**
```
skill: reddit
```

**Features:**
- Subreddit analysis
- Content creation strategies
- Community engagement guidelines
- AMA (Ask Me Anything) preparation

---

#### 6. twitter
Create and manage Twitter content and engagement.

**Usage:**
```
skill: twitter
```

**Features:**
- Tweet creation
- Thread development
- Engagement strategies
- Content scheduling tips

---

### 🔍 Research & Discovery Skills

#### 7. domain-hunter
Find available domain names for your projects.

**Usage:**
```
skill: domain-hunter
```

**Features:**
- Domain name generation
- Availability checking
- Creative naming suggestions

---

#### 8. requesthunt
Find and fulfill product requests on platforms like RequestHunter.

**Usage:**
```
skill: requesthunt
```

**Features:**
- Product request discovery
- Request analysis
- Idea validation

---

#### 9. seo-geo
SEO optimization with geographic targeting.

**Usage:**
```
skill: seo-geo
```

**Features:**
- Local SEO strategies
- Geographic keyword targeting
- Location-based optimization

---

## Installation

### Python Dependencies

Install required Python packages:

```bash
pip install -r skills/opc-skills/requirements.txt
```

Or install individually:

```bash
pip install google-genai Pillow requests
```

### Environment Setup

For image generation skills (banner-creator, logo-creator, nanobanana), set your Gemini API key:

```bash
export GEMINI_API_KEY="your-api-key-here"
```

Get your API key from: https://aistudio.google.com/apikey

## Skill Dependencies

Some skills depend on others:

- **banner-creator** requires: `nanobanana`
- **logo-creator** requires: `nanobanana`

All other skills work independently.

## Directory Structure

```
skills/
└── opc-skills/
    ├── SKILL_LIBRARY.md         # Complete skill catalog
    ├── requirements.txt          # Python dependencies
    ├── banner-creator/           # Banner creation
    ├── domain-hunter/            # Domain discovery
    ├── logo-creator/             # Logo creation
    ├── nanobanana/               # AI image generation
    ├── producthunt/              # Product Hunt launches
    ├── reddit/                   # Reddit engagement
    ├── requesthunt/              # Product requests
    ├── seo-geo/                  # Geographic SEO
    └── twitter/                  # Twitter content
```

## Usage Examples

### Create a GitHub README Banner

```bash
skill: banner-creator
# Then specify: GitHub README banner, 2:1 ratio, tech/minimalist style
```

### Generate a Logo

```bash
skill: logo-creator
# Then specify: Minimalist tech logo for startup named "Acme"
```

### Find a Domain Name

```bash
skill: domain-hunter
# Then specify: Find domains for AI-powered task manager
```

### Plan a Product Hunt Launch

```bash
skill: producthunt
# Then provide product details and target launch date
```

## Contributing

To add new skills to this library:

1. Create a new directory under `skills/`
2. Include a `SKILL.md` file with documentation
3. Add any necessary scripts or templates
4. Update this README with the new skill
5. Submit a pull request

## License

Skills converted from [ReScienceLab/opc-skills](https://github.com/ReScienceLab/opc-skills)

Original license applies to respective skill authors.
