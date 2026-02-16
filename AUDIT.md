# BMad OpenClaw Bridge — Audit Report

**Date:** 2026-02-16
**Auditor:** Automated comparison against [bmadcode/BMAD-METHOD](https://github.com/bmadcode/BMAD-METHOD)
**Official repo version:** v6 (cloned 2026-02-16)

---

## Summary

Our bridge has **12 agent prompts** covering the core implementation workflow. The official BMad Method v6 is significantly more sophisticated with structured YAML agent definitions, step-file workflow architecture, XML instruction files, detailed checklists, templates, and several agents/workflows we don't have.

**Our approach is fundamentally different:** We flatten BMad's interactive menu-driven agent system into standalone prompt files consumed by OpenClaw's `sessions_spawn`. This is a valid adaptation, not a bug — but we're missing substantial content.

---

## Gap Analysis

### 1. Missing Agents

| Official Agent | Status in Our Bridge |
|---|---|
| **Tech Writer (Paige)** — Documentation specialist with sidecar standards | ❌ Missing entirely |
| **Quick Flow Solo Dev (Barry)** — Rapid spec+dev for small changes | ❌ Missing entirely |
| **BMad Master** — Core orchestrator/knowledge custodian | ⚠️ Replaced by ORCHESTRATOR.md (OpenClaw extension) |

### 2. Missing Workflows

| Official Workflow | Status |
|---|---|
| **Research workflows** (market, domain, technical) | ❌ Missing — analyst can trigger 3 research types |
| **Create PRD** (12-step guided + validate + edit) | ⚠️ Our business-analyst is simplified single-pass |
| **Create UX Design** (14-step guided) | ⚠️ Our ux-designer is simplified single-pass |
| **Create Architecture** (8-step guided) | ⚠️ Our architect is simplified single-pass |
| **Create Epics & Stories** (4-step guided) | ⚠️ Our scrum-master is simplified single-pass |
| **Check Implementation Readiness** (6-step) | ⚠️ Our readiness-check exists but simpler |
| **Sprint Planning** (generates sprint-status.yaml) | ⚠️ Embedded in scrum-master prompt |
| **Sprint Status** (multi-mode status service) | ❌ Missing as standalone workflow |
| **Correct Course** (mid-sprint change management) | ❌ Missing entirely |
| **Quick Flow** (quick-spec + quick-dev) | ❌ Missing entirely |
| **Brainstorming** (multi-technique facilitation) | ❌ Missing entirely |
| **Party Mode** (multi-agent discussion) | ❌ Missing entirely |
| **Document Project** (brownfield analysis) | ❌ Missing entirely |
| **Generate Project Context** | ❌ Missing entirely |
| **Advanced Elicitation** | ❌ Missing entirely |
| **QA Automate** (test automation workflow) | ❌ Missing entirely |
| **Validate PRD** (13-step validation) | ❌ Missing entirely |

### 3. Missing Templates & Checklists

| Official Asset | Status |
|---|---|
| `product-brief.template.md` | ❌ Missing (our prompt generates ad-hoc) |
| `prd-template.md` | ❌ Missing |
| `ux-design-template.md` | ❌ Missing |
| `epics-template.md` | ❌ Missing |
| `readiness-report-template.md` | ❌ Missing |
| `architecture-decision-template.md` | ❌ Missing |
| `sprint-status-template.yaml` | ❌ Missing |
| `project-context-template.md` | ❌ Missing |
| `tech-spec-template.md` (quick flow) | ❌ Missing |
| Dev Story checklist (comprehensive DoD) | ⚠️ Our dev-story has basic quality gates |
| Code Review checklist | ⚠️ Our code-review has basic checklist |
| Create Story validation checklist | ❌ Missing |
| Sprint Planning checklist | ❌ Missing |
| Correct Course checklist | ❌ Missing |

### 4. Agent Persona Divergence

| Agent | Official | Ours |
|---|---|---|
| Product Owner / Analyst | **Mary** — Business Analyst with Porter's Five Forces, SWOT, treasure-hunter personality | Generic "Product Owner" without personality |
| Business Analyst / PM | **John** — Product Manager, detective personality, "WHY?" relentlessly | Generic "Business Analyst" |
| Architect | **Winston** — Calm, pragmatic, "boring technology" philosophy | Generic "Architect" — similar principles, no personality |
| UX Designer | **Sally** — "Paints pictures with words", empathetic advocate | Generic "UX Designer" — similar but flatter |
| Scrum Master | **Bob** — Certified SM, servant leader, checklist-driven | Generic "Scrum Master" — similar |
| Developer | **Amelia** — Ultra-succinct, file paths and AC IDs | ✅ We have Amelia! Good match |
| QA | **Quinn** — Pragmatic, "ship it and iterate" | Generic "QA Tester" — similar intent |

### 5. Structural Differences

| Feature | Official | Ours |
|---|---|---|
| Agent format | YAML with metadata, persona, menu, critical_actions | Markdown prompt files |
| Workflow execution | Step-file architecture with XML instructions | Single-pass prompt execution |
| Interactive flow | Menu-driven with fuzzy trigger matching | Command-based via orchestrator |
| State tracking | Frontmatter `stepsCompleted` arrays | File-based status tracking |
| Configuration | `module.yaml`, `team-fullstack.yaml`, manifests | Single project YAML config |
| Validation | Built-in validate workflows (PRD, story) | No validation workflows |

### 6. OpenClaw Extensions (Not in Official)

| Feature | Description |
|---|---|
| **ORCHESTRATOR.md** | Master orchestrator using `sessions_spawn` — replaces BMad Master's interactive menu with autonomous sub-agent management |
| **WORKFLOW-CYCLE.md** | Visual workflow cycle documentation with status transitions and decision trees |
| **UX Review agent** | Dedicated UX review as separate agent (official bundles this into UX Designer) |
| **HALT-based flow control** | Sub-agents HALT and orchestrator decides (vs interactive ask/wait) |
| **Auto-continue logic** | Priority-based next-action decision tree |
| **Retry logic** | Max 2 retries with failure context |

---

## Fixes Applied

### Phase 1: Add missing agents
- [x] Added `prompts/tech-writer.md` — ported from Paige (tech-writer.agent.yaml)
- [x] Added `prompts/quick-flow.md` — ported from Barry (quick-flow-solo-dev.agent.yaml)

### Phase 2: Add missing templates
- [x] Added `templates/product-brief.md`
- [x] Added `templates/prd.md`
- [x] Added `templates/architecture-decision.md`
- [x] Added `templates/epics.md`
- [x] Added `templates/ux-design.md`
- [x] Added `templates/sprint-status.yaml`
- [x] Added `templates/story.md`
- [x] Added `templates/readiness-report.md`

### Phase 3: Add missing checklists
- [x] Added `checklists/dev-story-dod.md` — Definition of Done
- [x] Added `checklists/code-review.md` — Review validation
- [x] Added `checklists/create-story-validation.md` — Story quality

### Phase 4: Add missing workflows
- [x] Added `prompts/correct-course.md` — Mid-sprint change management
- [x] Added `prompts/sprint-status.md` — Sprint status reporting

### Phase 5: Enrich agent personas
- [x] Updated all agent prompts with official personas (names, personalities, principles)

### Phase 6: Update documentation
- [x] Updated README.md with BMad vs OpenClaw distinction
- [x] Updated ORCHESTRATOR.md with new agents and workflows
- [x] Updated config/slyd.yaml with new agent entries

---

## Not Ported (By Design)

These official features are **intentionally not ported** because they don't fit the OpenClaw `sessions_spawn` model:

1. **Step-file architecture** — Our prompts are single-pass by design (sub-agents run autonomously)
2. **Interactive menus** — Replaced by orchestrator command routing
3. **XML instruction files** — Converted to markdown prompts
4. **Fuzzy trigger matching** — Replaced by natural language commands to orchestrator
5. **Party Mode** — Multi-agent discussion doesn't map to isolated sub-agents
6. **Brainstorming workflow** — Interactive by nature, better done in main session
7. **Advanced Elicitation** — Interactive technique, main session activity
8. **CLI tooling** — BMad has npx installer, IDE configs — not relevant to OpenClaw
9. **Module system** — BMad's core/bmm module split not needed for flat prompt structure
