# plansuite

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/double729/plansuite/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/double729/plansuite/SKILL.md)
> Category: Browser & Automation

---

## Description

No description available.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
What this workflow accomplishes.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run plansuite`)
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
You are executing the plansuite workflow. Use the following context:

Description: 

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: plansuite
category: Browser & Automation
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# PlanSuite

把“写计划（含子计划）→ 冻结计划（变更控制）→ 独立会话执行（带检查点）”合成一个最小可用流程。

## 文件结构（在当前工作目录创建/维护）
- `task_plan.md`：计划主文件（含子计划/里程碑）
- `progress.md`：执行进度（每次推进都要写）
- `findings.md`：发现/决策/坑点（避免重复踩坑）

> 不要把这三份写到聊天里：写到文件，才能恢复/续跑。

## 工作流（强约束，防跑偏）

### 0) 初始化（第一次做这个项目）
1. 如果缺文件：用模板创建 `task_plan.md/progress.md/findings.md`（见 `templates/`）。
2. 让用户确认目标、范围、约束、完成定义（DoD）。

### 1) 计划阶段（拆子计划）
在 `task_plan.md` 里输出：
- 背景/目标
- 范围（做/不做）
- 风险 & 回滚
- 子计划（Milestones）：每个子计划要有
  - 输入/输出
  - 验收标准
  - 预计工具调用/文件改动
  - 风险与回滚点

### 2) 冻结阶段（FINALIZED）
只有当用户明确说“按这个计划执行”后：
1. 在 `task_plan.md` 顶部写入：`STATUS: FINALIZED` + 时间戳。
2. 把“接下来要执行的子计划编号/名称”写入 `progress.md` 的 `Next`。

> 规则：未 FINALIZED 不允许进入执行阶段（最多做调查/补充计划）。

### 3) 执行阶段（独立会话 + 检查点）
当进入执行：
1. 建议用 `sessions_spawn` 开一个隔离执行会话（避免污染主会话上下文）。
2. 每完成一个子计划：
   - 更新 `progress.md`（Done/Next/Blockers）
   - 更新 `findings.md`（关键决策、踩坑、验证命令、回滚步骤）
3. 检查点策略（默认每个子计划至少一次）：
   - 执行前：复述子计划的 DoD + 风险 + 回滚
   - 执行后：给出验证步骤 + 结果

### 4) 变更控制（计划变更）
如果执行中发现计划不成立：
1. 不要“边做边改”。先写入 `findings.md`，再把变更提案写入 `task_plan.md`。
2. 把 `STATUS` 改为 `DRAFT`，等待用户重新确认。

## 你在什么时候用什么文件
- 需要问清楚/拆任务 → `task_plan.md`
- 需要告诉用户进度/下一步 → `progress.md`
- 需要记录结论/命令/坑/回滚 → `findings.md`

## 模板
- `templates/task_plan.md`
- `templates/progress.md`
- `templates/findings.md`

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
