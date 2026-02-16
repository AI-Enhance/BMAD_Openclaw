# BMad-OpenClaw Orchestrator

This document describes how to orchestrate the BMad Method workflow through OpenClaw's `sessions_spawn` mechanism. Each BMad agent runs as a spawned subagent session.

## How It Works

In the official BMad Method, agents are loaded into IDE contexts (Cursor, Windsurf, etc.) via YAML definitions and menu triggers. In OpenClaw, we achieve the same by spawning subagent sessions with the agent's `.md` file as context.

### Spawning an Agent

To invoke any BMad agent, use `sessions_spawn` with:
- **label**: The agent identifier (e.g., `bmad-pm`, `bmad-dev`)
- **prompt**: The agent's `.md` file from `agents/` as system context, plus your task description

### Agent Roster

| Icon | Name | Role | OpenClaw Label | Menu Triggers |
|------|------|------|---------------|---------------|
| 📊 | Mary | Business Analyst | `bmad-analyst` | BP, MR, DR, TR, CB, DP |
| 📋 | John | Product Manager | `bmad-pm` | CP, VP, EP, CE, IR, CC |
| 🏗️ | Winston | Architect | `bmad-architect` | CA, IR |
| 🎨 | Sally | UX Designer | `bmad-ux` | CU |
| 🏃 | Bob | Scrum Master | `bmad-sm` | SP, CS, ER, CC |
| 💻 | Amelia | Developer | `bmad-dev` | DS, CR |
| 🧪 | Quinn | QA Engineer | `bmad-qa` | QA |
| 📚 | Paige | Technical Writer | `bmad-tech-writer` | DP, WD, US, MG, VD, EC |
| 🚀 | Barry | Quick Flow Solo Dev | `bmad-quick-flow` | QS, QD, CR |
| 🧙 | BMad Master | Orchestrator | `bmad-master` | LT, LW |

## Workflow Execution Engine

The BMad Method uses a core workflow execution engine (`workflow.xml`) that governs how all workflows run. Key rules:

1. **Always read COMPLETE files** - NEVER use offset/limit when reading workflow files
2. **Instructions are MANDATORY** - either as file path, steps, or embedded list
3. **Execute ALL steps IN EXACT ORDER**
4. **Save to template output file after EVERY "template-output" tag**
5. **NEVER skip a step**

### Execution Modes

- **Normal mode**: Full user interaction and confirmation at every step
- **YOLO mode**: Skip all confirmations, auto-generate remaining sections

### Template-Output Checkpoints

After each template-output, the user can choose:
- **[a]** Advanced Elicitation - deeper exploration
- **[c]** Continue - proceed to next step
- **[p]** Party-Mode - multi-agent discussion
- **[y]** YOLO - auto-complete the rest

## Smart File Discovery (discover_inputs protocol)

Workflows use intelligent file discovery for project artifacts:

- **FULL_LOAD**: Load ALL files in directory (for PRD, Architecture, UX)
- **SELECTIVE_LOAD**: Load specific shard using template variable (for epics with specific epic number)
- **INDEX_GUIDED**: Load index.md, analyze structure, then intelligently load relevant docs

Priority: Try sharded documents first, fall back to whole document.

## OpenClaw-Specific Notes

- Each agent session is independent - spawn fresh sessions for each workflow
- For validation workflows, use a different LLM model if available
- Agent conversations are interactive - the agent will ask questions and wait for input
- Project artifacts should be stored in your workspace under a project-specific directory
