# voice-ui

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/yukihamada/voice-ui/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/yukihamada/voice-ui/SKILL.md)
> Category: Speech & Transcription

---

## Description

Self-evolving voice assistant UI. Talk to your AI, ask it to improve itself, and watch the code update in real-time.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Self-evolving voice assistant UI. Talk to your AI, ask it to improve itself, and watch the code update in real-time.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run voice-ui`)
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
You are executing the voice-ui workflow. Use the following context:

Description: Self-evolving voice assistant UI. Talk to your AI, ask it to improve itself, and watch the code update in real-time.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: voice-ui
category: Speech & Transcription
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Voice UI

**自己進化型AIアシスタントUI** - 音声で会話しながら自分自身を改善できる

## 機能

- 🎤 音声認識 (Whisper)
- 🔊 音声合成 (TTS)
- 🤖 かわいいロボットUI（表情変化）
- 🔄 自己進化（UIの変更を音声で指示）
- 📝 自動Gitコミット

## セットアップ

```bash
cd <workspace>/skills/voice-ui
npm install
./start.sh
```

ブラウザで http://localhost:8765 を開く

## 必要な設定

OpenClaw config (`~/.openclaw/openclaw.json`) に voice agent を追加:

```json
{
  "agents": {
    "list": [{
      "id": "voice",
      "name": "Voice Assistant",
      "model": { "primary": "anthropic/claude-sonnet-4-5" }
    }]
  }
}
```

## 使い方

1. マイクボタンをタップ（またはスペースキー長押し）
2. 話しかける
3. AIが返答

### 自己進化コマンド

- 「背景を青にして」→ CSSを自動編集
- 「ボタンを大きくして」→ スタイルを変更
- 「新機能を追加して」→ JSを編集

変更は自動でGitコミットされる。

## ファイル構成

- `index.html` - メインUI
- `server.cjs` - Node.jsサーバー
- `start.sh` - 起動スクリプト
- `CONTEXT.md` - AIへのコンテキスト情報

## 環境変数

- `OPENAI_API_KEY` - OpenAI API Key（Whisper/TTS用）

設定がない場合、OpenClawの設定から自動取得を試みる。

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
