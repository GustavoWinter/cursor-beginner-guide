# Exercise 3: Agent Mode in practice

> **Goal:** Implement changes following a plan, with careful review.
> **Mode:** Agent Mode
> **Estimated time:** 20 minutes
> **Prerequisite:** Exercises 1 and 2

---

## Scenario

You researched (Ask Mode), planned (Plan Mode), and now you will implement (Agent Mode). This is when code is actually written.

---

## Setup

1. Switch to **Agent Mode**
2. Open a **new session** (clean context!)
3. Have the plan from Exercise 2 ready

---

## Exercise 3.1 — Implement step by step

The key in Agent Mode is **not to ask for everything at once**.

### Prompt to copy and paste:

```
I will implement a change following a plan.
Implement ONE step at a time and show me what changed
before moving to the next.

Plan:
1. [Paste your first step]
2. [Paste your second step]
3. [Paste your third step]

Start with step 1.
```

### What to watch for:

- The agent should implement **only step 1** and stop
- It will show the diff (what changed)
- You review before authorizing the next step

### How to review:

- Does the code do what the step asked?
- Does it follow project patterns?
- Did it avoid changing unrelated files?

If everything looks good, reply:

```
OK, proceed to step 2.
```

If something is wrong:

```
Step 1 is not correct. The issue is: [describe].
Fix it before continuing.
```

---

## Exercise 3.2 — Use @ for precise context

Practice referencing files to give the agent exact context.

### Prompt to copy and paste:

```
Look at @src/components/[ExistingComponent].vue
and create a similar new component called [NewName].

The differences should be:
- [difference 1]
- [difference 2]

Keep the same prop, style, and structure patterns.
```

### What to watch for:

- With `@`, the agent reads the exact file as reference
- The result should be consistent with the original
- Compare: does the new component follow the same pattern?

---

## Exercise 3.3 — Incremental commits with Git

Practice review and commit step by step.

### Flow:

**After the agent makes a change:**

1. Review the diff in Cursor (shown automatically)
2. If approved, ask for a commit:

```
Commit this change with a descriptive message.
Use format: type(scope): description

Examples:
- feat(products): add filter field
- fix(auth): fix expired token validation
```

3. Verify the result:

```
Run git log --oneline -5 to show the latest commits.
```

### What to watch for:

- Each commit should be **small and focused**
- The message should describe **what** and **why**
- If something goes wrong, you can revert a specific commit

---

## Exercise 3.4 — Fix when the agent is wrong

Errors will happen. Practice handling them.

### Simulated scenario:

Ask the agent something intentionally vague and see what happens:

```
Improve the registration form.
```

The agent will probably:

- Make changes you did not want
- Assume things that are not correct
- Touch more files than necessary

### How to fix:

**Option 1 — Ask to revert:**

```
Revert all changes you made.
We will restart with more specific instructions.
```

**Option 2 — Accept partially:**

```
The change in file X is good, but the changes in files
Y and Z are not what I wanted. Revert only Y and Z.
```

**Option 3 — Use Git to revert:**

```
git checkout -- src/components/RegistrationForm.vue
```

### Lesson:

> Vague prompts produce unpredictable results. The more specific you are, the better the outcome.

---

## Exercise 3.5 — New session for a new task

Practice splitting tasks across sessions.

### Scenario:

You finished implementing the planned feature. Now you need to fix an unrelated bug.

**WRONG** — continue in the same session:

```
Now fix the bug in the login component where...
```

**RIGHT** — new session:

1. Close the current session (or open a new one)
2. In the new session, start clean:

```
I need to fix a bug in the login component.
The problem is: [describe the bug]
The relevant file is: @src/components/Login.vue
```

### Why this matters:

- Clean context = better quality
- The agent will not mix the previous feature with the bug
- Easier to track what was done in each session

---

## Review checklist — use on every implementation

Copy this checklist whenever the agent makes changes:

```
## Implementation review

### Code
- [ ] Does it do what was asked?
- [ ] Does it follow project patterns?
- [ ] Are variable and function names clear?
- [ ] No duplicated logic?
- [ ] No unnecessary dependencies?

### Scope
- [ ] Only expected files were changed?
- [ ] No out-of-scope changes?
- [ ] Nothing removed that should stay?

### Quality
- [ ] Tests pass?
- [ ] Linting OK?
- [ ] Build works?

### Git
- [ ] Commit message is descriptive?
- [ ] Diff reviewed before commit?
```

---

## What we learned

1. **Step by step is safer** than “do everything at once”
2. **`@` gives precise context** — use it to reference files
3. **Small commits** let you revert without losing everything
4. **Vague prompts → vague results** — be specific
5. **New task = new session** — never mix unrelated topics

---

## Next step

Now we will see how **rules** change output quality.

> **Next:** [04 — Rules exercise](./04-exercicio-regras.md)
