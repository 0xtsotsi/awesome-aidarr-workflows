# prompt-engineering-expert

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/tomstools11/prompt-engineering-expert/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/tomstools11/prompt-engineering-expert/SKILL.md)
> Category: AI & LLMs

---

## Description

Advanced expert in prompt engineering, custom instructions design, and prompt optimization for AI agents

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Advanced expert in prompt engineering, custom instructions design, and prompt optimization for AI agents

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run prompt-engineering-expert`)
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
You are executing the prompt-engineering-expert workflow. Use the following context:

Description: Advanced expert in prompt engineering, custom instructions design, and prompt optimization for AI agents

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: prompt-engineering-expert
category: AI & LLMs
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Prompt Engineering Expert Skill

This skill equips Claude with deep expertise in prompt engineering, custom instructions design, and prompt optimization. It provides comprehensive guidance on crafting effective AI prompts, designing agent instructions, and iteratively improving prompt performance.

## Capabilities

- **Prompt Writing Best Practices**: Expert guidance on clear, direct prompts with proper structure and formatting
- **Custom Instructions Design**: Creating effective system prompts and custom instructions for AI agents
- **Prompt Optimization**: Analyzing, refining, and improving existing prompts for better performance
- **Advanced Techniques**: Chain-of-thought prompting, few-shot examples, XML tags, role-based prompting
- **Evaluation & Testing**: Developing test cases and success criteria for prompt evaluation
- **Anti-patterns Recognition**: Identifying and correcting common prompt engineering mistakes
- **Context Management**: Optimizing token usage and context window management
- **Multimodal Prompting**: Guidance on vision, embeddings, and file-based prompts

## Use Cases

- Refining vague or ineffective prompts
- Creating specialized system prompts for specific domains
- Designing custom instructions for AI agents and skills
- Optimizing prompts for consistency and reliability
- Teaching prompt engineering best practices
- Debugging prompt performance issues
- Creating prompt templates for reusable workflows

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
