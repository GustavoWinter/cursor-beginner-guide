# The workflow: Research → Plan → Implement

> The number one mistake when starting with AI: jumping straight to implementation.
> This chapter teaches the flow that avoids most problems.

---

## The classic mistake

Most developers open Cursor and write something like:

> _“Implement an authentication system with JWT.”_

The agent complies. It generates hundreds of lines of code. The problem? It assumed:

- Which library to use
- How to structure files
- Which error pattern to follow
- How to store tokens
- Which middleware to use

If any assumption is wrong, you will spend **more time fixing** than you would have spent planning.

> _“One wrong line of research can generate hundreds of lines of wrong code.”_ — Dex Horthy

---

## The right flow

```
┌─────────────┐     ┌─────────────┐     ┌──────────────┐
│  RESEARCH   │ ──→ │    PLAN     │ ──→ │ IMPLEMENT    │
│ (Ask Mode)  │     │ (Plan Mode) │     │ (Agent Mode) │
└─────────────┘     └─────────────┘     └──────────────┘
     │                    │                     │
     ▼                    ▼                     ▼
  Understand the      Define the           Execute with
  problem             steps                clean context
```

Each phase maps to a specific **Cursor mode**. Each phase produces **output** that feeds the next.

---

## Phase 1: Research (Ask Mode)

**Goal:** Understand the problem before solving it.

**Cursor mode:** Ask Mode (read-only — the agent cannot change files)

**What to do:**

- How does the system work today?
- Which files are relevant?
- Which patterns does the project already use?
- How does data flow through the system?
- What edge cases exist?

**Example prompt:**

```
I need to add a search filter to the product listing.
Help me understand:

1. How does the listing work today? Which components are involved?
2. Is there already a filter implemented elsewhere in the system?
3. Where does the data come from? Which API is used?
4. What patterns should I follow based on what already exists?
```

**Expected output:** A clear understanding of the problem that you validate as a human.

**Human checkpoint:** _“Does this match how I understand the system?”_

---

## Phase 2: Plan (Plan Mode)

**Goal:** Define exactly what will be done before doing it.

**Cursor mode:** Plan Mode (the agent reads and suggests, but asks for approval before executing)

**What to define:**

- Which files will be created or changed
- Order of changes
- How to verify the change is correct (tests)
- What is **in** and **out** of scope

**Example prompt:**

```
Based on what we researched, create a plan to add the search filter
to the product listing.

The plan should include:
- Files to be created or modified
- Implementation order
- How we will test each change
- What we will NOT change right now
```

**Expected output:** A clear, step-by-step plan document.

**Human checkpoint:** _“Do the steps make sense? Is anything missing? Anything out of scope?”_

---

## Phase 3: Implement (Agent Mode)

**Goal:** Execute the plan with minimal context.

**Cursor mode:** Agent Mode (the agent can read, write, and run commands)

**How to do it:**

1. Open a **new session** (clean context)
2. Provide only the plan as context
3. Implement step by step
4. Review each change before continuing
5. Commit frequently

**Example prompt:**

```
Follow the plan below to implement the search filter.
Implement one step at a time and show me what changed before
moving to the next.

[paste the plan here or reference the file with @plan.md]
```

**Why a new session?**

- Clean context = better quality
- The “hard thinking” was already done in research and planning
- You can even use a smaller/faster model because the plan is explicit

---

## Why this flow works

### 1. It avoids wrong assumptions

Research ensures you and the agent understand the system before changing it.

### 2. It makes review easier

With an explicit plan, you know exactly what to expect. Checking whether the agent followed the plan is much easier than reviewing code that appeared “from nowhere.”

### 3. Cheap course corrections

Fixing a plan costs one message. Fixing hundreds of lines of code costs hours.

### 4. Less context during implementation

By Phase 3, context is basically the plan — no polluted history.

---

## When you do NOT need the full flow

Not every task needs all three phases. Use judgment:

| Task type                | Recommended flow                       |
| ------------------------ | -------------------------------------- |
| Fix a typo               | Straight to Agent Mode                 |
| Add a simple field       | Ask → Agent                            |
| Small new feature        | Ask → Agent                            |
| Medium/large new feature | Ask → Plan → Agent                     |
| Large refactor           | Ask → Plan → Agent (multiple sessions) |
| Complex bug              | Ask (debug) → Plan → Agent             |
| Architectural change     | Ask → Plan → human review → Agent      |

**Rule of thumb:** **the higher the risk of getting it wrong, the more research and planning are worth it.**

---

## Summary

| Phase     | Mode  | Goal         | Output                |
| --------- | ----- | ------------ | --------------------- |
| Research  | Ask   | Understand   | Validated diagnosis   |
| Plan      | Plan  | Define steps | Step-by-step plan     |
| Implement | Agent | Execute      | Code ready for review |

> _“AI does not replace thinking. It amplifies the thinking you did — or the lack of it.”_ — Dex Horthy

---

> **Next:** [02 — Cursor modes](../02-modos/01-ask-mode.md) — each mode in detail
