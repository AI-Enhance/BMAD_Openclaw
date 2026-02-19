# ARCHITECTURE_RECOMMENDATION

## Section 1: Framework Ratings (1–100 scale)

### 1) Current AIEnhance system (as-is before redesign)
**Score: 41/100**

**Strengths**
- Clear role intent exists (planning, dev, QA, review, devops) across SOUL/BMAD prompts.
- Good process language (readiness checks, adversarial review, retrospectives).
- Flexible multi-agent setup for rapid iteration.

**Weaknesses**
- Critical gates are mostly advisory, not mechanically enforced (CI/branch protections not hard-wired).
- Policy drift across SOUL.md vs AGENTS.md creates execution inconsistency.
- Proven production failures from missing dependency/import/build/config checks.

**Best for**
- Fast experimentation where outage risk is acceptable and a human is actively supervising.

### 2) BMAD original (bmadcode/BMAD-METHOD v6)
**Score: 78/100**

**Strengths**
- Strong spec-first artifact chain (PRD → architecture → epics/stories → implementation context).
- High-quality role decomposition and adversarial review posture.
- Readiness and definition-of-done checklists reduce ambiguity and context loss.

**Weaknesses**
- Many controls remain prompt/checklist enforced unless backed by external CI policy.
- Process overhead can be heavy for small/simple changes.
- Same-model self-review risk if no model diversity/human gate is added.

**Best for**
- Teams needing disciplined AI-assisted delivery with strong planning rigor.

### 3) MetaGPT
**Score: 74/100**

**Strengths**
- Excellent role-based decomposition and staged artifact generation.
- SOP-like flow improves requirement clarity before coding.
- Good for reducing “single-agent chaos” on medium/large efforts.

**Weaknesses**
- Reliability still depends on external hard gates (tests, CI, merge policy).
- Can produce verbose process output if not tightly scoped.
- Practical production integration requires additional engineering.

**Best for**
- Structured multi-role generation and design-heavy project planning.

### 4) AutoGen (hierarchical mode)
**Score: 76/100**

**Strengths**
- Mature orchestration primitives for manager-worker and routing patterns.
- Supports deterministic + LLM-driven control hybrids.
- Strong flexibility for custom enterprise workflows.

**Weaknesses**
- Easy to overcomplicate conversations without strict routing rules.
- Out-of-box quality guarantees are limited without CI/policy integration.
- Cost/latency can grow quickly in large multi-agent chats.

**Best for**
- Building custom orchestrators that need explicit control over handoffs.

### 5) CrewAI (hierarchical manager mode)
**Score: 75/100**

**Strengths**
- Clear manager + specialist model aligns with production team structure.
- Practical task graph and context passing patterns.
- Good blend of autonomous crews and deterministic flows.

**Weaknesses**
- Depends on careful task design to avoid noisy handoffs.
- Gate enforcement still external unless wired into CI/CD.
- Can drift if manager prompts are not strict about acceptance criteria.

**Best for**
- Teams wanting quick adoption of role-based orchestration with manageable complexity.

### 6) SWE-agent
**Score: 80/100**

**Strengths**
- Execution-grounded workflow (edit/run/test loop) rather than pure text coding.
- Strong benchmark discipline (fail→pass + pass→pass mindset).
- Tool interface design improves practical fix quality on real repos.

**Weaknesses**
- Benchmark strength does not automatically equal production readiness.
- Requires solid environment setup and harness discipline.
- Less focused on business-planning artifacts than BMAD-style methods.

**Best for**
- Repo-centric bug fixing where reproducible validation is essential.

### 7) Proposed new AIEnhance system (after redesign)
**Score: 89/100**

**Strengths**
- Hard, non-bypassable quality gates before merge/deploy.
- Project Manager per project/session removes cross-project context pollution.
- Mandatory Dev → QA → Code Review path with human merge approval.

**Weaknesses**
- Slightly slower cycle time vs today’s auto-merge behavior.
- Requires upfront engineering to wire test harnesses and policy controls.
- Demands disciplined baseline snapshots for regression comparison.

**Best for**
- Production-grade AI-assisted delivery where reliability and control are mandatory.

---

## Section 2: What AI Coding Agents Typically Miss (Top 10, ranked)

1. **Environment mismatch (dev vs prod)** — config, runtime filesystem, container assumptions.
2. **Missing/wrong dependencies and imports** — package hallucinations, lockfile drift.
3. **Build-time vs runtime config confusion** — especially frontend/public environment variables.
4. **Integration wiring gaps** — routes/jobs/migrations/services not actually registered.
5. **Insufficient regression validation** — fix passes narrow test but breaks existing behavior.
6. **Data freshness/business invariants** — technically “working” but stale or invalid domain outputs.
7. **Concurrency/race/idempotency bugs** — flaky behavior under retries/load.
8. **Infrastructure assumptions** — ports/network/compose behavior mismatch.
9. **Security hygiene misses** — hardcoded secrets, unsafe defaults, exposed services.
10. **Context drift across long sessions** — wrong project context or outdated assumptions reused.

