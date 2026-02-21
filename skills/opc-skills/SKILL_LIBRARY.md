# OPC Skills Library

Converted from [ReScienceLab/opc-skills](https://github.com/ReScienceLab/opc-skills)

## Available Skills

### 1. banner-creator
**Description:** Create professional banners using AI image generation through an iterative design process.

**Triggers:**
- "create a banner"
- "generate a header"
- "make a hero image"
- "GitHub banner"
- "Twitter header"
- "readme banner"

**Dependencies:**
- GEMINI_API_KEY environment variable
- nanobanana skill (for image generation)

**Usage:**
```
skill: banner-creator
```

---

### 2. domain-hunter
**Description:** Find available domain names for your projects.

**Triggers:**
- "find a domain"
- "check domain availability"
- "domain name ideas"
- "search for domains"

**Usage:**
```
skill: domain-hunter
```

---

### 3. logo-creator
**Description:** Create logos using AI image generation with iterative refinement.

**Triggers:**
- "create a logo"
- "generate a logo"
- "design a logo"
- "logo for [brand]"

**Dependencies:**
- GEMINI_API_KEY environment variable
- nanobanana skill (for image generation)

**Usage:**
```
skill: logo-creator
```

---

### 4. nanobanana
**Description:** AI image generation using Gemini 3 Pro Image API.

**Triggers:**
- "generate an image"
- "create an image"
- "AI image"
- "generate photo"

**Dependencies:**
- GEMINI_API_KEY environment variable

**Usage:**
```
skill: nanobanana
```

---

### 5. producthunt
**Description:** Prepare and launch products on Product Hunt.

**Triggers:**
- "launch on Product Hunt"
- "Product Hunt launch"
- "prepare for Product Hunt"
- "PH launch"

**Usage:**
```
skill: producthunt
```

---

### 6. reddit
**Description:** Engage with Reddit communities and create content.

**Triggers:**
- "post on reddit"
- "reddit marketing"
- "reddit content"
- "engage with [subreddit]"

**Usage:**
```
skill: reddit
```

---

### 7. requesthunt
**Description:** Find and fulfill product requests on platforms like RequestHunter.

**Triggers:**
- "find product requests"
- "request hunter"
- "what to build"
- "product ideas from requests"

**Usage:**
```
skill: requesthunt
```

---

### 8. seo-geo
**Description:** SEO optimization with geographic targeting.

**Triggers:**
- "seo for [location]"
- "local seo"
- "geo-targeted seo"
- "optimize for search"

**Usage:**
```
skill: seo-geo
```

---

### 9. twitter
**Description:** Create and manage Twitter content and engagement.

**Triggers:**
- "create a tweet"
- "twitter thread"
- "twitter content"
- "post on twitter"

**Usage:**
```
skill: twitter
```

---

## Setup Requirements

### Required Environment Variables

For image generation skills (banner-creator, logo-creator, nanobanana):

```bash
export GEMINI_API_KEY="your-api-key-here"
```

Get your API key from: https://aistudio.google.com/apikey

### Skill Dependencies

- **banner-creator** requires: nanobanana
- **logo-creator** requires: nanobanana

All other skills work independently.

## File Structure

```
skills/opc-skills/
├── banner-creator/
│   ├── SKILL.md
│   ├── scripts/
│   ├── templates/
│   ├── references/
│   └── examples/
├── domain-hunter/
│   └── SKILL.md
├── logo-creator/
│   ├── SKILL.md
│   ├── scripts/
│   ├── templates/
│   ├── references/
│   └── examples/
├── nanobanana/
│   ├── SKILL.md
│   ├── scripts/
│   ├── references/
│   └── examples/
├── producthunt/
│   └── SKILL.md
├── reddit/
│   └── SKILL.md
├── requesthunt/
│   └── SKILL.md
├── seo-geo/
│   └── SKILL.md
└── twitter/
    └── SKILL.md
```

## Usage

To use any OPC skill, reference it by name:

```bash
# Use directly
skill: banner-creator

# Or with context
skill: logo-creator create a minimalist logo for my tech startup
```

## Source

Original skills from: https://github.com/ReScienceLab/opc-skills

Converted for TinyClaw by: AzureDeer (Henry)
