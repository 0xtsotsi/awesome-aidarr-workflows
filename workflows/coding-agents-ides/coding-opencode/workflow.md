# coding-opencode

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/iqbalnaveliano/coding-opencode/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/iqbalnaveliano/coding-opencode/SKILL.md)
> Category: Coding Agents & IDEs

---

## Description

Memungkinkan penggunaan agen pengkodean OpenCode yang telah dikustomisasi dengan "Oh My OpenCode" untuk tugas pengembangan kode yang kompleks, eksplorasi codebase, debugging, refactoring, dan orkestrasi multi-model. Gunakan skill ini ketika Anda membutuhkan bantuan coding AI yang otonom dan canggih, terutama saat Anda ingin memanfaatkan fitur-fitur "Oh My OpenCode" seperti agen Sisyphus, Hephaestus, Oracle, Librarian, atau Explorer, serta alat LSP/AST.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Memungkinkan penggunaan agen pengkodean OpenCode yang telah dikustomisasi dengan "Oh My OpenCode" untuk tugas pengembangan kode yang kompleks, eksplorasi codebase, debugging, refactoring, dan orkestrasi multi-model. Gunakan skill ini ketika Anda membutuhkan bantuan coding AI yang otonom dan canggih, terutama saat Anda ingin memanfaatkan fitur-fitur "Oh My OpenCode" seperti agen Sisyphus, Hephaestus, Oracle, Librarian, atau Explorer, serta alat LSP/AST.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run coding-opencode`)
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
You are executing the coding-opencode workflow. Use the following context:

Description: Memungkinkan penggunaan agen pengkodean OpenCode yang telah dikustomisasi dengan "Oh My OpenCode" untuk tugas pengembangan kode yang kompleks, eksplorasi codebase, debugging, refactoring, dan orkestrasi multi-model. Gunakan skill ini ketika Anda membutuhkan bantuan coding AI yang otonom dan canggih, terutama saat Anda ingin memanfaatkan fitur-fitur "Oh My OpenCode" seperti agen Sisyphus, Hephaestus, Oracle, Librarian, atau Explorer, serta alat LSP/AST.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: coding-opencode
category: Coding Agents & IDEs
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Skill: coding-opencode

Skill ini dirancang untuk memanfaatkan kemampuan penuh dari instalasi OpenCode Anda yang telah dikustomisasi dengan "Oh My OpenCode". Ini memberikan akses ke orkestrasi multi-agen yang canggih, alat pengembangan yang terintegrasi, dan alur kerja otomatis untuk menyelesaikan tugas-tugas pengkodean.

## Kapan Menggunakan Skill Ini

Gunakan `coding-opencode` ketika Anda:
*   Membutuhkan bantuan AI untuk menulis atau memodifikasi kode.
*   Perlu melakukan eksplorasi codebase yang mendalam.
*   Membutuhkan bantuan untuk debugging atau refactoring.
*   Ingin memanfaatkan agen khusus seperti Frontend UI/UX Engineer atau Oracle.
*   Berencana untuk melakukan tugas pengembangan yang membutuhkan beberapa langkah dan koordinasi antar agen.
*   Ingin mengaktifkan mode "ultrawork" atau "ulw" untuk eksekusi tugas yang otonom dan berkelanjutan.

## Fitur Utama Melalui "Oh My OpenCode"

"Oh My OpenCode" menghadirkan beberapa agen dan fitur canggih ke OpenCode Anda:

*   **Sisyphus (Main Agent)**: Mengorkestrasi agen-agen lain untuk memastikan tugas diselesaikan sampai tuntas.
*   **Hephaestus (Autonomous Deep Worker)**: Agen otonom yang berorientasi pada tujuan untuk eksekusi mendalam.
*   **Oracle (Design & Debugging)**: Agen spesialis untuk membantu dalam desain dan proses debugging.
*   **Librarian (Docs & Codebase Exploration)**: Agen untuk mencari dokumentasi dan menjelajahi codebase.
*   **Explore (Fast Codebase Grep)**: Untuk eksplorasi codebase yang sangat cepat.
*   **LSP & AST Tools**: Dukungan penuh untuk Language Server Protocol (LSP) dan Abstract Syntax Tree (AST) untuk refactoring yang lebih akurat dan aman.
*   **Multi-model Orchestration**: Memungkinkan penggunaan berbagai model AI yang berbeda, masing-masing dioptimalkan untuk tugas tertentu.
*   **`ultrawork` / `ulw` Keyword**: Cukup sertakan `ultrawork` atau `ulw` dalam perintah Anda untuk mengaktifkan alur kerja otomatis penuh yang memanfaatkan semua agen dan fitur "Oh My OpenCode".

## Cara Menggunakan

Untuk menggunakan skill ini, Anda dapat memanggil perintah OpenCode melalui tool `exec`, dan menyertakan instruksi serta argumen yang diperlukan. Jika Anda ingin mengaktifkan orkestrasi penuh dari "Oh My OpenCode", pastikan untuk menyertakan `ultrawork` atau `ulw` dalam *prompt* atau argumen Anda.

**Contoh Umum:**

```bash
# Untuk memulai sesi OpenCode dengan mode ultrawork
opencode --agent build --ultrawork "Buatkan sebuah fungsi Python untuk menghitung deret Fibonacci"

# Untuk meminta agen Librarian mencari informasi tentang suatu API
opencode --agent build "ulw: Cari dokumentasi untuk API 'requests' Python dan berikan contoh penggunaan dasar."

# Untuk refactoring kode
opencode --agent build "ulw: Refactor file 'src/main.js' agar menggunakan async/await."
```

**Perhatikan:** Perintah `opencode` di atas adalah contoh. Karena OpenCode diinstal di **WSL** dan dijalankan via **PowerShell**, setiap perintah OpenCode perlu diawali dengan `wsl`.
Contoh: `wsl opencode ...`

**Target Folder:** Semua operasi pengkodean atau manipulasi file akan menargetkan `C:\Users\Administrator\Documents\Jagonyakomputer` sebagai *working directory* utama secara default, kecuali jika ditentukan lain.

**Integrasi Docker:** Agent memiliki kemampuan untuk mengoperasikan Docker container via PowerShell, jika diperlukan untuk tugas yang melibatkan containerisasi atau lingkungan pengembangan terisolasi.

## Konfigurasi

"Oh My OpenCode" sangat dapat dikustomisasi. Konfigurasi dapat ditemukan di:
*   `.opencode/oh-my-opencode.json` (untuk proyek)
*   `~/.config/opencode/oh-my-opencode.json` (untuk pengguna)

Anda dapat mengubah model yang digunakan oleh agen tertentu, suhu, *prompt*, dan izin di file konfigurasi ini.

Jika Anda perlu melakukan konfigurasi spesifik atau mengatasi masalah, saya akan merujuk ke dokumentasi "Oh My OpenCode" atau file konfigurasi tersebut.
---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
