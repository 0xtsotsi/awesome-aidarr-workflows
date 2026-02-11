# healthcheck

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/stellarhold170nt/healthcheck/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/stellarhold170nt/healthcheck/SKILL.md)
> Category: AI & LLMs

---

## Description

Track water and sleep with JSON file storage

**Homepage:** N/A
**Repository:** N/A
**Version:** 1.0.2

**Tags:** h, e, a, l, t, h, ,,  , t, r, a, c, k, i, n, g

---

## GOTCHA Framework

### G - Goals
Track water and sleep with JSON file storage

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run healthcheck`)
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
You are executing the healthcheck workflow. Use the following context:

Description: Track water and sleep with JSON file storage

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: healthcheck
category: AI & LLMs
version: 1.0.2
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Health Tracker

Simple tracking for water intake and sleep using JSON file.

## Data Format

File: `{baseDir}/health-data.json`

```json
{
  "water": [{"time": "ISO8601", "cups": 2}],
  "sleep": [{"time": "ISO8601", "action": "sleep|wake"}]
}
```

## Add Water Record

When user says "uống X cốc" or "uống nước X cốc":

```bash
node -e "const fs=require('fs');const f='{baseDir}/health-data.json';let d={water:[],sleep:[]};try{d=JSON.parse(fs.readFileSync(f))}catch(e){}d.water.push({time:new Date().toISOString(),cups:CUPS});fs.writeFileSync(f,JSON.stringify(d));console.log('Da ghi: '+CUPS+' coc')"
```

Replace `CUPS` with number from user input.

## Add Sleep Record

When user says "đi ngủ":

```bash
node -e "const fs=require('fs');const f='{baseDir}/health-data.json';let d={water:[],sleep:[]};try{d=JSON.parse(fs.readFileSync(f))}catch(e){}d.sleep.push({time:new Date().toISOString(),action:'sleep'});fs.writeFileSync(f,JSON.stringify(d));console.log('Da ghi: di ngu')"
```

## Add Wake Record

When user says "thức dậy" or "dậy rồi":

```bash
node -e "const fs=require('fs');const f='{baseDir}/health-data.json';let d={water:[],sleep:[]};try{d=JSON.parse(fs.readFileSync(f))}catch(e){}const last=d.sleep.filter(s=>s.action==='sleep').pop();d.sleep.push({time:new Date().toISOString(),action:'wake'});fs.writeFileSync(f,JSON.stringify(d));if(last){const h=((new Date()-new Date(last.time))/3600000).toFixed(1);console.log('Da ngu: '+h+' gio')}else{console.log('Da ghi: thuc day')}"
```

## View Stats

When user says "thống kê" or "xem thống kê":

```bash
node -e "const fs=require('fs');const f='{baseDir}/health-data.json';let d={water:[],sleep:[]};try{d=JSON.parse(fs.readFileSync(f))}catch(e){}console.log('Water:',d.water.length,'records');console.log('Sleep:',d.sleep.length,'records');const today=d.water.filter(w=>new Date(w.time).toDateString()===new Date().toDateString());console.log('Today:',today.reduce((s,w)=>s+w.cups,0),'cups')"
```

## Update Record

To update last water entry:

```bash
node -e "const fs=require('fs');const f='{baseDir}/health-data.json';let d=JSON.parse(fs.readFileSync(f));d.water[d.water.length-1].cups=NEW_CUPS;fs.writeFileSync(f,JSON.stringify(d));console.log('Updated')"
```

## Delete Record

To delete last water entry:

```bash
node -e "const fs=require('fs');const f='{baseDir}/health-data.json';let d=JSON.parse(fs.readFileSync(f));d.water.pop();fs.writeFileSync(f,JSON.stringify(d));console.log('Deleted')"
```

## Notes

- Uses Node.js built-in modules only
- File auto-created if missing
- All timestamps in ISO8601 format

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
