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
└─────────────────┘
    │
    ▼
Next Epic (or project complete)
```

## Status Transitions

### Epic Status
```
backlog → in-progress → done
         (first story)  (all stories done)
```

### Story Status
```
backlog → ready-for-dev → in-progress → review → done
          (create-story)   (dev-story)   (dev)    (code-review APPROVED)
                                 │                      │
                                 └──────────────────────┘
                                 (code-review CHANGES REQUESTED)
```

## Files Modified by Each Workflow

### create-story
**Creates:**
- `{implementation_artifacts}/{story_key}.md`

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
  - File List table
  - Change Log
- `sprint-status.yaml`:
  - Story: `ready-for-dev` → `in-progress` → `review`

### code-review
**Updates:**
- Story file:
  - Adds "Senior Developer Review (AI)" section
  - If CHANGES REQUESTED: Adds "Review Follow-ups (AI)" subsection
  - Status: `review` → `done` OR `review` → `in-progress`
  - Change Log
- `sprint-status.yaml`:
  - Story: `review` → `done` OR `review` → `in-progress`

### retrospective
**Creates:**
- `{implementation_artifacts}/epic-{N}-retrospective.md`

**Updates:**
- `sprint-status.yaml`:
  - `epic-{N}-retrospective`: `optional` → `done`

## Orchestrator Decision Tree

### When user says "next story" or "continue":

```python
def decide_next_action():
    status = read_sprint_status()
    
    # Check for stories needing review follow-up
    for story in stories_in_progress:
        if has_review_followups(story):
            return spawn_dev_story(story)  # Resume with follow-ups
    
    # Check for stories ready for review
    for story in stories_in_review:
        return spawn_code_review(story)
    
    # Check for stories ready for dev
    for story in stories_ready_for_dev:
        return spawn_dev_story(story)
    
    # Check for stories in backlog
    for story in stories_in_backlog:
        return spawn_create_story(story)
    
    # Check if epic complete
    if all_stories_done(current_epic):
        if not retrospective_done(current_epic):
            return spawn_retrospective(current_epic)
        else:
            return "Epic complete. Ready for next epic."
    
    return "All stories complete."
```

### When spawning each agent:

1. **create-story**: Include epics.md context, architecture.md, previous story learnings
2. **dev-story**: Include full story file, project-context.md, previous stories for patterns
3. **code-review**: Include story file, git status, actual code files to review
4. **retrospective**: Include all completed story files, architecture, learnings

## Critical Rules

1. **Never skip create-story** — every story needs a story file before dev
2. **Always run code-review** — never mark done without review
3. **Preserve sprint-status structure** — keep all comments, STATUS DEFINITIONS
4. **Handle review follow-ups** — dev-story must check for and prioritize [AI-Review] tasks
5. **Update epic status** — first story in epic triggers `in-progress`
6. **Run retrospective** — required before starting next epic
