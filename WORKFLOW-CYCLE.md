# BMad Method Workflow Cycle

This documents the complete BMad Method workflow cycle as defined in the official repository, with OpenClaw execution notes.

## Phase 1: Analysis (Analyst Agent — Mary 📊)

**Goal:** Understand the problem space, research the market, and create an executive product brief.

### Workflows

1. **Brainstorm Project (BP)** — Expert guided facilitation through brainstorming techniques with a final report
2. **Market Research (MR)** — Market analysis, competitive landscape, customer needs and trends
3. **Domain Research (DR)** — Industry domain deep dive, subject matter expertise and terminology
4. **Technical Research (TR)** — Technical feasibility, architecture options and implementation approaches
5. **Create Product Brief (CB)** — Guided experience to nail down your product idea into an executive brief
6. **Document Project (DP)** — Analyze an existing project to produce useful documentation (also available via Tech Writer)

### Output Artifacts
- Research reports (market, domain, technical)
- Product Brief
- Brainstorming report

> **OpenClaw:** Spawn `bmad-analyst` and use trigger codes (BP, MR, DR, TR, CB, DP).

---

## Phase 2: Planning (PM Agent — John 📋 + UX Designer — Sally 🎨)

**Goal:** Transform the product brief into detailed requirements and UX specifications.

### Workflows

1. **Create PRD (CP)** — Expert led facilitation to produce your Product Requirements Document
2. **Validate PRD (VP)** — Validate PRD is comprehensive, lean, well organized and cohesive
3. **Edit PRD (EP)** — Update an existing Product Requirements Document
4. **Create UX Design (CU)** — Guided UX design specification for architecture and implementation
5. **Create Epics and Stories (CE)** — Create the Epics and Stories listing that drives development

### Output Artifacts
- Product Requirements Document (PRD)
- UX Design Specification
- Epics and Stories document

> **OpenClaw:** Spawn `bmad-pm` for PRD/Epics work, `bmad-ux` for UX design.

---

## Phase 3: Solutioning (Architect — Winston 🏗️ + PM — John 📋)

**Goal:** Define technical architecture and validate implementation readiness.

### Workflows

1. **Create Architecture (CA)** — Guided workflow to document technical decisions
2. **Implementation Readiness (IR)** — Ensure PRD, UX, Architecture and Epics/Stories are all aligned

### Output Artifacts
- Architecture Decision Document
- Implementation Readiness Report

> **OpenClaw:** Spawn `bmad-architect` for architecture, either agent for readiness check.

---

## Phase 4: Implementation (SM — Bob 🏃 + Dev — Amelia 💻 + QA — Quinn 🧪)

**Goal:** Execute the plan through agile sprint cycles.

### Workflows

1. **Sprint Planning (SP)** — Generate sprint-status.yaml tracking file from epics
2. **Create Story (CS)** — Prepare a story with comprehensive context for the developer agent
3. **Dev Story (DS)** — Implement a story's tasks/subtasks with TDD, updating the story file
4. **Code Review (CR)** — Adversarial review finding 3-10 specific issues per story
5. **Sprint Status** — Summarize sprint progress and recommend next workflow
6. **Epic Retrospective (ER)** — Party Mode review of completed epic with all agents
7. **Course Correction (CC)** — Navigate significant mid-sprint changes
8. **QA Automate (QA)** — Generate tests for existing features

### Implementation Cycle

```
Sprint Planning (SP) → Create Story (CS) → Dev Story (DS) → Code Review (CR) → [next story or Retrospective (ER)]
```

### Status State Machine

**Epic:** `backlog` → `in-progress` → `done`
**Story:** `backlog` → `ready-for-dev` → `in-progress` → `review` → `done`
**Retrospective:** `optional` ↔ `done`

> **OpenClaw:** Spawn `bmad-sm` for planning/stories, `bmad-dev` for implementation/review, `bmad-qa` for test generation.

---

## Quick Flow (Solo Dev — Barry 🚀)

**Goal:** Rapid spec-to-implementation for smaller features with minimum ceremony.

### Workflows

1. **Quick Spec (QS)** — Conversational spec engineering producing implementation-ready tech specs
2. **Quick Dev (QD)** — Implement tech spec or direct instructions end-to-end
3. **Code Review (CR)** — Same adversarial review as Phase 4

### Quick Flow Cycle

```
Quick Spec (QS) → Quick Dev (QD) → Code Review (CR)
```

> **OpenClaw:** Spawn `bmad-quick-flow` for the complete quick flow cycle.

---

## Cross-Cutting Capabilities

### Advanced Elicitation
Available at any template-output checkpoint — deeper exploration of a topic using structured techniques.

### Party Mode
Multi-agent discussion simulation available at template-output checkpoints. Agents debate and collaborate on the current topic.

### Document Sharding
Large documents can be split into smaller files with an index.md for manageable loading.

### Project Context
A project-context.md file provides coding standards and project-wide patterns to all agents.
