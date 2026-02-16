# DIFF-REPORT: Exact Alignment with Official BMad Method v6

**Date:** 2026-02-16
**Scope:** All agent prompts, orchestrator, workflow cycle, checklists

---

## Summary

Every agent prompt in `bmad-openclaw/prompts/` has been rewritten to align with the official BMad Method repository at `github.com/BMad-code-org/bmad-method` (v6). The official repo uses a micro-file architecture (YAML agent definitions + step files + instruction XML/MD + checklists + templates). Our OpenClaw adaptation preserves the same behavior, steps, checklists, and validation rules while adapting the execution mechanism to `sessions_spawn`.

---

## Agent-by-Agent Alignment

### product-owner.md (Mary — Business Analyst)
**Official sources:** `analyst.agent.yaml`, `workflows/1-analysis/create-product-brief/workflow.md`, `steps/step-01-init.md` through `step-06-complete.md`, `product-brief.template.md`
**Was missing:**
- Full 6-step workflow architecture with step-file discipline (micro-file design, JIT loading, sequential enforcement)
- Step 1: Initialization with continuation detection (step-01b-continue.md)
- Step 1: Input document discovery with sharded document handling
- Step 2: Vision discovery (problem understanding, current solutions analysis, differentiators)
- Step 3: Target users with rich persona development and journey mapping
- Step 4: Success metrics with user success, business objectives, KPIs
- Step 5: MVP scope with out-of-scope boundaries and success criteria
- Step 6: Completion with quality validation and next-step guidance
- Menu system ([A] Advanced Elicitation, [P] Party Mode, [C] Continue) at each step
- Success/failure metrics per step
- Append-only document building with frontmatter state tracking
**Added:** All 6 steps with full content, continuation support, quality gates
**Confirmed aligned:** ✅

### business-analyst.md (John — Product Manager)
**Official sources:** `pm.agent.yaml`, `workflows/2-plan-workflows/create-prd/workflow-create-prd.md`, `steps-c/step-01-init.md` through `step-12-complete.md`, `workflow-validate-prd.md`, `workflow-edit-prd.md`
**Was missing:**
- Full 12-step PRD creation workflow (was simplified to 9 generic steps)
- Steps 5-7: Domain model, innovation/differentiation, project type classification
- Step 8: Scoping with MoSCoW framework
- Steps 9-10: Separate functional and non-functional requirements
- Step 11: Polish & coherence review
- Validate PRD workflow (13-step validation with density, measurability, traceability, implementation leakage, domain compliance, SMART, holistic quality checks)
- Edit PRD workflow
- Step-file architecture with continuation support
**Added:** All 12 creation steps, validate/edit workflow references
**Confirmed aligned:** ✅

### architect.md (Winston)
**Official sources:** `architect.agent.yaml`, `workflows/3-solutioning/create-architecture/workflow.md`, `steps/step-01-init.md` through `step-08-complete.md`, `data/domain-complexity.csv`, `data/project-types.csv`
**Was missing:**
- Full 8-step workflow (was simplified)
- Step 2: Context & requirements analysis with domain complexity assessment
- Step 3: Technology starter selection (not just listing stack)
- Step 4: Formal ADR creation process
- Step 5: Architecture patterns (service architecture, data access, caching, error handling, security, integration)
- Step 7: Validation & review cross-referencing against PRD
- Implementation Readiness Check workflow reference (6-step adversarial validation)
- Step-file architecture with continuation support
**Added:** All 8 steps, readiness check reference, domain complexity
**Confirmed aligned:** ✅

### ux-designer.md (Sally)
**Official sources:** `ux-designer.agent.yaml`, `workflows/2-plan-workflows/create-ux-design/workflow.md`, `steps/step-01-init.md` through `step-14-complete.md`, `ux-design-template.md`
**Was missing:**
- Full 14-step workflow (was 10 simplified steps)
- Step 3: Core experience definition
- Step 4: Emotional response mapping
- Step 5: Inspiration & references
- Step 7: Defining the experience (interaction principles, feedback patterns)
- Step 8: Visual foundation (hierarchy, grid, layouts)
- Step 9: Design directions (2-3 options for user choice)
- Step 10: UX-specific user journeys
- Step 12: UX patterns (form submission, data loading, modals, toasts)
- Step-file architecture with continuation support
**Added:** All 14 steps with full detail
**Confirmed aligned:** ✅

### scrum-master.md (Bob)
**Official sources:** `sm.agent.yaml`, `workflows/3-solutioning/create-epics-and-stories/workflow.md`, `steps/step-01-validate-prerequisites.md` through `step-04-final-validation.md`, `templates/epics-template.md`, `workflows/4-implementation/sprint-planning/workflow.yaml`, `instructions.md`, `checklist.md`, `sprint-status-template.yaml`
**Was missing:**
- Create Epics workflow with 4-step step-file architecture
- Step 1: Validate prerequisites (require PRD + Architecture, recommend UX)
- Step 4: Final validation (traceability matrix, no technical epics, no forward dependencies)
- Sprint Planning workflow with full status state machine
- Sprint status generation with dual metadata (comments + YAML fields)
- Status detection from existing story files
- Retrospective and Correct Course menu entries
- User-value epic organization enforcement
**Added:** Both workflows with full steps, status state machine, validation
**Confirmed aligned:** ✅

