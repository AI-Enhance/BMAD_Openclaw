# Architecture Decision Document — {PROJECT_NAME}

**Author:** Architect Agent
**Date:** {YYYY-MM-DD}

## 1. System Context

{High-level description of what the system does and its boundaries}

## 2. Architecture Principles

1. {Principle} — {Rationale}

## 3. Technology Stack

| Layer | Technology | Version | Rationale |
|-------|------------|---------|-----------|
| Runtime | {tech} | {ver} | {why} |
| Framework | {tech} | {ver} | {why} |
| Database | {tech} | {ver} | {why} |
| Auth | {tech} | {ver} | {why} |
| Hosting | {tech} | {ver} | {why} |

## 4. Architecture Decisions

### ADR-001: {Decision Title}

**Status:** Accepted
**Date:** {YYYY-MM-DD}

**Context:** {Why this decision is needed}

**Decision:** {What was decided}

**Options Considered:**

| Option | Pros | Cons |
|--------|------|------|
| {A} | {pros} | {cons} |
| {B} | {pros} | {cons} |

**Rationale:** {Why this option}

**Consequences:** {Trade-offs accepted}

## 5. System Architecture

### 5.1 Component Diagram
```
{ASCII or description of component relationships}
```

### 5.2 Data Architecture
{Database schema, entity relationships, RLS policies}

### 5.3 API Design
{REST/GraphQL/tRPC, endpoint patterns, error handling}

## 6. Project Structure

```
src/
├── {directory}/    # {purpose}
```

## 7. Coding Standards

| Convention | Rule | Example |
|-----------|------|---------|
| Files | {convention} | {example} |
| Components | {convention} | {example} |
| Functions | {convention} | {example} |

## 8. Testing Strategy

| Type | Tool | Coverage Target |
|------|------|----------------|
| Unit | {tool} | {target} |
| Integration | {tool} | {target} |
| E2E | {tool} | {target} |

## 9. Security Considerations
- {Consideration and mitigation}

## 10. Deployment
{Deployment strategy, environments, CI/CD}
