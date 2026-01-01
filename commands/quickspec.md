---
description: Lightweight spec-driven workflow for small features (spec → plan → build)
argument-hint: <feature description>
allowed-tools: Read, Write, Edit, Bash, Glob, Grep
---

# QuickSpec: Lightweight Spec-Driven Development

You are implementing a small feature using a structured but minimal workflow. Refer to constitution.md (if exists) and project CLAUDE.md for project guidance and standards.

**Feature request:** $ARGUMENTS

---

## Setup

1. Determine the next feature number by checking `.quickspec/` for existing directories (001, 002, etc.)
2. Create a kebab-case slug from the feature description (e.g., "dark mode toggle" → "dark-mode-toggle")
3. Create directory: `.quickspec/<number>-<slug>/` (e.g., `.quickspec/001-dark-mode-toggle/`)
4. All artifacts go in this directory

---

## Phase 1: Spec

Create `.quickspec/<number>-<slug>/spec.md`:

```markdown
# <Feature Name>

## What
[1-2 sentences - what you're building]

## Why
[1 sentence - user/business value]

## Acceptance Criteria
- [ ] [criterion 1]
- [ ] [criterion 2]
- [ ] [criterion 3]

## Out of Scope
- [excluded item]
```

- Keep to 3-5 acceptance criteria max
- If ambiguous, ask 1-2 clarifying questions before proceeding
- If scope seems too large for a quick feature, say so

**Wait for user confirmation before proceeding to Phase 2.**

---

## Phase 2: Plan

Scan the codebase, then create `.quickspec/<number>-<slug>/plan.md`:

```markdown
# Plan

## Files
- `path/to/file.py` — [change]
- `path/to/new.py` — [create, purpose]

## Approach
[2-4 sentences on implementation strategy]

## Risks
- [potential issue, if any]
```

- Use concrete file paths
- If touching >5-7 files, flag that scope may be too large
- Note any risks or dependencies

**Wait for user confirmation before proceeding to Phase 3.**

---

## Phase 3: Build

Implement the feature:

1. Follow the plan
2. Respect existing code conventions  
3. Write tests if the project has them
4. Check off acceptance criteria in `spec.md` as you complete them
5. Run existing tests/linting and fix issues

When done, summarize:
- Files changed
- Any deviations from plan
- How to verify it works

---

## Directory Structure

```
.quickspec/
├── 001-dark-mode-toggle/
│   ├── spec.md
│   └── plan.md
├── 002-user-preferences/
│   ├── spec.md
│   └── plan.md
└── ...
```

---

## Guidelines

- Be direct, no filler
- If the plan was wrong, update it and explain why
- If scope creeps, add to "Out of Scope" for follow-up
- Keep momentum — this is for small, quick features
