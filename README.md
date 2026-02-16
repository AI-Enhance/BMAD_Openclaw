# BMad-OpenClaw Bridge

An adaptation of the [BMad Method](https://github.com/bmad-code-org/bmad-method) for use with [OpenClaw](https://openclaw.com) via `sessions_spawn` subagent sessions.

## What Is This?

The BMad Method is an AI-driven agile development framework with specialized agents (Analyst, PM, Architect, UX Designer, Scrum Master, Developer, QA, Tech Writer) that guide you through the full product lifecycle — from brainstorming to implementation.

This repository adapts BMad for OpenClaw by providing each agent as a self-contained `.md` prompt file that can be loaded into a spawned subagent session.

## Repository Structure

```
bmad-openclaw/
├── agents/                    # One .md file per BMad agent
│   ├── ANALYST.md             # Mary — Business Analyst (📊)
│   ├── ARCHITECT.md           # Winston — Architect (🏗️)
│   ├── BMAD-MASTER.md         # BMad Master — Orchestrator (🧙)
│   ├── DEV.md                 # Amelia — Developer (💻)
│   ├── PM.md                  # John — Product Manager (📋)
│   ├── QA.md                  # Quinn — QA Engineer (🧪)
│   ├── QUICK-FLOW.md          # Barry — Quick Flow Solo Dev (🚀)
│   ├── SCRUM-MASTER.md        # Bob — Scrum Master (🏃)
│   ├── TECH-WRITER.md         # Paige — Technical Writer (📚)
│   └── UX-DESIGNER.md         # Sally — UX Designer (🎨)
├── templates/                 # Official BMad templates (verbatim copies)
│   ├── story-template.md
│   ├── sprint-status-template.yaml
│   ├── prd-template.md
│   ├── epics-template.md
│   ├── architecture-decision-template.md
│   ├── ux-design-template.md
│   ├── product-brief-template.md
│   ├── project-context-template.md
│   ├── readiness-report-template.md
│   ├── research-template.md
│   ├── brainstorming-template.md
│   └── tech-spec-template.md
├── checklists/                # Official BMad checklists (verbatim copies)
│   ├── code-review-checklist.md
│   ├── correct-course-checklist.md
│   ├── create-story-checklist.md
│   ├── dev-story-checklist.md
│   ├── sprint-planning-checklist.md
│   ├── qa-automate-checklist.md
│   └── document-project-checklist.md
├── ORCHESTRATOR.md            # How to orchestrate agents via OpenClaw
├── WORKFLOW-CYCLE.md          # Complete workflow phases and cycles
├── CHANGES.md                 # Rebuild documentation
└── README.md                  # This file
```

## Quick Start

1. **Pick an agent** from the table below
2. **Spawn a session** using `sessions_spawn` with the agent's `.md` file as context
3. **Use menu triggers** (e.g., type "CP" to create a PRD with the PM agent)

## Agent Roster

| Icon | Name | Role | Label | Key Triggers |
|------|------|------|-------|-------------|
| 📊 | Mary | Business Analyst | `bmad-analyst` | BP, MR, DR, TR, CB |
| 📋 | John | Product Manager | `bmad-pm` | CP, VP, EP, CE, IR, CC |
| 🏗️ | Winston | Architect | `bmad-architect` | CA, IR |
| 🎨 | Sally | UX Designer | `bmad-ux` | CU |
| 🏃 | Bob | Scrum Master | `bmad-sm` | SP, CS, ER, CC |
| 💻 | Amelia | Developer | `bmad-dev` | DS, CR |
| 🧪 | Quinn | QA Engineer | `bmad-qa` | QA |
| 📚 | Paige | Technical Writer | `bmad-tech-writer` | DP, WD, MG, VD, EC |
| 🚀 | Barry | Quick Flow Solo Dev | `bmad-quick-flow` | QS, QD, CR |
| 🧙 | BMad Master | Orchestrator | `bmad-master` | LT, LW |

## Workflow Phases

1. **Analysis** → Research, brainstorm, create product brief
2. **Planning** → PRD, UX design, epics & stories
3. **Solutioning** → Architecture, implementation readiness
4. **Implementation** → Sprint planning, story creation, development, code review, retrospective
5. **Quick Flow** → Rapid spec → dev → review for smaller features

See [WORKFLOW-CYCLE.md](WORKFLOW-CYCLE.md) for full details.

## Source

All agent definitions, workflow instructions, templates, and checklists are sourced directly from the [official BMad Method repository](https://github.com/bmad-code-org/bmad-method). The OpenClaw adaptation layer is minimal — just invocation headers on each agent file.

## License

Content derived from BMad Method — see the [original repository](https://github.com/bmad-code-org/bmad-method) for license terms.