---

## Section 3: Recommended Architecture — "AIEnhance v2"

AIEnhance v2 addresses current failure modes by replacing advisory process with enforceable gates and project-scoped management.

### Core design
- **Orchestrator** handles intake and project routing.
- **One Project Manager per project** (never shared).
- PM is **spawned fresh per session** for that project only.
- Every code path is enforced: **Dev Agent → QA Agent → Code Review Agent → PR**.
- PR remains blocked until **explicit human merge approval**.

### Full pipeline
```mermaid
flowchart TD
    U[User] --> O[Orchestrator]
    O --> PM[Project Manager (project-scoped session)]
    PM --> D[Dev Agent]
    D --> Q[QA Agent\nSmoke + Import + Data Freshness + Frontend Build]
    Q -->|Pass| R[Code Review Agent\nDiff vs last known-good]
    Q -->|Fail| D
    R -->|Approved| PR[Pull Request\nAwaits Human Merge]
    R -->|Changes Requested| D
```

### How this solves today’s issues
- **Production outages from unvalidated code**: blocked by build/smoke/regression gates.
- **No QA gate enforcement**: QA becomes mandatory transition gate, not optional.
- **Context pollution across projects**: PM/session isolation per project.
- **Auto-merge bypassing checks**: merge disabled until all gates + human approval.

### Key principles
1. One Project Manager per project (never shared).
2. PM is spawned fresh per project session (no cross-project memory bleed).
3. Every PR path is Dev → QA → Code Review before human merge.
4. QA executes real checks (smoke/import/data freshness/frontend build).
5. Code Review compares current diff against last working baseline.
6. Nothing merges unless **all** gates pass.

---

## Section 4: Multi-Project Architecture

To support multiple projects from the same chat without contamination:

- **Project Manager-per-project pattern**: each project has a dedicated PM context envelope.
- **Isolated sessions per project**: no shared task memory across projects; artifacts are project-keyed.
- **Router in Orchestrator**:
  1. classify incoming request by project ID/repo,
  2. route to matching PM session if active,
  3. otherwise spawn a fresh PM for that project,
  4. enforce project-bound tool scope and artifact paths.

Result: one chat can command many projects while execution contexts remain isolated.

---

## Section 5: Quality Gate Design (engineering-grade)

### Gate 1: Build Gate
**Objective:** Verify code is build/import valid before deeper tests.
- Frontend: `pnpm install --frozen-lockfile && pnpm build`
- Python/API: dependency sync + import smoke (e.g., `python -c "import app"`)
- Fail conditions: build errors, unresolved imports, lockfile drift.

### Gate 2: Smoke Gate
**Objective:** Verify runnable behavior and domain sanity.
- Health endpoint returns 200.
- Critical endpoint(s) return valid schema.
- Data freshness assertions pass (no stale candles, no mock payloads).
- Fail conditions: non-200 health, stale data, mock placeholders detected.

### Gate 3: Regression Gate
**Objective:** Prevent collateral damage.
- Compare key endpoint outputs to baseline snapshots/tolerances.
- Require fail→pass for the target fix and pass→pass for existing tests.
- Fail conditions: behavioral drift beyond tolerance, existing test regressions.

### Gate 4: Security Gate
**Objective:** Block obvious high-risk defects.
- Scan for hardcoded secrets/tokens/keys.
- Check for unintended exposed ports/services.
- Enforce dependency vulnerability threshold policy.
- Fail conditions: secret leak, unsafe exposure, policy-violating vuln findings.

### Gate 5: Human Review Gate
**Objective:** Preserve explicit human control over release.
- PR must be reviewed and explicitly approved by human.
- No auto-merge for AI-generated production-impacting changes.
- Fail condition: missing explicit human approval.

---

## Section 6: Implementation Roadmap

### Phase 1 (Now, 2–3 days): Close immediate reliability gaps
- Disable auto-merge for agent PRs.
- Add required CI checks: build, import smoke, baseline smoke endpoint.
- Enforce branch protection and required reviewers.
- Add dependency/import integrity checks in CI.

### Phase 2 (Week 1–2): Wire QA gate into delivery loop
- Insert mandatory QA stage between Dev and Code Review.
- Add data freshness tests and no-mock-data assertions.
- Generate structured QA reports attached to each PR.
- Block PR progression unless QA status is green.

### Phase 3 (Month 1): Full PM-per-project architecture
- Implement Orchestrator routing to project-scoped PM sessions.
- Enforce isolated context/artifact stores per project.
- Add regression baseline management and diff-aware code review automation.
- Add release controls: staged rollout checks + rollback triggers.

---

## Final Recommendation
Adopt **AIEnhance v2** with **hard gates + PM-per-project isolation** immediately; this is the fastest path to eliminate avoidable outages while preserving AI development speed under safe control.