### readiness-check.md
**Official sources:** `workflows/3-solutioning/check-implementation-readiness/workflow.md`, `steps/step-01-document-discovery.md` through `step-06-final-assessment.md`, `templates/readiness-report-template.md`
**Was missing:**
- Full 6-step workflow (was simplified to generic checklist)
- Step 1: Document discovery with sharded document handling and duplicate resolution
- Step 2: PRD analysis extracting ALL FRs and NFRs with IDs
- Step 3: Epic coverage validation with traceability matrix (FR → Story mapping)
- Step 4: UX alignment checking architecture support for UX requirements
- Step 5: Epic quality review (technical epic detection, forward dependency detection, story quality)
- Step 6: Final assessment with categorized findings and GO/NO-GO/CONDITIONAL
**Added:** All 6 steps with traceability matrix, quality enforcement
**Confirmed aligned:** ✅

### create-story.md
**Official sources:** `workflows/4-implementation/create-story/workflow.yaml`, `instructions.xml`, `checklist.md`, `template.md`
**Was missing:**
- Critical mission statement (prevent LLM developer mistakes)
- Step 1: Full story discovery with sprint-status parsing (auto-discover OR user-specified)
- Step 1: Epic in-progress marking logic (first story triggers)
- Step 1: Error handling for completed epics, invalid statuses
- Step 2: Exhaustive artifact analysis (not just loading)
- Step 2: Previous story intelligence extraction
- Step 2: Git intelligence for work patterns
- Step 3: Architecture analysis with 9 specific extraction categories
- Step 4: Web research for latest technical specifics
- Step 5: Template-based story creation with all sections
- Step 6: Validation checklist integration
- Zero user intervention goal
- Subprocess/subagent utilization directive
**Added:** All 6 steps with exhaustive analysis, validation checklist
**Confirmed aligned:** ✅

### dev-story.md (Amelia)
**Official sources:** `dev.agent.yaml`, `workflows/4-implementation/dev-story/workflow.yaml`, `instructions.xml`, `checklist.md`
**Was missing:**
- Critical actions from agent definition (8 critical directives)
- Step 1: Full sprint-based story discovery with fallback to file-based
- Step 2: Project context loading emphasis
- Step 3: Review continuation detection (resume after code review with follow-up prioritization)
- Step 4: Sprint status in-progress marking with error handling
- Steps 5-8: Detailed red-green-refactor with validation gates
- Step 8: Review follow-up handling ([AI-Review] task resolution with dual marking)
- Step 9: Enhanced Definition of Done validation (full checklist)
- Step 10: User communication with skill-level-appropriate explanations
- Continuous execution mandate (no pausing at milestones)
- File update cadence (save after each task, not batched)
**Added:** All 10 steps with DoD checklist, review continuation, continuous execution
**Confirmed aligned:** ✅

### code-review.md
**Official sources:** `workflows/4-implementation/code-review/workflow.yaml`, `instructions.xml`, `checklist.md`
**Was missing:**
- Step 1: Git discovery cross-referencing (git status vs story File List)
- Step 2: Attack plan with 4 review categories
- Step 3: Adversarial review with minimum issue requirement (re-examine if < 3)
- Step 4: Interactive fix options (fix automatically, create action items, show details)
- Step 5: Sprint status sync with conditional done/in-progress
- Folder exclusion list (_bmad/, .cursor/, .windsurf/, .claude/)
- Git commit after review with appropriate message
**Added:** All 5 steps with git verification, interactive fixing, sprint sync
**Confirmed aligned:** ✅

### correct-course.md
**Official sources:** `workflows/4-implementation/correct-course/workflow.yaml`, `instructions.md`, `checklist.md`
**Was missing:**
- Full 6-step workflow (was simplified to 5 generic steps)
- Step 2: Complete 6-section change analysis checklist (25 check items)
  - Section 1: Trigger and context (3 items)
  - Section 2: Epic impact assessment (5 items)
  - Section 3: Artifact conflict analysis (4 items)
  - Section 4: Path forward evaluation (4 items with effort/risk)
  - Section 5: Sprint change proposal components (5 items)
  - Section 6: Final review and handoff (5 items)
- Step 3: Specific edit proposals with old→new format
- Step 4: Sprint Change Proposal document generation
- Step 5: Implementation routing (Minor/Moderate/Major scope)
- Incremental vs Batch mode selection
- Sprint-status.yaml update for approved changes
**Added:** All 6 steps with complete checklist, proposal document, routing
**Confirmed aligned:** ✅

