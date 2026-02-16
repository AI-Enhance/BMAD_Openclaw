# BMad for OpenClaw

Adaptation of the [BMad Method](https://github.com/bmadcode/BMAD-METHOD) (v6) for OpenClaw's `sessions_spawn` architecture.

## What is BMad?

The **BMad Method** is a structured AI-agent workflow for software development, created by [bmadcode](https://github.com/bmadcode). It defines specialized agents (Analyst, PM, Architect, UX Designer, Scrum Master, Developer, QA) that collaborate through a phased workflow: Analysis → Planning → Solutioning → Implementation.

## What is This Bridge?

This repo adapts BMad's interactive, menu-driven agent system into **standalone prompt files** consumed by OpenClaw's `sessions_spawn` capability. Each agent runs as an isolated sub-agent, managed by a main-session orchestrator.

## Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                    Main Session (Orchestrator)               │
│  • Always responsive to user                                 │
│  • Spawns sub-agents for heavy work                          │
│  • Handles HALT conditions and retries                       │
└─────────────────────────────────────────────────────────────┘
                              │
                    sessions_spawn
                              │
         ┌────────────────────┼────────────────────┐
         ▼                    ▼                    ▼
┌─────────────────┐  ┌─────────────────┐  ┌─────────────────┐
│  Agent Prompts  │  │  Agent Prompts  │  │  Agent Prompts  │
│  (isolated)     │  │  (isolated)     │  │  (isolated)     │
└─────────────────┘  └─────────────────┘  └─────────────────┘
```

## File Structure

```
bmad-openclaw/
├── README.md                       # This file
├── ORCHESTRATOR.md                 # Master orchestrator instructions
├── WORKFLOW-CYCLE.md               # Implementation cycle with status transitions
├── AUDIT.md                        # Gap analysis vs official BMad repo
├── prompts/                        # Agent prompt files
│   ├── product-owner.md            # Mary — Product Brief creation
│   ├── business-analyst.md         # John — PRD creation
│   ├── architect.md                # Winston — Architecture decisions
│   ├── ux-designer.md              # Sally — UX Design specification
│   ├── scrum-master.md             # Bob — Epics, stories, sprint planning
│   ├── readiness-check.md          # Implementation readiness GO/NO-GO
│   ├── create-story.md             # Story file creation from epics
│   ├── dev-story.md                # Amelia — Story implementation (RGR)
│   ├── code-review.md              # Adversarial code review
│   ├── ux-review.md                # UX validation against spec
│   ├── qa-tester.md                # Quinn — Functional testing
│   ├── retrospective.md            # Epic retrospective
│   ├── tech-writer.md              # Paige — Documentation specialist
│   ├── quick-flow.md               # Barry — Quick spec+dev for small tasks
│   ├── correct-course.md           # Mid-sprint change management
│   └── sprint-status.md            # Sprint status reporting
├── templates/                      # Output templates
│   ├── product-brief.md
│   ├── prd.md
│   ├── architecture-decision.md
│   ├── epics.md
│   ├── ux-design.md
│   ├── story.md
│   ├── sprint-status.yaml
│   └── readiness-report.md
├── checklists/                     # Validation checklists
│   ├── dev-story-dod.md            # Definition of Done
│   ├── code-review.md              # Review validation
│   └── create-story-validation.md  # Story quality check
├── config/
│   └── slyd.yaml                   # Example project configuration
└── docs/
    └── bmad-openclaw-synthesis.*    # Architecture documentation
```

## Agents — BMad Origins

| Agent | BMad Name | Role | Official Source |
|-------|-----------|------|----------------|
| product-owner | Mary (Analyst) | Product Brief creation | `analyst.agent.yaml` |
| business-analyst | John (PM) | PRD creation | `pm.agent.yaml` |
| architect | Winston | Architecture decisions | `architect.agent.yaml` |
| ux-designer | Sally | UX Design specification | `ux-designer.agent.yaml` |
| scrum-master | Bob (SM) | Epics, stories, sprint planning | `sm.agent.yaml` |
| dev-story | Amelia (Dev) | Story implementation | `dev.agent.yaml` |
| qa-tester | Quinn (QA) | Testing | `qa.agent.yaml` |
| tech-writer | Paige | Documentation | `tech-writer.agent.yaml` |
| quick-flow | Barry | Quick spec+dev | `quick-flow-solo-dev.agent.yaml` |

## OpenClaw Extensions (Not in Official BMad)

These features are specific to the OpenClaw bridge:

| Feature | Description |
|---------|-------------|
| **ORCHESTRATOR.md** | Autonomous orchestrator using `sessions_spawn` (replaces BMad Master's interactive menu) |
| **WORKFLOW-CYCLE.md** | Visual status transitions and decision trees |
| **UX Review agent** | Dedicated UX review agent (official bundles into UX Designer) |
| **HALT-based flow** | Sub-agents HALT → orchestrator decides (vs interactive ask/wait) |
| **Auto-continue** | Priority-based next-action logic |
| **Retry logic** | Max 2 retries with failure context |
| **correct-course** | Mid-sprint change navigator |
| **sprint-status** | Standalone status reporting agent |

## Not Ported (By Design)

These official features don't fit the `sessions_spawn` model:

- **Step-file architecture** — Our prompts are single-pass autonomous agents
- **Interactive menus** — Replaced by orchestrator command routing
- **Party Mode** — Multi-agent discussion doesn't map to isolated sub-agents
- **Brainstorming/Elicitation** — Interactive by nature, done in main session
- **CLI/IDE tooling** — npx installer, IDE configs not relevant to OpenClaw

## Usage

See [ORCHESTRATOR.md](./ORCHESTRATOR.md) for commands and workflow details.

## License

BMad Method is © bmadcode. This bridge is an independent adaptation for OpenClaw.
