# travel-manager

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/alvarobcmed/travel-manager/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/alvarobcmed/travel-manager/SKILL.md)
> Category: Transportation

---

## Description

Comprehensive travel planning, booking, and management skill. Use when needing to plan international trips, manage multi-destination itineraries, handle family travel logistics, optimize travel costs, and coordinate complex travel arrangements.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Comprehensive travel planning, booking, and management skill. Use when needing to plan international trips, manage multi-destination itineraries, handle family travel logistics, optimize travel costs, and coordinate complex travel arrangements.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run travel-manager`)
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
You are executing the travel-manager workflow. Use the following context:

Description: Comprehensive travel planning, booking, and management skill. Use when needing to plan international trips, manage multi-destination itineraries, handle family travel logistics, optimize travel costs, and coordinate complex travel arrangements.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: travel-manager
category: Transportation
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Travel Manager Skill

## Core Capabilities
- International trip planning
- Multi-destination itinerary creation
- Family travel logistics
- Cost optimization
- Travel document management

## Workflow Steps
1. Destination Analysis
2. Route Optimization
3. Cost Calculation
4. Document Preparation
5. Booking Coordination

## Key Considerations for Family Travel
- Child-friendly routes
- Stopover comfort
- Baggage requirements
- Age-specific travel needs

## References
- [Family Travel Checklist](references/family-travel-checklist.md)
- [International Travel Documents](references/travel-documents.md)
- [Airline Comparison Matrix](references/airline-matrix.md)

## Usage Examples
- "Plan a family trip to Korea and Japan"
- "Find the most cost-effective international travel route"
- "Prepare travel documents for a multi-country trip"
---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
