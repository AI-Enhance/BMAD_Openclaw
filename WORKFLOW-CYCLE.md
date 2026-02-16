# BMad Workflow Cycle

## Complete Implementation Cycle

```
Epic Start
    │
    ▼
┌─────────────────────────────────────────────────────────────┐
│                    FOR EACH STORY                            │
│                                                              │
│   ┌─────────────┐                                           │
│   │create-story │ → Creates story.md, updates sprint-status │
│   │             │   First story also sets epic: in-progress │
│   └─────┬───────┘                                           │
│         │                                                    │
│         ▼                                                    │
│   ┌─────────────┐                                           │
│   │ dev-story   │ → Implements code (red-green-refactor)    │
│   │             │   Updates story status: in-progress→review│
│   └─────┬───────┘                                           │
│         │                                                    │
│         ▼                                                    │
│   ┌─────────────┐                                           │
│   │ code-review │ → Reviews implementation                  │
│   │             │   APPROVED → status: done                 │
│   │             │   CHANGES REQUESTED → status: in-progress │
│   └─────┬───────┘                                           │
│         │                                                    │
│         ▼                                                    │
│   ┌─────────────┐                                           │
│   │  (if fixes  │ → dev-story again with review follow-ups  │
│   │   needed)   │   Then back to code-review                │
│   └─────────────┘                                           │
│                                                              │
└─────────────────────────────────────────────────────────────┘
    │
    ▼ (when all stories done)
┌─────────────────┐
│  retrospective  │ → Reviews epic, extracts learnings
│                 │   Updates epic-X-retrospective: done
│                 │   Uses Party Mode for team discussion
└─────────────────┘
    │
    ▼
Next Epic (or project complete)
```

## Status Transitions

### Epic Status
```
backlog → in-progress → done
         (first story   (all stories done)
          created)
```

### Story Status
```
backlog → ready-for-dev → in-progress → review → done
          (create-story)   (dev-story)   (dev)    (code-review APPROVED)
                                 │                      │
                                 └──────────────────────┘
                                 (code-review CHANGES REQUESTED)
```

### Retrospective Status
```
optional ↔ done
```

## Files Modified by Each Workflow

### create-story
**Creates:**
- `{implementation_artifacts}/{story_key}.md` — Comprehensive story with Dev Notes, architecture requirements, previous story intelligence

**Updates:**
- `sprint-status.yaml`:
  - Story: `backlog` → `ready-for-dev`
  - Epic (if first story): `backlog` → `in-progress`

### dev-story
**Updates:**
- Story file:
  - Status: `ready-for-dev` → `in-progress` → `review`
  - Tasks/Subtasks checkboxes: `[ ]` → `[x]`
  - Dev Agent Record (model, debug log, completion notes)
  - File List (ALL new/modified/deleted files)
  - Change Log
- `sprint-status.yaml`:
  - Story: `ready-for-dev` → `in-progress` → `review`

**Critical Dev Rules:**
- Red-Green-Refactor cycle for each task
- Execute ALL tasks continuously — no pausing at "milestones"
- Mark task [x] ONLY when tests exist AND pass
- NEVER lie about test existence or passing

### code-review
**Updates:**
- Story file:
  - Adds "Senior Developer Review (AI)" section with findings
  - If CHANGES REQUESTED: Adds "Review Follow-ups (AI)" subsection under Tasks/Subtasks
  - Status: `review` → `done` (approved) OR `review` → `in-progress` (changes requested)
  - Change Log
- `sprint-status.yaml`:
  - Story: `review` → `done` OR `review` → `in-progress`

**Review Rules:**
- ADVERSARIAL — find 3-10 issues minimum
- Validate git reality vs story claims
- Exclude `_bmad/`, `.cursor/`, `.windsurf/`, `.claude/` folders

### retrospective
**Creates:**
- `{implementation_artifacts}/epic-{N}-retro-{date}.md` — Comprehensive retrospective with Party Mode dialogue

**Updates:**
- `sprint-status.yaml`:
  - `epic-{N}-retrospective`: `optional` → `done`

**Retro Features:**
- Deep story analysis (patterns across all stories)
- Previous retro integration (action item follow-through)
- Next epic preview with change detection
- Significant discovery alerts
- Critical readiness exploration
- NO TIME ESTIMATES — ever

### correct-course
**Creates:**
- `{planning_artifacts}/sprint-change-proposal-{date}.md`

**May Update:**
- Epics, PRD, Architecture, UX spec, sprint-status.yaml

### sprint-planning
**Creates/Updates:**
- `{implementation_artifacts}/sprint-status.yaml` — Complete tracking with all epics, stories, retrospectives

## Orchestrator Decision Tree

### When user says "next" or "continue":

```python
def decide_next_action():
    status = read_sprint_status()
    
    # Priority 1: Stories needing review follow-up
    for story in stories_in_progress:
        if has_review_followups(story):
            return spawn_dev_story(story)
    
    # Priority 2: Stories ready for review
    for story in stories_in_review:
        return spawn_code_review(story)
    
    # Priority 3: Stories in progress (interrupted)
    for story in stories_in_progress:
        return spawn_dev_story(story)
    
    # Priority 4: Stories ready for dev
    for story in stories_ready_for_dev:
        return spawn_dev_story(story)
    
    # Priority 5: Stories in backlog
    for story in stories_in_backlog:
        return spawn_create_story(story)
    
    # Priority 6: Epic complete, retro pending
    if all_stories_done(current_epic):
        if not retrospective_done(current_epic):
            return spawn_retrospective(current_epic)
        else:
            return "Epic complete. Ready for next epic."
    
    return "All work complete! 🎉"
```

### Context to include when spawning each agent:

1. **create-story**: epics.md, architecture.md, previous story learnings, sprint-status.yaml
2. **dev-story**: full story file, project-context.md, previous stories for patterns
3. **code-review**: story file, git status, actual code files, architecture for compliance
4. **retrospective**: all completed story files, sprint-status, architecture, previous retro

## Critical Rules

1. **Never skip create-story** — every story needs a comprehensive story file before dev
2. **Always run code-review** — never mark done without adversarial review
3. **Preserve sprint-status structure** — keep ALL comments, STATUS DEFINITIONS
4. **Handle review follow-ups** — dev-story must check for and prioritize [AI-Review] tasks
5. **Update epic status** — first story triggers `in-progress`
6. **Run retrospective** — required before starting next epic
7. **No time estimates** — AI has changed development speed fundamentals
