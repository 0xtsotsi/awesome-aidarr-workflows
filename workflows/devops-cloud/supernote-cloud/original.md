



# Supernote Private Cloud

Browse, upload, and manage files on a self-hosted Supernote Private Cloud via its reverse-engineered REST API. Includes article-to-ebook conversion for sending web content to the device.

## Setup

```bash
export SUPERNOTE_URL="http://192.168.50.168:8080"
export SUPERNOTE_USER="your@email.com"
export SUPERNOTE_PASSWORD="your_password"
```

Python dependencies (for article conversion): `readability-lxml`, `ebooklib`, `requests`, `beautifulsoup4`, `lxml`.

## Commands

### Send a web article to the device

```bash
{baseDir}/scripts/supernote.sh send-article --url "https://example.com/article" --format epub --dir-path Document
{baseDir}/scripts/supernote.sh send-article --url "https://example.com/article" --format pdf --dir-path "Document/Articles"
{baseDir}/scripts/supernote.sh send-article --url "https://example.com/article" --title "Custom Title" --dir-path Document
```

Fetches article content, extracts readable text with images, converts to clean EPUB or PDF, then uploads to the specified folder. Default format: epub. Default folder: Document.

### List directory contents

```bash
{baseDir}/scripts/supernote.sh ls
{baseDir}/scripts/supernote.sh ls --path Document
{baseDir}/scripts/supernote.sh ls --path "Note/Journal"
{baseDir}/scripts/supernote.sh ls --dir 778507258886619136
```

### Directory tree

```bash
{baseDir}/scripts/supernote.sh tree --depth 2
```

### Find directory ID by path

```bash
{baseDir}/scripts/supernote.sh find-dir --path "Document/Books"
```

### Upload a file

```bash
{baseDir}/scripts/supernote.sh upload --file /path/to/file.pdf --dir-path Document
{baseDir}/scripts/supernote.sh upload --file /path/to/book.epub --dir-path "Document/Books"
{baseDir}/scripts/supernote.sh upload --file /path/to/file.pdf --dir 778507258773372928 --name "Renamed.pdf"
```

### Check storage capacity

```bash
{baseDir}/scripts/supernote.sh capacity
```

### Login (manual)

```bash
{baseDir}/scripts/supernote.sh login
```

## Default Folders

| Folder | Purpose |
|--------|---------|
| Note | Handwritten notes (.note files) |
| Document | PDFs, EPUBs, documents |
| Inbox | Incoming files |
| Export | Exported content |
| Screenshot | Screenshots |
| Mystyle | Custom styles/templates |

## Notes

- EPUB is recommended for articles — renders cleanly on e-ink with reflowable text
- The API is reverse-engineered and unofficial — endpoints may change with firmware updates
- Directory args accept paths (e.g., "Document/Books") or numeric IDs
- Some sites block scraping — if fetch fails, try a different URL or use a cached/saved page

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