### retrospective.md
**Official sources:** `workflows/4-implementation/retrospective/workflow.yaml`, `instructions.md`
**Was missing:**
- Full 12-step workflow (was simplified to 7 steps)
- Step 1: Epic discovery with priority logic (sprint-status → user → file scan)
- Step 2: Deep story analysis (dev notes, review feedback, lessons, tech debt, testing across ALL stories)
- Step 3: Previous retro integration with action item follow-through tracking
- Step 4: Next epic preview with change detection
- Step 5: Rich context initialization with delivery metrics
- Step 6: Interactive Party Mode discussion (successes → challenges → patterns)
- Step 7: Next epic preparation with technical/business tension exploration
- Step 8: SMART action items with significant change detection alert
- Step 9: Critical readiness exploration (testing, deployment, stakeholder, stability, blockers)
- Step 10: Closure with celebration
- Step 11: Save and update sprint status
- Step 12: Final summary and handoff
- NO TIME ESTIMATES rule
- Party Mode protocol ("Name (Role): dialogue" format)
**Added:** All 12 steps with Party Mode, change detection, readiness exploration
**Confirmed aligned:** ✅

### sprint-status.md
**Official sources:** `workflows/4-implementation/sprint-status/workflow.yaml`, `instructions.md`
**Was missing:**
- Multi-mode service (interactive/validate/data)
- Step 2: Legacy status mapping (drafted→ready-for-dev, contexted→in-progress)
- Step 2: Status validation against known values with correction prompt
- Step 2: Risk detection (7 specific risk checks)
- Step 3: Priority-ordered next action recommendation
- Step 5: Interactive options (run recommended, show by status, show raw, exit)
- Step 20: Data mode for other workflows
- Step 30: Validate mode with metadata field checking
- No time estimates rule
**Added:** All modes with risk detection, validation, interactive options
**Confirmed aligned:** ✅

### quick-flow.md (Barry)
**Official sources:** `quick-flow-solo-dev.agent.yaml`, `workflows/bmad-quick-flow/quick-spec/workflow.md`, `quick-spec/steps/step-01-understand.md` through `step-04-review.md`, `quick-dev/workflow.md`, `quick-dev/steps/step-01-mode-detection.md` through `step-06-resolve-findings.md`
**Was missing:**
- Quick Spec: "Ready for Development" standard definition (5 criteria)
- Quick Spec: Step 4 with self-review checklist
- Quick Dev: Step 1 mode detection (tech-spec vs direct instructions)
- Quick Dev: Step 4 self-check with specific checklist
- Quick Dev: Step 5 adversarial self-review
- Quick Dev: Step 6 resolve findings
- Step-file architecture references
- Code Review menu entry reference
**Added:** Both workflows with all steps, standards, self-review
**Confirmed aligned:** ✅

### qa-tester.md (Quinn)
**Official sources:** `qa.agent.yaml`, `workflows/qa/automate/workflow.yaml`, `instructions.md`, `checklist.md`
**Was missing:**
- Welcome message with capability description
- Step 0: Test framework detection (auto-detect from project)
- Validation checklist (test generation, quality, output sections)
- "Keep It Simple" guidance
- TEA (Test Architect Enterprise) module reference
- Simplified scope clarification (generates tests ONLY, not review)
**Added:** All steps with welcome, framework detection, checklist, TEA reference
**Confirmed aligned:** ✅

### tech-writer.md (Paige)
**Official sources:** `tech-writer/tech-writer.agent.yaml`, `tech-writer-sidecar/documentation-standards.md`
**Was missing:**
- All 6 menu workflows: [DP] Document Project, [WD] Write Document, [US] Update Standards, [MG] Mermaid Generate, [VD] Validate Documentation, [EC] Explain Concept
- Sidecar reference (documentation-standards.md)
- Document Project sub-workflows (full scan, deep dive)
- hasSidecar: true flag
**Added:** All 6 workflows with descriptions, sidecar reference
**Confirmed aligned:** ✅

### ux-review.md
**Official sources:** No dedicated agent — UX review is a workflow. Preserved as-is with alignment to overall BMad patterns.
**Status:** Already well-aligned. Minor formatting improvements.
**Confirmed aligned:** ✅

---

## ORCHESTRATOR.md Changes

**Was missing:**
- Phase 1 (Analysis) and Phase 3 (Solutioning) distinction — was lumped as "Planning"
- Correct agent-to-official-BMad mapping (Mary=analyst, John=pm, etc.)
- Sprint Planning as separate workflow entry
- Correct course and sprint status as utility workflows
- Validate PRD command
- "contexted" and "drafted" as legacy status values to avoid

**Added:** 4-phase structure, complete agent mapping table, all commands, legacy status warnings

---

## WORKFLOW-CYCLE.md Changes

**Was missing:**
- Retrospective Party Mode mention
- Code review folder exclusions
- Dev story continuous execution mandate
- Comprehensive context-to-include guidance per agent
- No time estimates rule
- Retrospective features list (deep analysis, previous retro integration, change detection)

**Added:** All above details

---

## Checklists Updated

- `create-story-validation.md` — Aligned with official checklist.md (5 sections, LLM optimization)
- `dev-story-dod.md` — Aligned with official DoD checklist (5 sections, 25 items)
- `code-review.md` — Aligned with official review checklist (19 items including adversarial minimum)
