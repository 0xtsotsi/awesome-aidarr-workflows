# quantum-lab

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/bramdo/quantum-lab/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/bramdo/quantum-lab/SKILL.md)
> Category: Coding Agents & IDEs

---

## Description

Run the /home/bram/work/quantum_lab Python scripts and demos inside the existing venv ~/.venvs/qiskit. Use when asked (e.g., via Telegram/OpenClaw) to run quant_math_lab.py, qcqi_pure_math_playground.py, quantum_app.py subcommands, quantumapp.server, or notebooks under the repo.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Run the /home/bram/work/quantum_lab Python scripts and demos inside the existing venv ~/.venvs/qiskit. Use when asked (e.g., via Telegram/OpenClaw) to run quant_math_lab.py, qcqi_pure_math_playground.py, quantum_app.py subcommands, quantumapp.server, or notebooks under the repo.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run quantum-lab`)
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
You are executing the quantum-lab workflow. Use the following context:

Description: Run the /home/bram/work/quantum_lab Python scripts and demos inside the existing venv ~/.venvs/qiskit. Use when asked (e.g., via Telegram/OpenClaw) to run quant_math_lab.py, qcqi_pure_math_playground.py, quantum_app.py subcommands, quantumapp.server, or notebooks under the repo.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: quantum-lab
category: Coding Agents & IDEs
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Quantum Lab

## Overview
Run quantum_lab repo commands inside the preexisting qiskit venv. Prefer the helper scripts in `scripts/` so the venv and repo root are always set.

## Command List (full)
Use `<SKILL_DIR>` as the folder where this skill is installed (e.g., `~/clawd/skills/quantum-lab`).

- `bash <SKILL_DIR>/scripts/qexec.sh python quant_math_lab.py`
- `bash <SKILL_DIR>/scripts/qexec.sh python qcqi_pure_math_playground.py`
- `bash <SKILL_DIR>/scripts/qexec.sh python quantum_app.py`
- `bash <SKILL_DIR>/scripts/qexec.sh python quantum_app.py self-tests`
- `bash <SKILL_DIR>/scripts/qexec.sh python quantum_app.py playground`
- `bash <SKILL_DIR>/scripts/qexec.sh python quantum_app.py notebook notebooks/SomeNotebook.ipynb`
- `bash <SKILL_DIR>/scripts/qexec.sh python -m quantumapp.server --host 127.0.0.1 --port 8000`

## Command List (short)
Use these for quick Telegram/OpenClaw commands. Both `gl` and `ql` are supported and equivalent.

- `bash <SKILL_DIR>/scripts/gl self-tests`
- `bash <SKILL_DIR>/scripts/gl playground`
- `bash <SKILL_DIR>/scripts/gl app`
- `bash <SKILL_DIR>/scripts/gl lab-tests`
- `bash <SKILL_DIR>/scripts/gl playground-direct`
- `bash <SKILL_DIR>/scripts/gl notebook notebooks/SomeNotebook.ipynb`
- `bash <SKILL_DIR>/scripts/gl web 8000`

## Shorthand Handling
If the user types `gl ...` or `ql ...` without a full path, always expand it to the full command:
- `gl <args>` → `bash <SKILL_DIR>/scripts/gl <args>`
- `ql <args>` → `bash <SKILL_DIR>/scripts/ql <args>`

## Notes
- Repo root default: `$HOME/work/quantum_lab` (override with `QUANTUM_LAB_ROOT`).
- Venv default: `~/.venvs/qiskit` (override with `VENV_PATH`).
- If dependencies are missing: `bash <SKILL_DIR>/scripts/qexec.sh pip install -r requirements.txt`.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
