# twitter-ai-trending

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/snowshadow/twitter-ai-trending/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/snowshadow/twitter-ai-trending/SKILL.md)
> Category: AI & LLMs

---

## Description

Search Twitter/X for trending AI discussions

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Search Twitter/X for trending AI discussions

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run twitter-ai-trending`)
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
You are executing the twitter-ai-trending workflow. Use the following context:

Description: Search Twitter/X for trending AI discussions

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: twitter-ai-trending
category: AI & LLMs
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Twitter AI热议帖子搜索

## 任务说明
搜索Twitter上关于AI的热门讨论，返回Top 10帖子，按互动量排序。

## 输出格式
```
========== 晨间简报-{日期} ==========

- [标题] (链接)
  - 阅读量/互动量
  - 核心内容
  - 意外收获：反共识信息

- [标题] (链接)
  - 阅读量/互动量
  - 核心内容
  - 意外收获：反共识信息
  ...
=============================
```

## 搜索关键词
- "AI OR artificial intelligence OR LLM OR GPT"
- 筛选: 热门、英文、过去24小时

## 注意事项
1. 只选择有实质内容的讨论，避免简单转发/广告
2. 优先选择有反常识/独到见解的帖子
3. 链接必须是有效的Twitter链接
4. 互动量指点赞+转发+评论总数
5. 如果搜索结果不足10条，返回所有找到的结果

## 响应要求
- 全部使用中文
- 简洁有力，每个帖子描述不超过50字
- "意外收获"要挖掘帖子中反直觉的观点

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
