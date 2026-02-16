# Changes — Full Rebuild from Official BMad Repo

**Date:** 2026-02-16
**Source:** https://github.com/bmad-code-org/bmad-method (cloned to `/tmp/bmad-official/`)

## What Was Done

Complete rebuild of the BMad-OpenClaw bridge by reading every file in the official BMad repository and creating faithful adaptations for OpenClaw.

## Mapping: Official BMad → OpenClaw Bridge

### Agents

| Official Source | OpenClaw File | Notes |
|----------------|---------------|-------|
| `src/bmm/agents/analyst.agent.yaml` | `agents/ANALYST.md` | Full persona + menu + workflow descriptions |
| `src/bmm/agents/architect.agent.yaml` | `agents/ARCHITECT.md` | Full persona + menu + workflow descriptions |
| `src/bmm/agents/pm.agent.yaml` | `agents/PM.md` | Full persona + menu + all 6 workflow descriptions |
| `src/bmm/agents/dev.agent.yaml` | `agents/DEV.md` | Full persona + critical_actions + dev-story & code-review workflows |
| `src/bmm/agents/sm.agent.yaml` | `agents/SCRUM-MASTER.md` | Full persona + sprint-planning, create-story, retrospective, course-correction |
| `src/bmm/agents/ux-designer.agent.yaml` | `agents/UX-DESIGNER.md` | Full persona + UX design workflow |
| `src/bmm/agents/qa.agent.yaml` | `agents/QA.md` | Full persona + welcome message + QA automate workflow |
| `src/bmm/agents/tech-writer/tech-writer.agent.yaml` + sidecar | `agents/TECH-WRITER.md` | Full persona + documentation standards sidecar |
| `src/bmm/agents/quick-flow-solo-dev.agent.yaml` | `agents/QUICK-FLOW.md` | Full persona + quick-spec & quick-dev workflows |
| `src/core/agents/bmad-master.agent.yaml` | `agents/BMAD-MASTER.md` | Full persona + agent roster + phase overview |

### Templates (Verbatim Copies)

| Official Source | OpenClaw File |
|----------------|---------------|
| `src/bmm/workflows/4-implementation/create-story/template.md` | `templates/story-template.md` |
| `src/bmm/workflows/4-implementation/sprint-planning/sprint-status-template.yaml` | `templates/sprint-status-template.yaml` |
| `src/bmm/workflows/2-plan-workflows/create-prd/templates/prd-template.md` | `templates/prd-template.md` |
| `src/bmm/workflows/3-solutioning/create-epics-and-stories/templates/epics-template.md` | `templates/epics-template.md` |
| `src/bmm/workflows/3-solutioning/create-architecture/architecture-decision-template.md` | `templates/architecture-decision-template.md` |
| `src/bmm/workflows/2-plan-workflows/create-ux-design/ux-design-template.md` | `templates/ux-design-template.md` |
| `src/bmm/workflows/1-analysis/create-product-brief/product-brief.template.md` | `templates/product-brief-template.md` |
| `src/bmm/data/project-context-template.md` | `templates/project-context-template.md` |
| `src/bmm/workflows/3-solutioning/check-implementation-readiness/templates/readiness-report-template.md` | `templates/readiness-report-template.md` |
| `src/bmm/workflows/1-analysis/research/research.template.md` | `templates/research-template.md` |
| `src/core/workflows/brainstorming/template.md` | `templates/brainstorming-template.md` |
| `src/bmm/workflows/bmad-quick-flow/quick-spec/tech-spec-template.md` | `templates/tech-spec-template.md` |

### Checklists (Verbatim Copies)

| Official Source | OpenClaw File |
|----------------|---------------|
| `src/bmm/workflows/4-implementation/code-review/checklist.md` | `checklists/code-review-checklist.md` |
| `src/bmm/workflows/4-implementation/correct-course/checklist.md` | `checklists/correct-course-checklist.md` |
| `src/bmm/workflows/4-implementation/create-story/checklist.md` | `checklists/create-story-checklist.md` |
| `src/bmm/workflows/4-implementation/dev-story/checklist.md` | `checklists/dev-story-checklist.md` |
| `src/bmm/workflows/4-implementation/sprint-planning/checklist.md` | `checklists/sprint-planning-checklist.md` |
| `src/bmm/workflows/qa/automate/checklist.md` | `checklists/qa-automate-checklist.md` |
| `src/bmm/workflows/document-project/checklist.md` | `checklists/document-project-checklist.md` |

### Workflow Documentation

| Official Concept | OpenClaw File |
|-----------------|---------------|
| Workflow execution engine (`src/core/tasks/workflow.xml`) | `ORCHESTRATOR.md` — execution rules + OpenClaw spawn notes |
| BMad Method phases (derived from agent menus + workflow structure) | `WORKFLOW-CYCLE.md` — complete phase-by-phase guide |

## What Changed vs. Official

1. **Agent YAML → Agent Markdown**: Each `.agent.yaml` was converted to a self-contained `.md` file with an OpenClaw invocation header. The YAML definition is preserved as a code block.

2. **Workflow instructions embedded in agent files**: Instead of referencing separate step files via file paths, key workflow steps and critical rules are summarized within each agent's `.md` file. The full step files exist in the official repo but are too numerous to include individually.

3. **Templates and checklists are verbatim copies** from the official repo — no modifications.

4. **OpenClaw adaptation is minimal**: Only a 2-line header on each agent file explaining how to invoke via `sessions_spawn`.

## What's NOT Included

- Individual step files (e.g., `steps/step-01-init.md` through `step-14-complete.md` for each workflow) — there are 100+ of these. The agent `.md` files contain the key workflow logic.
- CLI tooling, IDE installer scripts, validation tools
- Website files, test fixtures
- GitHub workflows, CI/CD configuration
- Module configuration system (`config.yaml` generation)
