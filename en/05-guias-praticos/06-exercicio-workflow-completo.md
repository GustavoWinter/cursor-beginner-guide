# Exercise 6: Full workflow — from zero to commit

> **Goal:** Combine everything you learned in a real flow, from understanding to ready code.
> **Modes:** Ask → Plan → Agent
> **Estimated time:** 30–40 minutes

---

## Scenario

You received a real task: add a feature to the project. We will walk the full flow using all concepts and modes.

Pick a simple feature from your project for this exercise. Suggestions:
- Add a field to an existing form
- Create an empty state component (when there is no data)
- Add a copy-to-clipboard button
- Create a reusable tooltip

---

## Phase 1: Research (Ask Mode)

**Time:** ~5 minutes

### Switch to Ask Mode and use this prompt:

```
I need to implement [DESCRIBE THE FEATURE].

Help me understand:

1. Which existing components/files are relevant?
2. Is there something similar already implemented?
3. Which patterns should I follow?
4. Which files will I need to create or change?
5. Any edge cases or special considerations?

Do not implement anything — only research.
```

### Checklist before continuing:
- [ ] I understand how the system works today
- [ ] I know which files will be involved
- [ ] I know the patterns to follow
- [ ] I identified possible risks

> If any item is unchecked, ask more questions in Ask Mode before continuing.

---

## Phase 2: Plan (Plan Mode)

**Time:** ~10 minutes

### Switch to Plan Mode and use this prompt:

```
Based on our research, create an implementation plan for [FEATURE].

Structure it as:

## Summary
What will be done in 2–3 sentences.

## Files
- Create: [list]
- Modify: [list]

## Steps (in order)
1. [step]
2. [step]
...

## Tests
- How to verify each step
- Which unit tests to add

## Out of scope
- What we will NOT change
```

### Refine the plan:

Read the whole plan and request adjustments:

```
[If detail is missing]
Expand step X. I want to know exactly which functions to create
and which types to use.

[If too large]
This plan is too big. Split into Phase 1 (MVP) and Phase 2 (improvements).

[If tests are missing]
Add specific tests for each step.
```

### Checklist before continuing:
- [ ] Plan is clear and specific
- [ ] I know exactly which files will be created/changed
- [ ] Each step is detailed enough
- [ ] Scope is defined (in and out)
- [ ] Test strategy is defined

---

## Phase 3: Implement (Agent Mode)

**Time:** ~15–20 minutes

### Open a NEW session in Agent Mode

This is crucial — clean context for implementation.

### Initial prompt:

```
I will implement a feature following the plan below.
Implement ONE step at a time.
After each step, show me what changed and wait for my approval.

[Paste the full plan here]

Start with step 1.
```

### For each step:

**If the result is good:**
```
Approved. Proceed to step 2.
```

**If it needs adjustment:**
```
Almost. Adjust [specific issue] before continuing.
```

**If it is wrong:**
```
This is not correct. The problem is [describe].
Revert and try again considering [instruction].
```

---

## Phase 4: Commit and review

### After all steps are implemented:

```
Run tests to verify everything works.
```

If they pass:

```
Create a commit with a descriptive message in the format:
feat(scope): short description of what was added
```

If they fail:

```
Tests failed. Analyze the error and fix it.
Do not continue until all tests pass.
```

### Final review:

```
Show a summary of all changes:
- Files created
- Files modified
- Tests added
- Any remaining follow-ups
```

---

## Retrospective — reflection after the exercise

After completing the flow, reflect:

### Time

| Phase | Time spent | Was it worth it? |
| ----- | ---------- | ---------------- |
| Research (Ask) | __ min | |
| Planning (Plan) | __ min | |
| Implementation (Agent) | __ min | |
| Review and commit | __ min | |
| **Total** | __ min | |

### Quality

- Did the final result follow project patterns?
- Were there surprises during implementation?
- Do tests cover the important cases?
- Would you trust sending this PR to code review?

### What would you do differently?

- Was research enough?
- Was the plan detailed enough?
- Should you have asked for smaller implementation steps?
- Would any rule or skill help automate part of the process?

---

## Workflow template — copy and reuse

Use this template for future tasks:

```markdown
# Task: [name]

## Phase 1 — Research (Ask Mode)
- [ ] Understand current system
- [ ] Identify relevant files
- [ ] Identify patterns to follow
- [ ] Identify risks and edge cases

## Phase 2 — Planning (Plan Mode)
- [ ] Define files to create/modify
- [ ] Define steps in the right order
- [ ] Define tests
- [ ] Define scope (in/out)
- [ ] Review and approve plan

## Phase 3 — Implementation (Agent Mode)
- [ ] New session with clean context
- [ ] Implement step by step
- [ ] Review each change
- [ ] Run tests at each critical step

## Phase 4 — Wrap-up
- [ ] All tests passing
- [ ] Linting OK
- [ ] Commits with descriptive messages
- [ ] Ready for PR
```

---

## Congratulations!

You completed all exercises. You now know how to:

- **Research** with Ask Mode before acting
- **Plan** with Plan Mode before implementing
- **Implement** with Agent Mode in a controlled way
- **Use rules** for automatic consistency
- **Create skills** to automate repetitive tasks
- **Manage context** to keep answer quality high

### Next level

- Explore existing project rules in `.cursor/rules/`
- Read skills in `.cursor/skills/`
- Create your own rules and skills for your workflow
- Experiment and iterate — that is how you learn

> *“Pick one tool and practice a lot. It is part art and part science — you need repetition to develop intuition about what to trust the model with and what to keep for yourself.”*
