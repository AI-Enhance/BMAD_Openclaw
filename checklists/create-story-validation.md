# 🎯 Story Context Quality Validation Checklist

**Purpose:** Validate a story file created by the create-story workflow. This is an adversarial quality check.

**🔥 CRITICAL MISSION:** Outperform the original create-story LLM — find what's missing!

## How to Use

- Load the story file to review
- Load workflow variables (implementation_artifacts, epics_file, etc.)
- Proceed with systematic analysis

---

## Step 1: Load and Understand the Target

- [ ] Story file loaded and parsed
- [ ] Metadata extracted: epic_num, story_num, story_key, story_title
- [ ] All workflow variables resolved
- [ ] Current implementation guidance understood

## Step 2: Exhaustive Source Document Analysis

### 2.1 Epics and Stories Analysis
- [ ] Epic loaded completely
- [ ] Complete Epic context extracted (objectives, business value)
- [ ] ALL stories in epic reviewed for cross-story context
- [ ] Our story's requirements, ACs, technical requirements extracted
- [ ] Cross-story dependencies identified

### 2.2 Architecture Deep-Dive
- [ ] Architecture loaded (single or sharded)
- [ ] Technical stack with versions identified
- [ ] Code structure and organization patterns extracted
- [ ] API design patterns and contracts noted
- [ ] Database schemas and relationships mapped
- [ ] Security requirements extracted
- [ ] Performance requirements identified
- [ ] Testing standards documented
- [ ] Deployment patterns noted
- [ ] Integration patterns captured

### 2.3 Previous Story Intelligence
- [ ] Previous story file loaded (if applicable)
- [ ] Dev notes and learnings extracted
- [ ] Review feedback and corrections noted
- [ ] File patterns identified
- [ ] Testing approaches documented
- [ ] Problems and solutions captured

### 2.4 Git History Analysis
- [ ] Recent commits analyzed (if available)
- [ ] Code patterns identified
- [ ] Dependencies tracked

### 2.5 Latest Technical Research
- [ ] Libraries/frameworks identified
- [ ] Latest versions researched
- [ ] Breaking changes noted

## Step 3: Disaster Prevention Gap Analysis

### 3.1 Reinvention Prevention
- [ ] No areas where developer might create duplicate functionality
- [ ] Code reuse opportunities identified
- [ ] Existing solutions mentioned that should be extended

### 3.2 Technical Specification Gaps
- [ ] No wrong/missing library versions
- [ ] API contracts specified
- [ ] Database schema conflicts identified
- [ ] Security requirements present
- [ ] Performance requirements present

### 3.3 File Structure Gaps
- [ ] File locations specified correctly
- [ ] Coding standards referenced
- [ ] Integration patterns documented
- [ ] Deployment requirements noted

### 3.4 Regression Prevention
- [ ] Breaking change risks identified
- [ ] Test requirements specified
- [ ] UX requirements included
- [ ] Previous story context incorporated

### 3.5 Implementation Clarity
- [ ] No vague implementations
- [ ] Acceptance criteria complete and specific
- [ ] Scope boundaries clear
- [ ] Quality requirements defined

## Step 4: LLM Optimization Analysis

- [ ] No excessive verbosity wasting tokens
- [ ] No ambiguous instructions
- [ ] Information well-structured for LLM processing
- [ ] Key requirements not buried in verbose text
- [ ] Clear headings and scannable structure

## Final Verdict

```
Definition of Done: {PASS/FAIL}

✅ Story Ready: {story_key}
📊 Score: {completed}/{total} items passed
🔍 Quality Gates: {status}
```

If FAIL: List specific failures and required actions.
