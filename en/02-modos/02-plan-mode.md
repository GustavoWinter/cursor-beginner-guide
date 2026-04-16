# Plan Mode — plan before implementing

> Plan Mode is Cursor’s “architect.”
> It reads, analyzes, proposes — but only executes when you approve.

---

## What is Plan Mode?

Plan Mode is a **collaborative planning** mode. The agent can:

- Read project files
- Search the codebase
- Propose detailed changes
- Suggest step-by-step plans

The agent **does not execute** automatically. It asks for your approval before each action.

Difference from Ask Mode: here the agent goes beyond explaining — it **designs the solution**.

---

## How Ask, Plan, and Agent differ

| Aspect           | Ask Mode | Plan Mode     | Agent Mode    |
| ---------------- | -------- | ------------- | ------------- |
| Reads files      | Yes      | Yes           | Yes           |
| Explains         | Yes      | Yes           | Yes           |
| Proposes changes | No       | Yes           | Yes           |
| Executes changes | No       | With approval | Automatically |
| Runs commands    | No       | No            | Yes           |

**Plan Mode is the middle ground:** it thinks and proposes, but waits for you to say “go.”

---

## When to use Plan Mode

| Situation                | Why Plan Mode                                     |
| ------------------------ | ------------------------------------------------- |
| Medium/large new feature | You want to see the plan before code is generated |
| Refactor                 | You need to understand impact before changing     |
| Multiple files involved  | You want a clear order of changes                 |
| Architectural decision   | You need to compare approaches                    |
| Risky task               | You want to validate strategy before executing    |

---

## How to enable Plan Mode

In the chat mode selector, choose **“Plan.”** The agent will adopt planning behavior automatically.

---

## Example prompts for Plan Mode

### Plan a feature

```
I need to add pagination to the product listing.

Create a detailed plan with:
1. Which files will be created or changed
2. Implementation order
3. How we will test each step
4. What will not be changed
```

### Plan a refactor

```
The ProductCard component is 400 lines and does too much.

Propose a refactor plan that:
- Splits it into smaller components
- Keeps current behavior
- Is incremental (nothing breaks mid-way)
```

### Compare approaches

```
I need to implement API caching in this project.
What approaches would make sense here?

Compare:
- Cache in a composable
- Cache with a Pinia store
- Cache with a service worker

Consider what the project already uses and recommend one approach.
```

### Plan a bugfix

```
The date filter fails when the user selects
the same day as start and end.

Plan the fix:
1. Where the problem is (root cause)
2. What needs to change
3. Which tests to add to prevent regression
```

---

## Output of a good plan

A solid Plan Mode plan should include:

### Expected structure

```markdown
## Plan: [task name]

### Files involved

- `src/components/ProductList.vue` — add pagination controls
- `src/composables/useProducts.ts` — add pagination params
- `src/api/products.ts` — update API call

### Steps

1. Update `useProducts.ts` to accept `page` and `pageSize`
2. Modify the API call in `products.ts`
3. Add pagination UI in `ProductList.vue`
4. Add tests for the composable
5. Manually test navigation between pages

### Verification

- [ ] Unit tests passing
- [ ] Pagination works with 0, 1, and many results
- [ ] URL reflects current page

### Out of scope

- Do not change the visual design of the listing
- Do not implement infinite scroll (future phase)
```

---

## From plan to implementation

After you approve the plan:

1. **Save the plan** — e.g. `plans/task-name.md` or copy the content
2. **Open a new session** in Agent Mode
3. **Provide the plan** as initial context
4. **Implement step by step** following the plan order

That gives you:

- Clean context during implementation
- Clear steps for the agent
- Easier review (you know what to expect)

---

## Good practices in Plan Mode

1. **Ask for explicit scope** — always ask what is in and out of scope
2. **Ask for verification** — include how to know each step succeeded
3. **Review critically** — a plan is only as good as your review. Read before approving
4. **Iterate on the plan** — if something is unclear, ask for detail before implementing
5. **Do not skip steps** — if the plan has five steps, do not ask for all of them at once

---

## Common mistakes in Plan Mode

| Mistake                   | Consequence                                   | Fix                          |
| ------------------------- | --------------------------------------------- | ---------------------------- |
| Approving without reading | Agent implements the wrong thing              | Always read and validate     |
| Plan too vague            | Agent makes assumptions during implementation | Ask for more detail          |
| Plan too large            | Hard to implement and review                  | Split into smaller plans     |
| No scope defined          | Agent does more than it should                | Always define “out of scope” |

---

## Summary

| Aspect             | Detail                                                       |
| ------------------ | ------------------------------------------------------------ |
| **Capability**     | Read, analyze, propose (does not run on its own)             |
| **When to use**    | Medium/large tasks, refactors, decisions                     |
| **Goal**           | Have a clear plan before writing code                        |
| **Outcome**        | Step-by-step plan document                                   |
| **Common mistake** | Approving without reading or skipping straight to Agent Mode |

---

> **Next:** [03 — Agent Mode](./03-agent-mode.md) — executing changes with the agent
