# Exercise 2: Plan Mode in practice

> **Goal:** Learn to create plans before implementing.
> **Mode:** Plan Mode
> **Estimated time:** 15 minutes
> **Prerequisite:** Exercise 1 (Ask Mode)

---

## Scenario

You already researched and understand the system (Exercise 1). Now you will create a **detailed plan** before writing any code.

---

## Setup

1. Switch to **Plan Mode** in the mode selector
2. Have in mind the feature or change you researched in the previous exercise

---

## Exercise 2.1 — Create a basic plan

### Prompt to copy and paste:

```
Based on what exists in this project, create a plan to add [FEATURE/CHANGE].

The plan must include:

1. **Summary** — what will be done in 2–3 sentences
2. **Files involved** — which will be created, which will be modified
3. **Implementation steps** — in the correct order, one by one
4. **Tests** — how to verify each step is correct
5. **Scope** — what is IN scope and OUT of scope

Use existing project patterns as reference.
```

### What to watch for:

- The agent will read files and propose changes but **not execute**
- The plan should be specific to **your** project (not generic)
- It should list files with real paths

### Checkpoint:

> Read the whole plan. Ask yourself: “If I gave this to a junior dev, could they implement it?” If not, ask for more detail.

---

## Exercise 2.2 — Refine the plan

After reading the plan, there is almost always room to improve. Practice iterating.

### Prompts to refine:

**If details are missing:**

```
Step 3 is vague. Spell out exactly:
- Which functions need to be created
- Which types/interfaces are needed
- Expected behavior on error
```

**If scope is too large:**

```
The plan is too large for one implementation.
Split it into two smaller plans:
- Plan A: minimum viable (basic functionality)
- Plan B: improvements and edge cases (second iteration)
```

**If test strategy is missing:**

```
Add a testing section to the plan for each step:
- Which unit test to write
- Which behavior to verify manually
- Which edge cases to cover
```

**If you want to validate the approach:**

```
Before we continue, validate this plan:
- Is there any risk we did not consider?
- Is there any dependency between steps that could break?
- Is any step parallelizable?
```

### What to watch for:

- Each refinement makes the plan more **executable**
- Time spent here saves time during implementation
- You are training the agent to be more specific

---

## Exercise 2.3 — Compare: without plan vs. with plan

This exercise shows the difference between implementing directly and implementing with a plan.

### Part A — Without a plan (observe the result)

Open a new session in **Agent Mode** and ask directly:

```
Add a reusable alert/notification component to the project.
```

Observe:

- The agent will choose where to put the file
- It will decide the component API (props, events)
- It will choose styling on its own
- It may or may not create tests

**Do not accept the changes.** Only observe what the agent decided on its own.

### Part B — With a plan (compare)

Open a new session in **Plan Mode** and ask:

```
I want a reusable alert/notification component.

Before implementing, create a plan that defines:
1. Where the component will live (folder and file name)
2. Which props it will have (type, severity, message, etc.)
3. Which events it will emit (close, action, etc.)
4. How CSS will work (following project patterns)
5. Which variants exist (success, error, warning, info)
6. Which tests to create
7. How other components will use it
```

### Compare the two results:

- Is the planned result more **predictable**?
- Did the plan give you **control** over decisions?
- Would you feel more confident implementing with the plan?

---

## Exercise 2.4 — Save the plan

Good plans should be saved for reference. Practice:

### Prompt to copy and paste:

```
Save this plan as a Markdown file at plans/feature-name.md

Format it clearly with:
- Title and date
- Summary
- Numbered steps
- Validation checklist
```

> **Note:** This exercise works in Agent Mode, since it needs to create a file. It is a good example of when switching modes makes sense.

---

## What we learned

1. **Plans reduce surprises** — you know exactly what will happen
2. **Iterating on a plan is cheap** — fixing a plan takes seconds; fixing code takes minutes
3. **Plans give control** — you choose the approach, not the agent
4. **Time invested pays back** — implementation with a plan is faster and safer

---

## Next step

With a plan ready, we will **implement**.

> **Next:** [03 — Agent Mode exercise](./03-exercicio-agent-mode.md)
