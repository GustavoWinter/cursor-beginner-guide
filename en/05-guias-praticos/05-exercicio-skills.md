# Exercise 5: Skills in practice

> **Goal:** Create and use a skill to automate a repetitive workflow.
> **Mode:** Agent Mode
> **Estimated time:** 20 minutes

---

## Scenario

You will create a skill from scratch, use it, and see how it simplifies repetitive tasks.

---

## Exercise 5.1 — Create a simple skill

We will create a skill to generate a full Vue component (component + scss + test + i18n).

### Prompt to copy and paste:

```
Create a skill at .cursor/skills/create-vue-component/SKILL.md

The skill should document the full process of creating a Vue component
in this project. Analyze existing components and extract the pattern.

The skill should cover:
1. Creating the .vue file (script setup + ts)
2. Creating the .scss file (with BEM)
3. Creating the i18n file (if applicable)
4. Creating the test file (.spec.ts)
5. Validation checklist

Include a "Trigger" section explaining when to use this skill.
Include concrete examples based on what already exists in the project.
```

### What to watch for:

- The agent will **analyze existing components** before creating the skill
- The skill should reflect **real** project patterns
- It should be detailed enough to follow without ambiguity

---

## Exercise 5.2 — Use the skill

Now open a **new session** and use the skill you created.

### Prompt to copy and paste:

```
Create a user feedback component (UserFeedback) that:
- Shows a text field for the user to type
- Has a submit button
- Shows a loading state while submitting
- Shows success or error message after submit
```

### What to watch for:

- The agent should detect and load the skill
- It should follow all steps in order
- It should create all files listed in the skill
- The result should be consistent with existing components

### Verify:

- `.vue` file created with the right structure?
- `.scss` file created with BEM?
- i18n file created?
- Test file created?
- Matches patterns of existing components?

---

## Exercise 5.3 — Compare: with and without a skill

### Without a skill (typical result):

The agent creates the `.vue` and maybe `.scss`. Forgets i18n. No tests. Wrong folder.

### With a skill:

The agent follows the full checklist. All files created. Everything in the right place. Patterns followed.


| Aspect | Without skill | With skill |
| ------ | ------------- | ---------- |
| Files created | 1–2 | 3–4 (all) |
| i18n | Often forgotten | Included |
| Tests | Often forgotten | Included |
| Correct folder | Maybe | Yes |
| Consistency | Varies | Same every time |
| Prompt length | Long (you must specify everything) | Short (skill handles details) |


---

## Exercise 5.4 — Create a pre-commit skill

Create another useful skill: a checklist before committing.

### Prompt to copy and paste:

```
Create a skill at .cursor/skills/pre-commit-review/SKILL.md

This skill should be used before committing. It should:

1. List all modified files (git diff --name-only)
2. For each modified file:
   - Check whether it follows project patterns
   - Check for lint issues
   - Check whether hardcoded strings should use i18n
3. Run related tests
4. Produce a summary with:
   - What looks OK
   - What needs fixing
   - Suggested commit message

Trigger: "pre-commit review", "review before commit",
"check changes before commit"
```

### Test the skill:

After creating it, make any change in the project and use:

```
Run a pre-commit review of the current changes.
```

---

## Exercise 5.5 — Iterate and improve a skill

Skills should evolve. Practice improving an existing skill.

### Prompt to copy and paste:

```
Read the skill at @.cursor/skills/create-vue-component/SKILL.md

Based on my experience using it, add:
1. A step to register the component in the barrel export (index.ts)
   if one exists
2. Examples for complex props (arrays, objects)
3. A step for basic accessibility (aria-labels, roles)

Update SKILL.md while keeping the existing structure.
```

### What to watch for:

- Skills are living documents — they should be updated
- Each iteration makes the skill more complete
- The agent reads the existing skill and **extends** it without losing what was there

---

## When to create a skill

Use this mental flowchart:

```
Have you done this task before?
       │
       ├── No → Do it manually, learn the process
       │
       └── Yes → How many times?
                    │
                    ├── Once → Probably no skill yet
                    │
                    └── 2+ times → Create a skill!
                                     │
                                     └── More than 3 steps?
                                           │
                                           ├── Yes → Detailed skill
                                           └── No → Maybe a rule is enough
```

---

## What we learned

1. **Skills automate full workflows** — not only patterns
2. **The agent creates better skills** when it analyzes existing code
3. **Skills shrink prompts** — you do not repeat everything
4. **Skills enforce consistency** — same result every time
5. **Skills should evolve** — update as you learn

---

> **Next:** [06 — Full workflow](./06-exercicio-workflow-completo.md) — putting it all together in a real flow
