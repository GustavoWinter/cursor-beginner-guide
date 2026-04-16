# Agent Mode — implement and execute

> Cursor’s most powerful mode.
> Here the agent can read, write, create files, and run commands.
> With great power comes great responsibility.

---

## What is Agent Mode?

Agent Mode is **full execution** mode. The agent can:

- Read and search files
- Create new files
- Edit existing files
- Run terminal commands
- Install dependencies
- Run tests
- Make commits (if you allow it)

This is the mode where code is actually written and changes happen.

---

## When to use Agent Mode

| Situation                           | Example                                              |
| ----------------------------------- | ---------------------------------------------------- |
| **Implement a plan**                | You already researched and planned — time to execute |
| **Simple, direct tasks**            | Rename a variable, fix a typo, add a field           |
| **Execute with clear instructions** | You know exactly what you want and can describe it   |
| **Generate boilerplate**            | Create a component following an existing pattern     |

---

## When NOT to use Agent Mode (directly)

| Situation                                    | Recommended mode |
| -------------------------------------------- | ---------------- |
| You do not understand the problem            | Ask Mode first   |
| The task is complex and ambiguous            | Plan Mode first  |
| You want to explore options                  | Ask or Plan Mode |
| You do not know which files will be affected | Ask Mode first   |

**Golden rule:** If you cannot explain to a coworker what needs to be done, you are not ready for Agent Mode.

---

## How it works in practice

### 1. The agent acts on its own

Unlike Plan Mode, here the agent **executes** without asking permission at every step. It will:

1. Analyze what you asked
2. Decide which files to read
3. Make changes
4. Run commands if needed
5. Show you the result

### 2. You review afterward

Cursor shows a **diff** (before/after) for each changed file. You can:

- **Accept** the change
- **Reject** the change
- **Request adjustments** with a new prompt

---

## Example prompts for Agent Mode

### Simple, direct task

```
Add a "phone" field to the registration form.
Follow the same pattern as existing fields.
The field should be required and accept only digits.
```

### Implement from a plan

```
Implement the plan described in @plans/pagination.md

Follow the steps in order. After each step, show me
what changed before continuing.
```

### Fix a specific bug

```
The "Save" button in @src/components/UserForm.vue
does not disable while the form is submitting.

Fix this by adding a loading state that:
- Disables the button during submit
- Shows "Saving..." on the button
- Re-enables the button after the response (success or error)
```

### Generate code following an existing pattern

```
Create a new composable useCategories following the same pattern as
@src/composables/useProducts.ts

It should fetch categories from /api/categories and return:
- categories (list)
- isLoading
- error
- fetchCategories()
```

---

## Reviewing the agent’s work

After the agent makes changes, treat it like a **junior’s code review**:

### Review checklist

- Does the code do what was asked?
- Does it follow project patterns?
- Any unexpected side effects?
- Are variable and function names clear?
- No unnecessary dependencies?
- Do tests pass?

### Use Git as an ally

```
# See what changed before committing
git diff

# If something is wrong, revert
git checkout -- file-with-issue.ts

# Commit step by step, not everything at once
git add correct-file.ts
git commit -m "feat: add phone field to registration"
```

Frequent commits let you revert specific changes without losing everything.

---

## Autonomy controls

You can configure what the agent may do automatically in Cursor:

| Action           | Beginner recommendation  |
| ---------------- | ------------------------ |
| Read files       | Allow                    |
| Write files      | Allow (you review after) |
| Run commands     | Review case by case      |
| Install packages | Approve manually         |
| Make commits     | Approve manually         |

Start conservative and loosen as you gain confidence.

---

## Good practices in Agent Mode

1. **Give clear instructions** — the more specific, the better the result
2. **Reference files** — use `@` to point exactly where the agent should work
3. **Ask for step-by-step** — _“do one step at a time and show me before continuing”_
4. **Review everything** — never accept changes without reading the diff
5. **Commit often** — small commits are easier to revert
6. **New session for new tasks** — do not reuse long sessions

---

## Common mistakes in Agent Mode

| Mistake                      | What happens                           | How to avoid         |
| ---------------------------- | -------------------------------------- | -------------------- |
| Vague prompt                 | Agent assumes and generates wrong code | Be specific          |
| Not reading the diff         | Bugs slip to production                | Always read the diff |
| Session too long             | Quality degrades                       | New session per task |
| Accepting everything at once | Hard to revert if wrong                | Commit in chunks     |
| Not referencing files        | Agent may touch wrong files            | Always use `@`       |

---

## Agent Mode + Git = safer workflow

```
1. Agent makes changes
         ↓
2. You review the diff (git diff)
         ↓
3. Accept? → git add + commit with a clear message
   Reject? → git checkout -- file.ts
         ↓
4. Next step of the plan
         ↓
5. Repeat until done
```

Think of Git as your **first code review** before the PR goes to the team.

---

## Summary

| Aspect             | Detail                                      |
| ------------------ | ------------------------------------------- |
| **Capability**     | Read, write, execute — everything           |
| **When to use**    | Clear tasks, after research/planning        |
| **Goal**           | Implement changes in code                   |
| **Outcome**        | Code ready for commit and review            |
| **Common mistake** | Using it without researching/planning first |

---

> **Next:** [03 — Rules](../03-regras/01-o-que-sao-regras.md) — teach the agent your project’s standards
